Thank you for your valuable comments and insightful suggestions.



**Question 1:** There is a lack of code for evaluating the reproducibility.

**Answer:** According to the guidelines of NeurIPS 2023 for rebuttal, we submitted an anonymous link to Area Chair, which includes our code.



**Question 2:** How to extend the proposed method to images and texts? 

**Answer:** As mentioned in the Limitation part of Section 7, our method is derived and proposed under the Gaussian assumption. Therefore, to apply the proposed method to images and texts, it may be required for their output representations to potentially follow a Gaussian distribution. If the representations do not satisfy such conditions, one feasible approach is to impose additional probabilistic constraints to encourage the representations to conform to a Gaussian distribution. To achieve this, we adopt the following strategy. For a representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$ from view A or B, we first calculate mean $u_i$ and variance $v_i$ of $N$ points from the $i$-th dimension. Then, an 1-dim Gaussian distribution $p_i(x)$ based on $u_i$ and $v_i$ can be constructed. Further, we calculate the product of probabilities of $N$ samples in the $i$-th dim from $p_i(x)$, that is, $\prod_{k=1}^{N} p_i(H_{ki})$. In practice, we utilize its logarithm $\sum_{k=1}^{N} \log p_i(H_{ki})$. Considering all dimensions, we construct a loss $\mathcal{L}_{gau} = - \sum_{i=1}^{d} \sum_{k=1}^{N} \log p_i(H_{ki})$ and make representations tend towards a Gaussian distribution by minimizing $\mathcal{L}_{gau}$. It can be realized  by attaching $\kappa \cdot \mathcal{L}_{gau}$ to the original loss, where $\kappa$ is a weighted coefficient. As  mentioned in Section 7, due to limited computational resources, we regret that we cannot conduct relevant experiments on images.





**Question 3:** Can the authors evaluate the proposed method on graph classification tasks? 

**Answer:** In order to evaluate the method on graph classification tasks, a slight modification needs to be made to the model architecture. We incorporate a graph global-pooling function to obtain the graph-level representations. In particular, we use the concatenated results of MaxPooling and MeanPooling for the graph global-pooling function. For evaluation, we feed the learned graph-level representations into a downstream LIBSVM [1] classifier and report the mean accuracy of 10 results. The classification results are as follows:

| Dataset        | PROTEINS [2] | MUTAG [2] | IMDB-B [2] |
| -------------- | :----------: | :-------: | :--------: |
| InfoGraph [3]  |     74.8     |   89.0    |    73.0    |
| GraphCL [4]    |     74.4     |   89.8    |    71.1    |
| CLEAR [5]      |     76.1     |    --     |    72.5    |
| HGCL [6]       |     75.5     |   90.1    |    73.9    |
| GMIM-IC (ours) |     75.3     |   90.4    |    73.6    |

Due to time constraints, we did not extensively tune the hyperparameters. There is still room for improvement in the performance of our method.

[1] LIBSVM: a library for support vector machines.

[2] Deep graph kernel.

[3] Infograph: Unsupervised and semi-supervised graph-level representation learning via mutual information maximization.

[4] Graph contrastive learning with augmentations.

[5] CLEAR: Cluster-Enhanced Contrast for Self-Supervised Graph Representation Learning.

[6] Unsupervised graph-level representation learning with hierarchical contrasts.


