Introduction
============

This package provides a solver for a system of linear equations. It is an
implementation of the [tridiagonal matrix algorithm][1], also known as *Thomas
algorithm*.

Input:

    b[0] * x[0] + c[0] * x[1]                             = d[0]
    a[0] * x[0] + b[1] * x[1] + c[1] * x[2]               = d[1]
                  a[1] * x[1] + b[2] * x[2] + c[2] * x[3] = d[2]
                                a[2] * x[1] + b[3] * x[2] = d[3]

In matrix notation:

![Rendering in matrix notation][1]

For the algorithm to definitely find a solution, the tridiagonal matrix needs
to be *diagonally dominant:*

    |b[0]|   > |c[0]|
    |b[1]|   > |a[0] + c[1]|
    |b[2]|   > |a[1] + c[2]|
    …
    |b[n-1]| > |a[n-2]|

If that condition is not met, then it may happen that the algorithm cannot find
a solution even if one exists.

In case no solution is found, the result is `null`. For bad input, the result
is undefined.


Examples
========

  * Three unknowns:

    ![Rendering in matrix notation][3]

    Input:

        var solve = require('./node_main.js');
        return solve([4, 3], [1, 5, 8], [9, 7], [5, 6, 2]);

    Result: `[0.784387, 0.468401, 0.0743494]`

  * Matrix is *not* diagonally dominant, and algorithm fails although solution
    exists:

    ![Rendering in matrix notation][4]

    Snippet: `solve([0], [1, 0], [1], [1, 0]), null)`

    Result: `null`

  * Solution found although matrix is *not* diagonally dominant:

    ![Rendering in matrix notation][5]

    Snippet: `solve([1], [1, 0], [1], [1, 0]), null)`

    Result: `[0, 1]`


License
=======

Except where noted otherwise, files are licensed under the MIT License.


The MIT License (MIT)
---------------------

Copyright (c) 2014 [Felix E. Klee](mailto:felix.klee@inka.de)

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[1]: images/input-matrix.png
[2]: http://en.wikipedia.org/wiki/Tridiagonal_matrix_algorithm
[3]: images/example1.png
[4]: images/example2.png
[5]: images/example3.png
