
#Introduction
# This project analyzes the GDP and educational world bank data of 190 countries. The two separate files are merged  based on the countries' short codes and sorted in order from lowest to highest GDP. The merged data set is further organized by high income non-OECD and high income OECD groups.

	1.
library(plyr)

site<- "https://d396qusza40orc.cloudfront.net/"
# You can find out which directory is working by running the getwd
getwd()
# Change your working directory by using setwd and specify the path to the desired folder.
setwd("C:/Users/fowino/Documents")
# download desired file
site<- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv"
download.file(site,destfile="./GDPDATA.csv")file
# read dataset into R
data <- read.csv("GDPDATA.csv", header = TRUE)

site<- "https://d396qusza40orc.cloudfront.net/"
getwd()
site<- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv "
download.file(site,destfile="./EDUCDATA.csv")
 data2 <- read.csv("EDUCDATA.csv", header = TRUE)
# Obtain the first several rows of a matrix or data frame using head
head(data2)
# specify in the merge() function that there are 2 specific locations through the arguments by.x and by.y  which give the columns to be matched
data3 <-merge(data,  data2, by.x="X", by.y="CountryCode")
# get the dimensions data 3 
dim(data3)# get the dimensions data 3
#224 IDs match.
       

     2.
# Use arrange from plyr package
data4<- arrange(data3, desc(Gross.domestic.product.2012))
# get the first 6 rows with column headings
head(data4)
# get the 13th country
data4[13,1]# get the 13th country
#13th country is Serbia
      3.

data5 <- data4[which(data4$Income.Group=="High income: nonOECD"),]
# now I want to select rows where Income.Group  = High income: nonOECD
# Assign data5 to those elements of data4 where the Income.Group  variable= High income: nonOECD
> data5
# as.numeric used to covert factors to  numeric vectors
mean(as.numeric(data4$Gross.domestic.product.2012))
#The mean GDP ranking of High Income:nonOECD is  58.64865

Data6<- arrange(data2, desc(Gross.domestic.product.2012))# arrange GDP in descending order
data6 <- data4[which(data4$Income.Group=="High income: OECD"),]
> head(data6)
mean(as.numeric(data5$Gross.domestic.product.2012))
#The mean GDP rank of High income: OECD is 110.0667 

      4.
library(ggplot2)
#telling ggplot what dataset to use.
 data7 <- ggplot(data3,
# aes()if both X and Y axes are fixed for all layers
aes(x = Income.Group,
y = X.3)) + 
 theme(legend.position="top",
              axis.text=element_text(size = 6))
# Adding scatterplot geom (data8) and smoothing geom (data7)but specifying the aesthetics inside the geoms.
 (data8 <- data7 + geom_point(aes(color = Income.Group),
                        alpha = 0.5,
                       size = 1.5,
+                     position = position_jitter(width = 0.25, height = 0)))
 


Data8 <- subset(data3, select=c("Gross.domestic.product.2012"))
> summary(data8)

Data9<- c(178, 1, 10, 100, 101)
> sort(data9)
[1]   1  10 100 101 178
> sort(data9, decreasing = TRUE)
[1] 178 101 100  10   1
> quantile(data9, probs = seq(0, 1, 0.25), na.rm = FALSE,
+ names = TRUE, type = 7)
  0%  25%  50%  75% 100% 
   1   10  100  101  178

  0%  	25%  	50%  	75%	100%
1	10	100	101	178





