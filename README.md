### Systems Engineering Research

I explore programming languages and runtime environments as complementary tools for designing efficient, maintainable and scalable systems.

- **C** — network infrastructure, API-aware reverse proxies, traffic filtering and performance-critical processing.
- **Zig** — safe, resource-efficient native components and low-overhead abstractions where native implementation is advantageous.
- **Go** — standalone engineering tools, utilities and development infrastructure.
- **Node.js / Bun** — flexible backend development, rapid prototyping, frequently evolving application logic and API abstraction.
- **Java** — long-lived services, complex infrastructure, scalable APIs and strongly governed contracts designed for consistency and maintainability.

The underlying approach is to distribute responsibilities according to execution efficiency, development velocity and long-term maintenance costs. Components may operate independently or coexist, with each runtime selected according to the requirements and economics of its role.

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

