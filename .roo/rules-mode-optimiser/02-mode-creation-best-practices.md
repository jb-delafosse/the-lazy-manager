# Roo Code: Custom Mode Creation Best Practices
Creating effective custom modes in Roo Code is paramount for tailoring its behavior to your specific workflows and team standards. Here are best practices for custom mode creation, with a strong focus on instruction format and rules, drawing directly from the sources:
## Best Practices for Creating a Custom Mode
1. Choose Your Creation Method Wisely: Manual YAML Configuration is KingWhile "Ask Roo!" or using the Prompts Tab can create basic modes, manual YAML configuration offers the most precise control and is the preferred method for robust, version-controlled custom modes, especially in team environments [1-3].
•
For global modes, edit custom_modes.yaml (or custom_modes.json as a fallback if YAML is not present and automatic migration hasn't occurred) via the Prompts Tab settings menu [2, 4].
•
For project-specific modes, edit the .roomodes file (YAML is preferred, but JSON is supported) in your project root, also accessible via the Prompts Tab settings menu [2, 5].
•
Embrace YAML: YAML is the preferred format over JSON due to its superior readability, support for comments, cleaner multi-line strings, and less punctuation, making it easier to manage complex configurations [3, 6, 7]. Pay close attention to indentation, as it defines the structure, and use hyphens for list items [7].
2. Define Core Mode Properties with PrecisionEach property in your custom mode definition serves a critical purpose [8].
•
slug (Unique Internal Identifier):
◦
Be Opinionated: Your slug must be unique and should be short, descriptive, and follow the format of lowercase letters, numbers, and hyphens (e.g., docs-writer, py-refactor) [8, 9].
◦
Crucial Link: The slug is essential for linking your custom mode to file-based instructions, as the directory and file names for these instructions rely directly on it (e.g., .roo/rules-{modeSlug}/, .roorules-{modeSlug}) [8-11].
◦
Override Default Modes Carefully: If you intend to modify a built-in Roo mode (like code or debug), use its exact slug to override it [12].
•
name (Display Name):
◦
Be Specific: Choose a clear and human-readable name that appears in the Roo Code UI (e.g., "📝 Documentation Writer", "🧪 Test Engineer") [8, 9]. This is less critical for functionality but vital for user experience.
•
roleDefinition (Core Identity & Expertise):
◦
Be Opinionated: This property defines the fundamental persona and expertise of your mode [8, 13]. Use multi-line YAML (>- or |-) for comprehensive descriptions of the mode's identity, key skills, and specialized knowledge [3, 13].
◦
Focus on Core Identity: While the first sentence can summarize the mode, do not rely on it if you intend to use whenToUse [8, 13]. Its primary function is to define Roo's personality and behavior when the mode is active [8].
•
whenToUse (Optional, but Highly Recommended for Orchestration):
◦
Be Opinionated: Always populate whenToUse if your mode is intended for automated decisions, task orchestration (e.g., by the Orchestrator mode), or intelligent mode switching [8, 14].
◦
Precedence: This description takes precedence over the first sentence of roleDefinition for summarization purposes in contexts like new_task or switch_mode tools, ensuring Roo understands its purpose effectively [8, 13, 14].
•
groups (Tool Access & File Restrictions):
◦
Be Opinionated: Explicitly define all allowed tool groups ("read", "edit", "browser", "command", "mcp") [8, 15].
◦
Implement Strict File Restrictions for edit: For safety, efficiency, and context management, always use fileRegex within the "edit" group to limit your mode's modification capabilities to only the relevant file types [15-17]. * Opinionated Regex Formatting: Be aware of escaping rules: single backslashes for YAML (\.md$) and double backslashes for JSON (\\.md$) [15, 18, 19]. * Leverage Roo: If you're unsure about regex patterns, ask Roo to generate them for you (e.g., "Create a regex pattern that matches JavaScript files but excludes test files") [18]. * Test Your Patterns: Always test your fileRegex patterns against sample file paths using online regex testers to ensure they behave as intended [20].
•
customInstructions (Specific Behavioral Guidelines - Initial Set):
◦
Be Opinionated: Use this property for concise, top-level behavioral guidelines that are directly embedded in your mode's configuration [8, 14].
◦
Do Not Overload: For lengthy, complex, or evolving instructions, do not put everything here. Instead, rely on the file-based instruction methods detailed below [11]. This keeps your mode definition clean and makes instructions easier to manage [11].
3. Prioritize File-Based Instructions for Scalability and CollaborationWhile customInstructions within the mode definition are useful, file-based instructions are the best practice for organization, version control, and team standardization [11, 21-24].
•
Preferred Method: Directory-Based (.roo/rules/ and .roo/rules-{modeSlug}/)
◦
Workspace-Wide Rules: For instructions that apply to all modes in your project, create a directory named .roo/rules/ in your workspace root [21, 25].
◦
Mode-Specific Rules: For instructions specific to your custom mode, create a directory named .roo/rules-{modeSlug}/ (e.g., .roo/rules-docs-writer/) in your workspace root [10, 11, 22, 26]. This is the strongest recommendation for mode-specific instructions.
◦
Opinionated Organization: Place instruction files (e.g., .md, .txt) inside these directories [25, 26]. Organize them logically and name them alphabetically (e.g., 01-general.md, 02-coding-style.txt) as Roo Code reads files recursively and appends their content to the system prompt in alphabetical order [11, 25, 26].
◦
Precedence: These directory methods take precedence over single fallback files and are combined with instructions from the Prompts tab and the customInstructions property [22, 25-28].
•
Fallback Method (for backwards compatibility, less flexible): Single File (.roorules and .roorules-{modeSlug})
◦
Only use these if the preferred directory methods do not exist or are empty [21, 22, 25, 26, 28]. They offer less flexibility and organization [23].
4. Craft Your Instructions with Prompt Engineering PrinciplesThe content within your customInstructions property and your instruction files should adhere to strong prompt engineering principles for optimal results [29-31].
•
Be Clear and Specific: Always state precisely what you want Roo Code to do. Avoid vague or ambiguous language [29, 31]. (e.g., "Always use spaces for indentation, with a width of 4 spaces" [23] vs. "Fix the code" [29]).
•
Provide Context: Use context mentions (@/file.ts, @problems) where relevant within your prompts to guide Roo to specific information [32-34].
•
Break Down Tasks: If a task is complex, instruct Roo to break it down into smaller, manageable steps, or break down the instructions yourself across multiple files [32, 35].
•
Give Examples: If you have a specific coding style, output format, or pattern in mind, provide concrete examples within your instructions [23, 32].
•
Specify Output Format: If Roo needs to generate output in a particular format (e.g., JSON, Markdown), explicitly state it [32].
•
Guide Thinking (Think-Then-Do): Encourage Roo to analyze and plan before executing. Include instructions like "Explain your reasoning before providing code" [23] or guide it through "Analyze," "Plan," "Execute," and "Review" stages [30].
•
Handle Ambiguity Proactively: By providing clear, specific instructions from the outset, you minimize the need for Roo to make assumptions or ask follow-up questions [31, 36].
•
Enforce Standards: Use instructions to enforce coding style guidelines, documentation standards, testing requirements, preferred libraries/frameworks, and project-specific conventions [23, 31, 37].
5. Leverage for Team Standardization and Version Control
•
Be Opinionated: For team environments, always place your .roo/rules/ and .roo/rules-{modeSlug}/ directories under version control [11, 23]. This is the recommended way to standardize Roo's behavior across your team, ensuring consistent code style, documentation practices, and development workflows for all members [23]. This promotes consistency and reduces manual configuration efforts.
By following these specific and opinionated best practices, you can create highly effective custom modes that enhance your workflow and maintain consistency across your projects and teams.