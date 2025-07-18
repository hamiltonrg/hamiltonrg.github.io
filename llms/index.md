# Large Language Models (LLMs)

This is my basic understanding—there may be some inaccuracies or simplifications.

## How They Work (Basics)

1. **Tokenizer**

   * Text is split into one or more tokens by a tokenizer. Different models use different tokenization methods, so my example below isn't necessarily true in all cases.

     * *Example:* "sandwich" becomes two tokens: `["sand", "wich"]`.
     * Interactive tool: [https://platform.openai.com/tokenizer](https://platform.openai.com/tokenizer)

2. **Embedding**

   * A pretrained embedding model converts tokens into vectors. The model captures the meaning/semantics of the word as part of the training.  The model may or may not be built into the LLM, although most are.  The embedding models vary in how they work—some may develop vectors based on just the words themselves, while others may look at the surrounding words too for better context.

     * Example resource: [https://vectors.nlpl.eu/explore/embeddings/en/#](https://vectors.nlpl.eu/explore/embeddings/en/#)

3. **Inference**

   * Once tokens are vectorized, they’re sent into the language model.

     * This process depends on the model’s architecture. Calculations are performed on combinations of vectors, and the results continue to feed through layers. The final layer produces a probability of possible next tokens.
     * The inference engine uses parameters to select a subset of likely tokens and then selects some tokens from that set. This randomness is why outputs can differ between runs.

       * This isn't always true. There are other implementations, but this is a common one.

4. **Loop**

   * When text is sent through the above process and the next token is generated, all of that resulting text is fed back through the process until an end of text token is generated or a preconfigured maximum amount of tokens is generated.

---

## Example

### First Loop

#### Input

```plaintext
The carpool
```

#### Tokenization

```plaintext
["The", "car", "pool"]
```

#### Embeddings

*(Not real values — just to show the idea.)*

Each token gets turned into a vector basically a list of numbers.
Something like:

```plaintext
The → [0.12, -0.44, 0.88]
car → [0.56, 0.03, -0.77]
pool → [0.09, -0.15, 0.22]
```

#### Inference

The model looks at those vectors and guesses the most likely next token.
Let’s say it thinks `"is"` is the most probable next word.

---

### Second Loop

#### Input

```plaintext
The carpool is
```

#### Tokenization

```plaintext
["The", "car", "pool", "is"]
```

#### Embeddings

Each token gets turned into a new vector (they may look different this time because context matters).

```plaintext
The → [0.11, -0.42, 0.85, ...]
car → [0.55, 0.04, -0.75, ...]
pool → [0.30, -0.10, 0.40, ...]
is → [0.22, 0.18, -0.33, ...]
```

#### Inference

The model now looks at *this* new sequence and might predict `"full"` as the next most likely token.

---

### Third Loop

#### Input

```plaintext
The carpool is full
```

#### Tokenization

```plaintext
["The", "car", "pool", "is", "full"]
```

#### Embeddings

Vectors for each token are generated again, with updated context.

#### Inference

The model evaluates and this time predicts the end-of-text token (or maybe a period, depending on settings). Let's say it outputs the end-of-text signal.

---

#### Generation Ends

The loop stops. The model has finished its response.
