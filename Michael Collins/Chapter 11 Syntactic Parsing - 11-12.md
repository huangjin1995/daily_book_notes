天气：晴<br>阅读时间：早班车<br>记录时间：11-12/11-19



## Chapter 11

### Syntactic Parsing

The problem of mapping from a string of words to its parse tree is called syntactic parsing.

#### Convert CFG to CNF

1. Copy all conforming rules to the new grammar unchanged.
2. Convert terminals within rules to dummy non-terminals.
3. Convert unit-productions.

problem:question:

4. Make all rules binary and add them to new grammar.

### Partial parsing

A partial parser，or shallow parser, is simply identify and classify the segments or constituents in a text that are likely to contain valuable information.

Partial parsing methods:

1. flatter trees

Some make use of cascades of finite state transducers (:question:) to produce tree-like representations. These approaches typically produce flatter trees.

The intent is to produce parse trees that link all the major constituents in an input.

2. chunking

chunking is the process of identifying and classifying the flat, non-overlapping segments of a sentence that constitute the basic non-recursive phrases corresponding to the major content-word parts-of-speech: noun phrases, verb phrases, adjective phrases, and prepositional phrases.

The task of finding all the base noun phrases in a text is particularly common, named the base-NPs chunking.

What constitutes a syntactic base phrase depends on the application. Nevertheless, some standard guidelines are followed in most system.<br>First and foremost, base phrases of a given type do not recursively contain any constituents of the same type.<br>In most approaches, base phrases include the head word of the phrase, along with any pre-head material within the constituent, while crucially excluding any post-head material.<br>So, it relies on the accuracy of the head-finding rules.

Given a training set, **any sequence model** can be used.

#### Summary

+ Many practical problems, including information extraction problems, can be solved without full parsing.

+ Partial parsing and chunking are methods for identifying shallow syntactic constituents in a text.



