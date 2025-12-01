
***

# The Future of AI Engineering: Insights from Chip Huyen and Tri Dao

In a recent episode of *Together Talks*, Tri Dao (Chief Scientist at Together AI) sat down with Chip Huyen—engineer, author, and founder—to discuss the rapidly evolving landscape of AI engineering. From her experience teaching Stanford’s first TensorFlow course to her current work on GPU-native data processing, Chip shared a wealth of knowledge on building production ML systems.

Here are the key takeaways from their conversation, exploring the shift from traditional ML to the new era of Foundation Models, and why "AI Engineering" is becoming a distinct discipline.

## 1. The Evolution of AI Education: From Tools to First Principles

Chip’s journey into AI education started in 2016 when she taught a student-initiated course on TensorFlow at Stanford. However, she quickly learned a painful lesson: **tools change too fast.** By the time she wanted to teach the course again, TensorFlow had upgraded to 2.0, rendering 80% of her material obsolete.

This led to a pivot in her teaching philosophy: **Focus on the "Why," not just the "How."**

Instead of teaching specific frameworks, she shifted to **Machine Learning Systems Design**. While architectures (like Transformers vs. LSTMs) change, the fundamental problems of system design—latency, throughput, data drift, and reliability—remain constant.



[Image of Venn diagram showing intersection of Software Engineering, ML Engineering, and AI Engineering]


## 2. The New Stack: AI Engineering

A major theme of the discussion was the emergence of "AI Engineering" as a field distinct from, yet related to, traditional ML Engineering. Chip noted that while we have new powerful tools (LLMs), the systems required to make them useful rely heavily on classical techniques.

### The "Sandwich" Pattern of AI Applications
Chip described how modern AI applications often wrap a stochastic, generative core (the LLM) with deterministic, classical layers.

1.  **Routing (Classical ML):** Before a user query hits an expensive LLM, a simple classifier determines intent. (e.g., Is this question about coffee? If not, block it.)
2.  **Retrieval (Search/RecSys):** To ground the LLM, systems use Retrieval Augmented Generation (RAG). This relies on decades-old technology like **BM25** (keyword search) alongside modern Vector Search.
3.  **Generation (LLM):** The model generates the response.
4.  **Guardrails (Classical ML):** A final scoring model checks for toxicity, PII leaks, or relevance before showing the answer to the user.



[Image of RAG architecture flow]


## 3. Hallucinations vs. Factual Inconsistency

One of the most nuanced parts of the conversation was Chip’s distinction between **Hallucination** and **Factual Inconsistency**.

* **Hallucination:** The model generating something that doesn't exist. In creative writing or art, this is a *feature*, not a bug.
* **Factual Inconsistency:** When the model contradicts a provided fact.

Chip proposes thinking about consistency in two scopes:
1.  **Local Consistency:** Is the answer consistent with the provided context (e.g., a specific document or story)? This is solvable with RAG.
2.  **Global Consistency:** Is the answer consistent with "the truth" of the internet? This is incredibly hard because the internet itself contains conflicting "facts."

## 4. The Data Processing Bottleneck (And Why GPUs Matter)

Chip is currently the VP of AI & Open Source at Voltron Data, working on **GPU-native data processing**.

Historically, GPUs were reserved for Deep Learning (Training & Inference), while CPUs handled data processing (ETL, SQL queries). Chip argues this is an outdated separation. Data processing tasks like joins, aggregations, and filtering are massively parallelizable—perfect for GPUs.

By moving the ETL pipeline to GPUs, organizations can unify their infrastructure and drastically reduce the bottleneck between "raw data" and "model-ready data."

## 5. Advice for the Next Generation of Builders

When asked what developers should focus on, Chip advised against chasing the latest shiny tool. Instead, she suggested a "Problem-First" approach:

1.  **Pick a Problem, Not a Tech Stack:** It is easier to change jobs or tech stacks than to change industries. Find a domain (BioTech, Finance, Education) you care about.
2.  **Build a Safety Net:** Solve your "big" problems first (e.g., financial security, immigration status) to buy yourself the freedom to take risks later.
3.  **Learn to Tell Stories:** Whether you are fundraising from VCs or hiring engineers, your success depends on your ability to craft a compelling narrative.

***

### Conclusion
As AI transitions from a research curiosity to a core software component, the lines between "Data Systems" and "AI Systems" are blurring. Whether it is using GPUs for SQL queries or using Logistic Regression to route prompts for LLMs, the future of AI engineering is about using the right tool for the job—not just the newest one.

*For more insights, check out Chip’s book "Designing Machine Learning Systems" and stay tuned for her upcoming work on Engineering with Foundation Models.*
