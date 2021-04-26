![](https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg)
[1]

# Can Machine Learning be Used to Generate DSMs of Varying Complexities?
__Design Structure Matrices (DSMs)__ are square matrices that display relationships between components of a system in a compact, visual, and analytically advantageous format. These matrices are typically used in the automotive, aerospace, and electronics industries for the purpose of improving system design and product architecture. The goal of this project is to use Machine Learning to develop a program that generates DSMs based on preferences provided by the user, like number of system components, system complexity, etc. Having access to substantial amounts of DSMs with varying complexities can be helpful to researchers as it can save time and resources by eliminating the need to scrape information from websites or repositories.

# Data
To achieve the goals of this research project and develop the DSM generator, a significant amount of data will be needed for the purpose of training an algorithm. The dataset includes more than 2000 DSMs extracted from a repository published by Oregon State [Source](http://ftest.mime.oregonstate.edu/repo/browse/). However, the DSMs downloaded from the online repository are unlabeled and do not show an indication for their complexity. While there are many studies that investigate measures of complexity, very few define complexity for directed graphs. One such study proposes a polynomial-based approach to measuring complexity of directed graphs [Paper Link](https://par.nsf.gov/servlets/purl/10165220).

![](https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png)

_Design Structure Matrix_ [2]


[Here is a link to another page](./another_page) that is also part of your site.

# Methodology
We used __Variational Auto-Encoders (VAEs)__ which could generate new data from the original source dataset. The main idea of VAE is that it embeds the input X to a distribution rather than a point and then a random sample Z is taken from the distribution rather than generated from encoder directly, but VAE deals only images. However, we cannot just apply the idea of VAE because graph-structured data are irregular. Each graph has a variable size of unordered nodes and each node in a graph has a different number of neighbors. In order to achieve our project purposes, we used __Variational Graph Auto-Encoders (VGAEs)__ which applies VAE to graph structured data to generate new graphs.
To apply VGAE, we used adjacency matrix (A) (represents DSM in our project) to represent the input graph, feature matrix (X) to present the features of each node from the input graph. The encoder of VGAE consists of Graph Convolutional Networks (GCNs). It takes an adjacency matrix and a feature matrix as input and generates the latent variable (Z) as output [3].

![](https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg)

_The Architecture of the Variational Graph Autoencoder_ [4]

# Results

# Takeaways

# References
1. https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg
2. https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png
3. https://towardsdatascience.com/tutorial-on-variational-graph-auto-encoders-da9333281129#:~:text=Variational%20graph%20autoencoder%20%28VGAE%29%20applies%20the%20idea%20of,yet%20to%20see%20a%20detailed%20tutorial%20on%20VGAE.
4. https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg
