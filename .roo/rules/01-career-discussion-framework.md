# Career Discussion Framework and Scaffolding

This document outlines the structure and general guidelines for all modes when facilitating or participating in career-related discussions. This framework replaces any previous "Memory Bank" concepts.

## 1. Core Directory Structure (Scaffolding)

The primary location for all career discussion notes is within the project root, organized as follows:

*   `people/`
    *   `[firstname]/`: A dedicated directory for each team member, named with their first name (e.g., `alex/`, `sarah/`).
        *   `main.md`: This file within `people/[firstname]/` serves as the central document for compiled information about the person. It should include:
            *   Family situation (if relevant and shared by the individual).
            *   Goals and aspirations (professional and personal, if relevant).
            *   Current situation related to their career path.
            *   Do's and don'ts for managing or collaborating with this specific person.
        *   Other subdirectories (like `one-on-one/`, `performance-review/` as used by modes like Meeting Preparer and Meeting Archiver) will also reside within `people/[firstname]/`.
*   `career-path/`
    *   `[career_path_name].md` (e.g., `software-engineer.md`, `product-manager.md`): For notes, skills, expectations, and resources related to specific career trajectories within the team or company.

## 2. Automatic Scaffolding Setup (All Modes)

Upon the first interaction with any mode in this project:

*   **Check and Create Base Directories**:
    *   The mode **MUST** first check if the `people/` and `career-path/` directories exist at the project root.
    *   If they do not exist, the mode **MUST** attempt to create them.
        *   If the mode possesses `command` execution capabilities, it should use commands like `mkdir -p people career-path` to create them.
        *   If the mode lacks `command` capabilities, it **MUST** instruct the user clearly and immediately: "To begin, we need to set up the discussion structure. Please create two directories in your project root: `people` and `career-path`. Let me know once this is done." The mode should not proceed further until the user confirms creation.
*   **Prompt for Team Member Names and Create Person Files**:
    *   Once the `people/` directory is confirmed to exist, the mode **MUST** ask the user: "To personalize our discussions, could you please provide the first names of your team members? Please list them separated by commas (e.g., Alex, Sarah, Jordan)."
    *   For each first name provided by the user, the mode (if it has `edit` capabilities for `people/[firstname]/main.md`) **MUST** attempt to:
        1.  Create the directory `people/[firstname]/` if it doesn't already exist (e.g., `people/alex/`). If using `command` tools, `mkdir -p people/[firstname]` is suitable.
        2.  Create an empty file `people/[firstname]/main.md` (e.g., `people/alex/main.md`).
        *   Example content for a new `people/[firstname]/main.md` file:
            ```markdown
            # Career Profile: [firstname]

            ## Personal Context (Optional & Confidential)
            - **Family Situation**: (Note only if relevant and willingly shared)

            ## Goals and Aspirations
            - **Short-Term Goals (6-12 months)**:
            - **Long-Term Aspirations (1-3 years)**:
            - **Development Areas**:

            ## Current Career Situation
            - **Current Role & Responsibilities**:
            - **Alignment with Career Path**:
            - **Recent Achievements**:
            - **Challenges/Blockers**:

            ## Management & Collaboration Style
            - **Do's**: (Effective ways to manage, motivate, or collaborate)
            - **Don'ts**: (Things to avoid)
            ```
        *   If the mode cannot create directories/files directly, it should guide the user: "Great. Now, for each person, please create a directory inside `people/` (e.g., `people/alex/`) and inside each of those, create a file named `main.md`. You can use the template I'll provide for the `main.md` content." (And then provide the template).
*   **Career Path Files**:
    *   The `career-path/` directory will initially be empty. Modes should guide users to create `[career_path_name].md` files within it as discussions about specific career paths arise. For example: "Are there any specific career paths you'd like to define or discuss (e.g., Senior Engineer, Team Lead)? We can create files for them in the `career-path/` directory."

## 3. General Discussion Principles (All Modes)

*   **Focus**: Maintain a focus on constructive career development, feedback, and planning.
*   **Confidentiality**: Remind users to be mindful of the sensitivity of the information being discussed and stored, especially in shared environments.
*   **Action-Oriented**: Encourage the identification of action items, goals, and next steps within the `people/[firstname]/main.md` files or relevant `career-path/*.md` files.
*   **Clarity**: Strive for clear and concise note-taking.
*   **Regular Updates**: Encourage users to keep these documents updated as discussions progress.

## 4. Mode-Specific Responsibilities

While these are global rules, individual modes will have specific `roleDefinition` and `customInstructions` tailoring how they apply this framework. All modes that are intended to *write* to these files must have the appropriate `fileRegex` in their `edit` group (e.g., `people/[firstname]/main.md`, `career-path/*.md`). The `mode-optimiser` itself, as per its current definition, will not directly edit these files but will manage the rules and definitions for modes that do.