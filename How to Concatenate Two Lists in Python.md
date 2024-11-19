# Introduction

Concatenating lists can be quite useful for example if the two separate lists being concatenated had to pass through a function first. There are many ways of concatenating lists in python. We shall look at concatenating using the plus operator, multiply operator, a for loop, the method itertools.chain() and the inbuilt function extend. We will make use of the following lists:


```python
list_a = [1, 2, 3, 4]
list_b = [5, 6, 7, 8]
```

# Using plus operator

Python, like many other languages, uses the plus (+) operator to append or merge strings. It is the first method we will introduce here as it is quite straightforward. Look at the following example to see how it is done.


```python
list_c  = list_a + list_b
print (list_c)
```

    [1, 2, 3, 4, 5, 6, 7, 8]


# Using multiply operator

This method allows you to join multiple lists. It is actually new and only available from Python 3.6+. You put the operator before the list name followed by a comma. The other lists follow suit in the same way enclosed by square brackets.


```python
list_c  = [*list_a, *list_b, *list_a]
print (list_c)
```

    [1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 4]


# Using the for loop

In this method you will go through one list while appending each of its elements to the second list one by one. When the loop is over you will have one list with all desired elements.


```python
for i in list_b:
    list_a.append(i)
print (list_a)
```

    [1, 2, 3, 4, 5, 6, 7, 8]


# Using itertools.chain()

This method works with iterables. It chains all lists entered as arguments into one list. It does not need to store the concatenated list hence useful when the list is only needed once. You will need to import itertools.


```python
import itertools

list_c  = list(itertools.chain(list_a, list_b))
print (list_c)
```

    [1, 2, 3, 4, 5, 6, 7, 8]


# Using extend

It is an inbuilt function that can be used to expand a list. Here we are expanding the first list by adding elements of the second list to it.


```python
list_a.extend(list_b)

print (list_a)
```

    [1, 2, 3, 4, 5, 6, 7, 8]


# Conclusion

We have learnt five ways of concatenating two lists. You can decide to use whichever depending on your needs. While picking which one fits your use case, you may wanna check properties like memory usage and speed.
