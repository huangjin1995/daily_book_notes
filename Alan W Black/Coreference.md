more refer:

[Anaphora](https://en.wikipedia.org/wiki/Anaphora_%28linguistics%29#Anaphor_resolution)

CS 4705: Introduction to Natural Language Processing, Fall 2009 - [Kathy McKeown](http://www.cs.columbia.edu/~kathy)

http://www1.cs.columbia.edu/~kathy/NLP/index.htm



refer:<br>[CS 4705 Pronouns and Reference Resolution](http://www.cs.columbia.edu/~kathy/NLP/ClassSlides/Slides09/Class19-Pronouns/myref.pdf)



### Coreference

指代/所指现象：

+ 不定名词短语(indefinite noun phrase)

  A homeless man hit up Bloomberg for a dollar.
  Some homeless guy hit up Bloomberg for a dollar.
  This homeless man hit up Bloomberg for a dollar.

+ 有定名词短语(definite noun phrase)

  The poor fellow only got a lecture.

+ 指示词(demonstrative)

  This homeless man got a lecture but that one got carted off to jail.

+ 单个复指(one-anaphora)

  Clinton used to have a dog called Buddy. Now he’s got another one

+ 代词(pronoun)

指代/所指类型：Entities, concepts, places, propositions, events, ...

下面主要以**代词指代**来讲共指的概念。

#### anaphora / cataphora

两者都是指代，不同的是 referent 和 referring expression 出现的先后顺序

- **anaphora:** the use of a word referring to or replacing a word used earlier in a sentence
- **cataphora:** the use of a word or phrase that refers to or stands for a later word or phrase

**E.g., Anphora** 

```
I went to see my grandfather at the hopital.
The old man has been there for weeks.
He had surgery a few days ago.
--------------------------------
Referring expressions: the old man, he
Antecedents（先行词）: my grandfather
```

**E.g., Cataphora** 

```
– R: She didn’t like it!
– D: What do you mean?
– R: She didn’t like it!
– D: Who didn’t like what?
– R: Mary.
– D: What didn’t Mary like?
– R: She didn’t like the article I read in the *New Yorker*.
```



### Constraints on Co-reference

句法和语义约束

1. Agreement constraints - 一致性约束

+ Gender agreement

  John has a Porsche. He/it/she is attractive.

+ Number agreement

  John’s parents like opera. John hates it/John hates them

+ Person and case agreement

  ◦ Nominative(主格): I, we, you, he, she, they
  ◦ Accusative(宾格): me,us,you,him,her,them
  ◦ Genitive(所有格): my,our,your,his,her,their
  George and Edward brought bread and cheese. They shared them.

2. binding theory - Syntactic constraints

   **reflexive** required/prohibited (反身代词)
   反身代词可以用于同指包含它的最近邻从句的主语，而非反身代词不能同指该主语
   – John bought himself a new Ford. [himself=John]
   – John bought him a new Ford. [him≠John]
   – John said that Bill bought him a new Ford. [him≠Bill]
   – J said that B bought himself a new F. [himself=Bill]
   – He said that he bought J a new Ford. [both he≠J]

3. Selectional restrictions

   动词对论元(argument)施加的选择限制
   John parked his car in the garage after driving it around for hours.
   动词 drive 要求直接宾语是能够驾驶的事物，比如说 car

   John left his plane in the hangar.
   He had flown it from Memphis this morning.

### Pronoun Interpretation Preferences

优先级

1. Recency(近因) - Sentence ordering

   John bought a new boat. Bill bought a bigger one. Mary likes to sail it.

2. Parallelism(排比)

   Saturday, Mary went with Sue to the farmer’s
   market.
   Sally went with her to the bookstore.
   Sunday, Mary went with Sue to the mall.
   Sally told her she should get over her shopping
   obsession.

3. Grammatical Role

   subj>obj>others

   John went to the Acura dealership with Bill. He
   bought an Integra.
   Bill went to the Acura dealership with John. He
   bought an Integra.
   John and Bill went to the Acura dealership. He
   bought an Integra

4. Repeated mention

   John needed a car to go to his new job. He
   decided that he wanted something sporty. Bill
   went to the dealership with him. He bought a
   Miata.

   Who bought the Miata?  According grammatical role, bill bought the Miata, but actually it's John!   

5. Verb semantics/thematic roles

   有些动词的出现会对其中一个论元的位置产生语义上的强调，这会造成对其后代词的理解偏差.
   John **phoned/criticized** Bill. He lost the laptop.
   如果是 phone，明显应该是 John 丢了电脑，如果是 criticize，应该是 Bill 丢了。这被认为是动词的“隐含因果关系”，criticize 事件的隐含因果被认为是动词宾语，而 phone 被认为是动词主语

### Factors of Reference Resolution

+ Lexical factors
  ◦ Reference type: Inferrability, discontinuous set, generics, one anaphora, pronouns,…

+ Discourse factors:
  ◦ Recency
  ◦ Focus/topic structure, digression
  ◦ Repeated mention

+ Syntactic factors:
  ◦ Agreement: gender, number, person, case
  ◦ Parallel construction
  ◦ Grammatical role<br>◦ Selectional restrictions

+ Semantic/lexical factors
  ◦ Verb semantics, thematic role

+ Pragmatic factors

  ◦ Context-dependent meaning

  Jeb Bush was helped by his brother and so was Frank
  Lautenberg. (Strict vs. Sloppy)
  Mike Bloomberg bet George Pataki a baseball cap
  that he could/couldn’t run the marathon in under 3
  hours.
  Mike Bloomberg bet George Pataki a baseball cap
  that he could/couldn’t be hypnotized in under 1
  minute.

### Discourse Model

When a referent is first mentioned in a discourse, a representation is evoked in the
model
◦ Information predicated of it is stored also in the model
◦ On subsequent mention, it is accessed from the model

Referents of pronouns usually require some degree of salience in the discourse (as opposed to definite and indefinite NPs, e.g.)

+ How do items become salient in discourse?

  Salience via Simple Recency :question:

  Salience via Structural Recency :question:

  推理对象(inferrable)、不连续集(discontinuous set)和类属(generic)


### Algorithms

Lappin & Leas ‘94: weighting via recency and syntactic preferences. [paper](http://www.aclweb.org/anthology/J/J94/J94-4002.pdf)


Weights candidate antecedents by recency and syntactic preference (86% accuracy)

Two major functions to perform:
◦ Update the discourse model when an NP that evokes a new entity is found in the text, computing the salience of this entity for future anaphora resolution
◦ Find most likely referent for current anaphor by considering possible antecedents and their salience values

Partial example for 3P, non-reflexives

+ Saliency Factor Weights

  Sentence recency (in current sentence?) 100<br>Subject emphasis (is it the subject?) 80<br>Existential emphasis (existential prednom?) 70<br>Accusative emphasis (is it the dir obj?) 50<br>Indirect object/oblique comp emphasis 40<br>Non-adverbial emphasis (not in PP,) 50<br>Head noun emphasis (is head noun) 80

Implicit ordering of arguments:
subj/exist pred/obj/indobjoblique/dem.advPP

Update:
◦ Weights accumulate over time
◦ Cut in half after each sentence processed
◦ Salience values for subsequent referents accumulate for equivalence class of coreferential items (exceptions, e.g. multiple references in same sentence)<br>◦ Additional salience weights for grammatical role parallelism (35) and cataphora (-175) calculated when pronoun to be resolved
◦ Additional constraints on gender/number agrmt/syntax

+ Reference Resolution

  Collect potential referents (所指) (up to four sentences back): `{sofa,cat,bonbons}`
  Remove those that don’t agree in number/gender with pronoun `{bonbons}`
  Remove those that don’t pass intra-sentential syntactic coreference constraints
  `The cat washed it. (it≠cat)`
  Add applicable values for role parallelism (+35) or cataphora (-175) to current salience
  value for each potential antecedent
  Select referent with highest salience; if tie, select closest referent in string



#### Example

On the sofa, the cat was eating bonbons.
sofa: 100+80=180
cat: 100+80+50+80=310
bonbons: 100+50+50+80=280

The bonbons were clearly very tasty.
sofa: 180/2=90
cat: 310/2=155
bonbons: 280/2 +(100+80+50+80)=450

They were a gift from an unknown admirer.
sofa: 90/2=45
cat: 155/2=77.5
bonbons: 450/2=225 (+35) = 260….

---

Hobbs ‘78: syntax tree-based referential search



### Tools

[JavaRAP](http://wing.comp.nus.edu.sg/~qiu/NLPTools/JavaRAP.html) | [code](https://github.com/WING-NUS/JavaRAP)

[Stanford Deterministic Coreference Resolution System](https://nlp.stanford.edu/software/dcoref.shtml)

[ArkRef](http://www.ark.cs.cmu.edu/ARKref/) 

[SuperSense tagger](http://medialab.di.unipi.it/wiki/SuperSense_Tagger)

[Pronoun_Annotator](https://github.com/philgooch/Pronoun_Annotator)

https://www.minvolai.com/coreference-resolution-tools-a-first-look/ - 2010



