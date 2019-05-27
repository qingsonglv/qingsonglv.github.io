---
title: A Brief Survey of Embedding-based Entity Alignment Methods
description: >
  Entity alignment (EA) aims to merge the equivalent entities given two networks, which is important to many applications. For example, cross-platform social network (SN) user alignment can be used for user profiling and user interests mining. Another example, cross-lingual knowledge graph (KG) alignment is able to assist cross-lingual information retrieval and machine translation. This post is a brief survey of embedding-based EA methods.
---

There are two directions of traditional methods:

* Entity labels, e.g. user nicknames in SNs and entity labels in KGs.
* Handcrafted features, e.g. common neighbors or some task-specific features.

For entity labels, it is unstable and unpromising since many real world networks are complex. For handcrafted features, it is hard to migrate between different scenarios.

In recent years, embedding-based methods attract more and more attention. Given a network, embedding-based representation learning models project entities into a low-dimensional vector space. Among them, TransE is a typical model in KG domain, and DeepWalk in SN domain. Both of them are enlightened by Skip-gram word embedding model.

Similar to EA, cross-lingual word alignment is also an important in NLP. Before embedding-based methods proposed, they developed seperately. However, after embedding-based model becomes a rising star, their development tracks show a lot of similarity.

![English-Spanish word embeddings alignment by linear transformation](/assets/img/blog/EA/en-sp.png)

When embedding-based EA methods firstly proposed, they usually follow two threads.

The first track is to merge the pre-aligned entities first, then use single network embedding models to get embeddings of entities. The representative works are JE (CCKS 2016) in KG domain, and IONE (IJCAI 2016) in SN domain.

![](/assets/img/blog/EA/1.png)

The second track is to train two single networks seperately, then use the pre-aligned entities to get a mapping function between two vector spaces. The representative works are MTransE (IJCAI 2017) in KG domain, and PALE (IJCAI 2016) in SN domain.

![](/assets/img/blog/EA/2.png)

After that, there are two directions to tune alignment precision.

* Iterative alignment. Intuitively, newly aligned entities can furthor promote more aligned entities. Therefore, this is naturally iterative procedure. IPTransE (IJCAI 2017) is the first research to propose this idea. However, error propogation is a problem of iterative alignment. BootEA (IJCAI 2018) alleviate this problem by a seed editing method, which means newly aligned entities can also be edited or removed.
* Attribute information. Sometimes, only using structure information of network is not promising in EA, so combination with attribute information is also an important area. The representative works are JAPE (ISWC 2018) and GCN-Align (EMNLP 2018) in KG domain, and REGAL (CIKM 2018) and MEgo2Vec (CIKM 2018) in SN domain.

More recently, two fancy new directions are proposed:

* Firstly, unsupervised alignment. The prerequisite of pre-aligned entities is hard to satisfy in real world scenario, so researchers are exploring how to get alignment seeds from scratch. Two representative works are as follows:
    * Entity Alignment between Knowledge Graphs Using Attribute Embeddings (AAAI 2019)
    * Weakly-supervised Knowledge Graph Alignment with Adversarial Learning (ICLR 2019)
* Secondly, web-scale alignment. Most existing works test models on datasets with only millions of entities. However, when aligning billions of nodes, brand new problems come up from time complexity or precision control. Representative work is [OAG](https://www.aminer.cn/oag2019) (KDD 2019)