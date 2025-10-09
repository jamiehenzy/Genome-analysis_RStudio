#### load libraries
```{r}
library(tidyverse)
library(ggplot2)
```

#### Use dat.long from "wrangling" exercise
```{r}
dat.long <- read.delim('../data/GSE183947_long_format.txt', header = T)
```
#### basic format for ggplot
#### ggplot(data, aes(x = variable, y = variable1)) +
####   geom_col()

#### 1. barplot
```{r}
dat.long %>%
  filter(gene == 'BRCA1') %>%
  ggplot(., aes(x = samples, y = FPKM, fill = tissue)) +
  geom_col()
```
#### 2. density
```{r}
dat.long %>%
  filter(gene == 'BRCA1') %>%
  ggplot(., aes(x = FPKM, fill = tissue)) +
  geom_density(alpha = 0.3)
```
#### 3. boxplot 
```{r}
dat.long %>%
  filter(gene == 'BRCA1') %>%
  ggplot(., aes(x = metastasis, y = FPKM)) +
  ####geom_boxplot()
  geom_violin()
```
#### 4. scatterplot
```{r}
dat.long %>%
  filter(gene == 'BRCA1' | gene == 'BRCA2') %>%
  spread(key = gene, value = FPKM) %>%
  ggplot(., aes(x = BRCA1, y = BRCA2, color = tissue)) +
  geom_point() +
  geom_smooth(method = 'lm', se = FALSE)
```
#### 5. heatmap
```{r}
genes.of.interest <- c('BRCA1', 'BRCA2', 'TP53', 'ALK', 'MYCN')

pdf("heatmap_save2.pdf", width = 10, height = 8)

dat.long %>%
  filter(gene %in% genes.of.interest) %>%
  ggplot(., aes(x = samples, y = gene, fill = FPKM)) +
  geom_tile() +
  scale_fill_gradient(low = 'white', high = 'red')

dev.off()

#### Save the data
```{r}
ggsave(p, filename = 'heatmap_save1.pdf', width = 10, height = 8)
```
