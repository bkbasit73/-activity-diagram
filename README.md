## ATM Activity Diagram

```mermaid
flowchart TD

    %% ============ BANK CUSTOMER ============ %%
    subgraph Customer["Bank Customer"]
        start([Start]) --> insert[Insert Card]
        insert --> enter[Enter PIN]
    end

    %% ============ ATM SYSTEM ============ %%
    subgraph ATM["ATM System"]
        enter --> dec{Valid PIN?}

        %% ----- YES PATH (correct PIN) -----
        dec -->|Yes| read[Read and validate card]
        read --> menu[Display transaction menu]
        menu --> balance[Display account balance]
        balance --> again{Another transaction?}
        again -->|Yes| menu

        %% ----- NO PATH (wrong PIN) -----
        dec -->|No| prompt[Prompt for PIN again]
        %% loop for 3 attempts
        prompt -. "3 attempts max" .- enter

        %% ----- FINISH -----
        again -->|No| return[Return Card]
    end

    %% back to customer to take card and end
    return --> take[Take Card]
    take --> stop([End])
