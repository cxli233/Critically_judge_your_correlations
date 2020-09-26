# Critically judge your correlations! 

* Author: Chenxin Li
* Contact: lukli@ucdavis.edu 
* Twitter: ChenxinLi2 

Ever wonder if you should publish a correlation?

Moderate correlation coefficient and not sure if your correlation is real?

Here is a function to help you critically judge your correlations. 

The random_line() function takes the correlates (x and y) and produce a scatter plot.

On top of the scatter plot, it produces a best fit line and 5 "random" lines.

These 5 random lines all meet at (mean_x, mean_y). 

Ask yourself, can you tell which line is the best fit line?

If you can't, your correlation is probably not real. It might have a small p value, but it is nowhere near a strong correlation. 

# Try it out yourself
Can you tell which line is the best fit line?  
![Bad Example](https://github.com/cxli233/Critically_judge_your_correlations/blob/master/bad_example.png) 

Can you tell which line is the best fit line?  
![Good Example](https://github.com/cxli233/Critically_judge_your_correlations/blob/master/good_example.png) 
