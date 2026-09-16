# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A multi-tool disruption-care agent for Larkspur Airlines, connected to the Claude Messages API with 11 tools and an MCP server.
Does: Looks up bookings, checks live flight status and policy, issues vouchers, and rebooks customers — resolving disruption contacts without a human agent.
Number: 5 shapes tested; 22 turns, 74,624 tokens in total. Before fix: loop failed on turn 2 with a 400 error, 0 of 5 shapes resolved. After: 5 of 5 end_turn.
Guardrail: confirm_rebooking requires a token only the customer's own Confirm-click can produce. The agent cannot supply it from chat alone — proved by the demo server's /api/confirm endpoint refusing a made-up token.
Next: Fix the date-format error that costs one extra turn on every flight status lookup — a field description change, not a code change.
Still broken: The date field in get_flight_status still says MM/DD/YYYY, which costs one extra retry turn on every flight status lookup — a one-word fix in the schema description that was not in the canon we shipped.
Lever: intelligence

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
