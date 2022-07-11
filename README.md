# GENERATING A PCA PLOT USING R PROGRAMMING LANGUAGE
setwd("C:/Users/user/OneDrive/Hackbio Stage 3")

getwd()

#install ggplot

library ("ggplot2")

metadata <- read.table("C:/Users/user/OneDrive/Hackbio Stage 3/sample list 1000 genomes on grch38.tsv.tsv", sep = "\t", header = TRUE)

head(metadata)

#pcal
#Read the eigenvec file
pcal <- read.table("C:/Users/user/OneDrive/Hackbio Stage 3/plink.eigenvec", sep =" ", header = F)

#Merge the data from pcal and metadata
merge_data <- merge(x= pcal,y=metadata,by.x = "V2", by.y="Sample.name", all = F)

library ("ggplot2")

#Plot with ggplot
ggplot(data = merge_data, aes(V3,V4,color = Superpopulation.code)) + geom_point(size = 2.5)+
 scale_color_brewer(palette = "Set1") + theme_classic() + labs (title = "PCA Plot 1")+
 xlab("Pca1") + ylab("pca2")+
 theme(plot.title = element_text(hjust = 0.5, face = "bold", size =30),
axis.title.x = element_text(face = "italic", color="green", size =14),
axis.title.y = element_text(face = "italic", color= "#33993d", size = 14))
 
 #annotate("text", label = "cluster 1", x = 0.01, y = -0.02, size = 8, color = "green")+
  #annotate("text", label = "cluster 2", x = -0.05, y = 0.02, size = 8, color = "blue")+
  #annotate("text", label = "cluster 3", x = 0.01, y = -0.08, size = 8, color = "black")+
  #annotate("text", label = "cluster 4", x = 0.00, y = -0.12, size = 8, color = "red")+

 ggsave("plot.png", width = 25, height = 20, units = "cm", limitsize = FALSE, path = "C:/Users/user/OneDrive/Hackbio Stage 3", dpi =300 )
        
