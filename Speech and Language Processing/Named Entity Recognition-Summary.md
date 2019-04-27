refer:

Chinese NER Using CRFs and Logic for the Fourth SIGHAN Bakeoff, [paper](https://www.aclweb.org/anthology/I08-4016)

Entity Extraction, Linking, Classification, and Tagging for Social Media: A Wikipedia-Based Approach, [paper](http://pages.cs.wisc.edu/~anhai/papers/doctagger-vldb13.pdf)



#### models

Conditional Random Fields (Base Model)

Markov Logic Networks (Error Correction Model)





#### features

+ character features
+ word segment and pos features
+ dictionary features



#### domain knowledge

+ If a chunk (a series of continuous characters) occurs in the
  training data as a PER or a LOC or an ORG, then this
  chunk should be a PER or a LOC or an ORG in the testing
  data. In general, a unique string is defined as a PER, it
  cannot be a LOC somewhere else.
+ If a tagged entity ends with a location salient word, it is a
  LOC. If a tagged entity ends with an organization salient
  word, it is an ORG.
+ If a tagged entity is close to a subsequent location salient
  word, probably they should be combined together as a
  LOC. The closer they are, the more likely that they should
  be combined.
+ If a series of consecutive tagged entities are close to a subsequent
  organization salient word, they should probably
  be combined together as an ORG because an ORG may
  contain multiple PERs, LOCs and ORGs.
+ Similarly, if there exists a series of consecutive tagged entities
  and the last one is tagged as an ORG, it is likely that
  all of them should be combined as an ORG.
+ Entity length restriction: all kinds of tagged entities cannot
  exceed 25 Chinese characters.
+ Stopword restriction: intuitively, all tagged entities cannot
  comprise any stopword.
+ Punctuation restriction: in general, all tagged entities cannot
  span any punctuation.
+ Since all NEs are proper nouns, the tagged entities should
  end with noun words.
+ For a chunk with low conditional probabilities, all the
  above assumptions are adopted.

---

+ Overlapping mentions: For example, a rule may drop
  a mention if it is subsumed by another mention (e.g.,
  mention (Politics, $n_2$) is subsumed by (Politics of Love,
  $n_3$)).

+ Blacklists of strings and IDs: drop a mention if it is a

  blacklisted string (e.g., stop words, profanities, slangs,
  etc.; about 127K strings have been blacklisted), or if
  the mention refers to a blacklisted node in the KB
  (about 0.5M nodes have been blacklisted).

+ Prefix/suffix: drop a mention if it contains certain
  characters or words as prefixes or suffixes, or if the
  node name begins with a stop word (e.g., “a”, “an”,
  “the”).

+ Size/number: drop a mention if it is a one-letter word
  (e.g., “a”, “b”) or a number.

+ Straddling sentence boundaries: drop a mention if it
  straddles sentence boundaries, such as mention “Indian
  Cricket teams” from tweet “He’s an Indian. Cricket
  teams are popular in India.”

+ Part of a noun: if a mention is one word and the word
  before or after this mention is a noun phrase, then
  this mention is likely to be part of that noun phrase.
  Hence, drop this mention.



