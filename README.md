# sg4a-fe-shared-translations

Centralized translation resources for SmartGrid4All microfrontend modules.

## Overview

This folder stores module-scoped locale dictionaries as JSON files.

- Each top-level module folder (for example: `blueprint`, `container`, `userprofile`, `worldtimeclock`) contains one file per locale.
- Locale files are plain JSON key-value maps used by consuming frontend applications.

## Tech Stack

- JSON translation assets
- GitHub Actions workflows for deployment orchestration
- Azure Storage containers as deployment targets

## Repository Structure

- `.github/workflows/`:
	- `deploy_azure_storage.yml` for non-production deployment orchestration
	- `deploy_release_azure_storage.yml` for production release deployment orchestration
- Module folders such as `blueprint/`, `container/`, `servicelinks/`, `userprofile/`, `worldtimeclock/` with locale JSON files

## Build and Deploy

This folder does not contain a local build pipeline or package scripts.

Deployment is handled by GitHub Actions workflows that call reusable workflows from `SmartConnectSolutions/.github`:

- Non-production: manual trigger (`workflow_dispatch`) deploys to `dev-translations` and `test-translations` containers.
- Production: release publish trigger deploys to `prod-translations` container.

## GitHub Actions

- Dev/Test deployment behavior: manual dispatch runs non-production deployment via reusable workflow.
- Prod deployment behavior: publishing a GitHub Release triggers production deployment.
- Quality scan behavior: no repository-local quality scan workflow is defined in `.github/workflows`.
- Secrets note: workflows use `secrets: inherit`, so required secrets must exist in the calling repository/organization context.

## Troubleshooting

- If deployment does not start for dev/test, confirm the workflow was manually dispatched.
- If production deployment does not start, confirm a release was published (not just a tag push).
- If deployment fails at runtime, verify required inherited secrets are available to the workflow.
