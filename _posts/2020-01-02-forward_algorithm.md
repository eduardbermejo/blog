# Forward algorithm for HMM

In this post, I will be going through the forward algorithm and the usages of this algorithm in Hidden Markov Models.
In the image below we can see the probabilistic graphical model depicting a hidden markov model. The $z_k$ correspond to the unobserved random variables called hidden or latent variables and $x_k$ correspont to the observed ones.

<img src="/images/HMM.png" style="border:0;" title="Hidden Markov Model">


Our goal is to compute: $p(z_k,x_{1:k})$ where $x_{1:k}=(x_1,...,x_k)$

We assume we know the emission probability distribution $p(x_{k}\|z_{k})$ and the transition probability distribution $p(z_{k}\|z_{k-1})$

The forward algorithm uses Dynamic Programming ro decrease computational complexity. So the first thing we need to do is to find a way to state that recursion. What we could do is explicitly add the previous hidden random variable back like so:

We know $p(z_{k},x_{1:k})$ is the marginal distribution over the subset $(z_{k},x_{1:k})$ and that marginalization is the process of summming the joint distribution over all values of the variable or variables being discarded. So we will make that summation explicit in order to get $z_{k-1}$ back:

$$
p(z_{k},x_{1:k}) =\sum_{z_{k-1}} p(z_{k},z_{k-1},x_{1:k})
$$

Next, we are going to expand this join probability into the following by using the chain rule of probability:

$$
\sum_{z_{k-1}} p(z_{k},Z_{k-1},x_{1:k})=\sum_{z_{k-1}} p(x_{k}|z_{k},z_{k-1},x_{1:k-1})p(z_{k}|z_{k-1},x_{1:k-1})p(z_{k-1},x_{1:k-1})
$$

Then you probably start to see the pattern, where now our computation has become recursive and our joint probability depends now on the joint probability one step back.

One thing about Hidden Markov Models is its Markov property and we can use that to look for conditional independence in our Bayesian Network. So for example, $x_{k}$ is independent of $z_{k-1}$ and $x_{1:k-1}$ given $z_{k}$. The same goes for $z_{k}$ that is independent of $x_{1:k-1}$ given $z_{k-1}$ 

So our equation ends up like this:

$$
p(z_{k},x_{1:k}) = \sum_{z_{k-1}} p(x_{k}|z_{k})p(z_{k}|z_{k-1})p(z_{k-1},x_{1:k-1})
$$

So now we can check what we have got so far. The first term $p(x_{k}\|z_{k})$ is known and the second term $p(z_{k}\|z_{k-1})$ as well being the first one the emission probability and the second one the transition probability.

Let us rewrite the equation as follows:

$$
\alpha_k(z_k) = \sum_{z_{k-1}} p(x_k|z_k)p(z_k|z_{k-1})\alpha_{k-1})\quad for \quad k=2,...,n
$$


The only thing left is defining $\alpha_1 = p(z_1,x_1) = p(z_1)p(x_1\|z_1)$
where $p(z_1)$ is the initial distribution.

So the computational complexity of this algorithm is $O(nm^2)$ being $n$ the number of steps and $m$ the possible hidden states. We need $m$ computations for each $z_k$ (the summation) and there are $m$ $z_k$ and that is for each value of $k$ (the steps of the hidden markov model).














