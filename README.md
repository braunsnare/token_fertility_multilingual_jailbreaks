token_fertility_multilingual_jailbreaks
# Why LLMs Forget Guardrails: The Mechanistic Role of Token Fertility in Multilingual Jailbreaks

Overview

This repository contains the code, datasets, and visual artifacts for investigating Attention Starvation—a mechanistic hypothesis explaining why Large Language Models (LLMs) fail to enforce safety guardrails in low-resource languages.

We demonstrate that high-fertility tokenization in non-Latin scripts (e.g., Armenian) forces the model to distribute attention weights across an unnaturally high number of sub-word tokens. This mathematical dilution via the Softmax function inherently "starves" the safety-critical system prompt of the attention mass required to trigger a refusal, leading to multilingual jailbreaks.

Repository Structure

/data/: Contains translated benchmark dataset sorry-bench_arm_swa.json and clean_attention_results.json dataset containing the calculated ASR scores, token fertility and attention mass.
environment.yml: Conda environment file for exact dependency reproduction.

Reproducibility

1. Clone the repository:
   git clone https://github.com/braunsnare/token_fertility_multilingual_jailbreaks.git
   cd attention-starvation
2. Create the Conda environment:
   conda env create -f environment.yml
   conda activate attention-starvation-env
3. Provide HuggingFace Credentials:
   You will need to be logged into HuggingFace to download Llama-3-8B-Instruct. Run              huggingface-cli login in your terminal before running the scripts. 

Core Experiments

This project evaluates model behavior across three fertility baselines using Llama-3-8B-Instruct:
  1. English (Baseline): Low token fertility, strong safety adherence.
  2. Swahili (Latin Script): Medium token fertility, moderate safety adherence.
  3. Armenian (Non-Latin Script): Extremely high token fertility, severe attention
     starvation, and high jailbreak success rates.

Results and Artifacts

The primary finding of this research is that multilingual jailbreaks are not purely caused by uneven alignment training, but by a structural, mathematical failure of the transformer's attention mechanism when dealing with heavily fragmented tokens.

