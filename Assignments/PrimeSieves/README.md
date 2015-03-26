## Week 2: Prime number sieves

### Goals

* learn how to write/read output to/from a file
* learn some basics about lists
* learn to use modules
* learn to measure algorithm performance

### Read

* [Think Python](http://www.greenteapress.com/thinkpython/) ch. 10, 14
* [Sieve of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

### Assignment

**Prime Sieves**

Implement the Sieve of Eratostheses, an algorithms for finding all the prime numbers smaller than $N$. The code should compute all the Prime numbers $< N$, write them to a file and print some statistics (time required and the number of Primes found) on the screen

	$ pyhton3 Sieve_of_E.py 10000 prime.dat
	Found 9592 Prime numbers smaller than 10000 in 0.03620992274954915 sec.
	--------------------------------------------		

The file `prime.dat` should be formatted as

	2
	3
	5
	7
	
You can read input from the command line as follows

	import sys
	
	# sys.argv is a list with the command-line arguments. sysv.arg[0] is the name of Python script
	
	print('Number of arguments:', len(sys.argv), 'arguments.')
	print('Argument List:', str(sys.argv))	
	
Use a `list` to store all numbers from $1$ to $N$ and set all non-primes to zero. To do this, you will need a double loop.

To compute the time required for a piece of code use `time.perf_counter()` from the `time` module:

	import time
	
	T1 = time.perf_counter()
	
	# some code
	
	T2 = time.perf_counter()
	print('Time required', T2 - T1, 'sec.')


**Algorithm performance**

Algorithm performance (or complexity) is typically measured in terms of the size of the input ($N$ in this case). If we say that the runtime is $\mathcal{O}(N)$, we mean that it grows linearly with $N$. The constants matter in practice, but are typically ignored when presenting such an analysis. We would usually prefer an algorithm that has runtime $\mathcal{O}(N)$ to one that has runtime $\mathcal{O}(N^2)$, even though the latter *may* be faster for a specific (small) value of $N$.

We can analyse the complexity by counting operations. The loop 

	for i in range(1,N) :
		y[i] = 2*x[i]

has a complexity of $\mathcal{O}(N)$, for example. The double loop

		for i in range(1,N) :
			for j in range(1,N) : 
				y[i] = 2*x[j]

has a complexity of $\mathcal{O}(N^2)$. It's get more interesting when the limits of the inner loop depend on $i$.
			
Study empirically how the runtime of the algorithms increases with $N$ by making a table of the runtime for various $N$. Does this match your expectation based on the complexity analysis?

We can improve upon the algorithm by realizing that we only need to start the inner loop from $i^2$ and can this terminate the outer loop at $\sqrt{n}$. Create an improved version of the Sieve (preferably in a new branch, so you can always revert back to the original algorithm). 

How does the runtime increase with $N$ now? A further improvement can be made by listing only odd numbers and count in increments of $2i$ in the inner loop. How does this affect the behaviour of the run time with $N$?

**Bonus: Processing the output**

Write a separate program `CountPrimes` that reads in the file and prints the number of Primes $\pi(N)$ and the number of [twin primes](http://en.wikipedia.org/wiki/Twin_prime) $\pi_2(N)$. Use these to check the [Prime Number Theorem](http://en.wikipedia.org/wiki/Prime_number_theorem), which says that for large $N$

$$\frac{\pi(N)\log(N)}{N} \approx 1,$$

and the [First Hardy–Littlewood conjecture](http://en.wikipedia.org/wiki/Twin_prime) which states that

$$\frac{\pi_2(N)(\log(N))^2}{2C_2N} \approx 1,$$

where $C_2 = 0.6601618\ldots$.

Use the `math` module to evaluate the logarithm

	import math
	y = 10
	x = math.log(y)
	
The output should look like this:

	$ python3.4 CountPrimes.py prime.dat
	Largest Prime =  9999991
	--------------------------------
	pi(N)         =  664579
	N/log(N)      =  620420.1646975484
	ratio         =  1.0711756932078098
	--------------------------------
	pi_2(N)       =  58980
	2CN/log(N)^2  =  50822.09880482194
	ratio         =  1.1605187779927746

**Bonus: Sieve of Sundaram**

A less well-known algorithm for find all primes is the [Sieve of Sundaram](http://en.wikipedia.org/wiki/Sieve_of_Sundaram). Implement this sieve in a similar manner as the previous one. Check that the output of both algorithms is identical. Which algorithm is more efficient?
	
