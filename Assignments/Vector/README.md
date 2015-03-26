## Week 5: Object-oriented Programming I

### Goals

* learn about Object-oriented programming (classes, methods, objects, overloading)

### Read

* [Think Python](http://www.greenteapress.com/thinkpython/) ch. 15,16,17

### Assignment

Python does not have a natural way of representing vectors in $\mathbb{R}^n$. We can surely make an array (more efficient than using a list) of numbers

	>>> from array import array
	
	>>> u = array('d',[1,3,4])
	>>> v = array('d',[2,1,3])

where `d` indicates that it is an array of doubles. However, these vectors do not behave as we would expect (mathematically)

	>>> w = u+v
	>>> print(w)	
	array('d', [1.0, 3.0, 4.0, 2.0, 1.0, 3.0])

We could of course, add the two vectors as follows

	>>> w = array('d',[0,0,0]) 
	>>> for i in range(len(v)) : 
			w[i] = u[i] + v[i]
		
but this will not lead to very readable code.
To make our live a bit easier, we will make a class called `Vector` that represents a vector in $\mathbb{R}^n$. Start with writing the *constructor* (`__init__(self,n)`) that initializes the vector zeros. Then, write a method `__str__(self)`
that prints the elements of the vector on screen

	>>> from Vector import Vec
	>>> u = Vector(3)
	>>> print(u)
	0.000000
	0.000000
	0.000000

Next, we want to be able to get and set elements. Write methods `getElement(self,i)` and `setElement(self,i,a)` that return element `i` or assign `a` to element `i`

	>>> v.setElement(1,2)
	>>> v.getElement(1)
	2.0
	
Continue by writing the following methods to perform the usual operators on vectors $\mathbf{u},\mathbf{v}$ and scalars $\alpha,\beta$

| Method                     | Operation                              |
| ---------------------------| -------------------------------------- |
| `lincomb(self,other,a,b)`  | $\alpha \mathbf{u} + \beta\mathbf{v}$  |
| `scalar(self,a)`           | $\alpha\mathbf{u}$                     |
| `inner(self,other)`        | $\sum_{i=1}^{n} u_iv_i$	              |
| `norm(self)`               | $\sqrt{\sum_{i=1}^{n} u_i^2}$          |

Note that you can write `norm` in terms of `inner` and .
Finally, write methods `zero`, `one` and `random` to set all elements to zero, one or assign random values to the vector.

With these, we should be able to perform some basic operations

	>>> u = Vector(3)
	>>> v = Vector(3)
	
	>>> u.one()
	>>> v.random()
	
	>>> w = u.lincomb(v,10,1)
	>>> print(w)
	10.971972
	10.319745
	10.446400
	
	>>> w = w.scalar(2)
	21.943945
	20.639490
	20.892801
	
	>>> w.norm()
	36.661074678138924
	
	>>> w.inner(u)
	63.47623585462545
	

