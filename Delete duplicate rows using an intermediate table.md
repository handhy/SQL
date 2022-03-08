Step 1. Create a new table whose structure is the same as the original table:
```
CREATE TABLE source_copy LIKE source;
```

Step 2. Insert distinct rows from the original table to the new table:
```
INSERT INTO source_copy
SELECT * FROM source
GROUP BY col; -- column that has duplicate values
```

Step 3. drop the original table and rename the immediate table to the original one
```
DROP TABLE source;
ALTER TABLE source_copy RENAME TO source;
```

For example, the following statements delete rows with duplicate emails from the contacts table:
```
-- step 1
CREATE TABLE contacts_temp 
LIKE contacts;

-- step 2
INSERT INTO contacts_temp
SELECT * 
FROM contacts 
GROUP BY email;


-- step 3
DROP TABLE contacts;

ALTER TABLE contacts_temp 
RENAME TO contacts;
```
