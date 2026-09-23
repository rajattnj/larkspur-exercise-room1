# Overnight review: Larkspur disruption-care agent

**To:** rajattnj_larkspur-exercise-room1  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-22 17:24

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Overnight, Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. PITCH.md picks 'Lever' as a placeholder, still literally <cost | speed | intelligence>, with no choice made.**

The Lever line in PITCH.md reads exactly "Lever: <cost | speed | intelligence>", the template text untouched. Priya's model question is a cost/speed/intelligence tradeoff and this file is the one place the team was asked to name which axis they are optimizing. Nothing else in the repo picks one either.

Fill in Lever in PITCH.md with one of cost, speed, or intelligence and paste the updated file.

**2. TONE_ADDENDUM is 0 characters, so the tone question PITCH.md defers is not a model problem at all.**

PITCH.md's own "Still broken" line says "Tone handling for abusive messages is deferred to Build 4," and the static scan confirms TONE_ADDENDUM sits at 0 characters. That is a prompt-writing task, not a capability gap, and a bigger model behind an empty addendum still gets no tone instructions.

Run python3 run.py <PNR> --trace against an abusive-tone message once TONE_ADDENDUM is written and paste the response.

**3. fare_rules() in agent.py reads a local markdown file with no exception handling around the open() call.**

fare_rules(section) does path = os.path.join(...,"fare_rules_excerpt.md") then text = open(path, encoding="utf-8").read() with no try/except, unlike the rest of tool_results() which the scaffold comment notes runs error-returning branches. If the file is missing or the section argument is malformed the tool throws instead of returning the message string the function is designed to produce for a no-match case.

Run python3 verify.py 1.3 and paste the result to confirm fare_rules fails closed rather than raising.

**4. search_alternatives description grew from "search" (7 characters) to 207 characters in this diff, but no eval case measures whether that changed tool selection.**

The diff replaces the placeholder description "search" with a 207-character description telling Claude to "provide the PNR and review the returned options before offering one." There is no evals/cases.json in this repository and no readout-trace.json, so nothing shows whether that rewrite changed how often or how correctly the tool gets called.

Run python3 eval_harness.py once eval cases exist and paste the pass rate for search_alternatives-triggering cases.

**5. No readout-trace.json survived the push, so the loop's turns counter and MAX_TOOL_CALLS=8 cap are both unexercised by any committed run.**

The diff moves answer = text_of(response) to after the while loop and changes messages.append to append response.content instead of text_of(response), which changes what gets sent back on multi-turn tool calls. With zero committed wire runs, there is no evidence this survives more than one or two tool_use turns before hitting MAX_TOOL_CALLS = 8.

Run python3 run.py --all --trace and paste the totals footer showing turns per case.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (293 lines)`
- `PITCH.md`
- `TEAM.md (unchanged template)`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
