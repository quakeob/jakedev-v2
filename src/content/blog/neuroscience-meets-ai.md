---
title: "What Studying Brains Taught Me About Building AI"
description: "I study biological neural networks during the day and build artificial ones at night. The parallels are weirder than you'd think."
date: 2026-01-28
tags: ["neuroscience", "ai", "machine-learning"]
---

# What Studying Brains Taught Me About Building AI

I'm a neuroscience student who builds AI systems. People always ask if those two things are related. The answer is yes, but not in the way you'd expect.

The popular narrative is that neural networks are "inspired by the brain." That's... sort of true, in the same way that airplanes are "inspired by birds." The Wright brothers watched birds fly, sure. But a 747 has more in common with a missile than a sparrow.

Still, studying actual brains has changed how I think about building artificial intelligence. Here's how.

## Attention Is Everything (Literally)

In neuroscience, attention isn't a metaphor. It's a measurable phenomenon — specific neural circuits that amplify certain signals and suppress others. Your brain is constantly filtering out 99% of incoming sensory data. You don't notice the feeling of your shirt on your skin until I mention it. (Sorry.)

Transformers — the architecture behind GPT, Claude, and basically every modern LLM — use "attention mechanisms." The naming isn't a coincidence. The idea is the same: given a huge amount of input, figure out which parts matter for the task at hand.

But here's what's interesting — biological attention is way more sophisticated. Your brain doesn't just attend to tokens in a sequence. It modulates attention based on emotional state, prior experience, metabolic needs, social context. You pay more attention to a lecture when you're interested. The model doesn't care.

That gap is where the interesting problems are.

## Memory Isn't Storage

Ask a CS person how memory works and they'll talk about RAM and disk. Ask a neuroscientist and they'll talk about consolidation, reconsolidation, and the fact that every time you remember something, you're literally rewriting it.

Human memory isn't a database. It's a reconstruction. Every recall is a new synthesis based on your current state, recent experiences, and the cues available. This is why eyewitness testimony is unreliable and why you remember your childhood differently at 20 than you will at 40.

Current AI systems mostly treat memory as storage — context windows, RAG databases, vector embeddings. It works, but it's brittle. The system either has the information or it doesn't. There's no graceful degradation, no creative reconstruction, no "I don't remember exactly but it was something like..."

I think the next breakthrough in AI memory won't come from bigger context windows. It'll come from systems that can reconstruct and synthesize, the way brains do.

## Pattern Recognition vs. Understanding

Here's the thing that haunts me as both a neuroscience student and an AI builder: we don't actually know if brains "understand" things either.

Neuroscience has spent decades trying to figure out how the brain represents concepts. We know which regions activate. We can decode some patterns. But the hard problem of consciousness — how subjective experience arises from neural firing — is completely unsolved.

So when people say "AI doesn't really understand, it just does pattern matching" — well, we might just be doing pattern matching too, just with better hardware and a few billion years of optimization.

I'm not saying LLMs are conscious. I'm saying the line between "real understanding" and "very sophisticated pattern matching" might be blurrier than anyone's comfortable with.

## Why the Intersection Matters

Most AI researchers don't study neuroscience. Most neuroscientists don't build AI systems. I think that's a mistake.

Not because we should copy the brain — we shouldn't, it's too messy and too slow for silicon. But because the brain is proof that general intelligence is possible with finite resources. It runs on about 20 watts. Understanding *how* it achieves what it achieves, even approximately, is the best roadmap we have.

I'm not going to solve AGI in my dorm room. But I do think studying both sides gives me a different perspective than people who only know one. When I'm building a memory system for Yerb, I'm thinking about hippocampal consolidation. When I'm studying cortical attention circuits, I'm thinking about transformer architectures.

The cross-pollination is real, and I think it matters more than most people realize.
