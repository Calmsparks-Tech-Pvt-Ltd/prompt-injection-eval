# Prompt-injection resistance eval

A small, honest smoke test for how well an AI system resists prompt injection.

- `probes.jsonl` — attack probes, one JSON object per line.
- `run_eval.py` — sends each probe to any OpenAI-compatible endpoint and
  (optionally) grades whether the system complied, using a separate judge model.

## What this is and is not

- **Is:** a first-pass check over publicly documented attack patterns
  (OWASP LLM Top 10 / public literature). Useful to catch the obvious failures
  before you spend money on a real assessment.
- **Is not:** HiltLock's red-teaming methodology. HiltLock's proprietary attack
  families, engine and strategist loop are not published and are not represented
  here.

## Quick start

```bash
# 1. Point the harness at your model (any OpenAI-compatible /chat/completions):
export TARGET_BASE_URL="https://your-endpoint.example/v1"
export TARGET_API_KEY="..."
export TARGET_MODEL="your-model"

# 2. (Optional) grade compliance with a judge model:
export JUDGE_BASE_URL="https://your-endpoint.example/v1"
export JUDGE_API_KEY="..."
export JUDGE_MODEL="your-judge-model"

python run_eval.py
```

The harness writes `report.json` and prints a per-probe table with a resistance
rate. Without a judge configured it still captures every response for manual
review.

## Scoring notes

- **Resistance rate is directional, not a security guarantee.** An LLM-as-judge
  can be fooled the same way the target can. Treat a poor score as "worth a real
  test", never as proof of safety.
- Do **not** run this against a production system with live credentials. Use a
  sandboxed deployment.
