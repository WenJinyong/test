Thank you for your detailed review and helpful suggestions.

**Question 1:** Authors did not compare to CCA-SSG.

**Answer:** Thank you for your reminders and recommendations. In fact, we have compared with CCA-SSG in Table 1 of the submitted version. Furthermore, we have added a description of CCA-SSG in the related work section of our revision.

**Question 2:** The intuition or motivation for the between-channel minimum dependence principle. It would be helpful to explain why this principle is important and how it relates to the quality of graph representations.

**Answer:** (1) The intuition and motivation for the between-channel minimum dependence principle are as follows:

The between-channel minimum dependence principle is designed as a complement and enhancement to the cross-view maximum consistency principle. Focusing on learning cross-view invariant representations, the consistency principle imposes no constraints on the internal state of individual representations. In other words, the adopted statistical indicators can not impose no constraints on the internal state of individual representations. Consequently, the correlation and coupling between various representation channels significantly reduce the diversity of representations. For a graph with $N=6$ nodes, we assume the representation dimension $d$ is 4. When the representation matrix $\mathbf{H}\_A$ and $\mathbf{H}\_B$ satisfy

$$\mathbf{H}\_A = \mathbf{H}\_B = \begin{matrix} -1.064 & -1.064 & -1.064 & -1.064 \\ 0.097 & 0.097 & 0.097 & 0.097 \\ 1.839 & 1.839 & 1.839 & 1.839 \\ -0.484 & -0.484 & -0.484 & -0.484 \\ -0.484 & -0.484 & -0.484 & -0.484 \\ 0.097 & 0.097 & 0.097 & 0.097 \\ \end{matrix}$$, 

the statistical indicators such as matrix correlation and distance correlation will be maximized, that is, the consistency principle is satisfied. However, various representation dimensions are totally same, which are correlated and decoupled with each other. This issue greatly undermines the diversity of representations. Based on this consideration, we propose the between-channel minimum dependence principle to compensate the limitations of the consistency principle and enhance the diversity of representations. The between-channel minimum dependence principle impose constraints on the internal state of representation matrix and make different channels  convey distinct pieces of information.

(2) The visualization and empirical illustrations for the two principles were provided.

In the **Appendix I.1** of the supplementary material, we provided t-SNE visualizations of node representations under various settings, which illustrates the effects of the two principles. In the **Appendix I.2** of the supplementary material, we visualize the correlation matrices under various settings, whose results show that various representation dimensions can be decorrelated well with the between-channel minimum dependence principle. Besides, the toy experiments in the **Appendix F** of the supplementary material also demonstrate the effects of the two strategies of the between-channel minimum dependence principle.





The above is our response to your existing concerns. If you have any other questions, please feel free to tell us. We enjoy communicating with you.

