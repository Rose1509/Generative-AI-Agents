# Prompt Engineering & Model Output Optimization

**Prompt engineering** is the process of designing and refining prompts to improve a language model's **accuracy, relevance, consistency, and output quality**. It is usually the simplest first step for optimizing an AI application because it requires **no additional model training or infrastructure**.

---

## 1. Prompt Components

A chat-based prompt can contain several components:

| Component             | Purpose                                                    |
| --------------------- | ---------------------------------------------------------- |
| **System message**    | Defines the model's role, behavior, rules, and constraints |
| **User message**      | Contains the user's question or task                       |
| **Assistant message** | Provides previous conversation/model responses for context |
| **Examples**          | Demonstrate the expected input/output pattern              |

How you structure and combine these components determines how effectively the model responds.

### Example System Message

```text
You are a travel advisor for Margie's Travel.
Answer only travel-related questions.
Use a friendly and professional tone.
If information is missing, ask for clarification.
Format hotel recommendations as bullet points.
```

## 2. Design effective system messages

A **system message** is a set of instructions you provide to the model to guide its responses. System messages typically appear first in the conversation and act as the highest-level set of instructions. You use them to:

1. **Define the role** - Tell the model what it is and what it should accomplish.
2. **Set boundaries** - Specify what it should and shouldn't do.
3. **Define the output format** - Specify JSON, tables, bullets, etc., when required.
4. **Handle uncertainty** - Tell the model what to do when information is missing or unclear.

---

## 3. Apply Prompt Patterns

Effective prompts use patterns that help the model produce better responses. Here are some common patterns you can use:

### i. Persona Pattern

Instruct the model to take on a specific perspective or role. 
```text
Act as a senior Python developer.
Review the following code and identify bugs and improvements.
```

**Purpose:** Produces responses from a specific perspective.

---

### ii. Format Template Pattern

Define exactly how the response should be structured.

```text
Provide the hotel information using:
- Hotel name
- Location
- Star rating
- Price range
```

**Purpose:** Produces consistent and structured outputs that are easier to process.

---

### iii. Chain-of-Thought / Task Decomposition

Break complex tasks into smaller steps.

```text
Evaluate the hotel based on:
1. Location
2. Room size
3. Family amenities
4. Price
5. Overall suitability
```

**Important:** Chain-of-thought prompting is mainly relevant to non-reasoning models. Modern reasoning models generally perform reasoning internally.

**Better approach for applications:** Ask for the **key factors, conclusions, or structured results** rather than requiring the model to expose private internal reasoning.

---

### iv. Few-Shot Prompting

Provide one or more examples of the desired input and output to help the model identify the pattern you want. This technique is called **few-shot learning** (or **one-shot** for a single example).

```text
Message: "I need to change my flight."
Category: Booking Change

Message: "What's the weather in Bali?"
Category: Travel Information

Message: "Can I get a refund?"
Category:
```

The model uses the examples to infer the expected pattern.

* **Zero-shot:** No examples
* **One-shot:** One example
* **Few-shot:** Multiple examples

---

### 4. Use Delimiters & Clear Syntax

Use clear boundaries when a prompt contains multiple sections.

```text
# Instructions
Classify the following text.

# Examples
...

# Input
---
Customer: I want to cancel my booking.
---
```

Useful delimiters include:

* `---`
* Markdown headings
* XML tags
* Code blocks

**Why?** Clear separation helps the model distinguish instructions, examples, and input data.

**Tip:** Models can exhibit **recency bias**, where information near the end of a prompt can have greater influence. If an important instruction is frequently missed, reinforcing it near the end can sometimes help.

---

# 5. Model Parameters

Prompt text isn't the only way to control model output. Generation parameters can also affect behavior.

### a) Temperature

Controls randomness/creativity.

| Temperature           | Typical Use                    |
| --------------------- | ------------------------------ |
| **Low (e.g., 0.2)**   | Factual, deterministic tasks   |
| **Medium**            | General-purpose responses      |
| **High (e.g., 0.7+)** | Creative and varied generation |

**Example:**

* Factual hotel information → `0.2`
* Creative itinerary ideas → `0.7`

### b) Top-p

Controls randomness by limiting token selection to a probability mass.

For example:

```text
top_p = 0.9
```

means the model considers tokens within the most probable 90% probability mass.

**Best practice:** Generally adjust **temperature OR top-p**, rather than changing both simultaneously.

---

# 6. When Prompt Engineering Is Enough

Prompt engineering is usually the **first optimization technique** to try when you need to:

* Control model behavior and tone
* Improve response structure
* Specify task requirements
* Provide context
* Demonstrate expected outputs
* Quickly test different approaches
* Avoid additional training costs

---

# 7. Limitations

Prompt engineering cannot solve problems caused by missing capabilities or information.

For example, if the model doesn't have access to:

* Your company's private data
* A product/hotel database
* Required external information
* Sufficient training knowledge

then improving the prompt alone may not be enough.

Other approaches may be required, such as:

**Prompt Engineering → RAG / External Data → Fine-tuning → Additional Application Logic**

---

## Key Takeaways

> **Prompt engineering is the first and simplest method for optimizing an AI application's output.**

* Define a clear **role and objective**.
* Set **boundaries and constraints**.
* Specify the desired **output format**.
* Use **examples** when consistency matters.
* Break complex tasks into **smaller steps**.
* Use **delimiters** to separate prompt sections.
* Adjust **temperature or top-p** when appropriate.
* Test and iterate — a system prompt does **not guarantee** perfect compliance.
* If prompting cannot provide the required knowledge or behavior, consider **RAG, tools, fine-tuning, or application-level logic**.
