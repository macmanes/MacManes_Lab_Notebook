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