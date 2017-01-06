---
title: TensorFlow 学习(一)
date: 2017-01-03 09:43:14
tags: [TensorFlow, Learning]
mathjax: true
---

### Basic Usage
To use TensorFlow you need to understand how TensorFlow:
+ Represents computations as graphs.
+ Executes graphs in the context of `Sessions`.
+ Represents data as tensors.
+ Maintains state with `Variables`.
+ Uses feeds and fetches to get data into and out of arbitrary operations.

#### Overview
TensorFlow is a programming system in which you represent computations as graphs. Nodes in the graph are called ops (short for operations). An op takes zero or more `Tensors`, performs some computation, and produces zero or more `Tensors`. In TensorFlow terminology, a `Tensor` is a typed multi-dimensional array. For example, you can represent a mini-batch of images as a 4-D array of floating point numbers with dimensions `[batch, height, width, channels]`.

A TensorFlow graph is a description of computations. To compute anything, a graph must be launched in a `Session`. A `Session` places the graph ops onto `Devices`, such as CPUs or GPUs, and provides methods to execute them. These methods return tensors produced by ops as `numpy` `ndarray` objects in `Python`, and as `tensorflow::Tensor` instances in C and C++.

#### The computation graph
TensorFlow programs are usually structured into a construction phase, that assembles a graph, and an execution phase that uses a session to execute ops in the graph.

For example, it is common to create a graph to represent and train a neural network in the construction phase, and then repeatedly execute a set of training ops in the graph in the execution phase.

First Example:
```Python
from tensorflow import tf

matrix1 = tf.constant([[3., 3.]])
matrix2 = tf.constant([[2.],[2.]])

product = tf.matmul(matrix1, matrix2)

with tf.Session() as sess:
    result = sess.run([product])
    print (result)
```

#### Interactive Usage
```Python
import tensorflow as tf
sess = tf.InterativeSession()

x = tf.Variable([1.0, 2.0])
a = tf.constant([3.0, 3.0])

# Initialize 'x' using the run() method of its initializer op.
x.initializer.run()

sub = tf.sub(x, a)
print (sub.eval())

sess.close()
```
#### Tensor
TensorFlow programs use a tensor data structure to represent all data -- only tensors are passed between operations in the computation graph. You can think of a TensorFlow tensor as an n-dimensional array or list. A tensor has a static type, a rank, and a shape. 

#### Variables
Variables maintain state across executions of the graph.
```Python
#Create a Variable, that will be initialized to the scalar value 0.
state = tf.Variable(0, name="conunter")

# Create an Op to add one to 'state'.
one = tf.constant(1)
new_value = tf.add(state, one)
update = tf.assign(state, new_value)

# Varibale must be initialized by running an 'init' Op after having
# launched the graph. We first have to add the 'init' Op to the graph.
init_op = tf.global_variables_initializer()


# Launch the graph and run the ops.
with tf.Session() as sess:
    # Run the 'init' op
    sess.run(init_op)
    # Print the initial value of 'state'
    print (sess.run(state))
    # Run the op that updates 'state' and print 'state'
    for _ in range(3):
        sess.run(update)
        print (sess.run(state))
```

#### Fetches
To fetch the outputs of operations, execute the graph with a `run()` call on the **Session** object and pass in the tensors to retrieve.
为了取回操作的输出内容, 可以在使用 Session 对象的 run() 调用 执行图时, 传入一些 tensor, 这些 tensor 会帮助你取回结果.
```Python
input1 = tf.constant([3.0])
input2 = tf.constant([2.0])
input3 = tf.constant([5.0])
intermed = tf.add(input2, input3)
mul = tf.mul(input1, intermed)

with tf.Session() as sess:
    result = sess.run([mul, intermed])
    print (result)

# output
# [array([ 21.], dtype=float32), array([ 7.], dtype=float32)]
```

#### Feeds
The examples above introduce tensors into the computation graph by storing them in **Constants** and **Variables**. TensorFlow also provides a feed mechanism for patching a tensor directly into any operation in the graph.

A feed temporarily replaces the output of an operation with a tensor value. You supply feed data as an argument to a run() call. The feed is only used for the run call to which it is passed. The most common use case involves designating specific operations to be "feed" operations by using `tf.placeholder()` to create them:
```Python
input1 = tf.placeholder(tf.float32)
input2 = tf.placeholder(tf.float32)
output = tf.mul(input1, input2)

with tf.Session() as sess:
  print(sess.run([output], feed_dict={input1:[7.], input2:[2.]}))

# output:
# [array([ 14.], dtype=float32)]
```


---

### MNIST for ML Beginners
MNIST is a simple computer vision dataset.

#### Softmax Regressions
If you want to assign probabilities to an object being one of several different things, softmax is the thing to do, because softmax gives us a list of values between 0 and 1 that add up to 1. Even later on, when we train more sophisticated models, the final step will be a layer of softmax.

A softmax regression has two steps: first we add up the evidence of our input being in certain classes, and then we convert that evidence into probabilities.
为了得到一张给定图片属于某个特定数字类的证据(evidence),我们对图片像素值进行加权求和。如果这个像素具有很强的证据说明这张图片不属于该类,那么相应的权值为负数,相反如果这个像素拥有有利的证据支持这张图片属于这个类,那么权值是正数。

$$
\begin{eqnarray}
\nabla\cdot\vec{E} &=& \frac{\rho}{\epsilon_0} \
\nabla\cdot\vec{B} &=& 0 \
\nabla\times\vec{E} &=& -\frac{\partial B}{\partial t} \
\nabla\times\vec{B} &=& \mu_0\left(\vec{J}+\epsilon_0\frac{\partial E}{\partial t} \right)
\end{eqnarray}
$$
























