```mermaid
flowchart TD

    %% ===================== SWIMLANES ===================== %%
    %% We fake swimlanes using subgraphs (GitHub Mermaid allows this)
    subgraph Customer["Bank Customer"]
        start([Start]) --> insertCard[Insert Card]
        insertCard --> enterPIN[Enter PIN]
    end

    subgraph ATM["ATM System"]
        %% verify PIN after customer enters it
        enterPIN --> decision{Valid PIN?}

        %% ---------- VALID PIN PATH ----------
        decision -->|Yes| readCard[Read and validate card]

        %% after successful validation, go to transaction flow
        readCard --> showMenu[Display transaction menu]
        showMenu --> showBalance[Display account balance]

        %% user may do more transactions
        showBalance --> another{Another transaction?}
        another -->|Yes| showMenu

        %% if no more transactions → return card
        another -->|No| returnCard[Return card]
    end

    %% ---------- INVALID PIN PATH ----------
    decision -->|No| prompt[Prompt for PIN again]
    prompt --> showMenu
    %% note: to model 3 attempts in code, we add a note label
    prompt -. "3 attempts max" .- decision

    %% ========== ENDING ==========
    %% card goes back to customer
    returnCard --> takeCard[Take card]
    takeCard --> end([End])

    %% ========== OPTIONAL STYLING ==========
    classDef customer fill:#e3f2fd,stroke:#90caf9,stroke-width:1px;
    classDef atm fill:#fff8e1,stroke:#ffecb3,stroke-width:1px;
    class insertCard,enterPIN,takeCard,start,end customer;
    class decision,readCard,showMenu,showBalance,another,prompt,returnCard atm;
