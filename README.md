# Langfuse v4 on Railway

Source for the [Langfuse v4](https://langfuse.com) Railway template: open-source LLM
observability — tracing, evals, prompt management and cost analytics.

## What the template deploys

| Service | Source | Notes |
| --- | --- | --- |
| `langfuse-web` | `langfuse/langfuse:4` | The UI and ingestion API. Public domain, port 3000. |
| `langfuse-worker` | `langfuse/langfuse-worker:4` | Background ingestion and evals. Private only, port 3030. |
| `Postgres` | Railway database | Users, projects, prompts, config. |
| `clickhouse` | `clickhouse/clickhouse-server:26.3` | Trace and span storage. Volume at `/var/lib/clickhouse`. |
| `Redis` | Railway database | Queues, caching, rate limiting. |
| `Bucket` | Railway storage bucket | S3-compatible event, media and batch-export storage. |

## Why this layout

**ClickHouse binds IPv6.** Railway's private network is IPv6-only, and the stock
`clickhouse-server` image listens on `0.0.0.0` alone, so `langfuse-web` cannot reach
it. `clickhouse/railway-listen.xml` adds `::` to `listen_host`. Without it the web
service fails its ClickHouse migration on first boot.

**`CLICKHOUSE_CLUSTER_ENABLED=false`.** Langfuse defaults this to `true`, which makes
the migration issue `ON CLUSTER` statements that a single node rejects. This is the
most common reason a single-node Langfuse deploy never finishes migrating.

**A Railway bucket instead of MinIO.** Langfuse v4 requires S3 for event uploads.
Railway buckets are S3-compatible and cost nothing to run, so the template uses one
rather than a MinIO container that would need its own service and volume.

**Long health-check timeouts.** The first boot runs both the Postgres and the
ClickHouse migrations before the web service answers, which takes a few minutes.

## Layout

```
web/         Dockerfile + railway.toml for langfuse-web
worker/      Dockerfile + railway.toml for langfuse-worker
clickhouse/  Dockerfile, IPv6 listen config, railway.toml
```

Each directory is a service root in the template.

## Upstream

- [Langfuse docs](https://langfuse.com/docs)
- [Self-hosting configuration reference](https://langfuse.com/self-hosting/configuration)
- [langfuse/langfuse](https://github.com/langfuse/langfuse)
