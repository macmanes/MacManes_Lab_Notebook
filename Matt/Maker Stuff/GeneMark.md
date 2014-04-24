GeneMark Stuff
--------------------------------------------------------

As per the author - Before running GenMark, it is important to repeat mask your sequences - I am still not quite sure if GeneMark wants masked sequences are lower-case, or N's/

	nohup ~/maker/exe/RepeatMasker/RepeatMasker -pa 6 -nolow  \
	-species mouse ../pero.genes.fa

The command for running GeneMark is:

    /home/macmanes/gm_es_bp_linux64_v2.3e/gmes/gm_es.pl --min_contig 20000 \
    ../pero.genes.fa --BP OFF

There are a few other settings that you might consider setting.. 

> --min_contig [number]
>
> Short contigs, which are frequently found in draft assemblies,
> may introduce significant noise in self-training procedure.
> All contigs shorter then "min_contig" are excluded from training procedure.

GeneMark will create many folders in working directory. The final file that you need to provide to MAKER is in `mod/es.mod`.


---
15 Apr 14
---

Repeat masker finished, I invoked genemark like this:

	/home/macmanes/gm_es_bp_linux64_v2.3e/gmes/gm_es.pl --min_contig 20000 ../pero.genes.fa.masked --BP OFF