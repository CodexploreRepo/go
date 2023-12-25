# Database Design

## DB Diagram

- [DB Diagram IO](https://dbdiagram.io/) to draw the tables via DBML

````sql
// Use DBML to define your database structure
// Docs: https://dbml.dbdiagram.io/docs

Table account as A {
  // id integer [primary key, increment] // auto-increment
  id bigserial [pk] // bigserial ~ integer & auto-increment
  owner varchar [not null]
  balance bigint [not null]
  currency varchar [not null]
  created_at timestamptz [not null, default: `now()`] // tz: select timezone

  Indexes {
    owner
  }
}

Table entries {
  // this table to record all the changes in account table
  id bigserial [pk]
  account_id bigint [ref: > A.id, not null] // inline relationship
  amount bigint  [not null, note: 'can be positive or negative']
  created_at timestamptz [not null, default: `now()`]
  Indexes {
    account_id
  }
}

Table transfers {
  id bigserial [pk]
  from_account_id bigint [ref: > A.id, not null] // inline relationship
  to_account_id bigint [ref: > A.id, not null]
  amount bigint [not null, note: 'must be positive']//
  created_at timestamptz [not null, default: `now()`]
  Indexes {
    from_account_id
    to_account_id
    (from_account_id, to_account_id) // composite indexes
  }
}
```sql
- After the schema diagram is define, we can export into Postgres or MySQL commands

````

CREATE TABLE "account" (
"id" bigserial PRIMARY KEY,
"owner" varchar NOT NULL,
"balance" bigint NOT NULL,
"currency" varchar NOT NULL,
"created_at" timestamptz NOT NULL DEFAULT (now())
);

CREATE TABLE "entries" (
"id" bigserial PRIMARY KEY,
"account_id" bigint NOT NULL,
"amount" bigint NOT NULL,
"created_at" timestamptz NOT NULL DEFAULT (now())
);

CREATE TABLE "transfers" (
"id" bigserial PRIMARY KEY,
"from_account_id" bigint NOT NULL,
"to_account_id" bigint NOT NULL,
"amount" bigint NOT NULL,
"created_at" timestamptz NOT NULL DEFAULT (now())
);

CREATE INDEX ON "account" ("owner");

CREATE INDEX ON "entries" ("account_id");

CREATE INDEX ON "transfers" ("from_account_id");

CREATE INDEX ON "transfers" ("to_account_id");

CREATE INDEX ON "transfers" ("from_account_id", "to_account_id");

COMMENT ON COLUMN "entries"."amount" IS 'can be positive or negative';

COMMENT ON COLUMN "transfers"."amount" IS 'must be positive';

ALTER TABLE "entries" ADD FOREIGN KEY ("account_id") REFERENCES "account" ("id");

ALTER TABLE "transfers" ADD FOREIGN KEY ("from_account_id") REFERENCES "account" ("id");

ALTER TABLE "transfers" ADD FOREIGN KEY ("to_account_id") REFERENCES "account" ("id");

```
## Table Plus

- Delete Tables: Right Click on Table Name & Delete with Cascade option (to remove the links using Foreign Key)
  - Press `CMD + S` to completely remove the table
```
