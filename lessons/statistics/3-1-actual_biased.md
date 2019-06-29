[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

# QUESTION PROMPT
Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable `numkdhh` to construct the _actual distribution_ for the number of children under 18 in the respondents' households.

Now compute the _biased distribution_ we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means.

__Step 1:__ Import necessary modules
    
    import thinkstat2
    import nsfg
    import probability

__Step 2:__ Load data into `resp` variable

    resp = nsfg.ReadFemResp()
    
__Step 3:__ Compute Probability Mass Function (PMF) for series from column __numkdhh__ and label as _actual_.  PMF is the calculation of the probabilities of each instance, normalized within the collection of all included instances. 

    pmf = thinkstats2.Pmf(resp.numkdhh, label = 'actual')
        
Output: `Pmf({0: 0.466178202276593, 1: 0.21405207379301322, 2: 0.19625801386889966, 3: 0.08713855815779145, 4:       0.025644380478869556, 5: 0.01072877142483318}, 'actual')`

__Step 4:__ Compute the biased PMF from the _actual_ `pmf`.  Biased PMF is when the larger subsets are observed and result in overrepresentation  

    biased_pmf = probability.BiasPmf(pmf,'observed')
    
Output: `Pmf({0: 0.0, 1: 0.20899335717935616, 2: 0.38323965252938175, 3: 0.25523760858456823, 4: 0.10015329586101177, 5: 0.052376085845682166}, 'observed')`

__Step 5:__ Plot both actual pmf and biased pmf as a step function

    thinkplot.PrePlot(2)
    thinkplot.Pmfs([pmf, biased_pmf])
    thinkplot.Show(xlabel='number of children',ylabel='probabiltiy')    

Output: ![Alt text](https://drive.google.com/file/d/1GXoCqJzDVGbb2kk4tcPC4Q1Qjcj7NRsq/view?usp=sharing)

__Step 6:__ Plot both actual pmf and biased pmf as a step function

    print('Actual mean', pmf.Mean())
    print('Observed mean', biased_pmf.Mean())

Output: `Actual mean 1.024205155043831
         Observed mean 2.403679100664282`

## Conclusion
The biased pmf clearly underrepresents family with zero children, skewing the mean to roughly 2 kids per household
