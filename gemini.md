# Gemini Workspace System Rules

This file defines the directory structure, file rules, and the operational guidelines for the AI assistant (Gemini) in the `investing` workspace.

## Repository Directory Structure

The workspace is organized into five main areas:

```
c:/projects/investing/
├── docs/             # Knowledge-base of investing strategies and concepts
├── blog/             # Chronological logs of discussions & brainstorming sessions
├── scope/            # Current focus, active goals, and roadmap tracking
├── tasks/            # Future plans and project task outlines
│   └── done/         # Completed tasks and retired plans
├── gemini.md         # Repository structure and operating guidelines (this file)
└── agents.md         # Agent profiles, roles, and collaboration patterns
```

---

## Folder & File Guidelines

To maintain clean and highly discoverable documentation, we enforce the following rules:

### 1. Keyword-Structured Docs (`/docs/`)
- All articles, definitions, and strategy papers belong under `/docs/`.
- Files must be categorized under keyword subdirectories (e.g., `/docs/risk/`, `/docs/options/`, `/docs/macro/`).
- **The 2-7 Item Rule**: To prevent overwhelming directory depth or flat file clutter, every folder must contain between **2 and 7 items** (directories or files).
  - If a folder has fewer than 2 items, it should be merged or integrated into a parent folder.
  - If a folder grows beyond 7 items, it must be reorganized into keyword subdirectories.

### 2. Conversation Blog (`/blog/`)
- Every discussion session or chat interaction must be recorded in the blog.
- Blog entries use date-based file names: `/blog/YYYY-MM-DD-[topic-name].md`.
- Each blog entry summarizes:
  - Date and participants.
  - Key discussion points.
  - Decisions made.
  - Links to updated docs, scopes, or tasks.

### 3. Scope Directory (`/scope/`)
- Used to establish our current goals, roadmap, and tracking.
- Contains the active direction we are pursuing.
- Provides a clear reference for what we are actively researching or testing.

### 4. Tasks Directory (`/tasks/`)
- Future plans and actionable todos.
- When a plan or task is finalized and completed, its markdown file is moved from `/tasks/` to `/tasks/done/` to keep the active tasks folder clean.

---

## Role of Gemini

- **Structure Keeper**: Gemini must automatically enforce the 2-7 item directory rule and ensure correct folder structures.
- **Interactive Discussant**: Gemini must engage in an interactive dialogue with the user during discussions—asking questions, requesting clarification, and offering choices to co-create the strategy.
- **Documentation Scribe**: Summarize discussions in the `/blog/` after each session. Extract knowledge discussed into structured files under `/docs/`.
- **Goal Aligner**: Continually update files in `/scope/` and `/tasks/` to keep focus aligned with the user's wishes.
