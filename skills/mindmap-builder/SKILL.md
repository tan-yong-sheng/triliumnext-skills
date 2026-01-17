---
name: mindmap-builder
description: Create and edit mind maps to organize ideas hierarchically and visualize concepts. Use for mind maps, flowcharts, brainstorming, and structured concept mapping.

---

# Mindmap Builder

## Overview

Create hierarchical mindmaps from text content and save them directly to TriliumNext using the MCP tool.

## Workflow

1. **Analyze Content**: Identify the central topic, main branches, and sub-concepts
2. **Structure Hierarchy**: Organize ideas into a tree structure with appropriate nesting
3. **Balance Layout**: Distribute branches between left (direction: 0) and right (direction: 1) sides
4. **Apply Styling**: Choose appropriate theme and colors for visual appeal
5. **Generate JSON**: Construct the complete mindmap JSON structure
6. **Save to TriliumNext**: Use the `create_note` MCP tool to save the mindmap

## Mindmap Structure Guide

### Central Topic
- Place the main subject at the center (root node)
- Use clear, concise wording
- Apply root-level styling for emphasis

### Branch Organization
- **Left side (direction: 0)**: Typically for inputs, causes, problems, or past
- **Right side (direction: 1)**: Typically for outputs, effects, solutions, or future
- **Balanced distribution**: Aim for roughly equal content on both sides

### Hierarchy Levels
- **Level 1**: Main categories/themes (direct children of root)
- **Level 2**: Subcategories or specific items
- **Level 3+**: Details, examples, or further breakdowns
- **Limit depth**: Keep to 4-5 levels maximum for clarity

## Content Analysis Patterns

### Topic Exploration
When users want to explore a topic:
- Central topic → Main aspects → Specific elements → Examples/details

### Problem-Solution Structure
- Left: Problems, challenges, current state
- Right: Solutions, opportunities, future state

### Process or System
- Left: Inputs, prerequisites, preparation
- Right: Outputs, results, outcomes

### Comparison or Analysis
- Left: Option A, traditional approach, pros
- Right: Option B, modern approach, cons

## Styling Guidelines

### Theme Selection
- **Dark theme**: Professional presentations, technical topics
- **Light theme**: Educational content, collaborative work
- **Custom colors**: Match brand or topic (e.g., green for environmental topics)

### Color Coding
- Use consistent colors for related concepts
- Apply palette colors from theme for harmony
- Highlight important nodes with contrasting colors

### Typography
- Root node: Larger font size (24px+)
- Main branches: Medium size (18-20px)
- Sub-items: Standard size (14-16px)
- Use bold for emphasis on key concepts

## JSON Generation Rules

1. **Unique IDs**: Generate unique identifiers for each node
2. **Direction Balance**: Alternate between left (0) and right (1) for main branches
3. **Style Consistency**: Use theme colors and maintain visual hierarchy
4. **Complete Structure**: Include all required fields (see schema reference)
5. **Validation**: Ensure proper nesting and valid JSON syntax

For detailed JSON structure, see [references/mindmap-schema.md](references/mindmap-schema.md)

## Common Mindmap Types

### Knowledge Organization
```
Central Topic
├── Category 1 (left)
│   ├── Subcategory A
│   └── Subcategory B
└── Category 2 (right)
    ├── Subcategory C
    └── Subcategory D
```

### Project Planning
```
Project Name
├── Requirements (left)
├── Resources (left)
├── Timeline (right)
└── Deliverables (right)
```

### Decision Making
```
Decision Point
├── Factors (left)
│   ├── Pros
│   └── Cons
└── Options (right)
    ├── Option A
    └── Option B
```

## TriliumNext Integration

### Tool Call Format
Use the `create_note` tool from `triliumnext-mcp`:

```javascript
create_note({
    title: "Topic Name - Mindmap",
    content: JSON.stringify(mindmapData),
    type: "code",
    mime: "application/json"
})
```

### Content Parameter
- Pass the complete JSON structure as a stringified object
- Do NOT wrap in code blocks within the function call
- Ensure valid JSON syntax before calling

### Note Organization
- Use descriptive titles: "[Topic] - Mindmap"
- Consider adding labels for categorization
- Link related mindmaps using relations

## Example Workflow

**User Request**: "Create a mindmap for learning JavaScript"

**Analysis**:
- Central topic: "Learning JavaScript"
- Left side: Fundamentals, basics, prerequisites
- Right side: Advanced topics, projects, career paths

**Structure**:
```
Learning JavaScript
├── Fundamentals (left)
│   ├── Variables & Data Types
│   ├── Functions
│   └── Control Structures
├── Core Concepts (left)
│   ├── DOM Manipulation
│   └── Event Handling
├── Advanced Topics (right)
│   ├── Async Programming
│   ├── ES6+ Features
│   └── Frameworks
└── Practice (right)
    ├── Projects
    └── Coding Challenges
```

**Styling**: Use professional theme with color-coding by difficulty level

## Best Practices

1. **Clarity**: Use clear, concise node text
2. **Balance**: Distribute content evenly between sides
3. **Hierarchy**: Maintain logical parent-child relationships
4. **Visual Appeal**: Apply consistent styling and colors
5. **Completeness**: Include all relevant subtopics without overwhelming
6. **Actionability**: Make nodes specific enough to be useful

## Quality Checklist

Before generating the final JSON:
- [ ] Central topic clearly defined
- [ ] Balanced left/right distribution
- [ ] Logical hierarchy with appropriate nesting
- [ ] Consistent styling applied
- [ ] Unique IDs for all nodes
- [ ] Valid JSON structure
- [ ] Appropriate theme selected
- [ ] All required fields present

## Error Prevention

- **Invalid JSON**: Always validate syntax before output
- **Missing IDs**: Ensure every node has a unique identifier
- **Unbalanced structure**: Check left/right distribution
- **Inconsistent styling**: Apply theme colors systematically
- **Deep nesting**: Limit to 4-5 levels for readability
