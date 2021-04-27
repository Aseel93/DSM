![](https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg)
[1]

# Can Machine Learning be Used to Generate DSMs of Varying Complexities?
__Design Structure Matrices (DSMs)__ are square matrices that display relationships between components of a system in a compact, visual, and analytically advantageous format. These matrices are typically used in the automotive, aerospace, and electronics industries for the purpose of improving system design and product architecture. The goal of this project is to use Machine Learning to develop a program that generates DSMs based on preferences provided by the user, like number of system components, system complexity, etc. Having access to substantial amounts of DSMs with varying complexities can be helpful to researchers as it can save time and resources by eliminating the need to scrape information from websites or repositories.

# Data
To achieve the goals of this research project and develop the DSM generator, a significant amount of data was needed for the purpose of training an algorithm. The dataset used includes more than 2000 DSMs. 184 of these DSMs were extracted from a repository published by Oregon State [Source](http://ftest.mime.oregonstate.edu/repo/browse/). Since a larger amount of DSMs were needed to train a neural network, the lengths of the existing DSMs were altered to generate new but similar datasets. The figure below shows a simple DSM.

![](https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png)

# Measuring the Complexity of a Directed Graph
Since the ultimate goal of this project was to output DSMs based on the level of complexity provided by the user, a method for measuring the complexity of DSMS was needed. DSMs are directed graphs that can be represented as adjacency matrices. This [paper](https://par.nsf.gov/servlets/purl/10165220), which describes a polynomial-based approach to calculating the complexity of graphs was used. The complexity value defined in this paper is dependent on the in and out-degree of each graph.

# The Algorithms Used
Graph generation using machine learning is a new area with great potential because graphs can provide detailed information about the inerconnectivity of components through pairwise relations between objects. Some algorithms that were looked into during the exploration phase of this project included Graph Neural Networks (GNNs), Generative Adversarial Networks (GANs), Graph Autoencoders (GAEs), and Varational Graph Autoencoders (VGAEs). After thorough exploration it was found that GNNs are typically used for analysing structural data and that GANs were typically used to generate images of the same size. These algorithms did not suit the goals of this project due to the fact that the DSMs had varying sizes and needed to be generated. At this point, GAEs and VGAEs were explored.

__Variational Auto-Encoders (VAEs)__: VAEs generate new data from the original source dataset by embeding the input X into a distribution with a mean and standard deviation. A random sample Z is taken from this distribution and used to create a new but similar data point. However, VAEs are usually implemented with image datasets and cannot be applied to graphs directly due to irregularity [3].

![](https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg)
_The Architecture of the Variational Graph Autoencoder_ [4]

__Variational Graph Auto-Encoders (VGAEs)__: VGAEs are similar to VAEs but differ in the inputs that they take in as shown in the figure above. This algorithm, similar to the VAE, is composed of two parts: an encoder and a decoder. The encoder is comrpised of two __Graph Convolutional Networks (GCNs)__, which take the adjacency matrix and the feature matrix of the dataset as inputs. These inputs are run through the first layer of the GCN, which outputs a feature matrix of lower dimension. This output is then used as input for the second GCN, which gives a mean and standard deviation value for the calculation of the latent varaible, _Z_. The decoder then takes the inner product between _Z_ along with the logisitc sigmoid function to generate a new dataset. The figure below visually represents this explanation.

(Add image)

In order to achieve the purposes of this project, __Variational Graph Auto-Encoders (VGAEs)__ were used.

# Results


# Takeaways

# References
1. https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg
2. https://tinyurl.com/4msbtewk
4. https://tinyurl.com/4hc4tzdb
5. https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg
