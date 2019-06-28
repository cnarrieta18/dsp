[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

# QUESTION PROMPT
Using the variable __`totalwgt_lb`__,investigate whether first babies are lighter or heavier than others. Compute __Cohen’s d__ to quantify the difference between the groups. How does it compare to the difference inpregnancy length?

__Step 1:__ Import necessary modules
    
    import thinkstat2
    import nsfg

__Step 2:__ Load data while filtering for only LIVE BIRTH (outcome=1)

    live_preg = nsfg.ReadFemPreg()[preg.outcome == 1]
    
__Step 3:__ Categorize into first born and non-first born

    first_born = live_preg[live_preg.birthord == 1]
    non_first_born live_preg[live_preg.birthord != 1]

__Step 4:__ Calculate the mean for each category

    print('total weight in lbs, 
           first born mean: {} 
           non-first born mean: {}'
           .format(first_born.totalwgt_lb.mean(),
                   non_first_born.totalwgt_lb.mean()
                   )
           )

Output: `total weight in lbs, first born mean: 7.201094430437772 non-first born mean: 7.325855614973262`

__Step 5:__ Calculate Cohen's d

    d_totalwgt_lb = thinkstats2.CohenEffectSize(first_born.totalwgt_lb,non_first_born.totalwgt_lb)
    print("Cohen's d: ",d_totalwgt_lb)
    
Output: `Cohen's d:  -0.088672927072602`

## Conclusion
Average first born weight is slightly lighter than non-first born.  The difference in means is 0.09, which is not significant.
