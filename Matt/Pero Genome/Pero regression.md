Pero Regression:



    cs <- as.matrix(read.delim("pero.tpm.txt1"))
    for(n in 4:nrow(cs)) {
        x <- try(summary(lm(as.numeric(cs[2,c(2:7)]) ~ as.numeric(cs[n,c(2:7)])))$coefficients[2,4], silent = TRUE)
        y <- try(summary(lm(as.numeric(cs[3,c(2:7)]) ~ as.numeric(cs[n,c(2:7)])))$coefficients[2,4], silent = TRUE)
        if(x<.00001 & y<.00001) {
            cat(n,"\t",cs[n,1],"\t", "raw p= ", x, "\n", sep = "", file = "")
        }
    }

head(cs)



    > head(cs)
        names           wet1     wet2    dry1     dry2    dry3    dry4   
    [1,] "Sodium"        "   152" "  151" "   165" "  170" "  162" "  165"
    [2,] "c100008_g1_i1" "     0" "    0" "     0" "    0" "    0" "    0"
    [3,] "c100015_g1_i1" "     0" "    0" "     0" "    0" "    0" "    0"
    [4,] "c100015_g1_i2" "     0" "    0" "     0" "    0" "    0" "    0"
    [5,] "c100017_g1_i1" "     3" "    1" "     0" "    0" "    0" "    0"
    [6,] "c10001_g1_i1"  "     0" "    3" "     2" "    2" "    0" "    0"
    >


>>48500	c228273_g1_i1	raw p= 9.956139e-05

>>104266	c96263_g2_i1	raw p= 3.866828e-05


cat /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa | grep -wA1 c228273_g1_i1

	
    1814	c113620_g1_i1	raw p= 2.672977e-05 polysaccharide biosynthesis domain containing 1 (Pbdc1)
    2804	c119017_g1_i1	raw p= 2.910683e-05 phosphotriesterase related (Pter)
    *7235	c150421_g1_i1	raw p= 4.878605e-05	none
    11553	c171918_g1_i1	raw p= 2.329851e-05	heterogeneous nuclear ribonucleoprotein A/B (Hnrnpab)
    14929	c185268_g1_i1	raw p= 5.388551e-05 kelch-like 42 (Klhl42)
    15318	c186564_g1_i1	raw p= 5.186312e-05	VAMP (vesicle-associated membrane protein)-assoc. Vapb
    18319	c195420_g1_i1	raw p= 2.382286e-05 Fas cell surface death receptor (Fas)
    21959	c203027_g1_i3	raw p= 9.753688e-05 sirtuin 5 (Sirt5)
    23012	c204662_g1_i2	raw p= 5.388551e-05 nuclear receptor subfamily 1, group I, member 2 (Nr1i2)
    23279	c205036_g1_i1	raw p= 1.6561e-05  nth endonuclease III-like 1 (Nthl1)
    26377	c210242_g1_i4	raw p= 5.019948e-05 FGFR1 oncogene partner 2 (Fgfr1op2)
    27877	c212287_g1_i1	raw p= 5.554408e-05 peroxisomal biogenesis factor 11 alpha (Pex11a)
    30918	c215994_g1_i1	raw p= 9.956139e-05 kelch-like family member 22 (Klhl22)
    33430	c218632_g1_i2	raw p= 7.82864e-05 NFS1 cysteine desulfurase (Nfs1)
    34478	c219667_g1_i1	raw p= 5.04038e-05 sorting nexin 1 (Snx1)
    38568	c222873_g1_i2	raw p= 7.708392e-05 dematin actin binding protein (Dmtn)
    40668	c224147_g2_i7	raw p= 1.725915e-05 ATP5S-like (Atp5sl)
    44143	c226090_g1_i1	raw p= 1.016452e-06 aldo-keto reductase family 7, member A2 (Akr7a2)
    48059	c228069_g4_i2	raw p= 3.285311e-05 acyl-CoA synthetase short-chain family member 1 (Acss1)
    51599	c229614_g7_i1	raw p= 1.890506e-05 Ndst1
    53524	c230325_g3_i1	raw p= 1.6561e-05 Ldlrad3
    55417	c231114_g11_i1	raw p= 7.052927e-05 Anapc13
    55538	c231155_g1_i2	raw p= 2.235395e-05 Siae
    56326	c231448_g4_i1	raw p= 3.846585e-05 Gabarapl1
    59445	c232551_g5_i2	raw p= 7.297572e-05 Gtf2ird2
    60256	c232858_g3_i2	raw p= 8.382555e-06 Trub1
    61126	c233162_g3_i1	raw p= 2.830928e-05	Abca3***
    61230	c233197_g2_i1	raw p= 7.032711e-05 Slc22a11
    65123	c234519_g3_i1	raw p= 2.212793e-05 Fam149b1
    66825	c235090_g2_i1	raw p= 2.212793e-05 Ppm1l
    67702	c236231_g1_i1	raw p= 4.26761e-05 Pmpcb
    82469	c403035_g1_i1	raw p= 8.139244e-06 Ncbp2
	88560	c471472_g1_i1	raw p= 5.04038e-05 Hoxd10
	94969	c543038_g1_i1	raw p= 2.212793e-05 none
	104266	c96263_g2_i1	raw p= 3.948493e-05 Pter
	44188	c226125_g2_i11	raw p= 2.212793e-05 : Add1





    328	c113620_g1_i1	raw p= 2.672977e-05
    568	c119017_g1_i1	raw p= 2.910683e-05
    1504	c150421_g1_i1	raw p= 4.878605e-05
    2576	c171918_g1_i1	raw p= 2.329851e-05
    3446	c185268_g1_i1	raw p= 5.388551e-05
    3562	c186564_g1_i1	raw p= 5.186312e-05 VAMP
    4420	c195420_g1_i1	raw p= 2.382286e-05
    5556	c203027_g1_i3	raw p= 9.753688e-05
    5915	c204662_g1_i2	raw p= 5.388551e-05
    5995	c205036_g1_i1	raw p= 1.6561e-05
    7042	c210242_g1_i4	raw p= 5.019948e-05
    7498	c212287_g1_i1	raw p= 5.554408e-05
    8425	c215994_g1_i1	raw p= 9.956139e-05
    9272	c218632_g1_i2	raw p= 7.82864e-05
    9575	c219667_g1_i1	raw p= 5.04038e-05
    10860	c222873_g1_i2	raw p= 7.708392e-05
    11548	c224147_g2_i7	raw p= 1.725915e-05
    12615	c226090_g1_i1	raw p= 1.016452e-06
    13857	c228069_g4_i2	raw p= 3.285311e-05
    14892	c229614_g7_i1	raw p= 1.890506e-05
    15487	c230325_g3_i1	raw p= 1.6561e-05
    16053	c231114_g11_i1	raw p= 7.052927e-05
    16089	c231155_g1_i2	raw p= 2.235395e-05
    16338	c231448_g4_i1	raw p= 3.846585e-05
    17293	c232551_g5_i2	raw p= 7.297572e-05
    17547	c232858_g3_i2	raw p= 8.382555e-06
    17768	c233162_g3_i1	raw p= 2.830928e-05
    17801	c233197_g2_i1	raw p= 7.032711e-05
    18907	c234519_g3_i1	raw p= 2.212793e-05
    19354	c235090_g2_i1	raw p= 2.212793e-05
    19585	c236231_g1_i1	raw p= 4.26761e-05
    20552	c403035_g1_i1	raw p= 8.139244e-06
    21004	c471472_g1_i1	raw p= 5.04038e-05
    22311	c96263_g2_i1	raw p= 3.948493e-05


RCode

     test=2
     row=17766
     par(mfrow=c(2,2))
     plot(as.numeric(cs[test,c(2:7)]) ~ as.numeric(cs[row+3,c(2:7)]), lwd=4, pch=3, frame.plot=F, 
     	xlab='Abca3 expression', 
     	ylab='Serum Sodium', 
     	main='Na vs Abca3',
     	col=c("dodgerblue","dodgerblue","sienna4","sienna4","sienna4","sienna4"))
     abline(lm(as.numeric(cs[test,c(2:7)]) ~ as.numeric(cs[row+3,c(2:7)])), lwd=4, col='red')
     plot(as.numeric(cs[test+1,c(2:7)]) ~ as.numeric(cs[row+3,c(2:7)]), lwd=4, pch=3, frame.plot=F, 
     	xlab='Abca3 expression', 
     	ylab='Serum Chloride', 
     	main='Cl vs Abca3',
     	col=c("dodgerblue","dodgerblue","sienna4","sienna4","sienna4","sienna4"))
     abline(lm(as.numeric(cs[test+1,c(2:7)]) ~ as.numeric(cs[row+3,c(2:7)])), lwd=4, col='red')
     boxplot(as.numeric(cs[row+3,c(2:7)]) ~ cs[1,c(2:7)], main='Slc22a11', ylab='FPMK', frame.plot=F, cex.main=1.1, cex.lab=1, 
     	col=(c("sienna4","dodgerblue")))
































	