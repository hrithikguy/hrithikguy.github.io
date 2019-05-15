Title: VINAS
Date: 2018-01-21 16:44
Category: Projects
Tags: genetics, bioinformatics, statistics, machine learning, research
Authors: Aditya Gudibanda




This project holds a special place in my heart, because I consider it to be the first research project which I code completely from scratch, and I also got to work with some amazing colleagues at the Gerstein Lab at the Yale Department of Bioinformatics – Dr. Jing Zhang and Dr. Lucas Lochovsky.

I started off this project working with Jing with identifying whether a covariate-based approach to estimating mutation probabilities in the genome would be a valid approach, which involved a lot of data crunching and visualization in R. Some of the covariates I looked at were CpG, chromatin accessibility, and various other biologically significant variables. Once we had determined that it was in fact a feasible idea, we were off to the races in terms of deciding upon a suitable model.

The core problem that we wished to solve was to find genes that are significantly linked with cancer. There are some genes that have many mutations, but are located in regions of the genome with a high background mutation rate, and hence are not that significant. There are also genes that are significantly less mutated than they “should” be compared to the background mutation rate. The purpose of this project was first to quantify and come up with a model for the background mutation rate, and then to design a statistical methodology to determine when the observed mutation count was statistically significant.

Coming up with a model for the mutation rates of the genome is quite a daunting task. First, there are a huge number of biological factors that determine the true background mutation rate, and second, the genome is huge (~3 billion base pairs). We decided to use logistic regression on a set of 7 covariates, with binary output based on a cohort of genomes of cancer patients (whether, out of all the patients, any of them had a mutation in that location). This worked very well, as some of the covariates captured a high proportion of variance in the mutation rate.

This was an interesting engineering task – each chromosome is a few dozen gigabytes, so this added up to doing logistic regression on a few terabytes worth of data. I used the LIBSVM (https://www.csie.ntu.edu.tw/~cjlin/libsvm/) to do this, and I used MPI to perform this in parallel in Yale’s High-Performance Computing environment. The final code for all of this will be linked at the end of this blog post.

After doing this, the next step was to compute the p-values for each gene. Remember that the model so far has given us a set of probabilities p1, .., pn for each of the n bases in the gene, and we have the location and total count of the mutations for each gene. The task is to figure out how to calculate the p-values. If our test statistic is the total count, then this is actually the sum of independent Bernoulli variables with different success probabilities. This is a well-known distribution known as the Poisson binomial distribution (https://en.wikipedia.org/wiki/Poisson_binomial_distribution) and it is numerically tractable.

I am pleased to say that I completed this part of the project and I verified that the program outputted several genes that are known via experimental biology to be indeed significantly linked with cancer, as well as a few genes that have never been seen before (which I am not allowed to report because this was based on data that only the Gerstein Lab had access to and has not been published yet).

The final part of this project was to incorporate something called Funseq2 scores (http://funseq2.gersteinlab.org/), which is another project at the Gerstein Lab which gives each nucleotide in the genome a “score” related to its correlation with cancer. The idea was to change the test statistic from the sum of Bernoulli variables, to the weighted sum of Bernoulli variables, where the weights are the Funseq2 scores. I and my collaborators thought that this would increase our statistical sensitivity to detect cancerous genes by incorporating the information captured by Funseq2.

I found some papers that showed how to do this: This paper uses Chernoff-Hoeffding type bounds (https://www.cc.gatech.edu/~mihail/Rag88.pdf), and another paper (https://arxiv.org/pdf/1301.7392.pdf) gives a bound in both directions. However, both of these papers only give upper bounds and these bounds are too weak in practice. I coded both of these bounds and they gave results that were too weak (p-values that were too high) due to the fact that these are upper bounds on the true p-values.

At this point, the summer was reaching to an end, and I was not able to figure out how to solve the problem in time. However, this was an exhilarating experience, going from the initial idea, to full implementation, to the final frontier of trying to find new math and theory to compute a statistical p-value. This was especially exciting because the first approach without using the Funseq2 values was already finding genes that had never been reported before.

 

The code for VINAS is located here: https://github.com/hrithikguy/VINAS
