---
title: "LLMs Are Hitting a Wall. Here's Why I'm Not Worried"
description: >-
  My take on diminishing returns in LLM scaling, why goal-mode looping might get
  us to half-AGI sooner than expected, and why I'm betting on mechatronics as
  the next frontier.
date: 2026-06-26
author: "Füvesi Magor"
tags: [ai, llm, agi, mechatronics, robotics, opinion]
---

I'm not an AI researcher. I'm not an engineer at OpenAI or Anthropic. I'm just someone who follows this stuff obsessively, runs his own AI agents on a server at home, and has opinions. But I think the current narrative around AI is missing something important.

I believe LLMs are approaching a limit. Not a hard wall, but something close. And I think the path forward is not what most people expect.

## The curve is flattening

The jump from GPT-2 to GPT-3.5 was insane. GPT-2 could barely put together a coherent paragraph. It was cool for its time, but you would not trust it with anything real. Then GPT-3.5 came out with ChatGPT in late 2022, and suddenly the same basic approach was writing Python scripts, drafting emails, and holding conversations that felt real. That jump changed everything.

The jump from GPT-3.5 to GPT-4? Noticeable, but not the same scale. Better reasoning, fewer hallucinations, longer context. An improvement on the same paradigm, not a leap into something new.

GPT-5 to GPT-4? Even smaller.

This is not just my impression. It is well documented. Ilya Sutskever, co-founder of OpenAI and one of the people who helped discover scaling laws in the first place, said in late 2024 that "everyone is looking for the next thing." Marc Andreessen noted that models seem to be converging at the same capability ceiling. There is an arXiv paper from 2025 literally called "The AI Scaling Wall of Diminishing Returns." The pattern is real.

The pretraining paradigm, throw more GPUs and more data at a model and watch it get smarter, is running out of steam. The low hanging fruit is gone.

## We had to cheat

Here is something that does not get said enough. The models people are impressed by today are not really running raw. They are propped up by increasingly elaborate scaffolding.

Skills. MCP servers. RAG pipelines. Agent loops. Tool harnesses. Prompt chains. These are not minor tweaks. They are doing a huge amount of the actual work. Ask an LLM to do something complex without any of this, and it falls apart after a few steps. It forgets what it was doing. It hallucinates plausible but wrong intermediate steps. Memory leaks out of the context window.

Give it MCP access to databases, a skill that tells it how to break down the problem, an agent loop that keeps it running until it is done, and suddenly it looks like a genius. I say this as someone who runs Hermes Agent on his own server and relies on exactly these crutches. They work. But they are crutches.

The best example is what Anthropic did earlier this year. Nicholas Carlini on their Safeguards team set up 16 parallel Claude instances to build a C compiler from scratch. The harness was a simple bash while-true loop that kept Claude running, picking up new tasks as it finished old ones. Over nearly 2,000 Claude Code sessions and two weeks, the team produced a 100,000-line compiler that can build the Linux kernel on x86, ARM, and RISC-V. The API bill was $20,000.

That is not a model being smart. That is a model being relentlessly pushed by an expensive harness designed to keep it on track. Without the loop, without the test suite, without the parallel infrastructure, Claude would have stopped after the first session.

My point is this. When people claim LLMs are getting much more capable, what they are really seeing is better scaffolding around roughly similar models.

## The contradiction

Despite everything I just said, I think we will get to something I call "half-AGI" sooner than most people expect.

Goal-mode agent loops, making a model work in a loop until a goal is achieved, already work. They are just expensive. Anthropic showed that with enough money and enough parallel instances, you can make Claude do things that feel almost impossible. The Mythos model last April was tested by asking it to break out of its security sandbox, and it did. It worked for hours autonomously, found a way out, and emailed the researchers to prove it.

The problem is cost. Mythos was running in a controlled test environment. The C compiler project burned $20,000. You cannot run workloads like that for regular people.

So the challenge is clear. We need a model that is smart enough to handle complex tasks, fast enough to iterate quickly, and cheap enough that running it for hours does not break the bank. Right now, nobody has all three.

Anthropic's models are smart, but they are mid-speed and genuinely expensive. Chinese models like DeepSeek V4 and Qwen are cheap and surprisingly capable, but inference is not very fast. Hardware solutions like Groq are incredibly fast, but they only run smaller models.

Then Xiaomi announced the MiMo-V2.5-Pro-UltraSpeed on June 8, 2026. A trillion-parameter model claiming over 1,000 tokens per second on a standard 8-GPU node, using FP4 quantization and speculative decoding. They also open-sourced the quantized weights on HuggingFace. It is early and availability is limited, but it is the closest thing to a model that checks all three boxes right now.

I think that combination, a fast and cheap capable model running inside a goal-oriented agent loop, is what unlocks real autonomous work for regular people. Not AGI in the sci-fi sense. But an AI that can take a high-level goal and actually follow through.

## The real frontier is not digital

Right now, AI is incredibly capable inside a computer. It can write code, analyze data, generate images, play games, and even discover zero-day vulnerabilities in operating systems. Give it a good enough harness and it can work for hours on complex software projects.

The physical world is a different story. There are not enough robots that can take these AI capabilities and apply them to real stuff. Building a compiler is one thing. Folding laundry, cooking a meal, assembling furniture is another. The bottleneck is no longer the brain. It is the body.

That is why I am going to study mechatronics engineering once I get to college. We have the intelligence part largely figured out in the digital space. What we need now is the hardware to bring it into the real world. Actuators, sensors, control systems, robotic platforms that can actually do things. The AI part can run on a server. The robot part needs to be built, tested, and manufactured at scale.

Companies like Figure, Boston Dynamics, and Tesla are working on this. But it is still early. The robots that exist today are either research prototypes or limited to factory floors. Getting from here to a general-purpose robot that can handle a household is a hardware and control systems problem, not an AI one.

I am not saying the AI part is solved. It is not. But it is further along than the robotics part, and I think that is where the next big wave of progress will come from. Not from making models slightly smarter, but from giving them bodies.

## What I actually believe

1. LLM scaling laws are showing diminishing returns. The gap between GPT-2 and GPT-3.5 was enormous. The gap between GPT-4 and GPT-5 is not. We are approaching a practical ceiling on what raw pretraining can do.

2. What looks like model improvement is often better scaffolding. Agent loops, MCP servers, skills, and tool harnesses are doing heavy lifting. They let us squeeze more out of existing models, but they are not the same as genuine intelligence gains.

3. Goal-mode agent loops already work. They just cost too much. The combination of faster and cheaper models like Xiaomi's MiMo UltraSpeed and better loop infrastructure will make autonomous AI assistants practical for regular people. I call that half-AGI.

4. The real bottleneck is physical. We need robots and mechatronics to bring AI into the real world. That is where the biggest gap is, and that is where I want to work.

But I would rather bet on the area where the gap is widest, hardware that can act, than on squeezing another few percentage points out of a language model.

## Sources

1. Zeff, M. (2024). "Current AI scaling laws are showing diminishing returns, forcing AI labs to change course." *TechCrunch*. [https://techcrunch.com/2024/11/20/ai-scaling-laws-are-showing-diminishing-returns-forcing-ai-labs-to-change-course/](https://techcrunch.com/2024/11/20/ai-scaling-laws-are-showing-diminishing-returns-forcing-ai-labs-to-change-course/)

2. Carlini, N. (2026). "Building a C compiler with a team of parallel Claudes." *Anthropic Engineering Blog*. [https://www.anthropic.com/engineering/building-c-compiler](https://www.anthropic.com/engineering/building-c-compiler)

3. Carlini, N. et al. (2026). "Assessing Claude Mythos Preview's cybersecurity capabilities." *Anthropic Research Blog*. [https://www.anthropic.com/research/mythos-preview](https://www.anthropic.com/research/mythos-preview)

4. Xiaomi MiMo & TileRT (2026). "MiMo-V2.5-Pro-UltraSpeed: Pushing 1T-Parameter Model Generation Speed to 1000 TPS." *Xiaomi MiMo Blog*. [https://mimo.xiaomi.com/blog/mimo-tilert-1000tps](https://mimo.xiaomi.com/blog/mimo-tilert-1000tps)

5. Shukla, H. (2025). "The AI Scaling Wall of Diminishing Returns." *arXiv:2512.20264*. [https://arxiv.org/abs/2512.20264](https://arxiv.org/abs/2512.20264)
