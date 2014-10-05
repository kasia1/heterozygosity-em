heterozygosity-em
=================

HeterozygosityEM is an Expectation-Maximization algorithm for estimating genome-wide heterozygosity from sequence data.

This a reimplementation of the original C code that was used in: 

*A novel approach to estimating heterozygosity from low-coverage genome sequence*  
Bryc K, Patterson N, Reich D. *Genetics* 2013

which may result in slightly different convergence due to numerical rounding differences.

The previous version was dependent on a complex system of C libraries, so as a result, the code has been reimplemented in python with only standard dependencies (eg, numpy) which should make it easier to support and use. 

##### Brief overview of the algorithm
The EM algorithm works really well at finding an optimum likelihood when you are missing some observed data that would help you make that calculation. In our case, what we are missing is the true genotypic state underlying each position in the genome sequence data.

Instead, what we observe are the number of ancestral and derived alleles (we assume that we only see two variants) counts and some set of alleles in some other panel of individuals. The EM helps us to split up this matrix of observed counts into estimates of homozygous-ancestral, heterozygous, and homozygous-derived matrixes. From there, it is simple to count the number of heterozygous positions in the sequence total, providing us with an estimate of heterozygosity.

##### Some important information on the datafile and initialization conditions
The EM is a local-optimization algorithm. It is very good at increasing the likelihood, but it is not guaranteed to find the global maximum, and certainly doesn't know that we want to find the three states that correspond to homozygous for the ancestral allele, heterozygous, and homozygous for the derived allele.

To help the EM give our desired outcome, namely, to converge to three states that correspond to the genotype states, we initialize to states that match our expectations for the read counts given the genotypic states. So in our initialization, we assume certain things about the format of the counts file.

###### Assumptions on input data:  
* We assume that the rows capture the different permutations of allele combinations of the reference panel, and that the first row corresponds to the ancestral state for all individuals, which should, for sequence data, be the vast majority of the data. The last row should correspond to the state with all derived alleles.
* We assume that the columns correspond to counts of derived allele, such that the first column is 0 derived alleles, and the _n_th column corresponds to _n_ derived alleles.
* As a matter of formatting, we only allow integer counts of the data, with space-separated values.

It is possible that other data formats would still converge to the genotypic states, so you can give it a shot, but if your results don't make much sense, that may the be first place to troubleshoot.

## Troubleshooting

