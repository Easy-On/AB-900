---
name: write-practice
description: Writes a practice (Markdown with sections Setup, Task, Instructions) for training courseware in the style of the ETC/Easy On course materials. Use when the user wants to create, revise, or review a practice, a demonstration guide for course instructors, or "Practice: <task>".
---

# Write a practice

A practice is a step-by-step guide that the instructor demonstrates. Participants watch or follow along. Unlike a lab, it is not solved independently.

Formatting and wording rules are in `CLAUDE.md` and apply to labs as well. This skill covers the structure of a lab only.

## Procedure

1. **Gather information.** Needed: the task, the required VMs, the machine for the task (for example **CL1**, **WIN1**, **VN1-SRV1**, or portal/cloud), the sign-in account, target values (names, groups, settings), and whether there are preceding labs, practices, or scripts. If something essential is missing, ask. Use placeholders for non-essential values (`\<Group name\>`).
2. **Check sources.** If the repository has a `CLAUDE.md`, follow its conventions (file names, placeholders, machine names). Existing practices in the same folder serve as style references.
3. **Create the file.** File name: words separated by hyphens, first word capitalized, product names keep their spelling, imperative form (for example `Create-a-user-in-Entra.md`). The H1 heading equals the file name with spaces instead of hyphens.
4. **Check before handing over.** Go through the checklist below before you deliver the file.

Write the practice content in English (US). Reply to the user in the language they use.

## Structure

```markdown
# Practice: <Task>

<!-- Only for local VMs. Omit in online lab environments. -->

## Required VMs

* <VM>

## Setup

<Prerequisites, links to other labs or practices, catch-up script, sign-in>

## Task

<Complete description of the goal>

## Instructions

### <Method, for example PowerShell>

Perform this task on **<machine>**.

1. ...

    <Verification of the end state>
```

- The title is always `Practice: <Task>`, for example `Practice: Create a user in Entra`. Never use `Lab:` or any other prefix form.

## Section Required VMs (only for local VMs)

- Use this section only if the practice runs on local VMs that participants must start. Omit it in online lab environments, in which the machines are already available.
- List every VM that must be running for the practice as a bullet with the bold name: `* **CL1**`.
- If a VM depends on whether a lab or practice was completed, name it with a link, for example `If you did not complete the lab [Deploying domain controllers](/Instructions/Labs/Deploying-domain-controllers.md), in addition to the VMs above, **VN1-SRV1** is required.`
- If a VM is already shut down and must not be started again, state this explicitly: `If **VN1-SRV1** is already shut down after the lab, do not start it.`
- If no VMs are needed omit this section.
- This section always comes before `Setup`.

## Section Setup

- **Dependencies:** Link other labs or practices with a relative link, for example `[Install Remote Server Administration Tools](/Instructions/Practices/Install-Remote-Server-Administration-Tools.md)`. Add a sentence such as "If you skipped the practice [...], ...".
- **Catch-up script:** If a script covers skipped parts, describe the call completely, for example: in **PowerShell**, execute `C:\LabResources\Solutions\<ScriptName>.ps1`, and name the machine.
- **Prerequisites:** Explicitly name any sign-in to a computer, service, or portal (account, portal URL) that is needed before the task.
- If none of this applies, omit this section. Never write negative requirements such as "No preparation is needed" or "No previous lab is required".

## Section Task

- Describe the goal completely enough that experienced participants can complete the task without the Instructions. Name all names, values, groups, paths, permissions, options, and the expected end state.
- Use bullet points for requirements when there are several.
- No steps, click instructions, or solution hints in this section.

## Section Instructions

### Machine

The first sentence of the section names the machine or portal where the task is performed, for example:

- `Perform this task on **CL1**.`
- `Perform this task in the **Microsoft Entra admin center**, on **CL1**.`

If the practice switches machines, every subsection starts with such a sentence.

## Checklist before handover

- [ ] Title: `# Practice: <Task>`, and the file name matches the title with hyphens.
- [ ] Sections appear in this order: Required VMs (only for local VMs), Setup, Task, Instructions.
- [ ] If the practice uses local VMs, Required VMs lists every VM needed. In an online lab environment, the section is omitted.
- [ ] Setup names dependencies, the catch-up script, and sign-ins. It contains no negative statements such as "No preparation is needed".
- [ ] Task contains all details: names, values, permissions, end state. An experienced participant can complete the task without the Instructions.
- [ ] The Instructions begin with the sentence naming the machine.
- [ ] Every click and entry is documented as a step.
- [ ] Alternative methods are in their own subsections, each complete.
- [ ] All lists use `1.` or `*`, all values are bold, placeholders use `\<...\>`.
- [ ] No introduction, conclusion, or filler outside the sections.
