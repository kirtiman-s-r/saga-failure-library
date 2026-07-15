# Person 1 (Backend) — Progress Log
Format: ## [Month].[Week].[Day] — [Date]
Rule: only ADD entries at the bottom.

---

---

## M1.W1.D1 — July 12
**Did:** Installed Java 25, Maven, Git, Postman, DBeaver, IntelliJ. Verified each with version checks and opening IntelliJ once.
**Result:** All 6 tools confirmed installed and working.
**Notes:** None.

---

## M1.W1.D2 — July 12
**Did:** Installed Docker Engine (Linux, via snap, terminal-only). Ran a standalone Postgres container manually with docker run, confirmed with docker ps, then stopped and removed it.
**Result:** Postgres started on port 5433 (5432 already taken), confirmed running, then cleanly removed.
**Notes:** Port 5432 conflict — handle this in Day 4 docker-compose setup.

---
## M1.W1.D3 — July 14
**Did:** Generated Spring Boot project via start.spring.io (Spring Web, Spring Data JPA, PostgreSQL Driver), imported into IntelliJ, ran via `mvn spring-boot:run`.
**Result:** App started successfully, then failed as expected with "Failed to configure a DataSource" — no DB connection configured yet, no Postgres running. This is the expected Day 3 checkpoint error.
**Notes:** Maven wrapper (.mvn folder) got lost during manual folder move — not an issue, used system-installed Maven (mvn command) instead of wrapper (./mvnw).

---
## M1.W1.D4 — July [today]
**Did:** Wrote docker-compose.yml with a Postgres service (db: saga_db, port mapped 5433:5432 due to local Postgres conflict on 5432). Ran with `docker compose up -d`.
**Result:** Container `saga-postgres` running successfully, confirmed via docker ps.
**Notes:** Used `docker compose` (space) not `docker-compose` (hyphen) — the hyphenated command isn't installed on this system, but the newer space version is built into Docker already. Also had to remap port to 5433 due to existing local Postgres on 5432 (same as Day 2).

---