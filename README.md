# LMKG-Samples

<p align="center">  <a href="#-中文说明">中文</a> | <a href="./README_EN.md">English</a></p>

本仓库为论文 **A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models** 提供配套数据样例。样例展示了轨道交通电力机车检修记录如何被组织为机车检修知识图谱（Locomotive Maintenance Knowledge Graph, LMKG），内容包括去标识化表格样例、图谱关系 JSON 样例以及代表性提示词模板。

本仓库仅公开论文配套的去标识化样例数据，不包含完整企业检修数据集。完整原始数据涉及企业机车检修记录、运维信息和项目相关内容，受数据所有方限制，不能公开发布。

## 仓库结构

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

## 文件说明

| 路径 | 内容 |
|---|---|
| [行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) | 去标识化后的检修记录表格样例，展示原始文本、部件、故障和处理字段。 |
| [图谱信息样例-50/](./图谱信息样例-50/) | 50 个图谱关系 JSON 样例，用于展示从检修记录中抽取得到的节点和关系。 |
| [PromptList.py](./PromptList.py) | 代表性提示词模板，覆盖实体抽取、关系抽取、实体链优化和基于检索证据的回答生成。 |
| [README.txt](./README.txt) | 原始简要说明。 |

## 提示词模板

[PromptList.py](./PromptList.py) 提供了论文方法中使用的代表性提示词模板：

| 模板名称 | 功能 |
|---|---|
| `NER_PROMPT_TPL` | 从检修描述中抽取最可能直接发生故障的部件。 |
| `NETMOD_PROMPT_TPL` | 抽取故障修复方式。 |
| `ENTITY_EXTRACT_PROMPT` | 从问题中抽取部件名称及对应故障名称。 |
| `SH_ENTITY_EXTRACT_PROMPT` | 抽取部件名称、故障、实验方法、实验结果和处理方法等实体。 |
| `SH_RELATIONS_EXTRACT_PROMPT` | 根据实体列表抽取实体间关系。 |
| `ENTITY_CHAIN_OPTIMIZATION_PROMPT` | 从图谱实体链中筛选与问题意图相关的信息。 |
| `RAG_ANSWER_GENERATE_PROMPT` | 基于检索到的图谱信息生成检修问答回答。 |

这些模板用于说明 LLM-KG 协同抽取和拓扑约束检索增强推理中的提示词设计，不代表完整工程实现。

## 数据访问说明

本仓库仅包含去标识化后的样例数据。完整原始数据包含企业机车检修记录、运维信息和项目相关内容，不能公开发布。更多去标识化支持数据可在数据所有方许可下向论文通讯作者合理请求。

## 引用

如果本仓库中的样例数据对您的研究有帮助，请引用关联论文：

> A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models.
