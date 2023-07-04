Thank you for your constructive review and valuable suggestions.

**Question 1:** The principles introduced in the paper are common in self-supervised framework. How dose the graph structure make it necessary and difficult to apply in GNNs?

**Answer:** (1) Facing large-scale graphs, how to realize the two principles efficiently is an important topic. As described in the Answer 3 for reviewer *URJB*, our methods still maintain high performance under the condition of sampling only a subset of nodes, which greatly improves computational efficiency.

(2) Graph contrastive learning follows the technical route of multi-view learning and obtains multiple views through data augmentation. How to fully explore and utilize the graph structure during the data augmentation process is a critical topic.

(3) The message aggregation process controlled by graph structure in GNNs potentially smoothens node representations, which facilitates discriminative representations [1]. As described in the Appendix G of the supplementary material, the decorrelation principle can potentially play a role of smoothening node representations, which facilitates good node representations.

[1] Deeper Insights Into Graph Convolutional Networks for Semi-Supervised Learning. AAAI, 2018.



**Question 2:** The data augmentation method are limited in dropping edges for topology or feature masking. Adding a certain number of edges as noise or fake edges to augment the graph can be considered. 

**Answer:** Thank you very much for your suggestions. In the past few days, we performed relevant experiments by adding a certain number of edges randomly to augment the graph. Some experimental results are as follows:

| Dataset               |      Cora      |    Citeseer    |     Pubmed     |
| :-------------------- | :------------: | :------------: | :------------: |
| MC-DCD                | 84.5 $\pm$ 0.3 | 73.6 $\pm$ 0.3 | 81.7 $\pm$ 0.3 |
| MC-DCD + adding edges | 83.9 $\pm$ 0.4 | 73.1 $\pm$ 0.5 | 80.9 $\pm$ 0.5 |

| Dataset              |      Cora      |    Citeseer    |     Pubmed     |
| :------------------- | :------------: | :------------: | :------------: |
| MC-SR                | 84.4 $\pm$ 0.4 | 73.5 $\pm$ 0.4 | 81.5 $\pm$ 0.3 |
| MC-SR + adding edges | 83.7 $\pm$ 0.6 | 72.9 $\pm$ 0.5 | 80.6 $\pm$ 0.4 |

 We can observe that adding a certain number of edges randomly to augment a graph would weaken the performance. We hypothesize that the reason is that randomly added edges would establish connections between nodes of different classes. This leads to these nodes to be pulled close to each other in the representation space during the process of message aggregation of graph neural networks, which hinders the discriminability of node representations and results in weaker performance. Inspired by your reviews, we are considering to augment a graph by adding a certain number of edges between second-order neighbors and are conducting related experiments.





Thank you again for your time and efforts during the review process. If you have any other suggestions or concerns, please don't hesitate to let us know.

