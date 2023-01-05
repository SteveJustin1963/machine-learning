# machine learning algorithm for low-power slow computer
see https://github.com/SteveJustin1963/machine-learning/wiki for notes 

## decision tree
- integer data is a,b,c
- find logic that satify boolean y
- make a truth table then apply decision tree
- write forth code

To find a logic that satisfies a boolean condition y, you can use a truth table and a decision tree.

A truth table is a table that lists all possible inputs to a logical system and the corresponding outputs. For example, if you have three integer variables a, b, and c, you can create a truth table with 2^3 = 8 rows, one for each possible combination of values for a, b, and c. Then, you can evaluate the boolean condition y for each row and record the result in the truth table.

Once you have created the truth table, you can use it to construct a decision tree. A decision tree is a graphical representation of a logical system that shows the possible paths of execution based on the values of the input variables. To create a decision tree from a truth table, you can start by selecting the input variables that have the most impact on the output of the logical system. Then, you can use the values of these variables to split the decision tree into branches, with each branch representing a different possible value for the input variables. You can continue to split the branches of the tree based on the values of the other input variables until you have covered all of the rows in the truth table.
```
: satisfy-boolean ( a b c -- )
  0 0 0 do
    i j k
    dup a and swap b and or c not or .
  loop
;
```
This code defines a Forth word (i.e., function) called satisfy-boolean that takes three input values a, b, and c and prints the result of the boolean condition y for each combination of a, b, and c.

To test the function, you can call it with different combinations of a, b, and c like this:
```
0 0 0 satisfy-boolean
0 0 1 satisfy-boolean
0 1 0 satisfy-boolean
0 1 1 satisfy-boolean
1 0 0 satisfy-boolean
1 0 1 satisfy-boolean
1 1 0 satisfy-boolean
1 1 1 satisfy-boolean
```

o apply a decision tree to find a logic that satisfies a boolean condition y, you can start by selecting the input variables that have the most impact on the output of the logical system. Then, you can use the values of these variables to split the decision tree into branches, with each branch representing a different possible value for the input variables. You can continue to split the branches of the tree based on the values of the other input variables until you reach a leaf node that represents a row in the truth table where the boolean condition y is satisfied.
```
: satisfy-boolean ( a b c -- a b c )
  a b and c not or
  if
    a b c
  else
    a if
      b if
        a b c
      else
        c if
          a b c
        else
          a b c
    else
      c if
        b if
          a b c
        else
          a b c
      else
        a b c
  then
;
```
This code defines a Forth word (i.e., function) called satisfy-boolean that takes three input values a, b, and c and returns the input values if the boolean condition y is satisfied, or splits the decision tree if the boolean condition is not satisfied.

To test the function, you can call it with different combinations of a, b, and c like this:
```
0 0 0 satisfy-boolean . . .
0 0 1 satisfy-boolean . . .
0 1 0 satisfy-boolean . . .
0 1 1 satisfy-boolean . . .
1 0 0 satisfy-boolean . . .
1 0 1 satisfy-boolean . . .
1 1 0 satisfy-boolean . . .
1 1 1 satisfy-boolean . . .
```
## Ref
- https://scikit-learn.org/stable/modules/tree.html
- https://en.wikipedia.org/wiki/Decision_tree_learning
- https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm
- https://en.wikipedia.org/wiki/Linear_model
- https://www.spiceworks.com/tech/artificial-intelligence/articles/linear-regression-vs-logistic-regression/
- https://en.wikipedia.org/wiki/Naive_Bayes_classifier

## k-nearest neighbors (KNN) algorithm, 
the prediction for a given data point is based on the class of its nearest neighbors. The number of nearest neighbors to consider is determined by the parameter k. For classification, the predicted class for the data point is the most common class among the k nearest neighbors. For regression, the predicted value for the data point is the average of the values of the k nearest neighbors.

The KNN algorithm is considered a non-parametric method, which means that it makes no assumptions about the underlying distribution of the data. It is a simple and flexible approach that can be used for both classification and regression tasks.

One advantage of the KNN algorithm is that it is relatively fast to train, as it does not require any complex parameter fitting. It is also relatively fast to make predictions, as it only requires calculating the distances between the test data point and the training data points.

However, the KNN algorithm can be sensitive to the choice of k and can be affected by the presence of outliers in the data. It can also perform poorly on high-dimensional data, as the distance between points can be dominated by a few dimensions that are unrelated to the target variable.

In example applied to integer data. The training data consists of pairs of integers [x1, x2] and corresponding labels y, and the goal is to predict the label for a new data point [x1, x2]. The algorithm calculates the distance between the new data point and all training data points, finds the k nearest neighbors, and returns the most common label among the nearest neighbors as the predicted label for the new data point.

## 4x4 Data Sample with 16 Integers in Forth
```
: cmp ( a b -- n )
  a distance < b distance > or ;

: classify ( points num-points point k -- label )
  2dup >r >r
  create pairs 4 * cells allot
  r@ r@ 0 do
    i cells + pairs i + ! pairs i @ point features swap - swap * + sqrt
  loop
  pairs qsort cmp
  r@ r@ 0 do
    pairs i @ label i cells + label-counts + 1 cells + +!
  loop
  rdrop rdrop
  0 max-label ! -1 max-count !
  label-counts num-points 0 do
    i cells + label-counts i @ max-count < if
      i max-label ! label-counts i @ max-count !
    then
  loop
  max-label ;

: main ( -- )
  points create data 16 cells allot
  data 0 , 0 , 1 , 2 , 4 , cells + , 0 , 2 , 3 , 4 , cells + , 0 , 3 , 1 , 4 , cells + , 1 , 4 , 5 , 4 , cells + , 1 , 5 , 4 , 4 , cells + , 1 , 6 , 7 , 4 , cells +
  point create data 1 cells allot
  data -1 , 2 , 3 , 4 , cells +
  6 points classify 3 .
;
```
This code defines the following words:

cmp: a compare function that takes two data point distance pairs and returns -1 if the distance of the first pair is less than the distance of the second pair, 1 if the distance of the first pair is greater than the distance of the second pair, and 0 if the distances are equal. This function is used by the qsort function to sort the pairs by ascending distance.

classify: a word that takes a list of data points

## --

