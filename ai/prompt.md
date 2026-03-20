---
description: Review AI system prompts for clarity, structure, safety, token efficiency, and effectiveness
---

Review the prompt in $ARGUMENTS (file path or inline text).

**Step 1** — Read the prompt file or text and identify its purpose and target model.

**Clarity & Intent**
- The goal of the prompt is unambiguous
- No conflicting instructions that the model must guess between
- Persona or role definition is specific (not just "you are a helpful assistant")

**Structure**
- Instructions ordered from most to least important
- Examples provided for non-obvious output formats (few-shot)
- Output format explicitly specified (JSON, markdown, plain text, etc.)
- Edge cases and what to do when inputs are missing or ambiguous

**Effectiveness**
- Vague qualifiers removed ("good", "high quality") — replaced with specific criteria
- Negative instructions ("do not") minimized — state what to do instead
- Chain-of-thought elicited where reasoning improves output quality
- Unnecessary filler and politeness removed (token waste)

**Safety & Guardrails**
- Prompt injection attack surface identified (user input concatenated into system prompt)
- Output validated downstream — is the prompt relied on exclusively for safety?
- PII or sensitive data instructed to be excluded from output
- Hallucination risk: prompt asks for facts without a retrieval source

**Token Efficiency**
- Repeated instructions that appear more than once
- Context included that the model doesn't need for the task
- Static content that could be cached (Anthropic prompt caching)
- Estimated token count and whether a smaller model could handle the task

**Model-Specific**
- Tool/function definitions clear with accurate descriptions and types
- `max_tokens` set appropriately for expected output length
- Temperature appropriate for task (0 for deterministic, higher for creative)

Output findings as a prioritized list: **Critical > Major > Minor**. Suggest a revised version of any Critical/Major sections.
