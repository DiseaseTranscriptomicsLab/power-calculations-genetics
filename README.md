# Genetic power calculations <!-- omit in toc -->

Pipeline in R for performing power calculations (based on *[chi-squared](https://en.wikipedia.org/wiki/Chi-squared_test)* test) for genetic studies, using *[pwr](https://cran.r-project.org/web/packages/pwr)* R package (see vignette [here](https://cran.r-project.org/web/packages/pwr/vignettes/pwr-vignette.html)). Its main application is to assist users with experimental design.


## Table of contents <!-- omit in toc -->

<!-- vim-markdown-toc GFM -->
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
  - [Arguments](#arguments)
  - [Examples](#examples)
- [Output](#output)

<!-- vim-markdown-toc -->

<br>

## Introduction

The rational behind performing power calculations is that a study with low statistical power has a reduced chance of detecting a true effect, but it is less well appreciated that low power also reduces the likelihood that a statistically significant result reflects a true effect (see "[Power failure: why small sample size undermines the reliability of neuroscience](docs/Power%20failure%20why%20small%20sample%20size%20undermines%20the%20reliability%20of%20neuroscience.pdf)" published in [Nature Reviews Neuroscience](https://www.nature.com/articles/nrn3475) (2013)). The consequences of this include overestimates of effect size and low reproducibility of results. 

<br>

## Installation

Use the [environment.yaml](envm/environment.yaml) file to create conda environment and install required packages. The `-p` flag should point to the miniconda installation path. For instance, to create `power_calc_genetics` environment using miniconda installed in `/miniconda` directory run the following command:

```
conda env create -p /miniconda/envs/power_calc_genetics --file envm/environment.yaml
```

Activate created `power_calc_genetics` conda environment before running the pipeline

```
conda activate power_calc_genetics
```

<br>

## Usage

To run the pipeline execute the *[power_calc_genetics.R](./scripts/power_calc_genetics.R)* script. This script catches the arguments from the command line and passes them to the *[power_calc_genetics.Rmd](./scripts/power_calc_genetics.Rmd)* script to perform power calculations and produce the interactive `HTML` report.

### Arguments

Argument | Description | Required
------------ | ------------ | ------------
--samples_n | Total number of samples | No
--features_n | Total number of features (used for multihypothesis testing adjustment) | No
--power | Power of test (1 - type II error probability) | No
--sig_level | Significance level (type I error probability) | No
--deg_freedom | Degree of freedom | No
--report_name | Desired name for the report | No
--report_dir | Desired location for the report | **Yes**
--seed | Seed for random number generation | No
--hide_code_btn | Hide the "Code" button allowing to show/hide code chunks in the final `HTML` report | No

<br>

**Packages**: required packages are listed in [environment.yaml](envm/environment.yaml) file.

### Examples

Below is a command line use example for generating a ***genetic power calculations*** report for a hypothetical dataset of 10000 samples and 100000 genetic features (variants):


```
conda activate power_calc_genetics
```

<br>

*[power_calc_genetics.R](./scripts/power_calc_genetics.R)* script (see the beginning of [Usage](#usage) section) should be executed from the [scripts](./scripts) folder

```
cd Power_calc_genetics/scripts

Rscript power_calc_genetics.R  --samples_n 10000 --power 0.9 --sig_level 0.05 --deg_freedom 1 --features_n 100000 --report_name power_calc_genetics --report_dir output

```

The interactive `HTML` report named `power_calc_genetics.html` will be created in `output` folder.

**Note**: make sure that the created *conda* environment (see [Installation](#installation) section) is  activated

<br>

### Output

The pipeline generates `HTML`-based ***genetic power calculations*** report within user-defined `output` folder:

```
|
|____[output]
  |____[power_calc_genetics].html
  |____[power_calc_genetics].md
```

**Note**: the *[power_calc_genetics].md* file is a markdown (md) file containing a plain text representation of the content before it's formatted into the *.html* report.

<br>

