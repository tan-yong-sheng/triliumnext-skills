# TriliumNext Skills

A set of visual skills for [TriliumNext](https://github.com/TriliumNext/TriliumNext) that convert text into diagrams (Excalidraw, Mermaid, Mindmaps).  
Designed to work with [triliumnext-mcp](https://github.com/tan-yong-sheng/triliumnext-mcp).

## Installation

```bash
/plugin marketplace add tan-yong-sheng/triliumnext-skills
/plugin install triliumnext-skills
````

## Prerequisites

* [triliumnext-mcp](https://github.com/tan-yong-sheng/triliumnext-mcp)

## Available Skills

### Excalidraw Diagram Generator

**Skill:** `excalidraw-drawer`

Creates Excalidraw-style diagrams from text.

**Typical uses**

* Flowcharts
* Architecture diagrams
* Mind maps
* Timelines

Example:

```
Create an Excalidraw diagram for our deployment workflow
```

---

### Mermaid Visualizer

**Skill:** `mermaid-visualizer`

Generates Mermaid diagrams with validated syntax.

**Typical uses**

* Flowcharts
* Sequence diagrams
* State diagrams
* System architecture

Example:

```
Create a Mermaid sequence diagram for user login
```

---

### Mindmap Builder

**Skill:** `mindmap-builder`

Builds structured hierarchical mind maps.

**Typical uses**

* Knowledge organization
* Research summaries
* Feature breakdowns

Example:

```
Create a mindmap of the main ideas in this document
```

## How It Works

1. Analyze input text
2. Select the appropriate diagram type
3. Generate structured output
4. Save the result to TriliumNext via MCP

## Output Formats

| Skill      | Type         | MIME               |
| ---------- | ------------ | ------------------ |
| Excalidraw | JSON canvas  | `application/json` |
| Mermaid    | Mermaid text | `text/vnd.mermaid` |
| Mindmap    | JSON         | `application/json` |

## References

* Excalidraw schema: `skills/excalidraw-drawer/references/excalidraw-schema.md`
* Mermaid rules: `skills/mermaid-visualizer/references/syntax-rules.md`
* Mindmap schema: `skills/mindmap-builder/references/mindmap-schema.md`

## Issues

Report bugs or request features at:
[https://github.com/tan-yong-sheng/triliumnext-skills/issues](https://github.com/tan-yong-sheng/triliumnext-skills/issues)