---
sort: 12
---

# Grote Berichten Console Postgres Scripts

```sql
create table file_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         TIMESTAMP     NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            NUMERIC(2)    NOT NULL,
  status_time       TIMESTAMP     NOT NULL,
  status_message    TEXT          NULL,
  processed         SMALLINT      NOT NULL
);
```
