
***

# From ML Engineering to AI Engineering: Navigating the New Stack
**Based on the ACM Tech Talk by Chip Huyen**

The field of Artificial Intelligence is undergoing a fundamental shift. We are moving from an era defined by training specialized models from scratch (ML Engineering) to an era defined by composing applications using massive, pre-trained Foundation Models (AI Engineering).

In a recent talk for the ACM, Chip Huyen (author of *Designing Machine Learning Systems*) broke down what this transition looks like in practice, the new challenges in evaluation, and the architectural patterns defining the next generation of software.

## 1. Defining AI Engineering
Traditionally, building an AI product required a massive data science team to curate datasets and train models. Today, Foundation Models (FMs) like GPT-4 or Gemini act as platforms.

**AI Engineering** is the process of building applications *with* Foundation Models.
This shift has democratized access to AI. You no longer need a PhD in deep learning to build a sentiment analyzer or a code assistant; you need engineering skills to integrate, optimize, and guardrail these models via APIs or open-weight deployments. AI is becoming a standard software component, similar to a database or a JavaScript framework.

## 2. The Evaluation Crisis
In traditional ML, evaluation was "close-ended." You had a classification task, a ground truth label, and a clear metric like Accuracy or F1 Score.

With Generative AI, evaluation is **open-ended**.
* How do you score an essay?
* How do you verify if a code snippet is "good" (not just functional, but readable)?
* How do you detect subtle hallucinations?

Chip highlights that the "Vibe Check" (manually looking at a few outputs) is necessary but insufficient. We need scalable strategies:

* **Comparative Evaluation:** Instead of scoring a single output, present two outputs side-by-side and ask: "Which is better?"
* **AI-as-a-Judge:** Using a stronger model (e.g., GPT-4) to evaluate the outputs of a smaller, faster model. While controversial, this is becoming a standard practice for scaling evaluation without human annotators.



## 3. From Feature Engineering to Context Construction
In classical ML, engineers spent 80% of their time on **Feature Engineering**—extracting statistical signals from data. In AI Engineering, this has been replaced by **Context Construction**.

Models are prone to hallucinations—making things up—often because they lack the relevant information in their immediate view. To fix this, we don't necessarily retrain the model; we change its context.

### Retrieval Augmented Generation (RAG)
RAG is the architecture of bridging a model's knowledge gap. It connects a frozen LLM to your dynamic private data.

1.  **Retrieval:** When a user asks a question, the system searches a database for relevant documents.
2.  **Augmentation:** The system pastes those documents into the prompt.
3.  **Generation:** The model answers the question using *only* the provided information.



[Image of RAG architecture flow]


Chip notes that while **Vector Search** (embeddings) is the current hype, **Keyword Search** (like BM25) remains incredibly robust and hard to beat for many text-heavy applications.

### Handling Structured Data (Text-to-SQL)
RAG isn't just for unstructured text documents. It also applies to structured databases (SQL). However, you cannot simply "embed" a SQL database.

The workflow changes:
1.  **Retrieve Schemas:** Find the relevant table definitions.
2.  **Text-to-SQL:** Ask the LLM to write a SQL query based on the user's natural language question and the schemas.
3.  **Execute:** Run the query and return the data.

This introduces major security risks (e.g., dropping tables), necessitating strict **Guardrails** on what queries can be executed.

## 4. Agents: Giving Models Hands
If RAG gives a model "eyes" (access to data), Agents give a model "hands" (the ability to act).

An agent is defined by its ability to:
1.  **Perceive** an environment.
2.  **Act** upon that environment to change it.



For example, a "Web Browsing Agent" perceives the internet through HTML and acts by sending HTTP requests. This pattern allows models to stay up-to-date by searching Google rather than relying on stale training data.

## 5. The Decision Matrix: Prompting vs. RAG vs. Fine-Tuning
A common question in AI Engineering is: *"Should I use RAG or should I Fine-Tune?"*

Chip proposes a mental model based on the **Failure Mode**:

* **Information Failure:** The model doesn't know the fact (e.g., "What is the stock price today?" or "What is in my private document?").
    * *Solution:* **RAG / Context Construction.** Fine-tuning is bad here because facts change faster than you can retrain.
* **Behavior Failure:** The model has the facts but formats them wrong (e.g., "Speak like a pirate," "Output valid JSON," or "Be more concise").
    * *Solution:* **Fine-Tuning.** This is excellent for teaching style, tone, and format.



## 6. Infrastructure and Optimization
Even though we are using APIs, infrastructure matters. Models are getting massive (hundreds of billions of parameters). To run these efficiently, AI Engineers are turning to inference optimizations:

* **Quantization:** Reducing precision from 16-bit to 8-bit or 4-bit to save memory.
* **Low-Rank Adaptation (LoRA):** Efficiently fine-tuning only a tiny fraction of parameters.
* **Speculative Decoding:** speeding up text generation.

## Conclusion
The transition to AI Engineering requires a shift in mindset. It is less about statistical analysis and hyperparameter tuning, and more about systems engineering—building robust pipelines for retrieval, evaluation, and guardrailing.

As Chip advised regarding career growth: Focus on the fundamentals. Problem-solving, reading code, and understanding *why* a system is built a certain way will outlast the hype of any specific tool.
