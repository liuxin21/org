Note that the index 
i
i here is zero-based, in other words 
i
=
0
,
1
,
…
,
N
−
1
{\displaystyle i=0,1,\dots ,N-1} where 
N
N is the number of unknowns.

    try:
    import numpypy as np    # for compatibility with numpy in pypy
    except:
    import numpy as np      # if using numpy in cpython

    def TDMASolve(a, b, c, d):
        n = len(a)
        ac, bc, cc, dc = map(np.array, (a, b, c, d))
        xc = []
        for j in range(2, n):
            if(bc[j - 1] == 0):
                ier = 1
                return
            ac[j] = ac[j]/bc[j-1]
            bc[j] = bc[j] - ac[j]*cc[j-1]
        if(b[n-1] == 0):
            ier = 1
            return
        for j in range(2, n):
            dc[j] = dc[j] - ac[j]*dc[j-1]
        dc[n-1] = dc[n-1]/bc[n-1]
        for j in range(n-2, -1, -1):
            dc[j] = (dc[j] - cc[j]*dc[j+1])/bc[j]
        return dc

## Another way

    def TDMA(a,b,c,f):
        a, b, c, f = map(lambda k_list: map(float, k_list), (a, b, c, f))

        alpha = [0]
        beta = [0]
        n = len(f)
        x = [0] * n

        for i in range(n-1):
            alpha.append(-b[i]/(a[i]*alpha[i] + c[i]))
            beta.append((f[i] - a[i]*beta[i])/(a[i]*alpha[i] + c[i]))
                
        x[n-1] = (f[n-1] - a[n-2]*beta[n-1])/(c[n-1] + a[n-2]*alpha[n-1])

        for i in reversed(range(n-1)):
            x[i] = alpha[i+1]*x[i+1] + beta[i+1]
        
        return x

    # small test. x = (1,2,3)
    if __name__ == '__main__':
        a = [3,3]
        b = [2,1]
        c = [6,5,8]
        f = [10,16,30]
        print(TDMA(a,b,c,f))

## github 方法

    import numpy as np

    ## Tri Diagonal Matrix Algorithm(a.k.a Thomas algorithm) solver
    def TDMAsolver(a, b, c, d):
        '''
        TDMA solver, a b c d can be NumPy array type or Python list type.
        refer to http://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm
        and to http://www.cfd-online.com/Wiki/Tridiagonal_matrix_algorithm_-_TDMA_(Thomas_algorithm)
        '''
        nf = len(d) # number of equations
        ac, bc, cc, dc = map(np.array, (a, b, c, d)) # copy arrays
        for it in xrange(1, nf):
            mc = ac[it-1]/bc[it-1]
            bc[it] = bc[it] - mc*cc[it-1] 
            dc[it] = dc[it] - mc*dc[it-1]
                    
        xc = bc
        xc[-1] = dc[-1]/bc[-1]

        for il in xrange(nf-2, -1, -1):
            xc[il] = (dc[il]-cc[il]*xc[il+1])/bc[il]

        return xc

## Example:

    A = np.array([[10,2,0,0],[3,10,4,0],[0,1,7,5],[0,0,3,4]],dtype=float)   

    a = np.array([3.,1,3]) 
    b = np.array([10.,10.,7.,4.])
    c = np.array([2.,4.,5.])
    d = np.array([3,4,5,6.])

    print TDMAsolver(a, b, c, d)
    >> [ 0.14877589  0.75612053 -1.00188324  2.25141243]
    #compare against numpy linear algebra library
    print np.linalg.solve(A, d)
    >> [ 0.14877589  0.75612053 -1.00188324  2.25141243]