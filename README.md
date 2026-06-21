# nuq-postgres-docker

ARM64 rebuild of Firecrawl's `nuq-postgres` (Postgres 17 + `pg_cron` + the NUQ queue schema) for the
[Muffin](https://github.com/gururafiki/muffin) deployment on Oracle Cloud A1 (aarch64).

Upstream `ghcr.io/firecrawl/nuq-postgres` is published amd64-only, so it can't schedule on the ARM
node ("unsupported platform"), which also blocks `firecrawl-api`. The image is just
`postgres:17` + `postgresql-17-cron` + `nuq.sql`, all arm64-capable — the CI sparse-checks-out
`apps/nuq-postgres` from Firecrawl and builds it with `--platform linux/arm64`.

CI builds + pushes `ghcr.io/gururafiki/nuq-postgres-docker:latest` (native arm64 runner). Consumed
by `muffin-deployment` as the `firecrawl-postgres` service.
