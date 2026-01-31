# athology-SmolVLM2-2.2B

** MedNemesis 2.2B Pathology
A compact, domain-specialized visual question answering model for pathology

<p align="center">
  <img src="https://img.shields.io/badge/Model-2.2B-blue?style=for-the-badge&logo=huggingface&logoColor=white" alt="Model Size">
  <img src="https://img.shields.io/badge/Inference_VRAM-~5–7_GB_(fp16)-orange?style=for-the-badge" alt="VRAM fp16">
  <img src="https://img.shields.io/badge/Quantized-~3–4_GB-green?style=for-the-badge" alt="Quantized">
  <img src="https://img.shields.io/badge/License-Apache%202.0-brightgreen?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/Dataset-PathVQA-purple?style=for-the-badge" alt="Dataset">
</p>

## Project Vision

MedNemesis 2.2B Pathology demonstrates how very small multimodal models can be efficiently adapted to specialized medical imaging domains with modest compute.

By fine-tuning **SmolVLM2-2.2B-Instruct** — one of the most memory-efficient open vision-language models available — on the **PathVQA** dataset, the model gains improved grounding in pathology-specific reasoning: yes/no interpretation, histologic pattern description, gross feature identification, and short explanatory answers.

The entire effort emphasizes accessibility: training in one epoch on a single high-end GPU, low inference footprint, and a complete end-to-end pipeline that others can reproduce or extend.

**Important note**  
This project is strictly for **research and educational purposes**.  
It has **not** undergone clinical validation and must **never** be used for diagnostic, prognostic, or treatment-related decisions in real patient care.

## Model at a Glance

| Property                  | Details                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| Base architecture         | SmolVLM2-2.2B-Instruct (HuggingFaceTB)                                  |
| Parameter count           | 2.2 billion                                                             |
| Fine-tuning dataset       | PathVQA (~32.6k question-answer pairs, ~4.3k unique pathology images)   |
| Adaptation method         | 4-bit QLoRA (parameter-efficient fine-tuning)                           |
| Training duration         | 1 epoch                                                                 |
| Primary hardware          | Single H100 / A100 (high-end consumer GPUs viable with adjustments)     |
| Inference memory footprint| ~5–7 GB VRAM (float16) / ~3–4 GB (4-bit quantization)                   |
| Output style              | Yes/no + short descriptive answers                                      |
| License                   | Apache 2.0 (inherited from base model)                                  |

## Observed Improvements (Qualitative)

- Clearer recognition of pathology domain language and question intent
- Stronger performance on binary (yes/no) pathology questions
- Better alignment with common histologic descriptions, stain interpretations, and gross pathology features
- Still constrained by the base model’s resolution and capacity on very fine-grained or rare patterns

## Repository Contents (High-Level)

- Scripts to download, process, and reformat the PathVQA dataset into image + JSONL structure
- Complete fine-tuning pipeline using 4-bit quantization and a custom vision-language data collator
- Utility to merge trained LoRA adapters back into the base model for easy deployment
- Ready-to-run Gradio web interface for uploading images and asking questions
- Documentation and configuration files for reproducibility

## Intended Use & Audience

This repository is designed for:

- Researchers exploring efficient domain adaptation of small vision-language models
- Students learning multimodal fine-tuning in medical imaging
- Developers prototyping lightweight pathology AI tools
- Anyone interested in low-resource medical VQA experimentation

## Responsible AI & Limitations

- Single-epoch training means results should be considered preliminary
- No preference optimization, safety alignment, or red-teaming applied
- Performance on subtle, rare, or out-of-distribution pathology findings remains limited
- No formal quantitative benchmarks reported yet (planned future work)
- **Explicitly not suitable for clinical deployment or medical decision support**

## Acknowledgments

Heartfelt thanks to:

- HuggingFaceTB for creating and open-sourcing SmolVLM2 — truly democratizing multimodal AI
- The PathVQA authors (He et al., 2020) for releasing such a valuable domain-specific resource
- flaviagiammarino for maintaining and hosting PathVQA on Hugging Face
- The teams behind PEFT, bitsandbytes, accelerate, and transformers

## Citation

If this work contributes to your research or project, please consider citing:

```bibtex
@misc{mednemesis-pathology-2026,
  author       = {Rumii},
  title        = {MedNemesis 2.2B Pathology: Fine-tuned SmolVLM2 on PathVQA},
  year         = {2026},
  publisher    = {GitHub},
  journal      = {GitHub repository},
  howpublished = {\url{https://github.com/[your-username]/MedNemesis-2.2B-Pathology}}
}

@article{he2020pathvqa,
  title={PathVQA: 30000+ Questions for Medical Visual Question Answering},
  author={He, Xuehai and Zhang, Yichen and Mou, Luntian and Xing, Eric and Xie, Pengtao},
  journal={arXiv preprint arXiv:2003.10286},
  year={2020}
}
