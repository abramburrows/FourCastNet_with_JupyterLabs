Hardware 

```mermaid
graph TD
    A[FourcastNet Hardware Requirements]
    A --> B[Compute Resources]
    A --> C[Storage]

    B --> D[GPUs] 
    B --> E[CPUs]
    B --> F[Cloud Compute Instances]

    C --> G[High-speed Disk Storage]
    C --> H[Backup Storage]
    C --> I[Data Transfer Bandwidth]

    D --> J[A100]
    D --> K[L40]

    F --> L[JupyterHub]
