# Lecture 3

[Slides](C:\Users\Ali\Google Drive\Engineering Science\1T8 W\ECE358\Slides\Lec01-2.pdf)

Review of the **Master Theorem**. Need to practice this!

## Exceptions to the Master Theorem

$$
T(n) = 2T(\frac{n}{2})+n\log(n)
$$

So, $$a=2$$, $$b=2$$, and $$f(n)=n\log(n)$$. So, compare $$f(n)$$ with $$n^{\log_{2}(2)}=n$$. Now, $$f(n)$$ is larger than the calculated function, which is $$n$$. However, there is no $$\epsilon$$ such that $$n\log(n)=\Omega(n^{1+\epsilon})$$. So it's neither Case 1 or Case 2!

In the master theorem, you need $$f(n)$$ to be larger than $$n^{\log_{b}(a)}$$ not asymptotically, but polynomially, so you need to find an $$\epsilon$$ that satisfies the equation in the theorem. Some cases fall between Case 1 and 2, some fall between Case 2 and 3, and cannot be solved with this theorem


## Multiplication of Large Integers

**Input**: two numbers in binary each has n bits. 

| $$x$$  | $$X_1$$ | $$X_0$$ |
| ---- | ----- | ----- |
| $$y$$  | $$Y_1$$ | $$Y_0$$ |

Define $$X_1 = x_{n-1}...x_{\frac{n}{2}}$$ and $$X_0=x_{(\frac{n}{2}-1)}...x_1x_0$$, and define similarly for $$Y_0$$ and $$Y_1$$.

So, $$xy=2^nX_1Y_1 + 2^{\frac{n}{2}}X_1Y_0+2^{\frac{n}{2}}X_0Y_1+X_0Y_0$$

So,

```python
def multiply (x,y): # arrays of size n
	if n = 1:
		return x*y
	else:
		# set arrays X_1, X_0, Y_1, Y_0
		p1 = multiply(X1, X0)
		p2 = multiply(X1, Y0)
		p3 = multiply(X0, Y1)
		p4 = Multiply(X0, Y0)
		
		return 2^n * p1 + 2^(n/2) * p2 + 2^(n/2) * p3 + p4
```

 So, apply master theorem to it:
$$
T(n) = 4T(\frac{n}{2})+\Theta(n)
$$
So, we have $$T(n) = O(n^2)$$.

### A Better Approach to Multiplication

$$
xy=2^nX_1Y_1+X_0Y_0+2^{\frac{n}{2}}((X_1+X_0)(Y_1+Y_0)-X_1Y_1-X_0Y_0)
$$

This way we can reduce the number of sub-problems. Now we have three subproblems, with size $$n/2+1$$

```python
def multiply2 (x,y):
	p1 = multiply(x1,y1)
    p2 = multiply(x1+x0,y1+y0)
    p3 = multiply(x0,y0)
    return 2^n ....
```

$$T(n) = 3T(n/2)+\Theta(n)$$ and with master theorem we get $$T(n)=\Theta(n^{\log_2(3)})=\Theta(n^{1.58})$$.

## Maximum Subarray Problem

**Input**: an array ```A[1...n]``` 

**Output**: indices i and j such that A[i...j] has the highest possible sum

You can solve this with divide and conquer:

1. Divide array into ```A[low...mid]``` and ```A[mid+1...high]```
2. Solve for two subarrays
3. Find maximum subarray  that crosses the midpoint 
4. Use the best solution of the three

Check 