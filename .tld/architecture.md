# Central Agentic Ops — System Architecture Diagram
*Generated from Top-Level Design (`tld`)*

```mermaid
flowchart LR
  catalog["Campaign Catalog<br/><i>campaigns and workflows</i>"]
  control_repo["Control Repository<br/><i>cao.json & credentials</i>"]
  policy_resolver["Policy Resolver<br/><i>admit & narrow</i>"]
  orchestrator["Campaign Orchestrator<br/><i>dispatch orchestration</i>"]
  worker["One-Target Worker<br/><i>bounded safe execution</i>"]
  target_repo["Target Repository<br/><i>authorized live output</i>"]
  dashboard_server["Dashboard Server<br/><i>Go loopback HTTP</i>"]
  postgres_db[("PostgreSQL Database<br/><i>canonical & operational</i>")]

  catalog -->|installs reviewed release| control_repo
  control_repo -->|supplies policy & credentials| policy_resolver
  policy_resolver -->|admits & narrows| orchestrator
  orchestrator -->|bounded dispatch| worker
  worker -->|authorized live output| target_repo
  dashboard_server -->|reads & writes state| postgres_db
```

---

### Command to Re-render

To export the raw Mermaid diagram at any time:

```sh
tld render root -o .tld/architecture.mmd
```
