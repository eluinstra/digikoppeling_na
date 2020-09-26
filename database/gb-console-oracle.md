---
sort: 11
---

# Grote Berichten Console Oracle Scripts

```sql
create table file_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         TIMESTAMP     NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            NUMBER(2)     NOT NULL,
  status_time       TIMESTAMP     NOT NULL,
  status_message    CLOB          NULL,
  processed         NUMBER(2)	    NOT NULL
);
```
