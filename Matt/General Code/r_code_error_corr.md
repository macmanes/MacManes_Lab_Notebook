Plots for feeding paper
--

gain perf MUS:
```

reads <- c(1,2,5,10,20,40,60,80,100)

bless33 <- c(1.07E+05/1E+06,2.32E+05/2E+06,6.32E+05/5E+06,1.27E+06/10E+06,2.84E+06/20E+06,5.16E+06/40E+06,7.84E+06/60E+06,1.02E+07/80E+06,1.37E+07/100E+06)
bless55 <- c(8.15E+04/1E+06,1.86E+05/2E+06,4.88E+05/5E+06,1.07E+06/10E+06,2.29E+06/20E+06,4.79E+06/40E+06,7.37E+06/60E+06,1.01E+07/80E+06,1.29E+07/100E+06)
lighter <- c(2.88E+04/1E+06,8.00E+00/2E+06,7.54E+05/5E+06,1.40E+06/10E+06,2.54E+06/20E+06,5.18E+06/40E+06,7.81E+06/60E+06,1.06E+07/80E+06,1.33E+07/100E+06)
sga33 <- c(2.02E+04/1E+06,3.92E+04/2E+06,8.28E+04/5E+06,1.43E+05/10E+06,2.99E+05/20E+06,3.57E+05/40E+06,4.91E+05/60E+06,4.11E+05/80E+06,6.39E+05/100E+06)
sga55 <- c(1.52E+04/1E+06,3.21E+04/2E+06,7.28E+04/5E+06,1.29E+05/10E+06,2.18E+05/20E+06,3.19E+05/40E+06,4.61E+05/60E+06,3.99E+05/80E+06,8.74E+05/100E+06)
seecer <- c(1.37E+05/1E+06,2.93E+05/2E+06,7.51E+05/5E+06,1.53E+06/10E+06,3.12E+06/20E+06,6.33E+06/40E+06,9.57E+06/60E+06,1.28E+07/80E+06,1.61E+07/100E+06)
bfc33 <- c(1.63E+05/1E+06,3.47E+05/2E+06,9.00E+05/5E+06,1.79E+06/10E+06,3.45E+06/20E+06,6.49E+06/40E+06,9.28E+06/60E+06,1.19E+07/80E+06,1.44E+07/100E+06)
bfc55 <- c(1.27E+05/1E+06,2.73E+05/2E+06,7.27E+05/5E+06,1.49E+06/10E+06,2.97E+06/20E+06,5.81E+06/40E+06,8.52E+06/60E+06,1.11E+07/80E+06,1.37E+07/100E+06)
rcorr33 <- c(1.57E+05/1E+06,-2.31E+05/2E+06,-7.17E+05/5E+06,-1.40E+06/10E+06,-2.32E+06/20E+06,-4.69E+06/40E+06,-6.97E+06/60E+06,-9.29E+06/80E+06,-1.43E+07/100E+06)
rcorr55 <- c(-3.04E+03/1E+06,-2.45E+05/2E+06,-2.58E+05/5E+06,-5.19E+05/10E+06,-2.47E+06/20E+06,-5.00E+06/40E+06,-7.45E+06/60E+06,-9.93E+06/80E+06,-1.51E+07/100E+06)


plot(bless33 ~ reads, ylim=c(-.20,.20), xaxt="n",xlim=c(0,100), frame.plot=F, ylab='Percent Performance Gain', col='brown', lwd=3, pch=1, xlab='Number of reads')

points(bless55 ~ reads,col='brown', lwd=3,pch=2)
points(lighter ~ reads,col='green', lwd=3,pch=1)
lines(seecer ~ reads,col='blue', lwd=5,pch=2)
lines(bfc33 ~ reads,col='red', lwd=5,pch=1)
points(seecer ~ reads,col='blue', lwd=5,pch=2)
points(bfc33 ~ reads,col='red', lwd=5,,pch=1)
points(bfc55 ~ reads,col='red', lwd=3,pch=2)
points(rcorr33 ~ reads,col='grey', lwd=3,pch=1)
points(rcorr55 ~ reads,col='grey', lwd=3,pch=2)
points(sga33 ~ reads,col='hot pink', lwd=3,pch=1)
points(sga55 ~ reads,col='hot pink', lwd=3,pch=2)



axis(1, at=c(1,2,5,10,20,40,60,80,100), labels=c("1M","2M","5M","10M", "20M", "40M","60M","80M", "100M"))

legend(1, -.17, lty=c(1,1,1,1,1), lwd=5, col=c('blue','red', 'green', 'brown', 'grey', 'hot pink'), legend=c('SEECER','bfc', 'Lighter', 'Bless', 'Rcorrector', 'SGA'), bty='n', horiz = TRUE, seg.len=1)

```

BUSCO

```

reads <- c(1,2,5,10,20,40,60,80,100)

complete <- c(.17, .33, .56, .69, .77, .82, .83, .85, .85)
duplicates <- c(.014, .04, .11, .20, .30, .37, .39, .41, .41)

plot(complete ~ reads, ylim=c(0,1), xlim=c(0,100), xaxt="n", frame.plot=F, ylab='Percent', col='red', lwd=3, xlab='Number of reads')
lines(complete ~ reads,col='red', lwd=1)
lines(duplicates ~ reads,col='blue', lwd=1)
points(duplicates ~ reads,col='blue', lwd=1)

axis(1, at=c(1,2,5,10,20,40,60,80,100), labels=c("1M","2M","5M","10M", "20M", "40M","60M","80M", "100M"))

legend(1, .9, lty=c(1,1), lwd=5, col=c('blue','red'), legend=c('Percent Duplicates','Percent Complete'), bty='n', horiz = TRUE, seg.len=1)

```

TRANSRATE

```
score <- c(0.20833, 0.24155, 0.25973, 0.26067, 0.26593, 0.28101, 0.28886, 0.29768, 0.30088)
corr <- c(0.21304, 0.24969, 0.27503, 0.27558, 0.27877, 0.28885, 0.30437, 0.31259, 0.31786)

reads <- c(1,2,5,10,20,40,60,80,100)
plot(score ~ reads, ylim=c(.2,.35), xlim=c(0,100), xaxt="n", frame.plot=F, ylab='Transrate Score', col='red', lwd=3, xlab='Number of reads')
lines(score ~ reads,col='red', lwd=1)
lines(corr ~ reads,col='blue', lwd=1)
points(corr ~ reads,col='blue', lwd=3)
axis(1, at=c(1,2,5,10,20,40,60,80,100), labels=c("1M","2M","5M","10M", "20M", "40M","60M","80M", "100M"))
legend(1, .32, lty=c(1,1), lwd=5, col=c('blue','red'), legend=c('Corrected reads','Raw reads'), bty='n', horiz = TRUE, seg.len=1)
```

![alt](/Users/macmanes/Box\ Sync/error_corr_reads/transrate_corr.jpeg "test")
