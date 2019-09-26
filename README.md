# NetPAS
This repo provides URLs and codes for NetPAS. It contains resources (only URLs are provided) and codes for NetPAS (Network Permutation-based Association Study).

* The human protein-protein interaction network (PIN) is obtained from InWeb_IM network (Li et al. Nature Methods 2017, 14:61-64). This network was downloaded from Lage lab resources:
http://www.lagelab.org/resources/

* The gene ontology (GO) terms from GOC (geneontology.org) updated @ Feburary 2019 (The Gene Ontology Consortium, Nuc. Acids Res. 2019, 47:D330-D338). Genes related to all terms are downloaded from the Gene Ontology Resource:
http://geneontology.org/

* Pathways collected by ConsensusPathDB (Kamburov et al. Nuc. Acids Res. 2009, 37:D623-D628, Kamburov et al. Nuc. Acids Res. 2013, 41:D793-D800; Herwig et al. Nat. Protoc. 2016, 11:889-907) such as the KEGG, BioCarta and Reactome pathways (see example codes). All pathways are obtained from the CPDB:
http://cpdb.molgen.mpg.de/

* Genes related to 19 human diseases are from OMIM (Amberger et al. Nuc. Acids Res. 2019, 47:D1038-D1043):
https://www.omim.org/

* The 50 HALLMARK protein sets from MSigDB (category H):
http://software.broadinstitute.org/gsea/msigdb

A list of the 50 hallmark gene sets is saved in /data/hallmark.list

The R-codes include

1. 01.ms02star.R 
Apply this code to generate null permutations, such as

$ R -f 01.ms02star.R --args data/human.pin.csv output/ms02.1.csv 100 9

The augments include the original network followed by the output null permutation. For the last two terms, the former is used for number of cycles to rebuild from self-interacting and redundant edges to generate the correct model. The last term is for debug use and it is set to 9 to proceed. Usually the permutation may succeed within 100 recursive cycles. The success rate of this code depends on the original network: for yeast and human PINs, the success rate is around 80-90%. We recommend to perform more runs to make enough success permutations.

2. 02.hallmark.Rmd
Note: All resources need be downloaded from the URLs shown above. We not have the copy right to publish them in this repo.
Results of this markdown code is recorded in "hallmark.pdf".

The first chunk of this markdown code shows calculations of the interactions between a pair of gene sets, which results a 50x50 matrix for all hallmark sets, saved as "hhi.csv". This part of colde can be used for interaction analysis in ms02star null models.

The second chunk of this markdown code uses the Z-score matrix (also 50x50, which is based on the original interaction and matrices from 10k ms02star null models, see in "hhi.z.csv") to plot a Z-score heatmap. In our manuscript there are no dendrograms and all hallmark sets are named by serial numbers, also for comparison with the Jaccard heatmap (see below).

The third chunk of this markdown code constructs a Z-score network of all hallmark sets. Top 5% enriched (positive, shown in red) and suppressed (negative, shown in blue) are plotted.

The fourth chunk of this markdown code calculate the Jacard matrix (J = |A & B|/|A or B|), see the MS, and plot the Jaccard-heatmap. A Jaccard-network is also constructed using the top 5% Jaccard indices. Note that the hallmark sets are not presented in this repo and need be obtained from the URL above.

The fifth chunk of this markdonw code shows how to plot the interaction subnetwork between different sets using the PIN. 

3. 03.network.figs.R

This code is used to plot the subnetworks related to GO (can use pathways etc) terms. As an example, the top-5 enriched BP, CC and MF GO terms have been selected, and the subnetworks related to these terms are plotted (see Fig.4 of the MS).

Sample network graphs (functional neighbor subnetworks of the top-5 BP, CC and MF GO terms of the gene set "genes.csv") are saved in the folder network/. Also see Fig.4 of the MS.

The libraries used in the R-codes include "GO.db" to identify GO terms, "gplots" for heatmaps and "igraph" for network analysis.
