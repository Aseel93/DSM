![](https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg)

# Summery 
Design Structure Matrices (DSMs) are square matrices that display relationships between components of a system in a compact, visual, and analytically advantageous format. These matrices are typically used in the automotive, aerospace, and electronics industries for the purpose of improving system design and product architecture. The goal of this project is to use Machine Learning to develop a program that generates DSMs based on preferences provided by the user, like number of system components, system complexity, etc. Having access to substantial amounts of DSMs with varying complexities can be helpful to researchers as it can save time and resources by eliminating the need to scrape information from websites or repositories.

# Data
To achieve the goals of this research project and develop the DSM generator, a significant amount of data will be needed for the purpose of training an algorithm. The dataset includes more than 2000 DSMs extracted from a repository published by Oregon State [Source](http://ftest.mime.oregonstate.edu/repo/browse/). However, the DSMs downloaded from the online repository are unlabeled and do not show an indication for their complexity. While there are many studies that investigate measures of complexity, very few define complexity for directed graphs. One such study proposes a polynomial-based approach to measuring complexity of directed graphs [Paper Link](https://par.nsf.gov/servlets/purl/10165220).


[Here is a link to another page](./another_page) that is also part of your site.

# Methodology
We used Variational Auto-Encoders (VAEs) which could generate new data from the original source dataset. The main idea of VAE is that it embeds the input X to a distribution rather than a point and then a random sample Z is taken from the distribution rather than generated from encoder directly, but VAE deals only images. However, we cannot just apply the idea of VAE because graph-structured data are irregular. Each graph has a variable size of unordered nodes and each node in a graph has a different number of neighbors. In order to achieve our project purposes, we used Variational Graph Auto-Encoders (VGAEs) which applies VAE to graph structured data to generate new graphs.
To apply VGAE, we used adjacency matrix (A) (represents DSM in our project) to represent the input graph, feature matrix (X) to present the features of each node from the input graph. The encoder of VGAE consists of Graph Convolutional Networks (GCNs). It takes an adjacency matrix and a feature matrix as input and generates the latent variable (Z) as output.

![The Architecture of the Variational Graph Autoencoder](Picture 1.png)

# Takeaways
__A final section summarizes big takeaways in a concise format__
- Puppies are cute
- Smoler = cuter
- Future work should investigate how smol is too smol

# References

1. https://images7.memedroid.com/images/UPLOADED185/563b5bffa94d6.jpeg
2. 
3. 
4. 
