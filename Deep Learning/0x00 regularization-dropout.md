refer:

https://www.zhihu.com/question/300940578





Dropout [1]：完全随机扔

SpatialDropout [2]：按channel随机扔

Stochastic Depth [3]：按res block随机扔

DropBlock [4]：每个feature map上按spatial块随机扔

Cutout [5]：在input层按spatial块随机扔

DropConnect [6]：只在连接处扔，神经元不扔。

DropBlock

.........下一个在哪扔？

[1] Nitish Srivastava, Geoffrey Hinton, Alex Krizhevsky, Ilya Sutskever, and Ruslan Salakhutdinov. Dropout: A simple way to prevent neural networks from overfitting. The Journal of Machine Learning Research, 15(1):1929–1958, 2014. 

[2] Jonathan Tompson, Ross Goroshin, Arjun Jain, Yann LeCun, and Christoph Bregler. Efficient object localization using convolutional networks. In CVPR, 2015.

[3] Gao Huang, Yu Sun, Zhuang Liu, Daniel Sedra, and Kilian Q Weinberger. Deep networks with stochastic depth. In ECCV, pages 646–661. Springer, 2016.

[4] Golnaz Ghiasi, Tsung-Yi Lin, Quoc V. Le, DropBlock: A regularization method for convolutional networks. NIPS 2018.

[5] Terrance DeVries and Graham W Taylor. Improved regularization of convolutional neural networks with cutout. CoRR, abs/1708.04552, 2017.

[6] Li Wan, Matthew Zeiler, Sixin Zhang, Yann LeCun, Rob Fergus, Regularization of Neural Network using DropConnect, International Conference on Machine Learning, 2013

DropBlock: A regularization method for convolutional networks dropout