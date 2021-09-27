# SQL
#📥 
%%
#topic
#coding 
%%
**Related:**
-  [[Relational Databases]]

---

: Structured Query Language

*Selects just member_type, start_date, duration columns*
```SQL
SELECT
	member_type, start_date, duariotn
FROM 
	trip_data
LIMIT 
	10
```

*Lists the names of your tables and all of their columns and types (only works in SQLITE)*
```SQL
select name, sql from sqlite_master
```

## Filtering
Filtering by certain rows in a table.
- You can add `AND` to add more filter conditions
```SQL
SELECT
  member_type, start_date, duration
FROM
  trip_data
WHERE
  duration >= 3600
AND
  member_type = "Member"
LIMIT
  10
```

## Sorting
Add `ORDER BY` to sort. 
- `DESC` keyword specifies you want descending sort order, default is ascending
- Has to come after `WHERE` if you want both
```SQL
SELECT
  member_type, start_date, duration
FROM
  trip_data
ORDER BY
  duration DESC
LIMIT
  10
```

## Aggregation / Group By
Allows one to create summary information by grouping rows together. 

