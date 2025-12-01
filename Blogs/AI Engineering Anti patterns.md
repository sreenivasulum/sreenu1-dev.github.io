
***

# The 5 Biggest Anti-Patterns in AI Engineering (And How to Fix Them)

**Based on insights from Chip Huyen**

The landscape of software development is shifting beneath our feet. As we move from traditional Machine Learning (ML) to the era of Generative AI, the role of the engineer is evolving.

In a recent talk, Chip Huyen (author of *Designing Machine Learning Systems*) broke down the emerging discipline of "AI Engineering" and, more importantly, the common traps—or "anti-patterns"—that teams fall into when trying to push Large Language Models (LLMs) into production.

Here is a detailed breakdown of the differences between ML and AI engineering, followed by the five critical mistakes you need to avoid.

---

## Part 1: AI Engineering vs. ML Engineering

A common question arises: *Is "AI Engineering" just a buzzword to sell books?*

The answer is no. The workflow has fundamentally flipped.

**Traditional ML Engineering** typically involves building predictive models from scratch (e.g., fraud detection, recommendation systems). The process is linear and data-heavy from the start:
1.  Collect massive datasets.
2.  Train a model.
3.  Deploy.

**AI Engineering**, conversely, starts with Foundation Models. The models are increasingly commoditized (everyone uses GPT-4, Claude, Llama 3). The competitive advantage has shifted from *model architecture* to *data curation and product UX*. The workflow often looks like this:
1.  Prototype an idea instantly with a Foundation Model.
2.  Validate success.
3.  Work backward to gather data and fine-tune to reduce costs/latency.



### The Rise of the "AI Stack"
We are also seeing a convergence of roles. AI is becoming part of the full-stack toolkit, just like databases or JavaScript.

However, a production AI application is rarely just a raw prompt sent to a model. It is a system—a "sandwich" of components designed to ensure reliability.

**The Production Flow:**
* **The Router/Classifier:** Before the LLM answers, a smaller model determines intent. (e.g., Is this a billing question? Send to a human. Is this a joke request? Reject it.)
* **The Generator:** The LLM generates the response.
* **The Guardrail/Scorer:** Before the user sees the answer, another system checks for PII (Personally Identifiable Information) or brand-damaging hallucinations.



---

## Part 2: The 5 Engineering Anti-Patterns

Despite the excitement, many teams are failing to get value from GenAI. Chip highlighted five specific anti-patterns responsible for these failures.

### 1. Using GenAI When You Don't Need It
The hype cycle drives teams to use GenAI for the sake of the headline, not the utility.

Chip shared an example of a startup building an energy optimization app. The pitch: *Use GenAI to analyze a user's habits and tell them when to use electricity to save 30% on their bill.*

**The problem?** You don't need an LLM for this.
If electricity is cheaper after 9 PM, a simple greedy algorithm or convex optimization logic can schedule tasks for that time. It is faster, cheaper, and deterministic.

** The Lesson:** Be problem-oriented, not solution-oriented. Do not use a chainsaw to cut butter just because chainsaws are trending.

### 2. Confusing "Bad Product" with "Bad AI"
Engineers often obsess over the model's output quality without asking if the user actually wants that output.

**Example 1: The Meeting Summarizer**
A team agonized over whether users wanted 3-sentence summaries or 5-sentence summaries. It turned out users didn't read the summaries at all—they only cared about *Action Items*. The AI was good at summarizing, but the product hypothesis was wrong.

**Example 2: The LinkedIn Job Bot**
LinkedIn built a bot to assess if a user was a good fit for a job. The bot was accurate—it would tell users, "No, you are a terrible fit."
While accurate, this was a bad user experience. Users didn't want a hard "No"; they wanted a gap analysis (e.g., "You lack skill X, here is how to get it").

**The Lesson:** High model accuracy does not guarantee a successful product if you fundamentally misunderstand the user intent.

### 3. Complexity Overload (The RAG Trap)
There is a tendency to adopt complex tools too early. Many teams immediately jump to complex Vector Databases and Agentic Frameworks before they are ready.

**The RAG (Retrieval-Augmented Generation) Reality:**
While Vector DBs are powerful, many problems can be solved initially with simple keyword search (BM25). The real bottleneck in RAG is usually not the database, but **Data Preparation**.

If you chunk a document blindly, you lose context.
* *Scenario:* A document mentions "Project X" in the intro but refers to it as "The Initiative" in paragraph 4.
* *Result:* If you chunk paragraph 4 separately, the retrieval system won't know it relates to "Project X."



**The Lesson:** Focus on data hygiene, contextual chunking, and simple retrieval baselines before adopting complex agent frameworks that hide logic and make debugging difficult.

### 4. Foregoing Human Evaluation
Everyone wants to automate evaluation using "AI Judges" (using GPT-4 to grade a smaller model). While useful, this is dangerous if relied upon exclusively.

**The Problem with AI Judges:**
1.  **They are not stationary:** OpenAI updates their models. If your evaluation score jumps from 80% to 82%, did your app get better, or did the judge change?
2.  **Definition Mismatch:** A "Faithfulness" score from one tool might mean something totally different in another.



**The Lesson:** You must supplement AI judges with human review. Have experts review a random sample of logs weekly to correlate the AI Judge's performance with reality.

### 5. Over-Indexing on Early Success
This is the "Weekend Demo" trap.

With modern Foundation Models, you can build a demo that works 80% of the time in a single weekend. This leads teams to believe they are a week away from launch.

**The Reality:** The first 80% takes 2 days. The last 20%—handling edge cases, latency, PII scrubbing, and formatting errors—takes months.



**The Lesson:** Do not base your roadmap on the initial prototype's speed. The gap between a demo and a production system is vastly larger in AI engineering than in traditional software.
