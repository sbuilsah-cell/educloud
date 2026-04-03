# EduCloud Platform

EduCloud is being converted from the static prototype into a real full-stack school SaaS.

## Deployment

Canonical production path:

1. Copy [deploy.env.example](deploy.env.example) to `/opt/educloud/deploy.env` on the Droplet.
2. Set `DOMAIN`, `ADMIN_EMAIL`, `REPO_URL`, `STRIPE_SECRET_KEY`, and `RAZORPAY_KEY_ID`.
3. Run [scripts/deploy-digitalocean.sh](scripts/deploy-digitalocean.sh) as root.

See [docs/deployment.md](docs/deployment.md) for firewall, Caddy, and smoke-test details.

## Current structure

- `apps/web` - Next.js 14 app router frontend
- `apps/api` - NestJS API with domain modules and tenant context middleware
- `packages/shared` - shared TypeScript contracts
- `prisma/schema.prisma` - multi-tenant data model
- `docker-compose.yml` - local PostgreSQL and Redis services

## What is in place

- Tenant-aware dashboard shell
- Admissions, academics, finance, control plane, compliance, API, and roadmap sections
- NestJS resource modules for tenants, admissions, academics, finance, notifications, control plane, and compliance
- Prisma schema for tenants, schools, users, students, applications, attendance, invoices, notifications, audit logs, and feature flags
- Shared types for dashboard and tenant summaries

## Run locally

1. Copy `.env.example` to `.env`.
2. Set `EDUCLOUD_SERVICE_SECRET` to the same strong value for the web app and API so only the web server can establish request context.
3. Start PostgreSQL and Redis with `docker compose up -d`.
4. Install dependencies with `npm install`.
5. Apply the SQL migration and seed data with `npm run db:setup`.
6. Run the web app with `npm run dev:web`.
7. Run the API with `npm run dev:api`.
8. Generate Prisma client only if the Windows Prisma engine issue is resolved.

## Notes

- The current environment does not have Node.js or the .NET SDK installed, so the project cannot be executed or built here yet.
- The repository now contains the source structure needed for a proper Next.js + NestJS + Prisma implementation once dependencies are installed.
