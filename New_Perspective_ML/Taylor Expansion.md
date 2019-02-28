http://jacoxu.com/jacobian%E7%9F%A9%E9%98%B5%E5%92%8Chessian%E7%9F%A9%E9%98%B5/

refer:<br>https://www.zhihu.com/question/25627482

https://en.wikipedia.org/wiki/Taylor_series<br>https://en.wikipedia.org/wiki/Gradient_descent<br>https://en.wikipedia.org/wiki/Newton's_method_in_optimization

https://en.wikipedia.org/wiki/Jacobian_matrix_and_determinant<br>https://en.wikipedia.org/wiki/Hessian_matrix

### Taylor Expansion

动机: 如何计算三角函数在某一点的值？如$y=sin(x)​$, 计算$x=2​$的值。

寻找三角函数的近似函数，三角函数具有无限可导的特点，所以近似函数也必须无限可导，泰勒选择无穷多项式函数作为三角函数的近似，函数的参数由初始点的值及导数相等原则确定。

![taylor polynomial](https://github.com/bifeng/daily_book_notes/raw/master/resource/taylor_polynomial.png)

从上图可以看出，当初始点为$(0,0)$时，随着多项式阶数的递增，近似的部分也不断延伸。

推广：任意函数都可以用无穷多项式函数近似

$f(x)​$ 在初始点$(0,f(0))​$的近似函数：$g(x) = a_0 + a_1 x + a_2 x^2 + \ldots + a_n x^n​$，再根据导数相等原则，推断出近似函数的系数：$g(x) = g(0) + \frac{f^1(0)}{1!} x +  \frac{f^2(0)}{2!} x^2 + \ldots +  \frac{f^n(0)}{n!}  x^n​$。也可以选择任意点$(x_0,f(x_0))​$作为起始点，此时近似函数表示为：
$$
g(x) = g(x_0) + \frac{f^1(x_0)}{1!} (x-x_0) +  \frac{f^2(x_0)}{2!} (x-x_0)^2 + \ldots +  \frac{f^n(x_0)}{n!}  (x-x_0)^n
$$
即：
$$
g(x) = \sum_{i=0}^{n} \frac{f^{(i)}(x_0)}{i!} (x-x_0)^i 
$$
至此，可根据精度要求选择$n$值，作为近似函数。



结合上图，观察$n=13$时，多项式函数近似：
$$
sin(x) \approx x - \frac{x^3}{3!} + \frac{x^5}{5!} - \frac{x^7}{7!} + \frac{x^9}{9!} - \frac{x^{11}}{11!} + \frac{x^{13}}{13!}
$$
当$x = 2 \pi​$时，左边等于0，右边等于6.28318-41.34170+81.60524-76.70585+42.05869-15.09464+3.81995=0.62487.

我们可以发现，随着多项式中各项的阶数增加，其数值也逐渐递减。

接着，佩亚诺首先把泰勒展开式中没有写出来的那些项补全，然后，他把这些项之和称为误差项，之后，他想把误差项变为0，考虑到泰勒展开式中的项越来越小，他就让误差项除以最后一项，试图得到0的结果，最后发现，只有当$x$趋近于$x_0$时，这个商才趋近于0，索性就这样了。因此，这个误差项被称为佩亚诺余项。

后来，拉格朗日将误差项给整合成了一项，而且不一定要$x$趋近于$x_0$，可以在二者之间的任何一个位置$\xi$处展开：
$$
\frac{f^{n+1}(\xi)}{(n+1)!}(x-x_0)^{(n+1)}
$$
证明过程主要利用柯西中值定理：

设误差项为$R(x)$，$R(x) = \frac{f^{(n+1)}(x_0)}{(n+1)!}  (x-x_0)^{(n+1)} + \frac{f^{(n+2)}(x_0)}{(n+2)!}  (x-x_0)^{(n+2)} + \dots $，为了去除$(x-x_0)^{(n+1)}$，将其设为$T(x)$，即$T(x) = (x-x_0)^{(n+1)}$，两者相除：
$$
\frac{R(x)}{T(x)} 
=\underbrace{ \frac{R(x)-R(x_0)}{T(x)-T(x_0)} = \frac{R'(\xi_1)}{T'(\xi_1)}}_{柯西中值定理}
= \frac{R'(\xi_1)}{(n+1)(\xi_1 - x_0)^n}
$$
不断将分子分母利用柯西中值定理转化，可以得到最终的误差项表达式。



### Application

在泰勒展开式的应用中，通常只选择（某处）一阶或二阶泰勒展开式，相当于只取该处的一小部分用线性函数近似。

#### Gradient Descent



雅可比矩阵(Jacobian)：
$$
\begin{bmatrix} \frac{\partial y_1}{\partial x_1} & \cdots & \frac{\partial y_1}{\partial x_n} \\ \vdots & \ddots & \vdots \\ \frac{\partial y_m}{\partial x_1} & \cdots & \frac{\partial y_m}{\partial x_n}  \end{bmatrix}
$$




#### Newton's Method



海森矩阵(Hessian)：
$$
\begin{bmatrix}  \frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1\,\partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1\,\partial x_n} \\  \\  \frac{\partial^2 f}{\partial x_2\,\partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2\,\partial x_n} \\  \\  \vdots & \vdots & \ddots & \vdots \\  \\  \frac{\partial^2 f}{\partial x_n\,\partial x_1} & \frac{\partial^2 f}{\partial x_n\,\partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}  \end{bmatrix}
$$
