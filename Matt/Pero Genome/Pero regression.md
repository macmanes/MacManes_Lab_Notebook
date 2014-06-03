Pero Regression:


	cs <- as.matrix(read.delim("pero.tpm.txt"))
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


48500	c228273_g1_i1	raw p= 9.956139e-05

cat /mnt/data3/macmanes/pero_trans_assembly/pero.final.fa | grep -wA1 c111413_g1_i1