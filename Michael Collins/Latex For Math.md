> reference: 
>
> http://www.mohu.org/info/symbols/symbols.htm 常用数学符号的 LaTeX 表示方法
>
> https://blog.csdn.net/thither_shore/article/details/52260742



### 数学符号

#### 上标/下标

$a^1$, $a^{1}​$, 

$y'$,$y^{'}$,

$a_1$, $a_{1}$

$a^{3}_{ij}$

#### 分数

$\frac{1}{2}​$

#### 连乘

$\prod_{i=0}^n$, $\prod^{n}_{i=0}$
$$
\prod_\epsilon
$$


#### 求和

$\sum_{i=1}^{n}$, $\sum\limits_{i=1}^{n}$


$$
\sum_{i=1}^{n} \\
\sum\nolimits_{i=1}^{n}
$$


#### 重音符(导数)

`\bar`, `\dot`,`\acute`

$\bar{A}$, $\dot{A}$, $\acute{A}$ 

#### 上/下划线

$\overline{A}$,$\underline{A}$, 

#### 上/下括号

`\overbrace`, `\underbrace`

$\underbrace{a+b}_{c}$

#### 上/下字母

`\mathop`
$$
\mathop{\arg \max}_{\theta}
$$

### 字体

#### 希腊字母

##### 小写

$alpha$, $\beta$, $\gamma$, $\kappa$,

$\lambda$,

##### 大写

$\Sigma$, 

#### 数学字母

`\mathbb`

$\mathbb{R}$

#### 其他字体

##### 意大利体

$A$, $\it{A}$, $\mit{A}$

##### 罗马体

`\rm`

$\rm{A}$

##### 黑体

`\bf`

$\bf{A}$

##### 花体

`\cal`

$\cal{A}$

##### 打字机体

`\tt`

$\tt{A}$

##### 等线体

`\sf`

$\sf{A}$

### 二元运算符

$+$, $-$, $\times$, $\setminus$, $\cdot$, 

$\cup$, $\cap$, 

$\vee$, $\lor$, $\wedge$, $\land$, $\bigvee$, $\bigwedge$, 

### 二元关系符

$\in$, $\notin$,

$\propto$,



`\le` is stand for "less than or equal to".  And `slant` means 倾斜. 

`\ge` is stand for "greater than or equal to".

$\ge$, $\geq$, $\geqslant$, $\geqq$,

$\le$, $\leq$, $\leqslant$, $\leqq$,



### 箭头

$\leftarrow$, $\gets$, $\rightarrow$, $\to$,

$\Leftarrow$, $\Rightarrow$,

### 空格、换行

空格 -  `\`, `\quad`, `\qquad`

换行 - `\\`

示例：

$a\ b$, $a \quad b$, $a \qquad b$,

$a \\ b$

### 公式对齐

```
\begin{align*}
&=
\end{align*}
```

示例：
$$
\begin{align*}
u \cdot n
& =u n^T \\
& = u(A A^{-1})n^T \\
& =(uA)(A^{-1}n^T) \\
& =(uA)((A^{-1}n^T)^T)^T \\
& =(uA)(n(A^{-1})^T)^T \\
& =uA \cdot n(A^{-1})^T \\
& =uA\cdot nB \\
& =0
\end{align*}
$$

```
\begin{eqnarray*}
&=&
\end{eqnarray*}
```


$$
\begin{eqnarray*}

x^n+y^n &=& z^n \\

x+y &=& z 

\end{eqnarray*}
$$

```
\begin{split}
&=
\end{split}
```



$$
\begin{split}
a &= b \\
c &= d \\
e &= f 
\end{split} \tag{1.3}
$$



### 大括号（多行赋值）

```
\begin{cases}
&=
\end{cases}
```

$$
P(x|Pa_x)=
\begin{cases} 
		1, & x=f(Pa_{x})  \\ 
		0, & other\ values 
\end{cases}
$$



### 其他符号

`\cdots`, `\blacktriangleright`, `\blacktriangledown`

$\cdots$, $\blacktriangleright$, $\blacktriangledown​$,

