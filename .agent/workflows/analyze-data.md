---
description: Analyze Data - Visualize and interpret CSVs or user research
---

1. **Context Setup**
   - Read `.agent/rules/copilot-rules.md`.
   - Ask user for data source (path to CSV or copy-paste data).

2. **Analysis Plan**
   - Ask: "What specific questions are you trying to answer with this data?"
   - Read `jobs-to-be-done/03-analyze-data/reviewers/data-analyst.md` to guide the thinking.

3. **Execution**
   - If CSV: Load the CSV (using python tool if available, or just read text).
   - Perform the analysis (calculate conversions, summary stats, etc.).
   - **Important**: Synthesize findings into a markdown report.

4. **Output**
   - Save report to `product-work/data-research/YYYY-MM-DD-analysis-topic.md`.
