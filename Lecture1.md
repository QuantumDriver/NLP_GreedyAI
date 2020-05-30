### 课程内容

视频编号：P1 - P9

1. 所有课程介绍
2. NLP简介
3. 算法复杂度入门

### 课程介绍

1. 观看视频：直播+录播
2. 精炼学习笔记
3. 每周一个quiz + 9个课程项目 + 1个聊天机器人项目 + 1个Capstone项目 
4. 6篇博客 + 个人Github + 论文阅读总结

### NLP介绍

#### NLP的概念

什么是NLP？NLP是Natural Language Processing的缩写，意为自然语言处理。NLP主要包括两个要点，一个是Understanding理解，一个是Generation生成。所以从这个定义来看，NLP = NLU + NLG，从理解到生成。

对于AI领域来说，AI的核心其实就是把一个生活中遇到的问题转化为数学优化的问题，然后再找到合适的工具去解决这个问题。一般来讲，NLP的问题比CV的任务会更加难一点，因为文本的意思比图像的意思更加复杂，更加难以理解。

NLP的主要Challenge在于Ambiguity (一次多义)。通常的解决方法是用概率的方法进行求解，比如说interest有1,2,3种含义，在没有任何数据的情况下，我们计算出$p(1),p(2),p(3)$的概率来，然后再根据数据重新求解$p(1),p(2),p(3)$，即用数据更新概率。

以机器翻译为例子，过去的方法存在如下几个问题：速度慢，语义不对，缺乏上下文，语法问题，规则统计太多，等等。

我们看下面这句话：

今晚的课有意思 ------`分词`------ 今晚 | 的 | 课 | 有意思 ------ `统计` ------ w1 w2 w3 w4 (四个单词代指前面的句子)

![image-20200526214620581.png](https://i.loli.net/2020/05/27/7JImDp3SLOAPBXt.png)

一句话经过分词和统计可以转换成单词的组合，单词可以按照不同的顺序来生成句子，如S1 = w1w2w3w4, S2 = w2w1w3w4。那么这个时候，假设有一个模型L，对于有个句子，它存在 $L(S_i)= prob_i$，即模型L可以输出句子的概率，这样我们就能找到概率最大的句子作为我们想要的翻译结果。

但是我们会看到w1w2w3w4生成句子的方式是排列组合的方式，它的复杂度是$O(2^n)$，一个指数级的复杂度意味着这个问题是NP hard的情况，一般来说是无法解决的。

我们把汉语看成c，英语看成e，那么我们要解决的问题可以写作 $\max P(e|c)$，即给定c的情况下，概率最大的e。根据贝叶斯定理 $P(A | B)=\frac{P(B | A) P(A)}{P(B)}$ 可以把 $P(e|c)$ 写作 $P(e|c)=\frac{P(c|e)P(e)}{P(c)}$，对于每个句子e来说，$P(c)$ 作为分母是固定的，所以 $\max P(e|c)$ 等价于 $\arg \min_{e} P(c|e)P(e)$。

$P(c|e)$ 可以看成是给定词典下，用转换模型 (Translation Model) 转换过后的概率值，而 $P(e)$ 则是一个句子用语言模型 (Language Model) 计算出的概率值。这种用条件概率直接计算句子出现概率的算法是viterbi维特比算法。它被用于寻找最有可能的文本字符串(即句子)。

#### 语言模型 Language Model

语言模型可以告诉我们一句话是人话还是鬼话，我们希望 $p(人话) > p(鬼话)$ 即模型能够准确反映出人话的概率大于鬼话的概率。那么问题的关键就在于如何计算 $p(一句话)$。

对于一句话：S=w1w2w3w4 而言，常用的计算方法有：

Unigram ---> $p(S) = p(w1)p(w2)p(w3)p(w4)$

Bigram ---> $p(S) = p(w1)p(w2|w1)p(w3|w2)p(w4|w3)$

Trigram ---> $p(S) = p(w1)p(w2|w1)p(w3|w2w1)p(w4|w3w2)$

这一类方法统称N-gram模型，其中Unigram是假定每个词互相独立，而Bigram和Trigram的是假定词语之前存在条件概率，前者认为两个词存在条件概率，后者认为是三个词。

#### NLP的应用领域

- 问答系统
    - 给定一个知识库，输入问题，输出答案
- 情感分析 Sentiment Analysis
    - 股价预测
    - 舆情监控
    - 产品评论
    - 事件监测
- 机器翻译
- 自动摘要
- 聊天机器人
- 信息抽取

[NLP关键问题](https://www.quora.com/What-are-the-major-open-problems-in-natural-language-understanding)

#### NLP核心技术(4个维度)

1. Semantic 语义层面: NLU, ML
2. Syntax 句子层面: 句法分析，依存分析
3. Morphology 单词层面: 分词，词性，命名实体识别
4. Phonetics 声音层面 (信号处理，与NLP相关性不大)

主要技术有：

- Word Segmentation 分词
- Part-of-Speech 词性
- Named Entity Recognition 命名实体识别
- Parsing 句法分析
- Dependency Parsing 依存分析
- Relation Extraction 关系抽取
- Text Summarization 文本摘要
- Machine Dialog System 机器对话系统

对于这些技术，总的来说，句子的理解比句子的生成要容易一些，生成句子是最难的。

### 作业

#### 请列出至少5位你感兴趣的国外顶尖NLP专家以及他们目前所在单位和主要研究领域：

- 0. Kevin Knight: 之前USC，现在滴滴LA,  主要研究 Machine Translation
- 1. Michael Collins，哥伦比亚大学教授，主要研究 Parse Reranking
- 2. Christopher Manning，斯坦福教授，主要研究深度学习在NLP的应用
- 3. Jason Eisner，JHU教授，主要研究语言结构的概率模型
- 4. David Yarowsky， JHU教授，主要研究 Word sense disambiguation
- 5. Percy Liang，斯坦福教授，主要研究NLP阅读理解和对话系统


#### 请列出至少5位你感兴趣的国内顶尖NLP专家以及他们目前所在单位和研究领域：

- 1. 孙茂松，清华教授，汉语自动分词
- 2. 刘知远，清华教授，知识图谱
- 3. 刘挺，哈工大教授，事理图谱
- 4. 王厚峰，北大教授，语义分析技术、自动问答和人机对话
- 5. 宗成庆，中科院，机器翻译


#### 请列出至少3个国内外你感兴趣的博客（个人博客，提供链接）：

- 1. 刘知远，https://github.com/zibuyu/research_tao
- 2. Awesome-nlp, https://github.com/keon/awesome-nlp
- 3. Susan Li, https://medium.com/@actsusanli


#### 请列出至少5个你感兴趣的国内做NLP的公司以及他们主要产品

- 1. 搜狗，搜狗输入法
- 2. 科大讯飞，讯飞翻译
- 3. 腾讯，自然语言处理 NLP
- 4. 微软亚洲研究院，微软小冰
- 5. 阿里达摩院，AliReader/AliTranx/AliNLP



