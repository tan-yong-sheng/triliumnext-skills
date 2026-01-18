# Mindmap JSON Schema Reference

This document defines the complete JSON structure for mindmap data compatible with mindmap visualization tools.

## Root Structure

```json
{
  "nodeData": {
    "id": "unique-root-id",
    "topic": "Central Topic",
    "children": [...],
    "style": {...}
  },
  "arrows": [],
  "summaries": [],
  "direction": 2,
  "theme": {...}
}
```

## Node Structure

Each node (including root and children) follows this structure:

### Required Fields
- `id`: Unique identifier string (e.g., "bcc93d68bf00ed3e")
- `topic`: Display text for the node

### Optional Fields
- `children`: Array of child nodes (same structure)
- `direction`: 0 (left), 1 (right), or omitted for root
- `style`: Styling object

### Node Example
```json
{
  "id": "bcc94a3139eeb433",
  "topic": "Branch Topic",
  "direction": 0,
  "children": [
    {
      "id": "bcc952b42243432e",
      "topic": "Sub-topic",
      "children": []
    }
  ],
  "style": {
    "color": "#17a085",
    "background": "#e74c3c",
    "fontSize": "18px",
    "fontWeight": "bold"
  }
}
```

## Direction Values

- `0`: Left side of root
- `1`: Right side of root
- `2`: Both sides (root node only)
- Omitted: No specific direction (typically for root)

## Style Properties

### Available Style Options
- `color`: Text color (hex code)
- `background`: Background color (hex code)
- `fontSize`: Font size with units (e.g., "24px")
- `fontWeight`: Font weight ("normal", "bold", etc.)

### Style Examples
```json
{
  "style": {
    "fontSize": "24px"
  }
}

{
  "style": {
    "color": "#d35400",
    "fontSize": "24px",
    "fontWeight": "bold"
  }
}

{
  "style": {
    "background": "#f1c40e"
  }
}
```

## Theme Structure

The theme defines the overall appearance and color palette:

```json
{
  "theme": {
    "name": "Dark",
    "type": "dark",
    "palette": [
      "#848FA0", "#748BE9", "#D2F9FE", "#4145A5", "#789AFA",
      "#706CF4", "#EF987F", "#775DD5", "#FCEECF", "#DA7FBC"
    ],
    "cssVar": {
      "--node-gap-x": "30px",
      "--node-gap-y": "10px",
      "--main-gap-x": "65px",
      "--main-gap-y": "45px",
      "--root-radius": "30px",
      "--main-radius": "20px",
      "--root-color": "#ffffff",
      "--root-bgcolor": "#2d3748",
      "--root-border-color": "rgba(255, 255, 255, 0.1)",
      "--main-color": "#ffffff",
      "--main-bgcolor": "#4c4f69",
      "--topic-padding": "3px",
      "--color": "#cccccc",
      "--bgcolor": "#252526",
      "--selected": "#4dc4ff",
      "--accent-color": "#789AFA",
      "--panel-color": "#ffffff",
      "--panel-bgcolor": "#2d3748",
      "--panel-border-color": "#696969",
      "--map-padding": "50px 80px"
    }
  }
}
```

## Predefined Themes

### Dark Theme
- **Type**: "dark"
- **Primary colors**: Blues, purples, grays
- **Background**: Dark (#252526)
- **Text**: Light (#ffffff, #cccccc)

### Light Theme (Alternative)
```json
{
  "name": "Light",
  "type": "light",
  "palette": [
    "#2196F3", "#4CAF50", "#FF9800", "#9C27B0", "#F44336",
    "#00BCD4", "#795548", "#607D8B", "#FFC107", "#E91E63"
  ],
  "cssVar": {
    "--root-color": "#333333",
    "--root-bgcolor": "#ffffff",
    "--main-color": "#333333",
    "--main-bgcolor": "#f5f5f5",
    "--bgcolor": "#ffffff",
    "--color": "#333333"
  }
}
```

## Complete Example

```json
{
  "nodeData": {
    "id": "root-node-001",
    "topic": "Project Planning",
    "children": [
      {
        "topic": "Research Phase",
        "id": "node-left-001",
        "direction": 0,
        "children": [
          {
            "topic": "Market Analysis",
            "id": "node-left-child-001",
            "children": []
          },
          {
            "topic": "User Interviews",
            "id": "node-left-child-002",
            "children": []
          }
        ]
      },
      {
        "topic": "Development Phase",
        "id": "node-right-001",
        "direction": 1,
        "children": [
          {
            "topic": "Backend Setup",
            "id": "node-right-child-001",
            "style": {
              "background": "#4CAF50",
              "color": "#ffffff"
            }
          },
          {
            "topic": "Frontend Design",
            "id": "node-right-child-002",
            "style": {
              "background": "#2196F3",
              "color": "#ffffff"
            }
          }
        ]
      }
    ],
    "style": {
      "fontSize": "24px",
      "fontWeight": "bold"
    }
  },
  "arrows": [],
  "summaries": [],
  "direction": 2,
  "theme": {
    "name": "Professional",
    "type": "light",
    "palette": [
      "#2196F3", "#4CAF50", "#FF9800", "#9C27B0", "#F44336",
      "#00BCD4", "#795548", "#607D8B", "#FFC107", "#E91E63"
    ],
    "cssVar": {
      "--node-gap-x": "25px",
      "--node-gap-y": "15px",
      "--root-radius": "25px",
      "--main-radius": "15px",
      "--root-color": "#333333",
      "--root-bgcolor": "#ffffff",
      "--main-color": "#333333",
      "--main-bgcolor": "#f8f9fa"
    }
  }
}
```

## ID Generation Guidelines

- Use lowercase hexadecimal strings
- Length: 16 characters recommended
- Ensure uniqueness across all nodes in the mindmap
- Example pattern: "bcc93d68bf00ed3e", "node-001", "root-node-001"

## Best Practices

1. **Hierarchy**: Keep nesting levels reasonable (max 4-5 levels)
2. **Balance**: Distribute nodes between left and right sides
3. **Styling**: Use consistent color schemes within themes
4. **Performance**: Limit total nodes to under 100 for optimal rendering
5. **Accessibility**: Ensure sufficient color contrast in custom styles

## Layout Examples

### 1. Right-Oriented Mindmap
All branches extend to the right side only (direction: 1):

```json
{
  "nodeData": {
    "id": "bcc93d68bf00ed3e",
    "topic": "Main Topic",
    "children": [
      {
        "topic": "Branch 1",
        "id": "bcc94d2326965b73",
        "direction": 1,
        "children": [
          {
            "topic": "Sub-branch 1.1",
            "id": "bcc952b42243432e",
            "children": []
          }
        ]
      },
      {
        "topic": "Branch 2",
        "id": "bcc94c0787107540",
        "direction": 1,
        "children": []
      }
    ]
  },
  "direction": 1,
  "theme": {
    "name": "Dark",
    "type": "dark"
  }
}
```

### 2. Left-Oriented Mindmap
All branches extend to the left side only (direction: 0):

```json
{
  "nodeData": {
    "id": "bcc93d68bf00ed3e",
    "topic": "Main Topic",
    "children": [
      {
        "topic": "Branch 1",
        "id": "bcc94d2326965b73",
        "direction": 0,
        "children": [
          {
            "topic": "Sub-branch 1.1",
            "id": "bcc952b42243432e",
            "children": []
          }
        ]
      },
      {
        "topic": "Branch 2",
        "id": "bcc94c0787107540",
        "direction": 0,
        "children": []
      }
    ]
  },
  "direction": 0,
  "theme": {
    "name": "Dark",
    "type": "dark"
  }
}
```

### 3. Two-Sided Mindmap
Branches distributed on both left and right sides (direction: 2):

```json
{
  "nodeData": {
    "id": "bcc93d68bf00ed3e",
    "topic": "Central Topic",
    "children": [
      {
        "topic": "Left Branch 1",
        "id": "bcc94a3139eeb433",
        "direction": 0,
        "children": []
      },
      {
        "topic": "Left Branch 2",
        "id": "bcc94c9463e00b88",
        "direction": 0,
        "children": []
      },
      {
        "topic": "Right Branch 1",
        "id": "bcc94d2326965b73",
        "direction": 1,
        "children": [
          {
            "topic": "Sub-branch 1.1",
            "id": "bcc952b42243432e",
            "children": []
          }
        ]
      },
      {
        "topic": "Right Branch 2",
        "id": "bcc94c0787107540",
        "direction": 1,
        "children": []
      }
    ]
  },
  "direction": 2,
  "theme": {
    "name": "Dark",
    "type": "dark"
  }
}