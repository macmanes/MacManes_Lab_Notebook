Feeding
--

	svn checkout svn://svn.code.sf.net/p/trinityrnaseq/code/trunk trinityrnaseq-code
	...
	Checked out revision 3991
	make -j8
	
in `/mouse/feeding/`

    ./assembly.mk --dry-run
    Trinity --seqType fq --JM 50G --trimmomatic \
        --left /mouse/feeding/20M_corr/20M_corrk19.1.corrected.fastq.gz  \
        --right /mouse/feeding/20M_corr/20M_corrk19.2.corrected.fastq.gz \
        --CPU 32 --output 20M.ec.P2 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --left /mouse/feeding/100M_corr/100M_corrk19.1.corrected.fastq.gz  \
        --right /mouse/feeding/100M_corr/100M_corrk19.2.corrected.fastq.gz \
        --CPU 32 --output 100M.ec.P2 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --single /mouse/feeding/20M_corr/20M.corr.inter.norm.fastQ.gz \
        --run_as_paired \
        --CPU 32 --output 20M.ec.P2.C50 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"
    Trinity --seqType fq --JM 50G --trimmomatic \
        --single /mouse/feeding/100M_corr/100M.corr.inter.norm.fastQ.gz \
        --run_as_paired \
        --CPU 32 --output 100M.ec.P2.C50 \
        --quality_trimming_params "ILLUMINACLIP:/mouse/feeding/barcodes.fa:2:40:15 LEADING:2 TRAILING:2 MINLEN:25"

>Transrate

in `/mouse/feeding/transrate`

	transrate -a ../20M.ec.P2/Trinity.fasta -r ../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/20M.ec.P2/20M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/20M.ec.P2/20M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 20M.ec.P2 -t 20
	

in `/mouse/feeding/transrate`


	transrate -a Trinity.fasta -r ../Mus_musculus.GRCm38.pep.all.fa \
	-l 100M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i 100M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 100M.ec.P2 -t 20
	
	TRANSRATE ASSEMBLY SCORE: 0.361 


Post filtering
---

for `20M.ec.P2` in `/mouse/feeding/20M.ec.P2/express_filt`

Take the transrate express results.

	sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' Trinity.fasta > 20M.ec.P2.Trinity.fasta
	awk '1>$15{next}1' Trinity.fasta_results.xprs | awk '{print $2}' | sed '1,1d' | split -l 4000 -
	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp18.fa; done &
	for i in `cat xas`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp19.fa; done &
	for i in `cat xat`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp20.fa; done &
	for i in `cat xau`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp21.fa; done &
	for i in `cat xav`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp22.fa; done &
	for i in `cat xaw`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp23.fa; done &
	for i in `cat xax`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp24.fa; done &
	for i in `cat xay`; do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp25.fa; done &

	cat temp* > 20M.ec.P2.express.Trinity.fasta


	transrate -a 20M.ec.P2.express.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/20M.ec.P2/20M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/20M.ec.P2/20M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 20M.ec.express.P2 -t 20
	
	SCORE==.429


for `100M.ec.P2` in `/mouse/feeding/100M.ec.P2/express_filt`

	sed ':begin;$!N;/[ACTGNn-]\n[ACTGNn-]/s/\n//;tbegin;P;D' Trinity.fasta > 20M.ec.P2.Trinity.fasta
	awk '1>$15{next}1' Trinity.fasta_results.xprs | awk '{print $2}' | sed '1,1d' | split -l 4000 -
	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp18.fa; done &
	for i in `cat xas`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp19.fa; done &
	for i in `cat xat`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp20.fa; done &
	for i in `cat xau`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp21.fa; done &
	for i in `cat xav`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp22.fa; done &

	cat temp* > 100M.ec.P2.express.Trinity.fasta


	transrate -a 100M.ec.P2.express.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/100M.ec.P2/100M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/100M.ec.P2/100M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 100M.ec.express.P2 -t 20

100M Filter based on contig score
---

in `/mouse/feeding/100M.ec.P2/score_filt`

	awk -F "," '.3>$17{next}1' 100M.ec.P2_Trinity.fasta_contigs.csv   | awk -F "," '{print $1}' | split -l 8000
	

	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp18.fa; done &
	for i in `cat xas`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp19.fa; done &
	for i in `cat xat`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp20.fa; done &
	for i in `cat xau`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp21.fa; done &
	for i in `cat xav`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp22.fa; done &

	for i in $(cat xaw); do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp23.fa; done &
	for i in $(cat xax); do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp24.fa; done &
	for i in $(cat xay); do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp25.fa; done &
	for i in $(cat xaz); do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp26.fa; done &
	for i in $(cat xba); do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp27.fa; done &

	cat temp* > 100M.ec.P2.score.Trinity.fasta


	transrate -a 100M.ec.P2.score.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/100M.ec.P2/100M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/100M.ec.P2/100M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 100M.ec.score.P2 -t 40
	
	score = 0.3912

---

**filter 100M set based on express AND score .3**
--

---

in `/mouse/feeding/100M.ec.P2/score_express_filt`

	awk -F "," '1>$22{next}1' 100M.ec.P2_Trinity.fasta_contigs.csv  | awk -F "," '.3>$17{next}1' | awk -F "," '{print $1}' | split -l 4000
	
	ln -s ../express_filt/100M.ec.P2.Trinity.fasta .

	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp18.fa; done &

	cat temp* > 100M.ec.P2.score.express.Trinity.fasta

	transrate -a 100M.ec.P2.score.express.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/100M.ec.P2/100M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/100M.ec.P2/100M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 100M.ec.score.express.P2 -t 40

	TRANSRATE ASSEMBLY SCORE: 0.3648

---

Filter 100M to score > .5

in `/mouse/feeding/100M.ec.P2/high_score_filt`

	awk -F "," '.5>$17{next}1' 100M.ec.P2_Trinity.fasta_contigs.csv  | awk -F "," '{print $1}' | sed '1,1d' | split -l 8000

	for i in `cat xaa`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in `cat xab`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in `cat xac`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in `cat xad`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in `cat xae`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in `cat xaf`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in `cat xag`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in `cat xah`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in `cat xai`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in `cat xaj`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in `cat xak`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in `cat xal`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in `cat xam`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in `cat xan`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in `cat xao`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in `cat xap`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in `cat xaq`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in `cat xar`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp18.fa; done &
	for i in `cat xas`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp19.fa; done &
	for i in `cat xat`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp20.fa; done &
	for i in `cat xau`; do grep -A1 --max-count=1 -w $i 100M.ec.P2.Trinity.fasta >> temp21.fa; done &

	cat temp* > 100M.ec.P2.highscore.Trinity.fasta
	rm temp* x*

	transrate -a 100M.ec.P2.highscore.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/100M.ec.P2/100M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/100M.ec.P2/100M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 100M.ec.highscore.P2 -t 40

	TRANSRATE ASSEMBLY SCORE: 0.366


20M Filter based on contig score
--

for `20M.ec.P2` in `/mouse/feeding/20M.ec.P2/score_filt`

	awk -F "," '.3>$17{next}1' 20M.ec.P2_Trinity.fasta_contigs.csv | awk -F "," '{print $17}'  | sed '1,1d' | split -l 4000


	same filtering as above..


	cat temp* > 20M.ec.P2.contig_score.Trinity.fasta
	
	transrate -a 20M.ec.P2.contig_score.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/20M.ec.P2/20M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/20M.ec.P2/20M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 20M.ec.contig_score.P2_right -t 20

	**SCORE IS STILL .43**
	
20M Filter based on contig score and low expression
--

for `20M.ec.P2` in `/mouse/feeding/20M.ec.P2/score_express_filt`

	awk -F "," '.3>$17{next}1' 20M.ec.P2_Trinity.fasta_contigs.csv | awk -F "," '1>$22{next}1'  | awk -F "," '{print $1}' | sed '1,1d' | split -l 4000
	

	for i in $(cat xaa); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp1.fa; done &
	for i in $(cat xab); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp2.fa; done &
	for i in $(cat xac); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp3.fa; done &
	for i in $(cat xad); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp4.fa; done &
	for i in $(cat xae); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp5.fa; done &
	for i in $(cat xaf); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp6.fa; done &
	for i in $(cat xag); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp7.fa; done &
	for i in $(cat xah); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp8.fa; done &
	for i in $(cat xai); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp9.fa; done &
	for i in $(cat xaj); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp10.fa; done &
	for i in $(cat xak); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp11.fa; done &
	for i in $(cat xal); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp12.fa; done &
	for i in $(cat xam); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp13.fa; done &
	for i in $(cat xan); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp14.fa; done &
	for i in $(cat xao); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp15.fa; done &
	for i in $(cat xap); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp16.fa; done &
	for i in $(cat xaq); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp17.fa; done &
	for i in $(cat xar); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp18.fa; done &
	for i in $(cat xas); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp19.fa; done &
	for i in $(cat xat); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp20.fa; done &
	for i in $(cat xau); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp21.fa; done &
	for i in $(cat xav); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp22.fa; done &
	for i in $(cat xaw); do grep -A1 --max-count=1 -w $i 20M.ec.P2.Trinity.fasta >> temp23.fa; done &


	cat temp* > 20M.ec.P2.score.express.Trinity.fasta


	transrate -a 20M.ec.P2.score.express.Trinity.fasta -r ../../Mus_musculus.GRCm38.pep.all.fa \
	-l /mouse/feeding/20M.ec.P2/20M_corrk19.1.corrected.fastq.gz.PwU.qtrim.fq \
	-i /mouse/feeding/20M.ec.P2/20M_corrk19.2.corrected.fastq.gz.PwU.qtrim.fq \
	-o 20M.ec.express.score.P2 -t 40


try to use Transrate with full read dataset
--

in `/mouse/feeding`

	lighter -t 24 -r SRR797058_1.fastq.gz  -r SRR797058_1.fastq.gz -k 25 6000000000 .1
	
	java -Xmx50g -jar /share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/trimmomatic-0.32.jar PE \
	-threads 24 -baseout SRR797058.P2.fq \
	SRR797058_1.fastq.gz \
	SRR797058_2.fastq.gz  \
	ILLUMINACLIP:/share/trinityrnaseq-code/trinity-plugins/Trimmomatic-0.32/adapters/TruSeq2-PE.fa:2:30:10 \
	SLIDINGWINDOW:4:2 \
	LEADING:2 \
	TRAILING:2 \
	MINLEN:25











	

