---
title: "HR data to predict employee turnover"
author: "Kate and gang"
output:
  html_document:
    css: AnalyticsStyles/default.css
    theme: paper
    toc: yes
    toc_float:
      collapsed: no
      smooth_scroll: yes
  pdf_document:
    includes:
      in_header: AnalyticsStyles/default.sty
always_allow_html: yes
---



<hr>\clearpage

# The Business Questions

To analyse characteristics of employees to help managers predict the possibility of a particular employee leaving the company

The data is based on data we obtained from [Kaggle ](https://www.kaggle.com/ludobenistant/hr-analytics).

<hr>\clearpage

# The Process

1. *Part 1*: We clean the data to change categorical variables to dummy variables

2. *Part 2*: 

3. *Part 3*: 

Finally, we will use the results of this analysis to make business decisions on predicting the profile of employees that is at highest risk of leaving the company.




<hr>\clearpage

# The Data

First we load the data to use (see the raw .Rmd file to change the data file as needed):


```r
# Please ENTER the name of the file with the data used. The file should be a
# .csv with one row per observation (e.g. person) and one column per
# attribute. Do not add .csv at the end, make sure the data are numeric.
datafile_name = "data/HR_comma_sep.csv"

# Please enter the minimum number below which you would like not to print -
# this makes the readability of the tables easier. Default values are either
# 10e6 (to print everything) or 0.5. Try both to see the difference.
MIN_VALUE = 0.5

# Please enter the maximum number of observations to show in the report and
# slides.  DEFAULT is 10. If the number is large the report may be slow.
max_data_report = 10
```

We clean the data to create dummy variables for the Sales and Departments.
<img src="figure/unnamed-chunk-1-1.png" title="plot of chunk unnamed-chunk-1" alt="plot of chunk unnamed-chunk-1" style="display: block; margin: auto;" />



<hr>\clearpage

# Part 1: Key Customer Characteristics

We make a choice of the factor attributes and we use the Eigenvalue method to select the criterion.


```r
# Please ENTER then original raw attributes to use.  Please use numbers, not
# column names, e.g. c(1:5, 7, 8) uses columns 1,2,3,4,5,7,8
factor_attributes_used = c(1:6, 8, 11:20)

# Please ENTER the selection criterions for the factors to use.  Choices:
# 'eigenvalue', 'variance', 'manual'
factor_selectionciterion = "eigenvalue"

# Please ENTER the desired minumum variance explained (Only used in case
# 'variance' is the factor selection criterion used).
minimum_variance_explained = 65  # between 1 and 100

# Please ENTER the number of factors to use (Only used in case 'manual' is
# the factor selection criterion used).
manual_numb_factors_used = 5

# Please ENTER the rotation eventually used (e.g. 'none', 'varimax',
# 'quatimax', 'promax', 'oblimin', 'simplimax', and 'cluster' - see
# help(principal)). Default is 'varimax'
rotation_used = "varimax"
```



## Steps 1-2: Check the Data 

We check the data that it is all metric data:

<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Obs.01 </th>
   <th style="text-align:right;"> Obs.02 </th>
   <th style="text-align:right;"> Obs.03 </th>
   <th style="text-align:right;"> Obs.04 </th>
   <th style="text-align:right;"> Obs.05 </th>
   <th style="text-align:right;"> Obs.06 </th>
   <th style="text-align:right;"> Obs.07 </th>
   <th style="text-align:right;"> Obs.08 </th>
   <th style="text-align:right;"> Obs.09 </th>
   <th style="text-align:right;"> Obs.10 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> satisfaction_level </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.16%">-0.23</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 65.29%">1.36</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 73.98%">-1.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 92.50%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.95%">-0.27</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.50%">-0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.82</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.70</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.90%">-0.08</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> last_evaluation </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 93.37%">-0.95</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 37.86%">0.72</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 50.66%">0.82</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 68.33%">0.77</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 98.11%">-1.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.02%">0.26</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 40.86%">0.67</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 85.09%">1.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 89.20%">-0.95</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> number_project </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 34.00%">0.63</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.73</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 56.67%">0.63</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 93.01%">-1.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 91.89%">1.18</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 38.80%">0.63</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 40.92%">0.63</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 95.50%">-1.02</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> average_montly_hours </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 81.05%">-0.82</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 45.14%">0.89</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 63.67%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.00%">0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 78.21%">-0.79</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 81.65%">-0.89</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 52.79%">0.65</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 49.60%">0.84</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.04%">0.27</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.07</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> time_spend_company </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 88.63%">-0.90</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">2.17</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.25%">0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 88.63%">-0.90</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 82.52%">-0.90</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.43%">0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 65.54%">1.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 69.63%">1.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 84.70%">-0.90</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Work_accident </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.21%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.43%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.13%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.50%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.21%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.11%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.07%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.71%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.28%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.50%">-0.22</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> promotion_last_5years </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_accounting </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.71%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.00%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.28%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.26%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.94%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.20%">-0.25</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_hr </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.71%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.00%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.28%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.26%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.94%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.20%">-0.25</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_technical </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 49.79%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.00%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 32.77%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 45.00%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 49.79%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 46.70%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 40.98%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 31.60%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 33.19%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 47.80%">-0.49</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_support </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.11%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.43%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.52%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 40.00%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.11%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 41.46%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.56%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.51%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.88%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 42.40%">-0.43</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_management </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.53%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.86%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.88%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.50%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.53%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.86%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.64%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.63%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.97%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.10%">-0.16</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_IT </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 30.84%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.43%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.93%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.33%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 30.84%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.22%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.23%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.31%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.15%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.80%">-0.29</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_product_mng </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.11%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.29%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.22%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.17%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.11%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.85%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.54%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.74%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.39%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.30%">-0.24</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_marketing </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.71%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.00%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.05%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.28%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.26%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.94%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.20%">-0.25</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_RandD </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.37%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.14%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.51%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.00%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.37%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.49%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.85%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.17%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.63%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.80%">-0.19</span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->

The data we use here have the following descriptive statistics: 

<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> min </th>
   <th style="text-align:right;"> 25 percent </th>
   <th style="text-align:right;"> median </th>
   <th style="text-align:right;"> mean </th>
   <th style="text-align:right;"> 75 percent </th>
   <th style="text-align:right;"> max </th>
   <th style="text-align:right;"> std </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> satisfaction_level </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 71.30%">-1.33</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.17</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.57%">-0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 93.51%">1.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.87%">1.82</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> last_evaluation </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 72.76%">-1.36</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 86.09%">-1.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 72.14%">0.36</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 78.92%">0.92</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">1.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> number_project </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 56.22%">-1.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 87.73%">-1.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.14%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.18</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.21%">1.73</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> average_montly_hours </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 71.30%">-1.33</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 86.09%">-1.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 52.86%">0.27</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 76.49%">0.89</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.84%">1.68</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> time_spend_company </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.92</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 77.91%">-0.90</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.86%">0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 97.57%">1.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.44%">2.17</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Work_accident </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.30%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.27%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 42.14%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.16%">-0.22</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 32.50%">4.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> promotion_last_5years </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">13.67</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_accounting </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 48.57%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.59%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.34%">4.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_hr </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 48.57%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.59%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.53%">3.95</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_technical </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 30.43%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.36%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.05%">-0.49</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.41%">2.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_support </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.51%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 39.45%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 87.14%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 39.19%">-0.43</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.62%">2.33</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_management </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.38%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.36%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.29%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.30%">-0.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.93%">6.18</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_IT </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.70%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.00%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 57.14%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.84%">-0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.07%">3.48</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_product_mng </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.27%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.91%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 46.43%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.78%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.85%">4.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_marketing </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.76%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.73%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 48.57%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 24.59%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 29.41%">4.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_RandD </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.84%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.82%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 35.71%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 0.00%">0</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.73%">-0.19</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 38.75%">5.34</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1</span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->

## Step 3: Check Correlations

This is the correlation matrix of the customer responses to the 16 attitude questions - which are the only questions that we will use for the segmentation (see the case):



<img src="figure/bunch_o_figs_pointsize-1.png" title="plot of chunk bunch_o_figs_pointsize" alt="plot of chunk bunch_o_figs_pointsize" style="display: block; margin: auto;" />

**Questions**

1. Do you see any high correlations between the responses? Do they make sense? 
2. What do these correlations imply?

**Answers:**

*
*
*
*
*
*
*
*
*
*

## Step 4: Choose number of factors

We use Principal component analysis to understand the variance explained by components. 






<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Eigenvalue </th>
   <th style="text-align:right;"> Pct of explained variance </th>
   <th style="text-align:right;"> Cumulative pct of explained variance </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> Component 1 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">3.31</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">20.68</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">20.68</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 2 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.77%">1.34</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 44.78%">8.36</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.49%">29.04</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 3 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 41.12%">1.21</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 41.15%">7.55</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.05%">36.59</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 4 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 39.16%">1.14</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 39.22%">7.12</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.14%">43.72</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 5 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 38.32%">1.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 38.33%">6.92</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 43.99%">50.64</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 6 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 37.48%">1.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 37.43%">6.72</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 51.62%">57.36</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 7 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.92%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 37.03%">6.63</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 59.14%">63.99</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 8 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.92%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.94%">6.61</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 66.65%">70.61</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 9 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.64%">1.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.62%">6.54</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 74.06%">77.14</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 10 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.36%">1.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 36.49%">6.51</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 81.46%">83.66</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 11 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 34.95%">0.99</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 35.01%">6.18</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 88.47%">89.84</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 12 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 32.71%">0.91</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 32.81%">5.69</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 94.92%">95.52</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 13 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.17%">0.32</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.32%">2.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 97.20%">97.53</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 14 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.96%">0.17</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.06%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 98.40%">98.59</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 15 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.84%">0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.94%">0.81</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 99.32%">99.40</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Component 16 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.60</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">100.00</span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->


```
## Error in loadNamespace(name): there is no package called 'webshot'
```

**Questions:**

1. Can you explain what this table and the plot are? What do they indicate? What can we learn from these?
2. Why does the plot have this specific shape? Could the plotted line be increasing? 
3. What characteristics of these results would we prefer to see? Why?

**Answers**

*
*
*
*
*
*
*
*
*
*

## Step 5: Interpret the factors




In this case we selected the varimax rotation. For our data, the 10 selected factors look as follows after this rotation: 

<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Comp.1 </th>
   <th style="text-align:right;"> Comp.2 </th>
   <th style="text-align:right;"> Comp.3 </th>
   <th style="text-align:right;"> Comp.4 </th>
   <th style="text-align:right;"> Comp.5 </th>
   <th style="text-align:right;"> Comp.6 </th>
   <th style="text-align:right;"> Comp.7 </th>
   <th style="text-align:right;"> Comp.8 </th>
   <th style="text-align:right;"> Comp.9 </th>
   <th style="text-align:right;"> Comp.10 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> average_montly_hours </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.94</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.10%">-0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.98%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.22%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.98%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.01%">-0.01</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> last_evaluation </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 99.04%">0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 26.53%">0.18</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.99%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.22%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.86%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.01%">0.01</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> number_project </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 99.04%">0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 32.96%">-0.25</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.99%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.22%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.98%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.95%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> time_spend_company </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 85.64%">0.79</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 56.84%">0.51</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.99%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.96%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.86%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.93%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.94%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.01%">0.01</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_technical </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.83%">0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 67.36%">0.58</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 43.51%">-0.36</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.38%">-0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 43.26%">0.35</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 38.76%">-0.31</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 39.37%">-0.32</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 40.00%">-0.32</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.20%">-0.18</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_management </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.83%">0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.51%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.96%">0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.66%">-0.09</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.74</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 20.76%">-0.12</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.71%">0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.68%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.50%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.08%">-0.07</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_IT </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.91%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.84%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.91%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.95</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.87%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.57%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.74%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.62%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.08%">-0.07</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_RandD </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.91%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.84%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.92%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.91%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 28.24%">-0.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.87%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.93%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.95%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.94%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.89</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_support </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.96%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.92%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-0.91</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 23.40%">-0.15</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.30%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.72%">0.14</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.06%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.37%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 22.19%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.09%">-0.08</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> satisfaction_level </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.98</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.99%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.93%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.88%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_product_mng </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.76%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.93%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.79%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.86%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.85%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.49%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.68%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.96</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.04%">-0.04</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Work_accident </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.96%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.76%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.95%">-0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 21.49%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 45.27%">0.29</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 25.65%">0.17</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.78%">-0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.95%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.62%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 56.52%">0.46</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_accounting </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.96%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.92%">-0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.92%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.79%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.86%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.87%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.97</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.74%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.62%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.04%">-0.04</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_marketing </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.91%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.92%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.92%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.79%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.86%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.85%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.57%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.96</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.56%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.04%">-0.04</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_hr </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.83%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.92%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.92%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.74%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.43%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.42%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.63%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.50%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.06%">-0.05</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> promotion_last_5years </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.74%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.59%">0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.00</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.57%">0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 87.84%">0.64</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.78%">0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.49%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.53%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.38%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.07%">0.06</span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->

To better visualize and interpret the factors we suppress loadings with small values, e.g. with absolute values smaller than 0.5. In this case our factors look as follows after suppressing the small numbers:

<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Comp.1 </th>
   <th style="text-align:right;"> Comp.2 </th>
   <th style="text-align:right;"> Comp.3 </th>
   <th style="text-align:right;"> Comp.4 </th>
   <th style="text-align:right;"> Comp.5 </th>
   <th style="text-align:right;"> Comp.6 </th>
   <th style="text-align:right;"> Comp.7 </th>
   <th style="text-align:right;"> Comp.8 </th>
   <th style="text-align:right;"> Comp.9 </th>
   <th style="text-align:right;"> Comp.10 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> average_montly_hours </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.94</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> last_evaluation </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 94.00%">0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> number_project </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 94.00%">0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> time_spend_company </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.79</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.51</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_technical </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.58</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_management </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.74</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_IT </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.95</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_RandD </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.89</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_support </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-0.91</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> satisfaction_level </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.98</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_product_mng </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.96</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Work_accident </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_accounting </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.97</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_marketing </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">0.96</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> dummy_hr </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-0.93</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> promotion_last_5years </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.64</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%"></span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->

**Questions**

1. What do the first couple of factors mean? Do they make business sense? 
2. How many factors should we choose for this data/customer base? Please try a few and explain your final choice based on a) statistical arguments, b) on interpretation arguments, c) on business arguments (**you need to consider all three types of arguments**)
3. How would you interpret the factors you selected?
4. What lessons about data science do you learn when doing this analysis? Please comment. 

**Answers**

*
*
*
*
*
*
*
*
*
*

## Step 6:  Save factor scores 

We can now either replace all initial variables used in this part with the factors scores or just select one of the initial variables for each of the selected factors in order to represent that factor. Here is how the factor scores  are for the first few respondents:

<!--html_preserve--><div class="formattable_container"><table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Obs.01 </th>
   <th style="text-align:right;"> Obs.02 </th>
   <th style="text-align:right;"> Obs.03 </th>
   <th style="text-align:right;"> Obs.04 </th>
   <th style="text-align:right;"> Obs.05 </th>
   <th style="text-align:right;"> Obs.06 </th>
   <th style="text-align:right;"> Obs.07 </th>
   <th style="text-align:right;"> Obs.08 </th>
   <th style="text-align:right;"> Obs.09 </th>
   <th style="text-align:right;"> Obs.10 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> DV (Factor) 1 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 71.18%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 85.33%">1.16</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 66.57%">0.67</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 60.40%">0.72</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 54.70%">0.78</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 56.42%">0.83</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.09</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 2 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 27.27%">-0.21</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.55</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.38</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 30.00%">-0.24</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 19.34%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">-1.27</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.54</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 100.00%">1.60</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.36%">-0.06</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 3 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.91%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.91%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.85%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">-0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.01</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.84%">0.03</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 4 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.73%">0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.35%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.29%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.73%">0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.55%">0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.72%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.38%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.40%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.52%">0.05</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 5 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.27%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.94%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.33%">-0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.29%">-0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 17.27%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.79%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.60%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.19%">-0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.26%">-0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.73%">-0.10</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 6 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.82%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.47%">-0.13</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.67%">-0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 18.57%">-0.11</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.82%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.70%">-0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.04%">-0.09</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.36%">-0.12</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.23%">-0.12</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.68%">-0.04</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 7 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.71%">0.10</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 15.14%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.85%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.72%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.58%">0.09</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.96%">0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 8 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.94%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.67%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.29%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.88%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.79%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.26%">0.05</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.02</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 9 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.64%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.59%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.67%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.57%">0.04</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.64%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.40%">0.06</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.60%">0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 10.00%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 11.13%">0.03</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 12.52%">0.05</span> </td>
  </tr>
  <tr>
   <td style="text-align:left;"> DV (Factor) 10 </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.55%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.53%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.33%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 16.00%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.55%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.25%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.60%">-0.07</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.58%">-0.09</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 13.96%">-0.08</span> </td>
   <td style="text-align:right;"> <span style="display: inline-block; direction: rtl; border-radius: 4px; padding-right: 2px; background-color: #EEEEEE; width: 14.21%">-0.07</span> </td>
  </tr>
</tbody>
</table></div><!--/html_preserve-->

**Questions**

1. Can you describe some of the people using the new derived variables (factor scores)? 
2. Which of the 29 initial variables would you select to represent each of the factors you selected?  

**Answers**

*
*
*
*
*
*
*
*
*
*

<hr>\clearpage

