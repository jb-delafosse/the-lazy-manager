# AI-Assisted Note Taking with Roo

This project utilizes Roo Code, an AI assistant, to streamline and enhance note-taking processes, particularly for career development and meeting management. It leverages a structured directory system and custom operational modes to ensure consistency and efficiency.

## Core Directory Structure

The system relies on a defined directory structure within the project:

*   `people/`: Contains subdirectories for each team member (e.g., `people/alex/`).
    *   `[firstname]/main.md`: A central profile for each person, detailing goals, context, and management style.
    *   `[firstname]/one-on-one/`: Stores notes for one-on-one meetings.
    *   `[firstname]/performance-review/`: Stores notes for performance reviews.
*   `career-path/`: Contains Markdown files defining different career trajectories (e.g., `software-engineer.md`).

## Custom Roo Modes

This project employs specialized Roo modes to manage different aspects of the note-taking and system maintenance workflow:

### 1. ⚙️ Mode Optimiser (`mode-optimiser`)

*   **Purpose:** This mode is designed to refine and optimize the behavior of Roo itself, including its modes and global rules.
*   **Role:** Analyzes user feedback to update specific mode definitions (in `.roomodes`), their detailed instructions (in `.roo/rules-{modeSlug}/`), or global rules applicable to all modes (in `.roo/rules/`).
*   **When to Use:** Engage this mode when you have feedback on how an existing Roo mode is performing, or if you need to update global behaviors, project-level context, or system-wide architectural patterns. It's ideal for refining mode instructions, rules, or the `.roomodes` configuration file.
*   **Key Capabilities:** Can read and edit `.roomodes` and files within any `.roo/` subdirectory.

### 2. 🤝 Meeting Preparer (`meeting-preparer`)

*   **Purpose:** Facilitates the preparation of structured notes for one-on-one meetings and performance reviews.
*   **Role:** Helps determine the meeting type, identifies the team member, and creates/updates a meeting preparation document (e.g., `people/john/performance-review/next.md`). It uses predefined templates and attempts to pre-fill information from previous meetings and career path documents.
*   **When to Use:** Use this mode before a one-on-one or performance review to structure your thoughts and ensure all key discussion points are covered.
*   **Key Capabilities:** Can read relevant files and edit meeting preparation files (`people/[firstname]/[meeting_type]/next.md`). It can also execute commands, for example, to create necessary directories.

### 3. 🗓️ Meeting Archiver (`meeting-archiver`)

*   **Purpose:** Finalizes and archives meeting notes after a meeting has concluded.
*   **Role:** Takes a preparatory note (typically `next.md`), reformats it for conciseness while maintaining its structure, and saves it as a dated archive (e.g., `people/john/one-on-one/2025-06-16.md`). It also manages the original `next.md` file post-archival.
*   **When to Use:** After a meeting prepared with the "Meeting Preparer" (or similar) to create a clean, dated record.
*   **Key Capabilities:** Can read career profiles and meeting notes, and edit/create dated meeting archives and the `next.md` files. It can also execute commands for file management.

## General Workflow for AI-Assisted Note Taking

The typical workflow for using Roo in this project, especially for meeting management, is as follows:

1.  **Initial Setup (if not already done):**
    *   Roo, guided by global rules (like those in `01-career-discussion-framework.md`), will ensure the base directories (`people/`, `career-path/`) exist.
    *   It will prompt for team member names to create individual directories and `main.md` profile files within `people/`.

2.  **Meeting Preparation:**
    *   Engage the **`Meeting Preparer`** mode.
    *   Specify the person and type of meeting (one-on-one or performance review).
    *   Roo will create a `next.md` file in the appropriate directory (e.g., `people/john/performance-review/next.md`).
    *   It will read existing information from the person's `main.md`, past archived meetings, and relevant `career-path/*.md` files to pre-fill the `next.md` template.
    *   Roo will then ask a series of guided questions to help you complete the preparation notes in `next.md`.

3.  **Conducting the Meeting:**
    *   Use the notes in `next.md` as a guide for your discussion.

4.  **Meeting Archival:**
    *   After the meeting, engage the **`Meeting Archiver`** mode.
    *   Specify the person and meeting type. Roo will locate the corresponding `next.md` file.
    *   Provide the actual date of the meeting.
    *   Roo will read `next.md`, reformat its content for conciseness (while preserving structure), and save it as a new, dated Markdown file (e.g., `people/john/performance-review/YYYY-MM-DD.md`).
    *   Roo will then typically prompt for how to handle the original `next.md` (e.g., delete it or clear its content for the next meeting).

5.  **Ongoing Maintenance & Optimization:**
    *   The `people/[firstname]/main.md` files should be updated periodically (either manually or with Roo's help) to reflect new goals, achievements, or changes in context.
    *   If you find that any mode's behavior, prompts, or the rules governing them could be improved, use the **`Mode Optimiser`** to make adjustments. This ensures the system evolves with your needs.

This workflow aims to create a comprehensive, easily navigable, and AI-enhanced system for managing important discussions and career development information.