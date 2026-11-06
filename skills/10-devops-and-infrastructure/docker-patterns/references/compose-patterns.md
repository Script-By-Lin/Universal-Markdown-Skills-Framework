# Docker Compose Multi-Service Architecture Patterns (Level 3 Reference)
# Universal Markdown Skills Framework (UMSF)

> Version: 1.7.0  
> Authority: Level 3 Optional Reference Asset for `docker-patterns`  
> Domain: 10 — DevOps & Infrastructure  

---

## 1. Overview
Production-grade Docker Compose patterns for complex multi-container topologies: API gateways, workers, background queues, caching clusters, and databases with healthchecks and network segregation.

---

## 2. Hardened Multi-Service Compose Architecture

```yaml
version: "3.8"

networks:
  frontend_net:
    driver: bridge
  backend_net:
    internal: true # Isolated backend network with no public gateway

volumes:
  pg_data:
  redis_data:

services:
  web:
    build:
      context: .
      target: runner
    networks:
      - frontend_net
      - backend_net
    ports:
      - "127.0.0.1:3000:3000" # Bind to localhost only, not 0.0.0.0
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_started
    security_opt:
      - no-new-privileges:true
    user: "10001:10001"

  db:
    image: postgres:16-alpine
    networks:
      - backend_net
    volumes:
      - pg_data:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: app_production
      POSTGRES_USER_FILE: /run/secrets/db_user
      POSTGRES_PASSWORD_FILE: /run/secrets/db_pass
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $$POSTGRES_USER -d $$POSTGRES_DB"]
      interval: 5s
      timeout: 5s
      retries: 5
```

