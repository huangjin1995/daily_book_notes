cs231n



#### paper

+ GoogleNet - Going Deeper with Convolutions, Christian Szegedy, Wei Liu, Yangqing Jia, Pierre Sermanet, Scott Reed, Dragomir Anguelov, Dumitru Erhan, Vincent Vanhoucke, Andrew Rabinovich, CVPR 2014 [arxiv](https://arxiv.org/abs/1409.4842) 
+ 



ImageNet Large Scale Visual Recognition Challenge (ILSVRC) winners

AlexNet (2012) - ZFNet (2013) - VGG (2014) - GoogleNet (2014) - ResNet (2015)



#### AlexNet

Details/Retrospectives:
- first use of ReLU
- used Norm layers (not common anymore)
- heavy data augmentation
- dropout 0.5
- batch size 128
- SGD Momentum 0.9
- Learning rate 1e-2, reduced by 10 manually when val accuracy plateaus
- L2 weight decay 5e-4
- 7 CNN ensemble: 18.2% -> 15.4%



Historical note: 

Trained on GTX 580 GPU with only 3 GB of memory. Network spread across 2 GPUs, half the neurons (feature maps) on each GPU.

#### ZFNet

AlexNet but:
CONV1: change from (11x11 stride 4) to (7x7 stride 2)
CONV3,4,5: instead of 384, 384, 256 filters use 512, 1024, 512

ImageNet top 5 error: 16.4% -> 11.7%

#### VGG

Small filters, Deeper networks

Only 3x3 CONV stride 1, pad 1 and 2x2 MAX POOL stride 2

AlexNet (8 layers)  ->  VGG 16 (16 layers)    VGG 19 (19 layers)

Details:

- Similar training procedure as Krizhevsky 2012
- No Local Response Normalisation (LRN)
- Use VGG16 or VGG19 (VGG19 only slightly better, more memory)
- Use ensembles for best results
- FC7 features generalize well to other tasks

VGG top 5 error: 11.7% -> 7.3%



![vgg16](https://github.com/bifeng/daily_book_notes/raw/master/resource/vgg16_memory_params.png)



Q: Why use smaller filters? (3x3 conv) What is the effective receptive field of three 3x3 conv (stride 1) layers?

Stack of three 3x3 conv (stride 1) layers has same effective receptive field as one 7x7 conv layer - (the third 3x3 has the 7x7 receptive field, the second 3x3 has the 5x5 receptive field, the first 3x3 has the 3x3 receptive field)

But deeper, more non-linearities

And fewer parameters: $3 * (3^2C^2)$ vs. $7^2C^2$ for $C$ channels per layer



#### GoogleNet

Deeper networks, with computational efficiency
- 22 layers
- Efficient “Inception” module
- No FC layers
- Only 5 million parameters!
  12x less than AlexNet
- ILSVRC’14 classification winner
  (6.7% top 5 error)



![GoogLeNet](https://github.com/bifeng/daily_book_notes/raw/master/resource/GoogLeNet.png)



##### Inception module

“Inception module”: design a good local network topology (network within a network) and then stack these modules on top of each other

Apply parallel filter operations on the input from previous layer:
- Multiple receptive field sizes for convolution (1x1, 3x3, 5x5)
- Pooling operation (3x3)
  Concatenate all filter outputs together depth-wise



![inception_module](https://github.com/bifeng/daily_book_notes/raw/master/resource/inception_module.png)

Solution: “bottleneck” layers that use 1x1 convolutions to reduce feature depth

![inception_module_with_dimension_reduction](https://github.com/bifeng/daily_book_notes/raw/master/resource/inception_module_with_dimension_reduction.png)



#### ResNet

Very deep networks using residual connections
- 152-layer model for ImageNet
- ILSVRC’15 classification winner
  (3.57% top 5 error)
- Swept all classification and detection competitions in ILSVRC’15 and COCO’15!



Full ResNet architecture:
- Stack residual blocks
- Every residual block has two 3x3 conv layers
- Periodically, double # of filters and downsample spatially using stride 2 (/2 in each dimension)
- Additional conv layer at the beginning
- No FC layers at the end (only FC 1000 to output classes)
- For deeper networks (ResNet-50+), use “bottleneck” layer to improve efficiency (similar to GoogLeNet)



Training ResNet in practice:
- Batch Normalization after every CONV layer
- Xavier/2 initialization from He et al.
- SGD + Momentum (0.9)
- Learning rate: 0.1, divided by 10 when validation error plateaus
- Mini-batch size 256
- Weight decay of 1e-5
- No dropout used



##### residual block

![residual_block](https://github.com/bifeng/daily_book_notes/raw/master/resource/residual_block.png)



#### Comparison



![comparing complexity](https://github.com/bifeng/daily_book_notes/raw/master/resource/comparing_complexity.png)



#### Other architectures to know...

- NiN (Network in Network)
- Wide ResNet
- ResNeXT
- Stochastic Depth
- DenseNet
- FractalNet
- SqueezeNet



#### Summary

Even more recent trend towards examining necessity of depth vs. width and residual connections:

+ depth

  What happens when we continue stacking deeper layers on a “plain” convolutional neural network?

  -> The deeper model performs worse, but it’s not caused by over-fitting (performs worse on both training and test error) ! 

  Hypothesis: the problem is an optimization problem, deeper models are harder to optimize

  The deeper model should be able to perform at least as well as the shallower model.

  Solution: 

  1. A solution by construction is copying the learned layers from the shallower model and setting additional layers to identity mapping.  

     Use network layers to fit a residual mapping instead of directly trying to fit a desired underlying mapping -> This idea lead to the residual block in ResNet.

  2. 

+ width

  

+  residual connections

  





