## Week 3: Estimating $\pi$

### Goals

* learn how to write functions
* learn some basics about random number generators
* learn about reproducibility

### Read

* [Think Python](http://www.greenteapress.com/thinkpython/) ch. 3,6
* [Buffon's Needle](http://en.wikipedia.org/wiki/Buffon%27s_needle)

### Assignment

The value of $\pi$ can be approximated experimentally by throwing needles of length $l$ on
a board with parallel lines with distance $1$. If $l\leq 1$, the probability that the needle crosses a line is $2l/\pi$. 

We can simulate the experiment numerically by drawing a random pair $x_0,y_0\in [0,1]$ uniformly, a random angle $\theta \in [0,2\pi]$. The two end-points of the needle are $(x_0,y_0)$ and $(x_0 + l \cos(\theta), y_0 + l \sin(\theta))$. If endpoint crosses the line, we call it a *hit*. 

Write a function `drop_needle(L)` that drops a needle of length `L` and returns `True` if it is a hit and `False` if not. You can generate random numbers as follows

	import random
	
	# uniform in [0,1]
	x = random.random()
	
	# uniform in [0,2\pi]
	a = random.vonmisesvariate(0,0)

Write a code that, for given length `L`, repeats this experiment `N` times and counts the number of hits, and subsequently estimates $\pi$. Check wether the input is valid (i.e., `L<=1`). If insufficient input arguments are given, the code should print some useful info.

	$ python3.4 estimate_pi.py 
	Use: pyhton estimte_pi.py N L
	
	$ python3.4 estimate_pi.py 355
	Use: pyhton estimte_pi.py N L
	
	$ python3.4 estimate_pi.py 355 2
	AssertionError: L should be smaller than 1
	
	$python3.4 estimate_pi.py 355 1
	Buffon's Needles:
		226 hits in 355 tries
		Estimate of Pi = 710/226 = 3.141593

Wow, that is a remarkably good approximation! Can you get the same result? After a number tries, perhaps you can. However, the result is not really *reproducible*. Although it seems like a contradiction, it is possible to reproduce a (computational) experiment that involves random numbers. To see how we first need to understand how the computer generates random numbers. The basic method for generating a sequence of seemingly random numbers, we start from an $x_0$ and define subsequent numbers as

$$x_{i+1} = (a x_i + c) \mod m.$$

For some choices of $a,c$ and $m$ this leads to a sequence of numbers that are almost uniformly distributed, although the sequence will repeat itself after a number of iterations. By setting the *seed*, $x_0$, manually, we can reproduce the same sequence of numbers. In python, we can set the seed using `random.seed(seed)`. If you do not set the seed manually, Python uses the system time to generate a seed.

Include the possibility of passing a parameter `seed` on the command line. If this parameter is not given, the code should not set the seed. 

**Bonus: long needles**
For long needles $l>1$, the probability of a hit is

$$P = \frac{2l}{\pi} - \frac{2}{\pi}\left(\sqrt{l^2 - 1} + \frac{1}{\sin(l^{-1})} \right) + 1.$$

Make a new version of your code (in a new branch) that works for $l>1$ as well.


