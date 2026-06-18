# Prompt Engineering

## What is Prompt Engineering?

Prompt engineering is the practice of **designing and optimizing input instructions** to guide LLMs toward producing desired outputs — without modifying model weights. It is the most accessible and cost-effective way to control LLM behavior.

---

## Core Principles

1. **Be Specific**: Vague prompts → vague outputs. Constrain the format, length, style, and scope.
2. **Provide Context**: Give the model the information it needs to answer correctly.
3. **Use Examples**: Demonstrations are often clearer than descriptions.
4. **Assign a Role**: "You are a senior data scientist..." sets the tone and expertise level.
5. **Iterate**: Prompt engineering is empirical — test, evaluate, refine.

---

## Prompting Techniques

### Zero-Shot Prompting
No examples provided. Relies entirely on the model's pre-trained knowledge.

```
Classify the sentiment of this review as Positive, Negative, or Neutral:
"The battery life is amazing but the screen is dim."
```

### Few-Shot Prompting
Provide a few input-output examples before the actual query.

```
Classify the sentiment:
"Great product!" → Positive
"Terrible experience." → Negative
"The battery life is amazing but the screen is dim." →
```

> **Tip**: Choose diverse, representative examples. Order can matter — place similar examples last.

### Chain-of-Thought (CoT)
Instruct the model to reason step-by-step before answering.

```
Q: If a store has 45 apples and sells 3/5 of them, how many remain?
A: Let's think step by step.
   Total apples = 45
   Sold = 3/5 × 45 = 27
   Remaining = 45 - 27 = 18
```

- **Zero-shot CoT**: Simply append *"Let's think step by step"* to the prompt.
- Significantly improves performance on math, logic, and multi-step reasoning tasks.

### Self-Consistency
Generate multiple CoT reasoning paths → take the **majority vote** on the final answer. Improves robustness over single CoT.

### Tree of Thoughts (ToT)
Explores multiple reasoning branches at each step (like a search tree). The model evaluates and prunes branches. Best for complex planning / puzzle-solving tasks.

### ReAct (Reason + Act)
Interleaves reasoning traces with actions (tool calls, searches). The model thinks about what to do, acts, observes the result, and repeats.

```
Thought: I need to find the population of France.
Action: search("population of France 2024")
Observation: 68.4 million
Thought: Now I can answer the question.
Answer: The population of France is approximately 68.4 million.
```

### Directional Stimulus Prompting
Include a small hint or keyword in the prompt to steer the model toward the desired output without giving the full answer.

---

## Prompt Structure Template

```
[System/Role]    → Define who the model is
[Context]        → Provide background information
[Instruction]    → What you want the model to do
[Input Data]     → The specific data to process
[Output Format]  → How the output should be structured
[Constraints]    → Any restrictions or guardrails
[Examples]       → Few-shot demonstrations (optional)
```

**Example:**
```
You are an expert legal analyst.

Given the following contract clause, identify any risks for the buyer.

Clause: "The seller may terminate this agreement at any time with 7 days' notice."

Respond in JSON format:
{
  "risks": ["..."],
  "severity": "low | medium | high",
  "recommendation": "..."
}

Keep your response under 200 words.
```

---

## Advanced Techniques

| Technique | Description |
|---|---|
| **Prompt Chaining** | Break complex tasks into sequential sub-prompts; output of one feeds into the next |
| **Generated Knowledge** | Ask the model to generate relevant facts first, then answer using those facts |
| **Least-to-Most** | Decompose problem into sub-problems, solve from simplest to hardest |
| **Meta-Prompting** | Ask the LLM to write/improve its own prompt |
| **Constrained Decoding** | Use structured output formats (JSON mode, grammar-constrained generation) |
| **Negative Prompting** | Tell the model what *not* to do: "Do not include opinions or speculation" |

---

## System Prompts vs User Prompts

| Aspect | System Prompt | User Prompt |
|---|---|---|
| Purpose | Set persistent behavior, persona, guardrails | Task-specific instructions and data |
| Persistence | Applied to every turn in the conversation | Changes per interaction |
| Priority | Generally higher (model treats as ground rules) | Lower (can be overridden by system prompt) |

---

## Evaluation & Optimization

- **A/B test** prompts on representative datasets.
- Use **automatic prompt optimization** tools (DSPy, OPIS, PromptBreeder).
- Track metrics: accuracy, consistency, format compliance, latency, cost.
- **Temperature**: Lower (0.0–0.3) for deterministic tasks; higher (0.7–1.0) for creative tasks.
- **Top-p / Top-k**: Control diversity of generated tokens.

---

## Common Pitfalls

- Overloading a single prompt with too many instructions.
- Assuming the model "remembers" — each API call is stateless (unless using conversation history).
- Not testing for adversarial inputs (prompt injection, jailbreaks).
- Ignoring token limits — long prompts can push out important context.
- Using ambiguous language ("make it better" vs "increase the F1 score by reducing false positives").
