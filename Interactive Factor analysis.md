---
title: "Derived Attributes and Dimensionality Reduction: Interactive Tool"
author: "Ng Zhenfu"
runtime: shiny
output: 
  html_document:
    theme: paper
    toc: yes
    toc_float:
      collapsed: no
      smooth_scroll: yes

---

<!--html_preserve--><style type="text/css">p { text-align:justify; }</style><!--/html_preserve--><!--html_preserve--><style type="text/css">label { display: none; }</style><!--/html_preserve--><!--html_preserve--><style type="text/css">.c3 svg { font-size:13px; font-family:"Roboto", "Helvetica Neue", Helvetica, Arial, sans-serif; }</style><!--/html_preserve--><!--html_preserve--><style type="text/css">.formattable_widget { overflow:auto; max-height:425px; margin-bottom:23px; }</style><!--/html_preserve--><!--html_preserve--><style type="text/css">.formattable_widget table { margin-bottom:0; }</style><!--/html_preserve--><!--html_preserve--><style type="text/css">.formattable_widget td, .formattable_widget th { white-space: nowrap; }</style><!--/html_preserve-->


## Factor Analysis in 6 steps

This tool follows the 6 steps for factor analysis outlined in the [Derived Attributes and Dimensionality Reduction](http://inseaddataanalytics.github.io/INSEADAnalytics/Report_s23.html) reading of the course. 

First we load the data (`data/HR_clean.csv` by default):


```
## Error in eval(expr, envir, enclos): could not find function "fileInput"
```

```
## Error in eval(expr, envir, enclos): could not find function "eventReactive"
```

We also need to select which variables to consider for factor analysis (30 at most): 


```
## Error in eval(expr, envir, enclos): could not find function "selectizeInput"
```

```
## Error in eval(expr, envir, enclos): could not find function "observeEvent"
```

```
## Error in eval(expr, envir, enclos): could not find function "eventReactive"
```

Here is how the first 10 rows look like:


```
## function (...) 
## {
##     if (length(outputArgs) != 0 && !hasExecuted$get()) {
##         warning("Unused argument: outputArgs. The argument outputArgs is only ", 
##             "meant to be used when embedding snippets of Shiny code in an ", 
##             "R Markdown code chunk (using runtime: shiny). When running a ", 
##             "full Shiny app, please set the output arguments directly in ", 
##             "the corresponding output function of your UI code.")
##         hasExecuted$set(TRUE)
##     }
##     if (is.null(formals(origRenderFunc))) 
##         origRenderFunc()
##     else origRenderFunc(...)
## }
## <environment: 0x7fcc70819b88>
## attr(,"class")
## [1] "shiny.render.function" "function"             
## attr(,"outputFunc")
## function (outputId, width = "100%", height = "0") 
## {
##     shinyWidgetOutput(outputId, "formattable_widget", width, 
##         height, package = "formattable")
## }
## <bytecode: 0x7fcc6ef4df18>
## <environment: namespace:formattable>
## attr(,"outputArgs")
## list()
## attr(,"hasExecuted")
## <Mutable>
##   Public:
##     clone: function (deep = FALSE) 
##     get: function () 
##     set: function (value) 
##   Private:
##     value: FALSE
```


### Step 1: Confirm data is metric

The data we use here have the following descriptive statistics: 


```
## function (...) 
## {
##     if (length(outputArgs) != 0 && !hasExecuted$get()) {
##         warning("Unused argument: outputArgs. The argument outputArgs is only ", 
##             "meant to be used when embedding snippets of Shiny code in an ", 
##             "R Markdown code chunk (using runtime: shiny). When running a ", 
##             "full Shiny app, please set the output arguments directly in ", 
##             "the corresponding output function of your UI code.")
##         hasExecuted$set(TRUE)
##     }
##     if (is.null(formals(origRenderFunc))) 
##         origRenderFunc()
##     else origRenderFunc(...)
## }
## <environment: 0x7fcc6ecc56a0>
## attr(,"class")
## [1] "shiny.render.function" "function"             
## attr(,"outputFunc")
## function (outputId, width = "100%", height = "0") 
## {
##     shinyWidgetOutput(outputId, "formattable_widget", width, 
##         height, package = "formattable")
## }
## <bytecode: 0x7fcc6ef4df18>
## <environment: namespace:formattable>
## attr(,"outputArgs")
## list()
## attr(,"hasExecuted")
## <Mutable>
##   Public:
##     clone: function (deep = FALSE) 
##     get: function () 
##     set: function (value) 
##   Private:
##     value: FALSE
```


### Step 2: Scale the  data

Select variables to standardize:


```
## Error in eval(expr, envir, enclos): could not find function "selectizeInput"
```

```
## Error in eval(expr, envir, enclos): could not find function "observeEvent"
```

```
## Error in eval(expr, envir, enclos): could not find function "eventReactive"
```

These are the summary statistics of the scaled dataset:


```
## function (...) 
## {
##     if (length(outputArgs) != 0 && !hasExecuted$get()) {
##         warning("Unused argument: outputArgs. The argument outputArgs is only ", 
##             "meant to be used when embedding snippets of Shiny code in an ", 
##             "R Markdown code chunk (using runtime: shiny). When running a ", 
##             "full Shiny app, please set the output arguments directly in ", 
##             "the corresponding output function of your UI code.")
##         hasExecuted$set(TRUE)
##     }
##     if (is.null(formals(origRenderFunc))) 
##         origRenderFunc()
##     else origRenderFunc(...)
## }
## <environment: 0x7fcc717f4670>
## attr(,"class")
## [1] "shiny.render.function" "function"             
## attr(,"outputFunc")
## function (outputId, width = "100%", height = "0") 
## {
##     shinyWidgetOutput(outputId, "formattable_widget", width, 
##         height, package = "formattable")
## }
## <bytecode: 0x7fcc6ef4df18>
## <environment: namespace:formattable>
## attr(,"outputArgs")
## list()
## attr(,"hasExecuted")
## <Mutable>
##   Public:
##     clone: function (deep = FALSE) 
##     get: function () 
##     set: function (value) 
##   Private:
##     value: FALSE
```


### Step 3:  Check correlations 

This is the correlation matrix of the original variables we use for factor analysis:


```
## function (...) 
## {
##     if (length(outputArgs) != 0 && !hasExecuted$get()) {
##         warning("Unused argument: outputArgs. The argument outputArgs is only ", 
##             "meant to be used when embedding snippets of Shiny code in an ", 
##             "R Markdown code chunk (using runtime: shiny). When running a ", 
##             "full Shiny app, please set the output arguments directly in ", 
##             "the corresponding output function of your UI code.")
##         hasExecuted$set(TRUE)
##     }
##     if (is.null(formals(origRenderFunc))) 
##         origRenderFunc()
##     else origRenderFunc(...)
## }
## <environment: 0x7fcc70eb1438>
## attr(,"class")
## [1] "shiny.render.function" "function"             
## attr(,"outputFunc")
## function (outputId, width = "100%", height = "0") 
## {
##     shinyWidgetOutput(outputId, "formattable_widget", width, 
##         height, package = "formattable")
## }
## <bytecode: 0x7fcc6ef4df18>
## <environment: namespace:formattable>
## attr(,"outputArgs")
## list()
## attr(,"hasExecuted")
## <Mutable>
##   Public:
##     clone: function (deep = FALSE) 
##     get: function () 
##     set: function (value) 
##   Private:
##     value: FALSE
```


### Step 4: Choose number of factors 

This is the Variance Explained table, using all data selected for factor analysis:


```
## Error in eval(expr, envir, enclos): could not find function "eventReactive"
```

```
## function (...) 
## {
##     if (length(outputArgs) != 0 && !hasExecuted$get()) {
##         warning("Unused argument: outputArgs. The argument outputArgs is only ", 
##             "meant to be used when embedding snippets of Shiny code in an ", 
##             "R Markdown code chunk (using runtime: shiny). When running a ", 
##             "full Shiny app, please set the output arguments directly in ", 
##             "the corresponding output function of your UI code.")
##         hasExecuted$set(TRUE)
##     }
##     if (is.null(formals(origRenderFunc))) 
##         origRenderFunc()
##     else origRenderFunc(...)
## }
## <environment: 0x7fcc718994a0>
## attr(,"class")
## [1] "shiny.render.function" "function"             
## attr(,"outputFunc")
## function (outputId, width = "100%", height = "0") 
## {
##     shinyWidgetOutput(outputId, "formattable_widget", width, 
##         height, package = "formattable")
## }
## <bytecode: 0x7fcc6ef4df18>
## <environment: namespace:formattable>
## attr(,"outputArgs")
## list()
## attr(,"hasExecuted")
## <Mutable>
##   Public:
##     clone: function (deep = FALSE) 
##     get: function () 
##     set: function (value) 
##   Private:
##     value: FALSE
```

Here is the **scree plot**:

<!--html_preserve--><div style="height:480px">
<div id="out3f68de5d64b49e7d" style="width:100%; height:100%; " class="c3 html-widget html-widget-output"></div>
</div><!--/html_preserve-->

We now select the criterion to use for deciding how many factors to use:


```
## Error in eval(expr, envir, enclos): could not find function "selectizeInput"
```

```
## Error in eval(expr, envir, enclos): could not find function "conditionalPanel"
```

```
## Error in eval(expr, envir, enclos): could not find function "conditionalPanel"
```

```
## Error in eval(expr, envir, enclos): could not find function "observeEvent"
```

```
## Error in eval(expr, envir, enclos): could not find function "eventReactive"
```


### Step 5: Interpret the factors

We can now use a rotation to get easier to interpret results:


```
## Error in eval(expr, envir, enclos): could not find function "selectizeInput"
```











