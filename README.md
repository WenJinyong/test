

Thank you for your valuable feedback and constructive suggestions.

**Question 1:** There are some works combining statistical methods with contrastive learning, which have not been discussed [1,2]. 

**Answer:** Thank you for your recommendations and suggestions. We have read DATE [1] in the past few days. From a statistical perspective, DATE [1] constructs semantic similarity structure using ball-divergence to enhance the performance of deep unsupervised hashing. Due to time constraints, we haven't had the opportunity to read the paper [2] yet. We will carefully go through this paper in the coming days. We will cite the two works [1,2] and add them to the related work section.

[1] A Statistical Approach to Mining Semantic Similarity for Deep Unsupervised Hashing,

[2] On contrastive learning for likelihood-free inference.



**Question 2:** Maybe the authors can introduce more SOTA published in 2022-2023?. 

**Answer:** Thank you for your valuable suggestions. To make the comparison more thorough, we add GGD [3], AF-GCL [4], and SUGRL [5] to the unsupervised baselines, which are proposed in 2022. These works attempt to design augmentation-free graph contrastive learning methods. GGD addresses graph self-supervised learning as a node discrimination problem, which directly utilizes a simple binary cross-entropy loss to discriminate two groups of nodes. AF-GCL points out that graph augmentation makes GCL sensitive to graph homophily degree. Instead of data augmentation, AF-GCL proposes to construct the positive sample set based on the similarity between node representations. SUGRL regards two embeddings of one node from two various branches (that is, MLPs and GNNs) as a pair of positive samples. Besides, SUGRL adopts neighborhood nodes as positive samples to strengthen local proximity.

For all compared methods, we first utilize their models to learn node representations in an unsupervised manner. With the same experimental setup as ours, including the same dataset split, we further evaluate the learned representations on node classification task. The experimental results are summarized as follows:

| Dataset       |      Cora      |    Citeseer    |     Pubmed     |    Computers     |      Photo       |        CS        |     Physics      |
| ------------- | :------------: | :------------: | :------------: | :--------------: | :--------------: | :--------------: | :--------------: |
| GGD           | 83.6 $\pm$ 0.5 | 73.2 $\pm$ 0.5 | 80.2 $\pm$ 0.4 |  87.5 $\pm$ 0.4  |  92.3 $\pm$ 0.5  |  92.5 $\pm$ 0.3  | 95.12 $\pm$ 0.14 |
| SUGRL         | 83.5 $\pm$ 0.4 | 73.2 $\pm$ 0.5 | 81.8 $\pm$ 0.3 |  87.6 $\pm$ 0.2  |  92.6 $\pm$ 0.3  |  93.2 $\pm$ 0.2  | 95.21 $\pm$ 0.09 |
| AF-GCL        | 83.3 $\pm$ 0.3 | 72.2 $\pm$ 0.4 | 79.2 $\pm$ 0.6 |  87.3 $\pm$ 0.3  |  92.4 $\pm$ 0.2  |  92.1 $\pm$ 0.1  | 95.02 $\pm$ 0.18 |
| MC-DCD (ours) | 84.5 $\pm$ 0.3 | 73.6 $\pm$ 0.3 | 81.7 $\pm$ 0.3 | 88.70 $\pm$ 0.31 | 93.14 $\pm$ 0.15 | 93.60 $\pm$ 0.08 | 95.42 $\pm$ 0.12 |
| MC-SR (ours)  | 84.4 $\pm$ 0.4 | 73.5 $\pm$ 0.4 | 81.5 $\pm$ 0.4 | 88.78 $\pm$ 0.25 | 93.09 $\pm$ 0.14 | 93.56 $\pm$ 0.11 | 95.38 $\pm$ 0.08 |

[3] Rethinking and scaling up graph contrastive learning: An extremely efficient approach with group discrimination. NeurIPS 2022.

[4] Augmentation-free graph contrastive learning with performance guarantee. 2022.

[5] Simple unsupervised graph representation learning. AAAI, 2022.



**Question 3:** Can this method be used to tackle the graph-level problems?

**Answer:** Yes, our method can be used to dealing with graph-level tasks. To this end, the model architecture needs to make a slight modification. We utilize a graph global-pooling function to obtain the graph-level representation. Specifically, the concatenated results of MaxPooling and MeanPooling are adopted. For evaluation, we feed learned graph-level representations into a downstream LIBSVM [6] classifier and then report the mean accuracy of 10 results. The classification results are as follows:

| Dataset       | PROTEINS [7] | MUTAG [7] | IMDB-B [7] |
| ------------- | ------------ | --------- | ---------- |
| InfoGraph [8] | 74.8         | 89.0      | 73.0       |
| GraphCL [9]   | 74.4         | 89.8      | 71.1       |
| CLEAR [10]    | 76.1         | --        | 72.5       |
| HGCL [11]     | 75.5         | 90.1      | 73.9       |
| MC-DCD (ours) | 75.7         | 90.6      | 73.5       |

[6] LIBSVM: a library for support vector machines. 2011.

[7] Deep graph kernel. KDD, 2015.

[8] Infograph: Unsupervised and semi-supervised graph-level representation learning via mutual information maximization.

[9] Graph contrastive learning with augmentations.

[10] CLEAR: Cluster-Enhanced Contrast for Self-Supervised Graph Representation Learning.

[11] Unsupervised graph-level representation learning with hierarchical contrasts.





We truly appreciate your time, effort, and expertise invested in reviewing our manuscript. We are looking forward to further discussion and exchange with you.
