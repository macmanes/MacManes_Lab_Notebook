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
	biocLite("vsn")
	biocLite("gplots")
	biocLite("vsn")
	biocLite("gplots")
	
	library( "DESeq2")
	library("RColorBrewer")
	library("gplots")	pero <- read.delim("pero.effcounts.txt", header=T, row.names=1)
	ExDes <- data.frame(row.names=colnames(pero), condition = c("wet","wet","dry","dry","dry","dry"))
	samples <- data.frame(row.names=c("wet1","wet2","dry1","dry2","dry3","dry4"),
    	condition=as.factor(c(rep("wet",2), rep("dry",4))))
 
	bckCDS <- DESeqDataSetFromMatrix(countData = pero, colData=samples, design=~condition)
	dds <- DESeq(bckCDS)
	res <- results(dds)
	plotDispEsts(dds, ylim = c(1e-6, 1e1) )
	sum( res$padj < 0.01, na.rm=TRUE )
	plotMA(dds, alpha=.01)
	
	#hist of p values
	hist( res$pvalue, breaks=20, col="grey" )	

	#rlog transformation
	rld <- rlogTransformation(dds)	
	vsd <- varianceStabilizingTransformation(dds)

	#plot showing difference
	par( mfrow = c( 1, 2 ) )
	plot( log2( 1+counts(dds, normalized=TRUE)[, 1:2] ), col="#00000020", pch=20, cex=0.3 )
	plot( assay(rld)[, 1:2], col="#00000020", pch=20, cex=0.3 )
	
	#heatmap
	sampleDists <- dist( t( assay(rld) ) )
	sampleDistMatrix <- as.matrix( sampleDists )
	rownames(sampleDistMatrix) <- paste( rld$treatment,
	rld$patient, sep="-" )
	colnames(sampleDistMatrix) <- NULL
	library( "gplots" )
	library( "RColorBrewer" )
	colours = colorRampPalette( rev(brewer.pal(9, "Blues")) )(255)
	heatmap.2( sampleDistMatrix, trace="none", col=colours)


\#HEATMAP

	select <- order(rowMeans(counts(dds,normalized=TRUE)),decreasing=TRUE)[1:30]
	hmcol <- colorRampPalette(brewer.pal(9, "GnBu"))(100)
	heatmap.2(counts(dds,normalized=TRUE)[select,], col = hmcol,
		Rowv = FALSE, Colv = FALSE, scale="none",
		dendrogram="none", trace="none", margin=c(10,6))
	

this one is a good heatmap, looks art highly vriable genes

	library( "genefilter" )
	topVarGenes <- head( order( rowVars( assay(vsd) ), decreasing=TRUE ), 200 )
	heatmap.2( assay(vsd)[ topVarGenes, ], scale="row",
	trace="none", dendrogram="column",
	col = colorRampPalette( rev(brewer.pal(9, "RdBu")) )(255))
	

	ramp <- 1:3/3
	cols <- c(rgb(ramp, 0, 0),
	rgb(0, ramp, 0),
	rgb(0, 0, ramp),
	rgb(ramp, 0, ramp))
	print( plotPCA( rld, intgroup = c( "wet", "d"), rycol=cols ) )

	heatmap.2(assay(rld)[select,], col = hmcol,
		Rowv = FALSE, Colv = FALSE, scale="none",
		dendrogram="none", trace="none", margin=c(10, 6))    library("vsn")
    par(mfrow=c(1,3))
    notAllZero <- (rowSums(counts(dds))>0)
    meanSdPlot(log2(counts(dds,normalized=TRUE)[notAllZero,] + 1),
    ylim = c(0,2.5))
    meanSdPlot(assay(rld[notAllZero,]), ylim = c(0,2.5))
    meanSdPlot(assay(vsd[notAllZero,]), ylim = c(0,2.5))