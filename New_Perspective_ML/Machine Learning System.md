### conference

+ SysML

  http://www.sysml.cc/

  http://www.sysml.cc/2018/index.html

+ Systems for ML

  http://learningsys.org/nips18/index.html

### paper

+ SysML: The New Frontier of Machine Learning Systems, Alexander Ratner, Dan Alistarh, Gustavo Alonso, Peter Bailis, Sarah Bird, Nicholas Carlini, Bryan Catanzaro, Eric Chung, Bill Dally, Jeff Dean, Inderjit S. Dhillon, Alexandros Dimakis, Pradeep Dubey, Charles Elkan, Grigori Fursin, Gregory R. Ganger, Lise Getoor, Phillip B. Gibbons, Garth A. Gibson, Joseph E. Gonzalez, Justin Gottschlich, Song Han, Kim Hazelwood, Furong Huang, Martin Jaggi, Kevin Jamieson, Michael I. Jordan, Gauri Joshi, Rania Khalaf, Jason Knight, Jakub Konečný, Tim Kraska, Arun Kumar, Anastasios Kyrillidis, Jing Li, Samuel Madden, H. Brendan McMahan, Erik Meijer, Ioannis Mitliagkas, Rajat Monga, Derek Murray, Dimitris Papailiopoulos, Gennady Pekhimenko, Theodoros Rekatsinas, Afshin Rostamizadeh, Christopher Ré, Christopher De Sa, Hanie Sedghi, Siddhartha Sen, Virginia Smith, Alex Smola, Dawn Song, Evan Sparks, Ion Stoica, Vivienne Sze, Madeleine Udell, Joaquin Vanschoren, Shivaram Venkataraman, Rashmi Vinayak, Markus Weimer, Andrew Gordon Wilson, Eric Xing, Matei Zaharia, Ce Zhang, Ameet Talwalkar. white paper [arxiv](https://arxiv.org/abs/1904.03257) 
+ Machine Learning for Systems and Systems for Machine Learning, Jeff Dean (Google Brain), [paper](http://learningsys.org/nips17/assets/slides/dean-nips17.pdf) 
+ [Systems and Machine Learning Symbiosis](https://youtu.be/Nj6uxDki6-0), Jeff Dean



Motivation: The Rise of Full Stack Bottlenecks in ML

In real-world deployments, a range of bottlenecks begin to surface, which crucially are full-stack, systems-level concerns, rather than solely properties of the core machine learning algorithms. These include:

+ Deployment concerns: As ML becomes used in increasingly diverse and mission-critical ways, a new crop of
  systems-wide concerns has become increasingly prevalent. These include **robustness** to adversarial influences
  or other spurious factors; **safety** more broadly considered; **privacy** and **security**, especially as sensitive data is
  increasingly used; **interpretability**, as is increasingly both legally and operationally required; **fairness**, as ML
  algorithms begin to have major effects on our everyday lives; and many other similar concerns.
+  Cost: The original default solution for learning a CNN over ImageNet cost $2,300 of compute and took 13 days
  to train [2]. Annotation of the huge volumes of training data can alone cost hundreds of thousands to millions
  of dollars. Reducing cost measured in terms of other metrics—such as latency or power—is also critical for an
  expanding range of device and production deployment profiles.
+  Accessibility: As a widening range of people rush to use ML for actual production purposes—including a new
  breed of polyglot data scientists trained by large new programs at universities—ML systems need to be usable
  by developers and organizations without PhD-level machine learning and systems expertise.

The shared element in these emerging pain points is that they are full-stack issues that require reasoning not just
over core ML algorithms and methods, but the hardware, software, and overall systems that support them as well.
As ML adoption and excitement increases, full-stack solutions to the above pain points will be increasingly critical
to bridging the gap between machine learning’s promise and real-world utility. 





