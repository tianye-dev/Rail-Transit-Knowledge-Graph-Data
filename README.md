# 轨道交通电力机车检修知识图谱数据样例

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

## 数据概览

| 数据项 | 规模 |
|---|---:|
| 表格样例工作表 | 1 |
| 表格样例行数 | 4,887 |
| 表格样例列数 | 15 |
| 图谱关系 JSON 文件 | 50 |
| 图谱样例关系边 | 418 |
| 单个 JSON 文件关系边数量 | 4--20 |

节点类型包括 `部件名称`、`故障`、`处理方法`、`实验方法` 和 `实验结果`。关系类型包括 `发生`、`需要`、`产生`、`采用` 和 `验证`。

## 表格样例字段

[行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) 展示了图谱构建前的检修记录样例。主要字段如下：

| 字段 | 含义 |
|---|---|
| 更换及预防标签序号 | 样例记录编号。 |
| 季 | 记录所属季节。 |
| 故障内容 | 原始故障描述文本，是实体和关系抽取的主要输入。 |
| 处理方法 | 原始检修处理过程或维修措施描述。 |
| 时间起点对应修程（待C1~C4信息更新） | 检修记录对应的修程或时间粒度信息。 |
| 子系统名称 | 故障相关的车辆子系统。 |
| 部件名称 | 标准化后的部件名称。 |
| 一级配件名称 | 一级配件名称。 |
| 二级配件名称 | 二级配件名称。 |
| 部件一级编号 | 部件一级编码。 |
| 部件二级编号 | 部件二级编码。 |
| 配件编号 | 配件编码。 |
| 故障标签 | 故障处理类别标签。 |
| 需进一步讨论 | 专家复核标记。 |
| 处理方法包含关键词 | 处理方法中的关键词标签。 |

## 图谱关系格式

[图谱信息样例-50/](./图谱信息样例-50/) 中的 JSON 文件采用统一结构。每个文件包含一个 `relationships` 数组，每条关系由起始节点、终止节点和关系名称组成：

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

该格式可直接映射到图数据库中的节点和边。其中，`startNode.label` 与 `endNode.label` 表示节点类型，`startNode.name` 与 `endNode.name` 表示节点名称，`name` 表示关系类型。

## 图谱 Schema

样例数据围绕论文中的 `component-fault-treatment-test-result` 因果链组织。

### 节点类型

| 标签 | 英文含义 |
|---|---|
| 部件名称 | Component |
| 故障 | Fault |
| 处理方法 | Treatment |
| 实验方法 | Test method |
| 实验结果 | Test result |

### 关系类型

| 关系名 | 语义方向 | 论文中的关系定义 |
|---|---|---|
| 发生 | 部件名称 -> 故障 | Component_HasFault |
| 需要 | 故障 -> 实验方法 | Fault_TestedBy |
| 产生 | 实验方法 -> 实验结果 | Test_YieldsResult |
| 采用 | 故障 -> 处理方法 | Fault_TreatedBy |
| 验证 | 处理方法 -> 实验方法 | Treatment_TestedBy |

### 样例关系数量

| 关系名 | 数量 |
|---|---:|
| 发生 | 86 |
| 需要 | 73 |
| 产生 | 111 |
| 采用 | 88 |
| 验证 | 60 |
| **合计** | **418** |

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

## 使用方式

1. 通过 [行修更换、互换记录数据样例.xlsx](./行修更换、互换记录数据样例.xlsx) 了解去标识化检修记录的表格结构。
2. 参考 [PromptList.py](./PromptList.py) 中的提示词模板，理解实体抽取、关系抽取和图谱证据生成回答的基本形式。
3. 解析 [图谱信息样例-50/](./图谱信息样例-50/) 中 JSON 文件的 `relationships` 数组，构建图数据库节点和边。
4. 按照 `部件名称 -> 故障 -> 处理方法 -> 实验方法 -> 实验结果` 的路径组织方式构建局部 LMKG。

## 数据访问说明

本仓库仅包含去标识化后的样例数据。完整原始数据包含企业机车检修记录、运维信息和项目相关内容，不能公开发布。更多去标识化支持数据可在数据所有方许可下向论文通讯作者合理请求。

## 引用

如果本仓库中的样例数据对您的研究有帮助，请引用关联论文：

> A Graph-Topology-Constrained Retrieval-Augmented Reasoning Framework for Rail Transit Locomotive Maintenance with Large Language Models.
