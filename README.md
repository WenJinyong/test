Thank you for your detailed comments and valuable feedbacks.



**Question 1:** For the Gaussian assumption, only selecting a few dimensions for three dataset would not suffice.

**Answer:** Due to space limitations, we only visualized the conditions of four dimensions in our manuscript. In fact, we checked many dimensions, which exhibit similar appearances as the visualized ones. Besides, in Figure 1 of the PDF for rebuttal, we provide visualizations for other four datasets including CS, Ogbn-Arxiv, Physics and Computers, which also exhibit Gaussian appearance. Regarding the Gaussian assumption, we further engage in a relevant discussion in our response to your next question.



**Question 2:** What is the relation between deviation from normality and overall performance? 

**Answer:** Thank you for the meaningful and interesting question! To answer your question, we first need to find a way to make the node representations deviate from the Gaussian distribution. To achieve this, we adopt the following strategy. For a representation matrix $\mathbf{H} \in \mathbb{R}^{N \times d}$ from view A or B, we calculate mean $u_i$ and variance $v_i$ from  $N$ points from the $i$-th dimension. Then, we can construct an 1-dim Gaussian distribution $p_i(x)$ based on $u_i$ and $v_i$. Further, we calculate the product of probabilities of $N$ samples in the $i$-th dim from $p_i(x)$, that is, $\prod_{k=1}^{N} p_i(H_{ki})$. In practice, we utilize its logarithm $\sum_{k=1}^{N} \log p_i(H_{ki})$. Considering all dimensions, we construct a loss $\mathcal{L}_{dev} = \sum_{i=1}^{d} \sum_{k=1}^{N} \log p_i(H_{ki})$. We can minimize $\mathcal{L}_{dev}$ to make representations deviate from normality. We attach $\alpha \cdot \mathcal{L}_{dev}$ to the original loss, where $\alpha$ controls the degree of deviation. The curves between $\alpha$ and performance are placed in Figure 3 of the PDF for rebuttal. Overall, with the increase of $\alpha$, the performance decreases. However, it is not sensitive to small deviations. In other words, our method allows representations to deviate from normality, which grants the method higher robustness and broader application scenarios. In summary, although our method is derived and proposed under the Gaussian assumption, it remains effective even when the representations deviate moderately from Gaussian distribution. The reason why we don't directly construct a $d$-dim Gaussian distribution is that the empirical covariance matrix may not be positive-definite, which will lead to numerical instability.

We will incorporate the above contents into our revision as it is indeed valuable. Thank you again for your constructive comments. If you have any better suggestions to validate your question, please feel free to tell us. 





**Question 3:** There are many works in the literature discouraging to use public split for citation datasets. 

**Answer:** Based on your suggestions, we perform relevant experiments adopting a 1:1:8 random split for train/val/test on Cora, Citeseer, and Pubmed. The classification results are as follows:

|                | Cora | Citeseer | Pubmed |
| -------------- | :--: | :------: | :----: |
| GCN            | 82.8 |   72.0   |  84.9  |
| GAE            | 76.9 |   60.6   |  82.9  |
| VGAE           | 78.9 |   61.2   |  83.0  |
| DGI            | 82.6 |   68.8   |  86.0  |
| GRACE          | 83.3 |   72.1   |  86.7  |
| GMIM-IC (ours) | 84.7 |   73.3   |  86.5  |

It is worth noting that due to time constraints, we have barely adjusted the hyperparameters of our method. Therefore, there is still room for improvement for our method. We will include the above content in our revision.



Thank you again for your time and efforts during the review process. If you have any other suggestions or questions, please don't hesitate to let us know.

