```mermaid
flowchart TD

    %% ===================== SWIMLANES ===================== %%
    subgraph Customer["Bank Customer"]
        start([Start]) --> insertCard[Insert Card]
        insertCard --> enterPIN[Enter PIN]
    end

    subgraph ATM["ATM System"]
        enterPIN --> decision{Valid PIN?}

        %% ---------- VALID PIN PATH ----------
        decision -->|Yes| readCard[Read and Validate Card]
        readCard --> showMenu[Display Transaction Menu]
        showMenu --> showBalance[Display Account Balance]
        showBalance --> another{Another Transaction?}
        another -->|Yes| showMenu
        another -->|No| returnCard[Return Card]
    end

    %% ---------- INVALID PIN PATH ----------
    decision -->|No| prompt[Prompt for PIN Again]
    prompt -. "3 Attempts Max" .- decision

    %% ========== ENDING ==========
    returnCard --> takeCard[Take Card]
    takeCard --> endNode([End])
