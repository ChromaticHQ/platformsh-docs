---
title: "PostgreSQL (Database service)"
weight: 9
sidebarTitle: "PostgreSQL"
---

PostgreSQL is a high-performance, standards-compliant relational SQL database.

See the [PostgreSQL documentation](https://www.postgresql.org/docs/9.6/index.html) for more information.

{{% frameworks %}}

- [Hibernate](../guides/hibernate/deploy.md#mysql)
- [Jakarta EE](../guides/jakarta/deploy.md#mysql)
- [Spring](../guides/spring/mysql.md)

{{% /frameworks %}}

## Supported versions

| **Grid** | **Dedicated** | **Dedicated Generation 3** |
|----------------------------------|---------------|---------------|
|  {{< image-versions image="postgresql" status="supported" environment="grid" >}} | {{< image-versions image="postgresql" status="supported" environment="dedicated" >}} | {{< image-versions image="postgresql" status="supported" environment="dedicated-gen-3" >}} |

{{< image-versions-legacy "postgresql" >}}

\* No High-Availability on Dedicated.

{{< note >}}
Upgrading to PostgreSQL 12 using the `postgis` extension is not currently supported. Attempting to upgrade with this extension enabled will result in a failed deployment that will require support intervention to fix.

See the [Upgrading to PostgreSQL 12 with `postgis`](#upgrading-to-postgresql-12-with-the-postgis-extension) section below for more details.
{{< /note >}}

{{% deprecated-versions %}}

| **Grid** | **Dedicated** |
|----------------------------------|---------------|
|  {{< image-versions image="postgresql" status="deprecated" environment="grid" >}} | {{< image-versions image="postgresql" status="deprecated" environment="dedicated" >}} |

## Relationship

The format exposed in the ``$PLATFORM_RELATIONSHIPS`` [environment variable](../development/variables/use-variables.md#use-platformsh-provided-variables):

{{< relationship "postgresql" >}}

## Usage example

{{% endpoint-description type="postgresql" php=true /%}}

{{< codetabs >}}

---
title=Go
file=static/files/fetch/examples/golang/postgresql
highlight=go
---

<--->

---
title=Java
file=static/files/fetch/examples/java/postgresql
highlight=java
---

<--->

---
title=Node.js
file=static/files/fetch/examples/nodejs/postgresql
highlight=js
---

<--->

---
title=PHP
file=static/files/fetch/examples/php/postgresql
highlight=php
---

<--->

---
title=Python
file=static/files/fetch/examples/python/postgresql
highlight=python
---

{{< /codetabs >}}

## Access the service directly

Access the service using the Platform CLI by running `platform sql`.

You can also access it from your app container via [SSH](../development/ssh/_index.md).
From your [relationship data](#relationship), you need: `username`, `host`, and `port`.
Then run the following command:

```bash
psql -U <USERNAME> -h <HOST> -p <PORT>
```

Using the values from the [example](#relationship), that would be:

```bash
psql -U main -h postgresql.internal -p 5432
```

## Exporting data

The easiest way to download all data in a PostgreSQL instance is with the Platform CLI. If you have a single SQL database, the following command will export all data using the `pg_dump` command to a local file:

```bash
platform db:dump
```

If you have multiple SQL databases it will prompt you which one to export. You can also specify one by relationship name explicitly:

```bash
platform db:dump --relationship database
```

By default the file will be uncompressed. If you want to compress it, use the `--gzip` (`-z`) option:

```bash
platform db:dump --gzip
```

You can use the `--stdout` option to pipe the result to another command. For example, if you want to create a bzip2-compressed file, you can run:

```bash
platform db:dump --stdout | bzip2 > dump.sql.bz2
```

## Importing data

Make sure that the imported file contains objects with cleared ownership and `IF EXISTS` clauses. For example, you can create a DB dump with following parameters:

```bash
pg_dump --no-owner --clean --if-exists
```

The easiest way to load data into a database is to pipe an SQL dump through the `platform sql` command, like so:

```bash
platform sql < my_database_backup.sql
```

That runs the database backup against the SQL database on Platform.sh.
That works for any SQL file, so the usual caveats about importing an SQL dump apply
(for example, it's best to run against an empty database).
As with exporting, you can also specify a specific environment to use and a specific database relationship to use, if there are multiple.

```bash
platform sql --relationship database -e <BRANCH_NAME> < my_database_backup.sql
```

{{< note >}}
Importing a database backup is a destructive operation. It will overwrite data already in your database.
Taking a backup or a database export before doing so is strongly recommended.
{{< /note >}}

## Multiple databases

If you are using version `10`, `11`, `12`, `13`, or later of this service,
it's possible to define multiple databases as well as multiple users with different permissions.
To do so requires defining multiple endpoints.
Under the `configuration` key of your service there are two additional keys:

* `databases`:  This is a YAML array listing the databases that should be created. If not specified, a single database named `main` will be created.
* `endpoints`: This is a nested YAML object defining different credentials. Each endpoint may have access to one or more schemas (databases), and may have different levels of permission for each. The valid permission levels are:
  * `ro`: Using this endpoint only `SELECT` queries are allowed.
  * `rw`: Using this endpoint `SELECT` queries as well as `INSERT`/`UPDATE`/`DELETE` queries are allowed.
  * `admin`: Using this endpoint all queries are allowed, including DDL queries (`CREATE TABLE`, `DROP TABLE`, etc.).

Consider the following illustrative example:

```yaml
dbpostgres:
    type: postgresql:13
    disk: 2048
    configuration:
        databases:
            - main
            - legacy
        endpoints:
            admin:
                privileges:
                    main: admin
                    legacy: admin
            reporter:
                default_database: main
                privileges:
                    main: ro
            importer:
                default_database: legacy
                privileges:
                    legacy: rw
```

This example creates a single PostgreSQL service named `dbpostgres`. The server will have two databases, `main` and `legacy` with three endpoints created.

* `admin`: has full access to both databases.
* `reporter`: has `SELECT` query access to the `main` database, but no access to `legacy`.
* `importer`: has `SELECT`/`INSERT`/`UPDATE`/`DELETE` access (but not DDL access) to the `legacy` database. It does not have access to `main`.

If a given endpoint has access to multiple databases you should also specify which will be listed by default in the relationships array. If one isn't specified, the `path` property of the relationship will be `null`. While that may be acceptable for an application that knows the name of the database it's connecting to, automated tools like the Platform.sh CLI will not be able to access the database on that relationship. For that reason, defining the `default_database` property is always recommended.

Once these endpoints are defined, you will need to expose them to your application as a relationship. Continuing with the above example, your `relationships` in `.platform.app.yaml` might look like:

```yaml
relationships:
    database: "dbpostgres:admin"
    reports: "dbpostgres:reporter"
    imports: "dbpostgres:importer"
```

Each database will be accessible to your application through the `database`, `reports`, and `imports` relationships. They'll be available in the `PLATFORM_RELATIONSHIPS` environment variable and all have the same structure documented above, but with different credentials. You can use those to connect to the appropriate database with the specified restrictions using whatever the SQL access tools are for your language and application.

A service configuration without the `configuration` block defined is equivalent to the following default values:

```yaml
configuration:
    databases:
        - main
    endpoints:
        postgresql:
          default_database: main
          privileges:
            main: admin
```

If you do not define `database` but `endpoints` are defined, then the single database `main` will be created with the following assumed configuration:

```yaml
configuration:
    databases:
        - main
    endpoints: <your configuration>
```

Alternatively, if you define multiple databases but no endpoints, a single user `main` will be created with `admin` access to each of your databases, equivalent to the configuration below:

```yaml
configuration:
    databases:
        - firstdb
        - seconddb
        - thirddb
    endpoints:
        main:
            firstdb: admin
            seconddb: admin
            thirddb: admin
```

## Service timezone

To change the timezone for the current session, run `SET TIME ZONE <timezone>;`.

## Extensions

Platform.sh supports a number of PostgreSQL extensions. To enable them, list them under the `configuration.extensions` key in your `services.yaml` file, like so:

```yaml
db:
    type: postgresql:12
    disk: 1025
    configuration:
        extensions:
            - pg_trgm
            - hstore
```

In this case you will have `pg_trgm` installed, providing functions to determine the similarity of text based on trigram matching, and `hstore` providing a key-value store.

### Available extensions

The following is the extensive list of supported extensions. Note that you cannot currently add custom
extensions not listed here.

* `address_standardizer` - Used to parse an address into constituent elements. Generally used to support geocoding address normalization step.
* `address_standardizer_data_us` - For standardizing addresses based on US dataset example
* `adminpack` - administrative functions for PostgreSQL
* `autoinc` - functions for auto-incrementing fields
* `bloom` - bloom access method - signature file based index (requires 9.6 or higher)
* `btree_gin` - support for indexing common data types in GIN
* `btree_gist` - support for indexing common data types in GiST
* `chkpass` - data type for auto-encrypted passwords
* `citext` - data type for case-insensitive character strings
* `cube` - data type for multidimensional cubes
* `dblink` - connect to other PostgreSQL databases from within a database
* `dict_int` - text search dictionary template for integers
* `dict_xsyn` - text search dictionary template for extended synonym processing
* `earthdistance` - calculate great-circle distances on the surface of the Earth
* `file_fdw` - foreign-data wrapper for flat file access
* `fuzzystrmatch` - determine similarities and distance between strings
* `hstore` - data type for storing sets of (key, value) pairs
* `insert_username` - functions for tracking who changed a table
* `intagg` - integer aggregator and enumerator (obsolete)
* `intarray` - functions, operators, and index support for 1-D arrays of integers
* `isn` - data types for international product numbering standards
* `lo` - Large Object maintenance
* `ltree` - data type for hierarchical tree-like structures
* `moddatetime` - functions for tracking last modification time
* `pageinspect` - inspect the contents of database pages at a low level
* `pg_buffercache` - examine the shared buffer cache
* `pg_freespacemap` - examine the free space map (FSM)
* `pg_prewarm` - prewarm relation data (requires 9.6 or higher)
* `pg_stat_statements` - track execution statistics of all SQL statements executed
* `pg_trgm` - text similarity measurement and index searching based on trigrams
* `pg_visibility` - examine the visibility map (VM) and page-level visibility info (requires 9.6 or higher)
* `pgcrypto` - cryptographic functions
* `pgrouting` - pgRouting Extension (requires 9.6 or higher)
* `pgrowlocks` - show row-level locking information
* `pgstattuple` - show tuple-level statistics
* `plpgsql` - PL/pgSQL procedural language
* `postgis` - PostGIS geometry, geography, and raster spatial types and functions
* `postgis_sfcgal` - PostGIS SFCGAL functions
* `postgis_tiger_geocoder` - PostGIS tiger geocoder and reverse geocoder
* `postgis_topology` - PostGIS topology spatial types and functions
* `postgres_fdw` - foreign-data wrapper for remote PostgreSQL servers
* `refint` - functions for implementing referential integrity (obsolete)
* `seg` - data type for representing line segments or floating-point intervals
* `sslinfo` - information about SSL certificates
* `tablefunc` - functions that manipulate whole tables, including `crosstab`
* `tcn` - Triggered change notifications
* `timetravel` - functions for implementing time travel
* `tsearch2` - compatibility package for pre-8.3 text search functions (obsolete, only available for 9.6 and 9.3)
* `tsm_system_rows` - TABLESAMPLE method which accepts number of rows as a limit (requires 9.6 or higher)
* `tsm_system_time` - TABLESAMPLE method which accepts time in milliseconds as a limit (requires 9.6 or higher)
* `unaccent` - text search dictionary that removes accents
* `uuid-ossp` - generate universally unique identifiers (UUIDs)
* `xml2` - XPath querying and XSLT

{{< note >}}
Upgrading to PostgreSQL 12 using the `postgis` extension is not currently supported. Attempting to upgrade with this extension enabled will result in a failed deployment that will require support intervention to fix.

See the [Upgrading to PostgreSQL 12 with `postgis`](#upgrading-to-postgresql-12-with-the-postgis-extension) section below for more details.
{{< /note >}}

## Notes

### Could not find driver

If you see this error: `Fatal error: Uncaught exception 'PDOException' with message 'could not find driver'`, this means you are missing the `pdo_pgsql` PHP extension. You need to enable it in your `.platform.app.yaml` (see above).

## Upgrading

PostgreSQL 10 and later include an upgrade utility that can convert databases from previous versions to version 10 or later. If you upgrade your service from a previous version of PostgreSQL to version 10 or above (by modifying the `services.yaml` file), it upgrades automatically.

The utility can't upgrade PostgreSQL 9 versions, so upgrades from PostgreSQL 9.3 to 9.6 are not supported. Upgrade straight to version 11 instead.

{{< note theme="warning" >}}

Make sure you first test your migration on a separate branch.
{{< /note >}}

{{< note theme="warning" >}}

Be sure to take a backup of your production environment **before** you merge this change.
{{< /note >}}

Downgrading is not supported. If you want, for whatever reason, to downgrade you should dump to SQL, remove the service, recreate the service, and import your dump.

### Upgrading to PostgreSQL 12 with the `postgis` extension

Upgrading to PostgreSQL 12 using the `postgis` extension is not currently supported. Attempting to upgrade with this extension enabled will result in a failed deployment that will require support intervention to fix.

If you need to upgrade, you should follow the same steps recommended for performing downgrades: dump the database, remove the service, recreate the service with PostgreSQL 12, and then import the dump to that service.
