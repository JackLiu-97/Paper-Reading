# Self-Evolution

本方向收录自进化、自改进和自优化相关论文。重点关注模型或 Agent 如何利用反馈、反思、自动数据构造、环境交互、工具调用、记忆更新和迭代训练来持续提升能力。

该方向和自动化评审的关系主要包括：让评审 Agent 基于历史评审反馈进行自我改进，自动构造高质量评审训练数据，迭代优化审稿策略，以及在多轮评审流程中形成可复用的经验和偏好。


## 论文清单

| Priority | Paper | Venue/Year | Paper URL | GitHub/Code | Tags | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| P0 | Amory: Building Coherent Narrative-Driven Agent Memory through Agentic Reasoning | EACL 2026 | [Paper](https://aclanthology.org/2026.eacl-long.183/) | N/A | agent-memory, narrative-memory, agentic-reasoning, self-evolution, unread |  |
| P0 | An Efficient Context-Dependent Memory Framework for LLM-Centric Agents | NAACL Industry Track 2025 | [Paper](https://aclanthology.org/2025.naacl-industry.80/) | N/A | agent-memory, context-dependent-memory, llm-agent, self-evolution, unread |  |
| P0 | ASI-Evolve: AI Accelerates AI | arXiv 2026 | [Paper](https://arxiv.org/abs/2603.29640) | [GitHub](https://github.com/GAIR-NLP/ASI-Evolve) | ai-accelerates-ai, code-evolution, self-evolution, automated-research, unread |  |
| P0 | Assimilation and Accommodation: Task-Adaptive Hierarchical Abstraction for Solving Web Tasks | Findings ACL 2025 | [Paper](https://aclanthology.org/2025.findings-acl.720/) | [GitHub](https://github.com/Xinyu-Pang/A2) | web-agent, hierarchical-abstraction, task-adaptation, self-evolution, unread |  |
| P0 | Experiential Reflective Learning for Self-Improving LLM Agents | ICLR 2026 MemAgents Workshop | [Paper](https://openreview.net/forum?id=hQgSl6kj1W) | N/A | self-improving-agent, experiential-learning, reflection, memory, unread |  |
| P0 | M2PA: A Multi-Memory Planning Agent for Open Worlds Inspired by Cognitive Theory | Findings ACL 2025 | [Paper](https://aclanthology.org/2025.findings-acl.1191/) | N/A | multi-memory-agent, planning, open-world-agent, cognitive-theory, unread |  |
| P0 | Memory-Augmented Large Language Model-Based Agent with Cross-Task Experience Learning | ICLR 2026 Submission | [Paper](https://openreview.net/forum?id=0GMt2OWeCb) | N/A | memory-augmented-agent, cross-task-experience, experience-learning, read |  |
| P0 | ProcMEM: Learning Reusable Procedural Memory from Experience via Non-Parametric PPO for LLM Agents | arXiv 2026 | [Paper](https://arxiv.org/abs/2602.01869) | N/A | procedural-memory, experience-learning, non-parametric-ppo, llm-agent, read |  |
| P0 | R2D2: Remembering, Replaying and Dynamic Decision Making with a Reflective Agentic Memory | ACL 2025 | [Paper](https://aclanthology.org/2025.acl-long.1464/) | N/A | reflective-memory, replay, dynamic-decision-making, agentic-memory, unread |  |
| P0 | Self-Refine: Iterative Refinement with Self-Feedback | NeurIPS 2023 | [Paper](https://arxiv.org/abs/2303.17651) | [GitHub](https://github.com/madaan/self-refine) | self-refine, self-feedback, iterative-refinement, self-improvement, unread |  |
| P0 | Trajectory-Informed Memory Generation for Self-Improving Agent Systems | arXiv 2026 | [Paper](https://arxiv.org/abs/2603.10600) | [GitHub](https://github.com/cuga-project/cuga-agent) | trajectory-memory, self-improving-agent, memory-generation, agent-system, read |  |
| P0 | UI-Mem: Self-Evolving Experience Memory for Online Reinforcement Learning in Mobile GUI Agents | arXiv 2026 | [Paper](https://arxiv.org/abs/2602.05832) | N/A | gui-agent, experience-memory, online-reinforcement-learning, self-evolution, unread |  |

## 可维护主题

- Self-reflection：基于错误分析、反思或 critique 改进后续输出。
- Self-training：利用模型生成数据、伪标签或偏好数据进行迭代训练。
- Agent evolution：Agent 在工具使用、规划、记忆和任务执行中的长期自改进。
- Automated data construction：自动生成、过滤和增强训练或评测数据。
- Feedback-driven optimization：利用人类反馈、环境反馈或模型反馈更新策略。
- Evaluation：评估自进化过程是否真实提升能力，而不是过拟合局部任务或评测集。
