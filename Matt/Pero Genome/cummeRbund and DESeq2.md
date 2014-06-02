cummeRbund
-

	source("http://bioconductor.org/biocLite.R")
	biocLite("cummeRbund")
	library(cummeRbund)
	cuff<-readCufflinks()
	d<-dispersionPlot(genes(cuff))
	pBoxRep<-csBoxplot(genes(cuff),replicates=T)
	
DEseq2
-


	source("http://bioconductor.org/biocLite.R")
	biocLite("DESeq2")
	biocLite("gplots")
	library( "DESeq2")
	library("RColorBrewer")
	library("gplots")	pero <- read.delim("~/Documents/deseq2_analyses/pero.txt", header=T, row.names=1)
	ExDes <- data.frame(row.names=colnames(pero), condition = c("wet","wet","wet","dry","dry","dry"))
	samples <- data.frame(row.names=c("wet","wet.1","wet.2","dry","dry.1","dry.2"),
    	condition=as.factor(c(rep("ctl",3), rep("del",3))))
 
	bckCDS <- DESeqDataSetFromMatrix(countData = pero, colData=samples, design=~condition)
	dds <- DESeq(bckCDS)
	res <- results(dds)
	plotDispEsts(dds, ylim = c(1e-6, 1e1) )
	
\#HEATMAP

	select <- order(rowMeans(counts(dds,normalized=TRUE)),decreasing=TRUE)[1:30]
	hmcol <- colorRampPalette(brewer.pal(9, "GnBu"))(100)
	heatmap.2(counts(dds,normalized=TRUE)[select,], col = hmcol,
		Rowv = FALSE, Colv = FALSE, scale="none",
		dendrogram="none", trace="none", margin=c(10,6))
	