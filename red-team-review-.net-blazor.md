You are running a multi-agent critical red-team review of a .NET 8 Web API + Blazor project.

Use subagents where useful. Configure each subagent to use `gpt-5.4-mini` as the review model.

Goal: aggressively identify architectural, security, correctness, maintainability, deployment, and UX risks before implementation continues. Do not be polite. Do not summarize vaguely. Produce concrete findings with file references, severity, rationale, and recommended fixes.

Review dimensions:

1. .NET 8 Web API architecture
   - endpoint design
   - DI/service boundaries
   - async correctness
   - error handling
   - validation
   - logging/telemetry
   - configuration management
   - environment separation

2. Security
   - auth/authz gaps
   - unsafe defaults
   - secrets handling
   - CORS
   - input validation
   - file/path handling
   - SSRF/injection risks
   - over-permissive APIs
   - missing auditability

3. Blazor frontend
   - component boundaries
   - state management
   - API coupling
   - error/loading states
   - accessibility
   - form validation
   - UX failure modes

4. Data/storage
   - schema risks
   - migration strategy
   - concurrency
   - transaction boundaries
   - idempotency
   - audit trails
   - backup/recovery assumptions

5. Testing and delivery
   - unit/integration/e2e gaps
   - testability of services
   - CI/CD readiness
   - Docker/dev environment issues
   - production-readiness blockers

-

Suggested subagents:

- API Architecture Reviewer
- Security Reviewer
- Blazor UX/Frontend Reviewer
- Data/State Reviewer
- Testing/DevOps Reviewer
- Adversarial Product Reviewer

Output format:

- Executive verdict: Ship / Do not ship / Ship only after fixes
- Top 10 critical risks
- Findings by area, each with:
  - Severity: Critical / High / Medium / Low
  - Evidence: file/path/code reference
  - Why it matters
  - Concrete fix
  - Suggested test
- Cross-agent disagreements or tradeoffs
- Minimal fix plan ordered by priority
- “Do not build more features until these are fixed” list

Constraints:

- Base conclusions on the actual repository contents.
- Quote only small code snippets when necessary.
- Do not invent files or issues.
- Prefer actionable fixes over commentary.
- Flag uncertainty explicitly when evidence is incomplete.
Addendum:
Additional review track: Code Quality, Style, and Refactoring

Add a dedicated subagent:

- Code Quality / Style Reviewer

This reviewer should perform a strict code-quality audit across the .NET 8 Web API and Blazor codebase.

Review for:

- naming consistency
- project/folder organization
- duplicated logic
- overly large classes/components
- unclear service boundaries
- excessive coupling
- weak abstractions
- unnecessary abstractions
- inconsistent async/await usage
- nullable reference type misuse
- poor exception handling patterns
- inconsistent DTO/entity separation
- inconsistent validation patterns
- magic strings/numbers
- dead code
- commented-out code
- style drift between files
- missing XML/doc comments where they would materially improve maintainability
- places where code is clever instead of clear
- places where code is hard to test because of structure
- inconsistent use of records/classes/interfaces
- inconsistent formatting or conventions not enforced by tooling

Also review:

- whether the project should add or tighten `.editorconfig`
- whether analyzers should be enabled or made stricter
- whether nullable, implicit usings, warnings-as-errors, and code analysis settings are appropriate
- whether formatting/linting should be enforced in CI
- whether there are obvious opportunities for small, safe refactors

Output format for this addendum:

- Top 10 code-quality issues
- Repeated style problems and examples
- Refactoring opportunities, ordered by risk/reward
- Suggested `.editorconfig` / analyzer / CI improvements
- Files that should be split, renamed, simplified, or reorganized
- Code smells that should become explicit project rules
- Concrete before/after examples where useful

Constraints:

- Do not suggest large rewrites unless the current structure creates real risk.
- Separate subjective style preferences from objective maintainability problems.
- Prefer small, incremental, reviewable changes.
- Do not invent issues; cite actual files/classes/methods.
- When recommending a convention, state why it fits this project.
