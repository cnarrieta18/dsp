[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

# QUESTION PROMPT
In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters _μ = 178 cm_ and _σ = 7.7 cm_ for men, and _μ = 163 cm_ and _σ= 7.3 cm_ for women. In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: `usescipy.stats.norm.cdf.`

__Step 1:__ Import necessary modules
    
    import thinkstat2
    import thinkplot
    import nsfg
    import brfss
    import scipy.stats
    
__Step 2:__ Load male height data into `heights_male` with null entries dropped

    df = brfss.ReadBrfss()
    heights_male = df[df.sex == 1].htm3.dropna()
    
__Step 3:__ Compute mean and standard deviation 

    mu = heights_male.mean()
    sigma = heights_male.std()
    print(mu,sigma)
    
Output: `178.06622109101272 7.723563454782443`

__Step 4:__ Create a normal distribution from calculated mean and std

    dist = scipy.stats.norm(loc=mu, scale=sigma)

__Step 5:__ Function for converting foot,inch to centimeters

    def conversion_ft_cm(height):
        cm = (height[0]*30.48) + (height[1]*2.54)
        return cm

__Step 6:__ Convert height range to centimeters

    height_1 = [5,10]
    height_2 = [6,1]
    height_range_ft = [height_1,height_2]
    height_range_cm = [conversion_ft_cm(x) for x in height_range_ft]
    height_range_cm

Output: `[177.8, 185.42]`

__Step 6:__ Calculate percentage of the U.S. male population in this range

    top = dist.cdf(height_range_cm[1]) 
    bottom = dist.cdf(height_range_cm[0])
    print(top,bottom,top-bottom)

Output: `0.829482582277679 0.48625170584113814 0.3432308764365409`

## Conclusion
34% of the U.S. male population is within the height range [5'10",6'1]
