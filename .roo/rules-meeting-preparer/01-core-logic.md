# Meeting Preparer: Core Logic

This document outlines the core operational logic for the Meeting Preparer mode.

## 1. Initialization and Context Gathering

1.  **Determine Meeting Type**:
    *   If the user's request clearly specifies "one-on-one" or "performance review", proceed.
    *   If the meeting type is ambiguous or not provided, **MUST** ask the user: "What type of meeting are we preparing for? (e.g., one-on-one, performance review)"
    *   Store the meeting type (e.g., `one-on-one` or `performance-review`).

2.  **Identify Team Member**:
    *   Prompt the user: "Who is this meeting with? Please provide their first name."
    *   Store the first name (e.g., `alex`).

## 2. File and Directory Management

1.  **Construct File Path**:
    *   The target file path is `people/[firstname]/[meeting_type]/next.md`.
    *   Example: `people/alex/one-on-one/next.md`.

2.  **Ensure Directory Existence**:
    *   Check if the directory `people/[firstname]/[meeting_type]/` exists.
    *   If not, **MUST** create it using the `mkdir -p people/[firstname]/[meeting_type]` command.

## 3. Template Selection and Pre-filling

1.  **Select Template**:
    *   Based on the determined `[meeting_type]`, select the appropriate template from `.roo/rules-meeting-preparer/02-meeting-templates.md`.

2.  **Gather Information for Pre-filling (NEW)**:
    *   **Read Previous Meeting Notes**:
        *   Check for existing files in `people/[firstname]/[meeting_type]/` (excluding `next.md`). These could be past `next.md` files that were renamed (e.g., `2024-05-15-notes.md`).
        *   If previous notes exist, read the most recent one to extract relevant information (e.g., past action items, discussion points).
    *   **Read General Person Notes**:
        *   Read the content of `people/[firstname].md` to gather general context, ongoing goals, or feedback.
    *   **Read Career Path Information**:
        *   Attempt to identify the team member's current or target position by reading their `people/[firstname]/main.md` file (look for sections like "Current Role", "Goals", or "Career Path").
        *   If a position (e.g., "Software Engineer", "Product Manager") is identified:
            *   Convert the position name to a slug format (e.g., "software-engineer", "product-manager").
            *   Attempt to read the corresponding file: `career-path/[position-slug].md`.
            *   If read, use its content (skills, expectations, development areas) for pre-filling.
        *   If the position cannot be determined from `people/[firstname]/main.md`, or if the career path file for the identified position does not exist, ask the user: "What is [firstname]'s current or target position for this meeting (e.g., 'Software Engineer', 'Product Manager')? Or is there a specific career path document in `career-path/` we should refer to?"
        *   If the user provides a position or filename, attempt to read `career-path/[user-provided-slug].md`.
        *   If the relevant career path file cannot be read or found, note its absence and proceed. The performance review questioning (section 4.1) should still prompt for alignment with career expectations, even if the document isn't available.

3.  **Pre-fill Template**:
    *   Using the gathered information, attempt to pre-fill relevant sections of the selected template (e.g., person's name, date, carry-over action items, relevant goals).
    *   Clearly indicate any pre-filled information.

## 4. Interaction and Content Generation

1.  **Present Template and Guide Content Generation**:
    *   **For `meeting_type` other than `performance-review`**:
        *   Show the user the (pre-filled) template.
        *   Prompt the user to review the pre-filled information and fill in the remaining placeholders (e.g., "Here's a draft for your meeting with [firstname]. Please review the pre-filled sections and complete the rest:").
        *   Allow the user to provide content for each section of the template.
    *   **For `meeting_type` of `performance-review`**:
        *   Inform the user: "To prepare for [firstname]'s performance review, I will ask you a series of questions based on their career path and previous review. The template will be filled as we go."
        *   Present the (pre-filled) template structure for context if helpful, or fill it iteratively.
        *   **Sequentially ask questions** to gather information for each relevant section of the performance review template. These questions should cover (but are not limited to):
            *   Key achievements and contributions during the review period.
            *   Progress on goals set in the last performance review.
            *   Challenges encountered and how they were addressed.
            *   Alignment with the expectations outlined in their `career-path/[relevant-path].md`.
            *   Observed strengths and areas for development.
            *   Specific examples to support assessments.
            *   Proposed goals for the next review period.
        *   After each response, confirm understanding and populate the corresponding part of the `next.md` content.
        *   Allow the user to refine or add more details after the initial round of questions.

## 5. Saving the Meeting Notes

1.  **Handle Existing `next.md`**:
    *   If `people/[firstname]/[meeting_type]/next.md` already exists, ask the user: "There's an existing 'next.md' for this meeting type. Would you like to (O)verwrite it, (R)ename the old one (e.g., to `[timestamp]-next.md`), or (C)ancel?"
        *   If (O)verwrite: Proceed to save.
        *   If (R)ename: Prompt for a new name or suggest one (e.g., based on current date/time), then rename the old file using `mv` command, then proceed to save the new file.
        *   If (C)ancel: Stop the process.

2.  **Write to File**:
    *   Once the content is finalized, write the complete meeting notes to `people/[firstname]/[meeting_type]/next.md`.

## 6. Confirmation

*   Confirm to the user: "Your meeting preparation for [firstname] ([meeting_type]) has been saved to `people/[firstname]/[meeting_type]/next.md`."