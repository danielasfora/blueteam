# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A multi-turn Claude agent connected to 9 Larkspur operations tools and 2 read-only MCP tools (next_available_day, fare_rules) served by a separate MCP server.
Does: Looks up the customer's booking, checks live flight status, applies Larkspur disruption policy, and tells the stranded customer what they are owed — rebooking waiver, refund eligibility, or care vouchers — in 3–4 turns without asking them to repeat themselves.
Number: 0/5 shapes resolved before the loop was fixed; 5/5 after, averaging 3.8 API turns and 2.8 tool calls per resolved contact. Schema cost: 2,376 tokens per turn (9 tools) to 2,848 (11 tools, 2 via MCP).
Guardrail: Rebooking is irreversible and requires a confirmation_token only the customer's own Confirm-click produces; the agent cannot supply one itself. Proven: confirm_rebooking was never called across all 5 shapes because no token was ever present.
Next: Tone detection on the way in, the full hold-and-confirm rebooking flow end to end, passenger count passed to next_available_day, and a dollar-per-contact measurement against real volumes.
Still broken: An abusive message still gets a calm, helpful answer. There is no tone gate on the way in, and the agent does not detect or respond differently to hostile language.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
