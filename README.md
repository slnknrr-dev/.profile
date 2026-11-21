### Systems Engineering Research

I explore programming languages and runtime environments through a division of engineering responsibilities:

- **Zig** — general-purpose native software, zero-overhead abstractions and resource-efficient execution.
- **C** — reverse proxies, low-level networking and performance-critical components.
- **Go** — standalone engineering tools, utilities and development infrastructure.
- **Node.js / Bun** — backend development, application logic and runtime orchestration.
- **Java** — long-lived storage contracts, stable interfaces and EAFP-first, non-defensive API design.

The goal is to understand where each language provides the strongest engineering advantages and how their responsibilities can coexist within a cohesive software architecture.

```mermaid

flowchart TD
    CLIENT(["Clients"])

    subgraph NETWORK["Network Layer · C"]
        C["C · Native Network Processing"]
        INSPECT["Request & Header Inspection"]
        TOKEN["Token-aware Processing"]
        POLICY{"Traffic Decision"}
        REJECT["Reject / Filter"]
        CACHE["Cache"]
        ROUTE["Routing & Load Balancing"]

        C --> INSPECT --> TOKEN --> POLICY
        POLICY --> REJECT
        POLICY --> CACHE
        POLICY --> ROUTE
    end

    subgraph APPLICATION["Application Layer · Node.js / Bun"]
        JS["Flexible Backend & API"]
        PROTOTYPE["Prototyping & Rapid Development"]
        ADAPT["Abstractions & Request Adaptation"]
        STANDALONE["Standalone Application / Website"]

        JS --> PROTOTYPE
        JS --> ADAPT
        JS --> STANDALONE
    end

    subgraph CORE["Governed API Layer · Java"]
        JAVA["Java · Strict API Contracts"]
        DOMAIN["Complex Business Logic"]
        SERVICES["Long-lived Services"]
        INVARIANTS["Enforced Contracts & Invariants"]

        JAVA --> DOMAIN
        JAVA --> SERVICES
        JAVA --> INVARIANTS
    end

    subgraph NATIVE["Native Components · Zig"]
        ZIG["Safe & Efficient Native Implementations"]
        PRIMITIVES["Low-level Primitives"]
        ZIG --> PRIMITIVES
    end

    subgraph TOOLING["Engineering Tools · Go"]
        GO["Standalone Utilities & Tooling"]
    end

    CLIENT --> C
    ROUTE --> JS
    ROUTE --> JAVA
    JS --> JAVA

    JS -.->|"Optional native integration"| ZIG
    C -.->|"Optional native integration"| ZIG

    GO -.->|"Development tooling"| APPLICATION
    GO -.->|"Development tooling"| CORE

    CLIENT -.->|"C not required"| JS
```

