---
icon: 
---

# Sequence diagram

```
sequenceDiagram
  Server->>Client:  send_message(msg)
  Client-->>Client: process_message(msg)
  Client-->>Server: send_response()
```

```mermaid
sequenceDiagram
  Server->>Client:  send_message(msg)
  Client-->>Client: process_message(msg)
  Client-->>Server: send_response()
```