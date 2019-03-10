refer: cs231n

![Jacobian](https://github.com/bifeng/daily_book_notes/raw/master/resource/jacobian_example.png)
$$
\frac{\partial L}{\partial x} = \underbrace{\frac{\partial f}{\partial x}}_{Jacobian \ matrix} \frac{\partial L}{\partial f}
$$
The size of the Jacobian matrix is [4096 x 4096]! In practice, we process an entire minibatch (e.g. 100) of examples at one time: i.e. Jacobian would technically be a [409,600 x 409,600] matrix!

How to calculate this large matrix ? Look at this "element-wise", for each x input, it's only affect the corresponding f function, so this Jacobian matrix will reduce to diagonal matrix!









