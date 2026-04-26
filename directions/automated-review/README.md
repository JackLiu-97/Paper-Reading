# Automated Review

本方向是课题组当前主线，覆盖自动化评审及其上下游任务，包括审稿生成、评审质量评估、Meta-review、Rebuttal、Reviewer assignment、LLM-as-reviewer、评审一致性与可靠性分析。


## 论文清单

| Priority | Paper | Venue/Year | Paper URL | GitHub/Code | Tags | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| P0 | Agent Reviewers: Domain-specific Multimodal Agents with Shared Memory for Paper Review | ICML 2025 | [Paper](https://proceedings.mlr.press/v267/lu25p.html) | [GitHub (coming soon)](https://github.com/AReviewers/AgentReviewers) | automated-review, llm-as-reviewer, multi-agent, multimodal, shared-memory, unread |  |
| P0 | AgentReview: Exploring Peer Review Dynamics with LLM Agents | EMNLP 2024 | [Paper](https://aclanthology.org/2024.emnlp-main.70/) | [GitHub](https://github.com/Ahren09/AgentReview) | automated-review, peer-review-simulation, llm-agents, read |  |
| P0 | AgentRxiv: Towards Collaborative Autonomous Research | arXiv 2025 | [Paper](https://arxiv.org/abs/2503.18102) | [GitHub](https://github.com/SamuelSchmidgall/AgentLaboratory) | automated-research, collaborative-research, agent-lab, read |  |
| P0 | Automated Peer Reviewing in Paper SEA: Standardization, Evaluation, and Analysis | EMNLP 2024 | [Paper](https://arxiv.org/abs/2407.12857) | [GitHub](https://github.com/ecnu-sea/SEA) | automated-review, review-generation, review-evaluation, read |  |
| P0 | AutoRev: Multi-Modal Graph Retrieval for Automated Peer-Review Generation | arXiv 2025 | [Paper](https://arxiv.org/abs/2505.14376) | N/A | automated-review, review-generation, multimodal-rag, graph-retrieval, unread |  |
| P0 | CSPaper Review: Fast, Rubric-Faithful Conference Feedback | INLG 2025 | [Paper](https://aclanthology.org/2025.inlg-demos.2/) | N/A | automated-review, rubric-guided-review, conference-feedback, read |  |
| P0 | DeepReview: Improving LLM-based Paper Review with Human-like Deep Thinking Process | ACL 2025 | [Paper](https://aclanthology.org/2025.acl-long.1420/) | [GitHub](https://github.com/zhu-minjun/Researcher) | automated-review, review-generation, deep-thinking, read |  |
| P0 | DeepReviewer 2.0: A Traceable Agentic System for Auditable Scientific Peer Review | arXiv 2026 | [Paper](https://arxiv.org/abs/2604.09590) | [GitHub](https://github.com/ResearAI/DeepReviewer-v2) | automated-review, agentic-review, traceability, auditable-review, unread |  |
| P0 | OpenNovelty: An LLM-powered Agentic System for Verifiable Scholarly Novelty Assessment | arXiv 2026 | [Paper](https://arxiv.org/abs/2601.01576) | [GitHub](https://github.com/january-blue/OpenNovelty) | novelty-assessment, scholarly-review, retrieval, read |  |
| P0 | Reviewer2: Optimizing Review Generation Through Prompt Generation | arXiv 2024 | [Paper](https://arxiv.org/abs/2402.10886) | [GitHub](https://github.com/ZhaolinGao/Reviewer2) | automated-review, review-generation, prompt-generation, read |  |
| P0 | ReviewEval: An Evaluation Framework for AI-Generated Reviews | Findings EMNLP 2025 | [Paper](https://aclanthology.org/2025.findings-emnlp.1120/) | N/A | automated-review, review-evaluation, review-agent, unread |  |
| P0 | ReviewGrounder: Improving Review Substantiveness with Rubric-Guided, Tool-Integrated Agents | arXiv 2026 | [Paper](https://arxiv.org/abs/2604.14261) | [GitHub](https://github.com/EigenTom/ReviewGrounder) | automated-review, rubric-guided-review, tool-integrated-agent, unread |  |
| P0 | ReviewRL: Towards Automated Scientific Review with RL | EMNLP 2025 | [Paper](https://aclanthology.org/2025.emnlp-main.857/) | N/A | automated-review, reinforcement-learning, scientific-review, read |  |
| P0 | ScholarPeer: A Context-Aware Multi-Agent Framework for Automated Peer Review | arXiv 2026 | [Paper](https://arxiv.org/abs/2601.22638) | N/A | automated-review, multi-agent, context-aware-review, literature-search, read |  |
| P0 | Scoring, Reasoning, and Selecting the Best! Ensembling Large Language Models via a Peer-Review Process | arXiv 2025 | [Paper](https://arxiv.org/abs/2512.23213) | N/A | llm-ensemble, peer-review-process, llm-as-judge, unread |  |
| P0 | The AI Scientist-v2: Workshop-Level Automated Scientific Discovery via Agentic Tree Search | arXiv 2025 | [Paper](https://arxiv.org/abs/2504.08066) | [GitHub](https://github.com/SakanaAI/AI-Scientist-v2) | automated-scientific-discovery, agentic-tree-search, ai-scientist, unread |  |

## 可维护主题

- Review generation：根据论文生成结构化评审意见。
- Review quality estimation：预测评审是否有帮助、是否具体、是否可靠。
- Meta-review generation：综合多份评审和作者回复形成最终意见。
- Rebuttal analysis：建模作者回复对最终决策和审稿意见的影响。
- Reviewer assignment：评审人匹配、利益冲突、专业度与负载均衡。
- Evaluation：自动化评审的正确性、覆盖度、可操作性、公平性和一致性。
