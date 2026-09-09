# <img width="45" height="35" alt="Cerebrus" src="https://github.com/user-attachments/assets/233dbbd8-c7f2-4d43-9f23-92816cf2afff" /> Cerebrus 

> **More tokens, lower compute costs.** A context aware optimization pipeline designed to maximise LLM throughput while cutting unnecessary LLM calls.

Cerebrus acts as an intelligent optimization layer sitting between your client applications and frontier model providers. Instead of treating every prompt as a full, expensive model call, it caches semantically similar queries, eliminates redundant context overhead, and cascades difficult queries only to the models that actually need them.



## Request Lifecycle

Every user request moves through an intelligent, fallback-driven pipeline:
```
[ Frontend / Client ]
      │
      ▼
[ Backend Gateway ]
      │
      ├──► 1. Semantic Cache Check
      │     ├── Hit  ──► Return cached result immediately (Zero LLM cost)
      │     └── Miss ──▼
      ├──► 2. Context Classification & Pruning
      │        └── Decides if conversation history is needed & extracts minimal slice
      │
      ├──► 3. Model Cascading & Routing
      │        └── Evaluates complexity; routes to the cheapest capable model tier
      │
      ▼
[ Return Optimized Response ]
```
## Core Modules

Our architecture is split into focused microservices:

* **[Semantic Cache System](https://github.com/Pantheom/Semantic-Cache-System)**  
  Reduces repetitive LLM calls by checking vector similarity against previously answered prompts before dispatching new inferences.

* **[Context Classification & Summarization](https://github.com/Pantheom/contextclassandsum)**  
  Analyzes multi-turn dialogue on a per-prompt basis to determine whether chat history is required, injecting only the necessary context window to save tokens.

* **[Model Cascader](https://github.com/Pantheom/modelcascader)**  
  Dynamically measures prompt complexity to route queries to the most cost-effective model tier capable of handling the task.



*Each service contains its own setup guides, configuration options, and deep-dive documentation within its respective repository.*

