---
name: mindmap-builder
description: Create and edit hierarchical mind maps to organize ideas and visualize concepts using specific JSON structures. Automatically handles common syntax pitfalls (list syntax conflicts) to ensure diagrams render correctly in TriliumNext Note / Trilium Note.
---

# Mindmap Builder

## Overview

Create hierarchical mindmaps by generating specific structured JSON content.


## Quick Start

1.  **Analyze Content**: Identify the root topic and primary sub-concepts.
2.  **Determine Structure**: Decide if the flow is linear (Process), comparative (Split), or radial (Standard Mindmap).
3.  **Assign Directions**:
    * `direction: 1` (Right) for outputs/future/steps.
    * `direction: 0` (Left) for inputs/past/causes.
4.  **Generate JSON**: Construct the `nodeData` object with unique IDs and children arrays.
5.  **Call Tool**: Use `Notes` with the JSON string.

## Diagram Types

Since this tool uses a tree structure, map the conceptual types to the following layouts:

### 1. Process Flow (Linear Layout)
* **Structure**: Root node = Start. All children set to `direction: 1` (Right).
* **Use Case**: Step-by-step instructions, timelines, or pipelines.
* **Visual**: Grows in a single direction to mimic a flow chart.

### 2. Circular Flow (Cycle Breakdown)
* **Structure**: Root node = The Cycle Name. Main phases are Level 1 children.
* **Simulation**: Arrange children clockwise or sequentially on the right side.
* **Note**: Since trees do not loop, represent the "return" to start as the final node text (e.g., "Return to Step 1").

### 3. Comparison Diagram (Split Layout)
* **Structure**: Root node = "VS" or Subject.
* **Layout**:
    * Subject A branch → `direction: 0` (Left)
    * Subject B branch → `direction: 1` (Right)
* **Use Case**: Pros vs. Cons, Old vs. New, Problem vs. Solution.

### 4. Mindmap (Standard Radial)
* **Structure**: Balanced tree.
* **Layout**: Alternating branches left and right to maintain visual equilibrium.

### 5. Sequence Breakdown (Timeline Tree)
* **Structure**: Root = Event Name.
* **Layout**: Level 1 nodes are time phases (e.g., "Phase 1", "Phase 2"). Level 2 nodes are specific interactions.
* **Direction**: strictly Right-oriented.

### 6. State Hierarchy (Status Breakdown)
* **Structure**: Root = Entity Name.
* **Layout**: Level 1 nodes are States (e.g., "Idle", "Active", "Error"). Level 2 nodes are triggers or properties of that state.

---

## Critical Syntax Rules

* **Rule 1: Unique IDs**: Every node in the `nodeData` hierarchy must have a unique `id` string (e.g., "root", "sub1", "sub2").
* **Rule 2: Strict JSON Format**: Content must be valid, parseable JSON. No trailing commas.
* **Rule 3: Children Arrays**: Leaf nodes must have an empty `children: []` array.
* **Rule 4: Text Content**: Node `topic` must be plain text. Avoid Markdown or HTML tags inside the JSON strings.
* **Rule 5: Direction Integer**: `direction` must be `0` (left) or `1` (right). Do not use strings like "left".
* **Rule 6: Root Node Integrity**: There must be exactly one top-level object containing the `root` ID.

---

## Configuration Options

* **Theme Names**: `default`, `primary`, `warning`, `danger`, `success`, `info`.
* **Directions**:
    * `0`: Left (Inputs, Causes)
    * `1`: Right (Outputs, Effects)

## Example Usage Patterns

**User Request**: "Compare SQL and NoSQL."
**Pattern**: Comparison Diagram (Type 3). Root "Database Types". Left branch "SQL", Right branch "NoSQL".

**User Request**: "Show the steps to deploy code."
**Pattern**: Process Flow (Type 1). Root "Deployment". All steps extend to the Right.

---

## Workflow

### Color Scheme Defaults
* **Root Node**: `#4A90E2` (Bright Blue) - The anchor.
* **Level 1 Nodes**: `#50E3C2` (Teal) - Main categories.
* **Level 2 Nodes**: `#B8E986` (Light Green) - Details.
* **Warning/Error Nodes**: `#FF5757` (Red).

### Common Patterns

#### Swimlane Pattern (Grouping)
* *Simulation*: Use Level 1 nodes as "Lanes" (e.g., "Frontend", "Backend") and Level 2 nodes as tasks.

#### Feedback Loop Pattern
* *Simulation*: Use a specific node style (e.g., color red) to indicate a "Return" step, as actual link loops are not supported in tree JSON.

#### Hub and Spoke Pattern
* *Simulation*: Standard Mindmap with a massive Root node and shallow depth (many children, no grandchildren).

---

## Quality Checklist

- [ ] **Valid JSON**: Is the string valid JSON without syntax errors?
- [ ] **ID Uniqueness**: Are all node IDs distinct?
- [ ] **Balance**: Is the tree roughly balanced (unless it's a specific flow)?
- [ ] **Depth Control**: Is the hierarchy limited to 4-5 levels to prevent canvas clutter?
- [ ] **Node Brevity**: Are topics concise (1-5 words)?

---

## Implementation Notes & Tool Usage

### 1. Generating the Filename (Title)
* Create a descriptive title.
* **Format**: `[Topic] - Mindmap`
* **Example**: `Project Alpha - Mindmap`

### 2. Constructing the Content
You must generate a specific JSON object structure.

**Schema Structure:**
```json
{
  "nodeData": {
    "id": "root",
    "topic": "Central Topic",
    "children": [
      {
        "id": "child_1",
        "topic": "Left Branch",
        "direction": 0,
        "children": []
      },
      {
        "id": "child_2",
        "topic": "Right Branch",
        "direction": 1,
        "children": []
      }
    ]
  },
  "linkData": {}
}
```

### 3. Calling the MCP Tool
- Tool: Notes
- Type: mindMap
- Mime: application/json

Example Call:

```
create_note({
    title: "Launch Plan - Mindmap",
    type: "mindMap",
    mime: "application/json",
    content: "{\"nodeData\":{\"id\":\"root\",\"topic\":\"Launch\",\"children\":[{\"id\":\"c1\",\"topic\":\"Prep\",\"direction\":0,\"children\":[]},{\"id\":\"c2\",\"topic\":\"Go-Live\",\"direction\":1,\"children\":[]}]}}"
})
```

## References

- Ensure proper nesting of the children array.
- `direction` property is required for Level 1 children to determine layout side.

