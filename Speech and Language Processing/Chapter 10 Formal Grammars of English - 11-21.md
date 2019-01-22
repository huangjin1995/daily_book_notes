天气：晴<br>阅读时间：早班车/晚班车<br>记录时间：11-21

## Chapter 10

### Context-Free Grammars

Context-free grammars are also called Phrase-Structure Grammars, and the formalism is equivalent to Backus-Naur Form, or BNF. The idea of basing a grammar on constituent structure was first formalized by Chomsky (1956) and, independently, Backus (1959).

A CFG can be thought of in two ways: as a device for generating sentences and as a device for assigning a structure to a given sentence.

### Chomsky Normal Form (CNF)

The CNF grammars are binary branching, that is they have binary trees (down to the prelexical nodes). We make use of this binary branching property in the CKY parsing algorithm.

why we need the CNF :question:

The CNF is bi-gram model​ :question: 

### Heads and Head Finding

The idea of a head for each constituent dates back to Bloomfield (1914). It is central to **constituent-based grammar formalisms** such as Head-Driven Phrase Structure Grammar (Pollard and Sag, 1994), as well as the dependency-based approaches to grammar. Heads and head-dependent relations have also come to play a central role in computational linguistics with their use in probabilistic parsing and in dependency parsing.

What's head?<br>	The head is the word in the phrase that is grammatically the most important. Heads are passed up the parse tree; thus, each non-terminal in a parse tree is annotated with a single word, which is its lexical head.

How to find the head?<br>	Instead of specifying head rules in the grammar itself, heads are identified dynamically in the context of trees for specific sentences. In other words, once a sentence is parsed, the resulting tree is walked to decorate each node with the appropriate head. <br>	Most current systems rely on a simple set of hand-written rules, such as a practical one for Penn Treebank grammars given in Collins (1999).

### Lexicalized Grammars

The approach to grammar presented thus far emphasizes **phrase-structure rules** while minimizing the role of the lexicon. 

To overcome these issues, numerous alternative approaches
have been developed that all share the common theme of making better
use of the lexicon. Among the more computationally relevant approaches are Lexical-Functional Grammar (LFG) (Bresnan, 1982), Head-Driven Phrase Structure Grammar (HPSG) (Pollard and Sag, 1994), Tree-Adjoining Grammar (TAG) (Joshi, 1985), and Combinatory Categorial Grammar (CCG). These approaches differ with respect to how lexicalized they are — the degree to which they rely on the **lexicon** as opposed to phrase structure rules to capture facts about the language.

#### Combinatory Categorial Grammar (CCG)



[中文CCG树库的构建](http://jcip.cipsc.org.cn/CN/abstract/abstract1600.shtml)<br>[Chinese CCGbank: extracting CCG derivations from the Penn Chinese Treebank](http://aclweb.org/anthology/C/C10/C10-1122.pdf)

