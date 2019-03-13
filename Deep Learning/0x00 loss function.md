refer: Deep Learning book

http://cs231n.github.io/linear-classify/





#### Question

##### At initialization $W$ is small, What is the loss?

If the loss is not the expected at the first iteration or the start of training, then you should check the code. It's a very useful debugging strategy.

Example:

$L_i = \sum_{j\neq y_i} \max(0, s_j - s_{y_i} + \Delta)$, the initial loss is $(C-1) \cdot \Delta$, $C$ is the number of classes.

$L_i = -\log\left(\frac{e^{f_{y_i}}}{ \sum_j e^{f_j} }\right) \hspace{0.2in} \text{or equivalently} \hspace{0.2in} L_i = -f_{y_i} + \log\sum_j e^{f_j}$, the initial loss is $\log C​$.



##### Why we should choose this loss function? (Interpretation)

> The loss function quantifies our unhappiness with predictions on the training set.

Example:

Instead of the hinge loss $L_i = \sum_{j\neq y_i} \max(0, s_j - s_{y_i} + \Delta)$, we using the squared hinge loss $L_i = \sum_{j\neq y_i} \max(0, s_j - s_{y_i} + \Delta)^2$. 

The squared hinge loss, it penalizes violated margins more strongly (quadratically instead of linearly). 

The un-squared hinge loss, is more standard, but in some datasets the squared hinge loss can work better.

![margin](https://github.com/bifeng/daily_book_notes/raw/master/resource/margin.jpg)

The un-squared hinge loss "wants" the score of the correct class to be higher than all other scores by at least a margin of delta. If any class has a score inside the red region (or higher), then there will be accumulated loss. Otherwise the loss will be zero. Our objective will be to find the weights that will simultaneously satisfy this constraint for all examples in the training data and give a total loss that is as low as possible.

Softmax loss vs hinge loss:

The Softmax loss is never fully happy with the scores it produces: the correct class could always have a higher probability and the incorrect classes always a lower probability and the loss would always get better. 

The hinge loss is happy once the margins are satisfied and it does not micromanage the exact scores beyond this constraint. 



#### softmax

$p_i= \frac{e^{a_i}}{\sum_j e^{a_j}}​$

$L_{NLL}(p,y) = - \log p_y​$

$\frac{\partial}{\partial a_k} L_{NLL}(p,y) \\= \frac{\partial}{\partial a_k} ( - \log p_y) \\= \frac{\partial}{\partial a_k} (-a_y + \log \sum_j e^{a_j}) \\
= - 1_{y=k} + \frac{e^{a_k}}{\sum_j e^{a_j}} \\  
= p_k - 1_{y=k}$

Specifically, let us consider the case where the correct label is $i$ ($y=i$), an erroneous label is $j$ ($j \neq i$). (gradient update $a_y = a_y - loss\ gradient$)

The loss gradient for $a_y$ is $p_y - 1_{y=y} = p_y -1 <0$, so $a_y$ is always pushed up.<br>The loss gradient for $a_j$ is $p_j > 0$, so $a_j$ is always pushed down.



Squared error loss

$L_2(p(a),y) = ||p(a)-y||^2​$

$\frac{\partial}{\partial a_i} L_2(p(a),y) \\= \frac{\partial L_2(p(a),y)}{\partial p(a)}  \frac{\partial p(a)}{\partial a_i}\\= \sum_j 2(p_j(a) - y_j) p_j (1_{i=j} - p_i)​$

If the model incorrectly predicts a low probability for the correct class $y=i$, i.e., if $p_y=p_i \approx 0$, then $a_y$ does not get pushed up for the loss gradient $\frac{\partial}{\partial a_y} L_2(p(a),y)  \approx 0$.

This is one of many reasons that practitioners prefer to use the negative log-likelihood (cross-entropy) cost function, with the softmax/sigmoid non-linearity, rather than applying the squared error criterion to these probabilities. Second, the negative log-likelihood has the added advantage of a straightforward probabilistic interpretation as the maximum likelihood criterion for the softmax model.

Another useful property of the softmax: its output is invariant to adding a scalar to all of its inputs.
$$
softmax(a) = softmax(a+b)
$$
... this allows us to evaluate softmax with only small numerical errors ...





