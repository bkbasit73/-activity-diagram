```mermaid
---
title: UML Activity Diagram – ATM System
---
flowchart TD

%% ========= BANK CUSTOMER SWIMLANE ========= %%
subgraph Customer["Bank Customer"]
    A([Start]) --> B[Insert Card]
    B --> C[Enter Personal Identification Number (PIN)]
    I[Take Card] --> J([End])
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

%% ========= STYLING ========= %%
classDef start fill:#bbf5bb,stroke:#333,stroke-width:2px,color:#000;
classDef end fill:#ffb3b3,stroke:#333,stroke-width:2px,color:#000;
classDef decision fill:#ffe599,stroke:#333,stroke-width:1px,color:#000;
classDef process fill:#d0e1ff,stroke:#333,stroke-width:1px,color:#000;
classDef customer fill:#fef9e7,stroke:#333,stroke-width:1px,color:#000;

class A start;
class J end;
class M decision;
