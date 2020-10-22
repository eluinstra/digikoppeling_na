---
sort: 9
---

# Grote Berichten Console MSSQL Scripts

```sql
create table file_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         DATETIME      NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            TINYINT       NOT NULL,
  status_time       DATETIME      NOT NULL,
  status_message    TEXT          NULL,
  processed         TINYINT       NOT NULL
);
```
