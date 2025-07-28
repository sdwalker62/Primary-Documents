There are two common forms of supervised learning that we will talk about - _classification_ and _regression_ (there are other forms too such as _ranking_, _metric learning_, _sequence learning_, etc.). 

The primary difference between classification and regression is the type of label we can assign to an example. In classification problems the label is **discrete** and in regression problems the label is **continuous**. 

An example classification problem is mapping a person to the set $\{\text{parent}, \neg \text{parent}\}$. If we were a grocery story we might be interested in this mapping so that we can tailor advertisements to them for items commonly purchased by a parent or vice versa. 

An example regression problem is housing prices. If we take some number of features about a house such as square footage, number of bed rooms, etc. we want to learn a function that maps to a real number that represents price, 

$$f(\text{ft (sq)}, \text{bedroom count}, \ldots) \rightarrow \text{price} \in \mathbb{R}.$$
## Survey of Terms

#### Instances
Instances (or inputs) are vectors of attributes or values that define your input space. If your input space are pictures then your instances are the vectors of pixels that comprise an image. 

#### Concept
The function which maps inputs to outputs. Intuitively, a concept is an idea that describes a set of things. For example, what is the defining characteristic or concept of a parent is when we are labeling customers in the grocery store problem. Take cars as another example, when discussing the concept of a car we take the things which we commonly associate with a car such as a steering wheel, engine, radio and use them to identify a car. The attributes are then mapping these concepts to the notion or concept of a car. 

#### Target Concept
The difference between a target concept and a general notion of a concept is the target concept is the actual answer, it is the thing we are seeking to find. In other words, it is the correct hypothesis from our set of possible hypotheses. The true mapping of attributes to cars or parents is the one which is always right, we are trying to learn a function that is as approximate to this function as possible. Our function may take the attributes and mis-identify the instance as a truck or motorcycle instead of a car, but as we approximate the true function more faithfully, these errors are minimized. 

#### Hypothesis Class
The set of all concepts that you are willing to entertain (all the functions we are willing to consider). This links back to the inductive bias, since we will make assumptions about the target concept which allows us to narrow our hypothesis class and make learning easier. 

In the case of classification, we limit our hypothesis class to those which map to discrete values. In regression, we limit the hypothesis class to those which map to continuous values. 

#### Sample
A training set is a set of all of our inputs paired with the correct label. It is a tuple of instances with their correct labels so that we can inductively compute the target concept. 

If I was describing to you what a car is and the properties and features which are common to cars you will inductively learn to identify them. I do this instead of providing a dictionary which defines exactly what a car is. 

#### Candidate
A candidate is simply a concept that you think might be the target concept. It is a concept which may accurately map examples to the labels when evaluated. 

#### Testing Set
A testing set is identical to a training set, it is a tuple of instances and their associated labels. We will hold out this set from learning on to evaluate our understanding of the target concept. The more instances we correctly associate with the target label, the better we rank our candidate concept until we learn a concept which is near enough the target. 

The training set and testing set should be **separate**. We cannot test if our understanding generalizes if we apply our concept to the examples we have already seen. 