# CORE-CMR

> A privacy-preserving, locally deployable LLM pipeline for generating cardiac MRI report summaries with hallucination detection and uncertainty awareness.

CORE-CMR was developed as an MSc individual research project investigating how lightweight open-source language models can support safe, efficient cardiac magnetic resonance (cMRI) reporting. The pipeline was designed for highly specialised medical text generation, with an emphasis on local deployment, minimal compute requirements, factual grounding, and integrated model-safety evaluation.

## Project overview

The project evaluates a compact Llama 3.2 3B model for generating draft cMRI summaries from structured clinical findings. It combines:

- Parameter-efficient fine-tuning with Low-Rank Adaptation (LoRA)
- Quantised model loading and inference for resource-efficient execution
- Retrieval-Augmented Generation (RAG) over historical report embeddings
- A custom hallucination-detection classifier
- Token-level Monte Carlo dropout for confidence and uncertainty visualisation
- Classical NLP metrics alongside clinically relevant safety evaluation

The work was designed to keep patient data within a secure institutional environment, avoiding reliance on cloud-based LLM APIs.

## Key findings

- Classical text-generation metrics—including BLEU, ROUGE, METEOR, and cosine similarity—were poorly aligned with clinically significant errors, particularly small numerical hallucinations.
- The best RAG configuration, hybrid reranking with three retrieved examples, reduced the automated hallucination rate from **50.4% to 12.2%** across 540 test summaries.
- A custom hallucination-detection model achieved **76% accuracy**, with **81.8% sensitivity** and **71.4% specificity** on a held-out test set.
- LoRA fine-tuning produced more clinically styled outputs and reduced overconfidence, although its benefit was more modest than RAG and required manual evaluation because the detector was affected by domain shift.
- Monte Carlo dropout provided an exploratory interpretability layer, highlighting low-confidence, high-uncertainty tokens for clinician review.

## Technical focus

- Training, fine-tuning, quantising, and evaluating LLMs for a specialised medical NLP task
- Building resource-efficient local inference workflows
- Designing safety evaluation around hallucinations rather than generic language-similarity metrics
- Retrieval and reranking with vector embeddings
- Confidence calibration and uncertainty-aware generation
- GPU-cluster execution and parallel GPU processing

## Technologies

- Hugging Face
- Transformers
- PyTorch
- PEFT / LoRA
- BitsAndBytes
- Scikit-learn
- CUDA
- GPU cluster management and parallel GPU processing
- FAISS

## Data and code availability

This repository intentionally does not include source code, trained model parameters, patient-derived datasets, generated reports, or evaluation outputs. The project used sensitive clinical data held in a secure institutional environment, and these materials cannot be released publicly.

The implementation, experiment design, and model outputs can be demonstrated on request, subject to the relevant permissions and data-governance requirements.

## Important note

CORE-CMR is a research prototype and is **not** a clinical decision-support tool. All generated summaries require clinician review. The project’s purpose is to investigate safer, more interpretable workflows for AI-assisted reporting—not to replace clinical judgement.
