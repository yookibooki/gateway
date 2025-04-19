# Gazset Gateway Modernization  
**Building a production‑grade Go service with PostgreSQL**

---

## 1. Executive Summary  
- **Goal:** Replace existing Java SOAP client with a lightweight, high‑performance Go service  
- **Scope:**  
  - Real‑time telemetry ingestion (TCP/CSD/FTP)  
  - Incremental and full‑history archive fetch via SOAP/WSDL  
  - Data storage & retention in PostgreSQL  
  - Monitoring, logging, and CI/CD  
- **Value:**  
  - 2× throughput improvements  
  - Easier maintenance & faster feature delivery  
  - Reduced infra footprint

---

## 2. Key Features  
1. **SOAP/WSDL Go client**  
2. **Concurrent polling scheduler**  
3. **Incremental & historical archives**  
4. **Robust error‑handling & retries**  
5. **Containerized microservice**  
6. **Automated tests & CI/CD pipeline**

---

## 3. Proposed Architecture  

```txt
┌────────────┐    SOAP/WSDL    ┌──────────────┐    Postgres    ┌──────────┐
│  Devices   │ ──────────────▶ │  Go Service  │ ◀──────────── ▶ │ Database │
│(LIS200, TMR│                  │(GatewayWS    │               │ (schemas)│
│ , FTP, CSD)│ ──────────────▶ │ client +     │               └──────────┘
└────────────┘                  │ scheduler,   │
                                │ processor)   │
                                └──────────────┘
                                     │
                                     ▼
                             Monitoring & Logging
```

---

## 4. Team & Roles  
| Role                   | Headcount | Key Responsibilities                     |
|------------------------|:---------:|------------------------------------------|
| Backend Engineers      |     2     | Go client stubs, polling, data models    |
| Database Engineer      |     1     | Schema design, rowVersion triggers       |
| DevOps / SRE           |     1     | Docker, Kubernetes, CI/CD, monitoring    |
| QA Engineer            |     1     | Unit/integration tests, test automation  |
| **Total**              |     **5** |                                          |

---

## 5. High‑Level Timeline  
| Phase                      | Duration | Milestones                             |
|----------------------------|:--------:|----------------------------------------|
| **1. Discovery & Design**  | 2 weeks  | Architecture docs, WSDL mock‑ups       |
| **2. Stub Generation**     | 1 week   | Go SOAP client, XML marshalling tests  |
| **3. DB Schema & Migrations** | 2 weeks  | Tables, triggers, sample data loads    |
| **4. Core Service**        | 3 weeks  | Polling engine, archive fetch & store  |
| **5. Error Handling & Retries** | 1 week   | Map #ERROR codes, backoff logic        |
| **6. Testing & Hardening** | 2 weeks  | E2E tests, performance benchmarks      |
| **7. DevOps & Rollout**    | 1 week   | Docker images, Helm charts, staging    |
| **Total Time**             | **12 weeks** |                                      |

---

## 6. Investment & Costs  
- **Effort:** 5 FTE × 12 weeks = 60 person‑weeks  

---

## 7. Risk & Mitigation  
| Risk                                | Mitigation                              |
|-------------------------------------|-----------------------------------------|
| SOAP/WSDL edge cases                | Early stub generation & smoke tests     |
| Data schema evolution               | Versioned migrations, backward hooks    |
| Throughput limits under load        | Load test simulations, auto‑scaling     |
| Team ramp‑up                        | Dedicated knowledge‑share sessions      |

---

## 8. Next Steps  
1. **Sign‑off & budget approval**  
2. Kick‑off **Discovery** workshop  
3. Provision **staging environment**  
4. Begin **sprint 0**: WSDL analysis & schema design  
5. Regular **bi‑weekly demos** to track progress  
