mouse physiology
--

	water <- read.csv("Desert_Animal_Water.csv)
    boxplot(water$consumption_per_weight ~ water$animal, col=c('sienna4','sienna4','dodgerblue','dodgerblue','dodgerblue','grey','grey'), xlab='Individual ID', ylab='g water /g weight /day', frame.plot=F)
    
    abline(h=0.1065829, lwd=3)
    

<a href="http://imgur.com/CdqBJw2"><img src="http://i.imgur.com/CdqBJw2.png"></a>


	genus <- read.delim("~/Box Sync/Desert_Animal_Stuff/R_desert_animal_water/pero_genus_water_consumption.txt")

	colfunc <- colorRampPalette(c("sienna4", "dodgerblue"))
	colfunc(7)

	barplot(sort(genus$water) , lwd=1, pch=1, col=c("#8B4726", "#78534A", "#665F6E", "#546B92", "#4277B6", "#3083DA", "#1E90FF"), ylab='g water/g weight/day')

	abline(h=mean(genus$water), lwd=3)


<a href="http://imgur.com/vkwZzpe"><img src="http://i.imgur.com/vkwZzpe.png" title="source: imgur.com" /></a>



	boxplot(water$consumption_per_weight ~ water$animal, col=c("#8B4726", "#78534A","#1E90FF", "#3083DA", "#4277B6", "#546B92", "#665F6E"), xlab='Individual ID', ylab='g water /g weight /day', frame.plot=F)
	abline(h=0.1065829, lwd=3)

<a href="http://imgur.com/mD8WupX"><img src="http://i.imgur.com/mD8WupX.png" title="source: imgur.com" /></a>

	elytes <- read.csv("~/Box Sync/Desert_Animal_Stuff/R_desert_animal_water/Desert_Lab_Animals_elytes.csv", header=TRUE)
	
    par(mfrow=c(1,6))
    boxplot(elytes$Alt ~ elytes$water, frame.plot=F, ylim=c(0,300), xlab='Alt', cex.lab=2, col=c('sienna4', 'dodgerblue'))
    boxplot(elytes$BUN ~ elytes$water, axes=F, frame.plot=F, ylim=c(0,300), xlab='BUN', cex.lab=2, col=c('sienna4', 'dodgerblue'))
    
    boxplot(elytes$Na ~ elytes$water, axes=T, frame.plot=F, ylim=c(75,190), xlab='Na',  cex.lab=2, col=c('sienna4', 'dodgerblue'))
    boxplot(elytes$Cl ~ elytes$water, axes=F, frame.plot=F, ylim=c(75,190), xlab='Cl',  cex.lab=2, col=c('sienna4', 'dodgerblue'))
    
    boxplot(elytes$Cr ~ elytes$water, axes=T, frame.plot=F, ylim=c(0,1), xlab='Cr',  cex.lab=2, col=c('sienna4', 'dodgerblue'))
    boxplot(elytes$TCO2 ~ elytes$water, axes=T, frame.plot=F, ylim=c(0,25), xlab='Bicarb',  cex.lab=2, col=c('sienna4', 'dodgerblue'))


__t tests:__

	t.test(elytes$TCO2 ~ elytes$water)
	....

<a href="http://imgur.com/NdqPEAZ"><img src="http://i.imgur.com/NdqPEAZ.png" title="source: imgur.com" /></a>
