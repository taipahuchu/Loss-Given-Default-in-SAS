**Loss Given Default for Loan Facilities**

Predicting loss given default (LGD) is playing an increasingly crucial role in quantitative credit risk modeling. In this 
project, we explore the mixed effects models to predict Loan facilities LGD, as well as other widely used LGD 
models. The empirical results show that mixed effects models are able to explain the unobservable heterogeneity and 
to make better predictions compared with linear regression and fractional response regression. All the statistical 
models are performed in SAS/STAT®, SAS® 9.2, using specifically PROC REG and PROC NLMIXED, and the 
model evaluation metrics are calculated in PROC IML. This project gives a detailed description on how to use PROC 
NLMIXED to build and estimate generalized linear models and mixed effects models. 
[![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=taipahuchu)](https://github.com/anuraghazra/github-readme-stats)

### Hi there 👋, Modeling Loss Given Default in SAS/STAT
#### Loss given default (LGD) measures the percentage of all exposure at the time of default that can not be recovered.  Recovery rate (RR) is defined as one minus LGD
This project aims to fill in this gap by applying the random effect terms at multiple levels and to conduct a comparison 
study of the commonly used models in literature. We mainly investigate to apply the mixed effects models to predict 
the US corporate bonds recovery rates with the random effect terms specified at obligor, seniority and time levels. We 
find that the inclusion of an obligor-varying random effect term effectively explains the unobservable heterogeneity 
and the related predictive accuracies are also much better than the others. All the models are built up and realized in 
SAS/STAT® and the prediction results are generated in PROC IML.

Skills: SAS/Credit Risk

- 🔭 I’m currently working on this page. 


[<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg' alt='github' height='40'>](https://github.com/taipahuchu)  [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/linkedin.svg' alt='linkedin' height='40'>](https://www.linkedin.com/in/linkedin.com/in/taipa-huchu/)  

**Introduction**
Loss given default (LGD) measures the percentage of all exposure at the time of default that can not be recovered. 
Recovery rate (RR) is defined as one minus LGD. LGD/RR modeling attracts much less attention compared with the 
large volume of literature on PD modeling. With the portfolio loss estimation being a major concern in modern risk 
management system, increasing attention is being dedicated to LGD modeling as well as PD and LGD joint 
estimation. In terms of the methodologies there are two main streams: one approach is to apply fixed effect 
regression models including linear regression and fractional response regression to predict LGD (Gupton and Stein, 
2002, Dermine et al, 2006 and Bastos, 2010). In empirical studies LGD distributions often present bi-modal 
characteristics bounded between the interval [0, 1] based on its definition. Calabrese (2012) proposes an inflated 
beta regression model which considered the dependent variable as a mixture of a continuous beta distribution on (0,1)
and a discrete Bernoulli distribution to model the probability mass at the boundaries 0 and 1, which can be 
regarded as a special type of generalized linear regression model. 

A second approach is the use of the mixed effects models based on the Vasicek’s single factor framework (Vasicek 
1987) where LGD is assumed to be dependent on a systematic risk factor in the predictors (Hamerle et al, 2006). In 
the setting of a single factor model the unobservable systematic risk factor works as a random effect term and the 
idiosyncratic risk factor is the residual term. Consequently a single factor model with the observable covariates is 
equivalent as a mixed effects model. However, Hamerle et al (2006) only consider the time-varying latent factor and 
they do not make any further benchmarking studies. 

This project aims to fill in this gap by applying the random effect terms at multiple levels and to conduct a comparison 
study of the commonly used models in literature. We mainly investigate to apply the mixed effects models to predict 
the US corporate bonds recovery rates with the random effect terms specified at obligor, seniority and time levels. We 
find that the inclusion of an obligor-varying random effect term effectively explains the unobservable heterogeneity 
and the related predictive accuracies are also much better than the others. All the models are built up and realized in 
SAS/STAT® and the prediction results are generated in PROC IML. 

The remainder of this paper is structured as follows. The next section briefly introduces the data used in the empirical 
study and is followed by an overview of the models with SAS programs provided. The empirical results and analysis 
are then presented and the last section concludes this study.

**Data and Setup** 
The empirical study is based on the US corporate bonds recovery rates information from Moody’s Ultimate Recovery 
Database (MURD). The unit of observation in this study is instrument. This database covers the recovery information 
of more than 3000 instruments until date. The instruments include bank loans, revolvers and corporate bonds. In this 
study we are only interested in the corporate bonds and use recovery rate as the dependent variable instead of LGD, 
and the final sample has 1413 observations of defaulted bonds observed from 1986 to 2012. 
There are five different seniorities including Junior Subordinated, Subordinated, Senior Subordinated, Senior Secured 
and Senior Unsecured. Each obligor may issue more than one instrument with different seniorities. In MURD only 
instrument related information is provided including the debt characteristics and recovery process information. We 
integrate the accounting ratios from Compustat into our sample by using the common firm identifier. US 
macroeconomic variables are also included and extracted from the open sources online to capture features of the 
economic cycle. Here both Issue Size and Total Asset are subjected to a log transformation for scaling. Both 
accounting and macroeconomic covariates are incorporated one year prior to default and the regression model can 
be presented as follows 

Recovery Rate = Intercept + Recovery Characteristics + Firm Characteristics + Macroeconomic Variables

https://github.com/taipahuchu/Loss-Given-Default-in-SAS/blob/main/factors.xlsx


 





