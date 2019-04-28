cs231n

more:

http://blog.dlib.net/2018/02/automatic-learning-rate-scheduling-that.html





### learning rate decay 

Learning rate decay over time.

step decay:

e.g. decay learning rate by half every few epochs.

exponential decay:

$\alpha =\alpha_0 e^{-kt}$

1/t decay:

$\alpha = \alpha_0/(1+kt)$



Question:

When we need learning rate decay?

More critical with SGD+Momentum, less common with Adam

Learning rate decay is kind of a second order hyperparameter, you typically should not optimize it from the start.





