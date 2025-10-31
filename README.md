# 🏦 ATM Activity Diagram (with Swimlanes)

This UML **Activity Diagram** illustrates the interaction between the **Bank Customer** and the **ATM System**.  
It covers:
- Card insertion and PIN entry  
- PIN verification (with up to 3 attempts)  
- Viewing account balance  
- Option for another transaction or ending the session  

---

```mermaid
%%------------------------------------------------------------
%% ATM Activity Diagram with Swimlanes - Enhanced Version
%%------------------------------------------------------------
flowchart TD

    %% --- Bank Customer Swimlane ---
    subgraph Customer["🏠 Bank Customer"]
        A([Start]):::start --> B[Insert Card]:::action
        B --> C[Enter PIN]:::action
        I[Take Card]:::action --> J([End]):::end
    end

    %% --- ATM System Swimlane ---
    subgraph ATM["💻 ATM System"]
        B --> D[Read Card]:::system
        D --> E[Prompt for PIN]:::system
        C --> F[Verify Card and PIN]:::system

        %% PIN verification decision
        F -->|✅ [valid PIN]| G[Display Transaction Options]:::system
        F -->|❌ [invalid PIN]| H[Increment Attempt Count]:::system

        %% Attempts logic
        H -->|[attempts < 3]| E
        H -->|[attempts = 3]| I

        %% Balance viewing path
        G --> K[Retrieve Account Balance]:::system
        K --> L[Display Balance]:::system
        L --> M{Another Transaction?}:::decision

        %% Loop or exit
        M -->|Yes| G
        M -->|No| I
    end

    %% --- Styling section ---
    classDef start fill:#b3ffb3,stroke:#333,stroke-width:2px;
    classDef end fill:#ffcccc,stroke:#333,stroke-width:2px;
    classDef action fill:#fff2cc,stroke:#333,stroke-width:1px;
    classDef system fill:#cce5ff,stroke:#333,stroke-width:1px;
    classDef decision fill:#ffd6a5,stroke:#333,stroke-width:1px;
