'''mermaid

graph TD
    A[Start - @Scheduled job runs every 15 min] --> B[Load all active configs from DB]
    B --> C{Loop through each config}
    C -->|Check cron expression| D[Is current time matching cron?]
    D -->|Yes| E[Call FileFetcherService with config]
    E --> F[Check if expected file is present]
    F -->|Yes| G[Convert file to MultipartFile]
    G --> H[Call ValidationService]

    H --> I{Validation Result}
    I -->|Success| J[Call ImportService]
    I -->|Failed| K[Send email to Process Owner (validation failed)]

    F -->|No| L[Send email to producer (file missing)]

    D -->|No| M[Skip this config]

    J --> N[Update last_received_time in DB]
    K --> N
    L --> N
    M --> N

    N --> O[Repeat for next config]
    O --> P[End of 15-min cycle]
'''
