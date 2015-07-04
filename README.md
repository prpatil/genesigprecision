# genesigprecision
R Code for reproducing analysis for "Measuring the contribution of genomic predictors through estimator precision gain"

### R packages
Required packages:
BatchJobs, xtable, genefu, Biobase, rpart

### File Description
* functions.R contains the code necessary for estimator adjustment, as describe in the "Methods" section of the paper.
* genesigprecision_data.Rda contains the 296-patient MammaPrint validation (Buyse) dataset and the three GEO datasets referred to in the paper
* par_fun.R contains the parallelized simulation function that computes the adjusted estimators 1000 times. This is run 100 times each via BatchJobs to attain 100,000 total simulations.
* par_fun_internal.R contains a simulation approach to running 10 subsamplings of the data and resampling 100,000 times from each subsample. This is done to get a sense of the variability of our gain estimates.
* par_fun_double.R is the same as par_fun.R except we double the sample size when we resample with replacment
* par_fun_fewer.R is the same as par_fun.R except we use fewer clinical adjustment covariates
* par_fun_eset.R accomplishes the same task as par_fun.R, except it is tailored to handle ExpressionSet data as input
* par_fun_eset_double.R is the same as par_fun_eset.R, except we double the sample size when we resample with replacement
* internal_looper_nomod.R is a helper function to conduct the 10x10,000 simulation.
* genesigprecision_run.R contains code to run the analysis and reproduce the results in the paper.
* .BatchJobs.R and simple.tmpl are configuration files necessary for running the parallelized job on a cluster.

* supplement_run.R contains code used to generate additional results regarding variability of samples and permuatation of labels under larger sample size and fewer covariates.
* supplement.pdf is a PDF version of the supplementary material

### Instructions

NOTE: This analysis relies on a Sun Grid Engine cluster. We provide the configuration files and code necessary to reproduce this analysis
on an SGE platform. Please examine the code in genesigprecision_run.R before you run it because it contains the commands to create a registry
and submit SGE batch jobs via the BatchJobs R package.

1. Install the required packages.
2. Download all files in this github repository and keep them together in a local directory on your cluster.
3. Run the code from genesigprecision_run.R.
	* Please keep an eye for "submitJobs" commands in this file - these submit the batch jobs and are at the mercy of the cluster.
4. (Optional) Run the code from supplement_run.R if you would like to recreate the results in the supplement as well.	