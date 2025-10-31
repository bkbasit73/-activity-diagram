```mermaid
flowchart TD

    %% --- Bank Customer Swimlane ---
    subgraph Customer["Bank Customer"]
        A([Start]) --> B[Insert Card]
        B --> C[Enter PIN]
        I[Take Card] --> J([End])
    end

    %% --- ATM System Swimlane ---
    subgraph ATM["ATM System"]
        B --> D[Read Card]
        D --> E[Prompt for PIN]
        C --> F[Verify Card and PIN]

        %% PIN verification
        F -->|Valid PIN| G[Display Transaction Options]
        F -->|Invalid PIN| H[Increment Attempt Count]

        %% Attempts logic
        H -->|Attempts < 3| E
        H -->|Attempts = 3| I

        %% Balance viewing
        G --> K[Retrieve Account Balance]
        K --> L[Display Balance]
        L --> M{Another Transaction?}

        M -->|Yes| G
        M -->|No| I
    end
