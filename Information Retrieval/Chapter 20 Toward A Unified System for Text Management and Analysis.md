an operator-based text analysis system



#### operators

It can be applied to many different problems;<br>It also be standardized and compatible with each other so that they can be
flexibly combined to support potentially many different workflows.

High level operators:

Select

Split

Union and Intersection

Ranking

TopicExtraction

Interpret

Compare



Low level operators:

Select -> querying, browsing and recommendation

Split -> categorization, clustering

TopicExtraction -> topic analysis



#### System Architecture

![System Architecture](https://github.com/bifeng/daily_book_notes/raw/master/resource/high_level_architecture.jpg)

​	Multiple levels of services are provided to users:<br>a preprocessing step of natural language processing<br>a low-level service for multi-mode text data access, which includes querying, browsing, and recommendation<br>a medium-level service for text data analysis, which includes general analysis operators that can be combined with each other<br>a high-level application support, which includes support of application-specific user tasks.

It is important that a user has access to all these levels via a unified interaction interface where the user also has access to a working space that is personalized according to a specific user and a specific application task.



#### Question

+ 

+ The principle of system design? Algorithm-oriented or Application-oriented?






