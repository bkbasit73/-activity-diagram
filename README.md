# 🏦 Bank ATM Activity Diagram (UML)

This project demonstrates a **UML Activity Diagram** for a **Bank ATM System** using Mermaid syntax.  
The diagram shows the interaction between the **Bank Customer** and the **ATM System** — including card validation, PIN verification, transaction handling, and balance inquiry.

---

## 💻 Diagram Code

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
    takeCard --> end([End])

    %% ========== OPTIONAL STYLING ==========
    classDef customer fill:#e3f2fd,stroke:#90caf9,stroke-width:1px;
    classDef atm fill:#fff8e1,stroke:#ffecb3,stroke-width:1px;
    class insertCard,enterPIN,takeCard,start,end customer;
    class decision,readCard,showMenu,showBalance,another,prompt,returnCard atm;
