# 🧠 Psychology Quality Dataset

> A curated, high-quality dataset for training AI models on psychology and mental health conversations.

A cleaned and filtered dataset combining multiple public HuggingFace psychology datasets, optimized for training mental health conversation AI assistants.

---

## ✨ What's Inside

- Cleaned conversation pairs focused on psychology & mental health topics
- Converted to standard user/assistant format
- Ready for fine-tuning language models

---

## 📊 Source Datasets

| Dataset | Format |
|---------|--------|
| `Gragroo/psy_conv_v1_gpt1` | conversations |
| `Gragroo/psy_conv_v1_gpt2` | conversations |
| `Gragroo/psy_conv_v1_gpt3` | conversations |
| `psycode1/psyset` | [INST] text |
| `Gragroo/psychology-question-answer_psygpt_format` | Q&A |

---

## 🔧 Cleaning Pipeline

### Step 1: Load & Convert
Load from HuggingFace → Convert all formats to standard `user/assistant` structure

### Step 2: Remove Duplicates
Keep only one copy when user message + assistant reply are identical

### Step 3: Safety Filter
Remove responses containing harmful keywords like: kill, suicide, harm, abuse, violence, self-harm

### Step 4: Quality Filter
Keep only responses containing therapeutic keywords like: understand, feel, help, support, anxiety, stress, depression, therapy, coping

---

## 💻 Code & Processing

This dataset was created using a **Kaggle Notebook**. The notebook handles all the data loading, cleaning, and processing.

### Setup
- **Environment:** Kaggle with GPU (NVIDIA Tesla T4)
- **Python:** Version 3.12
- **Key Libraries:** torch, transformers, datasets, pandas

### Installation
The notebook installs required packages:
```python
!pip install torch
!pip install transformers datasets pandas
```

### Processing Steps in Code
1. **Load datasets** - Fetch all 5 datasets from HuggingFace using `load_dataset`
2. **Convert format** - Convert different formats to standard conversation structure (user/assistant)
3. **Deduplicate** - Remove duplicate conversation pairs
4. **Safety filter** - Filter out responses with harmful content keywords
5. **Quality filter** - Keep only responses with therapeutic keywords
6. **Export** - Save to CSV and JSON formats

### Key Code Snippets

```python
from datasets import load_dataset

# Load dataset from HuggingFace
ds = load_dataset("Gragroo/psy_conv_v1_gpt1")

# Convert to standard format
def convert_format(example):
    return {
        "conversations": [
            {"role": "user", "content": example["question"]},
            {"role": "assistant", "content": example["answer"]}
        ]
    }

# Safety keywords to filter
harmful_keywords = ["kill", "suicide", "harm", "abuse", "violence", "self-harm"]

# Quality keywords to keep
therapeutic_keywords = ["understand", "feel", "help", "support", "anxiety", "stress", "depression"]
```

---

## 📁 Output Files

| File | Description |
|------|-------------|
| `psychology_dataset.csv` | Tabular format |
| `psychology_dataset.json` | Conversation format |
| `psychology_dataset.zip` | Compressed archive |

---

## 📖 Example Data

```json
{
  "conversations": [
    {
      "role": "user",
      "content": "What are the symptoms of anxiety?"
    },
    {
      "role": "assistant",
      "content": "Anxiety can manifest as worrying thoughts, physical tension, and restlessness..."
    }
  ],
  "dataset_name": "Gragroo/psy_conv_v1_gpt1"
}
```

---

## 🔗 Source Links

All source datasets from HuggingFace:

1. [Gragroo/psy_conv_v1_gpt1](https://huggingface.co/datasets/Gragroo/psy_conv_v1_gpt1)
2. [Gragroo/psy_conv_v1_gpt2](https://huggingface.co/datasets/Gragroo/psy_conv_v1_gpt2)
3. [Gragroo/psy_conv_v1_gpt3](https://huggingface.co/datasets/Gragroo/psy_conv_v1_gpt3)
4. [psycode1/psyset](https://huggingface.co/datasets/psycode1/psyset)
5. [Gragroo/psychology-question-answer_psygpt_format](https://huggingface.co/datasets/Gragroo/psychology-question-answer_psygpt_format)

---

## 🎯 Use Cases

- Fine-tuning mental health chatbots
- Training therapy assistant LLMs
- Building psychology Q&A systems
- Researching AI in mental health

---

## 📜 License

Check individual source datasets for their respective licenses.