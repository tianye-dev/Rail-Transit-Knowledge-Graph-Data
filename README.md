# 轨道交通知识图谱数据

<p align="center">  <a href="#-中文说明">中文</a> | <a href="./README_EN.md">English</a></p>

本仓库为论文 **A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models** 提供配套数据。

## 仓库结构

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

## 文件说明

| 路径 | 内容 |
|---|---|
| [行修更换、互换记录数据.xlsx](./行修更换、互换记录数据.xlsx) | 去标识化后的检修记录表格样例，展示原始文本、部件、故障和处理字段。 |
| [图谱信息/](./图谱信息/) | 图谱关系 JSON。 |
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
