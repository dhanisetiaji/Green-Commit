```mermaid
graph TD
    A[Start] --> B[Check cron status]
    B -->|cronStatus.status !== 1| C[Return true]
    B -->|cronStatus.status === 1| D[Fetch storages to delete]
    D --> E[Filter storages with row_num > 1]
    E --> F[Map to idsToDelete]
    F -->|idsToDelete.length > 0| G[Soft delete storages]
    G --> H[Log soft deleted storages]
    F -->|idsToDelete.length === 0| H
    H --> I[Fetch active storages]
    I --> J[Iterate over active storages]
    J --> K[Fetch branch data for each storage]
    K --> L[Update storage name]
    L --> M[End]
