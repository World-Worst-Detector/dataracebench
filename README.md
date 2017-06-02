# DataRaceBench

DataRaceBench is a collection of files that can be used to test and evaluate race detection tools.


## Overview of benchmarks

Label | Meaning
---|---------------------------------
Y1 | Unresolvable dependences
Y2 | Missing data sharing clauses
Y3 | Missing synchronization
Y4 | SIMD data races
Y5 | Accelerator data races
Y6 | Undefined behaviors
Y7 | Numerical kernel data races
N1 | Embarrassingly parallel
N2 | Use of data sharing clauses
N3 | Use of synchronization
N4 | Use of SIMD directives
N5 | Use of accelerator directives
N6 | Use of special language features
N7 | Numerical kernels


## Mircobenchmarks with known data races (RACE-YES-SET)

P-Label| Micro-bechmark          | Source     | Description
-------|-------------------------|------------|----------------------------------------------------------------------------------------
Y1     | antidep1                | AutoPar    | Anti-dependence within a single loop
Y1     | antidep2                | AutoPar    | Anti-dependence within a two-level loop nest
Y7     | indirectaccess1         | LLNL App   | Indirect access with overlapped index array elements
Y7     | indirectaccess2         | LLNL App   | Overlapping index array elements when 36 or more threads are used
Y7     | indirectaccess3         | LLNL App   | Overlapping index array elements when 60 or more threads are used
Y7     | indirectaccess4         | LLNL App   | Overlapping index array elements when 180 or more threads are used
Y2     | lastprivatemissing      | AutoPar    | Data race due to a missing `lastprivate()` clause
Y3     | minusminus              | AutoPar    | Unprotected `--` operation
Y3     | nowait                  | AutoPar    | Missing barrier due to a wrongfully used nowait
Y6     | outofbounds             | AutoPar    | Out of bound access of the 2nd dimension of array
Y1     | outputdep               | AutoPar    | Output dependence and true dependence within a loop
Y1     | plusplus                | AutoPar    | `++` operation on array index variable
Y2     | privatemissing          | AutoPar    | Missing `private()` for a temp variable
Y2     | reductionmissing        | AutoPar    | Missing `reduction()` for a variable
Y3     | sections1               | New        | Unprotected data writes in parallel sections
Y1,Y4  | simdtruedep             | New        | SIMD instruction level data races
Y1,Y5  | targetparallelfor       | New        | Data races in loops offloaded to accelerators
Y3     | taskdependmissing       | New        | Unprotected data writes in two tasks
Y1     | truedep1                | AutoPar    | True data dependence among multiple array elements within a single level loop
Y1     | truedepfirstdimension   | AutoPar    | True data dependence of first dimension for a 2-D array accesses
Y1     | truedeplinear           | AutoPar    | Linear equation as array subscript
Y1     | truedepscalar           | AutoPar    | True data dependence due to scalar
Y1     | truedepseconddimension  | AutoPar    | True data dependence on 2nd dimension of a 2-D array accesses
Y1     | truedepsingleelement    | AutoPar    | True data dependence due to a single array element


## Microbenchmarks without known data races (RACE-NO-SET)

P-Label| Micro-bechmark          | Source     | Description
-------|-------------------------|------------|--------------------------------------------------------------------------------------
N2     | 3mm-parallel            | Polyhedral | 3-step matrix-matrix multiplication, non-optimized version
N2,N4  | 3mm-tile                | Polyhedral | 3-step matrix-matrix multiplication, with tiling and nested SIMD
N2     | adi-parallel            | Polyhedral | Alternating Direction Implicit solver, non-optimized version
N2,N4  | adi-tile                | Polyhedral | Alternating Direction Implicit solver, with tiling and nested SIMD
N1     | doall1                  | AutoPar    | Classic DOAll loop operating on a one dimensional array
N1     | doall2                  | AutoPar    | Classic DOAll loop operating on a two dimensional array
N1     | doallchar               | New        | Classic DOALL loop operating on a character array
N2     | firstprivate            | AutoPar    | Example use of firstprivate
N6     | functionparameter       | LLNL App   | Arrays passed as function parameters
N6     | fprintf                 | New        | Use of `fprintf()`
N2     | getthreadnum            | New        | single thread execution using `if (omp_get_thread_num()==0)`
N7     | indirectaccesssharebase | LLNL App   | Indirect array accesses using index arrays without overlapping
N1     | inneronly1              | AutoPar    | Two-level nested loops, inner level is parallelizable. True dependence on outer level
N1     | inneronly2              | AutoPar    | Two-level nested loops, inner level is parallelizable. Anti dependence on outer level
N7     | jacobi2d-parallel       | Polyhedral | Jacobi with array copying, no reduction, non-optimized version
N4,N7  | jacobi2d-tile           | Polyhedral | Jacobi with array copying, no reduction, with tiling and nested SIMD
N7     | jacobiinitialize        | AutoPar    | The array initialization parallel loop in Jacobi
N7     | jacobikernel            | AutoPar    | Parallel Jacobi stencil computation kernel with array copying and reduction
N2     | lastprivate             | AutoPar    | Example use of lastprivate
N7     | matrixmultiply          | AutoPar    | Classic i-k-j order matrix multiplication using OpenMP
N7     | matrixvector1           | AutoPar    | Matrix-vector multiplication parallelized at the outer level loop
N7     | matrixvector2           | AutoPar    | Matrix-vector multiplication parallelized at the inner level loop with reduction
N2     | outeronly1              | AutoPar    | Two-level nested loops, outer level is parallelizable. True dependence on inner level
N2     | outeronly2              | AutoPar    | Two-level nested loops, outer level is parallelizable. Anti dependence on inner level
N7     | pireduction             | AutoPar    | PI calculation using reduction
N6     | pointernoaliasing       | LLNL App   | Pointers assigned by different malloc calls, without aliasing
N6     | restrictpointer1        | LLNL App   | C99 restrict pointers used for array initialization, no aliasing
N6     | restrictpointer2        | LLNL App   | C99 restrict pointers used for array computation, no aliasing
N3     | sectionslock1           | New        | OpenMP parallel sections with a lock to protect shared data writes
N1,N4  | simd1                   | New        | OpenMP SIMD directive to indicate vectorization of a loop
N1,N5  | targetparallelfor       | New        | data races in loops offloaded to accelerators
N3     | taskdep1                | New        | OpenMP task with depend clauses to avoid data races