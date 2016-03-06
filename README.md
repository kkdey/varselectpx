# varselectpx
A R package + gh-pages on variable selection in topic models

## Overview

From the application of `maptpx` or `classtpx` models for unsupervised or semi-supervised topic model fitting to RNA-sequencing or other count data, we have observed that the computation time is usually pretty high especially when there are lots of features. This is a pretty commonplace issue in topic modeling on genetic data, because usually the features would either be transcripts/ genes / exons or even microsatellites and would usually vary from tens of thousands (genes) to around half a million (SNPs/ microsatellites).

As an instance, the `maptpx` model takes 3297 minutes to fit the topic model with $15$ clusters on the GTEx V6 data (n=8,555, p=16,069) at tolerance $0.1$. The model took $996$ minutes to run on the just on the GTEx brain samples (n=1,259, p=16,069) at same tolerance.

It must be noted that most of these genes are not relevant to the clustering and do not drive the clusters. Also under the general topic model, apart from the Dirichlet probablity constraint, the genes are considered independent. 

The idea therefore is to first split up the data into batches of genes and run a variable weighting method on these batches of genes. The variable weighting/selection method can be done in two ways

## Algorithm 


- Apply a topic model/ factor analysis on each batch of data, extract the theta matrix (cluster distributions) and extract the features for which there is a lot of evidence of them driving the clusters.Get a strength value for each gene in the batch based on cluster strength differences.

- Build a measure of strength for the topic model or the factor model. Note that if the batch of genes in the dataset is not important, then the clusters in the topic model would be very much randomly assigned. This is slightly trickier for unsupervised `maptpx` model but for `classtpx`, one can use the topic model fitted omega with the omega of training data to validate.

- Combine the strength of the clustering and the strength of the genes in each cluster to make an informed decision as to which genes should be kept in the study and which should be eliminated.

- Redo the topic model fitting on the filtered genes.

## Contact

For queries related to this project/package, contact [Kushal K Dey](kkdey@uchicago.edu)






