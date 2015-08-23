MYA khmer normalize
--

in `/mouse/Mya/nygc_reads/pe`

```
interleave-reads.py clam500.P2_1P.fq.gz clam500.P2_2P.fq.gz | normalize-by-median.py --max-memory-usage 4e10 -C 30 --gzip -o normalize.fq.gz -


interleave-reads.py clam300.P2_1P.fq.gz clam300.P2_2P.fq.gz | normalize-by-median.py --max-memory-usage 4e10 -C 30 --gzip -o normalize.clam300.P2.fq.gz -

```

stream

```
interleave-reads.py clam500.P2_1P.fq.gz clam500.P2_2P.fq.gz \
| normalize-by-median.py -s test.kh --max-memory-usage 8e10 -C 30 -o -  - \
| filter-abund.py --gzip --threads 10 --cutoff 2 -o 2pass.fq  test.kh -

```


```
interleave-reads.py file_1P.fq.gz file.2P.fq.gz \
| normalize-by-median.py -s test.kh --max-memory-usage 8e10 -C 30 -o -  - \
| filter-abund.py --gzip --threads 10 --cutoff 2 -o 2pass.fq  test.kh -

```

this actually works!
--


```
interleave-reads.py clam300.P2_1P.fq.gz clam300.P2_2P.fq.gz | normalize-by-median.py --max-memory-usage 8e10 -C 30 -o -  - | trim-low-abund.py -M 8e10 -o 2pass.fq.gz --cutoff 2 --gzip -


#and

interleave-reads.py clam500.P2_1P.fq.gz clam500.P2_2P.fq.gz | normalize-by-median.py --max-memory-usage 8e10 -C 30 -o -  - | trim-low-abund.py -M 8e10 -o 2pass.fq.gz --cutoff 2 --gzip -

```



