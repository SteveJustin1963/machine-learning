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



