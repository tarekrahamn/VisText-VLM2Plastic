# Plastic Pollution Through AI's Eyes — Experiment Code

This bundle contains a self-contained Colab/Jupyter notebook for the bilingual plastic-waste VQA paper.

## Files
- `Plastic_Pollution_VLM_Experiments.ipynb` — complete experiment pipeline
- `requirements.txt` — Python dependencies

## Implemented experiments
1. Zero-shot multi-VLM benchmark
2. English vs Bangla gap
3. Image+Question vs Question-only grounding ablation
4. English–Bangla output consistency
5. Category-wise recognition, macro vs micro
6. Paired bootstrap 95% confidence intervals
7. Human evaluation/error annotation template
8. Paper-ready CSV tables and PNG figures

## Default model IDs
- OpenAI: `gpt-5.6-luna` (configurable; can switch to `gpt-5.6-sol`)
- Gemini: `gemini-3.6-flash`
- Qwen: `Qwen/Qwen2.5-VL-7B-Instruct`
- Gemma: `google/gemma-3-4b-it`

## Before the final paper run
1. Upload `Dataset.zip` and `plastic_waste_vqa_bilingual.json` to Colab.
2. Add API keys to Colab Secrets: `OPENAI_API_KEY`, `GEMINI_API_KEY`, optionally `HF_TOKEN`.
3. Run a one-sample smoke test for each model.
4. Set `DEV_MODE=False`.
5. Run every model with exactly the same zero-shot prompt.
6. Do not tune prompts after looking at test results.
7. Complete the human annotation template for grounding/hallucination analysis.

## Important evaluation choices
- Recognition: strict and relaxed category accuracy.
- Description/environmental reasoning: multilingual semantic similarity.
- Grounding gain: paired score(Image+Q) - score(Q-only).
- Language gap: paired English score - Bangla score.
- Cross-lingual consistency: multilingual embedding similarity; the thresholded BCS should be calibrated on validation/human labels rather than treated as intrinsically correct.
- Report macro category accuracy because the dataset is class-imbalanced.

## Hardware
OpenAI/Gemini use APIs. Qwen/Gemma use local Hugging Face inference and are configured for 4-bit loading; a Colab GPU is strongly recommended. Load only one local VLM at a time.
