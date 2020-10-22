---
sort: 7
---

# Grote Berichten Oracle Scripts

```sql
create table gb_transaction
(
  id                VARCHAR(256)  PRIMARY KEY,
  timestamp         TIMESTAMP     NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  content_type      VARCHAR(256)  NOT NULL,
  url               VARCHAR(256)  NOT NULL,
  max_file_size     NUMBER(19)    NOT NULL,
  compression       NUMBER(2)     DEFAULT 0 NOT NULL,
  data_reference    CLOB          NULL,
  status            NUMBER(2)     DEFAULT 0 NOT NULL,
  status_time       TIMESTAMP     DEFAULT SYSDATE NOT NULL,
  status_message    CLOB          NULL
);

create table gb_file
(
  gb_transaction_id VARCHAR(256)  NOT NULL,
  filename          VARCHAR(256)  NOT NULL,
  status            NUMBER(2)     DEFAULT 0 NOT NULL,
  FOREIGN KEY (gb_transaction_id) REFERENCES gb_transaction(id)
);
```
