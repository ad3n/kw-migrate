# KW-Migrate

Manage postgresql cluster migration easly

## Requirements

- Go 1.17 or above

- `pg_dump` (optional) to support reverse migration

## Features

- Support multiple connections and schemas

- Reverse migration from existing database

## Install

- Download latest release `https://github.com/suryakoinworks/kw-migrate/tags`

- Extract source

- Download dependencies `cd kw-migrate && go get && go mod tidy`

- Build `go build -o kw-migrate`

- Move to bin or add to environment variables

- Check using `kw-migrate --help`

## Commands available

- `kw-migrate create <name>` to create new migration file

- `kw-migrate up [--all-connection=true] [--all-schema=true] <db> <schema>` to deploy migration(s) from database and schema which you provide

- `kw-migrate down [--all-connection=true] [--all-schema=true] <db> <schema>` to drop migration(s) from database and schema which you provide

- `kw-migrate generate <schema>` to reverse migration from your `source` database 

- `kw-migrate rollback <db> <schema> <step>` to rollback migration version from database and schema which you provide

Run `kw-migrate --help` for complete commands

## Usage

- Create new project folder

- Copy Kwfile.yml below

```yaml
version: 1.0

migrate:
    pg_dump: /usr/bin/pg_dump
    folder: migrations
    source: default
    clusters:
        local: [local]
    connections:
        default:
            host: default
            port: 5432
            name: database
            user: user
            password: s3cret
        local:
            host: localhost
            port: 5432
            name: database
            user: user
            password: s3cret
    schemas:
        public:
            excludes:
                - exclude_tables
            with_data:
                - data_included_tables
        user:
            excludes:
                - exclude_tables
            with_data:
                - data_included_tables
```

- Create new migration or generate from `source`

## Limitation

- `kw-migrate generate` command run use `--schema-only` option as default (except when data included), so many of features like UDT, functions, etc may not imported by it self
