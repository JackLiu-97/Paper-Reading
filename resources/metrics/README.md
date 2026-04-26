# Metrics

这里登记自动化评审相关评价指标。当前指标主要用于比较模型生成评审与人类评审之间的相似度、覆盖度、态度一致性，以及检查自动评审系统是否出现模板化输出。

## 自动化评审评价指标总览

| Metric | Task | Definition | Implementation | Reference | Notes |
| --- | --- | --- | --- | --- | --- |
| Distinct-4 | Language diversity | 不同 4-gram 数量 / 总 4-gram 数量，用于衡量输出是否重复、模板化。 | 自定义 tokenizer + n-gram counter | Distinct-n | 越大通常表示越不重复，但不代表内容更准确。 |
| Self-BLEU@4 | Language diversity | 将每条生成文本作为 candidate，其余生成文本作为 references，计算平均 BLEU-4。 | BLEU implementation + leave-one-out corpus loop | BLEU / Self-BLEU | 越小通常表示输出之间差异更大；高分可能说明模板化严重。 |
| Inverse Self-BLEU@4 | Language diversity | 对 Self-BLEU 做反向变换，使多样性分数变成越大越好。 | `2 - Self-BLEU` 或论文指定变换 | Self-BLEU variant | 必须和论文或代码实现保持一致，避免不同实验不可比。 |
| ROUGE-1 | Semantic consistency | Candidate 与 reference 的 unigram overlap，可报告 Precision / Recall / F1。 | `rouge-score` 或同类 ROUGE 实现 | ROUGE | 适合快速检查关键词和要点覆盖；对同义改写不敏感。 |
| ROUGE-L | Semantic consistency | 基于最长公共子序列 LCS 的文本顺序和结构对齐指标。 | `rouge-score` 或同类 ROUGE 实现 | ROUGE-L | 比 ROUGE-1 更关注顺序；评审要点顺序变化大时可能不稳定。 |
| SPICE | Semantic consistency | 将文本解析为语义元组或语义图后比较结构匹配。 | SPICE parser / semantic tuple matcher | SPICE | 更贴近语义结构，但依赖解析器质量，长文本场景成本较高。 |
| BERT-based Sentiment Score | Sentiment consistency | 用 BERT 类情感模型得到情感分数，再比较 candidate 与 reference 差异。 | Domain sentiment classifier / BERT classifier | BERT-based classifier | 需要区分情感分数和 BERTScore；学术评审中只能作为辅助指标。 |
| VADER Score | Sentiment consistency | 使用 VADER compound score 比较 candidate 与 reference 的整体情感极性。 | VADER sentiment analyzer | VADER | 对一般英文评论有效；学术评审语体较克制，信号可能较弱。 |
| METEOR | Text-level matching | 结合 exact match、stem match、synonym match 和顺序惩罚的文本匹配指标。 | METEOR implementation / NLTK METEOR | METEOR | 比 BLEU 更宽松，适合作为词级综合匹配参考。 |

> “越大越好”只表示更符合该指标本身，不代表评审质量一定更高。自动化评审评估应同时看内容覆盖、事实可靠性、可操作性、一致性和多样性。

## 适用场景

- 比较模型评审意见与人类评审意见是否一致。
- 比较不同自动评审系统的输出质量。
- 检查模型是否生成高度模板化、重复化的评审文本。
- 作为自动化评审系统的辅助量化指标，与人工评估或 LLM-as-judge 评估结合使用。

## Language Diversity

### Distinct-4

Distinct-4 用于衡量单条或一组生成文本的 4-gram 多样性。设文本 token 序列为：

$$
(w_1, w_2, \dots, w_N)
$$

所有 4-gram 为：

$$
g_i^{(4)} = (w_i, w_{i+1}, w_{i+2}, w_{i+3}), \quad i = 1, \dots, N-3
$$

记总 4-gram 集合为 $G_4$，不同 4-gram 集合为 $U_4$，则：

$$
\text{Distinct-4}(T) = \frac{|U_4|}{|G_4|} = \frac{|U_4|}{N-3}
$$

常见汇总方式：

- Macro：先计算每条文本的 Distinct-4，再取平均。
- Micro / Corpus：把所有文本拼接后统一计算。

注意事项：

- tokenizer 会显著影响结果，中文按字、按词、按子词切分会得到不同值。
- 文本长度小于 4 时，需要提前约定记为 0 还是跳过。
- Distinct 高只能说明更不重复，不等于更正确或更有帮助。

### Self-BLEU@4

Self-BLEU@4 用于衡量一组生成结果彼此是否过于相似。设生成集合为：

$$
S = \{s_1, s_2, \dots, s_M\}
$$

把每条 $s_i$ 当作 candidate，其余文本作为 references：

$$
\text{Self-BLEU@4}(S) = \frac{1}{M}\sum_{i=1}^{M} \text{BLEU}_4(s_i \mid S \setminus \{s_i\})
$$

解释：

- Self-BLEU 高：不同输出彼此很像，可能模板化严重。
- Self-BLEU 低：不同输出差异更大，多样性更高。

如果需要让多样性分数统一成“越大越好”，可以使用 Inverse Self-BLEU，例如：

$$
\text{Inverse Self-BLEU} = 2 - \text{Self-BLEU}
$$

具体变换应以论文或代码实现为准。

### BLEU 核心形式

$$
\text{BLEU} = \text{BP} \cdot \exp\left(\sum_{n=1}^{4} w_n \log p_n\right), \quad w_n = \frac{1}{4}
$$

其中 $p_n$ 是截断后的 n-gram precision，$\text{BP}$ 是长度惩罚项：

$$
\text{BP} =
\begin{cases}
1, & c > r \\
\exp(1-\frac{r}{c}), & c \le r
\end{cases}
$$

## Semantic Consistency

### ROUGE-1

ROUGE-1 衡量 unigram 重叠程度。设 candidate 为 $C$，reference 为 $R$：

$$
\text{Overlap}_1(C, R) = \sum_w \min(\text{Count}_C(w), \text{Count}_R(w))
$$

Recall、Precision 和 F1 分别为：

$$
\text{ROUGE-1}_R =
\frac{\text{Overlap}_1(C, R)}{\sum_w \text{Count}_R(w)}
$$

$$
\text{ROUGE-1}_P =
\frac{\text{Overlap}_1(C, R)}{\sum_w \text{Count}_C(w)}
$$

$$
\text{ROUGE-1}_{F1} = \frac{2PR}{P+R}
$$

特点：

- 能较粗粒度反映关键词是否对齐。
- 对同义改写不敏感。
- 适合做“是否覆盖关键要点”的快速判断。

### ROUGE-L

ROUGE-L 基于最长公共子序列 LCS，不要求连续，但要求顺序一致。设 $\text{LCS}(C, R)$ 为 candidate 和 reference 的最长公共子序列长度：

$$
P_{LCS} = \frac{\text{LCS}(C, R)}{|C|}
$$

$$
R_{LCS} = \frac{\text{LCS}(C, R)}{|R|}
$$

F-score 形式：

$$
\text{ROUGE-L} =
\frac{(1+\beta^2)P_{LCS}R_{LCS}}{R_{LCS} + \beta^2 P_{LCS}}
$$

特点：

- 比 ROUGE-1 更关注整体顺序和结构。
- 当评审意见顺序变化很大时，结果可能不够稳定。

### SPICE

SPICE 更偏向语义结构匹配。它会把句子表示成语义元组或语义图，再比较 candidate 与 reference 的匹配程度。

设 $T(C)$ 为 candidate 的语义元组集合，$T(R)$ 为 reference 的语义元组集合，$m = |T(C) \cap T(R)|$：

$$
P = \frac{m}{|T(C)|}, \quad
R = \frac{m}{|T(R)|}, \quad
\text{SPICE} = \frac{2PR}{P+R}
$$

特点：

- 更看重语义结构是否一致。
- 对解析器质量依赖较高。
- 长文本评审场景下结果可能不稳定。

## Sentiment Consistency

### BERT-based Sentiment Score

常见做法：

1. 用基于 BERT 的情感模型提取 candidate 和 reference 的情感分数。
2. 比较两者情感差异。
3. 差异越小，则情感一致性越高。

常见形式：

$$
1 - |s_C - s_R|
$$

或：

$$
\exp(-|s_C - s_R|)
$$

注意事项：

- 有些论文会把 “BERT-based score” 写得比较笼统，需要区分它是在做情感比较，还是在做语义相似度，例如 BERTScore。
- 学术评审文本情感信号较弱，情感一致性不应单独作为质量判断依据。

### VADER Score

VADER 是基于词典和规则的情感分析方法，通常输出 compound score，范围常见为 $[-1, 1]$。

使用方式：

- 分别计算 candidate 和 reference 的 VADER 分数。
- 比较它们的差异。
- 差异越小，情感一致性越高。

注意事项：

- 情感一致不等于论据正确。
- 学术评审语体通常较冷静，VADER 更适合作为辅助指标。

## METEOR

METEOR 是比 BLEU 更宽松的文本匹配指标，不仅看 exact match，还考虑词干匹配、同义词匹配和顺序惩罚。

典型流程：

1. 分词。
2. Exact match。
3. Stem match。
4. Synonym match。
5. 选择全局最优对齐。
6. 计算 Precision / Recall。
7. 计算顺序惩罚 fragmentation penalty。

如果最终匹配到 $m$ 个词：

$$
P = \frac{m}{|H|}, \quad
R = \frac{m}{|R|}
$$

METEOR 使用偏向 Recall 的加权 F-score：

$$
F_{\text{mean}} = \frac{10PR}{R + 9P}
$$

设 `chunks` 表示对齐片段数，$m$ 表示匹配词数，惩罚项常写为：

$$
\text{Penalty} = \gamma \left(\frac{\text{chunks}}{m}\right)^\beta
$$

最终：

$$
\text{METEOR} = F_{\text{mean}} \times (1 - \text{Penalty})
$$

直觉理解：

- chunk 少：顺序自然，惩罚小。
- chunk 多：顺序破碎，惩罚大。

## 推荐组合

自动化评审任务中，建议至少组合使用以下指标，而不是只看单项分数：

| 目标 | 推荐指标 | 用途 |
| --- | --- | --- |
| 检查模板化 | Distinct-4 + Self-BLEU@4 | 判断生成评审是否高度重复。 |
| 检查要点覆盖 | ROUGE-1 + ROUGE-L | 判断模型评审是否覆盖人类评审中的关键词、要点和基本结构。 |
| 补充语义结构 | SPICE | 判断核心语义关系是否保留。 |
| 辅助态度一致性 | VADER 或领域化 BERT 情感模型 | 判断正负倾向是否大体一致。 |
| 综合文本匹配 | METEOR | 作为比 BLEU 更宽松的词级匹配参考。 |

实际使用时，建议报告指标实现细节，包括 tokenizer、文本预处理、score aggregation 方式、是否使用 macro/micro 平均，以及是否对短文本或空输出做特殊处理。
