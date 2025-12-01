Structured to highlight the key technical and operational hurdles discussed by Chip Huyen.

***

# Navigating the LLM Avalanche: 10 Open Challenges in Large Language Models

**By Chip Huyen** (Adapted from the *LLM Avalanche* Talk)

The pace of innovation in Generative AI is breathless. If I were to write a guide on "How to Build an LLM Application" today, it would likely be obsolete by next week. The specific tools change, but the fundamental engineering hurdles remain.

Instead of focusing on the fleeting "how-to," we need to focus on the "what now?" As we move from toy demos to production systems, we are hitting a wall of open challenges. Based on my recent research and observations, here are the top challenges preventing companies from fully adopting and trusting Large Language Models (LLMs) today.

---

## 1. The Consistency Problem
Users expect software to be deterministic: if I click a button twice, I expect the same result twice. LLMs, by their stochastic nature, defy this expectation.

You can have the exact same input yield different outputs. While developers try to enforce determinism by setting parameters like `temperature = 0`, it isn’t a silver bullet. Furthermore, LLMs are incredibly sensitive to input perturbations. A minor change in your prompt can lead to a massive swing in the output quality or sentiment.



This makes building downstream applications difficult. If you are using an LLM to generate a score (e.g., 1–5) and want to parse that into a database, the lack of a guaranteed output schema (though improving) remains a major friction point.

## 2. Hallucinations and Factuality
This is arguably the biggest barrier to enterprise adoption. We’ve all heard the horror stories—like the teacher who used ChatGPT to grade essays, only to find the model hallucinated the feedback entirely.

For tasks requiring strict factuality, such as legal contract processing or text-to-SQL generation, current performance is concerning. On benchmarks like the Bird SQL leaderboard, even the best models often struggle to break 50% accuracy.

Why do they hallucinate? There are two prevailing hypotheses:
1.  **Causal Misunderstanding:** The model doesn't truly understand the cause-and-effect of its generated text.
2.  **Knowledge Mismatch:** There is a discrepancy between the model’s internal knowledge (internet data) and the labeler’s internal knowledge during the fine-tuning process. If a labeler forces a model to answer a question it doesn't actually "know," we are essentially training it to hallucinate.

## 3. The Privacy Dilemma: Build vs. Buy
When implementing LLMs, you face a difficult choice regarding data privacy.

* **Buying (APIs):** If you use OpenAI or Anthropic, you rely on their compliance. While they may have 30-day retention policies, highly regulated industries (healthcare, finance) often cannot risk sending PII (Personally Identifiable Information) to a third party at all.
* **Building (In-House):** If you host your own open-source model (like Llama 2 or Mistral), the data never leaves your perimeter. However, the onus of security falls entirely on you. You must ensure your internal chatbot doesn't accidentally reveal sensitive salary data or trade secrets to the wrong employee.

## 4. Context Length and "Lost in the Middle"
There is a debate about whether prompt engineering is dead. It is not. As long as human communication requires context, prompt engineering will exist.

While we now have models with context windows of 100k+ tokens, a larger window does not equal better attention. Research suggests that models often struggle to utilize information found in the middle of a long context window. For use cases like document processing or gene sequencing (where context can be hundreds of thousands of tokens), efficiency remains an open question.

## 5. Data Drift and Knowledge Cutoffs
ChatGPT made the world realize the importance of data drift. When a user asks a question about a recent event, the model fails because of its knowledge cutoff.



Studies show that models trained on past data degrade significantly (up to 15% performance drop) when asked to answer questions about the present, even when the evidence is provided in the context. The world changes, and static models struggle to keep up.

## 6. Backward Compatibility
The Transformer architecture has been incredibly "sticky," but new architectures and better base models are released weekly. This creates a regression testing nightmare.

If you have built a complex system of prompts optimized for GPT-3.5, and you swap the backend to GPT-4 or a new open-source model, will your prompts still work? Often, they break. We lack robust frameworks for ensuring prompt compatibility across different model versions.

## 7. LLMs on the Edge
The dream is the "Personal ChatGPT"—a model that runs entirely on your laptop or phone, trained on your private data, without ever touching the internet. This is vital for use cases like autonomous vehicles or healthcare in remote areas with poor connectivity.



However, the challenges are steep:
* **Inference:** Can the device hardware handle the compute load?
* **Updates:** How do we update the model? If we use techniques like Federated Learning to train on-device, how do we merge those insights without compromising privacy?

## 8. The "Tokenization Tax" on Non-English Languages
LLM performance is not equal across languages. For low-resource languages (like Vietnamese, Burmese, or Amharic), performance drops specifically because of tokenization.

English text is tokenized very efficiently. However, for other languages, the same sentence might require 2x or 3x the number of tokens. Since APIs charge by the token and latency is determined by token count, non-English speakers are essentially paying a "tax"—higher costs and slower speeds for worse performance.



## 9. Interface Efficiency: Chat vs. Search
Is Chat the universal interface? It is certainly robust—you can type anything and get *some* response. However, it isn't always efficient.

With a search bar, you use a specific DSL (keywords) to get a result. With Chat, you often have to negotiate with the bot, provide context, and iterate to get what you want. While Chat is accessible, it may not be the optimal UI for every workflow.

## 10. The Data Wall
Finally, we are facing a data bottleneck. We are running out of high-quality public internet data. Projections suggest we might exhaust public text data by 2026.

Worse, the internet is being flooded with AI-generated content. If future models are trained on the output of current models, we risk a feedback loop that could degrade model quality. This makes proprietary, high-quality human data the most valuable asset a company can possess.

---

### Conclusion: It Always Comes Back to Data
Despite the hype around generative AI, the solution to many of these challenges is not just "bigger models," but better data strategy.

Companies successfully deploying AI today are those prioritizing data governance, cleaning their data silos, and establishing ground-truth datasets. The hype cycle may shift, but the value of data remains the constant.

*See you at the next LLM Avalanche!*
