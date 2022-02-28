# Export and Import Example

{% hint style="info" %}
Best practice is to use get-exports and the owl\_rule table post 2021.09 release. Please refer to the [Export and Import API](export-and-import-api.md) page for more details.
{% endhint %}

### Steps

1. Find your dataset&#x20;
2. Pass your table to the following api call - [http://\<url>/v2/get-rules-export?dataset=public.transit\_6](http://localhost:9000/v2/get-export?dataset=public.transit\_6)
3. Run import on the desired environment, passing the output of the previous statement to the body of the request - [http://\<url>/v2/run-import](http://35.202.14.58/v2/run-import)

{% embed url="https://youtu.be/puXZwKi-CmM" %}

The following function needs to be declared in the postgres metastore before this can run.&#x20;

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

## From Swagger

Navigate to the API page

&#x20;

![](<../../.gitbook/assets/image (47).png>)

Find the Rest APIs link

![](<../../.gitbook/assets/image (59).png>)

Drill-in to the controller-scala section

![](<../../.gitbook/assets/image (49).png>)

Find the get-rules-export call

![](<../../.gitbook/assets/image (50).png>)

Click Try it out and enter a dataset name, Execute to run the call

![](<../../.gitbook/assets/image (52).png>)

Copy the response body&#x20;

![](<../../.gitbook/assets/image (53).png>)

Navigate to the controller-catalog section

![](<../../.gitbook/assets/image (54).png>)

Find run-import and Try it out&#x20;

![](<../../.gitbook/assets/image (55).png>)

Make any edits and paste in the response body from the previous step&#x20;

![](<../../.gitbook/assets/image (56).png>)

Visually validate the rules were transferred to another dataset successfully

![](<../../.gitbook/assets/image (57).png>)
