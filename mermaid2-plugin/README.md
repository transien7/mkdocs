# MkDocs with Mermaid support using Mermaid2 Plugin
This configuration supports Mermaid diagrams via the Mermaid2 plugin

This is achieved through the below configuration:
```text {title="requirements.txt"
mkdocs-mermaid2-plugin==1.1.1
```
Note that the below superfences is still required to treat the code block as a mermaid diagram
```yaml {title="mkdocs.yml"}
markdown_extensions:
  - toc
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:mermaid2.fence_mermaid_custom
``` 

