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


## Results
### Company profile
| Company Name | Website | Confidence |
|----------|----------|----------|
| Anxun Information Technology Co,. Ltd,.  | I-soon.net | 1.0  |

### User profiles 
| username            | name         | real_name     | real_name_confidence | company                           | website        | position         | position_confidence | message_count | conversation_partners             |
|:--------------------|:-------------|:--------------|----------------------:|:----------------------------------|:---------------|:------------------|----------------------:|---------------:|:----------------------------------|
| SWEET5683yao        | Brother Qing | Chen Qing     | 0.95                  | Anxun Information Technology C... | www.I-soon.net | Project Manager   | 0.75                  | 35             | wxid_7p054rmzkhqf21               |
| Shutd0wn            | Mr. Wu       | Wu Haibo      | 0.85                  | Anxun Information Technology C... | www.I-soon.net | General Manager   | 0.75                  | 3675           | lengmo, wxid_xusilpfkh31g21       |
| adpw90              | Mr. Zheng    | Zheng Wei     | 0.85                  | Anxun Information Technology C... | www.I-soon.net | Team Lead         | 0.75                  | 235            | wxid_7p054rmzkhqf21               |
| gzp1991101          | Mr. Gong     | Gong Tao      | 0.85                  | Anxun Information Technology C... | www.I-soon.net | General Manager   | 0.90                  | 603            | wxid_7p054rmzkhqf21, wxid_mgh2... |
| lengmo              | Mr. C        | [parse error] | 0.00                  | Anxun Information Technology C... | www.I-soon.net | [parse error]     | 0.00                  | 4981           | Shutd0wn, just910420, wxid_539... |
| nullroot            | Mr. Zhou     | [parse error] | 0.00                  | Anxun Information Technology C... | www.I-soon.net | [parse error]     | 0.00                  | 103            | tianyi-0608, wei592628            |
| wei592628           | Mr. Wei      | [parse error] | 0.00                  | Anxun Information Technology C... | www.I-soon.net | [parse error]     | 0.00                  | 87             | nullroot                          |
| wxid_5390224027312  | Mr. Wang     | [parse error] | 0.00                  | Anxun Information Technology C... | www.I-soon.net | [parse error]     | 0.00                  | 1409           | dujijiyiqxx, lengmo, qq7826346... |
| wxid_70w3p1jin84k22 | Sister Qian  | Xu Qian       | 1.00                  | Anxun Information Technology C... | www.-soon.net | Training Manager  | 0.90                  | 523            | wxid_5390224027312, wxid_nv9bv... |
| wxid_7p054rmzkhqf21 | Mr. Lu       | Lu Yongjun    | 0.95                  | Anxun Information Technology C... | www.I-soon.net | President         | 0.85                  | 894            | SWEET5683yao, adpw90, gzp19911... |

### Financial Structures - Salaries

#### Salary History (Employee: `just910420`)

| Year | Company | Base Salary (CNY, Before Tax) | Bonus/Extras                                   | Notes                      |
|------|---------|-------------------------------|------------------------------------------------|----------------------------|
| 2017 | Anxun   | 7,500                         | –                                              | –                          |
| 2018 | Anxun   | 8,500                         | –                                              | –                          |
| 2019 | Anxun   | 10,200                        | 2.5 months year-end bonus                      | –                          |
| 2020 | Anxun   | 11,700                        | 200 CNY confidentiality fee                    | Promotion to supervisor    |

---

