---
title: "LLM Prompting & Testing"
seoTitle: "Effective LLM Prompting & Testing Strategies"
seoDescription: "Master AI prompt engineering with this comprehensive guide on constructing, testing, and evaluating LLM prompts for optimal performance"
datePublished: Mon May 26 2025 08:46:44 GMT+0000 (Coordinated Universal Time)
cuid: cmb4ufr94000u09li8gth2zmy
slug: llm-prompting-and-testing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748249475586/a09beca5-a57b-4802-ade2-ea03a27448c9.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1748249187548/c54e2d1b-938a-4a2d-9539-491bbdf4f71a.png
tags: ai, software-development, python, testing, qa, chatbot, basics, llm, promptengineering, promptfoo, evals, deepeval

---

If you're looking to **master prompt engineering**, **AI model behavior**, and **build testable, production-grade prompts**, this is your field guide. This guide walks through everything from **basic prompting anatomy** to **evaluations (Evals)** and **parameter tuning**.

---

## What is Prompt Engineering?

Prompt engineering is the process of crafting instructions to guide large language models (LLMs) in generating reliable, relevant, and safe responses.

A "prompt" is any input or instruction you send to the model.

---

## LLM Request Structure – API Anatomy

### Example Request (OpenAI SDK - Python):

```plaintext
pythonCopyEditfrom openai import OpenAI
client = OpenAI()

response = client.responses.create(
    model="gpt-4.1",
    input="Write a one-sentence bedtime story about a unicorn."
)

print(response.output_text)
```

### Key Parameters:

| Parameter | Description |
| --- | --- |
| `model` | The model version (e.g., `gpt-4.1`, `gpt-3.5-turbo`) |
| `input` | The user's prompt (text instruction) |
| `instructions` | High-level system-level instruction (e.g., “Talk like a pirate.”) |
| `temperature` | Controls randomness in outputs |
| `top_p` | Controls the diversity of token selection (nucleus sampling) |
| `max_tokens` | (Optional) Limit response length |
| `stop` | (Optional) Specify stop sequences |

---

## Message Roles in Chat Models

| Role | Description |
| --- | --- |
| `system` | Sets behavior or tone. e.g., *"You are a helpful assistant."* |
| `user` | End-user prompt |
| `assistant` | Model’s response |
| `developer` | Special role to override and guide all messages (OpenAI API only) |

These are **not prompt types**, but how the API **structures the interaction**.

---

## 💡 Prompt Types (Techniques)

| Prompt Type | Example |
| --- | --- |
| **Zero-shot** | “Translate to French: Where is the pharmacy?” |
| **One-shot** | Provide 1 example before task |
| **Few-shot** | Provide multiple examples |
| **Chain-of-Thought (CoT)** | Ask the model to reason step-by-step |
| **Instruction-style** | “Summarize the following in one sentence.” |
| **Role-based** | “You are a financial advisor. Recommend a savings plan.” |
| **Contextual Prompt** | Include background context in the prompt |
| **Reflexion** | Let model review and revise its output |

---

## Prompt Writing Best Practices

### Do:

* Be explicit about your expectations.
    
* Use examples (few-shot) when accuracy matters.
    
* Use system role for behavior shaping.
    
* Break tasks into steps (CoT) for logic problems.
    

### Avoid:

* Vague instructions: *"Explain this?"*
    
* Overloading the prompt with unrelated info.
    
* Relying on temperature alone to fix response quality.
    

---

## Temperature vs Top\_p

| Parameter | Range | Use For | Higher Value Means... |
| --- | --- | --- | --- |
| `temperature` | 0.0 – 2.0 | Controls randomness | More creative / less deterministic |
| `top_p` | 0.0 – 1.0 | Probability sampling threshold | Broader token pool = more diversity |

**Pro Tip**: For stable, accurate outputs, set `temperature=0.2` and `top_p=0.9` as a starting point.

---

## Summary Cheat Sheet

| Concept | Meaning |
| --- | --- |
| `system/user/assistant` | API message structure |
| `Prompt types` | How you format task instructions |
| `Reflexion` | Self-evaluation by the model |
| `Few-shot prompting` | Feed examples to improve accuracy |
| `Instructions param` | Overrides normal prompts in some APIs |
| `Evaluation (Evals)` | Tools to benchmark and test prompts |
| `Pin model snapshots` | Ensure version consistency in production |

---

### What is RAG?

**Retrieval-Augmented Generation (RAG)** is a technique that combines two powerful components:

1. **Retrieval system:** This searches a large external database or document collection to find relevant information based on a user's question.
    
2. **Generative LLM (Large Language Model):** This uses the retrieved information to generate a precise, context-aware response
    

### How RAG uses prompts

* Normally, when you prompt an LLM, you send it a question or instruction, and it tries to answer based only on what it "knows" internally.
    
* In RAG, before generating an answer, the system **retrieves relevant documents** related to your question.
    
* These documents are then **added into the prompt** sent to the LLM.
    

**Example:**

User question:  
*“What is the company policy on remote work?”*

1. The retrieval system searches your company’s internal documents and finds a policy document about remote work.
    
2. The prompt to the LLM becomes something like:
    
    Based on the following document excerpts, answer the question.
    
    *Document excerpts:*
    
    * *"Our company allows remote work up to 3 days a week."*
        
    * *"Remote work requests should be approved by the team lead."*
        
    
    *Question: What is the company policy on remote work?*
    

## What's Next: Model Evaluation

Prompting is just the start. In a production-grade system, you’ll also:

* Use `Promptfoo` or `OpenAI Evals` to measure:
    
    * Consistency
        
    * Accuracy
        
    * Regression (across model versions)
        
* Save prompt snapshots and logs
    
* Write test cases in YAML/JSON for automated evaluation
    

---

## What next:

| Tool | Purpose |
| --- | --- |
| **Promptfoo** | Prompt benchmarking CLI tool |
| **DeepEval** | Evaluation framework for LLM outputs |
| **Jupyter Notebook** | Interactive Python scripting/testing |
| **LangChain/Evals SDK** | Pipeline and testing framework |