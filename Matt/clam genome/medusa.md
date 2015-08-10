Medusa
--


in `/mouse/Mya/assemblies/long`

```
for i in `ls *fasta`;
do F=`basename $i .fasta`;
long_fasta.py $i long/$F.fa 1000;
done;
```


in `/mouse/Mya/medusa`

```
java -jar /share/medusa/medusa.jar -f ../assemblies/long/ \
-i ../assemblies/reference/oyster71-8.fa -o meduasa.mya.fasta -v | tee medusa.out

```

the ref genome is too big

```
1: PREPARING DATA
2,3: RUNNING mummer AND CREATING CLUSTERS
# reading input file "asm_Mya_v2_asm.ntref" of length 1406592337
# construct suffix tree for sequence of length 1406592337
# (maximum reference length is 536870908)
# (maximum query length is 4294967295)
# process 14065923 characters per dot
/usr/bin/mummer: suffix tree construction failed: textlen=1406592337 larger than maximal textlen=536870908
ERROR: mummer and/or mgaps returned non-zero
ERROR: Could not parse delta file, asm_Mya_v2_asm.delta
error no: 400
done.
```

Took only the condigs 10kb and greater

`long_fasta.py asm.fa asm.long.fa 10000`

```
java -jar /share/medusa/medusa.jar -f ../assemblies/long/ \
-i ../assemblies/reference/asm.long.fa -o meduasa.mya.fasta -v
```