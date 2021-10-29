# Cross-Dataset Rules

{% hint style="danger" %}
**Best practice for cross-table joins is to define a view and scan the view.  **

****

**Only in circumstances when a view cannot be created should you define cross-table joins with 2 separate datasets (DQ Jobs) and express the join in the rule. **

****

**If you're doing multiple lookups this will improve long-term performance and consolidate maintenance. **
{% endhint %}

{% hint style="warning" %}
Cross-dataset rules require -libsrc or -addlib (prior to 2021.11)&#x20;
{% endhint %}

![When a cross-dataset rule uses two connections, be sure the jars are in the -lib or -addlib directory.](<../../../../../.gitbook/assets/image (100).png>)

## In-Clause (Single Column)

```sql
select * from @table1 where id 
not in ( select id from @table2 )
```

## Except (Multi-Column)&#x20;

```sql
select id, app_id, email, guid_num from @table1
EXCEPT
select id, app_id, email, guid_num from @table2
```

## Join Example

```sql
SELECT
    *
FROM
    @table1 A
    LEFT JOIN @table2 B ON A.id = B.id
where
    B.id is null OR (A.email != B.email)
```

## Cross-Table (Guided).  Use our wizard to do ad-hoc analysis and visual setup.

{% embed url="https://www.youtube.com/watch?v=uQ0tilvBUKc" %}

## Join Example Example (vs. cross-table guided seen above).

{% embed url="https://www.youtube.com/watch?v=BFw5ZIzwewQ" %}

## Multi-part condition rules with the rule builder.  Combines profiling metrics & builder in one screen.

{% embed url="https://www.youtube.com/watch?v=Zkw23umvf8o&feature=youtu.be&t=16" %}

## Sample Results

![](<../../../../../.gitbook/assets/image (55).png>)
