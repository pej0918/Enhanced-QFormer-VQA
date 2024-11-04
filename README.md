# Enhancing Q-Former for Knowledge-Based Visual Question Answering with Multi-Layer Co-Attention and Question-Aware Prompts

In **Knowledge-Based Visual Question Answering (KB-VQA)**, models must interpret both visual data and external knowledge to answer complex questions accurately. Our approach extends **Q-Former**, known for its foundational Cross-Attention mechanism for visual feature extraction, by integrating it with **MCAN** (Multimodal Co-Attention Network) and incorporating **Question-Aware Prompts** during fine-tuning. This structure not only strengthens the model’s understanding of question-image relationships but also leverages past interactions to improve overall answer accuracy.

## Model Architecture Overview
![Model Architecture](https://github.com/user-attachments/assets/f3f6f41f-1ac4-43b8-b4d7-f99369a655ea)

Our model architecture is based on a two-fold enhancement to the Q-Former structure:
1. **MCAN Integration**: **MCAN** provides a multi-layered Self-Attention and Cross-Attention framework, which captures nuanced interactions between the image and question across multiple attention layers. This multi-layer approach enables the model to handle the intricate and multi-dimensional relationships often present in KB-VQA, a task where single-layer attention mechanisms typically fall short.
2. **Question-Aware Prompts**: To further enhance reasoning capabilities, we introduce **Question-Aware Prompts** during fine-tuning. These prompts include **Answer Candidates** with confidence scores and **Answer-Aware Examples** from similar past cases, providing the model with additional context that improves its understanding of question intent and knowledge-based reasoning.

Together, these components allow the model to capture deeper interactions between images and questions, leveraging both visual and contextual knowledge for more accurate and contextually relevant answers.

### Q-Former and MCAN Integration

Our model builds upon **Q-Former** by embedding it within a more complex, multi-layer attention network via **MCAN**. The role of **Q-Former** in this setup is twofold:
- **Initial Cross-Modal Interaction**: Q-Former facilitates the initial interaction between visual and textual inputs by using a Cross-Attention layer that extracts visual features aligned with the question.
- **Bridge for Modality Gap**: Acting as a bridge, Q-Former connects the image encoder and the LLM (Large Language Model), enabling the smooth transition of visual features into a language-friendly representation, which is essential in KB-VQA tasks where nuanced visual-textual interactions are required.

However, due to its single-layer structure, Q-Former alone struggles to capture more complex question-image dependencies. To address this, we integrate **MCAN**, which brings multi-layered Self-Attention and Cross-Attention capabilities:
- **Self-Attention Layers**: These layers allow MCAN to refine the question representation iteratively, ensuring that each layer adds a deeper understanding of the question context.
- **Cross-Attention Layers**: The Cross-Attention layers focus on the image features aligned with the question, allowing the model to attend to relevant visual cues selectively.

This layered structure captures both high-level semantic interactions and detailed information, resulting in a more nuanced understanding of question-image relationships. Through MCAN, the model can process complex VQA queries with enhanced reasoning and higher accuracy.

### Fine-Tuning with Question-Aware Prompts
![Fine-Tuning Structure](imgs/model_finetuning.png)

To optimize the model for knowledge-dependent questions, we introduce **Question-Aware Prompts** during the fine-tuning phase. This component provides additional contextual information by including:
- **Answer Candidates**: A set of possible answers, each accompanied by a confidence score. These candidates help guide the model toward more probable answers, acting as a preliminary filter that narrows down options.
- **Answer-Aware Examples**: Past examples with similar question contexts, which include prior answers and the relevant image-question context. These examples allow the model to learn from prior cases and better understand the type of reasoning that might be required for similar queries.

These **Question-Aware Prompts** are especially valuable for KB-VQA tasks where questions require external knowledge or complex reasoning. By incorporating background knowledge and similar past interactions, the prompts help the model interpret questions more effectively, improving both response accuracy and contextual relevance.

#### Question-Aware Prompt Structure
![Question-Aware Prompt Structure](https://github.com/user-attachments/assets/53953d81-aa90-48cf-83c7-257e7d3eed87)

The **Question-Aware Prompt** is structured to combine multiple sources of context, as follows:
- **Answer Candidates**: Each candidate answer is paired with a confidence score, guiding the model toward probable answers and allowing it to weigh different options based on confidence levels.
- **Answer-Aware Examples**: These examples consist of past cases that contain similar questions, answers, and contexts, helping the model to draw on similar situations and answer in a more contextually relevant manner.

The **Question-Aware Prompt** thereby helps the model in:
1. **Focusing on Probable Answers**: By leveraging confidence scores in answer candidates, the model can focus on answers with higher relevance.
2. **Leveraging Contextual Examples**: Answer-aware examples provide a historical context, enabling the model to infer question intent based on similar past interactions, which is particularly useful for knowledge-based questions.

This prompt structure effectively equips the model with a broader understanding of potential answers and context, allowing it to better handle the complexity of KB-VQA tasks.

## Experiment Results

### 1. Environment Setup
```bash
conda create -n kbvqa python=3.9
```

### 2. Dataset Preparation
Download COCO, OK-VQA, and AOK-VQA datasets, and configure paths in the [dataset config files](daiv/configs/datasets/).

### 3. Training the Model
```bash
python train.py --cfg-path train_configs/pretrain_stage1.yaml
```

### 4. Fine-Tuning with Question-Aware Prompts
```bash
python train.py --cfg-path train_configs/finetune_stage2.yaml
```

### 5. Evaluation
```bash
python evaluate.py --cfg-path train_configs/finetune_stage2_eval.yaml
```

### Results on OK-VQA and AOK-VQA Datasets

Our enhanced model was evaluated on the **OK-VQA** and **AOK-VQA** datasets. Below is a comparison with the baseline **Q-Former**, **MCAN**, and our combined model with and without **Question-Aware Prompts**:

| Model           | Accuracy (Only-Question) | Accuracy (Question-Aware Prompt) |
|-----------------|--------------------------|----------------------------------|
| Q-Former        | 49.2%                     | 55.65%                          |
| MCAN            | **52.56%**                | -                                |
| Ours            | 50%                       | **56.1%**                        |

Our model, which integrates **MCAN** and **Question-Aware Prompts**, achieved a **6.9% improvement** in accuracy compared to the baseline Q-Former. This confirms the effectiveness of combining deep attention mechanisms with prompt-based fine-tuning for KB-VQA tasks, enabling the model to manage complex question-image relationships and draw on contextual knowledge.

## Conclusion

Our model for **Knowledge-Based Visual Question Answering (KB-VQA)** introduces two critical enhancements: **MCAN** for multi-layer attention, which allows deeper visual-textual interactions, and **Question-Aware Prompts** during fine-tuning, which provide supplementary context. These advancements enable the model to handle complex interactions and leverage external knowledge effectively, leading to more accurate, context-aware answers.

Experimental results show a **6.9% increase in accuracy**, validating the efficacy of this approach in advancing KB-VQA tasks without extensive fine-tuning. The integration of MCAN and Question-Aware Prompts demonstrates a promising direction for improving VQA models in scenarios requiring both rich visual analysis and external knowledge.
