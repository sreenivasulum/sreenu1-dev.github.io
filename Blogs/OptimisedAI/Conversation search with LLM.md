
***

# Beyond Keywords: Architecting High-Performance Conversational Search with LLMs

**Based on insights from Andrei Patena, Director at Neon 7i (ex-Google, Apple, Walmart Labs)**

For the past two decades, search was reactive. A user typed a keyword, and the engine returned a list of links. Speed was the only metric that mattered; if you couldn't return results in 200 milliseconds, you failed.

But the paradigm has shifted. According to search veteran Andrei Patena, we are moving from **Search** to **Task Completion**. Users are no longer just looking for a "loan officer"; they are asking, *"I want to finance my house, what steps should I take?"*

To support this, we must transition from simple information retrieval to **Conversational Search**—systems with long-term memory, multi-turn understanding, and proactive clarification. Here is the technical blueprint for building this next generation of search.

---

## 1. The Proactive Engine: Search Clarification
The biggest missed opportunity in modern search is **Clarification**. In e-commerce and vertical domains (like real estate), approximately 30% of search sessions require some form of clarification.

Simply plugging in an LLM to ask "What do you mean?" is insufficient. A robust system must handle specific clarification scenarios:
* **Broad to Narrow:** If a user searches for "shoes," the system shouldn't just dump results. It should proactively ask about gender, season, or occasion.
* **Multi-Intent:** Identifying when a query could mean two different things and disambiguating immediately.
* **Query Detailization:** Encouraging users to add attributes (e.g., specific neighborhoods in real estate).

**The Impact:** Implementing intelligent clarification can drive a **20% improvement in conversion rates**. Users who are guided to what they actually need are significantly less likely to bounce to a competitor.



---

## 2. Hybrid Query Understanding (The Cost/Latency Balance)
While LLMs are powerful, using them for every single query in a system processing millions of queries per second is financially and architecturally suicidal due to inference costs and latency.

The solution is a **Multi-Tiered Architecture**:
1.  **Tier 1 (Simple NLP):** Use lightweight, traditional NLP models for basic, navigational queries. These are fast and cheap.
2.  **Tier 2 (LLM Routing):** Route only complex, ambiguous, or multi-step queries to the LLM.
3.  **Optimization (Semantic Caching):** If the system has seen a similar semantic intent before, serve the cached reasoning rather than querying the LLM again.

This approach balances the depth of understanding required for queries like *"House with 5 bedrooms close to a highway within 30 mins of Seattle"* with the speed required for queries like *"iPhone 15."*



---

## 3. Fine-Tuning Embeddings: Context Matters
Off-the-shelf embedding models (from public leaderboards) are excellent starting points, but they lack domain-specific nuance.

**The "Recency" Problem:**
* If a user searches for **"Mobile Phones,"** recency is a critical relevance factor. They likely want the latest model, not one from 2018.
* If a user searches for **"Pillows,"** recency is irrelevant. A top-rated pillow from 2020 is still a good result.

Generic embeddings often fail to capture these domain-specific weights. To build a competitive search experience, you must **fine-tune embedding and ranking models** on your specific click-stream data and customer behavior. This allows the vector space to reflect what *your* users value, whether that is "school district" in real estate or "compatibility" in auto parts.



---

## 4. Summarization and Hallucination Mitigation
In Conversational Search, you don't just return a list; you summarize the answer. This introduces the risk of **Hallucination**.
* In generic chat, a small error is annoying.
* In e-commerce or finance, an LLM changing a price or inventing a compliance fact is catastrophic.

To mitigate this, architectures are adopting verification methods similar to Google DeepMind's "Safe" approach.
1.  **Decomposition:** Break the generated answer into "atomic chunks" (individual facts).
2.  **Verification:** Verify every single atomic fact against the retrieved index or database.
3.  **Citation:** Only present facts that are strictly grounded in the retrieved data.



---

### The Future: Deep Research
The next frontier is **Deep Research**. Users are willing to tolerate higher latency (waiting seconds instead of milliseconds) if the system can perform a complex task—like researching a neighborhood's crime rate, pollution levels, and school ratings—and aggregating that external data into a cohesive answer.

The future of search is not about finding the link; it is about doing the work.
Video: https://www.youtube.com/watch?v=gNSRTmXPAuk
