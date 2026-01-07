# Product Management Copilot

Welcome to your AI-powered Product Management workspace. This environment is designed to help you think deeper, move faster, and produce higher-quality work by leveraging expert AI personas and structured workflows.

## 🚀 Quick Start

Use these slash commands in your Agent chat to start a task:

| Command | Action | Output Location |
|:---|:---|:---|
| `/write-prd` | **Write a PRD**. Interactive interview to clarify problem/solution, then drafts spec. | `product-work/prds/` |
| `/product-strategy` | **Develop Strategy**. Strategic deep-dive into market, SWOT, and vision. | `product-work/strategy/` |
| `/analyze-data` | **Analyze Data**. Guidance on querying CSVs and finding insights. | `product-work/data-research/` |
| `/status-update` | **Status Update**. Drafts weekly or executive updates based on recent work. | `product-work/updates/` |

## 👥 Expert Reviewers

You can ask for specific persona reviews on any document:

- **`/review-eng`**: Engineering Feasibility (Technical constraints, complexity)
- **`/review-exec`**: Executive Strategy (Business impact, clarity, ROI)
- **`/review-design`**: UX/UI (User journey, edge cases, accessibility)
- **`/review-data`**: Data Analysis (Methodology validation, metric choice)
- **`/review-pmm`**: Product Marketing (Positioning, value prop, launch)

## 📂 Directory Structure & Workflow

We separate **Inputs (Context)** from **Outputs (Artifacts)**.

### 1. `tasks/` (The Kitchen 🍳)
*Input Context & Raw Ingredients*
- Create a folder here for each project: `tasks/YYYY-MM-DD-project-name/`.
- Dump **everything** in here: raw CSVs, PDF feedback, messy meeting notes, competitive screenshots, brain dumps.
- **Agent Action**: The Agent reads this folder to understand *Context*.

### 2. `product-work/` (The Dining Room 🍽️)
*Polished Outputs & Artifacts*
- The Agent generates final, polished documents here.
- **Agent Action**: The Agent writes structured PRDs, Strategy Decks, and Updates here.

### 3. `.agent/` (The Brain 🧠)
- System brains (Templates, Personas, Rules). Do not edit.

## 🚀 Quick Start

1.  **Prep**: Create `tasks/2026-01-07-my-feature/` and drop your files there.
2.  **Run**: Type `/write-prd`.
3.  **Context**: Tell the agent "Context is in `tasks/2026-01-07-my-feature`".
4.  **Result**: Find your polished PRD in `product-work/prds/`.

| Command | Action | Output Location |
|:---|:---|:---|
| `/write-prd` | **Write a PRD**. Interactive interview to clarify problem/solution, then drafts spec. | `product-work/prds/` |

## 💡 Philosophy
This Copilot uses a **Socratic approach**. It won't just "do the work" — it will challenge your assumptions, ask for evidence, and help you refine your thinking *before* generating the final document.
