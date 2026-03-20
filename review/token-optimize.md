---
description: Analyze and optimize AI token usage in prompts, context windows, and API calls
---

Analyze token usage in $ARGUMENTS (prompt file, API call code, or workflow description).

**Step 1** — Read the target file(s) and identify all AI API calls, system prompts, and context construction.

**Prompt Efficiency**
- Redundant or repeated instructions in system prompt
- Verbose phrasing that can be compressed without losing meaning
- Static context included that the model doesn't need for the task
- Examples that are longer than necessary for the pattern to be clear

**Context Window**
- Context constructed dynamically — is the maximum size bounded?
- Retrieved chunks (RAG) trimmed to relevant sections, not full documents
- Conversation history pruned or summarized for long sessions
- System prompt size relative to available space for user input + response

**API Call Patterns**
- Unnecessary round-trips that could be combined
- Streaming used where appropriate for UX (or avoided where not needed)
- `max_tokens` set appropriately — not leaving headroom for responses that will be truncated
- Prompt caching applicable for repeated system prompts (Anthropic)

**Cost Reduction**
- Smaller model sufficient for simpler tasks (route by complexity)
- Batch API used for non-real-time workloads
- Response format constrained to reduce output tokens (JSON schema, short answers)
- Embeddings cached instead of recomputed

Output: token count estimates, cost projection, and prioritized optimization recommendations sorted by savings impact.
