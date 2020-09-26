---
sort: 10
---

# Grote Berichten Console MySQL Scripts

```sql
create table file_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         TIMESTAMP     NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            TINYINT       NOT NULL,
  status_time       TIMESTAMP     NOT NULL,
  status_message    MEDIUMTEXT  NULL,
  processed         TINYINT       NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
