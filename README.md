# Critically judge your correlations! 

* Author: Chenxin Li
* Contact: lukli@ucdavis.edu 
* Twitter: [ChenxinLi2](https://twitter.com/ChenxinLi2)    

Ever wonder if you should publish a correlation?  
Moderate correlation coefficient and not sure if your correlation is real?   
Here is a function to help you critically judge your correlations.    
The random_line() function takes the correlates (x and y) and produce a scatter plot.   
On top of the scatter plot, it produces a best fit line and 5 "random" lines.     
These 5 random lines all meet at (mean_x, mean_y).     
Ask yourself, can you tell which line is the best fit line?    
If you can't, your correlation is probably not real. It might have a small p value, but it is nowhere near a strong correlation.   

```{r}
random_line <- function(x, y){  #takes scatter plot data as input: feed in x and y      
  
  randomize <- function(x, y){    
  b_random = runif(n = 1, min = min(y), max = max(y))    
  a_random = (mean(y) - b_random)/mean(x)   
  y_random = a_random*x + b_random    
} #this function produces a line w/ random slope & intercept that passes (mean(x), mean(y))      
  #the max and min y intercept is determined by the max and min y value      
  #since the line has to pass (mean(x), mean(y)), the slope = (mean(y) - y_intercept)/mean(x)    
  
  p = data.frame(   
    x = x,    
    y = y    
  ) %>%    
    cbind(replicate(randomize(x, y), n = 5) %>%  #produce 5 random lines      
            as.data.frame()) %>%    
  ggplot(aes(x = x, y = y)) +   
    geom_smooth(method = "lm", se = F, color = "skyblue3", size = 1.2, alpha = 0.8) + #your best fit line    
    geom_line(aes(y = V1), color = "skyblue3", size = 1.2, alpha = 0.8) +    
    geom_line(aes(y = V2), color = "skyblue3", size = 1.2, alpha = 0.8) +   
    geom_line(aes(y = V3), color = "skyblue3", size = 1.2, alpha = 0.8) +   
    geom_line(aes(y = V4), color = "skyblue3", size = 1.2, alpha = 0.8) +   
    geom_line(aes(y = V5), color = "skyblue3", size = 1.2, alpha = 0.8) +  #your 5 random lines   
    geom_point(size = 3, alpha = 0.8) + #the scattered points     
    theme_classic() + #just the theme, not critical     
    annotate(geom = "text",     
    label = paste("r = ", signif(cor(x, y), 3), sep = ""), #print the correlation coefficient    
    size = 5,    
    x = Inf,    
    y = if(cor(x, y) > 0){   #for r > 0, text appears at lower right corner    
       -Inf   
    } else {Inf},     #for r <= 0, text appeares at upper right corner     
    hjust = 1.1,    
    vjust = if(cor(x, y) > 0){    
       -1.1    #some fine adjustment on text justification     
    } else {1.1}      
    )    
  print(p)    
}      
```

# Try it out yourself
Can you tell which line is the best fit line?  
![Bad Example](https://github.com/cxli233/Critically_judge_your_correlations/blob/master/bad_example.png "normally distributed noise") 

Can you tell which line is the best fit line?  
![Good Example](https://github.com/cxli233/Critically_judge_your_correlations/blob/master/good_example.png "r = -0.9")  
