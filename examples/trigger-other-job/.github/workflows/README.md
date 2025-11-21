# Trigger other job

In this example, we trigger another job without having to configure a PAT token.
This is achieved by using github API and workflow_dispatch event.

```mermaid
flowchart LR
    subgraph BR["bump-release"]
        direction TB
        bump
        git_push["git push"]
        create_changelog["create changelog"]
        release
        workflow_dispatch

        bump --> git_push
        git_push --> create_changelog
        create_changelog --> release
        release --> workflow_dispatch
    end

    subgraph TM["trigger-me"]
        echo_version["echo version"]
        
        %% Workaround to increase height of the graph
        echo_version ~~~ spacer1[" "]:::hidden
        spacer1 ~~~ spacer2[" "]:::hidden
        spacer2 ~~~ spacer3[" "]:::hidden
        spacer3 ~~~ spacer4[" "]:::hidden
        spacer4 ~~~ spacer5[" "]:::hidden
    end

    BR --> TM
```
