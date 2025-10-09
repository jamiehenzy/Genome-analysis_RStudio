### Prior to starting an RStudio session, download GSE183947_fpkm.csv.gz from GEO database.
### Unzip the file and place somewhere in your home or scratch directory.

#### Install and load necessary packages
```{r}
BiocManager::install("GEOquery")
install.packages("tidyverse")
install.packages("dplyr")
```
#### Load libraries
```{r}
library(GEOquery)
library(tidyverse)
library(dplyr)
```
#### Read in counts data, downloaded from GEO database
```{r}
dat <- read.csv("course_datasets/GSE/GSE183947_fpkm.csv")
dim(dat)
```
#### Obtain metadata
```{r}
gse <- getGEO(GEO = 'GSE183947', GSEMatrix = TRUE)
```
#### Extract sample metadata, convert to dataframe
```{r}
metadata <- pData(phenoData(gse[[1]]))
```
#### For each step, check before continuing by using head(); assign to variable only after checked
#### + Select only the columns we want
#### + Rename columns 2 and 3
#### + Clean up descriptions in col 2 and 3
```{r}
metadata.modified <- select(metadata, c(1, 10, 11, 17)) %>%
  rename(tissue = characteristics_ch1) %>%
  rename(metastasis = characteristics_ch1.1) %>%
  mutate(tissue = gsub("tissue: ", "",  tissue)) %>%
  mutate(metastasis = gsub("metastasis: ", "",  metastasis))
```
#### Change format of the counts table (dat) from wide to long
 
```{r}
dat.long <- dat %>%
  rename(gene = X) %>%
  gather(key = 'samples', value = 'FPKM', -gene)
```
#### Join the dataframes (counts + metadata)
#### As above, first use head() to check, then assign to variable
```{r}
dat.long <- dat.long %>%
  left_join(., metadata.modified, by = c("samples" = "description"))
```
#### Save as a tab-delimited file
```{r}
write.table(metadata.modified, "course_datasets/GSE/GSE183947_long_format.txt", sep = "\t", row.names = FALSE, quote = FALSE)
```
