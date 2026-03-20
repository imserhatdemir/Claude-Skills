---
description: Estimate Claude or OpenAI API usage cost for a given feature or workflow
---

Estimate AI API cost for $ARGUMENTS (feature description, prompt file, or workflow description).

**Step 1** — Read the relevant code/prompts and identify all AI API call points.

**Step 2 — Identify Usage Pattern**
- How many API calls per user action?
- How many user actions per day / month (estimate)?
- Is this a batch job or real-time request?

**Step 3 — Token Count Estimate**
For each call, estimate:
- System prompt tokens (count or estimate from file)
- User message tokens (average input size)
- Assistant response tokens (average output size)
- Total tokens per call = input + output

Rule of thumb: ~1 token per 0.75 English words, ~1 token per 3-4 characters.

**Step 4 — Model Selection**
| Model | Input (per 1M tokens) | Output (per 1M tokens) | Best for |
|---|---|---|---|
| claude-haiku-4-5 | $0.80 | $4.00 | High volume, simple tasks |
| claude-sonnet-4-6 | $3.00 | $15.00 | Balanced quality/cost |
| claude-opus-4-6 | $15.00 | $75.00 | Complex reasoning |

**Step 5 — Cost Calculation**
```
Daily calls = [user actions/day] x [calls per action]
Daily input tokens = daily calls x avg input tokens
Daily output tokens = daily calls x avg output tokens
Daily cost = (input tokens / 1M x input price) + (output tokens / 1M x output price)
Monthly cost = daily cost x 30
```

**Step 6 — Optimization Opportunities**
- Prompt caching applicable? (repeated system prompts)
- Smaller model sufficient for this task?
- Batch API available and acceptable latency?
- Response length reducible with tighter output format?

Output: cost estimate table (daily / monthly) for each model option, with a recommended model and optimization actions sorted by savings impact.
