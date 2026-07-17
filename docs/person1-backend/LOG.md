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
## M1.W1.D4 — July 15
**Did:** Wrote docker-compose.yml with a Postgres service (db: saga_db, port mapped 5433:5432 due to local Postgres conflict on 5432). Ran with `docker compose up -d`.
**Result:** Container `saga-postgres` running successfully, confirmed via docker ps.
**Notes:** Used `docker compose` (space) not `docker-compose` (hyphen) — the hyphenated command isn't installed on this system, but the newer space version is built into Docker already. Also had to remap port to 5433 due to existing local Postgres on 5432 (same as Day 2).

---
## M1.W1.D5 — July 15
**Did:** Added datasource config to application.properties (URL, username, password matching docker-compose Postgres on port 5433). Restarted Spring Boot app. Verified connection in DBeaver too.
**Result:** Spring Boot starts with zero errors — Hikari connection pool connects successfully to saga_db. DBeaver "Test Connection" also confirms Connected.
**Notes:** Used port 5433 throughout (not 5432) due to existing local Postgres conflict from Day 2/4. No volume set up yet for Postgres data — data will be lost if container is removed; need to add a volume before real data matters (Week 2+).

---
## M1.W2.D1 — July 16
**Did:** Created SagaEvent entity class (transactionId, serviceId, status, timestamp fields) with @Entity/@Table annotations. Restarted Spring Boot app.
**Result:** saga_events table auto-created in Postgres via Hibernate ddl-auto=update, confirmed in DBeaver with correct columns (id, service_id, status, timestamp, transaction_id).
**Notes:** Postgres container had stopped (likely laptop restart/sleep) — had to run docker compose up -d again before Spring Boot could connect. Also learned mvn clean install runs tests (which need a live DB), while mvn spring-boot:run does not — that's why clean install failed when the container was down.

---