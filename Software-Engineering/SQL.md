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
- Must include `GROUP BY` column(s) in `SELECT` clause for it to work, in this case `COUNT()`
- If you include a column not in `GROUP BY` in `SELECT`, must do some form of aggregation on the values in that column.
	- Common functions: `SUM`, `AVG`, `MIN`, `MAX`

```SQL
SELECT
  member_type, COUNT(*)
FROM
  trip_data
GROUP BY
  member_type
ORDER BY
  COUNT(*) DESC
LIMIT
  10
```

Output is one col of the values in `member_type`, other is the count of how many times they occurred.  

## Joining
Joining data from two tables together by some common column (in most cases)

*Matching start_station from trip_data with station_id from bikeshare_stations, this value exists in both*
```SQL
SELECT
  *
FROM
  trip_data, bikeshare_stations
WHERE
  start_station = station_id
LIMIT
  10
```

Sometimes the comma between the table names is replaces by `JOIN` and `WHERE` -> `ON`

```SQL
SELECT
  COUNT(*)
FROM
  trip_data JOIN bikeshare_stations ON start_station = station_id
```