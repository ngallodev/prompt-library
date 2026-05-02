# backend api design .netcore

---
name: be-dotnet-core-api
description: Design a production-ready ASP.NET Core Web API for a given problem, including code examples.  use when prompt contains “Design an API for X” “Build a multi-tenant endpoint” “How would you structure this service?” or similar requests.

---

Act as a senior .NET backend engineer.

Design a production-ready ASP.NET Core Web API for the following problem:

[PASTE PROBLEM]

Include:

1. API contract (routes, request/response models)
2. Authentication/authorization approach (JWT, scopes, roles)
3. Multi-tenant strategy (header, subdomain, claims, etc.)
4. Service layer design (interfaces, separation of concerns)
5. Data access approach (EF Core, repository or not)
6. Validation and error handling strategy
7. Observability (logging, tracing, metrics)
8. How this would be deployed across environments

Then provide a minimal but clean code example for:

- Controller
- Service
- Middleware (if relevant)
- Data model and DbContext (if relevant)
