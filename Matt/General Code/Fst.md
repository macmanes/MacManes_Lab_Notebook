plotting relationship between Fst and Nmt

	nm=c(0,1,2,3,4,5,6)
	plot(1/(1+(4*nm)), type='l', lwd=4, frame.plot='F', ylab=parse(text='F[st]'), xlab=parse(text='Nm[T]'), ylim=c(0:1))