---
tags:
  - "#lecture-notes"
src-date: 2024-09-23
src-author:
  - Gustavo Arredondo
src-link: Databases I
---
# Databases I - Session 6

## `JOIN`

### `INNER JOIN`

> Show first name, last name, and the **full** province name of each patient.  
> Example: 'Ontario' instead of 'ON'

```sql
SELECT first_name, last_name, province_name
FROM patients pa
JOIN province_names pr ON pa.province_id = pr.province_id
```

### `LEFT JOIN`



### `RIGHT JOIN`



### `FULL JOIN`


## `MERGE`



