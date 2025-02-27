# 🎯 Enhancing Q-Former for Knowledge-Based Visual Question Answering with Multi-Layer Co-Attention and Question-Aware Prompts

In **Knowledge-Based Visual Question Answering (KB-VQA)**, models must interpret both visual data and external knowledge to answer complex questions accurately. Our approach extends **Q-Former**, known for its foundational Cross-Attention mechanism for visual feature extraction, by integrating it with **MCAN** (Multimodal Co-Attention Network) and incorporating **Question-Aware Prompts** during fine-tuning. This structure not only strengthens the model’s understanding of question-image relationships but also leverages past interactions to improve overall answer accuracy.

## 🧠 Model Architecture Overview

![Model Architecture](https://github.com/user-attachments/assets/f3f6f41f-1ac4-43b8-b4d7-f99369a655ea)

The architecture integrates **MCAN** and **Question-Aware Prompts** into the **Q-Former** framework, offering multi-layered cross-attention and enhanced contextual understanding.

## 💡 Key Contributions
- **MCAN Integration:** Multi-layered Self-Attention and Cross-Attention for richer image-question interactions.
- **Question-Aware Prompts:** Introduce answer candidates and past example contexts to enhance reasoning.
- **Improved Accuracy:** Achieved **6.9% increase** in accuracy on **OK-VQA** and **AOK-VQA** datasets.

## ⚙️ Methodology
1. **Q-Former & MCAN Integration:** Combines initial cross-modal interaction with deep multi-layer attention.
2. **Fine-Tuning with Question-Aware Prompts:** Utilizes answer candidates and answer-aware examples to boost context understanding.

### 📊 Question-Aware Prompt Structure

![Question-Aware Prompt Structure](https://github.com/user-attachments/assets/53953d81-aa90-48cf-83c7-257e7d3eed87)

This structure combines **Answer Candidates** with confidence scores and **Answer-Aware Examples** from past cases, enhancing the model's reasoning capabilities.

## 🚀 Experiment Results
| Model           | Accuracy (Only-Question) | Accuracy (Question-Aware Prompt) |
|-----------------|--------------------------|----------------------------------|
| Q-Former        | 49.2%                     | 55.65%                          |
| MCAN            | **52.56%**                | -                                |
| Ours            | 50%                       | **56.1%**                        |

## 🎯 Conclusion
- **6.9% accuracy improvement** on KB-VQA tasks.
- Demonstrated robust performance without extensive fine-tuning.


