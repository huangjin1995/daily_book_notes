cs231n

### multiple independent model

Train multiple independent models, use different initial random restarts



### snapshot of single model

Instead of training independent models, use multiple snapshots of a single model during training!

Cyclic learning rate schedules can make this work even better!

Huang et al, “Snapshot ensembles: train 1, get M for free”, ICLR 2017



Instead of using actual parameter vector, keep a moving average of the parameter vector and use that at test time (Polyak averaging)

Polyak and Juditsky, “Acceleration of stochastic approximation by averaging”, SIAM Journal on Control and Optimization, 1992.





