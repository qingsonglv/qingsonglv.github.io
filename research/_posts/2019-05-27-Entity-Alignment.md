---
title: A Brief Survey of Embedding-based Entity Alignment Methods
description: >
  Entity alignment (EA) aims to merge the equivalent entities given two networks, which is important to many applications. For example, cross-platform social network (SN) user alignment can be used for user profiling and user interests mining. Another example, cross-lingual knowledge graph (KG) alignment is able to assist cross-lingual information retrieval and machine translation. This post is a brief survey of embedding-based EA methods.
---

[Chinese Version](https://www.aminer.cn/research_report/5cecc3f41976c5c87c8bee63?download=false) (Since it is out of my control, it is out-dated compared with this post.)

There are two directions of **traditional methods**:

* Entity labels, e.g. user nicknames in SNs and entity labels in KGs.
* Handcrafted features, e.g. common neighbors or some task-specific features.

For entity labels, it is unstable and unpromising since many real world networks are complex. For handcrafted features, it is hard to migrate between different scenarios.

In recent years, **embedding-based methods** attract more and more attention. Given a network, embedding-based representation learning models project entities into a low-dimensional vector space. Among them, TransE is a typical model in KG domain, and DeepWalk in SN domain. Both of them are enlightened by Skip-gram word embedding model.

Similar to EA, cross-lingual word alignment is also an important area in NLP. Before embedding-based methods proposed, they developed seperately. However, after embedding-based model becomes a rising star, their development tracks show a lot of similarity.

![](/assets/img/blog/EA/en-sp.png)
<div align="center">Figure 1: English-Spanish word embeddings alignment by linear transformation [1]</div>

When **embedding-based EA** methods firstly proposed, they usually follow two threads.

The first track is to merge the pre-aligned entities first, then use single network embedding models to get embeddings of entities. The representative works are JE (CCKS 2016) [2] in KG domain, and IONE (IJCAI 2016) [3] in SN domain.

![](/assets/img/blog/EA/1.png)
<div align="center">Figure 2: JE (figure by [18])</div>

The second track is to train two single networks seperately, then use the pre-aligned entities to get a mapping function between two vector spaces. The representative works are MTransE (IJCAI 2017) [4] in KG domain, and PALE (IJCAI 2016) [5] in SN domain.

![](/assets/img/blog/EA/2.png)
<div align="center">Figure3: MTransE (figure by [18])</div>

**After that**, there are two directions to tune alignment precision.

* **Iterative alignment**. Intuitively, newly aligned entities can furthor promote more aligned entities. Therefore, this is naturally iterative procedure. IPTransE (IJCAI 2017) [6] is the first research to propose this idea. However, error propogation is a problem of iterative alignment. BootEA (IJCAI 2018) [7] alleviate this problem by a seed editing method, which means newly aligned entities can also be edited or removed.
* **Attribute information**. Sometimes, only using structure information of network is not promising in EA, so combination with attribute information is also an important area. The representative works are JAPE (ISWC 2017) [8], KDCoE (IJCAI 2018) [9] and GCN-Align (EMNLP 2018) [10] in KG domain, and REGAL (CIKM 2018) [11] and MEgo2Vec (CIKM 2018) [12] in SN domain. By the way, my bachelor degree research HIN-Align [21] shows that GCN-Align is also adaptive to SN domain.

**More recently**, alignment methods went through explosive grouth in 2019. Four fancy new directions are proposed:

* Firstly, **unsupervised alignment**. The prerequisite of pre-aligned entities is hard to satisfy in real world scenario, so researchers are exploring how to get alignment seeds from scratch. Two representative works are as follows:
    * Entity Alignment between Knowledge Graphs Using Attribute Embeddings (AAAI 2019) [13]
    * Deep Adversarial Network Alignment (arxiv 2019) [14]
* Secondly, **multi-view alignment**. Due to the complexity of alignment problem, embedding with one model (or view) is not enough to obtain promising result. MOANA (WWW 2019) [15] proposes a multi-level embedding model to embed information from multi-view. Moreover, they reduce the time complexity of seed excavation to linear. MuGNN (ACM 2019) [22] uses multi-channel GNN, which is also a kind of multi-view. GMNN (ACL 2019) [19] aims at aligning entities from the perspective of attribute, local strucutre and global structure. MultiKE (IJCAI 2019) [20] tried more views and more combination methods, and got higher hits score.
* The third one is a very hard-core direction, **modify embedding model to improve alignment**, which means the improvement is on a low level. SEA (WWW 2019) [16] is such a work. They point out that the existing embedding models usually make nodes with similar degree close, which is not good for alignment. And they propose an adversarial method to mitigate this drawback.
* Last, **web-scale alignment**. Most existing works test models on datasets with only millions of entities. However, when aligning billions of nodes, brand new problems come up from time complexity or precision control. Representative work is OAG (KDD 2019) [17].

For the last part of this article, I would like to share some of my thoughts.

First, about the directions that are not excavated so far in entity alignment.

* **An integrated alignment system.** Things are getting more and more complicated in alignment problem. For one thing, more techniques are proposed such as iterative procedure, multi-view ensembling, etc. For another, more and more datasets are constructed. Tens of experiments are needed to publish a paper for EA. We need an integrated alignment system or framework to tackle with these difficulties.
* **Online alignment.** Static graph alignment is not that practical in real world scenario. However, there is no work yet exploring this online alignment field, that performs alignment in an incremental way.

Second, intuition about multi-view alignment. I think the reason why multi-view alignment works, is that different models tend to make the same positive entity pairs close, but different negative entity pairs far. After combining these models, negative pairs will be further, even if they are close in one or two models before combining. I think this multi-view idea is the key to an integrated alignment system and online alignment.

## References

1. Mikolov T, Le Q V, Sutskever I. Exploiting similarities among languages for machine translation[J]. arXiv preprint arXiv:1309.4168, 2013.
2. Hao Y, Zhang Y, He S, et al. A joint embedding method for entity alignment of knowledge bases[C]//China Conference on Knowledge Graph and Semantic Computing. Springer, Singapore, 2016: 3-14.
3. Liu L, Cheung W K, Li X, et al. Aligning Users across Social Networks Using Network Embedding[C]//IJCAI. 2016: 1774-1780.
4. Chen M, Tian Y, Yang M, et al. Multilingual knowledge graph embeddings for cross-lingual knowledge alignment[J]. arXiv preprint arXiv:1611.03954, 2016.
5. Man T, Shen H, Liu S, et al. Predict Anchor Links across Social Networks via an Embedding Approach[C]//IJCAI. 2016, 16: 1823-1829.
6. Zhu H, Xie R, Liu Z, et al. Iterative Entity Alignment via Joint Knowledge Embeddings[C]//IJCAI. 2017: 4258-4264.
7. Sun Z, Hu W, Zhang Q, et al. Bootstrapping Entity Alignment with Knowledge Graph Embedding[C]//IJCAI. 2018: 4396-4402.
8. Sun Z, Hu W, Li C. Cross-lingual entity alignment via joint attribute-preserving embedding[C]//International Semantic Web Conference. Springer, Cham, 2017: 628-644.
9. Chen M, Tian Y, Chang K W, et al. Co-training embeddings of knowledge graphs and entity descriptions for cross-lingual entity alignment[J]. arXiv preprint arXiv:1806.06478, 2018.
10. Wang Z, Lv Q, Lan X, et al. Cross-lingual Knowledge Graph Alignment via Graph Convolutional Networks[C]//Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing. 2018: 349-357.
11. Heimann M, Shen H, Safavi T, et al. Regal: Representation learning-based graph alignment[C]//Proceedings of the 27th ACM International Conference on Information and Knowledge Management. ACM, 2018: 117-126.
12. Zhang J, Chen B, Wang X, et al. MEgo2Vec: Embedding matched ego networks for user alignment across social networks[C]//Proceedings of the 27th ACM International Conference on Information and Knowledge Management. ACM, 2018: 327-336.
13. Trisedya B D, Qi J, Zhang R. Entity Alignment between Knowledge Graphs Using Attribute Embeddings[C]. AAAI, 2019.
14. Derr T, Karimi H, Liu X, et al. Deep Adversarial Network Alignment[J]. arXiv preprint arXiv:1902.10307, 2019.
15. Zhang S, Tong H, Maciejewski R, et al. Multilevel Network Alignment[C]//The World Wide Web Conference. ACM, 2019: 2344-2354.
16. Pei S, Yu L, Hoehndorf R, et al. Semi-Supervised Entity Alignment via Knowledge Graph Embedding with Awareness of Degree Difference[C]//The World Wide Web Conference. ACM, 2019: 3130-3136.
17. https://www.aminer.cn/oag2019
18. https://github.com/zhichun
19. Xu K, Wang L, Yu M, et al. Cross-lingual Knowledge Graph Alignment via Graph Matching Neural Network[J]. arXiv preprint arXiv:1905.11605, 2019.
20. Zhang Q, Sun Z, Hu W, et al. Multi-view Knowledge Graph Embedding for Entity Alignment[J]. arXiv preprint arXiv:1906.02390, 2019.
21. https://github.com/1049451037/HIN-Align
22. Cao Y, Liu Z, Li C, et al. Multi-Channel Graph Neural Network for Entity Alignment[C]//Proceedings of the 57th Conference of the Association for Computational Linguistics. 2019: 1452-1461.