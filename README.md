# Week_Xiaoyuan
## Report for anscombe_quartet.rds dataset
anscombe_quartet <-  readRDS("../data/anscombe_quartet.rds")

### let's explore the dataset 
str(anscombe_quartet)

### what does the function str() do? 
Display the structure of the dataset

### let's check some summary statistics:

result <- anscombe_quartet %>% 
  group_by(dataset) %>% 
  summarise(
    mean_x    = mean(x),
    mean_y    = mean(y),
    min_x     = min(x), 
    min_y     = min(y),
    max_x     = max(x),
    max_y     = max(y),
    crrltn    = cor(x, y)
  )
result

### what do the summary statistics tell us about the different datasets? 
similar summary statistics (mean, min and max, correlation) for both x and y

### let's plot the data with ggplot:

require(ggplot2)

ggplot(anscombe_quartet, aes(x=x,y=y)) +
  geom_point() + 
  geom_smooth(method = "lm",formula = "y ~ x") +
  facet_wrap(~dataset)

### save the plot

ggsave("../plot/anscombe_quartet.png", width = 20, height = 20, units = "cm")


### conclusion
what do the plots tell us about the different datasets? 
they have notably different distributions and scatterplots

describe the relationship between x and y in the different datasets.
dataset_1: it shows a relatively strong positive linear relationship between x and y.
dataset_2: y has a sooth curved relation with x.
dataset_3: despite having an outlier, it also shows a strong positive linear relationship between x and y.
dataset_4: Most of the points are clustered on x = 8, and an outlier is located at x = 19, which affects the regression pattern.

would linear regression be an appropriate statistical model to analyse the x-y relationship in each dataset?
No. Although the datasets are completely different, they show same regression coefficient and similar strong positive linear relationships.

what conclusions can you draw for the plots and summary statistics? The fact that the summary statistics for the x and y variables in datasets are very similar does not mean that their distributions and scatterplots are also very similar. It is important to visualize data for a comprehensive understanding.

## Report for datasaurus_dozen.rds dataset
### load in the datasaurus dataset
datasaurus_dozen <-  readRDS("../data/datasaurus_dozen.rds")

### explore the dataset 
str(datasaurus_dozen)

### how many rows and columns does the datasaurus_dozen file have? 
there are 1426 rows and 3 columns in the dataset

### plot the dataset 
#### calculate the correlations and summary statistics for x and y in all datasets: 
result_2 <- datasaurus_dozen %>% 
  summarise(
    mean_x    = mean(x),
    mean_y    = mean(y),
    min_x     = min(x),
    min_y     = min(y),
    max_x     = max(x),
    max_y     = max(y),
    crrltn    = cor(x, y)
  )
result_2

ggplot(datasaurus_dozen, aes(x=x,y=y)) +
  geom_point() + 
  geom_smooth(method = "lm",formula = "y ~ x") +
  ggtitle("Datasaurus Dozen Scatterplot") +
  labs(x = "X-axis", y = "Y-axis") 
ggsave("../plot/datasaurus_dozen.png", width = 20, height = 20, units = "cm")


### r plot of each dataset
#### Plot the relationships between x and y in each dataset including the line of best fit.
#### save the plot 

ggplot(datasaurus_dozen, aes(x=x,y=y)) +
  geom_point() + 
  geom_smooth(method = "lm",formula = "y ~ x") +
  ggtitle("Datasaurus Dozen Scatterplot of different datasets") +
  labs(x = "X-axis", y = "Y-axis") +
  facet_wrap(~dataset)
ggsave("../plot/datasaurus_dozen_datasets.png", width = 20, height = 20, units = "cm")


### r conclusion for question 2
what conclusions can you draw for the plots and summary statistics? 
For the whole dataset, data points are randomly dispersed in a circle shape with a diameter equals to 100.
For different datasets, they have very similar mean, max, min and correlation but different data distributions.
Conclusion: The fact that the summary statistics for the x and y variables in datasets are very similar does not mean that their distributions and scatterplots are also very similar. It is important to visualize data for a comprehensive understanding.
```
