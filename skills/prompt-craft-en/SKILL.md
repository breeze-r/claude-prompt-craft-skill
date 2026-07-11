---
name: prompt-craft-en
description: Write, optimize, review, and structure prompts for AI assistants (Claude, ChatGPT, Codex, Claude Code, agents). Use this skill whenever the user asks to write a prompt, optimize a prompt, fix/improve a prompt, review a prompt, turn a vague request into a reusable prompt, design system prompts / task instructions for agents, or asks why an AI output missed the mark and how to fix the instructions. Also trigger when the user wants prompt templates for daily Q&A, work deliverables, or coding tasks.
---

# Prompt Craft — Prompt Design & Optimization

Turn the user's intent into a clear, reusable, ready-to-run prompt. The methodology is a field-tested four-element framework: **Goal, Context, Output, Boundaries**.

A good prompt needs no special syntax or fixed template. Add elements only when they help — not every one, every time.

---

## Workflow

When the user asks you to write or optimize a prompt, follow these steps.

### 1. Identify the task type

| Type | Traits | Template |
|------|--------|----------|
| Everyday | A question, brainstorming, a draft, a comparison, a small plan | Short prompt, 1–3 sentences |
| Deliverable | Multiple sources/steps, produces a file, shown to others | Full four elements + final check |
| Code | Working on code, fixing a bug, writing tests, refactoring | Behavior + repro/location + constraints + how to verify |
| Agent / system | System prompts, automation, scheduled runs | Four elements + approval boundaries + failure handling |

### 2. Fill gaps quickly

If the user hasn't given enough to pin down a key element, ask at most one most-important question (Audience? Purpose? What must not change?). When there's basically enough, just start — write your assumptions as annotations next to the prompt instead of asking round after round.

### 3. Produce the prompt

- Put the final prompt in a code block for easy copying.
- Write the prompt in the user's target language (English for English models/contexts; otherwise the user's language).
- Add 2–4 sentences of notes: why it's organized this way, where it can be trimmed or adjusted.
- For complex tasks, offer two versions: a lean one and a full one.

### 4. When optimizing an existing prompt

Diagnose before rewriting. Check for the common ailments, in priority order:

1. **Unclear result**: lots of steps, but no statement of what to produce or for whom → rewrite around the result.
2. **Context noise**: irrelevant sources/background stuffed in → keep only what changes the result.
3. **Missing boundaries**: doesn't say what's off-limits or what needs approval → add the 1–2 that matter most.
4. **Over-control**: every step nailed down, no room to adjust → delete procedural instructions, keep the constraints.
5. **No verification**: an important task with no final check → add a closing self-check.

After rewriting, explain in one sentence what you changed and why.

---

## Core principles

### Start from the result, not the steps

Describe what to produce and who it's for. Describe the process only when the process itself matters — otherwise leave the model room to search, compare, and adjust.

**Weak**: First read the meeting notes, then extract the key points, then categorize them, then write a report…
**Strong**: Turn these meeting notes into a short progress update for the project team. Put decisions and next actions first.

### Add only context that changes the result

- For each source, say what to take from it — don't just dump the file.
- For images, point to the key regions.
- If it depends on current information, require a web search with sources.
- When related tasks need shared files, organize them in a project.

### Boundaries guard against "real trouble"

Don't pile on boundaries — watch the 1–2 that matter most: details that ruin the output if wrong, and actions that should be reviewed before they affect others.

A library of boundary phrases:

- Keep approved dates and budget numbers unchanged.
- Use only the sources I provide; flag anything missing instead of guessing.
- Keep recommendations within the agreed budget.
- Prepare it as a draft; don't send.
- Get my approval before sending, publishing, or changing anything others rely on.
- Don't change the shape of the API / keep the public interface stable.
- User-visible behavior must not change.

### State the purpose so the model picks the right form

Audience and purpose decide length, level of detail, and structure:

- "Make it a one-page summary a director can scan before the meeting."
- "Turn it into a follow-up email with decisions, owners, and due dates."
- "Make a comparison table and flag every difference over 10%."

### Important tasks need a final check

Before wrapping up, have the model self-check once:

- Confirm every action item has an owner and a due date.
- Flag information that can't be verified.
- Check that multiple outputs are consistent with each other.

### The first version needn't be perfect — converge by follow-up

Tell the user: review the first result → name specific changes ("open more directly, keep the evidence, move recommendations before background") → no need to start over. You can add sources, correct direction, ask for alternatives, or adjust the level of detail. Once a prompt works, save it for reuse.

---

## Scenario templates

### Everyday (short prompt)

```
[what result] + [key conditions] + [format/length]
```

Examples:
- Explain compound interest to someone who's never invested. Use one concrete example and define every term you introduce.
- Draft a friendly email declining this invitation because I'll be traveling. Under 120 words; leave the door open for future events.
- Compare these two plans for someone who travels abroad twice a year. Put differences in a table, then recommend one and name the trade-off.

### Deliverable (full four elements)

```
[Goal] Prepare [deliverable] for [audience/occasion].
[Context] Use [what] from [source A], plus [what] from [source B].
[Output] [structure: what goes first, which sections, length].
[Boundaries] [1–2 things that must not change / need approval].
[Final check] Before wrapping up, check [specific self-check items].
```

A worked example:

> Prepare a one-page project status update for Monday's leadership meeting. Use the latest project plan in Drive, plus relevant decisions and progress from the project's Slack channel.
> Put the decisions leadership needs to make and the next actions first. Summarize progress, risks, owners, and due dates. Keep approved dates and budget numbers unchanged. Flag any conflicting or missing information; don't send or publish anything.
> Before wrapping up, check that every next action has an owner and a due date.

### Code

Four parts: **desired behavior + relevant code/repro steps + constraints + how to verify**.

Bug fix (a repro recipe beats a high-level description):

```
Bug: [symptom]
Repro steps:
1) [start command]
2) [action]
3) [observed wrong result]
Constraints:
- Don't change the shape of the API.
- Keep the fix minimal; add a regression test if feasible.
Reproduce locally first, then propose a patch and run the checks. After fixing, run lint + the smallest relevant test set, and report the commands and results.
```

Key points for other code scenarios:
- **Explain a codebase**: name the files; ask for a checkable numbered list of steps + the files involved + the "gotchas" when changing things.
- **Write tests**: scope the exact function/line range; follow the project's existing test conventions; cover the happy path + edge cases.
- **Screenshot to prototype**: the image gives only visual requirements; spell out implementation constraints (framework, routing, component style) in words; also describe behaviors the image can't show (hover, validation, keyboard interaction).
- **Iterate on UI**: ask for 2–3 options → pick one → refine round by round with small, specific prompts ("only change the header: more whitespace, make sure it looks good on mobile"); tell the model which changes you rolled back manually so they don't get overwritten.
- **Refactor**: ask for a plan first (which files each milestone touches + a rollback strategy), review it, then execute milestone by milestone.

### Agent / system

On top of the four elements, add:

- **Approval boundaries**: which actions (send, publish, delete, pay, change shared data) must get human approval first.
- **Failure handling**: what to do when information is missing or sources conflict (flag it vs. stop and ask — don't guess).
- **Scope control**: allow stopping or narrowing when it starts doing work that isn't needed.
- **Path to reuse**: for recurring tasks, refine the prompt in ordinary conversation first; once the output is stable, harden it into a scheduled/automated task.

---

## Personalization and layering

Remind the user to separate two layers:

- **Preferences that apply across tasks** (tone, formatting habits, tech stack) → put them in custom instructions / user preferences / CLAUDE.md.
- **Details useful only to the current task** → write them in the prompt.

Mixing the two layers is the common reason prompts get longer and messier over time.

---

## Delivery checklist

Before handing the user a prompt, self-check:

- [ ] Are the result and audience clear?
- [ ] Does every piece of context change the result? (Delete the ones that don't.)
- [ ] Are there 1–2 boundaries guarding against real trouble?
- [ ] Does an important task have a final check?
- [ ] Did you nail down the process and rob the model of room to adjust?
- [ ] Is the prompt in a code block?
