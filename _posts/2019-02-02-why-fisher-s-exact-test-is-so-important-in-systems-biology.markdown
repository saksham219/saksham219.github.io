---
layout:	post
title:	"Why Fisher's exact test is so important in systems biology?"
date:	2019-02-02
---

  ![](/img/0*opA4OAAkr68soFwh.png)
  *Cell*
  
In genomics studies, understanding the various changes taking place in various signalling and driving molecules and pathways is crucial. To understand how various signalling processes are undergoing change or enrichment, statistical methods are employed extensively.

To give you some context, every cell in our body has various proteins which signal each other to perform various processes such as cell division, cell death etc. These signalling networks are called pathways and understanding how these pathways change in different conditions such as cancer tumours, drug treatment etc are key for biologists to understand and design effective treatments for these conditions.

These pathways are a combination of proteins, metabolites, genes working together to send signals and perform various functions. Finding out which pathways are changing as a whole is key to identifying what changes are occurring inside a cell during different conditions such as cancer, or studying the effect of a drug.

![](/img/0*EzgaPmfsaEG3qoDf.jpg)

Let’s say you had some samples of cancerous tumours and you decided to run an RNA Sequencing experiment on them, and after some analysis you were able to identify a set of 50 genes that were characteristic of those tumour cells. These 50 genes are currently of no meaning to you, until you can identify which pathway(s) these might lie in. This is where Fisher’s test come in.

Decades of experiments, have enabled scientists to identify pathways in the cells and which genes(or proteins) these pathways are made of. This has led to the creation of pathway databases such as [KEGG](https://www.genome.jp/kegg/).

A pathway database is just a collection of pathways and the corresponding genes that lie within them. Now you have your set of 50 genes and you have a pathway database. Using these two you can identify pathways which are changing.

![](/img/1*wYCV-eRgbMvbOsIdcI-AgQ.png)
*Examples of pathways and the genes that lie in them*

But this could be done by just checking which pathway has the maximum overlap with my set of genes. Rightly so, but to assign how significant each overlap is you need a test. This is where Fisher’s test comes in.

#### What does the Fisher test exactly do?

In this case, Exact Fisher test is a method of statistically finding the overlap between elements of two lists. If you have two lists A and B. Both lists were sampled from a general population. If list A has 50 unique elements, and list B has 100 unique elements. Say 30 of the 100 elements in list B are present in list A. Now you ask yourself the question, did this overlap occur by pure chance (a null hypothesis in statistical terms) or was this significant (an alternate hypothesis in statistical terms)

The purpose of these two hypotheses is to give an answer to the question *— if I pick two lists randomly again and again from this ‘population’ will I still see this overlap again and again (i.e significance) or I will not and this was just a random occurrence caused by fate (non-significance)*? And the answer is quantified by a concept called ‘probability’.

The probability we try to find out here is — the probability of having more than 30 or more than intersecting elements between list A and list B assuming the null hypothesis to be true. This probability is what we call the p-value of the test.

So the p-value boils down to

p(30 overlap) + p(31 overlap) + …… p(50 overlap)

If this p-value comes out to be very small, then we can say that the likelihood of this overlap occurring between lists is very small and hence what we observe is significant.(rejecting the null). If not, what we observe is what we obtained by chance and has no significance(accepting the null)

The Fisher test uses a hypergeometric distribution to find this probability. This is just a fancy word for ‘combinations’ that is commonly taught in high schools.

Let us see how this p-value is calculated for our example. Let our gene list (G) consist of 50 genes, and let’s take one of the pathways(P) which consists of 30 genes. Let the intersection of these two be of 10 genes.

n(G∩P) = 10

Let’s make a table. You might have seen these kinds of 2x2 tables in other tests like the famous Chi-Square test.

![](/img/1*nGBOHjkm2jiGxDxFXZAZvw.png)

Now my goal is to find the probability of the overlap between P and G greater than 10.

p-value = P(10 overlap) + P(11 overlap) + …. p(30 overlap)

Now I can see that the probability of exactly x genes overlapping between P and G is,

P(x overlap) = Number of combinations where overlap is x/ Total number of combinations with any overlap

This probability can be found out easily using combinations, and the p-value can hence be calculated for all x’s.

Thus, we get a p-value for every pathway and after a p-value correction(because we are testing multiple hypothesis), the details of which I will not go into here, we can see which pathway is ‘significantly’ changing.

![](/img/1*XoZspJh4XXT4LDqsGpThrA.png)

We can then do experiments based on our findings and build new hypothesis on what is going on inside the cell.

  