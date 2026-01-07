# Product Management Copilot

Welcome to your AI-powered Product Management workspace. This environment is designed to help you think deeper, move faster, and produce higher-quality work by leveraging expert AI personas and structured workflows.

## 🚀 Quick Start

Use these slash commands in your Agent chat to start a task:

### 🌟 How to Start
Simply say **"Job menu"** or **"What can we do?"** to see the interactive task list.
You can then just type a number (1, 2, 3...) to kickstart that specific workflow.

| Command | Action | Output Location |
|:---|:---|:---|
| `/write-prd` | **Write a PRD**. Interactive interview to clarify problem/solution, then drafts spec. | `tasks/<task>/product-work-output/` |
| `/product-strategy` | **Develop Strategy**. Strategic deep-dive into market, SWOT, and vision. | `tasks/<task>/product-work-output/` |
| `/analyze-data` | **Analyze Data**. Guidance on querying CSVs and finding insights. | `tasks/<task>/product-work-output/` |
| `/status-update` | **Status Update**. Drafts weekly or executive updates based on recent work. | `tasks/<task>/product-work-output/` |

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

### 2. **Outputs** (The Dining Room 🍽️)
*Polished Outputs & Artifacts*
- The Agent generates final, polished documents.
- **Location**: `tasks/<task-name>/product-work-output/`.
- **Agent Action**: Automatically create this folder if it doesn't exist and save files there.

### 3. `.agent/` (The Brain 🧠)
- System brains (Templates, Personas, Rules in `.agent/rules/`). Do not edit.
- **Workflows**: Located in `.agent/workflows/` (pointing to `jobs-to-be-done/`).

## 🚀 Quick Start

1.  **Prep**: Create `tasks/2026-01-07-my-feature/` and drop your files there.
2.  **Run**: Type `/write-prd`.
3.  **Context**: Tell the agent "Context is in `tasks/2026-01-07-my-feature`".
4.  **Process**: The Agent will challenge your assumptions via Socratic questioning, *then* draft the finalized PRD.

| Command | Action | Output Location |
|:---|:---|:---|
| `/write-prd` | **Write a PRD**. Interactive interview to clarify problem/solution, then drafts spec. | `tasks/<task>/product-work-output/` |

## 💡 Philosophy
This Copilot uses a **Socratic approach**. It won't just "do the work" — it will challenge your assumptions, ask for evidence, and help you refine your thinking *before* generating the final document.
