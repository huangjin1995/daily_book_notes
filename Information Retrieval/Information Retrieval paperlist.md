

## relevance ranking

## importance ranking

### literature review

- An Introduction to Neural Information Retrieval, 2018.12 [paper](https://www.microsoft.com/en-us/research/publication/introduction-neural-information-retrieval/)
- NEURAL MODELS FOR INFORMATION RETRIEVAL, 2017.11 [ppt](https://www.microsoft.com/en-us/research/uploads/prod/2018/04/NeuralIR-Nov2017.pdf) 
- Hang Li, Zhengdong Lu, Deep Learning for Information Retrieval, SIGIR 2016 Tutorial, Pisa, July 2016. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/deep_learning_for_information_retrieval.pdf))
- Hang Li, Machine Learning for Information Retrieval, the Third Asian Summer School in Information Access, Kyoto University, August 2017. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/machine_learning_for_information_retrieval_-_kyoto.pdf))
- Hang Li, Opportunities and Challenges in Deep Learning for Information Retrieval, Tsinghua University,  Beijing, April 2016. ([pdf](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/tsinghua_opportunities_and_challenges_in_deep_learning_for_information_retrieval.pdf))

+ 




### papers

- Hang Li, Toward Building Self-Training Search Systems, Keynote Speech at CCIR 2018, Guilin, September 2018.  ([ppt](http://www.hangli-hl.com/uploads/3/4/4/6/34465961/unbiased_learning_to_rank.pptx)) 

#### Query

+ Jiafeng Guo, Xueqi Cheng, Gu Xu, Xiaofei Zhu, [Intent-Aware Query Similarity](http://www.bigdatalab.ac.cn/~gjf/papers/2011/Intent-Aware%20Query%20Similarity.pdf), Proceedings of The 20th ACM Conference on Information and Knowledge Management, pp. 259-268, October 2011, Glasgow, UK. (CIKM 2011, **Best Paper Award**) [slides](http://www.bigdatalab.ac.cn/~gjf/papers/2011/IQS_CIKM2011.pdf) 
+ 

#### Feedback

- **T. Joachims**, A. Swaminathan, T. Schnabel, *Unbiased Learning-to-Rank with Biased Feedback*, International Conference on Web Search and Data Mining (WSDM), 2017. Best Paper. [arxiv](https://arxiv.org/abs/1608.04468) 
  [PDF](http://www.cs.cornell.edu/people/tj/publications/joachims_etal_17a.pdf)][Software](http://www.cs.cornell.edu/People/tj/svm_light/svm_proprank.html)][[BibTeX](http://www.cs.cornell.edu/people/tj/publications/joachims.bib)] 

  **implicit feedback** - While implicit feedback has many advantages (e.g., it is inexpensive to collect, user centric, and timely), its inherent biases are a key obstacle to its effective use. For example, position bias in search rankings strongly influences how many clicks a result receives, so that directly using click data as a training signal in Learning-to-Rank (LTR) methods yields sub-optimal results. To overcome this bias problem, we present a counter-factual inference framework that provides the theoretical basis for unbiased LTR via Empirical Risk Minimization despite biased data.

- **T. Joachims**, L. Granka, B. Pan, H. Hembrooke, and G. Gay, *Accurately Interpreting Clickthrough Data as Implicit Feedback*, Proceedings of the Conference on Research and Development in Information Retrieval (SIGIR), 2005. [[Postscript\]](http://www.cs.cornell.edu/people/tj/publications/joachims_etal_05a.ps.gz) [[PDF\]](http://www.cs.cornell.edu/people/tj/publications/joachims_etal_05a.pdf) [[BibTeX](http://www.cs.cornell.edu/people/tj/publications/joachims.bib)] 

- 

#### Relevance matching

+ A Deep Relevance Matching Model for Ad-hoc Retrieval, Jiafeng Guo, Yixing Fan, Qingyao Ai, W. Bruce Croft, CIKM 2016, [arxiv](https://arxiv.org/abs/1711.08611) 

#### Language Models

- Relevance-based language models, V Lavrenko, WB Croft - ACM SIGIR Forum, 2017 [paper](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.193.3687&rep=rep1&type=pdf) 
- A study of smoothing methods for language models applied to ad hoc information retrieval, C Zhai, J Lafferty - ACM SIGIR Forum, 2017 [paper](http://www.academia.edu/download/30739074/10.1.1.65.8943.pdf) | [long paper](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.58.8978&rep=rep1&type=pdf) 
- C. Zhai. <u>Statistical Language Models</u> for Information Retrieval. 2008. [paper](http://sifaka.cs.uiuc.edu/czhai/pub/slmir-now.pdf) 
- A language modeling approach to information retrieval, JM Ponte, WB Croft - Proceedings of the 21st annual international ACM …, 1998 [paper](http://www.abdelali.net/ref/Ponte_LM_IR_98.pdf) 

#### Learning to Rank

- Learning to rank for information retrieval and natural language processing. Hang Li. Synthesis Lectures on Human Language Technologies, 4(1):1–113, 2011.
- A short introduction to learning to rank, Hang Li. 2011, [paper](https://www.jstage.jst.go.jp/article/transinf/E94.D/10/E94.D_10_1854/_pdf) 
- Future directions in learning to rank, O Chapelle, Y Chang, TY Liu, 2011 JMLR [paper](http://proceedings.mlr.press/v14/chapelle11b/chapelle11b.pdf) 
- From RankNet to LambdaRank to LambdaMART: An Overview, CJC Burges - Learning, 2010 [paper](https://www.microsoft.com/en-us/research/publication/from-ranknet-to-lambdarank-to-lambdamart-an-overview/) 
- Tie-Yan Liu. Learning to rank for information retrieval. Found. Trends Inf. Retr., 3(3):225–331, March 2009.
- Learning to rank for information retrieval (LR4IR 2007)  [paper](http://www.sigir.org/files/forum/2007D/2007d_sigirforum_joachims.pdf) 
- 