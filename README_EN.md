# LMKG-Samples

<p align="center">  <a href="./README.md">中文</a> | <a href="./README_EN.md">English</a></p>

This repository provides data samples associated with the manuscript **A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models**. The samples demonstrate how rail transit electric locomotive maintenance records can be organized into a Locomotive Maintenance Knowledge Graph (LMKG), including de-identified tabular samples, graph-relation JSON samples, and representative prompt templates.

This repository contains de-identified sample data only. It does not contain the complete enterprise maintenance dataset. The complete raw data include proprietary locomotive maintenance records, operational information, and project-related content, and therefore cannot be publicly released.

## Repository Structure

```text
.
├── README.md
├── README_EN.md
├── README.txt
├── PromptList.py
├── 行修更换、互换记录数据样例.xlsx
└── 图谱信息样例-50/
    ├── *.json
    └── ...
```

## Repository Contents

| Path | Description |
|---|---|
| [行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) | De-identified maintenance-record samples showing raw text, component, fault, and treatment fields. |
| [图谱信息样例-50/](./图谱信息样例-50/) | Fifty graph-relation JSON samples showing extracted nodes and relationships. |
| [PromptList.py](./PromptList.py) | Representative prompt templates for entity extraction, relation extraction, entity-chain optimization, and retrieval-grounded answer generation. |
| [README.txt](./README.txt) | Original short note in Chinese. |

## Prompt Templates

[PromptList.py](./PromptList.py) contains representative prompt templates used in the proposed method.

| Template | Function |
|---|---|
| `NER_PROMPT_TPL` | Extracts the component most likely to have a direct fault from a maintenance description. |
| `NETMOD_PROMPT_TPL` | Extracts the repair or treatment mode. |
| `ENTITY_EXTRACT_PROMPT` | Extracts the faulty component and corresponding fault from a question. |
| `SH_ENTITY_EXTRACT_PROMPT` | Extracts component, fault, test method, test result, and treatment entities. |
| `SH_RELATIONS_EXTRACT_PROMPT` | Extracts relations among a given entity list. |
| `ENTITY_CHAIN_OPTIMIZATION_PROMPT` | Selects question-relevant information from graph entity chains. |
| `RAG_ANSWER_GENERATE_PROMPT` | Generates maintenance question-answering outputs using retrieved graph evidence. |

These templates document part of the prompt design used for LLM-KG collaborative extraction and topology-constrained retrieval-augmented reasoning. They are not a complete production implementation.

## Data Access

This repository contains de-identified sample data only. The full raw data include enterprise locomotive maintenance records, operational information, and project-related content and cannot be publicly released. Additional de-identified supporting data may be requested from the corresponding author under reasonable conditions and with permission from the data owner.

## Citation

If these samples are useful for your research, please cite the associated manuscript:

> A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models.
