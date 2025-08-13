# mathCrow: Agentic AI for math and reasoning tasks

## Abstract

mathCrow is a proof-of-concept extension of ChemCrow [1] to math-based tasks. The mathCrow agent has access to two expertly designed tools and the ability to independently determine which tool to call to accomplish a given task. This framework provides greater autonomy than a human-based framework, where a human expert would parse the input prompt, decide which tool (function or software package) to call and preprocess the data according to the requirements of the selected tool. We provide an open-source/zero cost implementation of mathCrow using Meta’s llama3.3 model and Huggingface embeddings (in addition to a simpler implementation with paid OpenAI LLM models and embeddings). We test our proposed mathCrow framework on text datasets derived from two research papers and with complex linear assignment problems (LAP). Our results show that mathCrow i) reduces hallucinations in LLM generated responses, and ii) increases autonomous task completion by formulating a precise linear assignment problem from a complex input prompt. Interestingly, our results also confirm that, for the reasoning-based LAP task, GPT-o reasoning models perform better than their general counterparts.

## References
