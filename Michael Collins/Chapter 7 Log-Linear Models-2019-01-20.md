天气：晴<br>阅读时间：早班车<br>记录时间：2018-11-09~12 \ 2019-01-20



# chapter 7

### Features of LPCFGs

1. With less restriction, it mean more flexible to incorporate a broad set of contextual information.

we often use features templates to define features, and each features are indicator functions. <br>These features includes uni-grams, bi-grams, tri-grams, skip-bi-grams, prefix, suffix, and so on.

2. More accurate, but with more parameter, it mean need more data to estimate! It will face with data sparsity problem too (how handle it :question:)

### Definition of Log-Linear Models

We have some input domain $\cal{X}$, and a finite label set $\cal{Y}$. Aim is to provide a conditional probability $p(y|x)$ for any $x \in \cal{X}$ and $y \in \cal{Y}$.<br>A feature is a function $f: \cal{X} \times \cal{Y} \rightarrow \mathbb{R}$ (often binary features or indicator functions)<br>Say we have $m$ features $f_k$ for $k=1 \dots m$  $\Rightarrow$ A feature vector $f(x,y) \in \mathbb{R}^m$ for any $x \in \cal{X}$ and $y \in \cal{Y}$.<br>We also have a parameter vector $v \in \mathbb{R}^m$.<br>We define

$$
p(y|x;v) =\frac{e^{v \cdot f(x,y)}}{\sum_{y' \in \cal{Y}}{e^{v \cdot f(x, y')}}}
$$

$v \cdot f(x,y) = \sum\limits_{k}v_{k}f_{k}(x,y)$

($p(y|x;v) >0$ and $\sum_y p(y|x;v)=1$)

### Why the name?

$$
\log p(y | x; v) = \underbrace{v \cdot f(x,y) }_{Linear\ term} - \underbrace{\log \sum_{y' \in \cal{Y}} e^{v \cdot f(x,y')}}_{Normalization\ term}
$$

### Features of Log-linear models

For example, in practice, we would probably introduce one trigram feature for every trigram seen in the training data: i.e., for all trigrams $(u, v,w)$ seen in training data, create a feature
$$
f_{N(u,v,w)}(x, y) =
\begin{cases}
	1 \quad if\ y = w, w_{i-2} = u, w_{i-1} = v \\
	0 \quad otherwise
\end{cases}
$$
where $N(u,v,w)$ is a function that maps each $(u,v,w)$ trigram to a different integer.



### Parameter estimation

#### Maximum-likelihood estimation

Given training sample $(x^{(i)}, y^{(i)})$ for $i = 1 \dots n$, each $(x^{(i)}, y^{(i)}) \in \cal{X} \times \cal{Y}$:
$$
v_{ML} = \arg \max_{v \in \mathbb{R}^m}L(v)
$$
where
$$
L(v) = \sum_{i=1}^{n} \log p(y^{(i)} | x^{(i)}; v) = \sum_{i=1}^{n} v \cdot f(x^{(i)},y^{(i)})  - \sum_{i=1}^{n} \log \sum_{y' \in \cal{Y}} e^{v \cdot f(x^{(i)},y')}
$$


1. Gradient ascent methods

   Initialization: v = 0
   Iterate until convergence:

   Calculate $\Delta= \frac{dL(v)}{dv}$
   Calculate $ \beta_{*}= \arg \max_{\beta}L(v + \beta \Delta) $(Line Search)
   Set $v  \leftarrow v + \beta_{*} \Delta$

2. Conjugate gradient methods

   Conjugate gradient methods require calculation of gradient at each iteration, but do a line search in a direction which is a function of the current gradient, and the previous step taken.

   $calc\_gradient(v) \rightarrow (L(v), \frac{dL(v)}{dv})$

Calculating gradients:

$$
\frac{dL(v)}{dv} =  \underbrace{\sum\limits_{i=1}^{n} f(x^{(i)},y^{(i)}) }_{Empirical \ counts} -  \underbrace{\sum\limits_{i=1}^{n} \sum\limits_{y' \in \cal{Y}} f(x^{(i)},y') p(y'|x^{(i)};v)}_{Expected \ counts}
$$




### Smoothing/regularization

Modified loss function
$$
L(v) = \sum_{i=1}^{n} v \cdot f(x^{(i)},y^{(i)})  - \sum_{i=1}^{n} \log \sum_{y' \in \cal{Y}} e^{v \cdot f(x^{(i)},y')} - \frac{\lambda}{2} \sum_{i=1}^{m} v_{k}^{2}
$$

Calculating gradients:
$$
\frac{dL(v)}{dv_k} =  \underbrace{\sum\limits_{i=1}^{n} f_k(x^{(i)},y^{(i)}) }_{Empirical \ counts} -  \underbrace{\sum\limits_{i=1}^{n} \sum\limits_{y' \in \cal{Y}} f_k(x^{(i)},y') p(y'|x^{(i)};v)}_{Expected \ counts} - \lambda v_k
$$


### Disadvantage

Computing ${\sum_{y' \in \cal{Y}}{e^{v \cdot f(x, y')}}}$ is slow.



### Example: Language modeling

$x$ is a "history" $w_1,w_2, \dots w_{i-1}$, e.g.,

Third, the notion \grammatical in English" cannot be identied in any
way with the notion \high order of statistical approximation to English".
It is fair to assume that neither sentence (1) nor (2) (nor indeed any
part of these sentences) has ever occurred in an English discourse.
Hence, in any statistical

$y$ is an "outcome" $w_i$

Example features:
$$
\begin{eqnarray*}
f_1(x, y) &=&
\begin{cases}
1 \ if \ y = model \\
0 \ otherwise

\end{cases} \\

f_2(x, y) &=&
\begin{cases}
1 \ if\ y = model\ and\ w_{i-1} = statistical \\
0 \ otherwise
\end{cases} \\

f_3(x, y) &=&
\begin{cases}
1 \ if\ y = model, w_{i-2} = any, w_{i-1} = statistical \\
0 \ otherwise
\end{cases} \\


f_4(x, y) &=&
\begin{cases}
1 \ if\ y = model, w_{i-2} = any \\
0 \ otherwise
\end{cases} \\

\dots \\
f_k(x, y) &=& \dots
\end{eqnarray*}
$$


$f(x,model) = \sum\limits_{k}f_{k}(x,model)$

$p(model|x;v) = \frac{e^{v \cdot f(x,model)}}{\sum\limits_{y' \in \cal{Y}}{e^{v \cdot f(x, y')}}}$

