Software Diagram

```mermaid
graph TD
    A[FourcastNet Software Requirements]
    A --> B[Python Environment]
    A --> C[Deep Learning Frameworks]
    A --> E[Model Management Tools]
    A --> F[Deployment Tools]

    B --> G[Python Libraries]

    C --> L[PyTorch]

    E --> O[WandB]
    E --> P[YAML Files]

    F --> Q[CUDA]
    F --> R[Apex] 
