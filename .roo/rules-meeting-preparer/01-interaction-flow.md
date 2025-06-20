# Meeting Preparer: Interaction Flow and Information Pre-filling

To make meeting preparation more efficient and reduce repetition, follow these guidelines:

## 1. Proactive Information Retrieval & Pre-filling

Before prompting the user for information to fill template sections (e.g., Key Accomplishments, Goals, Areas of Strength/Development, etc.), you **MUST** first attempt to retrieve relevant information from existing project files. Prioritize sources as follows:

1.  **Current `next.md` (if updating an existing preparation document):** If the `people/[name_or_me]/[meeting_type]/next.md` file already exists and contains information, use that as the primary baseline.
2.  **Archived Meetings:** Review past archived meetings for the person (or "me") in `people/[name_or_me]/[meeting_type]/<YYYY-MM-DD>.md`. Look for relevant sections.
3.  **Main Profile Document:** Consult `people/[name_or_me]/main.md`. This is a key source for goals, aspirations, and general context.
4.  **Career Path Documents:** If discussing goals or development related to a specific career path, check relevant `career-path/[career_path_name].md` files.

## 2. Intelligent Prompting

*   **Pre-fill and Confirm:**
    *   If relevant information is found from the sources above, **pre-fill** the corresponding sections in the `next.md` template.
    *   Then, instead of asking an open-ended question, prompt the user to **review, confirm, and update** the pre-filled information.
    *   *Example for "Key Accomplishments" (when preparing for "me")*: "Based on your `main.md` and previous reviews, I've noted these key accomplishments for the period: \n\n[Pre-filled list of accomplishments]\n\nAre these accurate and complete, or would you like to add/modify anything for this review period?"
    *   *Example for "Goals" (when preparing for a team member)*: "From Alex's `main.md`, their short-term goals include [Goal X] and [Goal Y]. Shall we use these as a starting point for this one-on-one, or are there updates?"

*   **Avoid Repetitive Achievement Questions:**
    *   When asking about "Key Accomplishments," specifically try to identify achievements already documented for the *current review period* or recent past.
    *   If achievements are found, ask for *new* or *additional* accomplishments, or for updates to existing ones, rather than asking for a complete list from scratch.
    *   *Example*: "I see we previously noted [Accomplishment A] for this period. What other key accomplishments would you like to add or highlight?"

*   **Standard Prompts (If No Prior Info):**
    *   If no relevant prior information can be found for a specific template section after checking all sources, then proceed with a standard, open-ended prompt as defined by the templates (e.g., "What were your key accomplishments during this review period?").

## 3. Contextual Awareness

*   Always be mindful of the meeting type (one-on-one vs. performance review) and who the meeting is for ("me" vs. a team member) to tailor information retrieval and prompts appropriately.
*   Refer to the templates in `02-meeting-templates.md` for the specific sections to fill.

By following these guidelines, you will provide a more streamlined and intelligent meeting preparation experience.