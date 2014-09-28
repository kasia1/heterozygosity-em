heterozygosity-em
=================

HeterozygosityEM is an Expectation-Maximization algorithm for estimating genome-wide heterozygosity from sequence data.

This a reimplementation of the original C code that was used in 

*A novel approach to estimating heterozygosity from low-coverage genome sequence. * Bryc K, Patterson N, Reich D. *Genetics.* 2013

which may result in slightly different convergence due to numerical rounding differences.

The previous version was dependent on a complex system of C libraries, so as a result, the code has been reimplemented in python with only standard dependencies (eg, numpy) which should make it easier to support and use. 
