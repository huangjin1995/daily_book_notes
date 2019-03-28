refer: CS231n

http://cs231n.github.io/convolutional-networks/





#### Convolution Layer

![conv_layer](https://github.com/bifeng/daily_book_notes/raw/master/resource/conv_layer.png)

Common settings:
K = (powers of 2, e.g. 32, 64, 128, 512)

- F = 3, S = 1, P = 1
- F = 5, S = 1, P = 2
- F = 5, S = 2, P = ? (whatever fits)
- F = 1, S = 1, P = 0

 1x1 convolution layers make perfect sense, each filter has size 1x1x$D$, and performs a $D$-dimensional dot
product.



how to calculate the spatial size of the output volume?

$(W - F + 2P)/S + 1$

the input volume size ($W$), the receptive field size of the Conv Layer neurons ($F$), the stride with which they are applied ($S$), and the amount of zero padding used ($P$) on the border. 

Without zero padding will lead to the shrink of volume size. Shrinking too fast is not good, doesn’t work well.

In general, common to see CONV layers with stride 1, filters of size $F \times F$, and zero-padding with $(F-1)/2$. (will preserve size spatially)



##### Parameter Sharing (assumption)

It turns out that we can dramatically reduce the number of parameters by making one reasonable assumption: if one feature is useful to compute at some spatial position (x,y), then it should also be useful to compute at a different position (x2,y2). 

input: 227 x 227 x 3

receptive field size F=11, stride S=4, no zero padding P=0  $\rightarrow$ 11 x 11 x 3

conv layer: 55 x 55 x 96

Each of the 55 x 55 x 96 = 290400 neurons has 11 x 11 x 3 = 363 weights and 1 bias. This adds up to 290400 * 364 = 105,705,600 parameters on the first layer of the ConvNet alone. But With this parameter sharing scheme, the first Conv Layer in our example would now have only 96 unique set of weights (one for each depth slice), for a total of 96 x 364 = 34,944 parameters. Alternatively, all 55 x 55 neurons in each depth slice will now be using the same parameters.

Notice that the parameter sharing assumption <u>is relatively reasonable</u>: If detecting a horizontal edge is important at some location in the image, it should intuitively be useful at some other location as well due to the translationally-invariant structure of images. There is therefore no need to relearn to detect a horizontal edge at every one of the 55*55 distinct locations in the Conv layer output volume.

Note that sometimes the parameter sharing assumption <u>may not make sense</u>. One practical example is when the input are faces that have been centered in the image. You might expect that different eye-specific or hair-specific features could (and should) be learned in different spatial locations. In that case it is common to relax the parameter sharing scheme, and instead simply call the layer a **Locally-Connected Layer**.



What's the number of parameters in this layer?

Input volume: 32x32x3
10 5x5 filters with stride 1, pad 2

each filter has 5\*5\*3 + 1 = 76 params (+1 for bias)
=> 76*10 = 760



#### Pooling Layer

- makes the representations smaller and more manageable
- operates over each activation map independently



![pool_layer](https://github.com/bifeng/daily_book_notes/raw/master/resource/pool_layer.png)

Common settings:
F = 2, S = 2
F = 3, S = 2













