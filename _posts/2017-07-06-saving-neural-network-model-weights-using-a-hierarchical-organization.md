---
layout:     post
title:      "Saving Neural Network Model Weights Using a Hierarchical Organization"
date:       2017-07-06 10:00:00
permalink:  2017/07/06/saving-neural-network-model-weights-using-a-hierarchical-organization/
---

Over the last two weeks, I have been using more Theano-based code for Deep
Learning instead of TensorFlow, in part due to diving into OpenAI's [Generative
Adversarial Imitation Learning code][1]. 

That code base has also taught me something that I have wondered about on
occasion: what is the "proper" way to save and load neural network model
weights? At the very least, how should we as programmers save weights in a way
that's robust, scalable, and easy to understand? In my view, there are two major
steps to this procedure:

1. Extracting or setting the model weights from a single vector of parameters.
2. Actually storing that vector of weights in a file.

One way to do the first step is to save model weights in a vector, and use that
vector to load the weights back to the model as needed. I do this in [my
personal reinforcement learning repository][2], for instance. It's implemented
in TensorFlow, but the main ideas still hold across Deep Learning software.
Here's a conceptually self-contained code snippet for *setting* model weights
from a vector `self.theta`:

{% highlight python %}
self.theta = tf.placeholder(tf.float32, shape=[self.num_params], name="theta")
start = 0
updates = []
for v in self.params:
    shape = v.get_shape()
    size = tf.reduce_prod(shape)
    # Note that tf.assign(ref, value) assigns `value` to `ref`.
    updates.append( 
            tf.assign(v, tf.reshape(self.theta[start:start+size], shape)) 
    )
    start += size
self.set_params_flat_op = tf.group(*updates) # Performs all updates together.
{% endhighlight %}

In later code, I run TensorFlow sessions on `self.set_params_flat_op` and supply
`self.theta` with the weight vector in the `feed_dict`.  Then it iteratively
makes an update to extract a segment of the `self.theta` vector and assigns it
to the correct weight. The main thing to watch out about here is that
`self.theta` actually contains the weights in the correct ordering.

I'm more curious about the second stage of this process, that of saving and
loading weights into files. I used to use pickle files to save the weight
vectors, but one problem is the [incompatibility between Python 2 and Python 3
pickle files][3]. Given that I sometimes switch back and forth between
versions, and that I'd like to keep the files consistent across versions, this
is a huge bummer for me. Another downside is the lack of *organization*. Again,
I still have to be careful to ensure that the weights are stored in the correct
ordering so that I can use `self.theta[start:start+size]`.

After looking at how the GAIL code stores and loads model weights, I realized
it's different from saving single pickle or numpy arrays.  I started by running
their Trust Region Policy Optimization code (`scripts/run_rl_mj.py`) and
observed that the code specifies neural network weights with a list of
dictionaries. Nice! I was wondering about how I could better generalize my
existing neural network code. 

Moving on, what happens after saving the snapshots? (In Deep Learning it's
common to refer to weights after specific iterations as "snapshots" to be
saved.) The GAIL code uses a `TrainingLog` class which utilizes [PyTables][4]
and --- by extension --- the HDF5 file format. If I run the TRPO code I might
get `trpo_logs/CartPole-v0.h5` as the output file. It doesn't have to end with
the HDF5 extension `.h5` but that's the convention. Policies in the code are
subclasses of a generic `Policy` class to handle the case of discrete versus
continuous control. The `Policy` class is a subclass of an abstract `Model`
class which provides an interface for saving and loading weights.

I decided to explore a bit more, this time using the pre-trained CartPole-v0
policy provided by GAIL:

{% highlight python %}
In [1]: import h5py

In [2]: with h5py.File("expert_policies/classic/CartPole-v0.h5", "r") as f:
   ...:     print(f.keys())
   ...:     
[u'log', u'snapshots']

In [3]: with h5py.File("expert_policies/classic/CartPole-v0.h5", "r") as f:
   ...:     print(f['log'])
   ...:     print(f['snapshots'])
   ...:     
<HDF5 dataset "log": shape (101,), type "|V80">
<HDF5 group "/snapshots" (6 members)>

In [4]: with h5py.File("expert_policies/classic/CartPole-v0.h5", "r") as f:
   ...:     print(f['snapshots/iter0000100/GibbsPolicy/hidden/FeedforwardNet/layer_0/AffineLayer/W'].value)
   ...: 
# value gets printed here ...
{% endhighlight %}

It took me a while to figure this out, but here's how to walk through the nodes
in the entire file:

{% highlight python %}
In [5]: def print_attrs(name, obj):
   ...:     print(name)
   ...:     for key, val in obj.attrs.iteritems():
   ...:         print("  {}: {}".format(key, val))
   ...:         

In [6]: expert_policy = h5py.File("expert_policies/classic/CartPole-v0.h5", "r")

In [7]: expert_policy.visititems(print_attrs)

# Lots of stuff printed here!
{% endhighlight %}

PyTables works well for *hierarchical data*, which is nice for Deep
Reinforcement Learning because there are many ways to form a hierarchy:
snapshots, iterations, layers, weights, and so on.  All in all, PyTables looks
like a tremendously useful library. I should definitely consider using it to
store weights. Furthermore, even if it would be easier to store with a single
weight vector as I now do (see my TensorFlow code snippet from earlier) the
generality of PyTables means it might have cross-over effects to other code I
want to run in the future. Who knows?

[1]:https://danieltakeshi.github.io/2017/06/15/openais-generative-adversarial-imitation-learning-code/
[2]:https://github.com/DanielTakeshi/rl_algorithms
[3]:https://stackoverflow.com/questions/28218466/unpickling-a-python-2-object-with-python-3
[4]:http://www.pytables.org/
