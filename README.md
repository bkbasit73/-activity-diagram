```mermaid
flowchart TD

    %% ========= BANK CUSTOMER SWIMLANE ========= %%
    subgraph Customer["Bank Customer"]
        A([Start]) --> B[Insert Card]
        B --> C[Enter PIN]
        C --> I[Take Card]
        I --> J([End])
    end

    %% ========= ATM SYSTEM SWIMLANE ========= %%
    subgraph ATM["ATM System"]
        B --> D[Read and Validate Card]
        D --> E[Prompt for PIN]
        C --> F[Verify Card and PIN]

        %% ----- PIN Validation -----
        F -->|Valid PIN| G[Display Transaction Menu]
        F -->|Invalid PIN| H[Increase Attempt Counter]
        H -->|Attempts < 3| E
        H -->|Attempts = 3| I

        %% ----- Balance Enquiry Path -----
        G --> K[Retrieve Account Balance]
        K --> L[Display Account Balance]
        L --> M{Another Transaction?}
        M -->|Yes| G
        M -->|No| I
    end
