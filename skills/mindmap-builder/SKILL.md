---
name: mindmap-builder
description: Create and edit hierarchical mindmap to organize ideas and visualize concepts using specific JSON structures. Automatically handles common syntax pitfalls (list syntax conflicts) to ensure diagrams render correctly in TriliumNext Note / Trilium Note.
---

# Mindmap Builder

## Overview

Create hierarchical mindmaps by generating specific structured JSON content. Automatically handles common syntax pitfalls (list syntax conflicts) to ensure diagrams render correctly in TriliumNext Note / Trilium Note.

## Critical Syntax Rules

* **Rule 1: Unique IDs**: Every node in the `nodeData` hierarchy must have a unique `id` string (e.g., "root", "sub1", "sub2").
* **Rule 2: Strict JSON Format**: Content must be valid, parseable JSON. No trailing commas.
* **Rule 3: Children Arrays**: Leaf nodes must have an empty `children: []` array.
* **Rule 4: Text Content**: Node `topic` must be plain text. Avoid Markdown or HTML tags inside the JSON strings.
* **Rule 5: Direction Integer**: `direction` must be `0` (left) or `1` (right). Do not use strings like "left".
* **Rule 6: Root Node Integrity**: There must be exactly one top-level object containing the `root` ID.


## Cognitive Load Management

### Miller's Rule (7±2) - Core Limits
* **Max Children per Node**: 5-7 children (never exceed 9)
* **Max Depth**: 3-4 levels maximum (beyond 4 creates cognitive overload)
* **Node Topics**: 1-4 words optimal, max 6 words, 25 characters maximum
* **Total Nodes**: 20-40 nodes for standard complexity
* **Visual Colors**: Max 5-6 distinct colors to prevent confusion


## Visual Styles
* **minimal**: Clean, high contrast, reduced visual noise
* **professional**: Business-friendly with subtle colors
* **colorful**: Vibrant, engaging colors for learning/creativity
* **academic**: Structured, formal appearance

---

## Layout Selection Guidelines

### ⚠️ Critical Layout Choice Decision

**AVOID RADIAL (Two-sided) LAYOUTS** in most cases. Radial layouts often create:
- **Visual Chaos**: Intersecting lines and crossing branches
- **Cognitive Overload**: Eye doesn't know where to start or follow
- **Poor Readability**: Text overlaps and navigation confusion
- **Lost Hierarchy**: Can't distinguish main from sub-concepts

### When to Use Each Layout

#### ✅ **LEFT-SIDED Layout** (Recommended for most content)
**Perfect for:**
- **Knowledge breakdown** and analysis
- **Review content** (like rating/evaluating multiple items)
- **Educational content** (lessons, tutorials, explanations)
- **Research summaries** (papers, articles, videos)
- **Categorization** (organizing topics by type/theme)

**Why it works:**
- Natural left-to-right reading flow into central concept
- Clean visual hierarchy with no crossing lines
- Easy to follow logical progression
- Reduces cognitive load significantly

**Examples:**
- "AI Agents Review" (analyzing multiple tools/agents)
- "Video Content Summary" (breaking down main topics)
- "Technology Comparison" (features flowing into main concept)

#### ✅ **RIGHT-SIDED Layout**
**Perfect for:**
- **Process flows** and step-by-step procedures
- **Timelines** and sequential events
- **Implementation plans** (what to do next)
- **Troubleshooting guides** (problem → solutions)

**Examples:**
- "Deployment Steps"
- "Project Timeline"
- "Setup Instructions"

#### ⚠️ **RADIAL Layout** (Use sparingly)
**Only use when:**
- Content has **natural opposing sides** (pros vs cons)
- **True comparison** of exactly two things
- **Balanced analysis** where left/right sides are equally important
- Simple content (max 3-4 branches per side)

**Examples:**
- "SQL vs NoSQL" (feature comparison)
- "Pros vs Cons of Technology X"
- "Before vs After Analysis"

### Content Type → Layout Mapping

| Content Type | Recommended Layout | Reasoning |
|-------------|-------------------|-----------|
| Video summaries | LEFT-SIDED | Breaking down topics into central concept |
| Technology reviews | LEFT-SIDED | Analysis flows into main subject |
| Educational content | LEFT-SIDED | Natural learning progression |
| Process documentation | RIGHT-SIDED | Sequential flow from start to end |
| Comparison studies | LEFT-SIDED (usually) | Unless true 50/50 comparison |
| Research analysis | LEFT-SIDED | Findings flow into main topic |
| Feature breakdowns | LEFT-SIDED | Components flow into main product |

### Layout Decision Framework

**Ask yourself:**
1. **Is this content analytical/review-based?** → Use LEFT-SIDED
2. **Is this content process/sequence-based?** → Use RIGHT-SIDED
3. **Is this content a true comparison of exactly two equal things?** → Consider RADIAL (but often LEFT-SIDED is still better)

**Default choice:** When in doubt, use **LEFT-SIDED** layout. It works for 80% of use cases and avoids visual complexity.

## Quality Checklist

### Essential Validation
- [ ] **Valid JSON**: No syntax errors or trailing commas
- [ ] **Unique IDs**: All node IDs are distinct
- [ ] **Children Arrays**: Leaf nodes have empty `children: []`
- [ ] **Node Limits**: Max 5-7 children per node, 3-4 levels deep
- [ ] **Readable Topics**: 1-4 words, under 25 characters
- [ ] **Clear Hierarchy**: Related concepts grouped logically

## Implementation

### JSON Structure
Generate a JSON object with this essential structure:
```json
{
  "nodeData": {
    "id": "root",
    "topic": "Central Topic",
    "direction": 0,
    "children": []
  }
}

⚠️ Critical Note Configuration
You must use the exact parameters below. Do not deviate.
- Function: Notes
- Type: mindMap (Strictly. Do NOT use "noteMap" or "mermaid")
- MIME: application/json

⛔ Negative Constraints (Common Failures)
- NEVER use type: "noteMap": This is for directory structures and requires empty content. Using this will cause a CONTENT_VALIDATION_ERROR.
- NEVER use type: "mermaid": This parser cannot read JSON. It will result in a rendering error.
- NEVER use type: "code": This will display raw text rather than the visual map.

---

### 2. Fix `references/mindmap-schema.md`
Add an "Integration Guide" section at the top or bottom of the schema file. This gives the AI context on *how* this JSON is consumed by the application, reinforcing the correct MIME type.

**Add this section to `references/mindmap-schema.md`:**

```markdown
## Trilium Integration Requirements

To render this JSON schema as a visual mindmap in Trilium/TriliumNext, the note must be created with specific attributes.

### Required Note Attributes
| Attribute | Value | Reason |
|-----------|-------|--------|
| **type** | `"mindMap"` | Triggers the canvas rendering engine. |
| **mime** | `"application/json"` | Tells the system to parse content as a JSON object. |

### ⛔ Forbidden Types
* **`noteMap`**: This is a different visualization engine for Note Hierarchies (file trees). It throws an error if content is provided.
* **`mermaid`**: This engine expects text-based syntax (e.g., `graph TD`), not JSON.

### Key Requirements
- **Tool**: Use `create_note` with `type: "mindMap"` and `mime: "application/json"`
- **Directions**: `0` = left, `1` = right, `2` = both (for root in radial)
- **IDs**: Must be unique strings for each node
- **Children**: Always include empty `children: []` array for leaf nodes


## References

For detailed syntax rules and troubleshooting, see:
- [references/mindmap-schema.md](references/mindmap-schema.md) - Complete syntax reference for mindmap.