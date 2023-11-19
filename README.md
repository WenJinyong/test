Thank you for your thorough review and constructive feedback!



**Question 1:** The paper is not clear on the graph context. Why is the paper limited in scope to graph data? Besides, the introduction part does not specify whether the data is the graph or the nodes.

**Answer:** As stated in Appendix E, visualized histograms of *node representations* and the Gaussian assumption provided the initial motivation for our research, so we naturally regard (node representations on) graphs as objects. We believe that our approach can be extended to image data, but visual self-supervision typically relies on significant computational resources. Regrettably, the resources available to us do not permit us to conduct relevant experimental studies. This point was also highlighted in the *Limitations* section of the initial submission.

Thank you for your reminder about the unclear description. The data is nodes on the graph. In our revised version, we have employed the terms such as "node-level" and "node representations" at multiple places to indicate this point. Additionally, we have added more descriptions of crucial issues such as the composition of the encoder.

**Question 2:** Why does Property 2 potentially suggest that the unevenness of the eigenvalues of the covariance matrix leads to the issue of dimensional collapse?

**Answer:** We have provided a detailed explanation of this question in the red paragraph on page 17 of our revision.

**Question 3:** The authors should directly compare the proposed method with CorInfoMax [1].

**Answer:** In Table 1 of our revision, we add CorInfoMax as a baseline. When conducting related experiments, we adopt the same encoder architecture for CorInfoMax as ours. CorInfoMax falls behind our method in performance. Our method directly optimizes Gaussian mutual information in the representation space, while CorInfoMax adds an additional projection head following the encoder. This component is somewhat redundant and hinders the direct optimization of representations.

**Question 4:** Some questions and issues regarding comparison to previous works and experimental settings.

(1) To be truly self-supervised learning, a validation set would not be available. Is a grid search employed for hyper-parameter selection via a validation?

*Answer:* Based on a validation set in the downstream node classification task, we conduct a grid search for hyper-parameters of the proposed method in our experiments. In our paper, all self-supervised baselines go through such a process. *During the self-supervised pretraining process, no labels are involved in the training.*

Indeed, as you mentioned, the truly self-supervised learning should not have access to a validation set. However, in most existing literatures including classical works in both **vision and graph fields** (e.g., MAE, GRACE, and CCA-SSG), a hyper-parameter search is performed based on a validation of downstream task. In other words, they also do not achieve truly self-supervised learning. We think that this issue is primarily due to the huge gap between self-supervised proxy tasks and downstream tasks such as classification in the graph and vision fields. A well-performed self-supervised proxy task (e.g., a small InfoNCE loss) does not guarantee that the pre-trained model will still perform well on downstream classification tasks. Therefore, it is often necessary to perform hyper-parameter search based on the validation set of downstream tasks. Without relying on a validation set, constructing specific metrics or strategies to measure the effectiveness of self-supervised pretraining remains an important under-explored research problem. This is also a significant reason why the research on self-supervised learning in the fields of vision and graph lags behind that in the NLP. In NLP, proxy tasks like masked language modeling align well with downstream applications such as question-answering. Generally speaking, the issue the reviewer points out is actually one that the entire self-supervised learning community for graph and vision is facing and actively seeking solutions for.

(2) How are hyper-parameter searched? What are the details of the linear classifier?

*Answer:* The hyper-parameters are searched by a grid search as follows:

representation dimension: [64, 128, 256, 512]

$p_f$: [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6]

$p_e$: [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6]

trade-off factor $\beta$: [0.5, 1, 2, 3, 4, 5, 7, 10]

It is worth noting that when conducting sensitivity analysis for specific hyper-parameters, in order to make the experiments more thorough, the hyper-parameter settings will have a higher granularity than grid search.

After self-supervised pre-training, we can obtain node representations $\mathbf{H} = [\mathbf{h}_1,...,\mathbf{h}_N]^{\top}$ and evaluate their qualities with simple linear classifier $y = \mathbf{W} x + \mathbf{b}$, where $\mathbf{W}$ and $\mathbf{b}$ denote learnable parameters. The linear classifier realize mapping from representation space into label space and is used to assess the linear separability of representations.

(3) The augmentation intensities $p_f$ and $p_e$ have to be selected and the experimental results show that these also have a large effect.

*Answer:* Indeed, the augmentation intensity has a great influence on performance, which have been explored in a previous work [3]. In fact, we can observe that, when $p_f$ in [0.2, 0.4] and $p_e$ in [0.0, 0.6], the performance keep relatively stable and good.

(4) Are competing baselines using defaults or do they also enjoy a hyper-parameter search?

*Answer:* Based on the official codes of the baselines, we perform a hyper-parameter search to obtain their best results. For instance, in the case of GRACE, the official code is used to conduct experimental evaluations on random splits of Cora, Citeseer, and Pubmed. The given hyper-parameters perform poorly on the public splits, and we obtained the reported results in our paper after conducting a hyper-parameter search.

**Question 5:** In terms of writing, there are some typos and issues.

**Answer:** Thank you for your careful reading and detailed comments very much! We have corrected the typos and issues in our revised version based on your feedback. Here are a few points that need special clarification.

(1) The discussion of Proposition 3 about distributions on hyper-spheres can be related to Gaussian distribution.

*Answer:* Thank you for your suggestions! However, while preparing this rebuttal, we have not fully comprehended how the data points adhere to a Gaussian distribution on the hypersphere. For example, in the case of a two-dimensional space, the data points on a unit circle appear to be unable to conform to a Gaussian distribution. The paper [2] abandons the commonly used Gaussian prior and instead turns to a hyperspherical latent space. If you have any further suggestions or ideas, please do not hesitate to tell us.

(2) What does "as a pivot to elucidate" means?

*Answer:*  GMIM-IC is a contrastive objective derived from maximizing Gaussian Mutual Information. Here, "as a pivot to elucidate" means that we will demonstrate the relationship between contrastive methods  and decorrelation-based methods using GMIM-IC as an *intermediary* .

**Question 6:** More discussions of uncorrelated Gaussians in auto-encoders, independent component analysis, and blind source separation are expected.

**Answer:** Our method expects to enforce the representations to achieve an isotropic Gaussian distribution with the aim of decoupling various dimensions and learning diverse representations.

Conventional Independent Component Analysis (ICA) or Blind Source Separation (BSS) thinks that the observed mixed signals are obtained through a linear combination of source signals and aims to recover latent variables from observations. The traditional ICA assumes that the source signals follow non-Gaussian distributions and are statistically independent. The assumption of statistical independence among latent variables is, in fact, a decoupling or independence constraint. Non-linear ICA posits that the observed signals are obtained through a nonlinear transformation of the source signals. 

In variational auto-encoders (VAE), there is a term used to minimize the KL divergence between the variational posterior and the prior distribution. The chosen prior distribution is typically selected to satisfy certain independent properties, such as an isotropic Gaussian distribution. As a result, the KL divergence term potentially imposes a decoupling constraint on the latent variables. The $\beta$-VAE [4] multiplies the KL divergence term by a coefficient to enhance the decoupling effect on the latent variables. The KL divergence term and the entropy maximization term in our paper share a similar underlying principle. Similar to decorrelation-based self-supervised learning methods such as CCA-SSG, DIP-VAE [5] directly regularizes the elements in the covariance matrix of the posterior distribution, making it approach the identity matrix. Generally speaking, research on disentangled representation learning in VAEs mainly focuses on improving the KL divergence term or finding its alternatives.

We are currently organizing the content related to this question. We are conducting more extensive research and discussions, and  will integrate the relevant content into our revision.



[1] Self-supervised learning with an information maximization criterion. NeurIPS 2022.

[2] Hyperspherical variational auto-encoders. UAI, 2018.

[3] What makes for good views for contrastive learning? NeurIPS, 2020.

[4] beta-vae: Learning basic visual concepts with a constrained variational framework. ICLR, 2016.

[5] Variational inference of disentangled latent concepts from unlabeled observations. ICLR, 2018.



Thank you again for your detailed and valuable comments. The above is our response to your questions, and we are looking forward to further discussions with you.













