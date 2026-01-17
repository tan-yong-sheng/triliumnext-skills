---
name: excalidraw-diagram
description: Generate Excalidraw diagrams from text content for Trilium Notes. Use when user asks to create diagrams, flowcharts, mind maps, or visual representations. Triggers on "Excalidraw", "Diagram", "Flowchart", "Mind Map", "Visualize".
metadata:
  version: 1.1.0
---

# Excalidraw Diagram Generator

Create Excalidraw diagrams from text content and save them directly to Trilium Notes using the MCP tool.

## Workflow

1.  **Analyze Content**: Identify concepts, relationships, and hierarchy in the user's request.
2.  **Choose Diagram Type**: Select the appropriate visualization style (see guide below).
3.  **Generate Excalidraw JSON**: Construct the complete, valid JSON data structure.
4.  **Execute Tool**: Call the `create_note` function from `triliumnext-mcp`.
    * `title`: A descriptive title.
    * `content`: The complete Excalidraw JSON string.
    * `type`: `canvas`
    * `mime`: `application/json`
    * and other input parameters if required.
5.  **Notify User**: Confirm the note has been created in Trilium.

## Diagram Types & Selection Guide

Select the appropriate chart form to enhance understanding and visual appeal.

| Type | Description | Usage Scenario | Approach |
| :--- | :--- | :--- | :--- |
| **Flowchart** | Step-by-step logic | Processes, workflows, task sequences | Connect steps with arrows to show direction. |
| **Mind Map** | Radiating concepts | Brainstorming, topic classification, ideas | Radiate outwards from a central core node. |
| **Hierarchy** | Organizational tree | Org charts, system breakdowns, taxonomies | Build nodes top-down or left-to-right. |
| **Relationship** | Network/Connection | Dependencies, interactions, influences | Use lines/arrows with labels to show how items relate. |
| **Comparison** | Side-by-side | Analyzing two or more options/views | Columns or tables comparing specific dimensions. |
| **Timeline** | Chronological | Project schedules, history, evolution | Use a time axis with milestones and events. |
| **Matrix** | Quadrant/Grid | 2-axis classification, prioritization | Plot items on X and Y axes (e.g., Eisenhower Matrix). |
| **Freeform** | Unstructured | Rough ideas, mood boards, loose collections | No structural limits; free placement of elements. |

## Design Rules

### Text & Format
* **Font Family**: All text elements must use `fontFamily: 5` (Excalidraw handwritten style).
* **Font Sizes**:
    * Title: 24-28px
    * Subtitle: 18-20px
    * Body/Notes: 14-16px
* **Line Height**: Use `lineHeight: 1.25` for all text.
* **Sanitization**: Ensure all text within the JSON is properly escaped (e.g., escape double quotes `\"` inside the JSON string).

### Layout & Design
* **Canvas Area**: Keep elements within a virtual 0-1200 x 0-800 coordinate box.
* **Spacing**: Ensure appropriate whitespace for readability.
* **Hierarchy**: Use different colors and shapes to distinguish information levels.
* **Elements**: Use rectangles, circles, diamonds, and arrows to organize information effectively.

### Color Palette
* **Titles**: `#1e40af` (Deep Blue)
* **Subtitles/Connectors**: `#3b82f6` (Bright Blue)
* **Body Text**: `#374151` (Dark Gray)
* **Emphasis/Highlight**: `#f59e0b` (Amber/Gold)
* **General**: Use a harmonious color scheme; avoid visual clutter.

## JSON Structure (The Content Payload)

The `content` parameter of the `Notes` tool must be a **valid stringified JSON** following this structure:

```json
{
  "type": "excalidraw",
  "version": 2,
  "source": "[https://github.com/zsviczian/obsidian-excalidraw-plugin](https://github.com/zsviczian/obsidian-excalidraw-plugin)",
  "elements": [...],
  "appState": {
    "gridSize": null,
    "viewBackgroundColor": "#ffffff"
  },
  "files": {}
}

```

## Element Template

### Required Fields for All Elements

Each element in the `elements` array must have these fields:

```json
{
  "id": "unique-id-string",
  "type": "rectangle|text|arrow|ellipse|diamond",
  "x": 100, "y": 100,
  "width": 200, "height": 50,
  "angle": 0,
  "strokeColor": "#1e1e1e",
  "backgroundColor": "transparent",
  "fillStyle": "solid",
  "strokeWidth": 2,
  "strokeStyle": "solid",
  "roughness": 1,
  "opacity": 100,
  "groupIds": [],
  "frameId": null,
  "index": "a1",
  "roundness": {"type": 3},
  "seed": 123456789,
  "version": 1,
  "versionNonce": 987654321,
  "isDeleted": false,
  "boundElements": [],
  "updated": 1751928342106,
  "link": null,
  "locked": false
}

```

### Text-Specific Properties

Elements with `type: "text"` require these additional properties:

```json
{
  "text": "Display Text",
  "rawText": "Display Text",
  "fontSize": 20,
  "fontFamily": 5,
  "textAlign": "center",
  "verticalAlign": "middle",
  "containerId": null,
  "originalText": "Display Text",
  "autoResize": true,
  "lineHeight": 1.25
}

```

---

## Implementation Notes & Tool Usage

### 1. Generating the Filename (Title)

* Create a meaningful title based on the user's topic.
* **Format**: `[Topic] - [Type]`
* *Example*: `Business Model Canvas - Matrix` or `Login Flow - Flowchart`.

### 2. Constructing the Content

* Generate the full JSON object based on the "JSON Structure" and "Element Template" above.
* **Important**: The `content` argument passed to the tool must be the **raw JSON string**. Do not wrap it in Markdown code blocks (like `json ... `) inside the function call, unless specifically requested to store it as a code snippet. It should be the direct JSON data.

### 3. Calling the MCP Tool

You must use the `create_note` tool from `triliumnext-mcp`: https://github.com/tan-yong-sheng/triliumnext-mcp. If the `triliumnext-mcp` is not installed, just directly output the json data.

**Tool Call Logic:**

```
create_note(
    "title": "Project Timeline - Roadmap",
    "content": '{"type": "excalidraw", "version": 2, "elements": [...], ...}',
    "type": "canvas",
    "mime": "application/json"
)
```