refer: Deep Learning book

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





