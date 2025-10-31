```mermaid
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

        F -->|✅ [valid PIN]| G[Display Transaction Options]:::system
        F -->|❌ [invalid PIN]| H[Increment Attempt Count]:::system

        H -->|
