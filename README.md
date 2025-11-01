## ATM Activity Diagram

```mermaid
flowchart TD

    %% ============ BANK CUSTOMER ============ %%
    subgraph Customer["Bank Customer"]
        start([Start]) --> insert[Insert Card]
        insert --> enter[Enter Card]
        enter --> dec{Valid PIN?}
    end

    %% ============ ATM SYSTEM ============ %%
    subgraph ATM["ATM System"]
        dec -->|Yes| read[Read and Validate Card]
        read --> return[Return Card]
        dec -->|No| prompt[Prompt Attempt Try]
        prompt --> menu[Display Transaction Menu]
        menu --> balance[Display Account Balance]
        balance --> again{Another Transaction?}
        again -->|Yes| menu
        again -->|No| take[Take Card]
    end

    %% extra connector for 3 attempts
    prompt -. "3 Attempts" .- dec

    %% ending flow
    take --> stop([End])
