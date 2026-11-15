---
name: write-general-instructions
description: Writes a general instruction (Markdown with one section per method, such as Desktop experience and PowerShell, for a single task) for training courseware in the style of the ETC/Easy On course materials. Use when the user wants to create or revise a general instruction, a reusable how-to that labs and practices link to, or a file in Instructions/General/.
---

# Write a general instruction

A general instruction explains how to perform one task, for example raising the forest functional level. Labs and practices link to it from a step, so the lab can state the goal and leave the how-to to the general instruction. A general instruction belongs to no lab, module, or machine.

Formatting and wording rules come from the repository instructions and apply here as well. This skill covers the structure of a general instruction only.

## Procedure

1. **Gather information.** Needed: the single task, the methods to cover (Desktop experience, Windows Admin Center, PowerShell, and the PowerShell modules that can do the task), and the values the reader must enter. If the request covers more than one task, write one file per task. If something essential is missing, ask.
2. **Check existing files.** Search `Instructions/General/` for a file on the same task. Update that file instead of creating a duplicate.
3. **Create the file.** Place it in `Instructions/General/`. File name: words separated by hyphens, first word capitalized, product names keep their spelling, and the task in gerund form (for example `Raising-the-forest-functional-level.md`, `Changing-TCP-IP-settings-on-Windows-11.md`). The H1 heading is the file name with spaces instead of hyphens, without prefix.
4. **Check before handing over.** Go through the checklist below.

Write the content in English (US). Reply to the user in the language they use.

## Structure

```markdown
# <Task in gerund form>

## Desktop experience

1. Open **Active Directory Administrative Center**.
1. In Active Directory Administrative Center, in the context-menu of the forest root domain, click **Raise the forest functional level...**.

## PowerShell

1. Open a terminal.
1. Set the forest mode to Windows Server 2025.

    ````powershell
    # Between the quotes, insert the FQDN name of the forest root domain
    $identity = ''

    Set-ADForestMode -Identity $identity -ForestMode Windows2025Forest
    ````

    > The value for ForestMode should be Windows2025Forest.

## References

[Set-ADForestMode](https://learn.microsoft.com/en-us/powershell/module/activedirectory/set-adforestmode)
```

## Scope

- No introduction, no Required VMs, no Setup, no exercises. The first line after the H1 is the first method heading.
- Do not name a machine in a step, such as `On **CL1**`. The lab or practice that links here names the machine.
- Do not include the sentence `Perform this task on ...`. That sentence belongs to labs and practices.

## Methods

- Give each method its own H2 heading.
- Each method completes the whole task on its own. The reader chooses one method and does not need the others.
- Leave out a method that cannot complete the task. Do not write a section that says the method is unavailable.
- Start a PowerShell method with `Open a terminal.` unless the method needs a different start.

## Steps

- Each step contains one action on one page, panel, or dialog.
- Every value that the reader enters is an empty variable or an empty entry in the code block, with a comment that tells the reader what to insert. The reader fills in the value; the instruction does not supply a real one unless the value is fixed by the task.
- If a step has a visible result, add an indented paragraph below the step, for example `Verify that the forest mode is Windows2025Forest.`
- Use `*Note:*` for a note, as an indented paragraph.
- For PowerShell, start with a code block definining variables for parameters the reader must enter, then the cmdlet call. Use a comment to tell the reader what to insert. Use a code block for the cmdlet call, not inline code.

## References

- End the file with a `## References` section if the task has official documentation.
- List each reference as a link on its own line. Prefer the official Microsoft Learn or vendor pages.
- Omit the section if there is no reference.

## Checklist before handover

- [ ] Title: H1 in gerund form, and the file name in `Instructions/General/` matches the title with hyphens.
- [ ] The file covers one task only, and no existing file covers the same task.
- [ ] No introduction, Required VMs, Setup, or exercise sections.
- [ ] Methods appear in the order Desktop experience, Windows Admin Center, PowerShell, and each method completes the whole task.
- [ ] Each PowerShell module that can do the task has its own H3 heading.
- [ ] No step names a machine, and no `Perform this task on` sentence appears.
- [ ] Every entered value is an empty variable with a comment, or a fixed value required by the task.
- [ ] Each visible result has a verification paragraph below the step.
- [ ] The file ends with a single newline.
