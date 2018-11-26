more refer:

https://github.com/allenai/acl2018-semantic-parsing-tutorial

## Semantic Parsing

### CCG Semantic Parsing

+ Complex discrete learning algorithms

+ But, grammars hopefully generalize to unseen data well!

+ Difficult to engineer: few people can do it and it takes a lot of time

### Neural Semantic Parsing

+ Treat meaning as a string...
+ Apply NMT
+ Close to SOTA performance!!!
+ Much easier to build (with toolkits)

#### Constrained Decoding

Token-based Decoding:
The output space is tokens, but they are constrained to be relevant at each time step.

Grammar-based Decoding:
The output space is production rules, and a grammar defines the constraints.