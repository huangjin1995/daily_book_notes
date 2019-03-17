refer: CS231n

http://cs231n.github.io/neural-networks-3/



1. preprocess the data

2. choose the architecture

   **double check** that the loss is reasonable 

   1) disable regularization

   loss is what you expected.

   2) crank up regularization

   loss went up, good.

3. train

   1) start up with a very small amount of data and turn off regularization

   If you have a very small training set, you should be able to overfit this very well, and get very good training loss.

   2) Start with small regularization and find learning rate that makes the loss go down

   loss not going down: learning rate too low
   loss exploding: learning rate too high

   => Rough range for learning rate we should be cross-validating is somewhere [1e-3 … 1e-5].

4. monitor and visulize

   the loss curve

   the accuracy (training and validation)

5. track 

   the ratio of weight updates / weight magnitudes

   You might want to evaluate and track this ratio for every set of parameters independently. A rough heuristic is that this ratio should be somewhere around 1e-3 (0.001). If it is lower than this then the learning rate might be too low. If it is higher then the learning rate is likely too high. 

   ratio between the updates and values: ~ 0.0002 / 0.02 = 0.01 (about okay) 

   ```python
   # assume parameter vector W and its gradient vector dW
   param_scale = np.linalg.norm(W.ravel())
   update = -learning_rate*dW # simple SGD update
   update_scale = np.linalg.norm(update.ravel())
   W += update # the actual update
   print update_scale / param_scale # want ~1e-3
   ```

   

