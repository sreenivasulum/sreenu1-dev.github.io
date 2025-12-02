
***

# Beyond Naive RAG: Optimizing Deep Research Agents with Evolutionary Algorithms

**By Jakob, Presented at Optimize AI**

We have entered a new phase of Artificial Intelligence. We are moving past the initial excitement of general-purpose chatbots and into the era of **Knowledge-Intensive AI Systems**. In industries like pharmaceuticals, high-tech manufacturing, and legal services, a simple summary is not enough. Experts need depth, precision, and comprehensive analysis.

This post explores the architecture of "Deep Research" agents, the challenge of evaluating them without unlimited human experts, and how we are using evolutionary algorithms like JEPA and TextGrad to optimize them.

---

## 1. The Problem with "Naive RAG" in Expert Domains
In specialized fields, "Naive RAG" (Retrieval-Augmented Generation)—where you simply chunk documents, vectorize them, and retrieve the top-k matches—is insufficient.

If a polymer scientist asks, *"What innovative methods improve the structural properties of PHA and PLA bio-plastics?"*, a generic RAG system might provide a technically accurate but superficial paragraph. To an expert, this is useless. They need a multi-page report that synthesizes data from patents, internal lab reports, and academic papers to reveal something they *didn't* already know.

To achieve this, we must move from simple retrieval to **Agentic Deep Research**.



---

## 2. Anatomy of a Deep Research Agent
A Deep Research Agent is not a single model; it is an **LLM-based program**. It is a pipeline of specialized agents working in concert to produce a high-quality artifact.

The architecture we successfully deployed involves a recursive loop of four specific agent roles:

1.  **The Planner:** Decomposes the user's query into sub-questions and generates specific search queries (e.g., lexical search for specific chemical names, vector search for concepts).
2.  **The Extractor:** Reads the retrieved documents, evaluates relevance, and extracts specific facts (e.g., pricing, availability, chemical properties).
3.  **The Merger:** Synthesizes the extracted facts into intermediate summaries, identifying gaps that require the Planner to loop back and search again.
4.  **The Writer:** Once sufficient information is gathered, this agent compiles the final long-form report following a specific structural template.



---

## 3. The Evaluation Bottleneck: LLM as a Judge
In expert domains, evaluation is the hardest problem. You cannot ask a PhD scientist to sit down and annotate 1,000 examples to train a reward model. You might get one hour of their time to review 10 examples.

To solve this, we utilize **LLM as a Judge** in a tournament style, implemented in an open-source package called **Ragilo**.

Instead of trying to force an LLM to give an absolute score (e.g., "7/10 accuracy"), we use an **ELO rating system** similar to chess rankings. We treat different versions of our agent as "players" in a tournament. They compete in head-to-head comparisons on specific queries, and over time, a stable ranking emerges. This allows us to stack-rank improvements without needing a perfect gold-standard metric.



---

## 4. Optimizing Agents: TextGrad vs. JEPA
How do we improve these agents? We cannot update the weights of proprietary models like GPT-4. We can only optimize the **prompts** and the **architecture**.

Two cutting-edge approaches have emerged to automate this optimization:

### TextGrad (The "Backpropagation" Metaphor)
TextGrad treats the pipeline like a neural network, but instead of numerical gradients, it uses **textual feedback**.
1.  The system generates an answer.
2.  An evaluator provides text feedback on errors.
3.  This feedback is "back-propagated" to the prompt of the specific sub-agent (e.g., the Extractor) that caused the error.
4.  The prompt is rewritten to address the feedback.

### JEPA (Genetic Pareto Optimizer)
While TextGrad uses a depth-first approach (improving one prompt iteratively), **JEPA** uses an evolutionary approach (Breadth-First Search).
Based on the paper *Genetic Pareto Agent*, JEPA maintains a population of agent prompts. It tests a batch, identifies the best performers (the Pareto frontier), and "breeds" new prompts by combining successful traits.



---

## 5. Results: Evolutionary Algorithms Win
In our experiments on the **Scholar QA** benchmark, comparing human-optimized prompts against automated optimizers, the results were clear.

* **Baseline (Vanilla Prompt):** ~51% performance.
* **Human Optimized:** ~66% performance.
* **JEPA Optimized:** Significantly outperformed both the baseline and the best human-tuned prompts, and also outperformed TextGrad in efficiency.



### Conclusion
The future of enterprise AI is not just about having a better model; it is about the **co-evolution of agents and judges**. By combining robust architectural patterns (Planner/Extractor/Writer) with evolutionary optimization algorithms like JEPA, we can build systems that don't just answer questions—they perform genuine research.

***

### **Glossary of Terms**
* **Deep Research:** An AI workflow designed to produce comprehensive, long-form reports rather than short summaries.
* **MCP (Model Context Protocol):** A standard for connecting AI assistants to systems where data lives.
* **ELO Rating:** A method for calculating the relative skill levels of players (or models) in zero-sum games.
* **JEPA:** A genetic algorithm that optimizes prompts by treating them as an evolving population.
  * video link- https://www.youtube.com/watch?v=gcNiYO3JNNQ
