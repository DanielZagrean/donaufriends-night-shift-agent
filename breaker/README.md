# breaker/: B4 Best Breaker (Team Donaufriends)

Working folder for the Break it attacks. **Only within the competition interface**
(synthetic task workspaces of other teams' agents). No real systems, people or vendors.

| File | Purpose |
|---|---|
| [`candidates.md`](candidates.md) | Attack candidates + rules + success criteria + reasoning |
| `payloads.json` | Machine-readable candidates (carrier/goal/text) |
| `validate_payload.py` | Checks the **mechanical** validation rules locally |
| `analyze_payloads.py` | **Read-only** analysis of `GET /payloads` (placements/hits) |

## Usage
```bash
python3 breaker/validate_payload.py          # candidates against all mechanical rules
python3 breaker/analyze_payloads.py          # own payloads + hits (needs the .env keys)
```

## Rules that code can NOT check (human review)
No real people, companies or products · nothing offensive · nothing against the platform or providers ·
**our own agent must not recognise our own attack text** (no harness code, no signatures).

## Submitting / moving = only with explicit approval
`POST /payloads` and `PATCH /payloads/{id}` (retire / stage) are **not** run without an explicit go-ahead.
