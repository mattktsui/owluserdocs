---
description: Promoting and moving datasets across environments
---

# Export and Import API

## Pre-requirements

{% hint style="warning" %}
The database needs the [stored procedure](export-and-import-api.md#stored-procedure) (function) defined in order to use the Export/Import API.&#x20;
{% endhint %}

### V2 - Stable - available from 2022.02 release

#### Step 1 - Export content from source schema

{% swagger method="get" path="/db-export" baseUrl="https://<collibra-dq-url>/v2" summary="Export tables from database" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="datasets" required="true" type="List of strings" %}
List of datasets to export. You need to give at least one 

**valid**

 dataset name into the list
{% endswagger-parameter %}

{% swagger-parameter in="query" name="schema" type="String" %}
Name of the schema/tenant where you want to perform the export.

\




_Default value: **public**_
{% endswagger-parameter %}

{% swagger-parameter in="query" type="String" name="tables" %}
List of tables to export on the given schema & dataset(s).

\


If you leave it empty, the following tables will be exported altogether: 

_**rule_repo, owl_catalog, owl_rule, alert_cond, owl_check_repo, job_schedule, alert_output**_
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List of SQL - INSERT statements as JSON list" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Any error happened with error message" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

#### Step 1 - Import content

{% swagger method="post" path="/db-import" baseUrl="https://<collibra-dq-url>/v2" summary="Import content into the target tenant" %}
{% swagger-description %}
The target schema/tenant name will be part of the input SQL INSERT statements.

The import is rung on non-transactional mode, any error happens in the middle, the saved items will be left in the database as is.
{% endswagger-description %}

{% swagger-parameter in="body" type="" required="true" %}
List of SQL INSERT which will be imported into the target Collibra DQ metastore

Format: JSON string list
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="When the import was successful" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Any error happened with error message" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}



### V1 - This API is going to be deprecated soon

#### Step 1 - Get-Exports

Best practice is to use the get-exports endpoint for most scenarios.  You can pass in several dataset names and several tables at once. This endpoint will create a JSON payload

{% hint style="info" %}
Exports and Imports are currently limited to the 3 tables listed below.
{% endhint %}

**These are the three most common tables. These are the supported tables for re-promotion (running the export multiple times).  The most common use case is to copy jobs and rules from environment A to environment B.  Running the export/import sequence on the same environment likely result in a key constraint conflict, unless in-between edits are made to the insert payload.**

* owl\_rule
* job\_schedule
* owl\_check\_repo

```
http://<url>/v2/get-exports?dataset=public.dataset_scan_2,public.dataset_scan_1&schema=public&tables=owl_rule,job_schedule,owl_check_repo
```

#### Use Swagger to build this for you

This is located under controller-scala (internal API)

![](<../../.gitbook/assets/image (133).png>)

#### Click Try it out to input the details

![](<../../.gitbook/assets/image (58).png>)

#### Step 2 - Run-Import

{% hint style="info" %}
You will want to perform a find/replace on the import payload to check for differences in connections, agents, spark and environment configurations.  Migrating to different environments typically requires the payload to be modified.
{% endhint %}

Run import on the desired environment, passing the output of the previous statement to the body of the request&#x20;

```javascript
http://<url>/v2/run-import
```

#### Use Swagger to try it out&#x20;

This is under controller-catalog

![](<../../.gitbook/assets/image (125).png>)

![](<../../.gitbook/assets/image (115).png>)

This would be the body of the POST.

![](<../../.gitbook/assets/Screen Shot 2021-04-26 at 10.13.18 AM.png>)

## Requirement - Stored Procedure

The following function needs to be created in the Collibra DQ metastore, before this can run.&#x20;

```
CREATE OR REPLACE FUNCTION public.dump(p_schema text, p_table text, p_where text)
 RETURNS SETOF text
 LANGUAGE plpgsql
AS $function$
 DECLARE
     dumpquery_0 text;
     dumpquery_1 text;
     selquery text;
     selvalue text;
     valrec record;
     colrec record;
 BEGIN

     -- ------ --
     -- GLOBAL --
     --   build base INSERT
     --   build SELECT array[ ... ]
     dumpquery_0 := 'INSERT INTO ' ||  quote_ident(p_schema) || '.' || quote_ident(p_table) || '(';
     selquery    := 'SELECT array[';

     <<label0>>
     FOR colrec IN SELECT table_schema, table_name, column_name, data_type
                   FROM information_schema.columns
                   WHERE table_name = p_table and table_schema = p_schema
                   ORDER BY ordinal_position
     LOOP
         dumpquery_0 := dumpquery_0 || quote_ident(colrec.column_name) || ',';
         selquery    := selquery    || 'CAST(' || quote_ident(colrec.column_name) || ' AS TEXT),';
     END LOOP label0;

     dumpquery_0 := substring(dumpquery_0 ,1,length(dumpquery_0)-1) || ')';
     dumpquery_0 := dumpquery_0 || ' VALUES (';
     selquery    := substring(selquery    ,1,length(selquery)-1)    || '] AS MYARRAY';
     selquery    := selquery    || ' FROM ' ||quote_ident(p_schema)||'.'||quote_ident(p_table);
     selquery    := selquery    || ' WHERE '||p_where;
     -- GLOBAL --
     -- ------ --

     -- ----------- --
     -- SELECT LOOP --
     --   execute SELECT built and loop on each row
     <<label1>>
     FOR valrec IN  EXECUTE  selquery
     LOOP
         dumpquery_1 := '';
         IF not found THEN
             EXIT ;
         END IF;

         -- ----------- --
         -- LOOP ARRAY (EACH FIELDS) --
         <<label2>>
         FOREACH selvalue in ARRAY valrec.MYARRAY
         LOOP
             IF selvalue IS NULL
             THEN selvalue := 'NULL';
             ELSE selvalue := quote_literal(selvalue);
             END IF;
             dumpquery_1 := dumpquery_1 || selvalue || ',';
         END LOOP label2;
         dumpquery_1 := substring(dumpquery_1 ,1,length(dumpquery_1)-1) || ');';
         -- LOOP ARRAY (EACH FIELD) --
         -- ----------- --

         -- debug: RETURN NEXT dumpquery_0 || dumpquery_1 || ' --' || selquery;
         -- debug: RETURN NEXT selquery;
         RETURN NEXT dumpquery_0 || dumpquery_1;

     END LOOP label1 ;
     -- SELECT LOOP --
     -- ----------- --

 RETURN ;
 END
 $function$
;
```

This assignment needs added.

```
alter function dump(text, text, text) owner to <ownername>;
```

