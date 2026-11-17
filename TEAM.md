# Donaufriends (team-02): IBM Night Shift Agent

Efficient Local Agents Hackathon · IBM Vienna · Sat 14 Nov 2026
Challenge: **The MuggingFace Incident**. Small model. Smart harness.

Our agent solves the incident tasks of the Task API, **correctly and cheaply**.
Model: **`google/gemma-4-31b-it`** (+ `typesafe/jev-1.14`, `qwen/qwen3-embedding-8b`). Dev budget **$15**.

- Starter kit docs (commands, flags): [README.md](README.md)
- Rules for agents: [AGENTS.md](AGENTS.md)
- Strategy: [PLAYBOOK.md](PLAYBOOK.md)

## Setup

```bash
git clone https://github.com/DanielZagrean/donaufriends-night-shift-agent.git
cd donaufriends-night-shift-agent
cp .env.example .env   # add ARENA_API_KEY + OPENROUTER_API_KEY from the dashboard / team
uv sync
uv run main.py --kind dev --tasks t01 --note "baseline"
```

Adding packages: `uv add <package>` (updates `pyproject.toml` + `uv.lock`, commit both).
Installing uv (Mac): `brew install uv`

**Save budget:** `--tasks t01,t03`, `--level 1 --limit 6`, `--match '<regex>'`, `--seed <seed> --tasks …`. Full runs (48 tasks) only to confirm.

## Team and roles

| Role | Who | Responsibility |
|---|---|---|
| Infra | _TBD_ | Client, workspace mirror, parsers with locators, Dockerfile, budget and time guards, submit |
| Solver | _TBD_ | Instruction parser, compiler (B1), agent loop fallback |
| Eval + security | _TBD_ | Data collector, offline eval, guardrails, answer validator |
| Breaker | _TBD_ | Break it attacks (B4), hits from other teams → guardrail tests |

## Git rules

- `main` is **always runnable**.
- Code goes on its own branch: `name/feature` (e.g. `michel/json-retry`). Merge after a successful eval run.
- **Commit before every run**, always with `--note "<hypothesis>"`.
- **Never commit keys.** Keys only in `.env`.
- **Share context right away:** organiser updates, findings and measurements go into the repo. Docs go straight to `main` and are pushed immediately.
- Before every task: `git pull --rebase`.

## Schedule (Sat)

| Time | What |
|---|---|
| ~10:00 | Baseline: `uv run main.py --kind dev --tasks t01 --note "baseline"`, **note score + cost** |
| 10:30 | First Break it attack (B4) |
| 11:30 | Data collector + offline eval ready |
| 12:00 | Pizza |
| 14:00 | **Demo submission 1** |
| 16:30–16:45 | **Upload the final submission** |
| 17:00 | Everything locked |

## Baseline / results

| Version | Run ID | Tasks | Score | Cost | Note |
|---|---|---|---|---|---|
| Starter kit (c2ab907) | run_7FdiWah57oDE | t01 | 0.77 (sources 1/4) | $0.0045–0.007 | Answer correct, sources incomplete |
| Router fix + earliest_slot (0af3cc7) | run_hP6Aq5nhZhYl | all 48 | A 0.557 · final 0.322 | $1.70 | First full run, cost too high |
| + max_steps 14 (a0ae1fb) | run_VLE9AicO_TF3 | all 48 (replay) | A 0.578 · final 0.348 | $1.24 | Same seed, −27 % cost |
| + all code tools (431e3ec) | run__8OvzdDTetNJ | all 48, fresh seed | **A 0.700 · final 0.434** | **$0.97** | 0 rule violations, 11/48 at the step limit |
