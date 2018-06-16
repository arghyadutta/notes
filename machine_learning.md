No definite plan about this will go on. But right now I have started to learn
ML from various sources. I will just put down the notes from there. We will try
to sort it later.

2018-05-30, Mainz:

Andrew Ng's course:
Arthur Samuel(1959) ML is the field of study that gives computers the
ability to learn without being explicitly programmed.
Tom Mitchell(1998) Well-posed ML problem: A computer program is said to
learn from experience E with respect to some task T and some performance
measure P, if its performance on T, as measured by P, improves with
experience E.

Types of ML
- Supervised learning
- Unsupervised learning

#### Supervised learning
Example given: house price prediction algorithm
Question: how is it different from linear/Quadratic fitting?
"Right answers given" (meaning, we know whether it is benign or malignant tumor
for a particular size from our dataset, or we know the house price given
the size for samples in our dataset.)
Regression problem (continuous output variable)
Classification problem: Discrete output variable
In classification we can either plot the value of attributes in a
attribute vs value Y/N plot. Or we can omit the Y axis, and put
different labels for the different values. Because we are classifying
features for breast cancer: age, tumor size, clump thickness, uniformity of cell size, uniformity of cell shape
Support vector machine can have infinite number of features.

#### Unsupervised learning
The data does not have any label. No right or wrong answer. Given the
dataset can you find some structures or patterns.

Example: Given a dataset, find clusters based on some criteria.
(Clustering) Like Google news clusters stories from 1000s of different
newspaper on the same topic and present them together in Google News. Used to organize computing clusters, social network analysis,
market segmentation, astronomical data analysis

Cocktail party problem (non-clustering):
Find structure in a chaotic environment.
All the people talking at the same time,
2 people talking at the same time to 2 microphones set
at different distances from the peoples. This algorithm separate
out voices of different people based on the recording. Can be solved
using SVD (singular value decomposition). Advertisement for Octave follows.

### New
#### Supervised learning. Linear regression
Regression predictts a real valued output
Given : Training set of housing prices
$m$ : Number of training examples
$\mathbf{x}$ : input variables/features
$\mathbf{y}$ : Output variable/"target" variable
$(x,y)$ : one training example
$(x^(i), y^(i))$ : ith training examople

Training set -> {Size of house, Learning algorithm} -> hypothesis ->
Estimated price

$h_\theta(x)=\theta_0+\theta_1 x$
\theta_0 \theta_1: parameters for the hypothesis. Choose them so that h is 
"close" to y for our training examples

Cost function:
$1/2m\text{minimize}_{\theta_0,\theta_1}\sum_{i=1}^m(h_\theta(x^(i)-y^(i))^2$

Intuition about the cost function:
We have 
hypothesis: $h_\theta(x)=\theta_0+\theta_1 x$
paprameters:  \theta_0 \theta_1
cost function $J(\theta_0 \theta_1) =
1/2m\text{minimize}_{\theta_0,\theta_1}\sum_{i=1}^m(h_\theta(x^(i)-y^(i))^2$
goal $\text{minimize}_{\theta_0,\theta_1}J(\theta_0 \theta_1)$

Notice that h(x) is fixed for a fixed choice of \theta,
but J is a function of papramter \theta. In x-y plane, h is a line. In J
- \theta plane, it is 1 point. 

Tristan said that we make the error in the training set =0. Is that true?
I am just thinking about what I read in the ML review by Pankaj Mehta.
Need to clarify later.

Contour plots : Interesting discussion.

### Gradient descent algorithm for minimizing the cost function J
Start with some theta =0 lets say, then keep changing until we reach a
minimum of J.

$\theta_j:=\theta_j-\alpha \frac{\partial}{\partial\theta_j}J$ for $j=0,1$
Simultaneously update all \theta s.

$\alpha$ is called the "Learning rate".

Batch gradient descent. Batch means in each step of gradient descent used
all the training examples. This just means the sum of the training samples from
1 to m in J. 
