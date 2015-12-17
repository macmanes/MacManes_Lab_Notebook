perfect:
```
bless55 <- c(9.4E+05/10E+06,1.9E+06/20E+06,4.89E+06/50E+06,9.92E+06/10E+07)
bless33 <- c(9.88E+05/10E+06,2.01E+06/20E+06,5.15E+06/50E+06,1.04E+07/10E+07)
lighter <- c(9.74E+05/10E+06,1.88E+06/20E+06,4.64E+06/50E+06,9.35E+06/10E+07)
seecer <- c(1.07E+06/10E+06,2.15E+06/20E+06,5.43E+06/50E+06,1.09E+07/10E+07)
bfc33 <- c(1.07E+06/10E+06,2.11E+06/20E+06,5.12E+06/50E+06,9.88E+06/10E+07)
bfc55 <- c(1.02E+06/10E+06,2.03E+06/20E+06,5.02E+06/50E+06,9.81E+06/10E+07)


plot(bless33, ylim=c(.08,.12), xaxt="n", frame.plot=F, ylab='% reads made perfect', col='red', lwd=3, pch=1, xlab='Number of reads')
points(bless55,col='blue', lwd=3,pch=1)
points(lighter,col='green', lwd=3,pch=5)
points(seecer,col='orange', lwd=3,pch=6)
points(bfc33,col='brown', lwd=3,,pch=4)
points(bfc55,col='brown', lwd=3,pch=4)


axis(1, at=c(1,2,3,4), labels=c("10M", "20M", "50M", "100M"))
```
gain perf:
```
bless55 <- c(1.26E+06/10E+06,2.7E+06/20E+06,6.94E+06/50E+06,1.36E+07/10E+07)
bless33 <- c(1.05E+06/10E+06,2.24E+06/20E+06,5.98E+06/50E+06,1.23E+07/10E+07)
lighter <- c(1.39E+06/10E+06,2.53E+06/20E+06,6.06E+06/50E+06,1.24E+07/10E+07)
seecer <- c(1.54E+06/10E+06,3.12E+06/20E+06,7.95E+06/50E+06,1.61E+07/10E+07)
bfc33 <- c(1.78E+06/10E+06,3.44E+06/20E+06,7.93E+06/50E+06,1.45E+07/10E+07)
bfc55 <- c(1.48E+06/10E+06,2.96E+06/20E+06,7.18E+06/50E+06,1.37E+07/10E+07)


plot(bless33, ylim=c(.08,.20), xaxt="n", frame.plot=F, ylab='% Performance Gain', col='red', lwd=3, pch=1, xlab='Number of reads')
points(bless55,col='blue', lwd=3,pch=1)
points(lighter,col='green', lwd=3,pch=5)
points(seecer,col='orange', lwd=3,pch=6)
points(bfc33,col='brown', lwd=3,,pch=4)
points(bfc55,col='brown', lwd=3,pch=4)


axis(1, at=c(1,2,3,4), labels=c("10M", "20M", "50M", "100M"))

legend(1, .2, pch=c(1,4,5,6), col=c('red','brown','green','orange'), legend=c('bless','bfc', 'lighter', 'seecer'), bty='n', horiz = TRUE, seg.len=5)

