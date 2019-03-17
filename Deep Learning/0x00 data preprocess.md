refer: CS231n, http://cs231n.github.io/neural-networks-2/

zero-centered data

normalized data

In practice, you may also see PCA and Whitening of the data



### Summary

TLDR: In practice for Images: center only

e.g. consider CIFAR-10 example with [32,32,3] images

- Subtract the mean image (e.g. AlexNet)
  (mean image = [32,32,3] array)
- Subtract per-channel mean (e.g. VGGNet)
  (mean along each channel = 3 numbers)
