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
Apply this code to generate MS02star null permutations, such as

$ R -f 01.ms02star.R --args data/human.pin.csv output/ms02.1.csv 100 9

The augments include the original network followed by the output null permutation. For the last two terms, the former is iterative number for removing self-interacting and redundant edges. The last term is for debugging, and it is set to 9 here to proceed. Usually the permutation succeeds within 100 recursive cycles. The success rate of this code depends on the original network: for yeast and human PINs, the success rate is around 80-90%. We recommend to perform more runs to generate enough number of null permutations.

2. 02.hallmark.Rmd
Note: All resources need be downloaded from the URLs shown above. Also see "hallmark.pdf" for markdown results.

The first chunk shows calculations of the interactions among 50 hallmark gene sets from MSigDB, which results a 50x50 matrix which is saved as "hhi.csv". This chunk can be extendefd for interaction analysis in ms02star null models.

The second chunk uses the Z-score matrix (also 50x50, which is based on the original PIN versus 10k ms02star null models, and is saved in "hhi.z.csv") to plot a Z-score heatmap. No dendrograms were added in the manuscript and all hallmark sets are named by serial numbers from 1 to 50, which can be used for comparison with the Jaccard heatmap (see below).

The third chunk constructs a Z-score network of all hallmark sets. Top 5% enriched (positive, shown in red) and top 5% suppressed (negative, shown in blue) are plotted.

The fourth chunk calculates the Jacard matrix (J = |A & B|/|A or B|), see the MS, and plot the Jaccard-heatmap. A Jaccard-network is also constructed using the top 5% Jaccard indices. Note that the hallmark sets are not presented in this repo and can be downloaded from the URL above.

The fifth chunk plots the interaction subnetwork between two gene sets based on the PIN; it can be extended to plot subnetworks based on MS02star null models. 

3. 03.network.figs.R

This code plots the subnetworks related to GO (BP, CC and MF, and pathways can also be used) terms. As an example, the subnetworks related to top-5 enriched BP, CC and MF GO terms for the hallmark gene set, HALLMARK_OXIDATIVE_PHOSPHORYLATION, were plotted. Also see Fig.4 of the manuscript.

The libraries used in the R-codes include "GO.db" to identify GO terms, "gplots" for heatmaps and "igraph" for network analysis.

Citation: <br> 
Guo, H., Qin, H. Association study based on topological constraints of protein–protein interaction networks. Sci Rep 10, 10797 (2020). https://doi.org/10.1038/s41598-020-67875-w
