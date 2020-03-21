## Sparse K-Means

Most people are familiar with the [k-means algorithm](https://towardsdatascience.com/k-means-clustering-algorithm-applications-evaluation-methods-and-drawbacks-aa03e644b48a), a relatively simple, iterative approach to clustering. However, k-means is not robust to the scenario of high-dimensional data where only a few of the many features available are relevant. We can see an example of this in the following simulation. 

Suppose we generate p-dimensional vectors <img src="https://render.githubusercontent.com/render/math?math=\boldsymbol{y}_i = (x_{i1}, \ldots, x_{i100})"> belonging to one of three clusters. In cluster 1, <img src="https://render.githubusercontent.com/render/math?math=x_{i1},x_{i2} \sim \mathcal{N}(0,1)">, in cluster 2, <img src="https://render.githubusercontent.com/render/math?math=x_{i1},x_{i2} \sim \mathcal{N}(4,1)">, and in cluster 3, <img src="https://render.githubusercontent.com/render/math?math=x_{i1},x_{i2} \sim \mathcal{N}(-4,1)">. Across all three clusters, we allow all other features besides these first two to be generated from a uniform distribution on the interval (-4,4). In other words, only these first two features distinguish the three clusters from one another, and the remaining 98 features are just noise. 

We can see this visually. Looking only at the first two features, the three clusters are visually separable: 

However, looking at any other two features, for example the 3rd and 4th, we no longer see such clear visual separation:

If we apply a clustering algorithm, we would ideally hope to see clustering done along those first two features, and ignoring the remaining noisy 98. Unfortunately, if we just directly apply k-means, we get the following result:


Clearly, k-means is not robust to the noise present here. We can gain some intuition for why this occurs from looking at the k-means objective function: 

It's this lack of robustness that motivates the sparse k-means clustering algorithm, which can identify the important features and ignore the noisy ones.
