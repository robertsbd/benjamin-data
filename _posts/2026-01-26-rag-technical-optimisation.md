---
title: "Four technical tactics to reduce RAG costs"
date: 2026-01-08
---

![RAG Optimisation](/benjamin-data/docs/assets/images/rag_technical_optimisation.png)

In my last post, I discussed how "Clean Data" is the foundation of a high-performance RAG system. But even with perfect data, a standard retrieval process can still be a token-hog.

When building an AI assistant, your goal should be clear: Maximum precision, minimum waste. We didn’t want to just throw data at the LLM; we wanted to engineer a surgical retrieval process.

Moving beyond "out-of-the-box" settings, here are four technical strategies that will improve accuracy and reduce costs.

# Move to Semantic Chunking
Standard RAG systems often use "Fixed-Size Chunking"—splitting a document every 500 characters, regardless of whether it's mid-sentence.

The technical fix to this is Semantic Chunking. This uses an embedding model to identify logical "breakpoints" in the text where the topic actually shifts.

This is interesting very much like an analytic technique I used years ago in my PhD, whereby I conducted a semantic analysis of human discourse, calculating for strings of text throught the discourse a semantic value. Where this value changed beyond a certain threshold this was identified as a change of topic.

The Benefit: Instead of sending three fragmented chunks to the LLM to get the full story, we send one coherent "thought." This reduces irrelevant tokens and stops the AI from getting "distracted" by noise at the edges of a chunk.

# The "Two-Stage" Retrieval (Re-ranking)
Vector search is fast, but it isn't always perfectly accurate. It finds things that are mathematically similar, not necessarily logically relevant.

The technical fix here is to add a re-ranker (Cross-Encoder) layer. The system first retrieves the top 20 possible matches using cheap, fast vector search. It then runs those 20 through a re-ranker, which picks the Top 3 most relevant to the user’s specific query.

The Benefit: We only inject 3 high-confidence chunks into the LLM instead of 10 "maybe" chunks. This creates a massive saving in input tokens without sacrificing depth.

# Metadata Pre-Filtering
Why search the whole database when you know the answer is in the "Backend API" documentation?

Here one should tag data with its source, project phase, and squad. When a user asks a question about "Schema Migration," the system filters the database to only look at "Data Migration" tags before performing the vector search.

The Benefit: It prevents the AI from being "confused" by similar terms in the UI/UX documentation, leading to faster, cheaper, and more accurate retrieval.

# Implementing Prompt Caching
For a project knowledge base, certain information is "static", like our system prompt and the core project definitions that get sent with almost every query.

Utilise Prompt Caching. This allows the LLM provider to cache the "stable" part of the prompt.

The Benefit: Only pay full price for those static tokens once. For every subsequent query, those cached tokens are processed at a massive discount, and latency is significantly reduced.

# The Bottom Line: AI is a Data Analysis and Engineering Discipline
Optimising an AI solution isn't just about the "intelligence" of the model; it’s about understanding and preparing your data, and the efficiency of the data pipeline. By combining the Data Hygiene I discussed in my previous post with these Technical Tactics, built a system that is lean and powerful.

If you are looking to move your AI project from an expensive "proof of concept" to a cost-effective production tool, your underlying data architecture is the place to start. Let’s talk about how to build a data platform that is truly AI-ready.

