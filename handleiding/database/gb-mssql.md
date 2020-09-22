---
sort: 5
---

# Grote Berichten MSSQL Scripts

```sql
create table gb_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         DATETIME      NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  content_type      VARCHAR(256)  NOT NULL,
  url               VARCHAR(256)  NOT NULL,
  max_file_size     BIGINT        NOT NULL,
  compression       TINYINT       NOT NULL DEFAULT 0,
  data_reference    TEXT          NULL,
  status            TINYINT       NOT NULL DEFAULT 0,
  status_time       DATETIME      NOT NULL DEFAULT GETDATE(),
  status_message    TEXT          NULL
);

create table gb_file
(
  gb_transaction_id VARCHAR(256)  NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            TINYINT       NOT NULL DEFAULT 0,
  FOREIGN KEY (gb_transaction_id) REFERENCES gb_transaction(id)
);
```
