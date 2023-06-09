```mermaid
graph LR;
    subgraph GPU_Server
        B("lama.cpp");
    end
    subgraph Backend_Server
        D("back end api");
        subgraph GitLab_API
            F("API source code");
        end
    end
    subgraph UI_Server
        E("front end ui");
        subgraph GitLab_UI
            G("UI source code");
        end
    end
    subgraph Network_Storage
        A("100 Models");
        C("parameters files");
    end
    subgraph GitLab
        H("Source code");
    end
    subgraph RDBMS
        J("Postgres");
    end
    A -->|Stored in| Network_Storage;
    C -->|Stored in| Network_Storage;
    Network_Storage -->|Input| GPU_Server;
    GPU_Server -->|Process| Backend_Server;
    Backend_Server -->|Output| UI_Server;
    UI_Server -->|Request| Backend_Server;
    Backend_Server -->|Request| GPU_Server;
    C -->|Request| GPU_Server;
    F -->|Used by| Backend_Server;
    G -->|Used by| UI_Server;
    H -->|Used by| GPU_Server;
    H -->|Used by| Backend_Server;
    H -->|Used by| UI_Server;
    Backend_Server -->|Pulls data from| J;
    J -->|Feeds content into| B;
``` 
