# Berry Levinsohn Pakes 1995 algorithm implementation
This repository provides a class implementation of BLP(1995)
for Python 3.+, based upon several guiding principles written
by Aviv Nevo in his famous Practitioner Guide.

Some of the features of this BLP implementations are:
1. Flexible simulation of population. Modifiable by user-provided distribution.
2. Two algorithms for the optimization routine:
..* Nelder-Mead non-derivative search. Better suited for an initial exploration, as it is less sensible to starting points but slower.
..* L-BFGS-B gradient based search. A bounded BFGS algorithm that has better performance and helps avoid the common overflows due to the exponential form of logit.
3. Adaptive delta fixed-point tolerance (as recommended by Aviv Nevo).
4. Flexible separation of the fixed point by markets. This allows for:
..* Solving the entire data each step.
..* Separating by groups and solving each sequentially.
..* Separating by groups and solving in parallel on a multiprocessor computer.
5. Optional Anderson acceleration of the delta fixed-point.
6. A lot of comments to guide anyone who wants to implement his one version.

Additionally to the main BLP.py class, the file test.py provides
a fairly random Monte-Carlos simulator that generate an unbalanced panel
for testing the class. The package also provides three tests:
1. test.py: test the general functioning of the class
2. test_acceleration.py: shows the advantages of the Anderson acceleration
3. test_mul.py: shows the advantages of the multiprocessing technique.
test_log.txt shows the results of the last one, that also showcases the other
points.

So far, the recommended workflow for this class is to first preform a few high-tolerance runs with different starting points using the Nelder-Mead algorithm.
Once you have figured out where the results might be, do a low-tolerance bounded run with the L-BFGS-B algorithm.
In general, Anderson acceleration, adaptive delta tolerance are recommended. Parallelization is recommended only if each fixed-point calculation takes long enough to justify the overhead implied in the parallelization.

See notes.txt for a short description of the algorithm and
further details about possible future updates to this package.