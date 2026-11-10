---
layout: default
title: DSC 180A Methodology Assignment 4
---

## About Me

- **Name:** Jingwen Gu
- **Email:** [jig040@ucsd.edu](mailto:jig040@ucsd.edu)
- **Section:** D25, LLM Applications
- **Mentor:** Jingbo Shang

## Looking Ahead to Quarter 2

**1. What is the most interesting topic covered in your domain this quarter?**

How much of an LLM app's behavior is decided outside the model. In voice agents, no architecture wins outright: a cascade stopped talking 0.17 s after an interruption versus 1.61 s for a native full-duplex model, yet the native model talked through background speech far more often (84% vs 12%). My Q1 project showed the same thing: when the conversation history recorded text the user never heard, the model quoted that unheard sentence in all 10 trials.

**2. Describe a potential investigation you would like to pursue for your Quarter 2 Project.**

Turning my Q1 protocol into a working voice agent that can do real work while it talks: a fast model handles conversation, and slower jobs (search, coding agents, long reasoning) run as interruptible tools. I'd test whether my four primitives are still enough, or whether new rules such as cancelling a tool mid-call are needed, by removing each rule and measuring what breaks. Backup ideas: a client library that makes any OpenAI-compatible endpoint interruptible, or a harness that replays Full-Duplex-Bench audio against any cascade.

**3. What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**

Track what the user heard word by word instead of sentence by sentence, since the current rule made the model claim it had said nothing in 2 of 10 trials. I'd also replace simulated timings with recorded Full-Duplex-Bench speech and test more prompts and models.

**4. What other techniques would you be interested in using in your project?**

- Forced alignment for word-level audio timestamps
- Learned turn detection (e.g. Smart Turn)
- LLM-as-a-judge to label model replies
- Fault injection (network jitter, dropped events) to stress-test the coordinator
