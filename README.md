# Srinath Siddamsetty

# Sigmoid Function
Sigmoid function is one of the mostly-used and well-known activation functions.The output of the activation function is always going to be in range (0,1) compared to (−∞,∞) of linear function. So we have our activations bound in a range. The activations will not blow up then. However, there are couple of problems with sigmoid function.Towards either end of the sigmoid function, the y values tend to respond very less to changes in x. The gradient at that region is going to be small. It gives rise to a problem of “vanishing gradients” because derivative of sigmoid is always less than 0.25 for all inputs except 0. Sigmoid neurons will stop learning when they saturate.

# Hyperbolic Tangent Function
Another popular activation function is Hyperbolic Tangent function. Hyperbolic Tangent function, also known as tanh function, is a rescaled version of the sigmoid function.It has characteristics similar to sigmoid function. It is nonlinear in nature, so, we can stack layers. The tanh non-linearity squashes real numbers to range between [−1,1] so one needs not to worry about activations blowing up. The gradient is stronger for tanh than sigmoid (derivatives are steeper). Deciding between the sigmoid or tanh will depend on your requirement of gradient strength. However, unlike the sigmoid neuron, the output of tanh function is zero-centered.

# Rectified Linear Unit (ReLU)
ReLU is a piecewise non-linear function that corresponds to:
> ReLU(x)={0 if x<0 ;x if x≥0
Another way of writing the ReLU function is like so:ReLU(x)=max(0,x)
 
where x is the input to a neuron. In other words, when the input is smaller than zero, the function will output zero. Else, the function will mimic the identity function. So, the range of ReLU is between 0 to ∞.

ReLU is less computationally expensive than tanh and sigmoid neurons due to its linear, non-saturating form and involving simpler mathematical operations. It’s very fast to compute because its derivative is easy to handle. When the input is greater or equal to zero, the output is simply the input, and hence the derivative is equal to one. The function is not differentiable at zero.

**Zeros initialization** -- setting initialization = "zeros" in the input argument.
**Random initialization** -- setting initialization = "random" in the input argument. This initializes the weights to large random values.
**He initialization** -- setting initialization = "he" in the input argument. This initializes the weights to random values scaled according to a paper by He et al., 2015.

### Different initializations lead to different results
- Random initialization is used to break symmetry and make sure different hidden units can learn different things
- Don't intialize to values that are too large
- He initialization works well for networks with ReLU activations.

# Need for adaptive learning rate:
Assume, if the model we’re going to frame is of f(x) = W.x + B. For this simple model, let’s check how parameter update happens:

As we saw from the above derivations, if a particular feature say x1 is sparse and 0 most of the times, gradient of weight of that particular feature(grad w1) will be 0 mostly, leading to no updates for weight of that feature(w1). It will take lot of epochs for weight of that particular feature to converge at an optimal value. To avoid that, we need an adaptive learning rate where the learning rate should grow to some large value if we encounter a sparse feature. Adagrad comes to the rescue!

## Adagrad:

The main objective of this algorithm is to make better updates for sparse features. For that, it brings in adaptive learning rate, where learning rate varies for both sparse feature and dense feature. For sparse feature, grad(w) will be zero and hence vt will be minimal, which leads to increase in W(larger parameter update).For dense features, if vt increases, learning rate decays and eventually lead to minimal updates to parameters of those features.
## RMSProp:
      To address the learning rate decay of dense features in Adagrad, RMSProp introduces an additional hyperparameter(beta).With introduction of additional parameter(beta), we can fix the learning rate decay problem for dense feature.RMSProp takes sparse and dense features into account and adapts the learning rate accordingly. But it did not take into account the momentum(history). This lead to advent of Adam optimizer.
## Adam Optimizer:
     Adam optimizer clubs both RMSProp approach(which addresses parameter updates for sparse and dense features) and Momentum based GD(which updates parameters based on history). 
