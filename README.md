# HiltLock Open Research

Public, reusable assets that show how generative AI systems are broken, and how to
test them. Two artifacts live here:

1. **`prompt-injection-eval/`** — a small benchmark: a set of prompt-injection
   probes plus a dependency-free Python harness that runs them against any
   OpenAI-compatible endpoint and (optionally) grades resistance with a judge
   model.
2. **`anonymized-findings/`** — a structured, anonymized dataset of red-team
   findings, derived strictly from what is already published on
   <https://hiltlock.com/evidence>.

## What is deliberately NOT here (our edge)

- HiltLock's internal attack-family library, the attack engine, the 19-family
  taxonomy, and the RL/strategist loop are **proprietary** and are not published.
- The benchmark uses only **publicly documented** attack patterns (OWASP LLM Top 10
  and public prompt-injection literature). It is a smoke test, not a full red
  team, and it is not the methodology we sell.
- The findings dataset contains **only facts already published** on the evidence
  page. Nothing here reveals a client, a technique we have not already written
  about, or any detail that could deanonymize an engagement.

## Anonymization checklist (applied to every row)

- No client, vendor, or partner names.
- No endpoints, hostnames, tool names, or field names.
- No payloads or exact strings that could be used to identify a target.
- No unpublished numbers. Every statistic traces to a published case study.

## License

- Code (`run_eval.py`): MIT.
- Data (`probes.jsonl`, `findings.jsonl`): CC-BY-4.0 (you may reuse with attribution).

---

## 1. Publish the benchmark to GitHub

The GitHub organisation is `Calmsparks-Tech-Pvt-Ltd`.

```bash
cd open-source/prompt-injection-eval

git init
git add .
git commit -m "Initial release: prompt-injection resistance eval"

# If you use the GitHub CLI:
gh repo create Calmsparks-Tech-Pvt-Ltd/prompt-injection-eval --public --source=. --push

# Or without the CLI: create an empty public repo named `prompt-injection-eval`
# on github.com, then:
git remote add origin https://github.com/Calmsparks-Tech-Pvt-Ltd/prompt-injection-eval.git
git branch -M main
git push -u origin main
```

Then add the topic tags `llm-security`, `prompt-injection`, `red-teaming` on the
repo page so it surfaces in GitHub search.

## 2. Publish the dataset to Hugging Face

```bash
pip install huggingface_hub
huggingface-cli login

# Upload the findings dataset to a dataset repo:
cd open-source/anonymized-findings
huggingface-cli upload Calmsparks-Tech-Pvt-Ltd/hiltlock-anonymized-findings findings.jsonl
```

If you prefer the web UI: go to huggingface.co → New → Dataset → name it
`hiltlock-anonymized-findings`, then drag `findings.jsonl` into the Files tab.
Add the tags `ai-security`, `red-teaming`, `prompt-injection`, `llm`.

## 3. (Optional) Link from the website

Once both are live, add a short "Open research" note on the evidence page linking
to the GitHub repo and the HF dataset. That turns these assets into inbound links
for the main site.
