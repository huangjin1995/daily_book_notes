http://cs231n.github.io/optimization-2/

**Motivation**: Understanding of this process and its subtleties is critical for you to understand, and effectively develop, design and debug Neural Networks.

In practice we usually only compute the gradient for the parameters (e.g. $W$,$b$) so that we can use it to perform a parameter update. However, as we will see later in the class the gradient on $x_i$ can still be useful sometimes, for example for purposes of visualization and interpreting what the Neural Network might be doing.

#### Interpretation of the gradient

Keep in mind what the derivatives tell you: They indicate the rate of change of a function with respect to that variable surrounding an infinitesimally small region near a particular point:
$$
\frac{df(x)}{dx} = \lim_{h \rightarrow 0} \frac{f(x+h)-f(x)}{h}
$$
A nice way to think about the expression above is that when *h* is very small, then the function is well-approximated by a straight line, and the derivative is its slope. In other words, the derivative on each variable tells you the sensitivity of the whole expression on its value. (This can be seen by rearranging the above equation ($f(x+h)=f(x) + h \frac{df(x)}{dx}​$))

> The derivative on each variable tells you the sensitivity of the whole expression on its value.

#### Intuitive understanding of backpropagation

...

> *This extra multiplication (for each input) due to the chain rule can turn a single and relatively useless gate into a cog in a complex circuit such as an entire neural network.*

...

Backpropagation can thus be thought of as gates communicating to each other (through the gradient signal) whether they want their outputs to increase or decrease (and how strongly), so as to make the final output value higher.

...

1. 链式法则将一个个独立的门转变为非常复杂的运算
2. 通过分析每一个门，可以分析其对最终结果的影响

#### Staged computation

Suppose that we have a function of the form:
$$
f(x,y) = \frac{x + \sigma(y)}{\sigma(x) + (x+y)^2}
$$
It is very important to stress that if you were to launch into performing the differentiation with respect to either $x$ or $y$, you would end up with very large and complex expressions. However, it turns out that doing so is completely unnecessary because we don’t need to have an explicit function written down that evaluates the gradient. We only have to know how to compute it.

The **forward pass** computes values from inputs to output. 

```python
x = 3 # example values
y = -4

# forward pass
sigy = 1.0 / (1 + math.exp(-y)) # sigmoid in numerator   #(1)
num = x + sigy # numerator                               #(2)
sigx = 1.0 / (1 + math.exp(-x)) # sigmoid in denominator #(3)
xpy = x + y                                              #(4)
xpysqr = xpy**2                                          #(5)
den = sigx + xpysqr # denominator                        #(6)
invden = 1.0 / den                                       #(7)
f = num * invden # done!                                 #(8)
```

The **backward pass** then performs backpropagation which starts at the end and recursively applies the chain rule to compute the gradients all the way to the inputs.

```python
# backprop f = num * invden
dnum = invden # gradient on numerator                             #(8)
dinvden = num                                                     #(8)
# backprop invden = 1.0 / den 
dden = (-1.0 / (den**2)) * dinvden                                #(7)
# backprop den = sigx + xpysqr
dsigx = (1) * dden                                                #(6)
dxpysqr = (1) * dden                                              #(6)
# backprop xpysqr = xpy**2
dxpy = (2 * xpy) * dxpysqr                                        #(5)
# backprop xpy = x + y
dx = (1) * dxpy                                                   #(4)
dy = (1) * dxpy                                                   #(4)
# We have calculate the dx and dy, the following dx and dy should accumulate its value. So we should use += instead of =.
# backprop sigx = 1.0 / (1 + math.exp(-x))
dx += ((1 - sigx) * sigx) * dsigx # Notice += !! See notes below  #(3)
# backprop num = x + sigy
dx += (1) * dnum                                                  #(2)
dsigy = (1) * dnum                                                #(2)
# backprop sigy = 1.0 / (1 + math.exp(-y))
dy += ((1 - sigy) * sigy) * dsigy                                 #(1)
# done! phew
```

Notice a few things:

**Cache forward pass variables**. To compute the backward pass it is very helpful to have some of the variables that were used in the forward pass. In practice you want to structure your code so that you cache these variables, and so that they are available during backpropagation.

**Gradients add up at forks**. The forward expression involves the variables **x,y** multiple times, so when we perform backpropagation we must be careful to use `+=` instead of `=` to accumulate the gradient on these variables (otherwise we would overwrite it). This follows the *multivariable chain rule* in Calculus, which states that if a variable branches out to different parts of the circuit, then the gradients that flow back to it will add.

#### Patterns in backward flow (intuition of operation)

It is interesting to note that in many cases the backward-flowing gradient can be interpreted on an intuitive level. For example, the three most commonly used gates in neural networks (**add,mul,max**), all have very simple interpretations in terms of how they act during backpropagation. Consider this example circuit:

![example of patterns in backward flow.png](https://github.com/bifeng/daily_book_notes/raw/master/resource/example of patterns in backward flow.png)

##### Add gate (gradient distributor)

The **add gate** always takes the gradient on its output and distributes it equally to all of its inputs, regardless of what their values were during the forward pass. This follows from the fact that the local gradient for the add operation is simply +1.0, so the gradients on all inputs will exactly equal the gradients on the output because it will be multiplied by x1.0 (and remain unchanged).

##### Max gate (gradient router)

The **max gate** routes the gradient. Unlike the add gate which distributed the gradient unchanged to all its inputs, the max gate distributes the gradient (unchanged) to exactly one of its inputs (the input that had the highest value during the forward pass). This is because the local gradient for a max gate is 1.0 for the highest value, and 0.0 for all other values. 

##### Multiply gate (gradient switcher)

The **multiply gate** is a little less easy to interpret. Its local gradients are the input values (except switched), and this is multiplied by the gradient on its output during the chain rule.

*Unintuitive effects and their consequences*. Notice that if one of the inputs to the multiply gate is very small and the other is very big, then the multiply gate will do something slightly unintuitive: <u>it will assign a relatively huge gradient to the small input and a tiny gradient to the large input.</u> Note that in linear classifiers where the weights are dot producted $w^Tx_i$ (multiplied) with the inputs, this implies that the scale of the data has an effect on the magnitude of the gradient for the weights. For example, if you multiplied all input data examples $x_i$ by 1000 during preprocessing, then the gradient on the weights will be 1000 times larger, and you’d have to lower the learning rate by that factor to compensate. This is why **preprocessing** matters a lot, sometimes in subtle ways! And having intuitive understanding for how the gradients flow can help you debug some of these cases.

#### Debug models with backpropagation

##### Vanishing gradients on sigmoids (or tanh) non-linearities

Causes: weight initialization or data preprocessing

![sigmoid](https://github.com/bifeng/daily_book_notes/raw/master/resource/sigmoid.png)

```python
z = 1/(1 + np.exp(-np.dot(W, x))) # forward pass
dx = np.dot(W.T, z*(1-z)) # backward pass: local gradient for x
dW = np.outer(z*(1-z), x) # backward pass: local gradient for W
```

A non-obvious fun fact about sigmoid is that its local gradient (z*(1-z)) achieves a maximum at 0.25, when z = 0.5. That means that every time the gradient signal flows through a sigmoid gate, its magnitude always diminishes by one quarter (or more) (<u>diminishes at least one quarter</u>). If you’re using basic SGD, this would make the lower layers of a network train much slower than the higher ones (fist computing the gradient of higher layers, then computing the gradient of lower layers).



The inappropriate **weight initialization or data preprocessing** will lead to these non-linearities “saturate” and entirely stop learning — your training loss will be flat and refuse to go down.

If your weight matrix W is initialized too large, the output of the matrix multiply could have a very large range (e.g. numbers between -400 and 400), which will make all outputs in the vector z almost binary: either 1 or 0. But if that is the case, z*(1-z), which is local gradient of the sigmoid non-linearity, will in both cases become zero (“vanish”), making the gradient for both x and W be zero. The rest of the backward pass will come out all zero from this point on due to multiplication in the chain rule.

See a longer explanation in this [CS231n lecture video](https://youtu.be/gYpoJMlgyXA?t=14m14s).

##### Dying ReLUs

Causes: weight initialization or aggressive learning rate

![relu](https://github.com/bifeng/daily_book_notes/raw/master/resource/relu.png)

```python
z = np.maximum(0, np.dot(W, x)) # forward pass
dW = np.outer(z > 0, x) # backward pass: local gradient for W
```

If a neuron gets clamped to zero in the forward pass (i.e. z=0, it doesn’t “fire”), then its weights
will get zero gradient. This can lead to what is called the “dead ReLU” problem, where if a ReLU neuron is unfortunately initialized such that it never fires, or if a neuron’s weights ever get knocked off with a large update during training into this regime, then this neuron will remain
permanently dead.

Sometimes you can forward the entire training set through a trained network and find that a large fraction (e.g. 40%) of your neurons were zero the entire time.

Neurons can also die during training, usually as a symptom of aggressive learning rates.

See a longer explanation in [CS231n lecture video](https://youtu.be/gYpoJMlgyXA?t=20m54s).

##### Exploding gradients in RNNs

...



See a longer explanation in this [CS231n lecture video](https://www.youtube.com/watch?v=yCC09vCHzF8).

##### Spotted in the Wild: DQN Clipping

...





#### Question

+ Backpropagation will happen into both `logits` and `labels` ?
+ 











