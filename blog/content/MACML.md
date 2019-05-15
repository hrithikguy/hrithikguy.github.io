Title: MACML
Date: 2018-01-15 16:44
Category: Projects
Tags: genetics, bioinformatics, statistics, machine learning, research, public health
Authors: Aditya Gudibanda




This project is based on a software and algorithm developed by the Townsend Lab at the Yale School of Public Health, located here: http://medicine.yale.edu/lab/townsend/sand/

The paper for this project is located here: https://www.ncbi.nlm.nih.gov/pubmed/19557160
The basic setup of this project is sequences of discrete binary data. The purpose is to find significant regions of higher or lower probability of a “1” in these sequences. This is useful for genome data, where the elements of the sequence represent nucleotides of a gene, and a “1” represents the presence of a mutation.

At first glance one might think that we should just set each “region” to be one nucleotide long and set the probability to be 0 or 1 depending on if the actual sequence has a 0 or 1 in that location. This model would assign the best possible likelihood of 1 to the observed data. However, there are two problems – first, we could have multiple sequences as input, and the likelihood would no longer be 1 (although you could argue that we just assign the probability to be the empirical distribution of that nucleotide across all sequences). Second, this model has a lot of parameters – each nucleotide adds an additional parameter to this model. This raises the significant possibility of overfitting, which is a common problem in practice.

In this project, I extended the existing software which only worked for one dimensional data, to two dimensional data. The code is located here: https://github.com/hrithikguy/PEMA
