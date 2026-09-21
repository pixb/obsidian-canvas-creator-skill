# Obsidian Canvas Creator Skill

## Purpose

Transform text content into structured Obsidian Canvas files (.canvas) with support for MindMap and freeform layouts.

## When to Use

- Creating visual mind maps from text content
- Organizing information spatially in Obsidian
- Converting articles, notes, or outlines into interactive canvas files
- Building diagrams with nodes and connections

## Input Format

Accepts:
- Plain text
- Markdown content
- Structured outlines
- Articles with headings and sections

## Output

Generates valid JSON Canvas files (.canvas) that can be opened directly in Obsidian.

## Key Files

- `SKILL.md` - Main skill instructions
- `references/canvas-spec.md` - JSON Canvas format specification
- `references/layout-algorithms.md` - Positioning algorithms for layouts
- `assets/` - Template canvas files

## Workflow

1. Analyze input content structure
2. Choose layout type (MindMap or Freeform)
3. Plan node hierarchy and connections
4. Generate JSON with proper positioning
5. Validate and output .canvas file
