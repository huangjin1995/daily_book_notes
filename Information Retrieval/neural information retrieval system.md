refer: https://hanxiao.github.io/2018/01/10/Build-Cross-Lingual-End-to-End-Product-Search-using-Tensorflow/#neural-ir-system



### architecture

![symbolic](https://github.com/bifeng/daily_book_notes/raw/master/resource/symbolic_ir_system.png)

![symbolic parsing](https://github.com/bifeng/daily_book_notes/raw/master/resource/symbolic_parsing.png)

![neural](https://github.com/bifeng/daily_book_notes/raw/master/resource/neural_ir_system.png)



|          | **Symbolic IR system**                                       | **Neural IR system**                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Pros** | Efficient in query-time; <br>straightforward to implement; <br>results are interpretable; <br>many off-the-shelf packages. | Automatic; <br/>resilient to noise; <br/>scale-out easily; <br/>requires little domain knowledge. |
| **Cons** | Fragile; <br/>Hard-coded knowledge; <br/>high maintenance costs. | Less efficient in query-time;<br/> hard to add business rules;<br/> requires a lot of data. |

This is not a Team Symbol or Team Neural choice. Both systems have their own advantages and can complement each other pretty well. Therefore, a better solution would be combining these two systems in a way so that we can enjoy all advantages from both sides.

### data 

training data:

If your only data source is the query log of a symbolic IR system, then your neural IR system is inevitably biased. The performance of your final system highly depends on the ability of the symbolic system.

In that sense, we are “bootstrapping” the symbolic IR system to build a neural IR system. Given enough training data, we hope that some previously hard-coded rules or manually coded functions can be picked up and *generalized* by deep neural networks.

negative example:

A straightforward way is just random sampling all products, hoping that no positive product gets accidentally sampled.

More sophisticated solutions could be collecting those products that generate impressions on customers yet not receive any clicks as negative ones. This requires some collaborations between you, the frontend team and the logging team, making sure those no-click items are really uninterested to users, not due to screen resolution, lazy loading, etc. 

#### Question

+ Is there much gain from the sophisticated solutions for negative sampling which compare to the random negative sampling?



### evaluation (validation set)

check the following features (those feature of symbolic information retrieval):<br>singleton query<br>compositional query<br>spell-checking<br>named-entity<br>...

































