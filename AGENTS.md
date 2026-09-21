# obsidian-canvas-creator-skill

Create Obsidian Canvas files from text content, supporting both MindMap and
freeform layouts. The user provides text, markdown, or structured content, and
this skill generates a valid JSON Canvas file (.canvas) that can be opened
directly in Obsidian.

## Activation

Invoke with `/obsidian-canvas-creator-skill <content description>`, or naturally:

- "Create a mind map about solar system planets"
- "Turn this article into a canvas"
- "Visualize this project structure"
- "Make a knowledge map about Python programming"

## How to use this file

This is the cross-tool companion file (AAIF format). The full skill
instructions — workflows, algorithms, validation rules, and examples — live in
[SKILL.md](SKILL.md) at this skill root. Read SKILL.md and follow it; treat
this file as the pointer, not the instructions.

## What this skill produces

This skill generates valid JSON Canvas files (.canvas) with:
- Properly positioned nodes (text, file, link, group types)
- Valid edge connections between nodes
- Correct z-index ordering (groups before content)
- Consistent color schemes (preset or custom hex)
- Chinese quote escaping (『』 and 「」)
- Minimum spacing requirements (320px horizontal, 200px vertical)

## Key Files

- `SKILL.md` - Main skill instructions, workflows, and algorithms
- `references/canvas-spec.md` - Complete JSON Canvas format specification
- `references/layout-algorithms.md` - Positioning algorithms for MindMap and freeform layouts
- `assets/template-*.canvas` - Example canvas files for reference
- `README.md` - Installation and usage instructions
- `discovery.json` - Skill metadata and routing configuration
