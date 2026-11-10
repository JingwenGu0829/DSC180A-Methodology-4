---
layout: default
---

## About Me

- **Name:** Jingwen Gu
- **Email:** [jig040@ucsd.edu](mailto:jig040@ucsd.edu)
- **Section:** D25, LLM Applications
- **Mentor:** Jingbo Shang

## Looking Ahead to Quarter 2

**1. What is the most interesting topic covered in your domain this quarter?**

How much of an LLM application's behavior is decided outside the model itself. In voice agents, published measurements show that no architecture wins outright: on one GPU, a cascade of separate speech recognition, language, and speech synthesis models stopped speaking 0.17 s after an interruption while a native full-duplex model took 1.61 s, yet the native model kept talking through background speech in 84% of samples versus 12% for the cascade. My Q1 project showed the same theme from another angle. A hosted chat model can only answer from the conversation history the application hands it, so when that history recorded text the user never actually heard, the model quoted an unheard sentence in all 10 trials. Small bookkeeping rules in the application layer, not just model quality, decide whether an agent behaves like a real conversation partner.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

I would like to turn my Q1 protocol into a working voice agent that can do real work while it talks. Following the Talker-Reasoner idea, a fast conversational model would handle speech, while slower jobs (web search, coding-agent calls, long reasoning) run as tools behind the same session coordinator. The question is whether the four Q1 primitives (session, cancel, run identity, playback progress) are still enough once a long-running tool can be interrupted, or whether new rules are needed: for example, cancelling a tool call mid-flight, reporting its progress aloud, or deciding what the history should say about a tool result the user never heard. I would test each candidate rule the same way as in Q1, by removing it and measuring what breaks. The deliverable would be a working app plus that ablation study, which fits our domain's goal of a working application by the end of Q2.

Related backup projects, in case this goes faster or slower than expected: (a) a small client library that makes any OpenAI-compatible endpoint interruptible, or (b) a benchmark harness that replays Full-Duplex-Bench audio against any cascade built from HTTP endpoints.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

I would move from sentence-level to word-level conversation history. Right now the history keeps only sentences that fully played, and in 2 of 10 hosted-model trials this made the model claim it had said nothing even though the user had heard part of a sentence. Word-level timestamps from the speech synthesizer (or forced alignment) would let the history record exactly what was heard. I would also replace the assumed timings in my simulation with recorded speech from Full-Duplex-Bench, and widen the hosted-model test beyond one prompt and one model, so the results show a failure rate rather than just a direction.

**4. What other techniques would you be interested in using in your project?**

- **Forced alignment / word-level timestamps** to line up synthesized audio with text.
- **Learned turn detection and voice activity detection** (e.g. Smart Turn) as plug-in inputs, to see how detection errors interact with the protocol.
- **LLM-as-a-judge**, validated against hand labels, to classify model replies instead of exact string matching.
- **Fault injection and property-based testing**: adding network jitter and dropped or reordered events, and checking that the coordinator's state machine still keeps a consistent history.
- **Confidence intervals** (exact binomial or bootstrap), since trial counts are small.
- **Distributed tracing** (OpenTelemetry-style spans) to record event timelines from real deployments.
