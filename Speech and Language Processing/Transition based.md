### transition system

+ Automata
  –State
  • Start state —— an empty structure
  • End state —— the output structure
  • Intermediate states —— partially constructed structures
  –Actions
  • Change one state to another

+ State

  – Corresponds to partial results during decoding

+ Actions

  – The operations that can be applied for state transition
  – Construct output incrementally



基于转移的语义依存分析方法。该方法主要分为两部分结构，一是预测，二是执行。预测部分是由一个分类器实现。执行部分需要一个转移算法 ，包括一些预定义的转移动作等。

转移状态包括一个保存正在处理中的词的栈（Stack），一个保存待处理词的缓存（Buffer），和一个记录已经生成的依存弧的存储器（memory），最后是一个deque， 暂时跳过一些词。

转移动作：

LEFT-REDUCE转移动作，LEFT是生成一条由缓存顶的词指向栈顶词的一条弧，REDUCE，是指生成弧之后，将栈顶词消除掉。

LEFT-PASS转移动作，暂时不把之前的词语消除，经过一系列转移动作，再执行LEFT-REDUCE交互， 再消除之前的词语。



用来处理依存树结构的转移系统，以Choi等人在2013年提出的转移系统为例。

用来处理依存图结构的转移系统