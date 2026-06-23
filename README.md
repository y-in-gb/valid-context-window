# Valid Context Window: Real-world Translation Task Evaluation Study based of OFAT Raw Text Data and Open Source LLMs
**崖雁yayan [Bilibili: 作者_崖雁 , GitHub: y-in-gb]**
*Author of “Over Flow And Throw”*
*Starter of OFAT v1.0 License*
*Open Source “Over Flow And Throw” Chinese & English raw text data in GitHub repository : y-in-gb/open-fiction-access-token*
**June 23, 2026**

## Background
Large Language Models (LLMs) with long context window show escalating hallucination and bad memory (e.g. forget to follow instruction) issues as the input gets longer. Although the severity and task performance varies for different open source LLM providers and model size, these issues appear commonly in many well-known open source LLMs.

## Abstract
This study aims to provide reproducible experiment methodology and results to introduce the idea of “Valid Context Window” through a real-world task of translating the fiction “Over Flow And Throw” (OFAT) from Chinese to English.

### Definition of Context Window
The idea of “Valid Context Window” is built upon “Context Window” also known as “Context Length,” which refers to the total combined token capacity of a single LLM inference:

Context Window = Input tokens (Total Message Tokens) + Output tokens (LLM Generated Tokens)

### Definition of Total Message Tokens
Total Message Tokens = System Prompt tokens + User Prompt tokens (Input Chinese Text Tokens)

Here’s an example process of converting input text to tokens:

Input Text [Chinese text with 602 characters] → Model Tokenizer → Input Tokens [592 tokens]

Every LLM has its own model tokenizer, so it’s not always the case that the number of tokens will be less than the number of characters after tokenization, it can be larger, and it varies depend on the model tokenizer.

### Definition of Valid Context Window
“Valid” means the LLM generated output result (e.g. the English translation) is good enough, it does not need to be perfect, but just good enough so that 0 human effort (e.g. editing) is required to amend the result.

“Valid Context Window” (VCW) is the context window that can allow the LLM to generate purely valid output result for a specific task, and in this study, it’ll be the Chinese to English translation task. 

Since the length of the output English translation is dictated by the input Chinese text length, the output tokens(which does not contain system prompt) will be relatively stable and always be smaller than the input tokens(which contain system prompt). 

Therefore, the only variable required to manipulate is the input tokens. The input tokens that allow LLM to generate valid output will be refer as the “Valid Input Tokens” (VIT).
### Why “Valid” is so important? 
Because the editing experience produced upon the output is hard to accumulate and reuse in any other LLMs. Flaws like wrong choosing of word in the output can be subtle, but the problem is those flaws cannot be 100 percent taken care by regex. LLMs can sprout all kinds of different word choices and combinations to make the resulting sentence not smooth, coherent, or make sense to human.

Instead of fixing endless small flaws from the output side, I think it’s more worthy to try fixing it from source, which is the input. I can build a vocabulary set to past on word knowledge as the context to any LLMs as long as they have the basic ability to follow instruction. 

Task-related knowledge should be easily portable as context for any LLM to facilitate their task. My thought is to explore a new way for the LLMs to adapt just enough knowledge, and then generate valid output, but I will need to design another set of experiments to consolidate my hypothesis by testing out the most LLM adaptable format of the vocabulary set in future study.

## Goal
In the current study, my goal is to test out the VIT for various LLMs, and within the VIT, the LLMs are expected to have 0 hallucination, 0 bad memory issue, and able to generate valid results.

## Quick Look of the Final Results
Llama, Mistral, Qwen, and GLM models with context window of 32k or 128k are tested in this study, and surprisingly, the empirical VCW for Chinese to English translation task is much smaller than the model’s context window.

A model with a 32k context window had a measured VCW of around 4k tokens.

A model with a 128k context window also had a measured VCW of around 4k tokens.

This suggest a huge gap exist between theoretical capacity and real-world utility. While these models can technically ingest 32k+ tokens, their VCW for reliable translation consistently falls within just 3% to 12% of the context window.

Check out the Methodology, Detailed Experiment Results, and [`the full VCW report`](VCW-report.pdf) via https://github.com/y-in-gb/valid-context-window

Get the open source raw data used in this project via https://github.com/y-in-gb/open-fiction-access-token

*This paper “Valid Context Window: Real-world Translation Task Evaluation Study based of OFAT Raw Text Data and Open Source LLMs,” is publicly released in GitHub repository “y-in-gb/valid-context-window” by 崖雁yayan [Bilibili: 作者_崖雁 , GitHub: y-in-gb] in June 2026.*

## Acknowledgements
I would like to express my sincere gratitude to all those who have contributed to the foundation models that made this work possible. First, I want to thank the original content creators, whose writings, conversations, and creative works formed the raw material from which knowledge is drawn. I am also deeply grateful to the curators and annotators who carefully collected, cleaned, and organized these content into high-quality datasets, providing the essential foundation for training these powerful models. I further thank the research teams who built and trained these models using these datasets, including Meta AI for developing and releasing the Llama-3.2-3B-Instruct and Llama-3.1-8B-Instruct models, Mistral AI for their Mistral-Nemo-Instruct-2407 model, the Qwen Team for their series of models (Qwen2, Qwen2.5, Qwen2.5-1M, Qwen3, and Qwen3.5), and Zhipu AI for providing the GLM-4-9B-0414 model. Their technical expertise, dedication, and commitment to open research have been truly inspiring. Lastly, I want to acknowledge the sponsors who funded these research teams, as their financial support enabled the computational resources and sustained efforts necessary to develop these state-of-the-art models.

At the end, I would like to thank DeepSeek for being an awesome coding assistant throughout this research.

## Citations
[1] Meta AI. Llama-3.2-3B-Instruct. https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct, 2024. Accessed: 2026.

[2] Meta AI. Llama-3.1-8B-Instruct. https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct, 2024. Accessed: 2026.

[3] Mistral AI. Mistral-Nemo-Instruct-2407. https://huggingface.co/mistralai/Mistral-Nemo-Instruct-2407, 2024. Accessed: 2026.

[4] Qwen Team. Qwen3 Technical Report. *arXiv preprint arXiv:2505.09388*, 2025. https://arxiv.org/abs/2505.09388.

[5] A. Yang et al. Qwen2 Technical Report. *arXiv preprint arXiv:2407.10671*, 2024.

[6] Qwen Team. Qwen2.5: A Party of Foundation Models. https://qwenlm.github.io/blog/qwen2.5/, September 2024. Accessed: 2026.

[7] Qwen Team. Qwen2.5-1M: Deploy Your Own Qwen with Context Length up to 1M Tokens. https://qwenlm.github.io/blog/qwen2.5-1m/, January 2025. Accessed: 2026.

[8] A. Yang et al. Qwen2.5-1M Technical Report. *arXiv preprint arXiv:2501.15383*, 2025.

[9] Qwen Team. Qwen3.5: Towards Native Multimodal Agents. https://qwen.ai/blog?id=qwen3.5, February 2026. Accessed: 2026.

[10] Zhipu AI. GLM-4-9B-0414. https://huggingface.co/zai-org/GLM-4-9B-0414, 2024. Accessed: 2026.

## GitHub repository links for the open source LLMs used in this research
- Llama-3.2-3B-Instruct: https://github.com/meta-llama/llama3
- Llama-3.1-8B-Instruct: https://github.com/meta-llama/llama3
- Mistral-Nemo-Instruct-2407: https://github.com/mistralai/mistral-inference
- Qwen3-4B-Instruct-2507: https://github.com/QwenLM/Qwen3
- Qwen3-8B: https://github.com/QwenLM/Qwen3
- Qwen2.5-7B-Instruct: https://github.com/QwenLM/Qwen2.5
- Qwen2.5-7B-Instruct-1M: https://github.com/QwenLM/Qwen2.5
- Qwen3.5-9B: https://github.com/QwenLM/Qwen3.6
- GLM-4-9B-0414: https://github.com/zai-org/GLM-4
