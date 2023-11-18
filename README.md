Thank you for your positive recognition of our work and valuable feedback!



**Question 1:** While Figure 6 shows some similarity between the dataset distribution and Gaussian distribution, the slight disparity is unlikely to significantly impact model performance. Thus, this claim might be over-sell, additional evidence with alternative datasets would be valuable. Besides, it is crucial to further investigate whether the generalization performance of the representation is influenced by the Gaussian assumption.

**Answer:** In our revision, we visualize the histograms for three additional datasets: Ogbn-Arxiv, CS, and Computers. On the CS and Computers, the representations deviate noticeably from Gaussian distribution, but our proposed method still exhibits satisfactory performance on these two datasets. This can serve as empirical evidence for the effectiveness of our method in non-Gaussian scenarios.

Below, we analyze from the perspective of multi-view self-supervised learning why our method remains effective in non-Gaussian scenarios. Current multi-view learning methods can be decomposed into two complementary components: a) enhancing the consistency between representations from different views, and b) employing specific strategies to avoid collapsed solutions. The former usually brings representations from different views closer in the representation space. Among existing methods, the latter includes strategies such as negative sampling, decorrelation strategies, and asymmetric network architectures. In our paper, we demonstrate that our method can indeed achieve both effects a) and b) in Section 3.2 and 5.1, and this analysis is not conducted under the Gaussian prior, which is a crucial factor contributing to the effectiveness of our approach in non-Gaussian scenarios.

If our method indeed exhibits suboptimal performance in non-Gaussian scenarios in practical applications, a coping strategy can be to imposing probabilistic constraints on the representations to encourage them to approximate a Gaussian distribution. For a representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$ from view A or B, we first calculate mean $u_i$ and variance $v_i$ of $N$ points from the $i$-th dimension. Then, a 1-dim Gaussian distribution $p_i(x)$ based on $u_i$ and $v_i$ can be constructed. Further, we calculate the product of probabilities of $N$ samples in the $i$-th dim from $p_i(x)$, that is, $\prod_{k=1}^{N} p_i(H_{ki})$. In practice, we utilize its logarithm $\sum_{k=1}^{N} \log p_i(H_{ki})$. Considering all dimensions, we construct a loss $\mathcal{L}_{gau} = - \sum_{i=1}^{d} \sum_{k=1}^{N} \log p_i(H_{ki})$ and make representations tend towards a Gaussian distribution by minimizing $\mathcal{L}_{gau}$. It can be realized  by attaching $\mathcal{L}_{gau}$ to the original loss. After applying the above constraints, we observed that the performance nearly did not improve on the experimental datasets. The reason is that our method is not influenced by the non-Gaussian conditions on these datasets.

**Question 2:** It is necessary to provide further clarification on the underlying reason for the efficiency difference between the infoNCE and the proposed GMI.

**Answer:** In addition to the objective function, our method and InfoNCE-based methods also differ significantly in the overall network architecture. Our architecture only comprises one encoder, which maps the input space to the representation space. In contrast, infonce-based methods include an additional projection head following the encoder, which maps node representations to a new embedding space, adding computational burden and decreasing efficiency. In addition, we directly compute the loss function in the representation space while InfoNCE-based methods operate in the new embedding space. Compared to infonce-based methods, our encoder parameters are closer to the source of gradients, allowing for better optimization and, consequently, faster convergence.

**Question 3:** Given that the objective of SSL methods is to acquire a discriminative and robust representation, it is important to include visualizations of the learned representations and conduct comparisons.

**Answer:** Thank you for your suggestions. In Appendix H.6 of our revision, I have included t-SNE visualizations of our method under different configurations and compared them with other methods, offering a more profound understanding of our approach.



The above is our response to the questions in your review. Once again, we appreciate your valuable comments and suggestions.

