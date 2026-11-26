# Project Instructions for Goose

## 1. Operational Principles & Policy
- **Verify Before Action:** Always inspect files and directory structures (using `tree`, `ls`, etc.) before making changes.
- **Mandatory Pre-approval:** Before creating, editing, or deleting any files or directories, you MUST present the proposed changes (including target file names and a description/summary of the intended modifications) to the user and obtain explicit approval.
- **Session Isolation & Management:** To maintain organization, create a dedicated session folder with an appropriate name for each session/task and perform work within that folder. 
- **Operations Outside Scope:** Do not modify files outside the designated session scope or directory without prior explicit approval.
- **Minimal Impact:** Make only the changes necessary to complete the task. Avoid excessive or unnecessary modifications.
- **Incremental Development:** Build and verify in small steps to avoid large errors.

## 2. Python Development (Mandatory)
- **Environment Management:** Always use `uv` for all Python-related tasks to ensure consistency.
- **Environment Verification:** At the start of a task or when new libraries are required, verify the environment using `uv --version` and check available packages with `uv pip list`.
- **Dependency Management:**
  - **Adding Libraries:** Use `uv add <package>` to add new libraries.
  - **Project Awareness:** Always check for a `pyproject.toml` file. If it exists, **you must** use `uv add`.
  - **Fallback:** If no `pyproject.toml` is found, use `uv pip install <package>`.
  - **Library Suggestion:** If a required library is missing, suggest it to the user instead of attempting unapproved installations.
- **Script Execution:** Always prefer `uv run python <script.py>` to ensure the correct virtual environment is utilized.

## 3. File & Tool Usage
- **Exploration:** Use `tree` for high-level structure and `ls` for file lists.
- **Search:** Use `grep` or `rg` to search for specific patterns or symbols within the codebase.
- **Editing:** Always read the file content (`cat` or `head`) before using `edit` or `write` to ensure the context is accurate and the `before` text matches exactly.

## 4. Workflow & Communication
- **Permission for External Resources:** If a task requires accessing external URLs or using tools that require internet connectivity (e.g., `web_search`), do not proceed autonomously. Inform the user and obtain permission first.
- **Plan:** For complex tasks, provide a brief summary of your execution plan to the user before proceeding.
- **Error Handling (Self-Correction):** If a command fails, analyze the error and `stderr` systematically, check the environment (e.g., via `uv pip list`), and try a different approach to resolve it.
- **Test & Verify:** After modifying code, run the relevant script or test command to verify that the changes work as intended and haven't broken existing functionality.
- **Clean up:** Ensure no unnecessary temporary files, debug logs, or leftover session folders remain in the working directory after task completion.
