# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A multi-tool disruption-care agent for Larkspur Airlines that handles cancelled and delayed flight conversations end-to-end.
Does: Looks up bookings, checks live flight status and policy, issues vouchers, and rebooks customers — reducing calls escalated to human agents.
Number: 4 tool calls per conversation on average; 4 out of 5 disruption shapes resolved without human escalation.
Guardrail: Rebooking is irreversible — confirm_rebooking requires a token only the customer's own Confirm-click can produce. The agent cannot supply it, and "the customer said yes" in chat does not substitute for it.
Next: Tighten date-format handling to eliminate the extra turn Claude wastes correcting MM/DD/YYYY to YYYY-MM-DD on every flight status lookup.
Still broken: Abusive-message tone — the agent resolves R8KD3F calmly with no escalation or tone gate. Build 4 closes this.
Lever: intelligence

## Priya asked

Costs: ~17,000 tokens per complex conversation (~$0.05–0.10 per case at current API pricing). Schema overhead is 2,848 tokens on every turn regardless of what fires.
Wrong: Claude occasionally passes the wrong date format to get_flight_status, burning an extra API turn to self-correct. No data loss, but avoidable latency.
Runs it: Any web interface that calls run_agent(pnr, last_name, message) — the demo server at demo/serve.py shows it working in a browser today.
Left out: Group bookings, voluntary change payment collection, and refund processing all escalate to humans. Multi-passenger coordination is out of scope for this build.
