![](https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg)
[1]

# Can Machine Learning be Used to Generate DSMs of Varying Complexities?
__Design Structure Matrices (DSMs)__ are square matrices that display relationships between components of a system in a compact, visual, and analytically advantageous format. These matrices are typically used in the automotive, aerospace, and electronics industries for the purpose of improving system design and product architecture. The goal of this project is to use Machine Learning to develop a program that generates DSMs based on preferences provided by the user, like number of system components, system complexity, etc. Having access to substantial amounts of DSMs with varying complexities can be helpful to researchers as it can save time and resources by eliminating the need to scrape information from websites or repositories.

# Data
To achieve the goals of this research project and develop the DSM generator, a significant amount of data was needed for the purpose of training an algorithm. The dataset used includes more than 2000 DSMs. 184 of these DSMs were extracted from a repository published by Oregon State [Source](http://ftest.mime.oregonstate.edu/repo/browse/). Since a larger amount of DSMs were needed to train a neural network, the lengths of the existing DSMs were altered to generate new but similar datasets. The figure below shows a simple DSM.

![](https://upload.wikimedia.org/wikipedia/commons/3/36/A_sample_Design_Structure_Matrix_%28DSM%29.png)

_A simple DSM example_[2]

# Measuring the Complexity of a Directed Graph
Since the ultimate goal of this project was to output DSMs based on the level of complexity provided by the user, a method for measuring the complexity of DSMS was needed. DSMs are directed graphs that can be represented as adjacency matrices. This [paper](https://par.nsf.gov/servlets/purl/10165220), which describes a polynomial-based approach to calculating the complexity of graphs was used. The complexity value defined in this paper is dependent on the in and out-degree of each graph.

# The Algorithms Used
Graph generation using machine learning is a new area with great potential because graphs can provide detailed information about the inerconnectivity of components through pairwise relations between objects. Some algorithms that were looked into during the exploration phase of this project included Graph Neural Networks (GNNs), Generative Adversarial Networks (GANs), Graph Autoencoders (GAEs), and Varational Graph Autoencoders (VGAEs). After thorough exploration it was found that GNNs are typically used for analysing structural data and that GANs were typically used to generate images of the same size. These algorithms did not suit the goals of this project due to the fact that the DSMs had varying sizes and needed to be generated. At this point, GAEs and VGAEs were explored.

__Variational Auto-Encoders (VAEs)__: VAEs generate new data from the original source dataset by embeding the input X into a distribution with a mean and standard deviation. A random sample Z is taken from this distribution and used to create a new but similar data point. However, VAEs are usually implemented with image datasets and cannot be applied to graphs directly due to irregularity [3].

![](https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg)

_The Architecture of the Variational Graph Autoencoder_[4]

__Variational Graph Auto-Encoders (VGAEs)__: VGAEs are similar to VAEs but differ in the inputs that they take in as shown in the figure above. This algorithm, similar to the VAE, is composed of two parts: an encoder and a decoder. The encoder is comrpised of two __Graph Convolutional Networks (GCNs)__, which take the adjacency matrix and the feature matrix of the dataset as inputs. These inputs are run through the first layer of the GCN, which outputs a feature matrix of lower dimension. This output is then used as input for the second GCN, which gives a mean and standard deviation value for the calculation of the latent varaible, _Z_. The decoder then takes the inner product between _Z_ along with the logisitc sigmoid function to generate a new dataset. The figure below visually represents this explanation.

![image](https://user-images.githubusercontent.com/74516659/116267955-db15f580-a74a-11eb-9f8f-f4be78e1778d.png)

_A visual breakdown of VGAEs_

In order to achieve the purposes of this project, __Variational Graph Auto-Encoders (VGAEs)__ were used.

# Implementing the Algorithm
The [Spektral](https://graphneural.network/) and [PyTorch Geometric](https://pytorch-geometric.readthedocs.io/en/latest/notes/installation.html) were used to import the DSM dataset, pre-process the dataset, and train the VGAE model.

Some trouble was encountered while reading the dataset into these libraries. To continue with the goal of this project however, a placeholder [dataset](https://pytorch-geometric.readthedocs.io/en/latest/modules/datasets.html#torch_geometric.datasets.Planetoid) was used.

The placeholder dataset was used along with am existing GitHub [repository](https://github.com/AntonioLonga/PytorchGeometricTutorial) to create the encoder portion of the VGAE. Some example code for the training of the GCN has been provided below:

```Python
# Import necessary libraries
import torch
from torch_geometric.datasets import Planetoid
import torch_geometric.transforms as T
from torch_geometric.nn import GCNConv
from torch_geometric.utils import train_test_split_edges

from torch_geometric.nn import VGAE

# Create Variational GCN Encoder
class VariationalGCNEncoder(torch.nn.Module):
    def __init__(self, in_channels, out_channels):
        super(VariationalGCNEncoder, self).__init__()
        self.conv1 = GCNConv(in_channels, 2 * out_channels, cached=True) # cached only for transductive learning
        self.conv_mu = GCNConv(2 * out_channels, out_channels, cached=True)
        self.conv_logstd = GCNConv(2 * out_channels, out_channels, cached=True)

    def forward(self, x, edge_index):
        x = self.conv1(x, edge_index).relu()
        return self.conv_mu(x, edge_index), self.conv_logstd(x, edge_index)
```
To access the code for this project, go to thhis [Google Colab](https://colab.research.google.com/drive/1dC7BRLXqv-ft44fHXNSvR90wHQVaIwt1?usp=sharing) document.

# Generating DSMs
The decoder portion of this VGAE is still in progress. However, once this portion is completed, the new graphs generated can be used to achieve the goals of this project. If the user enters a complexity of 0.6, the VGAE created should generate DSMs and calculate their complexity based on the code provided in this [Google Colab](https://colab.research.google.com/drive/1ODusi118flxoX-hyRy4beeZnhTQcOU3M?usp=sharing) document. Once the model finds a generated DSM to have the same or a similar level of complexity to that specified by the user, a DSM with complexity level matching that requested by the user will be produced. This process can be repeated multiple times to generate large amounts of DSMs with varying complexities.

# References
1. https://dsmweborg.files.wordpress.com/2019/10/wuerfel_gedreht_rgb.jpg
2. https://tinyurl.com/4msbtewk
4. https://tinyurl.com/4hc4tzdb
5. https://miro.medium.com/max/1224/1*CijfkQ_NMDKsYbsN6FqCRA.jpeg
