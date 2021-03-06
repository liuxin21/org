# Outline
- Python 的 lists 和 functions
- 基本的 Numpy array 操作
- 用 matplotlib 画图
- calling Fortran/C from Python
- Benchmarking Python performance

# Fluid dynamics
**Discretisation** 是最重要的一个过程。
因为我们考虑 steady state, 所以先不考虑时间上的 discretisation 方法。
在空间上，有许多 discretisation 方法，例如 FDM, FVM, FEM。
在这个练习中，我们采用 finite difference method (FDM) 用来计算 
flow pattern of a fluid in a cavity 的问题。

## 问题
为了简便，我们假设流体的 viscosity (黏度$\mu$)为 0 。
也就是说，没有 vortices (or whirpools 漩涡)。

cavity 如下图所示，上面是 inlet, 右面是 outlet。

![](http://wx2.sinaimg.cn/mw690/8db2c8cbgy1flkfcpfv0uj20xk0fwaai.jpg)

## 列方程
当 viscosity 为 0 时，stream function $\Psi$ 满足
拉普拉斯方程（poisson 右侧不为零）： 

$$
\nabla^2 \Psi = \frac{\partial^2 \Psi}{\partial x^2} +
 \frac{\partial^2 \Psi}{\partial y^2} = 0 
$$

把上式写为 finite difference 的形式：

$$
\Psi_{i-1,j} + \Psi_{i+1,j} + \Psi_{i,j-1} + \Psi_{i,j+1} - 4\Psi_{i,j} = 0
$$

如果边界确定的话，那么除边界外的每个点，都可以通过周围四个点的平均值而计算出来。
这个过程（求周围四个点的平均值）会一直持续，直到结果 converges, 保持一个稳定值。
这个解 PDE (Laplas) 的方法就叫做 Jacobi Algorithm.

$$
u_x = \frac{\partial \Psi}{\partial y} = \frac12 
(\Psi_{i,j+1} - \Psi_{i,j-1}) , \ \ \ 
u_y = \frac{\partial \Psi}{\partial x} = \frac12 
(\Psi_{i+1,j} - \Psi_{i-1,j}),
$$

## 算法 outline

    列出 stream function 的 bc (边界条件)

    while (convergence 收敛 = FALSE) do
        for 每一个除边界外的点 do
            取周围四个相邻点的平均值来 update stream function 的值
        end do
        检查 convergence
    end do

    for 每一个除边界外的点 do 
        计算 $u_x$
        计算 $u_y$
    end do

## Python

- How the external "jacobi" function is included
- How the lists are declared and initialised to zero
- How the timing works 

cfd-python 文件下有三个文件夹：
- doc : Contains this exercise document
- code：
    - python: Contains the basic Python version of the source code (**cfd.py, jacobi.py**) , plotting utilities (**util.py, [plot_flow.py]()**) and source code for the extra exercises
    - verify: Contains output files to verify your results against 
- solutions: Contains subdirectories of various solution programs
**[numpy_loops, numpy_index, scipy, fortran, c_f2py]()**


## 运行和验证
cd到 python 文件夹，运行 cfd.py:

`87$ python cfd.py 1 1000`

cfd.py 1 1000
注意后面的 “1 1000”，意思是 scalefactor of 1 and 1000 Jacobi_iteration steps. 

- **scalefactor** 决定了 the size of the simulation (1 相当于 32x32 gris, 2 相当于 64x64 gris, 以此类推)。

- **interation steps** 是指在 Jacobi algorithm 中迭代的次数。(对于比较大的 girds, 你需要更多的 interation steps 来 converge)。

运行的结果如下：

    2D CFD Simulation
    =================
    Scale factor = 1
    Iterations   = 1000

    Grid size = 32 x 32

    Starting main Jacobi loop ...

    completed iteration 1000

    ... finished

    Calculation took 0.81351s

这个 program 同时生成了一个叫 velocity.dat 的文件，里面包含了每一个 grid point 的速度。

另外一个文件夹 verify 里有正确答案 cfd_velocity_1_1000.dat ， 可以利用下面的代码来验证你的结果：

`$ diff velocity.dat ../verify/cfd_velocity_1_1000.dat`


## numpy

把文件中的 psi 和 tmp 两个 list 改成 numpy arrays.

先
`psi = [[0 for col in range(n+2)] for row in range(m+2)]`

可改为：

`psi = np.zeros((m+2, n+2))`