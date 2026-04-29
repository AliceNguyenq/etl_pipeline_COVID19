# AGENTS.md

This repository is a Docker-first Dagster ETL project. Keep agent changes small, local, and consistent with the existing pipeline structure.

## Where to look first

- Project overview and layout: [README.md](README.md)
- Dagster package workflow: [etl_pipeline/README.md](etl_pipeline/README.md)
- Build and runtime commands: [Makefile](Makefile)

## Working conventions

- Treat the Dagster assets under [etl_pipeline/etl_pipeline/assets](etl_pipeline/etl_pipeline/assets) as the main behavior surface.
- Treat the IO managers under [etl_pipeline/etl_pipeline/resources](etl_pipeline/etl_pipeline/resources) as the main integration surface for MySQL, PostgreSQL, MinIO, and Spark.
- Prefer minimal changes that preserve the existing bronze / silver / gold / warehouse layering.
- Link to the existing README files instead of copying their content into new instructions.

## Validation defaults

- Use `make up` and `make down` for the container stack.
- Use `pytest etl_pipeline_tests` for Python-side checks.
- Use `dagster dev` when you need to inspect the Dagster UI locally.

## Windows notes

- The `Makefile` sets `SHELL:=/bin/bash`, so `make` requires a bash-capable shell on Windows such as Git Bash, MSYS2, or WSL.
- Docker Compose is the primary execution path, so prefer running the repo through Docker Desktop with a Windows terminal that supports ConPTY.
- If a task depends on Windows terminal behavior, keep it compatible with bash-first workflows rather than adding Windows-only branching.

## When changing code

- Update tests alongside asset or resource changes when practical.
- Avoid broad refactors unless they are required for the requested behavior.
- Keep documentation updates in the existing README files unless a new instruction file is clearly needed.