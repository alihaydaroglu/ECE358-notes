**ECE356**  
**Problem Set 1**  
**Ali Haydaroglu - 1002191415**

### Q1.

#### \(i\)

Using KCL on the top node \(and using the fact that $$v_C = v$$\), we get:


$$
\begin{align}
\dot {v_C} & = \frac 1C (i + i_L) \\
& = \frac 1C (i_L + h(v_C)) \\
& = \frac 1C (i_L + \frac 13 v_C^3 - v_C) \tag{1.1}
\end{align}
$$


Apply KVL on the left nodes to get:


$$
v_C = L \dot {i_L} + u \tag{1.2a}
$$


Alternatively,


$$
\dot i_L = \frac{1}{L} v_C - \frac{u}{L} \tag{1.2b}
$$


Equations $$(1.1)$$ and $$(1.2b)$$ can be used to mathematically model the system.

#### \(ii\)

We want to express the system in the form:


$$
\begin{bmatrix} \dot{v_C} \\ \dot{i_L} \end{bmatrix} = \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix} \begin{bmatrix} v_C \\ i_L     \end{bmatrix} + \mathbf{B}u(t) \tag{1.3}
$$


Using equations $$(1.1)$$ and $$(1.2b)$$, we get:


$$
\begin{bmatrix}
    \dot{v_C} \\ \dot{i_L}
\end{bmatrix} =
\begin{bmatrix}
    - \frac 1C & - \frac 1C \\
    \frac 1L & 0
\end{bmatrix}
\begin{bmatrix}
    v_C \\ i_L
\end{bmatrix} +
\begin{bmatrix}
    \frac 13 v_C^3 \\ -\frac uL
\end{bmatrix} \tag{1.4}
$$


### Q2.

For $$M_1$$, the forces applied on the object are:

* Spring force of $$k_1$$ - depends on $$X_1$$ only
* Spring force of $$k_2$$ - depends on both $$X_1, X_2$$
* Damping force from $$b$$ - depends on the speed of both objects
* Applied force from $$u$$

So, for the first object, the force balance gives:


$$
M_1 \ddot{X_1} = -k_1X_1-k_2(X_1-X_2)-b(\dot{X_1}-\dot{X_2}) + u \tag{2.1a}
$$


The second object, similarly:


$$
M_2 \ddot {X_2} = -k_3X_1+k_2(X_1-X_2)+b(\dot{X_1}-\dot{X_2}) \tag{2.1b}
$$


The two equations above describe the motion of the given system.

### Q3.

#### \(i\)

To find the equilibrium, first set $$\dot{x_1} = 0$$:


$$
0 = -x_1 + 1 \\
x_1 = 1 \tag{3.1a}
$$


Next, $$\dot {x_3} = 0$$:


$$
0 = e^{x_1}x_2+1 \\
e*x_2 = -1 \\
x_2 = -\frac 1e \tag{3.1c}
$$


Finally, set $$\dot{x_2} = 0$$:


$$
0 = -2x_2 + x_3 \\
x_3 = 2x_2 \\
x_3 = - \frac 2e \tag{3.1b}
$$


So, combine $$(3.1a,b,c)$$. Let $$\mathbf{x^\ast}$$ be the equilibrium point:


$$
\mathbf{x^\ast} = \begin{bmatrix} x_1^\ast \\ x_2^\ast \\ x_3^\ast \end{bmatrix} = \begin{bmatrix} 1 \\ -\frac 1e \\ - \frac 2e \end{bmatrix} \tag{3.2a}
$$


Also,


$$
y^\ast = 1 - \frac 1e \tag{3.2b}
$$


#### \(ii\)

Define $$f_1, f_2,f_3$$ as the following:


$$
\begin{align}
f_1(x_1,x_2, x_3,u) & = -x_1 + u \\
f_2(x_1,x_2, x_3,u) & = -2x_2 + x_3 \\
f_3(x_1,x_2, x_3,u) & = e^{x_1}x_2+u \tag{3.3}
\end{align}
$$


Also, define a change of variables:


$$
\begin {align}
\delta x_1  = x_1 - x_1^{\ast} &= x_1 - 1 \\
\delta x_2  = x_2 - x_2^{\ast} &=  x_2 + \frac 1e \\
\delta x_3  = x_3 - x_3^{\ast} &= x_3 + \frac 2e \\
\delta u = u - u^\ast &= u - 1 \\
\delta y= y - y^\ast &= y - 1 + \frac 1e
\end {align} \tag{3.4}
$$


Using the change of variables, take the Taylor Expansion of the function \(ignoring the higher order terms\) to obtain the following approximation:


$$
\newcommand{\pder}[2]{\frac{\partial#1}{\partial#2}}
\newcommand{\at}[2][]{#1|_{#2}}
\begin{align}
\begin {bmatrix}
\dot{\delta x_ 1} \\ \dot{\delta x_2} \\ \dot{\delta x_3}    
\end {bmatrix} =
\begin{bmatrix}
\pder {f_1}{x_1} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_1}{x_2} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_1}{x_3} \at {(\mathbf{x^\ast},u^\ast)} \\
\pder {f_2}{x_1} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_2}{x_2} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_2}{x_3} \at {(\mathbf{x^\ast},u^\ast)} \\
\pder {f_3}{x_1} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_3}{x_2} \at {(\mathbf{x^\ast},u^\ast)} &
\pder {f_3}{x_3} \at {(\mathbf{x^\ast},u^\ast)} \\
\end {bmatrix}
\begin{bmatrix}
\delta x_1 \\ \delta x_2 \\ \delta x_3
\end{bmatrix}
+
\begin{bmatrix}
\pder{f_1}{u} \at {(\mathbf{x^\ast},u^\ast)} \\
\pder{f_2}{u} \at {(\mathbf{x^\ast},u^\ast)} \\
\pder{f_3}{u} \at {(\mathbf{x^\ast},u^\ast)} \\
\end{bmatrix}
\delta u
\end{align} \tag {3.5}
$$


Populate the Jacobian:


$$
\begin{align}
\begin {bmatrix}
\dot{\delta x_ 1} \\ \dot{\delta x_2} \\ \dot{\delta x_3}    
\end {bmatrix}
& =
\begin {bmatrix}
-1 & 0 & 0 \\
0 & -2 & 1 \\
x_2^\ast e^{x_1^{\ast}} & e^{x_1^\ast} & 0
\end{bmatrix}
\begin{bmatrix}
\delta x_1 \\ \delta x_2 \\ \delta x_3
\end{bmatrix}
+
\begin{bmatrix}
1 \\ 0 \\ 1
\end{bmatrix}
\delta u
\\
\\
& =
\begin {bmatrix}
-1 & 0 & 0 \\
0 & -2 & 1 \\
-1 & e & 0
\end{bmatrix}
\begin{bmatrix}
\delta x_1 \\ \delta x_2 \\ \delta x_3
\end{bmatrix}
+
\begin{bmatrix}
1 \\ 0 \\ 1
\end{bmatrix}
\delta u
\end{align} \tag{3.6a}
$$


And finally,


$$
\delta y = \delta x_1 + \delta x_2 \tag{3.6b}
$$


Equations $$(3.6a)$$ and $$(3.6b)$$ present a linearized model of the given system.

### Q4.

#### \(i\)

Since this is a homogenous system, only the homogenous solution is considered. First, find the eigenvalues of the given matrix $$\mathbf A$$.


$$
\mathbf A = \begin{bmatrix} 4 & 2 \\ 3 & -1 \end {bmatrix}
$$


$$  \  
\begin{align}  
0 &= \Bbb{det}\(s\mathbf I - \mathbf A\)   \  
& = \Bbb{det}\begin{bmatrix} s - 4 & -2  -3 & s+1 \end{bmatrix} \  
& = s^2 -4s +s -4 -6  & = s^2 -3s -10 \  
& = \(s+2\)\(s-5\)  
\end{align} \tag{4.1}


$$
Therefore, the eigenvalues are $$\lambda_1 =-2,\lambda_2=5$$. Solve for the eigenvectors $$v_1, v_2$$ using $$(4.2)$$:
$$


\begin{align}  
\(\lambda\_i \mathbf I - \mathbf A\)v\_i & = 0 \  
\end{align} \tag {4.2}


$$
This gives:
$$


v\_1 = \begin{bmatrix} 1  -3 \end{bmatrix},  
v\_2 = \begin{bmatrix} 2  1\end{bmatrix}  
\tag{4.3}


$$
The eigenvalue method allows us to express the solution with the fundamental matrix, $$\mathbf \Phi$$, and a 2x1 column vector of arbitrary constants, $$\mathbf c$$.
$$


x\(t\) = \mathbf \Phi \(t\) \mathbf c =  
\begin {bmatrix}  
    e^{-2t} & 2e^{5t} \  
    -3e^{-2t} & e^{5t}  
\end {bmatrix}  
\mathbf c \tag {4.4}


$$
####(ii)
Plugging in the initial condition, we can find $$\mathbf c$$.
$$


x\(0\) = \begin {bmatrix} 1  1 \end {bmatrix}  
= \begin {bmatrix} 1 & 2  -3 & 1 \end {bmatrix}  
\begin {bmatrix} c\_1  c\_2 \end {bmatrix}  
\tag{4.5}


$$
Solving for $$\mathbf c$$ gives:
$$


x\(t\) = \mathbf \Phi \(t\) \mathbf c =  
\begin {bmatrix}  
    e^{-2t} & 2e^{5t} \  
    -3e^{-2t} & e^{5t}  
\end {bmatrix}  
\begin {bmatrix}  
    -\frac 1 7 \  
    \frac 4 7  
\end {bmatrix}  
\tag {4.6}


$$
The solution which satisfies the initial condition is given in $$(4.6)$$.

###Q5.
####(i)
The eigenvalues and corresponding eigenvectors of the matrix, using the same method shown in $$(4.1,4.2)$$, are $$\lambda_1 = 5, v_1 = [7 \quad 1]^T$$, and $$\lambda_2 = -1, v_2 = [1 \quad 1]^T$$.

The fundamental matrix can be written down easily with this information:
$$


\mathbf \Phi\(t\) =  
\begin{bmatrix}  
    7e^{5t} & e^{-t}  
    \  
    e^{5t} & e^{-t}  
\end{bmatrix} \tag{5.1}


$$
####(ii)
Variation of parameters states that the particular solution will be equal to:
$$


\begin {align}  
x\_p\(t\) & =  \mathbf \Phi \(t\) \int\_0^t \mathbf \Phi ^{-1} \(t\) \mathbf B u\(s\)ds  \  
& =  
    \begin{bmatrix}  
        7e^{5t} & e^{-t}  
        \  
        e^{5t} & e^{-t}  
    \end{bmatrix}  
    \int\_0^t  
    \left\(  
    \frac {1}{\(7-1\)e^{4s}}  
    \begin{bmatrix}  
        e^{-s} & -e^{-s}  
        \  
        -e^{5s} & 7e^{5s}  
    \end{bmatrix}  
    \right\)  
    \begin{bmatrix}  
        0  1  
    \end{bmatrix}  
    ds  
 \  
& =  
    \frac 16  
    \begin{bmatrix}  
        7e^{5t} & e^{-t} \  
        e^{5t} & e^{-t}  
    \end{bmatrix}  
    \int\_0^t  
    \begin{bmatrix}  
        -e^{-5s}  7e^s  
    \end{bmatrix} ds  \  
& =  
    \frac 16  
    \begin{bmatrix}  
        7e^{5t} & e^{-t} \  
        e^{5t} & e^{-t}  
    \end{bmatrix}  
    \begin{bmatrix}  
        \frac 15 e^{-5t} - 1  7e^t - 1  
    \end{bmatrix}  \  
& =  
    \frac 16  
    \begin{bmatrix}  
        \frac 75 - 7e^{5t} + 7 -e^{-t} \  
        \frac 15 - e^{5t} + 7 - e^{-t}  
    \end{bmatrix}  \  
& =  
    \begin{bmatrix}  
        \frac {7}{5} - \frac{7e^{5t}}{6}-\frac{e^{-t}}{6} \  
        \frac {6}{5} - \frac{e^{5t}}{6} - \frac{e^{-t}}{6}  
    \end{bmatrix}  
\end{align} \tag{5.2}


$$
####(iii)
First, let us write down the full solution combining $$(5.1)$$ and $$(5.2)$$, where $$\mathbf c$$ is a column matrix of arbitrary constants.
$$


\begin{align}  
x\(t\) &= x\_h\(t\)+x\_p\(t\)  \  
& = \mathbf \Phi \(t\) \mathbf c + x\_p\(t\)  \  
& =  
\begin{bmatrix}  
    7e^{5t} & e^{-t}  
    \  
    e^{5t} & e^{-t}  
\end{bmatrix}  
\begin{bmatrix}  
    c\_1  c\_2  
\end{bmatrix} +  
\frac 15  
\begin{bmatrix}  
    7  6  
\end{bmatrix} -  
\frac 16  
\begin{bmatrix}  
    7  1  
\end{bmatrix}e^{5t} -  
\frac 16  
\begin {bmatrix}  
    1  1  
\end{bmatrix}  
 e^{-t}  
\end{align} \tag{5.3}


$$
Now, plug in the initial condition for $$t=0$$:
$$


\begin{align}  
\begin {bmatrix}  
    2  1  
\end{bmatrix}  
& =  
\begin {bmatrix} 7 & 1  1 & 1 \end{bmatrix}  
\begin {bmatrix} c\_1  c\_2 \end{bmatrix} +  
\begin {bmatrix} \frac 75 - \frac 76 - \frac 16  \frac 65 - \frac 16 - \frac 16 \end{bmatrix}  
\end{align} \tag{5.4}


$$
Expanding $$(5.4)$$ gives the following equations:
$$


2 = 7c\_1 + c\_2 + \frac 1{15} \  
1 = c\_1 + c\_2 + \frac {10}{15} \tag{5.5}


$$
Solving these gives $$c_1 = \frac{4}{15}$$, and $$c_2 = \frac{1}{15}$$. Therefore, the full solution is:
$$


\begin{align}  
x\(t\) &=  
\begin{bmatrix}  
    7e^{5t} & e^{-t}  
    \  
    e^{5t} & e^{-t}  
\end{bmatrix}  
\begin{bmatrix}  
    \frac {4}{15} \frac{1}{15}  
\end{bmatrix} +  
\frac 15  
\begin{bmatrix}  
    7  6  
\end{bmatrix} -  
\frac 16  
\begin{bmatrix}  
    7  1  
\end{bmatrix}e^{5t} -  
\frac 16  
\begin {bmatrix}  
    1  1  
\end{bmatrix}  
 e^{-t}  
\end{align} \tag{5.3}

$$

