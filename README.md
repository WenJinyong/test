Thank you for your constructive review and valuable feedback.

**Question 1:** The theoretical claims such as Property 1 are well known facts, and the relevant statements should be improved.

**Answer:** In fact, before crafting this response, I conducted a survey among some of my peers, and it turns out that some of them are not familiar with these theorems or properties. In order to facilitate a better understanding of our paper for those who are not familiar with these concepts and to maintain the self-sufficiency of our article, we decided to retain these contents. Besides, we follow your suggestions to improve the relevant statements such as emphasizing the data $\mathbf{H}$ has been de-centered in Property 1. We sincerely appreciate the valuable suggestions you have provided to enhance our paper.



**Question 2:** Some details are missing, for example, how was minimizing $\mathcal{L}\_{sr}$ (i.e., Eq. (14)) implemented. 

**Answer: ** In the **Appendix K** of the supplementary material, we provided PyTorch-style pseudocode of the detailed implementations of the four statistical indicators and the two decorrelation strategies. For the convenience of the reviewer, we represent the implementation details of $\mathcal{L}\_{sr}$ here, which is described in the **Algorithm 6** of the supplementary material.

```python
# H_A: representations from view A, shape=[N,d]
# H_B: representations from view B, shape=[N,d]

def loss_SR(H_A, H_B):
    N = H_A.shape[0]  # number of nodes
    
    # calculate covariance matrix
    c_A = torch.mm(H_A.T, H_A) / N 
    c_B = torch.mm(H_B.T, H_B) / N 
    
    eigvals_A = torch.linalg.eigvals(c_A).float()
    std_A = torch.std(eigvals_A)
    eigvals_B = torch.linalg.eigvals(c_B).float()
    std_B = torch.std(eigvals_B)
	
    loss_sr = std_A + std_B
    return loss_sr
```

Based on the above algorithm, we can obtain $\mathcal{L}\_{sr}$ and then minimizing it directly. In addition, we will open-source our code to help readers better understand our paper and to expand the impact of our work. If necessary, we can also provide the code now. We are primarily concerned about the potential impact on anonymity due to uncertain factors such as hidden files in the code repository.



**Question 3:** The paper should present computational complexity analysis.

**Answer: ** Assuming the number of nodes is $N$ and the representation dimension is $d$, the computational complexity of Matrix Correlation is $\mathcal{O}(d^2 N)$. The complexity of Distance Correlation, HSIC, and RV-coefficient is about $\mathcal{O}(N^2 d)$. The complexity of  Direct Channel Decorrelation is $\mathcal{O}(d^2 N)$. The complexity of Spectral Regularization is about $\mathcal{O}(d^2 N)+\mathcal{O}(d^3)$. The above operations have excellent parallelism and can be computed very quickly with the support of GPUs.

By the way, the process of realizing the two principles actually involves statistical estimation. It is not necessary to adopt all nodes on the graph. We sample a subset of all nodes, whose indices are referred to as $idx$. Thus, we can obtain the sampled representation matrices $\mathbf{H}\_A[idx]$ and $\mathbf{H}\_B[idx]$, which can be used to realize the two principles. Some experimental results after sampling 50% nodes are as follows: 

| Dataset             | Cora           | Citeseer       | Pubmed         | Computers        | Photo            |
| ------------------- | -------------- | -------------- | -------------- | ---------------- | ---------------- |
| MC-DCD (100% nodes) | 84.5 $\pm$ 0.3 | 73.6 $\pm$ 0.3 | 81.7 $\pm$ 0.3 | 88.70 $\pm$ 0.31 | 93.14 $\pm$ 0.15 |
| MC-DCD (50% nodes)  | 84.4 $\pm$ 0.3 | 73.6 $\pm$ 0.3 | 81.5 $\pm$ 0.4 | 88.64 $\pm$ 0.37 | 93.10 $\pm$ 0.17 |

| Dataset            | Cora           | Citeseer       | Pubmed         | Computers        | Photo            |
| ------------------ | -------------- | -------------- | -------------- | ---------------- | ---------------- |
| MC-SR (100% nodes) | 84.4 $\pm$ 0.4 | 73.5 $\pm$ 0.4 | 81.5 $\pm$ 0.4 | 87.78 $\pm$ 0.25 | 93.09 $\pm$ 0.14 |
| MC-SR (50% nodes)  | 84.3 $\pm$ 0.5 | 73.4 $\pm$ 0.4 | 81.3 $\pm$ 0.5 | 87.69 $\pm$ 0.28 | 93.06 $\pm$ 0.16 |

We can observe that the results after sampling do not exhibit significant differences compared to the results using all nodes.





Thank you very much for your efforts during the review process, which are greatly helpful for improving our article. If you have any other suggestions or concerns, please feel free to tell us. We look forward to further discussion with you.

