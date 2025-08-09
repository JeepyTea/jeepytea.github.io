---
layout: post
title: "Benchmark Fury: TiānshūBench 0.0.1-mini vs Claude Opus 4.1, GPT-5, Kimi K2, and More"
date: 2025-08-09
categories: [general, update]
---


It\'s been an exciting couple of weeks, with new models released by big
players like Anthropic and OpenAI, as well as open weight models from
the scrappy challengers Moonshot AI and Alibaba.

With so many new models in the pipeline, TiānshūBench faced a few
problems:

-   The complete problem set took too long to run on each new model. The
    combination of testing different programming languages, number of
    shots (retries) allowed, and individual test cases means that each
    model would have to run over 1000 tests, many of which would require
    multiple queries.\
    \
    This lag time meant that I couldn\'t get great feedback on improving
    the tests themselves. This is still a part time project, so being
    able to improve things quickly is critical.\
    \
    More importantly, the results wouldn\'t be *timely*, which would
    make them useful to me and anyone else following TiānshūBench.

-   Providers would remove models without warning or would otherwise be
    unreliable.

-   With this explosion in test cases came an explosion in costs. For
    example, it cost around \$150 just to do a complete test on Claude
    Sonnet 3.7, an older, cheaper model.

The solution is here, though: introducing TiānshūBench version
0.0.1-mini! The mini version of the test will restrict the test cases
thusly:

-   Only one generated programming language used. Previous runs show
    that the generated language used didn\'t affect the outcome that
    much, even if it did provide more samples, and therefore more
    accuracy.
-   Only run the 8-shot version of the tests. This provides more of an
    agentic environment and gives the models a chance to correct errors
    due to underspecification in the language description.
-   Don\'t run the easiest tests. These are nearly saturated with the
    top end models scoring near 100% for "Hello World" type tasks.

Tradeoffs
---------

While much faster and cheaper, this newfound flexibility comes at the
cost of accuracy. Some of the models end up tied due to the low number
of tests. Model settings that "should" come out ahead will often flub a
couple tests, dragging their test scores down.

Costs
-----

With the advent of TiānshūBench 0.0.1-mini, costs and time came way
down. For example, testing Claude 3.7 Sonnet went down from \$150 to
about \$3.50. It still is around \$17 just to test Claude Opus 4.1.
OpenAI seems *much *less expensive at this point, with a cost of around
\$11 to test 6 different LLM configurations.

Updates
-------

With this release of TiānshūBench, there are several updates:

-   Updated the language description, filling in block and statement
    sections, and fixing typos.
-   Updating the system prompt.
-   Adding new model providers, including OpenAI, Gemini, and Anthropic.
    This was tricky, as all of them have slightly different advanced
    parameters, max\_completion\_tokens instead of max\_tokens, for
    example.

( I don\'t have any hard numbers, but these updates seemed to help Kimi
K2 quite a bit.)

Full list of models tested:

-   anthropic/claude-3-5-haiku-20241022
-   anthropic/claude-3-7-sonnet-20250219
-   anthropic/claude-opus-4-1-20250805
-   anthropic/claude-opus-4-20250514
-   anthropic/thinking/claude-3-7-sonnet-20250219
-   anthropic/thinking/claude-opus-4-1-20250805
-   chutes/deepseek-ai/DeepSeek-R1-0528
-   chutes/zai-org/GLM-4.5-Air
-   gemini/gemini-2.5-flash
-   gemini/gemini-2.5-pro
-   gemini/thinking/gemini-2.5-flash
-   gemini/thinking/gemini-2.5-pro
-   nvidia/moonshotai/kimi-k2-instruct
-   nvidia/openai/gpt-oss-120b
-   nvidia/openai/gpt-oss-20b
-   openai/gpt-5
-   openai/gpt-5-mini
-   openai/gpt-5-nano
-   openai/thinking/gpt-5
-   openai/thinking/gpt-5-mini
-   openai/thinking/gpt-5-nano

Future Updates
--------------

I found that many of the models "cheated" by writing to the test. For
example, haiku-3-5, one of the weaker models, passed test\_case23, a
JSON parsing task, by making some big assumptions about the file format,
which happened to work in this test case. In the future, we\'ll need to
run each generated program against multiple sets of input and output to
guarantee that they work. The re-prompt will probably be something like
"this program did not work for input XXXX" instead of giving away the
correct output!

OpenAI\'s Responses API may be the way of the future for this type of
task.

The heavier thinking models often take a long time, time out, and fail
the test. In the future, we need to allow some flexibility in this
timeout for multi-shot and thinking models.

Models On the Short List for Testing in the Future
--------------------------------------------------

-   chutes/Qwen/Qwen3-235B-A22B-Thinking-2507
-   Qwen3-Coder-480B-A35B-Instruct
-   Qwen3-235B-A22B-Instruct-2507
-   Grok

That\'s all for now, and keep an eye out for the results of TiānshūBench
0.0.1-mini to be posted soon!
