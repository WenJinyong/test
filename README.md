We sincerely appreciate your detailed, professional, and valuable reviews, which greatly contribute to the improvement of our work! Next, we will try our best to address your questions and further enhance our work.

**Question 1:** The theoretical contributions seem rather straight-forward as most can be found or deduced from other papers.

**Answer:** Here, we will respond point by point to the questions raised by the reviewer in the "**Redundant theoretical analysis**" part.

(1) Mutual Information between multivariate Gaussians is already well-studied and can be found in several classical books of Information Theory and Statistics.

*Answer:* We are grateful to the reviewer for providing the references. Indeed, as the reviewer pointed out, there have been some researches on Gaussian Mutual Information (GMI) in the fields of statistics and information theory. In our revision, we have included citations involving GMI. Simultaneously, we will preserve the derivation process of Gaussian mutual information in Appendix A to ensure the self-completeness of our paper. This allows interested readers to directly browse the derivation of GMI without searching for related literature. To be honest, we have not found any existing literature that provides a complete derivation process for Gaussian mutual information.

(2) The relations and differences between our paper and CorInfoMax should be clearly stated in terms of design. The distinctions between them mainly lie in how to handle instability.

*Answer:* In the design of objective function, the ways in addressing the numerical instability issue during the optimization process are a significant distinction between the two works. Besides, compared with the ways in addressing the instability, more important difference we think is that our approach does not employ additional projection heads. Our objective function directly operates on the output representations of the encoder, while CorInfoMax first employs a projector of 3-layer MLP to map the outputs of the encoder to a new embedding space and then calculate loss function in the new space. This distinction is not only the discrepancy in network architecture but, more importantly, it actually indicates the difference in motivations between the two works. The purpose of our research is to directly calculate mutual information under the Gaussian assumption without reliance on neural estimators or additional designs. *If our method could only work with the blessing of the additional projection heads, we would not complete this paper, which is contrary to our original motivation.*  In fact, we found the paper CorInfoMax after we had almost finished our work. There are indeed some similarities between the two works. Hence, we cited this paper and spent considerable space on relations and differences between the two works in Appendix F. We have done our best to make these statements comprehensive and objective. 

(3) The analysis of $I_G$-based solution clearly connects with the information theory point of view of CCA-SSG already developed in this paper.

*Answer:* The $I_G$-based variant is obtained from the original formula of Gaussian mutual information. In our paper, the analysis about it mainly involves two aspects. Firstly, we point out that directly optimizing $I_G$-based objective will result in numerical instability and thus introduce a strategy of offsetting and scaling eigenvalues. Secondly, we decompose Gaussian mutual information maximization into two components (conditional entropy minimization and information entropy maximization). Further, we introduce identity constraint to realizing conditional entropy minimization, which aligns with the design of our shared encoder across two views. Besides, the discussion focuses on the relationship between the encoded representations from two views *A* and *B*, that is, the two variables in the formula are respectively linked to the representations from two views.

Different from ours, CCA-SSG interprets its objective from the view of information theory, which focuses on explaining the roles of the two items in the objective function. The relationship discussed in CCA-SSG involves the encoded representations and the inputs of the encoder, that is, the two variables in the formula are respectively related to the inputs and outputs of the neural networks.

In summary, both works have analyzed their methods from the perspective of information theory, but they differ in two aspects including purposes and objects (variables).

**Question 2:** Some experimental settings and details are missing.

**Answer:** Below is our response to questions regarding experimental details and configuration.

(1) There are no clear descriptions of the architectures and hyperparameters for the results reported in Table 1.

*Answer:* The network architectures are implemented through Graph Convolutional Networks (GCNs). The hyperparameters for GMIM are as follows, where "lr" denotes learning rate and "wd" indicates weight decay:

|   Dataset   | Layers | Representation dim |  lr  |  wd  | $p_f$ | $p_e$ |
| :---------: | :----: | :----------------: | :--: | :--: | :---: | :---: |
|    Cora     |   2    |        512         | 1e-3 |  0   |  0.4  |  0.5  |
|  Citeseer   |   1    |         64         | 1e-3 |  0   |  0.4  |  0.5  |
|   Pubmed    |   2    |        512         | 1e-3 |  0   |  0.2  |  0.6  |
|  Computers  |   2    |        512         | 1e-3 |  0   |  0.1  |  0.3  |
|    Photo    |   2    |        512         | 1e-3 |  0   |  0.2  |  0.3  |
| Coauthor-CS |   2    |        512         | 1e-3 |  0   |  0.2  |  1.0  |

The hyperparameters for GMIM-IC are as follows:

|   Dataset   | Layers | Representation dim | $\beta$ |  lr  |  wd  | $p_f$ | $p_e$ |
| :---------: | :----: | :----------------: | :-----: | :--: | :--: | :---: | :---: |
|    Cora     |   2    |        512         |   1.0   | 1e-3 |  0   |  0.1  |  0.5  |
|  Citeseer   |   1    |         64         |   0.5   | 1e-3 |  0   |  0.0  |  0.6  |
|   Pubmed    |   2    |        512         |    3    | 1e-3 |  0   |  0.3  |  0.5  |
|  Computers  |   2    |        512         |    4    | 1e-3 |  0   |  0.1  |  0.3  |
|    Photo    |   2    |        512         |    7    | 1e-3 |  0   |  0.2  |  0.3  |
| Coauthor-CS |   2    |        512         |    1    | 1e-3 |  0   |  0.2  |  1.0  |

(2) The gains in terms of performance seem rather marginal compared with CCA-SSG in Table 1.

*Answer:* As pointed out by the reviewer, our method shows only marginal performance improvement compared to CCA-SSG. We discuss the theoretical relationship between the two methods in our paper, which implies that they may have similar experimental results. From this perspective, the experimental results presented in Table 1 can serve as an empirical support for the theoretical analysis, which we will state on in the experimental analysis of our revision.

(3) The paper lacks justifications for the choice of supervised evaluation. Besides, there are no experiments in semi-supervised settings or fully unsupervised evaluations.

*Answer:* After self-supervised pre-training for graph $G(\mathbf{A}, \mathbf{X})$, we obtain node representations $\mathbf{H} = [\mathbf{h}_1,...,\mathbf{h}_N]^{\top}$ and evaluate their qualities with simple linear classifier $y = \mathbf{W} x + \mathbf{b}$ under supervised settings. Good node representations should exhibit discriminability in space according to their true categories. The linear classifier under the supervised manner maps node representations to label space, and the linear classification results can well reflect the linear separability and quality of node representations. Besides, the supervised linear evaluation is a widely adopted practice in the field of self-supervised learning, including graph and computer vision. The self-supervised baselines in their papers almost universally employ linear evaluation for comparison. Thus, we also follow this practice.

Here, we evaluate the learned representations on node clustering task in an unsupervised manner, where the number of categories serves as a known parameter. The clustering results are evaluated through two metrics: Normalized Mutual Information (NMI) and Adjusted Rand Index (ARI). The compared baselines include k-means, spectral clustering, DeepWalk [1], DNGR [2], MGAE [3], DAEGC [4], DGI [5], and GRACE [6]. The experimental results are as follows:

|       Dataset       | Cora  | Cora  | Citeseer | Citeseer | Pubmed | Pubmed |
| :-----------------: | :---: | :---: | :------: | :------: | :----: | :----: |
|     **Metrics**     |  NMI  |  ARI  |   NMI    |   ARI    |  NMI   |  ARI   |
|       k-means       | 0.377 | 0.149 |  0.241   |  0.154   | 0.263  | 0.247  |
| spectral clustering | 0.265 | 0.158 |  0.082   |  0.075   | 0.136  | 0.091  |
|      DeepWalk       | 0.401 | 0.254 |  0.238   |  0.085   | 0.251  | 0.203  |
|        DNGR         | 0.318 | 0.142 |  0.180   |  0.043   | 0.153  | 0.059  |
|        MGAE         | 0.489 | 0.436 |  0.416   |  0.425   | 0.271  | 0.224  |
|        DAEGC        | 0.528 | 0.496 |  0.397   |  0.410   | 0.266  | 0.278  |
|         DGI         | 0.565 | 0.529 |  0.431   |  0.434   | 0.281  | 0.263  |
|        GRACE        | 0.556 | 0.518 |  0.377   |  0.369   | 0.251  | 0.230  |
|       GMIM-IC       | 0.578 | 0.533 |  0.441   |  0.452   | 0.303  | 0.281  |

For DeepWalk, the number of random walks is 10, the path length of each walk is 20, the context size is 10, and the number of embedding dimension is 256. For DNGR, the encoder is built with two 512-dim hidden layers and a 256-dim embedding layer. For RMSC, the trade-off parameter is set to 0.005. For MGAE, we set the number of layers, corruption level $p$, and regularization coefficient $\lambda$ to 3, 0.4, and $10^{-5}$ respectively. For DAEGC, the encoder is constructed with a 256-dim hidden layer and a 16-dim embedding layer, and the clustering coefficient is set to 10. Due to time limitation, we currently only present the results in the table. In the future, we will conduct more clustering-related experiments.

(4) There is no sensitivity analysis w.r.t the encoder.

*Answer:* We adopt simple Graph Convolutional Networks (GCNs) [7] as the encoder, which is stated in Section 6.1. The relevant supervised counterpart is listed in Table 1. The paper [8] adopts different splits of the datasets from ours, so we kindly argue that directly comparing the two works is somewhat unreasonable. The work [8] is a great job with good performance. However, in our study, we primarily focus on the performance improvement brought by self-supervised learning strategies rather than the backbone network itself.

(5) The analysis of the results is incomplete or arguable.

*Answer:* Thank you for your guidance.  In our revision, we have conducted a more detailed analysis and discussion of the experimental results. 



**Question 3:** The reviewer thinks that the dynamics with regard to representation dimension is biased by the choice of linear classifier. The representations tend to be more linear as the dimension grows. So the linear classifier would better suit these settings but it does not mean that embeddings are more informative. Besides, empirical covariance matrices would be poorer estimates of true covariance matrices given a fixed number of nodes while increasing the dimension.

**Answer:** Many thanks to the reviewer's thoughts and advices. We fully admire your perspectives. As the dimension increases, the representations become more linearly separable in high-dimensional space, naturally contributing to improved classification results. The number of nodes (i.e., empirical observations) is fixed, and as the dimension increases, it becomes more challenging to obtain an accurate empirical estimation of the true covariance matrix, which potentially hinders the effectiveness of self-supervised training in high-dimensional settings. We sincerely appreciate the reviewer's reminder, as we did not initially consider the perspective on a poorer estimation of covariance matrix. The related analysis has been added to the experimental part w.r.t representation dimensions in our revision. 

(1) Can the authors further justify the choice of linear classifier?

*Answer:* In general, we expect representations to cluster in space based on their true categories. Node classification task is employed to evaluate the linear separability and discriminative characteristic of representations. Linear classifier has limited expressive power, merely performing straightforward linear mapping. In this scenario, the  classification performance is predominantly determined by the quality of node representations themselves. In other words, the classification results are a combined outcome of the representations themselves and the classifier, and thus the results under a simple classifier are able to effectively reflect the quality of the representations. Besides, the training set for downstream evaluation is usually small. Thus, a more complex network may lead to overfitting issues, thereby impacting the analysis and discussion of the quality of node representations themselves. Moreover, the linear evaluation is widely adopted in the field of self-supervised learning including graph and computer vision. Thus, in our paper, we follow this common practice.

(2) Can the authors provide evaluations with a non-linear classifier such as 2-layer MLP with ReLU activation.

*Answer:* The related experimental results are as follows:

| Dataset         | Cora | Citeseer | Pubmed | Computers | Photo | CS    |
| --------------- | ---- | -------- | ------ | --------- | ----- | ----- |
| GMIM-IC (2-MLP) | 84.3 | 71.2     | 80.9   | 88.76     | 92.6  | 93.39 |

The performance under a 2-layer MLP is weaker than that under a linear classifier. The reason is that the node representations already possess discriminative characteristics in the space, and using a linear classifier can yield satisfactory results. Applying a more complex network may actually hinder performance due to overfitting issues.

(3) The authors are encouraged to complete Figure 2 with the other benchmarked datasets and check if there are correlations with their statistics of the datasets.

*Answer:* In our revision, we have completed Figure 2 with the Computers dataset. The reason for not plotting $I_G$-based variant is due to encountering numerical instability issues on the Computers dataset in all conducted dimensions. Among all the datasets, Pubmed has the smallest input feature dimension. Relatively speaking, the performance on this dataset shows the most significant decline with increasing dimensions. Overall, the method is not sensitive to dimensions, especially when the representation dimension exceeds 64.

**Question 4:** Some questions about the Gaussian assumption and non-Gaussian behaviour of representations.

(1) Can the authors detail experiments corresponding to visualizations of histograms in Figure 6?

*Answer:* For the node representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$, where $d$ is the number of representation dimension (channel), we randomly select several (four in Figure 6) channels for visualizations. For each channel, we visualize the histograms of the $N$ samples. Besides, we can compute mean and variance from the $N$ samples. Furthermore, we visualize a curve of a Gaussian distribution with the estimated mean and variance, which can be serve as a reference. The  histogram and the Gaussian curve exhibit a certain degree of alignment, leading us to initially think that node representations follow a Gaussian distribution. However, rigorous hypothesis testing refutes our assumption. In our revision, we have added histogram visualizations for three additional datasets. In CS and Computers dataset, the alignment between the Gaussian curve and the histogram is relatively poor. 

(2) Could the authors also check via hypothesis testing the evolution of the Gaussian behaviour w.r.t the embedding dimensions?

*Answer:* For the node representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$, we conduct hypothesis testing separately for each channel and take the average of the results from all channels as the final testing result of the entire representation matrix. The relationships between the results of hypothesis testing and representation dimensions are as follows:

| dimension | 32        | 64       | 128       | 256       | 512       | 1024      |
| --------- | --------- | -------- | --------- | --------- | --------- | --------- |
| Cora      | 2.52e-20  | 6.51e-8  | 1.48e-22  | 1.3e-17   | 2.48e-12  | 1.0e-13   |
| Pubmed    | 1.48e-118 | 1.48e-64 | 1.21e-84  | 1.69e-70  | 1.33e-57  | 1.07e-63  |
| CS        | 0.0       | 0.0      | 0.0       | 0.0       | 0.0       | 0.0       |
| Computers | 5.45e-182 | 0.0      | 1.25e-281 | 1.94e-178 | 4.39e-285 | 5.18e-181 |

A larger value indicates that the representations are closer to a Gaussian distribution. The results of the hypothesis testing do not appear to have a significant relationship with representation dimensions.

**Question 5:** Isotropic gaussian distributions are probably the best ones to promote uniformity in the embedding space so it does not seem so obvious that other prior distributions would perform better. Could the authors further discuss this point?

**Answer:** We highly agree with the reviewer's opinion. We  also do not think that other prior distributions would perform better than the Gaussian distribution. As a basic knowledge in statistics, the Gaussian distribution is the most common distribution in life and nature. Besides, the Gaussian assumption is justifiable and extensively employed in numerous disciplines such as economics, data science, and physics. More importantly, although the hypothesis test indicates that node representations do not exhibit a purely Gaussian distribution, the visualization results suggest that they present a Gaussian appearance. This phenomenon contributes to the study under the Gaussian assumption. Considering the above factors, in terms of performance and practical value, we are not optimistic that other priors can outperform the Gaussian distribution. However, deriving a closed-form solution for mutual information under specific distributions is not a effortless task. Therefore, please forgive us for not being able to provide empirical results for other prior distributions here. These deserve further exploration in a new research. In fact, the derivation of Gaussian mutual information has been a laborious endeavor in our paper, even though it might be available in existing literature. In the *future work* section of our paper, we also demonstrate the prospect of extending the Gaussian assumption to other priors, aiming to inspire interested readers.



[1] Deepwalk: Online Learning of Social Representations. SIGKDD, 2014.

[2] Deep Neural Networks for Learning Graph Representations. AAAI, 2016.

[3] Mgae: Marginalized Graph Autoencoder for Graph Clustering. CIKM, 2017.

[4] Attributed Graph Clustering: A Deep Attentional Embedding Approach. IJCAI, 2019.

[5] Deep Graph InfoMax. ICLR, 2018.

[6] Deep Graph Contrastive Representation Learning. 

[7] Semi-supervised classification with graph convolutional networks. ICLR, 2017.

[8] Revisiting heterophily for graph neural networks. NeurIPS, 2022.





Thank you again for your efforts and constructive comments. The above is our response to your questions. If we have any misunderstandings regarding your questions, please kindly point them out. We are looking forward to further communication with you.

