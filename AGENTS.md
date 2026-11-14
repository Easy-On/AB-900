# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language

All texts in this repository are written in English (US): Markdown content, file names, folder names, scripts, comments, and commit messages. Reply to the user in the language they use, but never write German into repository files.

## Distinguishing practices and labs

- Practices are short exercises, the instructor demonstrates, and participants follow along. They should be completed in 5 - 10 minutes. Use the skill [Write a practice](.claude/skills/write-practice/SKILL.md) to create practices.
- Labs are longer than practices, participants work independently, lasting 15 minutes or longer. The should be no more than one lab per course module. A lab must not be associated with more than one course module. Use the skill [Write a lab](.claude/skills/write-lab/SKILL.md) to create labs.
- Practices and labs must not be redundant. Before creating or revising one, check that no other practice or lab covers the same tasks. If a lab exercise already covers the content of a practice, do not create the practice.
- Minimize dependencies between practices and labs. A practice or lab should be completable on its own. Prefer objects that already exist in the tenant, such as existing users and documents, over objects that an earlier practice or lab creates. Name a dependency in the Setup section only if it cannot be avoided, and do not add new dependencies when extending a practice or lab.

## Writing style for instructions

### General

If tasks or practices can be executed in different ways, e. g. using a desktop experience, a web portal, PowerShell, or Windows Admin Center, include instructions for all methods. If there is only one way to perform a task, do not create a separate subsection (heading) for the method; start the Instructions section directly with the sentence naming the machine or portal.

Method headings are exactly one heading level below the heading above them (for example `###` under `## Instructions`), never two levels. Different PowerShell modules are separate methods at the same level, for example `### Microsoft Graph PowerShell` and `### Microsoft Entra PowerShell`; do not group them under a general `PowerShell` heading. If there is only one PowerShell method, its heading is `### PowerShell`, not the module name. Each method starts with the sentence naming the machine or portal. If there are different PowerShell modules to complete the task, include instructions for each module. Use the skill [Write a practice](.claude/skills/write-practice/SKILL.md) to create practices.

### UI Elements and Steps

- UI elements the user must interact with are always bolded, for example **New**, **User**, **OK**, **Settings**. UI elements that are not interacted with are not bolded, for example the page name **Microsoft Entra admin center**.
- Start a step with the phrase `In ...,` naming the page, panel, or dialog only when its location differs from the previous step's location, for example `In Secure score, note ...` after a step that opened Secure score. Switching to another tab also counts as a change of location; the first step on the new tab starts with `On the tab Name, ...` instead of `In ...,`. Do not bold page, tab, panel, or dialog names in these phrases; bold only the UI elements the user clicks, types, or selects. Steps that stay in the same page, panel, or dialog omit the phrase.
- After signing in, state in the Instructions which admin center or portal the user is in, for example: `After signing in, you are in the **Microsoft Entra admin center**, on the home page.`
- Each step contains actions the user must perform in a single page, panel, or dialog. If a step opens a new page, panel, or dialog, the next instruction starts with the phrase `In ...,` naming that page, panel, or dialog (for example `In Secure score, note ...`).
- Verifying results is never a separate step. Instead, it is an indented paragraph below the step that produced the result, for example `Verify that the user is listed.`.
- Expected results and checks are indented paragraphs below the step, for example `Verify that the user is listed.`
- If a user action significantly changes the page, panel, or dialog, e.g. sorting a table, the next user action must be a separate step.
- Always use `1.` for every list item (automatic numbering).
- Wording: context first, then action. `In **Active Directory Users and Computers**, in the context-menu of **IT**, click **New**, **Group**.`
- Window and dialog names in the context part are not bold. Message text is quoted exactly, without quotation marks: `In the message box Remove user?, click **Remove**.`
- Start a step with the phrase `In ...,` naming the page, panel, or dialog only when its location differs from the previous step's location (for example `In Secure score, note ...` after a step that opened Secure score). Switching to another tab also counts as a change of location; the first step on the new tab starts with `On the tab Name, ...` instead of `In ...,`. Do not bold page, tab, panel, or dialog names in these phrases; bold only the UI elements the user clicks, types, or selects. Steps that stay in the same page, panel, or dialog omit the phrase. Never start a step with `On the page ...`.
- After signing in, state which admin center or portal the user is in, for example `After signing in, you are in the **Microsoft Entra admin center**, on the home page.`
- Several clicks in one path: `click **New**, **User**`.
- Verbs: *click*, *type*, *select*, *activate*/*deactivate* (checkboxes, switches), *find and click* (people pickers or search fields), *navigate to*, *execute* (scripts), *sign in as*, *sign out*.
- Icons without text: `click the *Settings* icon (the gear icon)`.
- Notes are indented paragraphs with an italic label: `*Note:* ...` or `*Important:* ...`. No GitHub admonitions (`> [!NOTE]`).

### Scripts and code

- Code blocks: four backticks with a language identifier, indented by 4 spaces when inside a step.
- Values that participants must enter stay empty and get a comment: `$tenantName = '' # Between the quotes insert your tenant name`.
- Long cmdlet calls use backtick line continuation, one parameter per line, in `-Parameter:$value` syntax.
- End sessions with a disconnect (`Disconnect-MgGraph`, `Disconnect-PnPOnline`).

### Placeholders and escaping

- Placeholders in angle brackets with backslashes: `\<your tenant\>`, `**admin@\<your tenant\>.onmicrosoft.com**`.
- Escape asterisks in running text: `**Word Template (\*.dotx)**`.
- Bold (`**...**`) for everything that must be clicked, entered, selected, or recognized exactly: UI elements, values to enter, user, group, and site names, app names, machines, accounts, URLs, and file paths.

### Lists and formatting

- Bullets use `*`, not `-`.
- Nested content (sub-lists, code, tables, notes, links) is indented by 4 spaces and separated from the step by blank lines.
- Use tables for values to enter (names, groups, settings), with a header row.
- One blank line before and after headings, lists, tables, and code blocks.
- The file ends with a single newline.

### Links

- Links to general instructions (General) go in an indented paragraph below the step.
- Links to other labs or practices in Setup use a repository-absolute path.
