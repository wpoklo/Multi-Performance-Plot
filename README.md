# THE MULTI-PERFORMANCE PLOT: GUIDANCE

**_BACKGROUND_**

Simulation studies can be used to evaluate the performances of statistical methods, such as to determine how accurately or precisely an estimand can be estimated by each 
method. Commonly used performance measures include (Morris et al., 2019): 

•	bias (the difference between the true value of the estimator and its estimate averaged over _N_ simulations);

•	empirical standard error (EmpSE; the variance of the _N_ simulated estimates);

•	mean squared error (MSE; the squared difference between the true value and its estimate, averaged over _N_ simulations);

•	average model standard error (ModSE; the estimated variance of the estimator, averaged over _N_ simulations), and 

•	coverage (the probability the estimand lies in a preset interval).

A tabular display of these performance measures is the simplest and most common presentation method as all exact estimated values can be displayed systematically. 
When many simulation parameters, methods and performance measures are explored, the tables can be unwieldy.

Visual presentations can improve the ease of interpreting the raw results. Morris et al. (2019) proposed the use of lollipop plots and zip plots to visualise the 
distribution of each performance measure and its associated Monte Carlo standard error. Rucker and Schwarzer (2014) proposed the concept of a nested-loop plot, where the 
results of one performance measure from combinations of multiple simulation parameters can be combined into one plot. 

However, neither proposal allows the simultaneous visualisation of multiple performance measures in one plot.

**_METHODS_**

I therefore propose a new graphical display called a multi-performance plot that allows for seven performance measures to be visualised in one plot, in addition to multiple 
methods and simulation parameters. The procedure to generate the plot is as follows.

1.	For each data-generating mechanism, plot the bias and empirical standard error on the horizontal and vertical axes respectively to give the point (Bias, EmpSE). 
    Points closer to the origin are desirable. The distance from each point to the origin is approximately its MSE due to Pythagoras’ theorem.
    
2.	For each data-generating mechanism, illustrate the average model standard error by drawing a vertical line from the point downwards of length ModSE.

3.	For each data-generating mechanism, illustrate the coverage by shading the point using a suitable colour gradient. This gradient should start from the
    smallest coverage among all data-generating mechanisms and end at a pre-determined coverage threshold (usually this is 0.95, or 95%).
  	Importantly, any point with coverage reaching at least this coverage threshold must have a different colour (e.g. cyan), so that results with sufficient coverage
  	can be easily identified.
    
5.	The shape of the point, and the colour and/or type of the vertical line can be altered to reflect different simulation parameters and/or methods.

These steps allow the visualisation of the five bullet-pointed performance measures in the Background section of this document. 
Additionally, two relative performance measures (Morris et al., 2019) can also be visualised:

•	relative % error in ModSE (the percentage increase in ModSE relative to its EmpSE in the same data-generating mechanism) – this can be visualised by whether the 
  vertical line in step 2. intersects the horizontal axis. If the line does not intersect the axis, then EmpSE is greater than ModSE, and conversely if the line extends 
  beneath the axis. Ideally, the line should end at the horizontal axis.
  
•	relative increase in precision (the percentage increase of EmpSE in one data-generating mechanism relative to another data-generating mechanism) – this can be visualised 
  simply by comparing the heights of the two corresponding points on the multi-performance plot.

**_RSHINY APPLICATION_**

An RShiny app for its implementation can be found here: 

  https://poklo.shinyapps.io/MultiPerformancePlot_1-0/

The procedure to upload a compatible CSV is as follows:

- Using the A**D**E**M**P stucture described by Morris et al. (2019), tabulate all combinations of parameters of  **D**ata-generating mechanisms and **M**ethods.
  As an example, using this case: https://cran.r-project.org/web/packages/rsimsum/vignettes/B-relhaz.html, the **M**ethods investigated are [Cox vs Exp vs RP(2)] models,
  and there are two simulated parameters to generate the **D**ata-generating mechanisms: Baseline hazard function [Exponential vs Weibull], and Sample size [50 vs 250].
  Therefore, there are three parameters in total: model; baseline; sample size. These result in (3 x 2 x 2) = 12 combinations:

  ```
  [Cox + Exponential + 50];  [Exp + Exponential + 50]; [RP(2) + Exponential + 50]; [Cox + Weibull + 50]; [Exp + Weibull + 50]; [RP(2) + Weibull + 50];
  [Cox + Exponential + 250]; [Exp + Exponential + 250]; [RP(2) + Exponential + 250]; [Cox + Weibull + 250]; [Exp + Weibull + 250]; [RP(2) + Weibull + 250]
  ```

  Please see Example table at the end of this document.
  
- In producing the CSV, leave the first four columns blank, and enter these combinations of parameters from the fifth column onwards, as shown in the Example table at the
  end of this document.

- After the results of the simulation study have been collected, the first four columns [bias; empirical standard error; average model standard error; coverage] can be
  filled, in correspondence with the combinations described above. Each set of results must match their original data-generating mechanism and method.
  Please ensure that the headings of these first four columns are respectively named: "bias"; "empse"; "modelse"; "cover". An example is provided at the end of this document.

Two example CSVs are attached in this repository: gasparinidf.csv which is the example described here, and parastdf.csv with data taken from
Table I of Parast et al. (2016).

Once the CSV has been uploaded, a total of seven boxes will be displayed. The first three boxes ask for which parameters should be presented in the multi-performance plot,
in the form of shapes, line types and line colours (as described in the Methods section). The fourth boxes asks for the pre-determined coverage threshold; by default,
this is set to 0.95. Finally, the last three boxes ask for the names of the parameters that should be displayed in the legends of the multi-performance plot.

The two example CSVs can be uploaded to experiment with this tool, before uploading your own dataset.

Example table:

```
        bias	      empse	    modelse	cover	model	baseline	  n
 0.021479986	0.328476474	0.318460370	0.95	Cox	  Exponential	 50
 0.023914113	0.325755906	0.312674786	0.94	Exp	  Exponential	 50
 0.018283911	0.331174565	0.316501970	0.95	RP(2) Exponential	 50
-0.028186623	0.311454757	0.305189809	0.97	Cox	      Weibull    50
 0.150920681	0.204130251	0.288842868	0.99	Exp	      Weibull	 50
-0.034771249	0.311079844	0.299609422	0.95	RP(2)	  Weibull	 50
-0.021524079	0.148833647	0.139605737	0.93	Cox	  Exponential	250
-0.021353589	0.150640036	0.138085835	0.92	Exp	  Exponential	250
-0.022743755	0.148944708	0.139392412	0.93	RP(2) Exponential	250
-0.012041211	0.133345051	0.132047807	0.94	Cox	      Weibull	250
 0.148162448	0.092941412	0.128051187	0.85	Exp	      Weibull	250
-0.013933685	0.136774527	0.131277399	0.94	RP(2)	  Weibull	250
```
