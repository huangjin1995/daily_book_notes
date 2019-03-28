CS231n



#### (Truncated) Backpropagation through time

Backpropagation through time: 

Forward through entire sequence to compute loss, then backward through entire sequence to compute gradient

Truncated Backpropagation through time:

Run forward and backward through chunks of the sequence instead of whole sequence, Carry hidden states forward in time forever, but only backpropagate for some smaller number of steps.



#### Searching for interpretable cells

Karpathy, Johnson, and Fei-Fei: Visualizing and Understanding Recurrent Networks, ICLR Workshop 2016



##### Question

What's (each cell of) RNN learned in this sequence learning?

How to make RNN learn the structure of sequence?

#### RNN (Gradient flow)

Computing gradient of $h_0$ involves many factors of $W$ (and repeated $tanh$)

(During the backwards pass, we are continually multiply by the **same** weight matrix $W$ over and over again)

Largest singular value of $W$ > 1:  $\rightarrow$  Gradient clipping: Scale gradient if its norm is too big
Exploding gradients

Largest singular value of $W$ < 1:  $\rightarrow$  Change RNN architecture (LSTM.GRU/...)
Vanishing gradients

![rnn_gradient_flow](https://github.com/bifeng/daily_book_notes/raw/master/resource/rnn_gradient_flow.png)



#### LSTM (Gradient flow)

LSTM: A Search Space Odyssey, Greff et al., 2015 :star::star::star::star::star:

The idea of managing gradient flow properly through these additive connections and these multiplicative gates is super useful.

Backpropagation from $c_t$ to $c_{t-1}$ only elementwise multiplication by $f$, no matrix multiply by $W$

(During the backward pass, elementwise multiplication will potentially be multiplying by a **different** forget gate at every time step. The forget gate is coming out from a sigmoid and guaranteed to be **between zero and one**, which leads to sort of nicer numerical properties if you imagine multiplying by these things over and over again.)

If you imagine backpropagating from the final hidden state back to the first cell state, then through that backward path, we only backpropagate through a single tanh nonlinearity rather than through a separate tanh at every time step.

![lstm_gradient_flow](https://github.com/bifeng/daily_book_notes/raw/master/resource/lstm_gradient_flow.png)

In this residual network, we had this path of identity connections going backward through the network and that give sort of a gradient super highway for gradients to flow backward in ResNet. It's kind of the same intuition in LSTM, where these additive and elemenwise multiplicative interactions of the cell state can give a similar gradient super highway for gradients to flow backwards through the cell state in an LSTM.

By the way, the Highway Networks is kind of in between this idea of the LSTM cell and these residual networks



##### Question

+ If you imagine backpropagating from the final hidden state back to the first cell state, then through that backward path, we only backpropagate through a single tanh nonlinearity rather than through a separate tanh at every time step. How to understand it ?

+ Due to the nonlinearities, Could this still be susceptible to vanishing gradients?

  That could be the case. Maybe if these forget gates are always less than one, you might get vanishing gradients as you continually go though these forget gates.

  One sort of trick that people do in practice is that initialize the biases of the forget gate to be somewhat positive. So that at the beginning of training those forget gates are always very close to one.











#### GRU



#### Other RNN Variants

An Empirical Exploration of Recurrent Network Architectures, Jozefowicz et al., 2015 :star::star::star::star::star:





#### Image Captioning

Explain Images with Multimodal Recurrent Neural Networks, Mao et al.
Deep Visual-Semantic Alignments for Generating Image Descriptions, Karpathy and Fei-Fei
Show and Tell: A Neural Image Caption Generator, Vinyals et al.
Long-term Recurrent Convolutional Networks for Visual Recognition and Description, Donahue et al.
Learning a Recurrent Visual Representation for Image Caption Generation, Chen and Zitnick

##### Image Captioning with Attention

RNN focuses its attention at a different spatial location when generating each word

Xu et al, “Show, Attend, and Tell: Neural Image Caption Generation with Visual Attention”, ICML 2015



#### Visual Question Answering

Agrawal et al, “VQA: Visual Question Answering”, ICCV 2015

##### Visual Question Answering: RNNs with Attention

Zhu et al, “Visual 7W: Grounded Question Answering in Images”, CVPR 2016



