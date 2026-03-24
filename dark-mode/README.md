# MkDocs with Mermaid2 Plugin and Dark Mode

## Dark mode
This sample extends the mermaid2 plugin configuration by adding support to toggle dark mode on or off. This works out of the box with mkdocs-material provided the below palette options are included in `mkdocs.yml`.

```yaml title="mkdocs.yml"
theme:
  name: material
  palette: 

    # Palette toggle for light mode
    - scheme: default
      toggle:
        icon: material/brightness-7 
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
```

## Support for newer diagrams
Changes were made to the `mkdocs.yml` to support the rendering of newer diagrams added since Mermaid v11.1.0.

```yml title="mkdocs.yml"
markdown_extensions:
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          # From:
          #format: !!python/name:mermaid2.fence_mermaid_custom
          # To:
          format: !!python/name:mermaid2.fence_mermaid

plugins:
  - mermaid2:
      # Explicitly provide a Mermaid version
      version: 11.1.0  # min version for architecture diagrams
```

## Documentation structure
The documenmtation structure has changed in this same, providing a base template that can be extended to any project.
