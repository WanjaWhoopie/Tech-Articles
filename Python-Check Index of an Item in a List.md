# Introduction

Lists are useful in different ways compared to other datatypes especially because of how versatile they are. We are going to learn how to get index of an item in a list in different contexts. We will use the following list in this tutorial. 



```python
myList = ['a', 'b', 'c', 'd', 'e', '1', '2', '3', 'b']
```

# Using the index() method

Let us checkout the index() method for this instance. The syntax of the index method is: **list_name.index(element, start, end)** 

**element**: this is the actual element in the list you are looking for
**start**: this is the position from which you want the search to begin
**end**: this is the position where the search ends

In the following example we are looking for element 2 between the 2nd and 8th position. Remember we start counting from zero.


```python
index = myList.index('2', 2, 8)
print ("The index is: ", index)
```

    The index is:  6


You do not have to use the start and end though. You could write it as: **list_name.index(element)** which will search through the whole list until it gets the first instance of the element you are looking for. Other elements after are ignored.


```python
index = myList.index('c')
print ("The index is: ", index)
```

    The index is:  2


There may be several occurrences of the element you are looking for and you may need to get the last position of the element. To get the last occurrence of the element you are looking for you may decide to first do *list_name.reverse()* then use the index method but this just gives the index of the element counting the last as first. Look at the following example that makes use of slicing.


```python
index= len(myList) - myList[::-1].index('b')-1
print("Last index of b is: ", index)
```

    Last index of b is:  8


You may also need to find all the positions of the element in the list at once. This example does not use the index method but uses range. 


```python
index= [ i for i in range(len(myList)) if myList[i] == 'b' ]

print('Indexes of all occurrences of "b" in the list are : ', index)
```

    Indexes of all occurrences of "b" in the list are :  [1, 8]


You can also use the enumerate method.


```python
index = [i for i,x in enumerate(myList) if x == 'b']
print('Indexes of all occurrences of "b" in the list are : ', index)
```

    Indexes of all occurrences of "b" in the list are :  [1, 8]


If the item you are looking for is not in the list you will get an error message and the program stops. To counter this we are going to throw an exception so it just prints the error message but does not give an error. This is especially useful when it is part of a bigger program.


```python
try:
    index = myList.index('z')
    print ("The index is: ", index)
except ValueError as err:
    print(err)
```

    'z' is not in list


# Conclusion

We have learnt how to use the index method to find the first and last occurrence of an element in a list. We have also learnt how to list all occurrences of the element and how to catch an error if element is not in the list. Happy coding! 
