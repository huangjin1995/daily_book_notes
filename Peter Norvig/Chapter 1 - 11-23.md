## Chapter 1

### The history of artificial intelligence

#### The gestation of AI (1943-1955)

Alan Turing's vision. 

He introduced the Turing Test, machine learning, genetic algorithms, and reinforcement learning.

#### The birth of AI (1956)

The Dartmouth workshop.

It introduce all the major figures to each other.

#### Early enthusiasm, great expectations (1952-1969)

Newell and Simon (1976) formulate the famous **physical symbol system** hypothesis, which states that "a physical symbol system has the necessary and sufficient means for general intelligent action."

...

#### A dose of reality (1966-1973)

The first kind of difficulty arose because most early programs knew nothing of their subject matter; they succeeded by means of simple syntactic manipulations.<br>(Such as dictionary-based method in machine translation)

The second kind of difficulty was the intractability of many of the problems that AI was attempting to solve.<br>(Such as solve problems by trying out different combinations of steps until the solution was found - "combinatorial explosion")

The third kind of difficulty was some fundamental limitations on the basic structures being used to generate intelligent behavior.<br>(Such as Minsky and Papert's book Perceptrons (1969) proved that a two-input perceptron could not be trained to recognize when its two inputs were different, but the new back-propagation learning algorithms for multilayer networks was discovered first in 1969 (Bryson and Ho, 1969).)

#### Knowledge-based systems: The key to power? (1969-1979)

Feigenbaum and others at Stanford began the Heuristic Programming Project (HPP) to investigate the extent to which the new methodology of **expert systems** could be applied to other areas of human expertise.

The widespread growth of applications to real-world problems caused a concurrent increase in the demands for **workable knowledge representations schemes**. Some were based on
logic..., Others, following Minsky’s idea of **frames** (1975), adopted a more
structured approach, assembling facts about particular object and event types and arranging
the types into a large taxonomic hierarchy analogous to a biological taxonomy.

#### The return of neural networks (1986-present)

These so-called **connectionist models** of intelligent systems were seen by some as direct
competitors both to the **symbolic models** promoted by Newell and Simon and to the
**logicist approach** of McCarthy and others (Smolensky, 1988).

...

There is a recognition that machine learning should not be isolated from information theory, that uncertain reasoning should not be isolated from stochastic modeling, that search should not be isolated from classical optimization and control, and that automated reasoning should not be isolated from formal methods and static analysis.

...

Such as approaches based on hidden Markov models (HMMs) in speech recognition、 an approach based on sequences of words, with models learned according to the principles of information theory in machine translation.

...

Judea Pearl’s (1988) Probabilistic Reasoning in Intelligent Systems led to a new acceptance of probability and decision theory in AI, following a resurgence of interest epitomized by Peter Cheeseman’s (1985) article “In Defense of Probability.” The Bayesian network formalism was invented to allow efficient representation of, and rigorous reasoning with, uncertain knowledge. This approach now dominates AI research on uncertain reasoning and expert systems.

...

Work by Judea Pearl (1982a) and by Eric Horvitz and David Heckerman (Horvitz and Heckerman, 1986; Horvitz et al., 1986) promoted the idea of **normative expert systems**: ones that act rationally according to the laws of decision theory and do not try to imitate the thought steps of human experts. The $Windows^{TM}$ operating system includes several normative diagnostic expert systems for correcting problems.

#### The availability of very large data sets (2001-present)

The “knowledge bottleneck” in AI—the problem of how to express all the knowledge that a system needs—may be solved in many applications by learning methods rather than hand-coded knowledge engineering, provided the learning algorithms have **enough data** to go on (Halevy et al., 2009).

Such as, Yarowsky’s (1995) work on word-sense disambiguation: given the use of the word “plant” in a sentence, does that refer to flora or factory? Previous approaches to the problem had relied on human-labeled examples combined with machine learning algorithms. Yarowsky showed that the task can be done, with accuracy above 96%, with no labeled examples at all. Instead, given a very large corpus of unannotated text and just the dictionary definitions of the two senses—“works, industrial plant” and “flora, plant life”—one can label examples in the corpus, and from there **bootstrap** to learn new patterns that help label new examples.













