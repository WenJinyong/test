Thank you for your critical comments and valuable review, which are crucial for improving our paper.



**Question 1:** The appearance of the idea and formulation is same as a recent article [1].

**Answer:** Thank you for your recommendation. Over the past few days, we have thoroughly read this article, word by word. We acknowledge the presence of similarities in equations between our paper and the article [1], but they still exhibit essential differences.

(1) The objects operated by loss functions are different. Our loss function directly operates on the **output representations of the encoder** $f(\cdot)$. As shown in Figure 2 of [1], [1] first **utilizes a projector of 3-layer MLP to map the outputs of the encoder** $f(\cdot)$ **to a new embedding space**, and then calculate loss function in the new space. Our approach reduces model capacity and enhances efficiency by directly optimizing the output space of the encoder. The differences between the two approaches not only result in distinct model structures but, more importantly, lead to significant disparities in motivations and ideas. The raw mutual information (MI) is hard to calculate directly from data and its acquisition usually relies on addition projectors and estimators, giving rise to a series of works like InfoNCE. As mentioned multiple times in our paper (e.g., line 9, 58, 155, 157), the reason for adopting Gaussian MI is because it can be directly calculated from empirical data without introducing additional network architecture, which is the fundamental motivation and starting point of our research. **The projectors introduced in [1] completely deviates from our initial motivation.** Based on GMIM-IC, the following results show that the performance degrades when adding similar projectors as in [1].

|                     | Cora           | Citeseer       | Pubmed         |
| ------------------- | -------------- | -------------- | -------------- |
| GMIM-IC             | 84.6 $\pm$ 0.5 | 73.8 $\pm$ 0.4 | 81.8 $\pm$ 0.6 |
| GMIM-IC + projector | 82.9 $\pm$ 0.4 | 72.3 $\pm$ 0.5 | 80.6 $\pm$ 0.5 |

(2) An important issue we addressed in the paper is that directly incorporating the logarithm of the determinant of the covariance matrix in the objective function can lead to numerical instability, which is detailedly analyzed and discussed in lines 168-176 of the main text and Appendix E. To cope with this issue, we adopt the strategy of **offsetting and scaling eigenvalues to be around 1**. [1] turns to **adding a disturbance** in Eq. (6). The comparison between the two strategies are placed in Figure 4 of the PDF for rebuttal. When dimensions are higher than 128, the train process under the strategy of adding disturbance was terminated due to numerical instability, because it cannot change the fact that many eigenvalues remain very close to 0.

(3) We establish connections between contrastive and decorrelation-based methods, providing an explanation for decorrelation-based methods from the perspective of MI maximization. These contributions are of significant importance in establishing a unified theoretical framework for self-supervised learning methods. [1] does not involve these aspects.

(4) In Section 5.1, we theoretically demonstrate from the perspective of eigen spectrum that entropy maximization term can prevent dimensional collapse. In Section 5.2, we show that InfoNCE potentially maximize information entropy. These contents go beyond the scope of [1].

We appreciate your recommendation for this article. In our revision, we will devote significant space to describing their differences in detail. Emphasizing these distinctions will not only help understand our paper but also highlight key points of our research. Moreover, it also reflects the respect that should be given to [1]. We genuinely hold the view that the significance of a new work resides in its potential to offer valuable insights and benefits to its readers. Despite some similarities between the two works, we believe that our research still makes substantial contributions.

[1] Self-supervised learning with an information maximization criterion.



**Question 2:** Lemma 2-3 are well-known facts. 

**Answer:** Yes, they are well-known and can be easily derived based on linear algebra knowledge. We put them in the appendix to assist in the proofs of other theorems, rather than considering them as the main contributions of this paper.



**Question 3:** Is there a constraint on the boundedness of eigenvalues of the covariance matrix in Proposition 2? Is it an unbounded maximization problem?

**Answer:** We don't make any constraints on eigenvalues. According to Property 2, an eigenvalue is equal to the variance along the corresponding principle direction of data $\mathbf{H}$, which is always greater than 0. In other words, the magnitude of eigenvalues is determined by the appearance of the data distribution. However, as Section 3.1 describes, representation matrices are normalized to 0-mean and 1-standard deviation along sample direction.  For the covariance matrix $\mathbf{\Sigma}=\frac{1}{N}\mathbf{H}^{\top}\mathbf{H}$, its trace is $d$, which is equal to the sum of all eigenvalues. **This can be regarded as an implicit constraint on eigenvalues (no constraints are applied to individual eigenvalues but we restrict their sum to a constant $d$).** Based on the proof process of Proposition 2, we can know $0 \leq \det(\mathbf{\Sigma}) \leq 1$, that is, $\log \det(\mathbf{\Sigma}) \in (-\infty,0]$, which **has a upper bound**. The similar discussion can be applied to $\det(\mathbf{I} + \eta \cdot \mathbf{\Sigma})$. Thus, Proposition 2 is a bounded maximization problem.



We sincerely appreciate your time and constructive suggestions. Thank you for your valuable contributions to our work.

