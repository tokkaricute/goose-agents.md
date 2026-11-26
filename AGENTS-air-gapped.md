# Project Instructions for Goose (Air-gapped Environment Optimized)

## 1. Operational Principles & Policy
- **Verify Before Action:** Always inspect files and directory structures (using `tree`, `ls`, etc.) before making changes.
- **Mandatory Pre-approval:** Before creating, editing, or deleting any files or directories, you MUST present the proposed changes (including target file names and a description/summary of the intended modifications) to the user and obtain explicit approval.
- **Session Isolation & Management:** To maintain organization, create a dedicated session folder with an appropriate name for each session/task and perform work within that folder. 
- **Operations Outside Scope:** Do not modify files outside the designated session scope or directory without prior explicit approval.
- **Minimal Impact:** Make only the changes necessary to complete the task. Avoid excessive or unnecessary modifications.
- **Incremental Development:** Build and verify in small steps to avoid large errors.

## 2. Air-gapped Environment Constraints (Mandatory)
- **No External Connectivity:** Assume that the environment has no access to the internet. Do not attempt to use tools that require external communication (e.g., `web-search`) unless explicitly instructed by the user for a specific purpose.
- **Resource Acquisition:** If new information, data, or libraries are required that are not available locally, do not attempt to download them. Instead, inform the user of the requirement and ask for guidance on how to provide the necessary resources.

## 3. Python Development (Offline-First)
- **Environment Verification:** At the start of a task or when new libraries are required, ALWAYS verify the current environment using `uv pip list` to check if the required packages are already installed.
- **Dependency Management:**
  - **Adding Libraries:** If a library is missing, suggest it to the user. Before attempting `uv add <package>`, explicitly inform the user that this operation may fail due to network constraints.
  - **Error Handling (Connection Errors):** If any command (e.g., `uv add`, `uv pip install`) fails due to a network error (Connection Error, Timeout, etc.), **DO NOT attempt to retry or seek alternative download methods.** Immediately stop and report the error to the user, stating that it is due to the air-gapped environment.
  - **Project Awareness:** Always check for a `pyproject.toml` file. If it exists, use `uv add`.
- **Script Execution:** Always prefer `uv run python <script.py>` to ensure the correct virtual environment is utilized.

## 4. File & Tool Usage
- **Local Context Priority:** Prioritize gathering information from the local filesystem and codebase. Use `tree`, `ls`, `grep`, `rg`, `cat`, or the `analyze` extension as your primary sources of knowledge.
- **Editing:** Always read the file content (`cat` or `head`) before using `edit` or `write` to ensure the context is accurate and the `before` text matches exactly.

## 5. Workflow & Communication
- **Handling Missing Resources:** When a task requires information or tools that are not available in the current air-gapped environment, proactively suggest alternative ways for the user to provide them (e.g., "Please provide the documentation as a local file").
- **Plan:** For complex tasks, provide a brief summary of your execution plan to the user before proceeding.
- **Error Handling (Self-Correction):** 
  - For logic or code errors: Analyze the error and `stderr` systematically, check the environment, and try a different approach.
  - For network/connectivity errors: **Stop immediately and report.** Do not treat connectivity issues as something to be "fixed" via autonomous retry.
- **Test & Verify:** After modifying code, run the relevant script or test command to verify that the changes work as intended and haven't broken existing functionality.
- **Clean up:** Ensure no unnecessary temporary files, debug logs, or leftover session folders remain in the working directory after task completion.
