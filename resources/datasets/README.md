# Datasets

这里整理自动化评审相关数据集。表格中的 `Storage/Access` 统一预留为百度网盘链接，后续由维护者补充。

## 数据集总览

| Dataset | Task | Source | License | Scale | Storage/Access | Owner | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| DeepReview-13K | LLM 论文评审训练；结构化审稿推理；meta-review 生成；accept/reject 决策建模 | [ACL 2025 paper](https://aclanthology.org/2025.acl-long.1420/); [Hugging Face dataset card](https://huggingface.co/datasets/WestlakeNLP/DeepReview-13K) | DeepReviewer License | 13,378 samples；平均约 10,178 tokens/sample；公开文件包含 `train.csv`、`test_2024.csv`、`test_2025.csv` | [百度网盘 DeepReview-13K.zip](https://pan.baidu.com/s/1gwQLaHI9qTa7MN5meGmS2g?pwd=y5cu)，提取码：`y5cu` | WestlakeNLP / DeepReview authors | 数据来自 OpenReview ICLR 与 arXiv，包含论文内容和多阶段审稿推理。许可明确禁止将数据或由其训练的模型用于正式同行评审。 |
| NLPeer | 同行评审计算研究；review score prediction；guided skimming；pragmatic label prediction；跨领域评审分析 | [ACL 2023 paper](https://aclanthology.org/2023.acl-long.277/); [official GitHub](https://github.com/UKPLab/nlpeer); [NLPeer v1 archive](https://tudatalib.ulb.tu-darmstadt.de/handle/tudatalib/3618); [NLPeer v2 archive](https://tudatalib.ulb.tu-darmstadt.de/handle/tudatalib/4459) | 整体为 CC BY-NC 4.0；不同子集可能有来源级许可；代码为 Apache-2.0 | v1: 5,672 papers, 11,515 reviews；v2 继续加入 ARR-EMNLP-2024、EMNLP-2023、PLOS 2019-2024、eLife 2023-2024 | [百度网盘 NLPeer.zip](https://pan.baidu.com/s/1R2zS6faazXtJx_dwRUmZfQ?pwd=9axm)，提取码：`9axm` | UKP Lab / TU Darmstadt | 多领域、伦理来源、统一格式的同行评审数据集，包含论文草稿、camera-ready 版本、评审、元数据、解析后的结构化论文表示和版本信息。 |
| PeerRead | acceptance prediction；review aspect score prediction；同行评审过程分析；论文-评审建模 | [NAACL 2018 paper](https://aclanthology.org/N18-1149/); [official GitHub](https://github.com/allenai/PeerRead); [Hugging Face dataset card](https://huggingface.co/datasets/allenai/peer_read) | 未统一明确；部分来源受许可限制，需逐源核查 | 14,784 paper drafts；10,770 textual reviews；覆盖 CoNLL 2016、ACL 2017、ICLR 2017、NIPS 2013-2017、arXiv 2007-2017 | [百度网盘 PeerRead.zip](https://pan.baidu.com/s/1-DI3wMisefayycLX7wmsKA?pwd=hif6)，提取码：`hif6` | AllenAI / PeerRead authors | 早期公开同行评审数据集，包含论文草稿、接收/拒绝或可能拒绝标签，以及部分论文对应的专家评审文本和 aspect scores。 |
| SEA_data | 自动化论文评审 SFT；评审标准化；评审生成；review JSON 处理；mismatch score 分析 | [EMNLP 2024 paper](https://aclanthology.org/2024.findings-emnlp.595/); [project page](https://ecnu-sea.github.io/); [Hugging Face dataset card](https://huggingface.co/datasets/ECNU-SEA/SEA_data) | Apache-2.0 | 公开 HF 数据为 9,021 rows，来自 NeurIPS 2023 与 ICLR 2024；论文实验总计使用 12,296 papers 与 47,602 reviews | [百度网盘 SEA](https://pan.baidu.com/s/18R2t-5-cA9gsz3DmIa_gkg?pwd=mvjj)，提取码：`mvjj` | ECNU-SEA | 公开数据包含原始 PDF、Nougat 解析 MMD、原始评审文本和结构化 review JSON。适合直接构造 paper-to-review 与 review-standardization 任务。 |
| NIPS/NeurIPS Review Archive | 历年机器学习会议评审分析；review-only 数据统计；评分、置信度和评审文本建模 | 自整理；来源为 NIPS/NeurIPS 历年公开评审数据 | 待核查；按原始公开评审来源约束使用 | NIPS/NeurIPS 2016-2025 历年评审数据；仅包含评审相关数据，不包含论文 PDF | [百度网盘 NIPS.zip](https://pan.baidu.com/s/1tysS9O77y2UpLat1IF7dfg?pwd=5bit)，提取码：`5bit` | 课题组自整理 | 包含三类形态：原始评审数据、统一结构化后的历年评审数据、LLM 抽取的优点/缺点/重要性/问题-作者回复 rebuttal 对及满意度。 |
| ICLR Review Archive | 历年 ICLR 评审分析；OpenReview review-only 数据建模；评分、置信度和决策趋势分析 | 自整理；来源为 ICLR / OpenReview 历年公开评审数据 | 待核查；按 OpenReview 与原始公开数据约束使用 | ICLR 2017-2026 历年评审数据；仅包含评审相关数据，不包含论文 PDF | [百度网盘 ICLR.zip](https://pan.baidu.com/s/1asoXRCrNxSzIEHXbqTCn4A?pwd=kgyg)，提取码：`kgyg` | 课题组自整理 | 包含三类形态：原始评审数据、统一结构化后的历年评审数据、LLM 抽取的优点/缺点/重要性/问题-作者回复 rebuttal 对及满意度。 |

## DeepReview-13K

### 数据简介

DeepReview-13K 是 DeepReview 工作发布的论文评审训练数据集，目标是让模型学习更接近专家审稿的多阶段分析流程。数据卡说明该数据集包含 13,378 条高质量样本，每条样本对应一个详细论文评审过程，平均长度约 10,178 tokens，平均评分约 5.18，accept rate 约 33.24%。

### 数据来源与年份

| 组成 | 年份/划分 | 说明 |
| --- | --- | --- |
| OpenReview ICLR papers | 公开数据卡只明确来源为 ICLR，不给出更细年份分布 | 用于构建真实论文内容、评分和决策相关信息。 |
| arXiv papers | 公开数据卡只明确来源为 arXiv，不给出更细年份分布 | 用于补充论文内容和领域覆盖。 |
| `train.csv` | 未在数据卡中细分年份 | 主训练文件，文件体积约 5.56 GB。 |
| `test_2024.csv` | 2024 | 测试集文件之一，文件体积约 133 MB。 |
| `test_2025.csv` | 2025 | 测试集文件之一，文件体积约 129 MB。 |

更细的会议年份、arXiv 年份和领域分布，公开数据卡没有直接列出，需要下载后按字段统计。

### 字段构成

每条样本主要包含：

- 原始论文内容：真实研究论文的文本内容。
- Novelty Verification：问题、论文分析、相关文献检索结果，用于判断创新性。
- Multi-dimensional Review：从多个专家视角模拟的多维度评审。
- Reliability Verification：方法、实验和综合分析，用于定位弱点、收集证据和生成建议。
- Meta-Reviewer Comment：整合多阶段分析后的 meta-review。
- Overall Rating：1-10 的整体评分。
- Decision：接收或拒绝决策。

### 适用任务

- 训练自动化审稿模型。
- 研究结构化审稿推理过程。
- 构建 reward model 或偏好学习数据。
- 分析 LLM 生成评审中的证据链、可靠性和决策一致性。

### 使用注意

- 数据集是 gated dataset，需要同意 Hugging Face 数据卡中的使用条款。
- DeepReviewer License 明确要求：数据集以及基于它训练、分发或复现的模型不能用于正式同行评审。
- 数据中包含 LLM 生成的结构化推理步骤，可能存在不一致、偏差或幻觉，需要人工抽查。

## NLPeer

### 数据简介

NLPeer 是面向同行评审计算研究的统一资源。v1 数据集覆盖 5 个来源，共 5,672 篇论文和 11,515 份评审；v2 在 v1 基础上继续扩展 ARR-EMNLP-2024、EMNLP-2023、PLOS 2019-2024 和 eLife 2023-2024。NLPeer 的重点不是单一自动审稿生成，而是为 review assistance、跨领域同行评审分析、score prediction 和 guided skimming 提供统一数据表示。

### v1 构成

| 子集 | 年份 | 评审机制 | 领域 | Papers | Reviews | Accepted 比例 | 说明 |
| --- | --- | --- | --- | ---: | ---: | ---: | --- |
| ARR-22 | 2021-2022 | blind review | NLP/CL | 476 | 684 | 100% | 通过 ACL Rolling Review 捐赠流程收集，包含草稿、camera-ready 版本和评审。 |
| COLING-20 | 2020 | blind review | NLP/CL | 89 | 112 | 93% | COLING 2020 捐赠数据，作者和评审者同意科研使用。 |
| ACL-17 | 2016-2017 | blind review | NLP/CL | 136 | 272 | 67% | 来自 PeerRead 的 ACL 2017 部分，并被 NLPeer 统一格式化。 |
| CONLL-16 | 2015-2016 | blind review | NLP/CL | 22 | 39 | 50% | 来自 PeerRead 的 CoNLL 2016 部分，并被 NLPeer 统一格式化。 |
| F1000-22 | 2012-2022 | open review | multi-domain | 4,949 | 10,418 | 34% | 来自 F1000Research，保留开放评审语境；这里的 accepted 比例按论文定义近似计算。 |
| Total | 2012-2022 | blind/open | multi | 5,672 | 11,515 | 69% avg. | 论文报告总计超过 4M review tokens。 |

### v2 扩展

| 子集 | 年份 | 领域 | 说明 |
| --- | --- | --- | --- |
| ARR-EMNLP-2024 | 2024 | NLP | ARR 为 EMNLP 2024 捐赠的数据；v1.1 包含 findings papers 的 camera-ready 版本。 |
| EMNLP-2023 | 2023 | NLP | EMNLP 2023 公开同行评审数据。 |
| PLOS | 2019-2024 | multi-domain | PLOS 公开同行评审数据。 |
| eLife | 2023-2024 | multi-domain | eLife 公开同行评审数据。 |

### 字段构成

NLPeer 使用统一数据结构组织不同来源的评审数据，通常包含：

- paper draft：投稿版本论文。
- camera-ready version：最终发表版本。
- reviews：评审文本，可兼容结构化或非结构化评审。
- scores：不同 venue 的评分字段，经过统一表示。
- metadata：venue、year、reviewing system、version 等信息。
- parsed paper representation：解析后的结构化论文表示。
- links/versioning：论文版本、评审和段落之间的关联信息。

### 适用任务

- review score prediction。
- guided skimming，即根据评审定位论文中应重点阅读的段落。
- pragmatic label prediction，例如 summary、strength、weakness、request 等评审句子功能分类。
- 跨领域、跨 venue 的同行评审风格和评分分析。

### 使用注意

- 不应用于 reviewer profiling。
- 不同子来源可能有不同许可和再分发约束。
- v2 文件访问受限，使用时需要通过 TU Darmstadt 数据库入口申请或下载。

## PeerRead

### 数据简介

PeerRead 是 NAACL 2018 发布的早期公开同行评审数据集，包含论文草稿、接收/拒绝或可能拒绝标签，以及部分论文的专家文本评审。它适合做论文接受预测、review aspect score prediction 和同行评审过程分析。

### 数据构成

| 子集 | 年份 | Papers | Reviews | Accepted / Rejected | 说明 |
| --- | --- | ---: | ---: | --- | --- |
| NIPS | 2013-2017 | 2,420 | 9,152 | 2,420 / 0 | 只包含已接收论文及其公开评审，因此不能直接用于 accepted/rejected 二分类。 |
| ICLR | 2017 | 427 | 1,304 | 172 / 255 | 来自 OpenReview，包含官方匿名评审、1-10 recommendation 和 1-5 confidence。 |
| ACL | 2017 | 137 | 275 | 88 / 49 | 作者和评审者 opt-in 的 Softconf 数据，包含文本评审和 aspect scores。 |
| CoNLL | 2016 | 22 | 39 | 11 / 11 | 作者和评审者 opt-in 的 Softconf 数据，包含文本评审和 aspect scores。 |
| arXiv | 2007-2017 | 11,778 | 0 | 2,891 / 8,887 | 来自 `cs.cl`、`cs.lg`、`cs.ai`，通过是否匹配顶会发表记录构造 accepted / probably rejected 标签。 |
| Total | 2007-2017 | 14,784 | 10,770 | 5,582 / 9,202 | 总体包含 14.7K paper drafts 和 10.7K expert reviews。 |

### GitHub 目录结构

官方仓库按 venue 或 arXiv 类别组织：

- `acl_2017`
- `conll_2016`
- `iclr_2017`
- `nips_2013-2017`
- `arxiv.cs.ai_2007-2017`
- `arxiv.cs.cl_2007-2017`
- `arxiv.cs.lg_2007-2017`

每个 section 进一步划分为 train/dev/test，论文中说明比例为 0.9 / 0.05 / 0.05。数据对象通常包含 paper details、accept/reject/probably-reject decision 和 reviews。

### 字段构成

- PDF 论文草稿。
- Science Parse 提取的论文文本。
- 接收、拒绝或 probably-rejected 标签。
- 专家文本评审，部分子集无评审文本。
- reviewer recommendation / confidence。
- aspect scores，例如 clarity、originality、soundness、substance、impact 等。

### 使用注意

- NIPS 2013-2017 只包含 accepted papers，不能作为平衡的 acceptance prediction 数据。
- arXiv 子集的 rejected 标签是 probably-rejected，不是真实拒稿记录。
- 部分 section 因许可限制只提供下载说明，不直接包含全部数据文件。
- 整体许可不如 NLPeer 清晰，项目内再分发前需要逐来源核查。

## SEA_data

### 数据简介

SEA_data 是 Paper SEA 工作公开的数据集，服务于 SEA-S、SEA-E 和 SEA-A 三个模块：评审标准化、评审生成和一致性分析。公开 Hugging Face 数据主要来自 OpenReview 上的 NeurIPS 2023 与 ICLR 2024，共 9,021 条，对应论文表中的 3,368 篇 NeurIPS 2023 论文和 5,653 篇 ICLR 2024 论文。

### 公开 SEA_data 构成

| 子集 | 年份 | Papers / Rows | Reviews | Domain | Accepted 比例 | 说明 |
| --- | --- | ---: | ---: | --- | ---: | --- |
| NeurIPS | 2023 | 3,368 | 15,027 | ML | 95% | 来自 OpenReview，论文中用于 in-domain evaluation；接收比例较高，需要注意类别偏斜。 |
| ICLR | 2024 | 5,653 | 21,839 | ML | 37% | 来自 OpenReview，论文中用于 in-domain evaluation；与 NeurIPS 2023 相比接收率更低。 |
| Total public SEA_data | 2023-2024 | 9,021 | 36,866 | ML | 约 59% | 与 Hugging Face 数据卡的 9,021 rows 对应。 |

### SEA 论文实验中的完整数据来源

SEA 论文实验还使用了 cross-domain 和历史 in-domain 数据，统计如下：

| 子集 | 年份 | Papers | Reviews | Domain | 来源关系 |
| --- | --- | ---: | ---: | --- | --- |
| CONLL-16 | 2016 | 22 | 39 | NLP/CL | 来自 PeerRead。 |
| ACL-17 | 2017 | 136 | 272 | NLP/CL | 来自 PeerRead。 |
| COLING-20 | 2020 | 88 | 112 | NLP/CL | 来自 NLPeer。 |
| ARR-22 | 2022 | 364 | 684 | NLP/CL | 来自 NLPeer。 |
| NeurIPS-16-22 | 2016-2022 | 1,048 | 3,847 | ML | 来自 REVIEWER2 相关数据。 |
| ICLR-17-23 | 2017-2023 | 1,617 | 5,779 | ML | 来自 REVIEWER2 相关数据。 |
| NeurIPS-23 | 2023 | 3,368 | 15,027 | ML | SEA 新爬取 OpenReview 数据。 |
| ICLR-24 | 2024 | 5,653 | 21,839 | ML | SEA 新爬取 OpenReview 数据。 |
| Total | 2016-2024 | 12,296 | 47,602 | multi | SEA 论文 Table 1 总统计。 |

### 文件与字段构成

Hugging Face 数据卡说明每个数据集包含四类文件：

- `paper_raw_pdf`：原始论文 PDF。
- `paper_nougat_mmd`：使用 Nougat 解析后的 MMD 文件。
- `review_raw_txt`：爬取的原始评审文本。
- `review_json`：处理后的结构化评审 JSON。

`review_json` 包含：

- `Decision`
- `Meta Review`
- `Summary`
- `Strengths`
- `Weaknesses`
- `Questions`
- `Soundness`
- `Presentation`
- `Contribution`
- `Confidence`
- `Rating`

### 适用任务

- paper-to-review 评审生成。
- 多评审整合与标准化。
- 训练结构化评审生成模型。
- mismatch score 或 review-paper consistency 分析。
- 自动化评审系统中 SEA-S / SEA-E / SEA-A 模块复现。

### 使用注意

- NeurIPS 2023 的 accepted 比例很高，做分类或决策分析时要注意偏斜。
- 不同会议年份的 review schema 不完全一致，SEA 的核心贡献之一就是标准化这些格式差异。
- 如果使用百度网盘镜像，建议记录官方 Hugging Face 下载日期和文件版本，便于之后和官方数据对齐。

## NIPS/NeurIPS Review Archive

### 数据简介

这是课题组自整理的 NIPS/NeurIPS 历年评审数据，覆盖 2016-2025 年。该数据集是 review-only 形式，重点保留评审相关信息，不包含论文 PDF 文件。它更适合做评审文本、评分、置信度、年份变化趋势、rebuttal 交互和作者回复满意度分析，而不是直接做 paper-to-review 生成。

### 数据构成

| 子集 | 年份 | 数据内容 | 是否包含论文 PDF | 说明 |
| --- | --- | --- | --- | --- |
| NIPS / NeurIPS raw reviews | 2016-2025 | 原始评审数据，包括原始评审文本、评分/推荐分、置信度、决策或元信息字段，具体字段以压缩包内文件为准 | 否 | 尽量保留原始公开数据形态，适合回溯、复核和重新清洗。 |
| NIPS / NeurIPS structured reviews | 2016-2025 | 统一结构化后的历年评审数据，将不同年份的 review schema 对齐到一致字段 | 否 | 适合跨年份统计、训练和分析，减少不同年份字段差异带来的处理成本。 |
| NIPS / NeurIPS extracted review points | 2016-2025 | 利用 LLM 从评审意见中抽取的优点、缺点、重要性，以及问题-作者回复 rebuttal 数据对和满意度 | 否 | 满意度用于表示作者回复是否得到审稿人认可，适合研究 rebuttal effectiveness 和 review-author interaction。 |

### 三类数据形态

1. 原始评审数据：保留历年公开评审的原始形态，包含原始 review text、评分/推荐分、置信度、决策或元信息。该版本适合做数据审计、复核字段、重新定义清洗规则。
2. 结构化评审数据：将不同年份、不同字段名和不同评分尺度统一到一致 schema。该版本适合直接做跨年份统计、review score prediction、review quality analysis 和时间趋势分析。
3. LLM 抽取数据：从评审文本中抽取优点、缺点、重要性，以及问题-作者回复的 rebuttal 数据对。每个 rebuttal pair 同时包含满意度字段，用于表示作者回复是否得到了审稿人的认可。

### 适用任务

- 历年评审评分分布分析。
- review-only 文本建模。
- 评审意见长度、结构和风格随年份变化的趋势分析。
- 置信度、推荐分和最终决策之间的关系分析。
- 优点、缺点、重要性等结构化 review aspect 分析。
- 问题-作者回复 rebuttal 对建模。
- 作者回复满意度预测，即判断 rebuttal 是否得到审稿人认可。
- 与 ICLR 历年评审数据做跨会议对比。

### 使用注意

- 该数据只有评审相关数据，没有论文 PDF。
- 如需做 paper-aware review generation，需要额外补充论文 PDF、论文文本或论文元数据。
- 不同年份的评分字段和 review schema 可能不完全一致，正式实验前需要先做字段标准化。
- LLM 抽取字段需要抽样人工核查，尤其是优点/缺点边界、重要性等级和满意度标签。

## ICLR Review Archive

### 数据简介

这是课题组自整理的 ICLR 历年评审数据，覆盖 2017-2026 年。该数据集同样是 review-only 形式，主要用于分析 ICLR 多年评审文本、评分体系、置信度、决策、年度变化趋势、rebuttal 交互和作者回复满意度，不包含论文 PDF 文件。

### 数据构成

| 子集 | 年份 | 数据内容 | 是否包含论文 PDF | 说明 |
| --- | --- | --- | --- | --- |
| ICLR raw reviews | 2017-2026 | 原始评审数据，包括原始评审文本、评分/推荐分、置信度、决策或元信息字段，具体字段以压缩包内文件为准 | 否 | 尽量保留 OpenReview 原始字段，适合回溯、复核和重新清洗。 |
| ICLR structured reviews | 2017-2026 | 统一结构化后的历年评审数据，将不同年份的 OpenReview schema 对齐到一致字段 | 否 | 适合跨年份统计、训练和分析，减少 OpenReview 字段变化带来的处理成本。 |
| ICLR extracted review points | 2017-2026 | 利用 LLM 从评审意见中抽取的优点、缺点、重要性，以及问题-作者回复 rebuttal 数据对和满意度 | 否 | 满意度用于表示作者回复是否得到审稿人认可，适合研究 rebuttal effectiveness 和 review-author interaction。 |

### 三类数据形态

1. 原始评审数据：保留 ICLR / OpenReview 原始评审字段，包含 review text、rating、confidence、decision、forum/reply 等元信息。该版本适合回溯来源和重新清洗。
2. 结构化评审数据：将 ICLR 2017-2026 不同年份的字段统一成一致 schema。该版本适合跨年比较、模型训练、评分预测和评审质量分析。
3. LLM 抽取数据：从评审意见中抽取优点、缺点、重要性，并构建问题-作者回复的 rebuttal 数据对。每个 rebuttal pair 同时包含满意度字段，用于表示作者回复是否得到了审稿人的认可。

### 适用任务

- ICLR 历年评分、置信度和接收趋势分析。
- OpenReview 评审文本风格分析。
- review-only 分类、聚类和可视化。
- 不同年份 review schema 变化分析。
- 优点、缺点、重要性等结构化 review aspect 分析。
- 问题-作者回复 rebuttal 对建模。
- 作者回复满意度预测，即判断 rebuttal 是否得到审稿人认可。
- 与 NIPS/NeurIPS 历年评审数据做跨会议对比。

### 使用注意

- 该数据只有评审相关数据，没有论文 PDF。
- 如需关联论文标题、摘要、全文或 PDF，需要额外补充论文侧数据。
- ICLR 不同年份的 OpenReview 字段可能发生变化，建议先统一字段名、评分尺度和决策标签。
- LLM 抽取字段需要抽样人工核查，尤其是优点/缺点边界、重要性等级和满意度标签。
