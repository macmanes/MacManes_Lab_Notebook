SOAP Error Correction
-

in `/mnt/data0/macmanes/SOAP`

	SOAPdenovo-Trans-127mer all -K 35 -p 20 -s soap.config -o 10M_0
	
optimize k

	for k in 35 45 55 65; do SOAPdenovo-Trans-127mer all -K $k -p 20 -s soap.config -o 20M_5_$k; done


making pslx
-

	/share/trinityrnaseq_r20140413p1/Analysis/FL_reconstruction_analysis/FL_trans_analysis_pipeline.pl \
	--target Mus_musculus.GRCm38.71.cdna.abinitio.fa --query ../assemblies/10M_0.scafSeq