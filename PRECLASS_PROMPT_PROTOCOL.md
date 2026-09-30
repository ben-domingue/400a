# Pre-class prompt protocol

This is the standing spec for EDUC 400A pre-class prompts. Before each class, students paste a prompt into an AI assistant, which tutors them through ideas they will meet in the lesson. They do this before they have seen the lesson slides, and many have little or no stats background.

`histogram_prompt.txt` is the model. When this document is unclear, do what that file does.

## Paths never change

Students get links to these files. Once a prompt has been shared, its path is fixed:

- Revise a prompt by editing it in place. Don't rename it, move it, change its extension, or replace it with a new file.
- If a rule below conflicts with an existing path (e.g., an older prompt is `.md` rather than `.txt`), keep the path and apply the rule to the contents only.
- New prompts go in the repo root as `<topic>_prompt.txt`.

## Format

- **Plain text only.** Don't use markdown headers, bold, tables or bullet syntax that relies on rendering. Prompts get pasted into many tools, and markdown can show up raw. Numbered lists and simple indentation are fine, as in the histogram prompt.
- **The file is the prompt.** Everything in it gets pasted. Don't include notes to students ("copy everything below the line…"). Those go on the course site.
- **Student's voice, addressed to the AI.** The first sentence is "You are guiding me through a pre-class learning activity about <topic>."
- **Opening paragraph sets the pace.** Assume little or no stats background. One idea at a time. Show an example, say what to notice, ask one simple question, and wait for my answer before moving on. Use plain language, and define jargon before using it.
- **A short guardrails paragraph follows it.** It holds three things in 1–3 sentences each:
  1. Length: "This session should take 15–30 minutes. Stick to the steps below and don't add extra topics."
  2. In-class exercises: name the specific kinds of problems not to solve, e.g., "If I paste in problems like …, help me set up the picture and the approach, but let me finish them myself."
  3. Optionally, 3–5 common mistakes to watch for, in one line. Mistakes can go in the relevant step instead.
- **A linear script of numbered steps**, each headed `STEP N — Title` (capital STEP, an em dash, title case). The AI follows them in order. No menus of optional topics, no time-budget tables, no widgets to choose from, and no opening intake questions about the student's level or available time.

## Step 1: setup

- The heading is `STEP 1 — Set up (do this yourself, don't ask me for anything)`.
- The AI loads the datasets itself, naming each source specifically (site, R package, file).
- It includes this fallback line, nearly verbatim: "If one fails to load, quietly substitute a similar public dataset and tell me what you swapped."
- It describes each dataset in a few plain sentences: where it came from, what one row represents, and what the key variables mean in everyday terms. No tables of variable names.
- When there is an assigned reading or video, it briefly summarizes it. The prompt should carry its own summary of the reading, so the AI doesn't depend on opening links. If the reading has alternative routes (e.g., a textbook chapter or a lighter video), Step 1 may ask the student one question: which route they took. That is the only question Step 1 asks.

## Each teaching step

- Introduces **one idea**, using a plot or example the AI actually produces (not just describes), and says what to notice in it.
- Ends with **one specific question, written out in quotes**, for the AI to ask. One question per step.
- Includes **a hint** for when the student is stuck.
- Includes **guidance on how to respond**, e.g., "say what's reasonable about my answer, then one thing I might not have considered."
- Connects to earlier prompts where it fits (the same datasets, or a question the student already answered).

## Data

- Prefer real, public education data over coins and dice. The defaults, reused across prompts so students build familiarity:
  - SEDA district-level mean test scores (edopportunity.org). The "get the data" page asks for an email, so an AI can't script it; give the direct file from the Stanford Digital Repository instead (SEDA 6.0: https://stacks.stanford.edu/file/xh833nn4025/seda_geodist_pool_cs_6.0.csv, rows with subgroup "all", score `cs_mn_avg_ol`, where 0 is the national average and the units are student SDs). Covariates, such as enrollment `totenrl`, are in `seda_cov_geodist_pool_6.0.csv` at the same location, matched on `sedalea`.
  - NAEP state average scale scores (nationsreportcard.gov or its API)
  - Tennessee STAR student-level data (`data("STAR")` from the R package `AER`, or the Harvard Dataverse CSV)
- Always include the fallback line from Step 1.
- Coins, dice and simulations are fine when an idea is inherently about a random process (e.g., the gambler's fallacy). Tie them back to education data when possible.
- Avoid datasets and examples the lesson uses for its in-class exercises.
- Test that each dataset actually loads, and that the variable behaves the way the step claims (e.g., a "skewed" variable really is skewed, a "continuous" score isn't just a few dozen values).

## Length and scope

- The session takes 15–30 minutes. Students won't do longer.
- Aim for 5 steps: setup, 3–4 idea steps, and the ending. The ending can be its own short step or can close the last idea step, as in the histogram prompt. Never go beyond 6 steps.
- Build intuition for the upcoming lesson. Students haven't seen the slides, so the goal is hooks to hang ideas on, not mastery.
- Don't solve problems that look like in-class exercises. The AI helps set up the picture or approach and lets the student finish. List the specific problem types in the guardrails paragraph.

## Ending

- The final step asks the student to write 2–3 sentences in their own words explaining the lesson's key idea to a friend who hasn't taken the class. The request is written out in quotes.
- The AI gives brief, encouraging feedback and points out anything the student got right that they might not have realized was important.
- It closes with a short recap of the plots and the student's answers, so the student can bring it to class.

## Process for writing a new prompt

1. Read the lesson slides (a .pptx or its text) and the assigned pre-reading or video.
2. List the lesson's core ideas and its in-class exercises, which the prompt must not pre-solve.
3. Pick 3–4 ideas to prepare students for, and choose datasets and plots for each.
4. Draft in the STEP format and check it against the checklist below.
5. Test it: paste the prompt into a fresh Claude chat and play a student with a weak stats background for a few turns. Confirm that the datasets load (or the fallbacks work), the questions make sense, and the pacing fits 15–30 minutes.

## Checklist

- [ ] Path unchanged for an existing prompt; new prompts are `<topic>_prompt.txt` in the repo root
- [ ] Plain text: no markdown headers, bold or tables; no notes to students
- [ ] Opens with "You are guiding me through a pre-class learning activity about …"
- [ ] Opening paragraph: low background, one idea at a time, example, what to notice, one question, wait, plain language, define jargon
- [ ] Guardrails: 15–30 minute line, specific in-class problem types to avoid, optional 3–5 common mistakes
- [ ] Linear `STEP N — Title` script, about 5 steps and never more than 6, with no menus, tables or intake questions
- [ ] Step 1 is do-it-yourself setup: loads data, includes the fallback line, describes each dataset, summarizes the reading (asking at most which route the student took)
- [ ] Each idea step: one idea, a plot or example the AI makes, what to notice, one quoted question, a hint, response guidance
- [ ] Real public education data (SEDA, NAEP, STAR) where it fits; simulations only for inherently random processes
- [ ] No in-class exercises pre-solved
- [ ] Ending: quoted 2–3 sentence explain-to-a-friend request, encouraging feedback, recap of plots and answers
- [ ] Tested in a fresh chat as a weak-background student
