# Rail Transit Knowledge Graph Data

<p align="center">  <a href="./README.md">中文</a> | <a href="./README_EN.md">English</a></p>

This repository provides supporting data for the paper **A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models**.

## Repository Structure

```text
.
├── README.md
├── README_EN.md
├── PromptList.py
├── 行修更换、互换记录数据.xlsx
└── 图谱信息/
    ├── *.json
    └── ...
```

## File Description

| Path | Content |
|---|---|
| [行修更换、互换记录数据.xlsx](./行修更换、互换记录数据.xlsx) | De-identified maintenance-record table samples showing raw text, component, fault, and treatment fields. |
| [图谱信息/](./图谱信息/) | Knowledge graph relationship JSON files. |
| [PromptList.py](./PromptList.py) | Representative prompt templates covering entity extraction, relation extraction, entity-chain optimization, and retrieval-evidence-based answer generation. |
| [README.txt](./README.txt) | Original brief description. |

## Prompt Templates

[PromptList.py](./PromptList.py) provides representative prompt templates used in the paper's method:

| Template Name | Function |
|---|---|
| `NER_PROMPT_TPL` | Extracts the component most likely to have a direct fault from a maintenance description. |
| `NETMOD_PROMPT_TPL` | Extracts the fault repair method. |
| `ENTITY_EXTRACT_PROMPT` | Extracts the component name and corresponding fault name from a question. |
| `SH_ENTITY_EXTRACT_PROMPT` | Extracts entities such as component name, fault, test method, test result, and treatment method. |
| `SH_RELATIONS_EXTRACT_PROMPT` | Extracts relationships among entities according to an entity list. |
| `ENTITY_CHAIN_OPTIMIZATION_PROMPT` | Selects information related to the question intent from graph entity chains. |
| `RAG_ANSWER_GENERATE_PROMPT` | Generates maintenance question-answering responses based on retrieved graph information. |
