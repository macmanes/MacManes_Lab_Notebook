Pero Regression:


	cs <- as.matrix(read.delim("pero.tpm.counts"))
	for(n in 3:nrow(cs)) {
   	  x <- try(summary(lm(as.numeric(cs[1,c(2:7)]) ~ as.numeric(cs[n,c(2:7)])))$coefficients[2,4], silent = TRUE)
   	  if(x<.0001) {
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


1440	c111413_g1_i1	raw p= 1.427684e-05
24562	c207751_g1_i1	raw p= 5.075292e-05
32376	c217365_g1_i4	raw p= 5.179443e-05
35604	c220601_g1_i1	raw p= 9.954003e-05
44539	c226315_g2_i2	raw p= 4.302244e-05
44629	c226369_g2_i1	raw p= 3.607383e-05
48500	c228273_g1_i1	raw p= 6.335171e-05
66825	c235090_g2_i1	raw p= 9.267964e-05
67556	c235410_g1_i1	raw p= 8.189539e-05
104266	c96263_g2_i1	raw p= 6.123636e-05

cat /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa | grep -wA1 c111413_g1_i1