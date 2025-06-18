# AI-Soon


![Logo](https://i.gzn.jp/img/2024/02/26/china-hacking-leak-documents-isoon/00.png)


## Overview

This Jupyter Notebook (`main.ipynb`) presents AI-Soon, a modular end-to-end data analysis pipeline tailored for handling compressed datasets containing diverse file formats for the I-Soon leak or generic use (e.g., `.md`, `.txt`, `.log`, `.png`). It performs a series of structured operations including extraction, parsing, large language model (LLM)-based classification, multilingual translation, and domain-specific analysis. This pipeline is applicable in cybersecurity, digital forensics, and business intelligence domains.

## Built with
- Python Version 3.11.8
- JupyterLab Version 3.6.8

## Requirements

Install dependencies using:

```bash
pip install requirements.txt
```

## Ollama Models Utilized
```bash
ollama pull gemma3:27b
ollama pull llama3.1:8b
ollama pull mxbai-embed-large
```

## 1. **Raw Data Extraction From ZIP**
- This uncompresses the zip file and sorts all the data generically based on the identified extensions, creating a convenient setup for further analysis.

## 2. **Data Parsing**
- Creates a dataframe with full file paths.
- Applies format-specific parsing:
  - Markdown (`.md`) → CSV conversations.
  - Text (`.txt`) and log files (`.log`) → structured tabular form.
  - PNG images (`.png`) → processed via OCR into CSV. (image parsing can be obtained from a .py file located outside

### 1. **Large Language Model Classification**
- Uses LLMs (e.g., `Gemma-3 27B`) to classify content within `.md` files.
- Cross-references files to discover interdependencies or related content.

## 3. **Data Translation Pipeline**
- To effectively run LLMs with Threadpool executor, utilize the following:
    ```bash
    export OLLAMA_NUM_PARALLEL=8             # Run 8 translations in parallel - depending on the Number of GPUs available
    export OLLAMA_SCHED_SPREAD=1             # Distribute load across CPU cores
    export OLLAMA_KEEP_ALIVE="1h"            # Keep model loaded in memory
    export OLLAMA_FLASH_ATTENTION=true       # Use faster GPU attention (if supported)
    ```
- Converts multilingual content into English using LLMs and OCR.
- Supports both conversational and OCR output translation.

## 4. **User Analysis**
- Associates usernames with aliases or mentioned individuals.
- Identifies organizations to enrich user profiles.
- Constructs user profiles based on:
  - Company affiliations
  - Communication volume
  - Interpersonal communication networks

## 5. **Financial Infrastructure Analysis**
- Includes rule-based financial term extraction.
- Performs salary and compensation pattern analysis.
- Attempts Retrieval-Augmented Generation (RAG) for financial document insights.

---

