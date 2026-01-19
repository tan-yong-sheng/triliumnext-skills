# TriliumNext Skills

A collection of visual skills for [TriliumNext](https://github.com/TriliumNext/TriliumNext) that transform text content into interactive diagrams and visual representations. These skills work seamlessly with [triliumnext-mcp](https://github.com/tan-yong-sheng/triliumnext-mcp) to create professional visualizations directly in your TriliumNext notes.

## 📦 Installation

```bash
/plugin marketplace add tan-yong-sheng/triliumnext-skills
/plugin install triliumnext-skills
```

## 🎯 Prerequisites

This plugin requires [triliumnext-mcp](https://github.com/tan-yong-sheng/triliumnext-mcp) to be installed and configured for full functionality.

## 🎨 Available Skills

### 1. Excalidraw Diagram Generator
**Skill Name:** `excalidraw-drawer`

Transform text descriptions into beautiful hand-drawn style diagrams using Excalidraw.

**Use Cases:**
- Flowcharts and process diagrams
- Mind maps and brainstorming visuals
- System architecture diagrams
- Organizational charts
- Timeline visualizations
- Matrix and comparison charts

**Trigger Keywords:** "Excalidraw", "Diagram", "Flowchart", "Mind Map", "Visualize"

**Features:**
- Professional hand-drawn aesthetic
- 8 different diagram types (flowchart, mind map, hierarchy, relationship, comparison, timeline, matrix, freeform)
- Consistent color palette and typography
- Canvas-optimized layout (1200x800)
- Interactive elements with proper spacing

**Example Usage:**
```
Create an Excalidraw diagram showing our software development workflow
```

### 2. Mermaid Visualizer
**Skill Name:** `mermaid-visualizer`

Create clean, professional Mermaid diagrams with automatic syntax error prevention.

**Use Cases:**
- Process flows and workflows
- System architectures
- Sequence diagrams for API interactions
- State diagrams for system states
- Comparison diagrams
- Circular flow processes

**Trigger Keywords:** "Mermaid", "Flowchart", "Sequence", "State", "Process Flow"

**Features:**
- 6 diagram types with smart type selection
- Automatic syntax validation and error prevention
- Professional color schemes with semantic meaning
- Multiple layout options (vertical, horizontal, circular)
- Detail level control (simple, standard, detailed, presentation)
- TriliumNext/GitHub compatible output

**Example Usage:**
```
Create a Mermaid sequence diagram showing user authentication flow
```

### 3. Mindmap Builder
**Skill Name:** `mindmap-builder`

Generate hierarchical mindmaps with cognitive load optimization following Miller's Rule (7±2).

**Use Cases:**
- Knowledge organization and categorization
- Topic breakdowns and analysis
- Educational content structure
- Research summaries
- Feature analysis
- Review organization

**Trigger Keywords:** "Mindmap", "Mind Map", "Organize", "Hierarchy", "Knowledge Map"

**Features:**
- Cognitive load management (max 5-7 children per node)
- Smart layout selection (left-sided, right-sided, radial)
- 4 visual styles (minimal, professional, colorful, academic)
- Automatic depth limiting (3-4 levels)
- Optimized node text length (1-4 words, max 25 characters)
- Layout decision framework for content type matching

**Example Usage:**
```
Create a mindmap organizing the key concepts from this AI research paper
```

## 🚀 How Skills Work

Each skill follows a consistent workflow:

1. **Content Analysis** - Understanding the input and identifying key concepts
2. **Type Selection** - Choosing the most appropriate visualization method
3. **Configuration** - Applying layout, style, and detail settings
4. **Generation** - Creating the structured output (JSON/Mermaid/Excalidraw)
5. **Note Creation** - Saving directly to TriliumNext via MCP tools

## 🎯 Skill Selection Guide

| Content Type | Recommended Skill | Best For |
|-------------|------------------|----------|
| **Process workflows** | Mermaid Visualizer | Step-by-step procedures, decision trees |
| **System architecture** | Excalidraw Drawer | Technical diagrams, component relationships |
| **Knowledge organization** | Mindmap Builder | Topic categorization, learning materials |
| **API interactions** | Mermaid Visualizer | Sequence diagrams, message flows |
| **Brainstorming results** | Excalidraw Drawer | Creative layouts, freeform organization |
| **Research summaries** | Mindmap Builder | Paper analysis, concept breakdowns |
| **Comparison analysis** | Any skill | Choose based on complexity and style preference |

## 🎨 Visual Styles & Themes

### Excalidraw Themes
- **Hand-drawn aesthetic** with consistent typography (Excalidraw font family)
- **Professional color palette** (blue tones, amber highlights, neutral grays)
- **Layout optimized** for 1200x800 canvas
- **Element variety** (rectangles, circles, diamonds, arrows)

### Mermaid Themes
- **Minimal** - Monochrome, clean lines
- **Professional** - Semantic colors, clear hierarchy (default)
- **Colorful** - Vibrant colors, high contrast
- **Academic** - Formal styling for documentation

### Mindmap Themes
- **Minimal** - Clean, high contrast, reduced visual noise
- **Professional** - Business-friendly with subtle colors
- **Colorful** - Vibrant, engaging colors for creativity
- **Academic** - Structured, formal appearance

## 🔧 Technical Details

### Output Formats
- **Excalidraw**: JSON format with `type: "canvas"` and `mime: "application/json"`
- **Mermaid**: Text format with `type: "mermaid"` and `mime: "text/vnd.mermaid"`
- **Mindmap**: JSON format with `type: "mindMap"` and `mime: "application/json"`

### Quality Assurance
Each skill includes built-in validation:
- **Syntax error prevention** for rendering compatibility
- **Cognitive load optimization** following UX best practices
- **Layout optimization** for readability
- **Consistent styling** across all outputs

## 📚 References & Inspiration

- **Excalidraw Schema**: [references/excalidraw-schema.md](skills/excalidraw-drawer/references/excalidraw-schema.md)
- **Mermaid Syntax Rules**: [references/syntax-rules.md](skills/mermaid-visualizer/references/syntax-rules.md)
- **Mindmap Schema**: [references/mindmap-schema.md](skills/mindmap-builder/references/mindmap-schema.md)

## 🏗️ External Dependencies

| Requirement | Purpose | Documentation |
|------------|---------|---------------|
| [triliumnext-mcp](https://github.com/tan-yong-sheng/triliumnext-mcp) | Note creation and management | Required for saving visualizations |
| [TriliumNext](https://github.com/TriliumNext/TriliumNext) | Host application | Desktop mind mapping application |
| [mind-elixir.com](https://desktop.mind-elixir.com/zh#) | Mindmap rendering | For mindmap visualization |
| [Reveal.js integration](https://docs.triliumnotes.org/user-guide/collections/presentation) | Presentation mode | For slide-based workflows |

## 🤝 Credits

Inspired by:
- [axton-obsidian-visual-skills](https://github.com/axtonliu/axton-obsidian-visual-skills) - Visual skills concept and structure
- [obsidian-skills](https://github.com/kepano/obsidian-skills) - Skills framework design

## 📄 License

This project follows the same license as TriliumNext. See the [TriliumNext repository](https://github.com/TriliumNext/TriliumNext) for details.

## 🐛 Issues & Contributions

- **Issues**: Report problems at [GitHub Issues](https://github.com/tan-yong-sheng/triliumnext-skills/issues)
- **Contributions**: Pull requests welcome for new skills, improvements, and bug fixes
- **Discussions**: Join the TriliumNext community for questions and feature requests

---

**Quick Start Example:**
```
User: "Create a flowchart showing our customer onboarding process"
Claude: [Analyzes content → Selects Mermaid → Generates professional flowchart → Saves to TriliumNext]
```

Transform your text into visuals effortlessly! 🎨✨