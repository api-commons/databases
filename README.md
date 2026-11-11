# Databases

The common managed-database vocabulary -- database clusters and instances, the databases inside them, their users, and their backups -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Database, Databases, SQL, PostgreSQL, MySQL, NoSQL, Database as a Service, MongoDB, Redis in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| database_cluster | 33 | 30 | id 63%, name 57%, status 57% | clusters 17, cluster 10, branches 7, instances 3 |
| database | 48 | 47 | name 68%, id 51% | databases 34, database 13, db 4, dbs 1 |
| database_user | 11 | 11 | username 100%, password 73%, created_at 55% | users 8, roles 3 |
| backup | 32 | 31 | id 77%, status 64% | backups 24, backup 7, snapshots 6 |

Cohort: 184 providers with harvested OpenAPI, 73 crosswalks. Of the providers exposing a database_cluster: 58% create, 91% list, 61% fetch, 39% update, 58% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Managed databases agree on little beyond identity: clusters on id, name and status, databases on name and id, backups on id and status. The engine reaches only 30% of clusters, because most providers serve one engine and never say which.
- Database users agree on username and password -- every provider returns the password at creation -- with created_at at 55%.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- database_cluster covers clusters, instances, deployments and serverless projects: the provisioned unit that holds databases.
- Neon-style branches count as clusters for now; revisit if branching spreads beyond a few providers.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
