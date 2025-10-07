# Jaume Lab PhD Candidate Assignment

**Due date:** 10 days after receiving instructions. Please let me know if you need more time. 

## Overview

Welcome to the Jaume Lab selection assignment.  
This exercise is **open-ended by design**: it tests your ability to think, design, and implement within a modern multimodal AI research framework.

Your task is to **propose and/or implement part of a model and data preparation pipeline** for developing a **zero-shot segmentation and classification model in microscopy imaging**, using **H&E-stained histology** as an example.

## Background

### H&E Imaging
**Hematoxylin and Eosin (H&E)** staining is the most widely used technique in histopathology to visualize the microscopic architecture of tissues. **Hematoxylin** stains nuclei blue or purple, and **Eosin** stains cytoplasm, connective tissue, and extracellular components pink or red.  

Together, they provide morphological contrast that allows pathologists to identify **cell types, tissue organization, and pathological changes** such as inflammation, necrosis, or malignancy.  
In computational pathology, H&E images serve as the foundation for developing models that detect, segment, and classify cellular and tissue structures across disease types.

---

### Zero-Shot Segmentation and Classification
**Zero-shot learning** refers to a model’s ability to generalize to **new, unseen classes or tasks** without explicit training examples for them (think like ChatGPT).  
In microscopy:
- **Zero-shot segmentation** means delineating any structure from text descriptions provided by a user. Aka, no supervised learning anymore, we become fully open-ended. 
- **Zero-shot classification** means labeling tissue or cell types based on descriptive prompts rather than fixed training labels.

These models typically rely on **joint vision–language representations** trained on paired data (i.e., images + text captions). When prompted with a new instruction like *“highlight apoptotic bodies”* or *“detect fibrotic areas”*, the model can perform the task by transferring knowledge from semantically related concepts it has already learned.

---

### Instruction Fine-Tuning
**Instruction fine-tuning** is a training strategy where a model (here a multimodal LLM) learns to follow **natural-language instructions** rather than specific labels.  
Instead of simple supervision like  
> Image → “Tumor”  

The model is trained with structured samples like  
> Instruction: “Identify and outline the tumor region.”  
> Input: Image patch  
> Output: Segmentation mask + caption  

By exposing the model to many of such examples, the system learns to:
- Interpret diverse phrasing of user requests,
- Perform multimodal reasoning, and
- Produce consistent, interpretable outputs.  

---

## 🎯 Objective

Design a **small but meaningful component** of a large system that takes:

- **Input:** a region of interest (ROI) image + a **text instruction** (e.g., _“highlight necrotic regions”_, _“count mitotic figures”_)  
- **Output:** a combination of  
  - **Segmentation mask** (semantic or instance),  
  - **Bounding boxes**,  
  - **Accompanying descriptive text.**

You **do not** need to build the full system (this is a 1-year project!), but you must:
1. **Propose a concrete architecture or pipeline** covering the whole concept.
2. **Implement one small component** (e.g., data ingestion, model selection, training loop, evaluation, instruction generation, etc.)
3. **Justify your design choices** (technical rationale, scalability, feasibility).

Assume **compute is unlimited**:
- You can fine-tune a **70B LLM** and a **1B vision model** without a problem.  
- You have **unlimited OpenAI API access** to generate synthetic instructions, captions, or QA pairs. Or any other LLMs of your choice. 

---

## 🧩 Suggested Directions

You may focus on one or more of the following components:

### 1. Data Ingestion and Preparation
- Identify **existing public segmentation/classification datasets** (e.g., PanNuke, Lizard, NuCLS, CoNSeP, MoNuSeg, etc.).
- Propose a **pipeline to transform existing annotations** (masks, nuclei, captions, etc.) into instruction–response pairs suitable for **zero-shot training**.
- Design a **data generation loop** using LLMs to produce varied and realistic instructions (e.g., “Find mitotic figures” → segmentation mask + caption).
- Think about guardrails! E.g., what if a user asks to count the hepatocytes (liver cells), but the tissue is actually kidney? The output should likely look like: "This appears to be kidney tissue, are you sure this is a liver image?"
- Discuss how to **maximize diversity** across tissue types and diseases.

### 2. Modeling Strategy
- Propose a **joint model** (vision–language transformer, or instruction-tuned LLM+ViT hybrid).
- Discuss **transfer learning** and how to leverage pretrained biomedical or general models.
- Suggest training objectives (contrastive loss, segmentation loss, caption loss, instruction tuning).
- Suggest ways to generate the segmentation output. How are SegmentAnything, BioMedParse, etc., doing this task?

### 3. Implementation Component
Choose one small but technically interesting piece to implement, for example:
- Dataset loader and instruction generator.
- Vision encoder fine-tuning script.
- Prompt-to-segmentation proof of concept using a pretrained SAM/CLIP/DINO model.
- LLM-based instruction expansion pipeline.
- It can be any component that you feel most comfortable implementing. Being small is not a problem, but it has to be justified and clean. 

---

## 📚 References

You could take inspiration from the following foundational works:

- [**A foundation model for joint segmentation, detection and recognition of biomedical objects across nine modalities**](https://www.nature.com/articles/s41592-024-02499-w)  
- [**A multimodal generative AI copilot for human pathology**](https://www.nature.com/articles/s41586-024-07618-3)

---

## 🧮 Evaluation Criteria

Your submission will be evaluated on:

| Criterion | Description |
|------------|--------------|
| **Originality** | Novel, clear, and well-motivated approach |
| **Technical Depth** | Understanding of multimodal learning and data engineering |
| **Implementation Quality** | Clean, reproducible code for the selected component |
| **Scalability Thinking** | How easily your approach can scale to large datasets and multiple modalities |
| **Clarity** | Well-structured explanation and justification |

---

## ⚙️ Practical Details

- **Submission:**  
  Fork this repository and submit your project as a **private GitHub repo** with `guillaumejaume` as a collaborator.

- **Structure:**

├── README.md # Main description (this file)
├── data/ # Example data or links
├── src/ # Code for your component
├── notebooks/ # Optional exploratory notebooks
├── results/ # Optional visualizations
└── references/ # Additional papers, diagrams, or notes


- **Language:** Python (preferably with PyTorch)
- **Tools:** You are encouraged to use **ChatGPT, Cursor, or similar tools** to accelerate prototyping. 

---

## Final Thought

This is not a test of your ability to finish—there is WAY too much work. It's a test of how you **think and approach a complex problem**.  
Show curiosity, ambition, and clarity.  
Surprise us.

— *Jaume Lab* 
Department of Oncology, CHUV/UNIL
