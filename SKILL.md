---
name: obsidian-canvas-creator-skill
description: Create Obsidian Canvas files from text content, supporting both MindMap and freeform layouts. Use this skill when users want to visualize content as an interactive canvas, create mind maps, or organize information spatially in Obsidian format.
license: MIT
activation: /obsidian-canvas-creator-skill
metadata:
  author: pix
  version: 1.0.0
  created: 2026-09-20
  last_reviewed: 2026-09-21
  review_interval_days: 90
  tags: [obsidian, canvas, mindmap, visualization, json, canvas-file]
provenance:
  maintainer: pix
  source_references: [references/canvas-spec.md, references/layout-algorithms.md]
---

# Obsidian Canvas Creator

Transform text content into structured Obsidian Canvas files with support for MindMap and freeform layouts.

## When to Use This Skill

- User requests to create a canvas, mind map, or visual diagram from text
- User wants to organize information spatially
- User mentions "Obsidian Canvas" or similar visualization tools
- Converting structured content (articles, notes, outlines) into visual format

## Data Source

This skill operates on user-provided text content. No external APIs or data sources are required.

### Input Types

- **Plain Text**: Raw text content to visualize
- **Markdown Content**: Structured with headings, lists, emphasis
- **Structured Outlines**: Hierarchical bullet points or numbered lists
- **Articles**: Full documents with sections and subsections

### Data Flow

1. User provides text content
2. Skill analyzes content structure
3. Skill determines layout type (MindMap or Freeform)
4. Skill generates JSON Canvas structure
5. Output is a valid `.canvas` file

### No External Dependencies

This skill uses only Python standard library. No API keys, network access, or external services required.

## Core Workflow

### 1. Analyze Content

Read and understand the input content:

- Identify main topics and hierarchical relationships
- Extract key points, facts, and supporting details
- Note any existing structure (headings, lists, sections)

### 2. Determine Layout Type

Ask user to choose or infer from context:

**MindMap Layout:**

- Radial structure from center
- Parent-child relationships
- Clear hierarchy
- Good for: brainstorming, topic exploration, hierarchical content

**Freeform Layout:**

- Custom positioning
- Flexible relationships
- Multiple connection types
- Good for: complex networks, non-hierarchical content, custom arrangements

### 3. Plan Structure

**For MindMap:**

- Identify central concept (root node)
- Map primary branches (main topics)
- Organize secondary branches (subtopics)
- Position leaf nodes (details)

**For Freeform:**

- Group related concepts
- Identify connection patterns
- Plan spatial zones
- Consider visual flow

### 4. Generate Canvas

Create JSON following the Canvas specification:

**Node Creation:**

- Assign unique 8-12 character hex IDs
- Set appropriate dimensions based on content length
- Apply consistent color schemes
- Ensure no coordinate overlaps

**Edge Creation:**

- Connect parent-child relationships
- Use appropriate arrow styles
- Add labels for complex relationships
- Choose line styles (straight for hierarchy, curved for cross-references)

**Grouping (Optional):**

- Create visual containers for related nodes
- Use subtle background colors
- Add descriptive labels

### 5. Apply Layout Algorithm

**MindMap Layout Calculations:**

Refer to `references/layout-algorithms.md` for detailed algorithms. Key principles:

- Center root at (0, 0)
- Distribute primary nodes radially
- Space secondary nodes based on sibling count
- Maintain minimum spacing: 320px horizontal, 200px vertical

**Freeform Layout Principles:**

- Start with logical groupings
- Position groups with clear separation
- Connect across groups with curved edges
- Balance visual weight across canvas

### 6. Validate and Output

Before outputting:

**Validation Checklist:**

- All nodes have unique IDs
- No coordinate overlaps (check distance > node dimensions + spacing)
- All edges reference valid node IDs
- Groups (if any) have labels
- Colors use consistent format (hex or preset numbers)
- JSON is properly escaped (Chinese quotes: 『』 for double, 「」 for single)

**Output Format:**

- Complete, valid JSON Canvas file
- No additional explanation text
- Directly importable into Obsidian

## Node Sizing Guidelines

**Text Length-Based Sizing:**

- Short text (<30 chars): 220 × 100 px
- Medium text (30-60 chars): 260 × 120 px  
- Long text (60-100 chars): 320 × 140 px
- Very long text (>100 chars): 320 × 180 px

## Color Schemes

**Preset Colors (Recommended):**

- `"1"` - Red (warnings, important)
- `"2"` - Orange (action items)
- `"3"` - Yellow (questions, notes)
- `"4"` - Green (positive, completed)
- `"5"` - Cyan (information, details)
- `"6"` - Purple (concepts, abstract)

**Custom Hex Colors:**
Use for brand consistency or specific themes. Always use uppercase format: `"#4A90E2"`

## Critical Rules

1. **Quote Handling:**
   - Chinese double quotes → 『』
   - Chinese single quotes → 「」
   - English double quotes → `\"`

2. **ID Generation:**
   - 8-12 character random hex strings
   - Must be unique across all nodes and edges

3. **Z-Index Order:**
   - Output groups first (bottom layer)
   - Then subgroups
   - Finally text/link nodes (top layer)

4. **Spacing Requirements:**
   - Minimum horizontal: 320px between node centers
   - Minimum vertical: 200px between node centers
   - Account for node dimensions when calculating

5. **JSON Structure:**
   - Top level contains only `nodes` and `edges` arrays
   - No extra wrapping objects
   - No comments in output

## Examples

### Example 1: Simple MindMap Request

User: "Create a mind map about solar system planets"

**Process:**

1. Analyze content: Solar system has planets, dwarf planets, moons
2. Determine layout: MindMap (hierarchical structure)
3. Identify center: "Solar System"
4. Primary branches: Inner Planets, Outer Planets, Dwarf Planets
5. Secondary nodes: Individual planets with key facts
6. Apply radial layout with 400px radius
7. Generate JSON with proper spacing

**Output Structure:**
```json
{
  "nodes": [
    {"id": "center", "type": "text", "text": "# Solar System", "x": -150, "y": -60, "width": 300, "height": 120},
    {"id": "inner", "type": "text", "text": "Inner Planets", "x": 400, "y": -200, "width": 200, "height": 80},
    {"id": "outer", "type": "text", "text": "Outer Planets", "x": 400, "y": 200, "width": 200, "height": 80}
  ],
  "edges": [
    {"id": "e1", "fromNode": "center", "toNode": "inner", "toEnd": "arrow"},
    {"id": "e2", "fromNode": "center", "toNode": "outer", "toEnd": "arrow"}
  ]
}
```

### Example 2: Freeform Content Request

User: "Turn this article into a canvas" + [article text]

**Input:**
```
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

**Process:**

1. Extract article structure (intro, body sections, conclusion)
2. Identify key concepts and relationships
3. Group related sections spatially
4. Connect with labeled edges
5. Apply freeform layout with clear zones

**Output Structure:**
- Central "Machine Learning" node
- Three main groups: Supervised, Unsupervised, Deep Learning
- Individual technique nodes within each group
- Connections showing relationships

### Example 3: Project Structure Visualization

User: "Visualize our project structure: Frontend (React, TypeScript, Tailwind), Backend (Node.js, Express, PostgreSQL), DevOps (Docker, GitHub Actions, AWS)"

**Process:**

1. Analyze content: Three main layers with technologies
2. Determine layout: Freeform with groups
3. Create three main groups for each layer
4. Add technology nodes within each group
5. Show dependencies with edges

**Output Structure:**
```json
{
  "nodes": [
    {"id": "frontend", "type": "group", "label": "Frontend", "x": 0, "y": 0, "width": 300, "height": 200},
    {"id": "react", "type": "text", "text": "React", "x": 20, "y": 40, "width": 120, "height": 60},
    {"id": "typescript", "type": "text", "text": "TypeScript", "x": 160, "y": 40, "width": 120, "height": 60}
  ],
  "edges": [
    {"id": "e1", "fromNode": "react", "toNode": "typescript", "label": "uses"}
  ]
}
```

### Example 4: Meeting Notes Canvas

User: "Create a canvas from these meeting notes: Q1 Results (Revenue up 15%, Costs down 8%), Q2 Goals (Launch new feature, Hire 3 engineers), Action Items (Design review by Friday, API docs by next week)"

**Process:**

1. Analyze content: Three sections with items
2. Determine layout: Freeform with timeline or grouped
3. Create groups for each section
4. Color-code by priority
5. Connect related items

**Output Structure:**
- Timeline layout from left to right
- Q1, Q2, and Action Items as main nodes
- Individual items as child nodes
- Edges showing dependencies

### Example 5: Knowledge Map Creation

User: "Make a knowledge map about Python programming: Core (Variables, Control Flow, Functions), OOP (Classes, Inheritance, Polymorphism), Libraries (NumPy, Pandas, Matplotlib)"

**Process:**

1. Analyze content: Three main areas with subtopics
2. Determine layout: MindMap (hierarchical)
3. Create central "Python Programming" node
4. Add three main branches
5. Position specific library nodes with descriptions

**Output Structure:**
```json
{
  "nodes": [
    {"id": "python", "type": "text", "text": "# Python Programming", "x": -150, "y": -60, "width": 300, "height": 120, "color": "4"},
    {"id": "core", "type": "text", "text": "Core Concepts", "x": 400, "y": -200, "width": 200, "height": 80, "color": "5"},
    {"id": "oop", "type": "text", "text": "OOP", "x": 400, "y": 0, "width": 200, "height": 80, "color": "6"},
    {"id": "libs", "type": "text", "text": "Libraries", "x": 400, "y": 200, "width": 200, "height": 80, "color": "3"}
  ],
  "edges": [
    {"id": "e1", "fromNode": "python", "toNode": "core", "toEnd": "arrow"},
    {"id": "e2", "fromNode": "python", "toNode": "oop", "toEnd": "arrow"},
    {"id": "e3", "fromNode": "python", "toNode": "libs", "toEnd": "arrow"}
  ]
}
```

### Example 6: Process Flow Diagram

User: "Create a flowchart for user registration: Start → Enter Email → Validate Email → Create Account → Send Welcome Email → End"

**Process:**

1. Analyze content: Linear process with steps
2. Determine layout: Timeline or tree layout
3. Create sequential nodes
4. Connect with directional edges
5. Add decision points if needed

**Output Structure:**
- Horizontal timeline layout
- Each step as a node
- Arrows showing flow direction
- Color coding for different types of steps

## Reference Documents

Read these references for detailed information:

- Read `references/canvas-spec.md` for complete JSON Canvas format specification and edge cases
- Read `references/layout-algorithms.md` for detailed positioning algorithms for both MindMap and freeform layouts

## Scripts

This skill does not require external scripts. All canvas generation logic is handled directly by the agent using the algorithms and specifications provided in the reference documents.

### Validation Commands

For manual validation of generated canvas files:

```bash
# Validate JSON syntax
python3 -c "import json; json.load(open('output.canvas'))"

# Check node ID uniqueness
python3 -c "
import json
data = json.load(open('output.canvas'))
ids = [n['id'] for n in data.get('nodes', [])]
ids += [e['id'] for e in data.get('edges', [])]
print('All IDs unique:', len(ids) == len(set(ids)))
"
```

## Analyses

For detailed content analysis methods and canvas generation analysis, read
`references/analysis-and-errors.md`. This includes:

- Structure detection and hierarchy extraction
- Layout recommendation algorithms
- Node sizing and color assignment
- Edge routing and quality metrics

## Errors

For comprehensive error handling and prevention procedures, read
`references/analysis-and-errors.md`. This includes:

- Common errors and solutions
- Error prevention strategies
- Validation steps
- Quality metrics

## Keywords

obsidian, canvas, mindmap, visualization, json, canvas-file, diagram, spatial-organization, knowledge-management, note-taking, visual-thinking, concept-mapping, flowchart, network-diagram, hierarchical-structure, radial-layout, freeform-layout, node-positioning, edge-connection, color-coding, grouping, z-index, collision-detection, spacing-algorithm, content-analysis, structure-extraction

## Tips for Quality Canvases

1. **Keep text concise**: Each node should be scannable (<2 lines preferred)
2. **Use hierarchy**: Group by importance and relationship
3. **Balance the canvas**: Distribute nodes to avoid clustering
4. **Strategic colors**: Use colors to encode meaning, not just decoration
5. **Meaningful connections**: Only add edges that clarify relationships
6. **Test in Obsidian**: Verify the output opens correctly

## Common Pitfalls to Avoid

- Overlapping nodes (always check distances)
- Inconsistent quote escaping (breaks JSON parsing)
- Missing group labels (causes sidebar navigation issues)
- Too much text in nodes (use file nodes for long content)
- Duplicate IDs (each must be unique)
- Unconnected nodes (unless intentional islands)

## Gotchas

- Obsidian Canvas files require specific JSON structure with `nodes` and `edges` arrays only
- Chinese quotes must be converted: double quotes → 『』, single quotes → 「」
- Node IDs must be unique 8-12 character hex strings across entire canvas
- Minimum spacing between nodes: 320px horizontal, 200px vertical
- Z-index order matters: groups must come before text nodes for proper layering
