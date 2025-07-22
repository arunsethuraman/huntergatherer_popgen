# Hunter-Gatherer Population Genomics
Contains data files for analyses of Native African Hunter Gatherer populations, as described by Sethuraman et al., 2025.

# Data Generation
African Hunter-Gatherer populations (Hadza, Sandawe) are a culturally diverse group of indigenous populations who are hypothesized to have diverged from other ancient African modern human lineages (particularly the Pygmy (Baka) and Yoruba (agricultural) populations). The Hadza and Sandawe are both historically Hunter-Gatherer populations from Central Tanzania, and are known to share a complex cultural and demographic history. 
While the Hadza are hypothesized to have little cultural confluence with other native populations, the Sandawe, on the other hand, have historically admixed with other Northern populations, including the Baka (pygmy), and Yoruba (pastoral/agricultural).

Here we filtered the genomes of 20 individuals (5 each of Hadza, Sandawe, Baka, and Yoruba) with filters used by Gronau et al., 2011, based on removing recombination hotspots, duplications, syntenic regions with chimpanzees. The filtered diploid SNP loci were then phased to obtain haplotypes across populations. The haplotypes were then filtered further to remove possible recombining segments using a four-gamete test.
This produced a total of 355 random, unlinked, putatively neutral loci, which were used in IM and admixture analyses, which are presented here in pairwise, IMa3 formatted input files.

# Data Analyses
Demography was then inferred under different models of population history - (1) 2 population IM models with all pairs of populations (Hadza-Sandawe, Sandawe-Baka, Baka-Yoruba, Baka-Hadza, Sandawe-Yoruba, Hadza-Yoruba) assuming that there is no ghost population, and (2) 2 population IM models with all pairs of populations, assuming that there is an outgroup ghost population.

All priors on population sizes, divergence times, and migration rates were set based on the guidelines of Hey (2011), by using the harmonic mean of Watterson's estimator of Ne across loci, and are shown below. Parallel runs of MCMC were then performed with 100,000 iterations of burn-in, followed by a total run time of 48 hours. Mixing, and convergence were assessed by observing swap rates over runs, acceptance rates of parameter updates, effective sample sizes, and autocorrelations. Convergence of the MCMC was then assessed using Tracer (Rambaut 2018). Sampled genealogies were used to estimate marginal posterior density distributions of demographic parameters and scaled with the modern human generation time of 29 years. Likelihood ratio tests were then used to determine statistical significance of migration estimates. These estimates were then compared with the four-population models (with ghost) of Hey et al., 2019, to understand potential parameter biases and ascertain power to provide support for or against the presence of unsampled ghost populations. 

# Prior distributions 

| Model | Theta | m     | t    |
|-------|-------|-------|------|
| BH    | 14.20 | 0.70  | 1.42 |
| HS    | 14.20 | 0.70  | 1.42 |
| SY    | 15.98 | 0.63  | 1.60 |
| BS    | 14.20 | 0.70  | 1.42 |
| BY    | 15.39 | 0.65  | 1.54 |
| HY    | 15.98 | 0.63  | 1.60 |
| All   |  5.51 | 20.00 | 2.20 |

**Table:** Prior upper limits on population sizes (Theta), migration rates (m), and divergence times (t) used in `IMa3` analyses of African Hunter-Gatherer demographic history. Models include pairwise comparisons among Baka (B), Hadza (H), Sandawe (S), and Yoruba (Y), and a full four-population model ("All").

# Models and Estimated Parameters

![africa_models_2pops.pdf](https://github.com/user-attachments/files/21374407/africa_models_2pops.pdf)

# IMa3 analyses
To perform IMa3 analyses with any of the files on an OpenMPI-equipped machine:

<pre lang="markdown">
bash #!/bin/bash 
# Run IMa3 from the folder where you have one of the files above
mpirun -np 4 ima3 -i BakaHadzaAllchromosomes -o bhall -q14.2 -m0.7 -t1.42 -b100000 -l48.0 -hn20 -ha0.97
</pre>


