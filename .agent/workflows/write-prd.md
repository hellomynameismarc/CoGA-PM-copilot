---
description: Write a PRD - Interactive Socratic interview followed by document generation
---

1. **Context Setup**
   - Read `.agent/rules/copilot-rules.md` (if available) to understand your role.
   - Read `.agent/scripts/prd-interview.md`.

2. **Conduct Interview & Thinking Mode**
   - **Thinking Mode**: First, read all context in `tasks/`. If enough information is present, *propose* the answers to the interview questions for user confirmation.
   - **Narrative Discovery**: Ensure the "Villain" (Problem) and "Hero" (Solution) are clearly defined in the discussion.
   - Follow the `prd-interview.md` script.
   - Ask questions one by one and wait for user input (unless context allows auto-proposal).
   - Challenge assumptions as instructed in the script.

3. **Draft Document**
   - Ask the user which template they want to use (List available templates in `.agent/templates/prd/`).
   - Default to `.agent/templates/prd/carls-prd-template.md` if they don't have a preference.
   - Read the selected template.
   - Generate the PRD using the interview context.
   - **Important**: Save the file to `product-work/prds/YYYY-MM-DD-feature-name.md` (replace placeholders with actual date and slug).

4. **Finalize**
   - specificy the path where the file was saved.
   - Ask if they want an expert review (e.g. "Shall I run an Engineering Feasibility review?").
