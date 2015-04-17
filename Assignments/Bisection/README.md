## Bisection

### Goals

* learn about recursion
* learn more about functions and modules

### Read

* [Think Python](http://www.greenteapress.com/thinkpython/) ch. 5, 7
* [The bisection method](http://en.wikipedia.org/wiki/Bisection_method)


### Assignment

We can solve a non-linear equation $f(x) = 0$, where $f:\mathbb{R}\rightarrow \mathbb{R}$ is a continuous function, using the *bisection* method. The basic idea is as follows. First, find an interval $[x_0,x_0+h]$ that contains a solution. Using the [intermediate value theorem](http://en.wikipedia.org/wiki/Intermediate_value_theorem), we can verify that the interval indeed contains a solution when $f(x_0) < 0$ and $f(x_0+h) > 0$ (or vice-versa). If this condition fails, we increase $h$. Having found an interval that contains the root, we halve the interval and check if the solution lies in the left $[x_0,x_0+h/2]$ or right $[x_0+h/2,x_0+h]$ half of the interval. If, for example, the solution lies in the left interval, we let $x_1 = x_0$ and $h = h/2$ and repeat. The algorithm terminates when $h\leq \epsilon$, where $\epsilon$ is a give tolerance.

The algorithm is of a *recursive* nature; finding a solution in the interval $[x_i,x_i+h]$ is done by finding a solution in the left or right half of the interval, which is done by finding a root in the left or right half of *that* interval, etc. 

Write a function `findroot(x_0,h,epsilon)` that determines in which half of the interval the solution lies and calls `findroot(x_0,h/2,epsilon)` or `findroot(x_0+h/2,x_0+h,epsilon)` accordingly. If `h<=epsilon` the function should return `x_0`. Save the function in a file called `bisection.py`.

We'd like to define the function $f(x)$ *dynamically* so we can use the same code for different functions. We can achieve this in Python as follows. First, make a new file `f1.py` with a function `value(x)` that evaluates the function $f$. For $f(x) = x(x-1)-1$, for example, we have

	def value(x)
		return x*(x - 1) - 1
		
We'd like to call our main file as

	$ python3 bisect.py f1 0 2 1e-6
	found root x = 1.618034
	
to indicate we want find a solution of the function defined in `f1.py` in the interval $[0,2]$ with an accuracy of $10^{-6}$. In the main file, you can import a variable module as follows

	import importlib
	
	# import module as `function`
	function = importlib.import_module(sys.argv[1])

	# we can now evaluate the function as follows
	x = 1
	y = function.value(x) 
	
Include input-checking and automatically increasing $h$ when the initial interval does not contain a solution (be ware, the interval might not contain a solution no matter how big the interval gets). Test your code on the following functions

$$f_1 = x(x-1)-1,$$
$$f_2 = x^2,$$
$$f_3 = \cos(x).$$

Does it always work? 

**Bonus: finding more than one root**

Think how you would extend your code to find more than one root.

aaaa