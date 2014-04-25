simulating drift in R
    
    N = 10 # number of diploid individuals
    N.chrom = 2*N # number of chromosomes
    p = .5; q = 1-p
    N.gen = 100 # number of generations
    N.sim = 10 # number of simulations
    
    
    # Simulation
    X = array(0, dim=c(N.gen,N.sim))
    X[1,] = rep(N.chrom*p,N.sim) # initialize number of A1 alleles in first generation
    for(j in 1:N.sim){
    for(i in 2:N.gen){
        X[i,j] = rbinom(1,N.chrom,prob=X[i-1,j]/N.chrom)
        } 
    }
    X = data.frame(X/N.chrom)
    
    
    # Reshape data and plot the 5 simulations
    sim_data <- melt(X)
    p1 <- ggplot(sim_data, aes(x = rep(c(1:N.gen), N.sim), y = value, colour = variable, legend.position="none")) + geom_line() + 
    theme_bw() + labs(x = "Generations", y = "Allele Frequency") +
    labs(title = "n=10") +
    theme(plot.title = element_text(size = rel(1.5))) +
    theme(legend.position = "null")
    
    N = 50 # number of diploid individuals
    N.chrom = 2*N # number of chromosomes
    p = .5; q = 1-p
    N.gen = 100 # number of generations
    N.sim = 10 # number of simulations
    
    
    # Simulation
    X = array(0, dim=c(N.gen,N.sim))
    X[1,] = rep(N.chrom*p,N.sim) # initialize number of A1 alleles in first generation
    for(j in 1:N.sim){
    for(i in 2:N.gen){
        X[i,j] = rbinom(1,N.chrom,prob=X[i-1,j]/N.chrom)
        } 
    }
    X = data.frame(X/N.chrom)
    
    
    # Reshape data and plot the 5 simulations
    sim_data <- melt(X)
    p2 <- ggplot(sim_data, aes(x = rep(c(1:N.gen), N.sim), y = value, colour = variable, legend.position="none")) + geom_line() + 
    theme_bw() + labs(x = "Generations", y = "Allele Frequency") +
    labs(title = "n=50") +
    theme(plot.title = element_text(size = rel(1.5))) +
    theme(legend.position = "null")
    
    N = 100 # number of diploid individuals
    N.chrom = 2*N # number of chromosomes
    p = .5; q = 1-p
    N.gen = 100 # number of generations
    N.sim = 10 # number of simulations
    
    
    # Simulation
    X = array(0, dim=c(N.gen,N.sim))
    X[1,] = rep(N.chrom*p,N.sim) # initialize number of A1 alleles in first generation
    for(j in 1:N.sim){
    for(i in 2:N.gen){
        X[i,j] = rbinom(1,N.chrom,prob=X[i-1,j]/N.chrom)
        } 
    }
    X = data.frame(X/N.chrom)
    
    
    # Reshape data and plot the 5 simulations
    sim_data <- melt(X)
    p3 <- ggplot(sim_data, aes(x = rep(c(1:N.gen), N.sim), y = value, colour = variable, legend.position="none")) + geom_line() + 
    theme_bw() + labs(x = "Generations", y = "Allele Frequency") +
    labs(title = "n=100") +
    theme(plot.title = element_text(size = rel(1.5))) +
    theme(legend.position = "null")
    
    N = 1000 # number of diploid individuals
    N.chrom = 2*N # number of chromosomes
    p = .5; q = 1-p
    N.gen = 100 # number of generations
    N.sim = 10 # number of simulations
    
    
    # Simulation
    X = array(0, dim=c(N.gen,N.sim))
    X[1,] = rep(N.chrom*p,N.sim) # initialize number of A1 alleles in first generation
    for(j in 1:N.sim){
    for(i in 2:N.gen){
        X[i,j] = rbinom(1,N.chrom,prob=X[i-1,j]/N.chrom)
        } 
    }
    X = data.frame(X/N.chrom)
    
    
    # Reshape data and plot the 5 simulations
    sim_data <- melt(X)
    p4 <- ggplot(sim_data, aes(x = rep(c(1:N.gen), N.sim), y = value, colour = variable, legend.position="none")) + geom_line() + 
    theme_bw() + labs(x = "Generations", y = "Allele Frequency") +
    labs(title = "n=1000") +
    theme(plot.title = element_text(size = rel(1.5))) +
    theme(legend.position = "null")
    
    grid.arrange(p1,p2, p3, p4)
    

time to fixation:

	n=1000
	p=p=c(0, 0.1,0.2,.3, .4, .5, .6, .7, .8, .9, 1)
	plot(-4*(n)*(p*log(p) + ((1-p)*log(1-p))), type='l', frame.plot='F', lwd=8, col='red', xaxt='n', xlab='Initial Allele Frequency', ylab='Expected time to fixation or loss (Number Generations)', ylim=c(0,3000))
	axis(1, at=c(1,2,3,4,5,6,7,8,9,10,11), labels=c("0", ".1", '.2', '.3', ".4", '.5', '.6', '.7', '.8', '.9', '1'))
	n=100
	lines(-4*(n)*(p*log(p) + ((1-p)*log(1-p))), type='l', lwd=8, col='green', xaxt='n')
	n=500
	lines(-4*(n)*(p*log(p) + ((1-p)*log(1-p))), type='l', lwd=8, col='blue', xaxt='n')
