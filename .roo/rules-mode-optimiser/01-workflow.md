# Mode Optimiser Workflow

1.  **Gather Feedback**: Prompt the user for specific feedback regarding a mode's performance, project documentation, or general operational behavior.

2.  **Determine Feedback Scope**:
    *   **Analyze Feedback Content**:
        *   Does it suggest a behavioral change for *all* or *most* modes (e.g., updates to the career discussion framework)? -> **Scope: Global Rules (`/.roo/rules/`)**
        *   Does it clearly target a *single, named mode* (e.g., a specific career discussion mode)? -> **Scope: Specific Mode (`/.roomodes`, `/.roo/rules-{modeSlug}/`)**
        *   Is it ambiguous? -> Ask clarifying questions to determine the correct scope.

3.  **Analyze Current Configuration**:
    *   Based on the determined scope, read the relevant files:
        *   Specific Mode: Target mode's definition from `/.roomodes` and rules from `/.roo/rules-{target-mode-slug}/`.
        *   Global Rules: Files within `/.roo/rules/` (e.g., `01-career-discussion-framework.md`).

4.  **Propose Changes**:
    *   Based on the feedback, scope, and best practices (see `.roo/rules-mode-optimiser/02-mode-creation-best-practices.md`), formulate specific changes.
    *   **Prioritize Modification**: When the scope involves Global Rules:
        *   First, assess if the feedback can be addressed by modifying an *existing, relevant* file within that scope (e.g., enhancing the `01-career-discussion-framework.md`). Prefer enhancing or adding to an existing file if the new information is logically related.
        *   Propose creating a *new* global rule file only if the feedback introduces a distinctly new topic or rule that doesn't fit well within existing structures.
    *   This approach helps maintain a compact and well-organized set of rules.

5.  **Present Plan**: Explain the proposed changes to the user, including which files will be modified and how the changes address their feedback and the identified scope.

6.  **Seek Approval**: Ask the user to approve the changes before applying them.

7.  **Implement Changes**: Use the `edit` tools to modify the relevant files (`/.roomodes`, `/.roo/rules/`, `/.roo/rules-{modeSlug}/`).

8.  **Verify**: Ask the user to test the optimized career discussion modes or review the career discussion framework changes and confirm if they meet their expectations.