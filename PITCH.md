# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A multi-turn Larkspur disruption-care agent with tool routing and local extensions.
Does: Runs a multi-turn disruption conversation and returns Claude's final answer after all required tool calls.
Number: 11 tools; 2,391 to 2,840 input-schema tokens per turn (+449).
Safety check: Requires booking and flight context before policy decisions; irreversible rebooking still requires a confirmation token.
Next: Run the before-and-after intelligence bench across the Stage 2 cases.
Still broken: Fare-rules routing and the intelligence improvement still need broader measured coverage.
Lever: cost

## Priya asked

Costs:
Wrong: The original prompt treated an abusive legal threat like a normal disruption request.
Runs it: python run.py R8KD3F --last-name Brandt --message "You people are absolutely useless and I'm calling my lawyer in the morning." --trace
Left out: The MCP probe proved next_available_day, but fare_rules still needs its own routing case; Stage 2 needs before-and-after runs.
