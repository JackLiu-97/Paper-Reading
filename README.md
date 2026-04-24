# Paper Reading Repo

本仓库用于课题组共享论文、数据集、评价指标和个人阅读笔记。当前主线方向是**自动化评审**，相关方向包括 Agent、Prompt Engineering、Agent Memory、Self-Evolution、评审数据集、评价指标与经典基础论文。

## 目录导航

```text
.
|-- directions/                         # 按研究方向组织的论文清单和笔记
|   |-- automated-review/               # 自动化评审主方向
|   |   |-- README.md                   # 该方向论文清单
|   |   |-- notes/                      # 该方向阅读笔记
|   |-- agent-memory/                   # Agent 记忆机制
|   |   |-- README.md
|   |   |-- notes/
|   |-- self-evolution/                 # 自进化与自改进机制
|   |   |-- README.md
|   |   |-- notes/
|   |-- prompt-engineering-and-agent-origins/
|   |   |-- README.md
|   |   |-- notes/
|   |-- classic-must-read/              # 经典必读基础论文
|   |   |-- README.md
|   |   |-- notes/
|-- resources/
|   |-- datasets/                       # 跨方向可复用数据集索引
|   |-- metrics/                        # 跨方向可复用评价指标索引
```

## 使用方式

1. 添加论文：进入对应方向的 `README.md`，在论文表格中新增一行。
2. 添加笔记：在该方向的 `notes/<paper-slug>/<your-name>.md` 新建个人笔记。
3. 添加数据集：统一登记到 `resources/datasets/README.md`。
4. 添加评价指标：统一登记到 `resources/metrics/README.md`。

## 论文条目规范

每篇论文必须包含以下信息：

| 字段        | 说明                                                                                |
| ----------- | ----------------------------------------------------------------------------------- |
| Priority    | 推荐优先级，建议使用 `P0`、`P1`、`P2`                                               |
| Paper       | 论文标题                                                                            |
| Venue/Year  | 会议或期刊及年份                                                                    |
| Paper URL   | 论文地址，优先使用 arXiv、OpenReview、ACL Anthology、NeurIPS Proceedings 等稳定链接 |
| GitHub/Code | 官方 GitHub 优先；没有官方代码时写 `N/A`，可额外补充可信复现仓库并标注 `Unofficial` |
| Tags        | 主题标签，便于检索                                                                  |
| Notes       | 该论文的组内笔记目录                                                                |

推荐格式：

```md
| P1 | Paper Title | Venue 2026 | [Paper](https://...) | [GitHub](https://github.com/...) | automated-review, llm-as-judge | [notes](./notes/paper-title/) |
```

## 方向划分建议

- `automated-review`：审稿生成、评审质量预测、Meta-review、Rebuttal、Reviewer assignment、LLM-as-reviewer、评审一致性与可靠性。
- `agent-memory`：短期/长期记忆、检索增强记忆、情景记忆、工作流状态、记忆压缩与遗忘机制。
- `self-evolution`：模型、Agent 或系统通过反馈、反思、自动数据构造、工具调用和迭代优化实现自改进。
- `prompt-engineering-and-agent-origins`：Prompt Engineering、Chain-of-Thought、Tool Use、ReAct、早期 Agent 框架。
- `classic-must-read`：Transformer、RL、检索、生成模型、评估等跨方向基础论文。

## 协作原则

- 论文清单只放结构化信息，不写长篇读后感。
- 每个人的阅读笔记独立成文件，避免多人同时编辑同一个笔记文件（笔记可以是md文件，也可是做的ppt文件）。
- 大文件不要直接提交到 Git；优先放外部链接、网盘路径或数据卡片。确需提交时先讨论是否使用 Git LFS。
- 不确定是否官方代码时，不要写成 `Official`；先标注为 `Reference`、`Unofficial` 或 `N/A`。
