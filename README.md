# Obsidian Canvas Creator Skill

Create Obsidian Canvas files from text content, supporting both MindMap and freeform layouts.

## Installation

### Prerequisites

- Obsidian with Canvas plugin enabled
- Python 3.7+ (for running validation scripts)
- opencode agent platform

### Install for opencode

```bash
# Clone or copy this skill to your opencode skills directory
cp -r obsidian-canvas-creator-skill ~/.config/opencode/skills/

# The skill is now available at:
# /obsidian-canvas-creator-skill
```

### Install for Other Platforms

#### Cursor

Copy the skill directory to:
- `~/.cursor/skills/obsidian-canvas-creator-skill/`

#### Windsurf

Copy the skill directory to:
- `~/.windsurf/skills/obsidian-canvas-creator-skill/`

#### Manual Installation

1. Copy the skill directory to your agent's skills folder
2. Ensure the directory structure is preserved
3. Restart your agent if needed

## Usage

### Basic MindMap Creation

```
/obsidian-canvas-creator-skill Create a mind map about solar system planets
```

### Freeform Layout

```
/obsidian-canvas-creator-skill Turn this article into a canvas: [paste article text]
```

### With Specific Content

```
/obsidian-canvas-creator-skill Create a visual diagram from these notes:
- Project A: Frontend, Backend, Database
- Project B: API, Documentation
- Dependencies: Shared authentication module
```

## Examples

### Example 1: Solar System Mind Map

**Input:**
```
/obsidian-canvas-creator-skill Create a mind map about solar system planets
```

**Output:**
A canvas file with:
- Central node: "Solar System"
- Primary branches: Inner Planets, Outer Planets, Dwarf Planets
- Secondary nodes: Individual planets with key facts
- Proper spacing and connections

### Example 2: Article to Canvas

**Input:**
```
/obsidian-canvas-creator-skill Turn this article into a canvas:

# Machine Learning Basics

## Supervised Learning
- Classification
- Regression

## Unsupervised Learning
- Clustering
- Dimensionality Reduction

## Deep Learning
- Neural Networks
- CNNs
- RNNs
```

**Output:**
A canvas file with:
- Hierarchical structure matching article sections
- Groups for each learning type
- Connected related concepts

### Example 3: Project Structure

**Input:**
```
/obsidian-canvas-creator-skill Visualize our project structure:
- Frontend: React, TypeScript, Tailwind
- Backend: Node.js, Express, PostgreSQL
- DevOps: Docker, GitHub Actions, AWS
```

**Output:**
A canvas file with:
- Three main groups for each layer
- Individual technology nodes
- Dependency connections

### Example 4: Meeting Notes

**Input:**
```
/obsidian-canvas-creator-skill Create a canvas from these meeting notes:
- Q1 Results: Revenue up 15%, Costs down 8%
- Q2 Goals: Launch new feature, Hire 3 engineers
- Action Items: Design review by Friday, API docs by next week
```

**Output:**
A canvas file with:
- Timeline or grouped layout
- Color-coded by priority
- Connected related items

### Example 5: Knowledge Map

**Input:**
```
/obsidian-canvas-creator-skill Make a knowledge map about Python programming:
- Core: Variables, Control Flow, Functions
- OOP: Classes, Inheritance, Polymorphism
- Libraries: NumPy, Pandas, Matplotlib
```

**Output:**
A canvas file with:
- Central "Python Programming" node
- Three main branches
- Specific library nodes with descriptions

## Configuration

### Layout Types

#### MindMap Layout
- Best for: Hierarchical content, brainstorming, topic exploration
- Structure: Radial from center, parent-child relationships
- Colors: Use semantic colors (green for positive, red for warnings)

#### Freeform Layout
- Best for: Complex networks, non-hierarchical content
- Structure: Custom positioning, flexible relationships
- Groups: Use for visual organization

### Node Sizing

| Text Length | Recommended Size |
|-------------|------------------|
| Short (<30 chars) | 220 × 100 px |
| Medium (30-60 chars) | 260 × 120 px |
| Long (60-100 chars) | 320 × 140 px |
| Very long (>100 chars) | 320 × 180 px |

### Color Scheme

Preset colors (recommended):
- `"1"` - Red (warnings, important)
- `"2"` - Orange (action items)
- `"3"` - Yellow (questions, notes)
- `"4"` - Green (positive, completed)
- `"5"` - Cyan (information, details)
- `"6"` - Purple (concepts, abstract)

## Troubleshooting

### Canvas Won't Open in Obsidian

**Solution:**
1. Validate JSON syntax
2. Check all node IDs are unique
3. Verify edge references exist
4. Ensure required fields are present

### Nodes Appear Overlapped

**Solution:**
1. Increase spacing between coordinates
2. Account for node dimensions
3. Use minimum spacing: 320px horizontal, 200px vertical

### Colors Don't Match Expectations

**Solution:**
1. Use consistent color format (all hex OR all presets)
2. Remember presets adapt to theme
3. Test in both light and dark mode

### Text Appears Truncated

**Solution:**
1. Increase node dimensions
2. Break long text into multiple nodes
3. Use file nodes for lengthy content

### JSON Parsing Errors

**Solution:**
1. Validate JSON structure
2. Check for proper quote escaping
3. Ensure Chinese quotes are converted: `"` → `『』`, `'` → `「」`

## Performance Tips

- Keep node count reasonable (<500 for smooth performance)
- Use compressed images for backgrounds
- Keep node text concise; use file nodes for long content
- Minimize crossing edges for clarity

## Validation

```bash
# Validate skill structure
python3 scripts/validate.py .

# Run security scan
python3 scripts/security_scan.py .

# Run all gates
python3 scripts/skill_graph.py run . --jobs 4
```

## Contributing

1. Follow the skill structure guidelines
2. Add tests for new functionality
3. Update documentation
4. Run validation before submitting

## License

MIT License

## Support

For issues or questions:
- Check the troubleshooting section
- Review the canvas specification in `references/canvas-spec.md`
- See layout algorithms in `references/layout-algorithms.md`
