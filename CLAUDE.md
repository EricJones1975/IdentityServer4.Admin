# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Skoruba.IdentityServer4.Admin — an administration UI, API, and Security Token Service (STS) for IdentityServer4 + ASP.NET Core Identity. Targets .NET 6. The upstream project is no longer maintained (superseded by skoruba/Duende.IdentityServer.Admin); this fork works on the `StokwareAdmin` branch.

## Commands

```sh
dotnet build Skoruba.IdentityServer4.Admin.sln     # build everything
dotnet test                                        # run all tests (xUnit)
dotnet test tests/Skoruba.IdentityServer4.Admin.UnitTests   # one test project
dotnet test --filter "FullyQualifiedName~ClientServiceTests"  # single test class/method

# Run an app (each is independently runnable; run all three for a working system)
dotnet run --project src/Skoruba.IdentityServer4.STS.Identity   # https://localhost:44310
dotnet run --project src/Skoruba.IdentityServer4.Admin          # https://localhost:44303
dotnet run --project src/Skoruba.IdentityServer4.Admin.Api      # https://localhost:44302 (Swagger at /swagger)

# Seed database (initial data from identitydata.json / identityserverdata.json)
dotnet run --project src/Skoruba.IdentityServer4.Admin /seed
```

EF migrations (initial migrations are committed; regenerate with the script):

```powershell
cd build
.\add-migrations.ps1 -migration MigrationName -migrationProviderName All   # or SqlServer | MySql | PostgreSQL
```

Frontend assets (only needed when changing CSS/JS) — in `src/Skoruba.IdentityServer4.Admin` and `src/Skoruba.IdentityServer4.STS.Identity`: `npm install`, then `gulp build` (or `gulp watch`; `fonts`/`styles`/`scripts`/`clean` tasks also exist).

Docker: `docker-compose build && docker-compose up -d` — requires host entries and mkcert certificates for `*.skoruba.local` (see README "Running via Docker").

## Architecture

Three runnable ASP.NET Core apps share a layered library stack:

- **`Skoruba.IdentityServer4.STS.Identity`** — the IdentityServer4 instance itself plus login/registration/2FA UI (ASP.NET Core Identity). The other two apps authenticate against it via OIDC.
- **`Skoruba.IdentityServer4.Admin`** — thin bootstrap host. Nearly all admin UI code (controllers, views, DI wiring, middleware) lives in **`Skoruba.IdentityServer4.Admin.UI`**, consumed via one large generic call `services.AddIdentityServer4AdminUI<...DbContexts, ...Identity entities, ...DTOs>()` in `Startup.cs`. To change admin UI behavior, edit `Admin.UI`, not the bootstrap project.
- **`Skoruba.IdentityServer4.Admin.Api`** — REST API (Swagger) exposing the same management operations. Uses generic controllers registered through `Configuration/ApplicationParts/GenericControllerRouteConvention.cs`.

Layering beneath the apps (dependency direction: apps → BusinessLogic → EntityFramework):

- **Two parallel business-logic stacks**: `Admin.BusinessLogic` (IdentityServer config: clients, resources, scopes, grants) and `Admin.BusinessLogic.Identity` (ASP.NET Identity: users, roles). Each contains DTOs, Services, Repositories interfaces, AutoMapper profiles, and audit `Events`. `Admin.BusinessLogic.Shared` has shared DTOs/exception handling.
- **EF layer**: `Admin.EntityFramework` (IdentityServer entities/repositories), `Admin.EntityFramework.Identity` (Identity repositories), `Admin.EntityFramework.Shared` (all six DbContexts and Identity entity classes), `Admin.EntityFramework.Configuration`, `Admin.EntityFramework.Extensions`.
- **`Skoruba.IdentityServer4.Shared`** / **`Shared.Configuration`** — DTOs and configuration helpers common to all three apps.

Almost everything is generic over the Identity entity types and DTO types (`UserIdentity`, `UserIdentityRole`, ... `string` key), so type-parameter lists are long and repeated across the apps — changing an entity/DTO type generally means touching the generic registration in all three `Startup` classes.

### Databases and providers

Six DbContexts (all in `Admin.EntityFramework.Shared/DbContexts`): `AdminIdentityDbContext`, `IdentityServerConfigurationDbContext`, `IdentityServerPersistedGrantDbContext`, `AdminLogDbContext`, `AdminAuditLogDbContext`, `IdentityServerDataProtectionDbContext`.

Provider is chosen at runtime via `appsettings.json` → `DatabaseProviderConfiguration:ProviderType` (SqlServer | MySql | PostgreSQL). Each provider has its own migrations project (`Admin.EntityFramework.SqlServer` / `.MySql` / `.PostgreSQL`); `MigrationAssemblyConfiguration` maps the provider to its migrations assembly.

### Cross-cutting

- **Configuration-driven**: nearly all behavior (auth URLs, admin role, themes, CSP, Azure Key Vault, SendGrid/SMTP, external login providers) is bound from `appsettings.json`; prefer extending configuration classes over hardcoding.
- **Audit logging**: services in the BusinessLogic layers call `AuditEventLogger.LogEventAsync(new SomethingChangedEvent(...))` with event classes from their `Events` folders; sinks write to `AdminAuditLogDbContext`.
- **Authorization**: admin controllers use the policy in `AuthorizationConsts.AdministrationPolicy`, which requires the role named by `AdministrationRole` in appsettings.
- **Localization**: all UI strings live in `.resx` files under `/Resources` in the UI/STS projects (11 languages) — user-facing string changes belong there.
- **Logging**: Serilog, configured from `serilog.json` / appsettings.

### Tests

xUnit + FluentAssertions + Bogus. Integration tests use each app's `StartupTest` class (`Configuration/Test/StartupTest.cs`) with an InMemory database and cookie-auth faked by `AuthenticatedTestRequestMiddleware` — no real STS is needed to run them.
