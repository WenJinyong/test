Thank you for your detailed comments and valuable feedbacks.



**Question 1:** The reviewer does not think selecting a few dimension for three dataset would suffice either.

**Answer:** Due to space limitations, we only visualized the conditions of four dimensions. In fact, we checked many dimensions, which exhibit similar appearances. Besides, in the PDF for rebuttal, we provide visualizations for the other four datasets in Figure 1, which also exhibit a Gaussian appearance. 



**Question 2:** What is the relation between deviation form normality and overall performance? 

**Answer:** Thank you for the meaningful and interesting question! To answer your question, we first need to find a way to make the node representations deviate from the Gaussian distribution. To achieve this, we adopt the following strategy. For a representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$ from view A or B, we calculate mean $u_i$ and variance $v_i$ from  $N$ points from the $i$-th dimension. Then, we can construct an 1-dim Gaussian distribution $p_i(x)$ based on $u_i$ and $v_i$. Further, we calculate the product of probabilities of $N$ samples in the $i$-th dim from $p_i(x)$, $\prod_{k=1}^{N} p_i(H_{ki})$. In practice, we utilize its logarithm $\sum_{k=1}^{N} \log p_i(H_{ki})$. Considering all dimensions, we construct a loss $\mathcal{L}_{dev} = \sum_{i=1}^{d} \sum_{k=1}^{N} \log p_i(H_{ki})$. We can minimize $\mathcal{L}_{dev}$ to make representations deviate from normality. We attach $\alpha \cdot \mathcal{L}_{dev}$ to the original loss, where $\alpha$ controls the degree of deviation. The curves between $\alpha$ and performance are placed in Figure 3 of the PDF for rebuttal. Overall, with the increase of $\alpha$, the performance decreases. It is not sensitive to small deviations. In other words, our method allows representations to deviate from normality, which grants the method higher robustness and generalization. The reason why we don't directly construct a $d$-dim Gaussian distribution is that the empirical covariance matrix may not be positive-definite, which will lead to numerical instability.

We will incorporate the above contents into our revision as it is valuable. Thank you again for your comments. If you have any better suggestions to validate your question, please feel free to tell us. 





**Question 3:** There are many works in the literature discouraging the use public split for citation datasets. 

**Answer:** Based on your suggestions, we perform relevant experiments adopting a 1:1:8 random split for train/val/test on Cora, Citeseer, and Pubmed. The classification results are as follows:

|         | Cora | Citeseer | Pubmed |
| ------- | :--: | :------: | :----: |
| GCN     | 82.8 |   72.0   |  84.9  |
| GAE     | 76.9 |   60.6   |  82.9  |
| VGAE    | 78.9 |   61.2   |  83.0  |
| DGI     | 82.6 |   68.8   |  86.0  |
| GRACE   | 83.3 |   72.1   |  86.7  |
| GMIM-IC | 84.7 |   73.3   |  86.5  |

It is worth noting that due to time constraints, we have barely adjusted the hyperparameters. Therefore, there is still room for improvement for our method. We will include the above content in our revision.



Thank you again for your time and efforts during the review process. If you have any other suggestions or suggestions, please don't hesitate to let us know.


