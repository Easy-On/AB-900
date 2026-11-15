---
name: write-lab
description: Writes a lab (Markdown with sections Setup, Introduction, Exercises, and numbered steps that link to general instructions) for training courseware in the style of the ETC/Easy On course materials. Use when the user wants to create, revise, or review a lab, a hands-on exercise that participants complete on their own, or "Lab: <title>".
---

# Write a lab

A lab is a longer exercise that participants complete independently, usually 15 minutes or more. The instructor does not demonstrate it. A lab states the goal of each step. The how-to for each step lives in a general instruction, which the step links to.

Formatting and wording rules come from the repository instructions and apply to labs as well. This skill covers the structure of a lab only.

## Procedure

1. **Gather information.** Needed: the module the lab belongs to (exactly one), the goal, the exercises and steps, the required VMs (if the lab uses local VMs), the sign-in accounts, the input data (names, groups, values), and preceding labs or practices with their catch-up scripts. If something essential is missing, ask.
2. **Check the length.** If the work takes less than 15 minutes, or is demonstrated rather than done independently, it is a practice. Tell the user and use the skill [Write a practice](../write-practice/SKILL.md) instead.
3. **Check the general instructions.** For each step that needs a how-to, search `Instructions/General/` for a matching file. If none exists, write it with the skill [Write a general instruction](../write-general-instructions/SKILL.md) before linking to it.
4. **Check sources.** Read the table of contents in `README.md`, which lists labs by module. Existing labs in `Instructions/Labs/` serve as style references.
5. **Create the file.** Place it in `Instructions/Labs/`. File name: words separated by hyphens, first word capitalized, product names keep their spelling, imperative or descriptive form (for example `Migrate-Active-Directory.md`). The H1 heading is `Lab: ` followed by the title with spaces instead of hyphens.
6. **Check before handing over.** Go through the checklist below.

Write the lab content in English (US). Reply to the user in the language they use.

## Structure

```markdown
# Lab: <Title>

<!-- Only for local VMs. Omit in online lab environments. -->

## Required VMs

* <VM>

## Setup

1. On **<machine>**, sign in as **<account>**.

You must have completed the practice [<Practice title>](../Practices/<Practice-file>.md). If you skipped the practice, on **<machine>**, run ````<script path>````.

## Introduction

<Scenario in two to four sentences, no steps>

## Exercises

1. [<Exercise title>](#exercise-1-<exercise-title>)

## Exercise 1: <Title>

1. On **<machine>**, <goal of the step>.

    <Input data, if the step needs it>

    [<General instruction title>](../General/<General-file>.md)

1. <Next goal>.

    Verify that <expected result>.
```

## Sections

### Required VMs (only for local VMs)

- Use this section only if the lab runs on local VMs that participants must start. Place it before Setup and list every VM that the lab needs, one bullet per VM with the bold name.
- Omit the section in online lab environments, in which the machines are already available, and if no VMs are needed.

### Setup

- Start with the sign-ins, as a numbered list. Name the machine and the account for each sign-in.
- Then name the prerequisites: each lab or practice the participant must have completed, with a link, and the catch-up script that replaces it if it was skipped.
- Link to other labs and practices with a relative path.
- The section contains no lab steps.
- Never write negative requirements such as "No previous lab is required" or "No preparation is needed". If there is no prerequisite, omit the sentence.

### Introduction

- Describe the business scenario and what the participant must achieve, in two to four sentences.
- Name no VMs, values, or steps here.

### Exercises

- Group the steps into exercises by topic. Each exercise title names its goal, for example `Manage domain users`.
- List the exercises as a numbered table of contents with links to the exercise headings.

### Exercise steps

- The numbered steps under an exercise are the tasks. A lab has no separate `Task` headings.
- Each step states one goal and names the machine in its first words when the machine is not the one from the previous step, for example `On **VN1-SRV5**, ...`.
- Each step should be completed on one single machine. A step must not require switching between machines. If a step requires multiple machines, split it into several steps.
- A step with a how-to links to the matching general instruction in an indented paragraph below the step. Do not describe the clicks or PowerShell commands in the lab step.
- If the step uses values, put them in a table with a header row, in a bullet list, or in a code block with variables. Empty variables for values the participant must enter get a comment.
- A step that depends on an earlier step says so, for example `Use the variables from the previous step.`
- If the participant must check the result, add an indented paragraph below the step, starting with `Verify that`.
- Notes are indented paragraphs with `*Note:*`.

## Checklist before handover

- [ ] Title: `# Lab: <Title>`, and the file name in `Instructions/Labs/` matches the title with hyphens.
- [ ] The lab belongs to exactly one module and takes 15 minutes or more.
- [ ] Sections appear in this order: Required VMs (only for local VMs), Setup, Introduction, Exercises, then the exercises.
- [ ] Setup names the sign-ins, and the catch-up scripts for skipped labs and practices.
- [ ] The exercise table of contents links to every exercise, and the anchors match the exercise headings.
- [ ] Every step states one goal and names its machine when the machine changes.
- [ ] Every step with a how-to links to an existing general instruction, placed in an indented paragraph below the step.
- [ ] Every step with a visible result has a verification paragraph.
- [ ] Input data is in tables with header rows, or in variables with comments.
- [ ] No `Task` headings, no `Instructions` section, and no introduction or conclusion outside the sections.
