# Large Language Models (LLMs)

## 1. What is an LLM?

- It stands for Large Language Model
- It is a generative AI model that learns the linguistic and semantic relationships between words and phrases.
- It uses these relationships to understand prompts and generate meaningful completions.

It uses them to:
- Understand prompts
- Predict what comes next
- Generate meaningful responses

👉 Think of an LLM as 'super-powered predictive text'.

For example, consider the following sentence:

> _I heard a dog bark loudly at a cat_

Now, suppose you only heard the first few words: _"I heard a dog ..."_. You know that some of these words are more helpful clues as to what the next word might be than others. You know that "heard" and "dog" are strong indicators of what comes next, and that helps you narrow down the probabilities. You know that there's a good chance the sentence will continue as _"I heard a dog **bark**"_.

# How LLM Works??

## 1. Tokenization

The first step is to provide the model with a large vocabulary of words and phrases; and we do mean _large_.
LLMs don't process text exactly as humans see it. They break text into **tokens**.

Wait a minute. _Tokens_?

While we tend to think of language in terms of _words_, LLMs break down their vocabulary into _tokens_. Tokens include words, but also _sub_\-words (like the "un" in "unbelievable" and "unlikely"), punctuation, and other commonly used sequences of characters. The first step in training a large language model therefore is to break down the training text into its distinct tokens, and assign a unique integer identifier to each one, like this:
-   I (1)
-   heard (2)
-   a (3)
-   dog (4)
-   bark (5)
-   loudly (6)
-   at (7)
-   a (3) _already assigned_
-   cat (8)

and so on.

A token can be:
- A complete word
- Part of a word
- Punctuation
- A commonly used sequence of characters

Example:

unbelievable → un + believable

Each token is assigned a **unique numerical ID**.

### Process

Text → Tokens → Token IDs

**As you add more trainig data, more tokens will be added to the vocabulary and assigned identifiers**


## 2.Transforming tokens with a transformer
A transformer helps understand relationships between tokens using **attention**.
(basically helps understand relationships between tokens using attention)

Now that we have a set of tokens with unique IDs, we need to find a way to relate them to one another. To do this, we assign each token a _vector_ (an array of multiple numeric values, like \[1, 23, 45\]). Each vector has multiple numeric _elements_ or _dimensions_, and we can use these to encode linguistic and semantic attributes of the token to help provide a great deal of information about what the token _means_ and how it relates to other tokens, in an efficient format.

- It used attention to understand which tokens are important in a given context.

We use a transformer model. This kind of model consist of two "block".

1. Encoder: 
- It basically creates contextual embeddings.
- It uses attention and multi-head attention to understand relationships between tokens and create useful embeddings.

2. Decoder:
- It uses embeddings, attention and a neural network to predict the next token in a sequence.

c:\Users\bhagi\OneDrive\Documents\Pictures\Screenshots\Screenshot 2026-08-14 195219.png

## 3. Initial vectors and positional encoding
-   **Initial vectors:** Token vectors start with **randomly assigned values** before being processed by the Transformer.
-   **Positional encoding:** Provides information about the **position/order of each token** in a sequence.
-   This is important because the **order of words affects their meaning and relationships**.

For eg:  `Dog bites man` ≠ `Man bites dog`
(**Positions are different which matters a lot.**)
The same words have different meanings because their **positions are different**.
"C:\Users\bhagi\OneDrive\Documents\Pictures\Screenshots\Screenshot 2026-08-14 200203.png"

> **In short:** Initial vectors represent tokens, while positional encoding tells the Transformer **where each token appears in the sequence**.

## 4. Attention and embeddings

### Attention 
It determines which tokens have more influence on another token.
By assigning different weights to surrounding tokens.
Example:

I heard a dog bark



When understanding **"bark"**, the words **"heard"** and **"dog"** are more important than **"I"** or **"a"**.

The model gives different **weights** to tokens based on their context

### Embeddings

The model converts tokens into **vectors called embeddings**. These vectors capture the token's **meaning and contextual relationships**.
(basically converts tokens into number)
Example:

| Token | Embedding |
| --- | --- |
| dog | `[10, 3, 2]` |
| puppy | `[5, 3, 2]` |
| car | `[-2, -2, 1]` |

### Multi-Head Attention

**Multi-head attention** allows the model to focus on different relationships between tokens **simultaneously**, making the understanding of context more effective.

### Cosine Similarity

**Cosine similarity** measures how similar two embedding vectors are:

-   **Closer to 1** → more similar
-   **Closer to 0** → less similar
-   **Closer to -1** → opposite directions

> **In short:** Attention understands relationships between tokens, while embeddings represent their meaning as vectors.


## 5. How an LLM Generates Text

The basic process is:

Prompt

   ↓

Tokenization

   ↓

Token IDs

   ↓

Vectors

   ↓

Embeddings

   ↓

Attention + Transformer

   ↓

Predict next token

   ↓

Add token to sequence

   ↓

Predict next token again

   ↓

Repeat until response is complete

The decoder predicts the **most probable next token** based on the tokens that came before it.

# ⭐ Quick Revision

| Concept | Remember |
| --- | --- |
| **LLM** | Understands language relationships & predicts text |
| **Token** | Piece of text |
| **Tokenization** | Breaking text into tokens |
| **Vector** | Numerical representation |
| **Embedding** | Vector containing semantic/contextual information |
| **Transformer** | Processes relationships between tokens |
| **Attention** | Determines which tokens are important |
| **Multi-head attention** | Examines multiple relationships in parallel |
| **Positional encoding** | Tells the model token position |
| **Decoder** | Predicts the next token |
| **Cosine similarity** | Measures semantic similarity |

### 🧠 One-line Memory

> **LLM = Tokenize → Convert to vectors → Create embeddings → Use attention → Predict the next token.**