---
title: A Brief Survey of Embedding-based Entity Alignment Methods
description: >
  Entity alignment (EA) aims to merge the equivalent entities given two networks, which is important to many applications. For example, cross-platform social network (SN) user alignment can be used for user profiling and user interests mining. Another example, cross-lingual knowledge graph (KG) alignment is able to assist cross-lingual information retrieval and machine translation. This post is a brief survey of embedding-based EA methods.
---

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
<div align="center">Figure 2: JE (figure by [19])</div>

The second track is to train two single networks seperately, then use the pre-aligned entities to get a mapping function between two vector spaces. The representative works are MTransE (IJCAI 2017) [4] in KG domain, and PALE (IJCAI 2016) [5] in SN domain.

![](/assets/img/blog/EA/2.png)
<div align="center">Figure3: MTransE (figure by [19])</div>

**After that**, there are two directions to tune alignment precision.

* **Iterative alignment**. Intuitively, newly aligned entities can furthor promote more aligned entities. Therefore, this is naturally iterative procedure. IPTransE (IJCAI 2017) [6] is the first research to propose this idea. However, error propogation is a problem of iterative alignment. BootEA (IJCAI 2018) [7] alleviate this problem by a seed editing method, which means newly aligned entities can also be edited or removed.
* **Attribute information**. Sometimes, only using structure information of network is not promising in EA, so combination with attribute information is also an important area. The representative works are JAPE (ISWC 2017) [8], KDCoE (IJCAI 2018) [9] and GCN-Align (EMNLP 2018) [10] in KG domain, and REGAL (CIKM 2018) [11] and MEgo2Vec (CIKM 2018) [12] in SN domain.

**More recently**, alignment methods went through explosive grouth in 2019. Five fancy new directions are proposed:

* Firstly, **unsupervised alignment**. The prerequisite of pre-aligned entities is hard to satisfy in real world scenario, so researchers are exploring how to get alignment seeds from scratch. Two representative works are as follows:
    * Entity Alignment between Knowledge Graphs Using Attribute Embeddings (AAAI 2019) [13]
    * Weakly-supervised Knowledge Graph Alignment with Adversarial Learning (ICLR 2019, though rejected, it worths learning) [14]
* Secondly, **multi-network alignment**. Most settings of alignment task is network-pair alignment. However, when aligning multiple networks, pairwise alignment is time-consuming and lack of interaction between multiple networks. Representative work is CrossMNA (WWW 2019) [15]. Interestingly, they emphasize not using attribute information in this paper.
* Thirdly, **multi-view alignment**. Due to the complexity of alignment problem, embedding with one model (or view) is not enough to obtain promising result. MOANA (WWW 2019) [16] proposes a multi-level embedding model to embed information from multi-view. Moreover, they reduce the time complexity of seed excavation to linear. ACL 2019 also has a publication [20] aiming at aligning entities from the perspective of attribute, local strucutre and global structure.
* The fourth one is a very hard-core direction, **modify embedding model to improve alignment**, which means the improvement is on a low level. SEA (WWW 2019) [17] is such a work. They point out that the existing embedding models usually make nodes with similar degree close, which is not good for alignment. And they propose an adversarial method to tackle with this problem.
* Last, **web-scale alignment**. Most existing works test models on datasets with only millions of entities. However, when aligning billions of nodes, brand new problems come up from time complexity or precision control. Representative work is OAG (KDD 2019) [18].

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
14. https://openreview.net/forum?id=S14h9sCqYm
15. Chu X, Fan X, Yao D, et al. Cross-Network Embedding for Multi-Network Alignment[C]//The World Wide Web Conference. ACM, 2019: 273-284.
16. Zhang S, Tong H, Maciejewski R, et al. Multilevel Network Alignment[C]//The World Wide Web Conference. ACM, 2019: 2344-2354.
17. Pei S, Yu L, Hoehndorf R, et al. Semi-Supervised Entity Alignment via Knowledge Graph Embedding with Awareness of Degree Difference[C]//The World Wide Web Conference. ACM, 2019: 3130-3136.
18. https://www.aminer.cn/oag2019
19. https://github.com/zhichun
20. Xu K, Wang L, Yu M, et al. Cross-lingual Knowledge Graph Alignment via Graph Matching Neural Network[J]. arXiv preprint arXiv:1905.11605, 2019.