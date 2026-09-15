# Overnight review: Larkspur disruption-care agent

**To:** danielasfora__blueteam  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-09-15 13:02

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

**1. agent.py wires an MCP server into tool_list() but the tool description gap remains uneven across the nine schemas.**

The diff changes tool_list() from build_tools() + EXTRA_TOOLS to build_tools() + mcp_client.tools(), and separately rewrites search_alternatives's description from the placeholder string "search" to a 196-character description. hold_seat is still 73 characters and send_confirmation is still 71 characters, both far short of check_policy's 445. No model swap touches those two strings.

Run python3 run.py --show-tools and paste the full list so the remaining short descriptions can be compared against what Claude actually does with hold_seat and send_confirmation.

**2. PITCH.md's Number line claims 5 of 5 shapes resolved but the repository holds only one committed trace.**

PITCH.md states "5 shapes tested; 22 turns, 74,624 tokens in total" and "After: 5 of 5 end_turn," but readout-trace.json shows a single run: 4 API turns, 4 tool calls, 16,029 tokens in and 622 out. There is no evals/cases.json and no second trace file in this material backing the aggregate 22-turn, 74,624-token figure.

Run python3 run.py --all --trace and paste the totals footer so the 22-turn, 74,624-token claim in PITCH.md has a matching artifact.

**3. PITCH.md flags a missing tone gate on R8KD3F while TONE_ADDENDUM sits at 0 characters in agent.py.**

The Still broken line reads "No tone gate. An abusive message (R8KD3F) gets a calm, helpful answer with no escalation." The static scan confirms TONE_ADDENDUM is still empty at 0 characters, and the diff touching agent.py does not write to that slot. This is a prompt-content gap, not a capability gap a different model would close on its own.

Run python3 verify.py 4.1 to check whether the tone gate this pitch flags as missing has a bound gate result.

**4. The banked gates in readout.html cover 2.1 and 2.2 only, leaving MAX_TOOL_CALLS and the escalation path unverified.**

The evidence block lists "gates banked: 2.1, 2.2" with nothing for the confirm_rebooking guardrail step or the tone/escalation step described in PITCH.md's Guardrail line. MAX_TOOL_CALLS is hard-capped at 8 in agent.py and nothing in the visible material shows a run that exercises that ceiling.

Run python3 verify.py 4.1 and python3 verify.py 3.1 and paste both results to close the gap between what PITCH.md claims and what is banked.

**5. The last committed trace shows a next_available_day call that is not in the nine declared tool schemas.**

readout-trace.json lists the tool call sequence as lookup_booking, get_flight_status, next_available_day, get_flight_status, but next_available_day appears in agent.py only as an import from support, not among the nine schemas the static scan counted. EXTRA_TOOLS is declared but at 0 entries, and LOCAL_TOOLS has no executors, so this call's schema origin is not visible in the material reviewed here.

Run python3 run.py --show-tools and check whether next_available_day appears, then paste the mcp_client.tools() output it would come from.

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

- `agent.py (225 lines)`
- `PITCH.md`
- `TEAM.md (unchanged template)`
- `readout-trace.json`
- `readout.html (evidence block)`

Reviewer: `claude-sonnet-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
