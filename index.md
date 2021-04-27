![](https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg)
[1]

# Can Machine Learning be Used to Generate DSMs of Varying Complexities?
__Design Structure Matrices (DSMs)__ are square matrices that display relationships between components of a system in a compact, visual, and analytically advantageous format. These matrices are typically used in the automotive, aerospace, and electronics industries for the purpose of improving system design and product architecture. The goal of this project is to use Machine Learning to develop a program that generates DSMs based on preferences provided by the user, like number of system components, system complexity, etc. Having access to substantial amounts of DSMs with varying complexities can be helpful to researchers as it can save time and resources by eliminating the need to scrape information from websites or repositories.

# Data
To achieve the goals of this research project and develop the DSM generator, a significant amount of data was needed for the purpose of training an algorithm. The dataset used includes more than 2000 DSMs. 184 of these DSMs were extracted from a repository published by Oregon State [Source](http://ftest.mime.oregonstate.edu/repo/browse/). Since a larger amount of DSMs were needed for the 

# Measuring Complexity of a Directed Graph
However, the DSMs downloaded from the online repository are unlabeled and do not show an indication for their complexity. While there are many studies that investigate measures of complexity, very few define complexity for directed graphs. One such study proposes a polynomial-based approach to measuring complexity of directed graphs [Paper Link](https://par.nsf.gov/servlets/purl/10165220).

![](https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png)

_Design Structure Matrix_ [2]

# Methodology
 __Variational Auto-Encoders (VAEs)__: VAEs generate new data from the original source dataset by embeding the input X to a distribution with a mean and standard deviation. A random sample Z is taken from this distribution and used to creat a new but similar data point. However, VAEs are usually implemented with image datasets and cannot be applied to graphs directly due to irregularity. In order to achieve our project purposes, we used __Variational Graph Auto-Encoders (VGAEs)__, which applies VAE to graph structured data for the purpose of generating new graphs.
To apply VGAE, we used adjacency matrix (A) (represents DSM in our project) to represent the input graph, feature matrix (X) to present the features of each node from the input graph. The encoder of VGAE consists of Graph Convolutional Networks (GCNs). It takes an adjacency matrix and a feature matrix as input and generates the latent variable (Z) as output [3].

![](https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg)

_The Architecture of the Variational Graph Autoencoder_ [4]

# Results

# Takeaways

# References
1. https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg
2. https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png
4. https://towardsdatascience.com/tutorial-on-variational-graph-auto-encoders-da9333281129#:~:text=Variational%20graph%20autoencoder%20%28VGAE%29%20applies%20the%20idea%20of,yet%20to%20see%20a%20detailed%20tutorial%20on%20VGAE.
5. https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg
