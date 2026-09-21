# Content Analysis and Error Handling

Detailed analysis methods and error handling procedures for canvas generation.

## Content Analysis

### Structure Detection

Before generating canvas, analyze input content:

1. **Heading Detection**
   - Identify H1, H2, H3 headings
   - Extract hierarchy from heading levels
   - Map headings to node importance

2. **List Detection**
   - Bulleted lists (unordered)
   - Numbered lists (ordered)
   - Nested list structures

3. **Paragraph Recognition**
   - Identify text blocks
   - Extract key sentences
   - Determine content length

4. **Concept Extraction**
   - Key nouns and phrases
   - Action verbs and relationships
   - Technical terms and definitions

### Hierarchy Extraction

1. **Parent-Child Relationships**
   - Direct parent-child from headings
   - Implied hierarchy from content
   - Cross-reference connections

2. **Sequential vs Parallel**
   - Linear processes (sequential)
   - Independent concepts (parallel)
   - Mixed structures

3. **Grouping Opportunities**
   - Related concepts
   - Common themes
   - Logical clusters

4. **Cross-References**
   - Explicit references
   - Implicit connections
   - Shared concepts

### Layout Recommendation

1. **MindMap Layout**
   - Hierarchical content
   - Single central concept
   - Parent-child relationships
   - Examples: outlines, taxonomies, decision trees

2. **Freeform Layout**
   - Network structures
   - Multiple relationships
   - Non-hierarchical connections
   - Examples: knowledge graphs, concept maps, process flows

3. **Hybrid Approach**
   - Mixed content types
   - Multiple hierarchies
   - Complex relationships

## Canvas Generation Analysis

### Node Sizing

1. **Text Length Calculation**
   - Count characters
   - Estimate line breaks
   - Consider font rendering

2. **Sizing Guidelines**
   - Short text (<30 chars): 220 × 100 px
   - Medium text (30-60 chars): 260 × 120 px
   - Long text (60-100 chars): 320 × 140 px
   - Very long text (>100 chars): 320 × 180 px

3. **Readability Check**
   - Default zoom level
   - Screen resolution
   - Text contrast

### Color Assignment

1. **Semantic Mapping**
   - Red (`"1"`): Warnings, important, negative
   - Orange (`"2"`): Action items, deadlines
   - Yellow (`"3"`): Questions, notes, neutral
   - Green (`"4"`): Positive, completed, good
   - Cyan (`"5"`): Information, details, neutral
   - Purple (`"6"`): Concepts, abstract, creative

2. **Consistency Rules**
   - Same concept = same color
   - Similar concepts = similar colors
   - Avoid random color usage

3. **Accessibility**
   - Contrast ratios
   - Color blindness considerations
   - Theme compatibility

### Edge Routing

1. **Minimize Crossings**
   - Optimal node positioning
   - Edge bundling
   - Layered layouts

2. **Connection Points**
   - Nearest sides
   - Directional flow
   - Avoid long edges

3. **Label Placement**
   - Center of edge
   - Avoid overlaps
   - Readable orientation

## Quality Metrics

### Completeness Check

- All content represented as nodes
- All relationships shown as edges
- No missing important concepts

### Readability Check

- Text sizes appropriate
- Colors consistent
- Spacing adequate
- Edges clear

### Balance Check

- Visual weight distributed
- No clustering
- Center of mass near origin

### Performance Check

- Node count reasonable (<500)
- Edge count manageable
- No excessive crossings

## Error Prevention

### Validation Steps

1. **JSON Syntax**
   - Valid JSON structure
   - Proper escaping
   - No syntax errors

2. **Node Validation**
   - Unique IDs
   - Required fields present
   - Valid types

3. **Edge Validation**
   - Reference valid nodes
   - No duplicate edges
   - Valid connection points

4. **Layout Validation**
   - Minimum spacing
   - No overlaps
   - Proper z-index order

### Common Issues

1. **Duplicate IDs**
   - Generate unique hex strings
   - Check for collisions
   - Verify before output

2. **Missing Fields**
   - Validate required attributes
   - Provide defaults where appropriate
   - Check edge references

3. **Spacing Violations**
   - Apply collision detection
   - Adjust positions
   - Verify minimum distances

4. **Quote Encoding**
   - Convert Chinese quotes
   - Escape special characters
   - Validate JSON strings
