# Data Samples for Rail Transit Electric Locomotive Maintenance Knowledge Graph Construction

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

## Data Overview

| Item | Size |
|---|---:|
| Worksheet in the tabular sample | 1 |
| Rows in the tabular sample | 4,887 |
| Columns in the tabular sample | 15 |
| Graph-relation JSON files | 50 |
| Relationship edges in the graph samples | 418 |
| Relationship edges per JSON file | 4--20 |

Node labels include `部件名称`, `故障`, `处理方法`, `实验方法`, and `实验结果`. Relation names include `发生`, `需要`, `产生`, `采用`, and `验证`.

## Tabular Sample Fields

[行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) contains representative maintenance records before graph construction. The main fields are listed below.

| Column | Meaning |
|---|---|
| 更换及预防标签序号 | Sample record identifier. |
| 季 | Season of the record. |
| 故障内容 | Original fault-description text used as the main input for entity and relation extraction. |
| 处理方法 | Original maintenance action or treatment-process description. |
| 时间起点对应修程（待C1~C4信息更新） | Maintenance grade or time-granularity information. |
| 子系统名称 | Vehicle subsystem related to the fault. |
| 部件名称 | Standardized component name. |
| 一级配件名称 | First-level part name. |
| 二级配件名称 | Second-level part name. |
| 部件一级编号 | First-level component code. |
| 部件二级编号 | Second-level component code. |
| 配件编号 | Part code. |
| 故障标签 | Fault or treatment-category label. |
| 需进一步讨论 | Expert review flag. |
| 处理方法包含关键词 | Keywords contained in the maintenance action. |

## Graph Relation Format

The JSON files in [图谱信息样例-50/](./图谱信息样例-50/) use a consistent structure. Each file contains a `relationships` array, and each relationship consists of a start node, an end node, and a relation name:

```json
{
  "relationships": [
    {
      "startNode": {
        "label": "部件名称",
        "name": "大闸"
      },
      "endNode": {
        "label": "故障",
        "name": "不缓解(大闸)"
      },
      "name": "发生"
    }
  ]
}
```

This structure can be mapped directly to nodes and edges in a graph database. `startNode.label` and `endNode.label` define node types, `startNode.name` and `endNode.name` define node names, and `name` defines the relation type.

## Graph Schema

The samples follow the `component-fault-treatment-test-result` causal chain described in the manuscript.

### Node Labels

| Label | Meaning |
|---|---|
| 部件名称 | Component |
| 故障 | Fault |
| 处理方法 | Treatment |
| 实验方法 | Test method |
| 实验结果 | Test result |

### Relation Types

| Relation | Semantic Direction | Manuscript-Level Relation |
|---|---|---|
| 发生 | Component -> Fault | Component_HasFault |
| 需要 | Fault -> Test method | Fault_TestedBy |
| 产生 | Test method -> Test result | Test_YieldsResult |
| 采用 | Fault -> Treatment | Fault_TreatedBy |
| 验证 | Treatment -> Test method | Treatment_TestedBy |

### Relation Counts in the Samples

| Relation | Count |
|---|---:|
| 发生 | 86 |
| 需要 | 73 |
| 产生 | 111 |
| 采用 | 88 |
| 验证 | 60 |
| **Total** | **418** |

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

## Usage

1. Use [行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) to understand the structure of de-identified maintenance records.
2. Refer to [PromptList.py](./PromptList.py) for prompt templates used in entity extraction, relation extraction, and graph-evidence-grounded answer generation.
3. Parse the `relationships` array in the JSON files under [图谱信息样例-50/](./图谱信息样例-50/) into graph database nodes and edges.
4. Build a local LMKG following the `Component -> Fault -> Treatment -> Test method -> Test result` organization.

## Data Access

This repository contains de-identified sample data only. The full raw data include enterprise locomotive maintenance records, operational information, and project-related content and cannot be publicly released. Additional de-identified supporting data may be requested from the corresponding author under reasonable conditions and with permission from the data owner.

## Citation

If these samples are useful for your research, please cite the associated manuscript:

> A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models.
