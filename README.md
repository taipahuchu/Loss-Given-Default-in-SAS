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

INTRODUCTION 
Loss given default (LGD) measures the percentage of all exposure at the time of default that can not be recovered. 
Recovery rate (RR) is defined as one minus LGD. LGD/RR modeling attracts much less attention compared with the 
large volume of literature on PD modeling. With the portfolio loss estimation being a major concern in modern risk 
management system, increasing attention is being dedicated to LGD modeling as well as PD and LGD joint 
estimation. In terms of the methodologies there are two main streams: one approach is to apply fixed effect 
regression models including linear regression and fractional response regression to predict LGD (Gupton and Stein, 
2002, Dermine et al, 2006 and Bastos, 2010). In empirical studies LGD distributions often present bi-modal 
characteristics bounded between the interval [0, 1] based on its definition. Calabrese (2012) proposes an inflated 
beta regression model which considered the dependent variable as a mixture of a continuous beta distribution on (0, 
1) and a discrete Bernoulli distribution to model the probability mass at the boundaries 0 and 1, which can be 
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
DATA AND SETUP 
The empirical study is based on the US corporate bonds recovery rates information from Moody’s Ultimate Recovery 
Database (MURD). The unit of observation in this study is instrument. This database covers the recovery information 
of more than 3000 instruments until date. The instruments include bank loans, revolvers and corporate bonds. In this 
2 
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
Recovery Ratei,t = Intercept + Recovery Characteristicsi + Firm Characteristicsi,t-1 + Macroeconomic Variablest-1
Figure 1 presents the distribution of recovery rates in our sample. We can observe the clustered observations with 
recovery rates equal to 0 and 1 from the figure. Table 1 presents the recovery rates distribution by seniority and Table 
2 gives the descriptions of the variables used in this study. 
Figure 1. Distribution of recovery rates 
No. Mean Std Min Max 
Junior Subordinate Bonds 28 0.1628 0.2634 0 1 
Senior Secured Bonds 332 0.6292 0.3688 0 1.1298 
Senior Subordinate Bonds 198 0.3150 0.3617 0 1.6978 
Senior Unsecured Bonds 681 0.5100 0.3813 0 1.0499 
Subordinate Bonds 174 0.3217 0.3743 0 1.3691 
Total 1413 0.4806 0.3915 0 1.6978 
Table 1. Recovery rates by seniority 
3 
Debt Characteristics 
Var1: Collateral Rank Instruments are ranked related to each other based on the structure prior to 
default, taking into consideration collateral and instrument type. 
Var2: Percent Above Percentage of debt which is contractually senior to the current instrument. 
Var3: Issue Size Face value of the relevant instrument. 
Firm Characteristics 
Var4: Total Asset Total assets of the obligor 
Var5: EBITDA Earnings before interest, taxes, depreciation and amortization 
Var6: Leverage Ratio of total debt and total assets 
Var7: Debt Ratio Ratio of current liabilities and long term debt 
Var8: Book Value per Share Book value of assets scaled by the total outstanding shares 
Var9: Asset Tangibility Ratio between intangible assets and tangible assets 
Var10: Quick Ratio Sum of cash and short-term investment and total receivables divided by the 
current liabilities. 
Macroeconomic Variables 
Var11: Growth Rate US annual GDP growth rate 
Var12: T-Bill Rate US three months Treasury bill rate 
Var13: Aggregated Default Rates US annual issuer-weighted corporate default rates 
Var14: Unemployment Rate US annual unemployment rate 
Table 2. List of covariates 
MODELS AND SAS PROGRAMS 
This section gives an overview of the models in this study. The following mathematical notations are used through 
this paper. The recovery rate of instrument i is defined as i y and the vector of covariates is given as i x . 0 b and β
denote the intercept term and the vector of parameters respectively. In the following SAS programs we name the 
dependent variable as ‘RR’, and the independent covariates are indexed as ‘Var1-Var14’. The parameters of 
intercept term and all the covariates are named as ‘b0-b14’, and the cleaned dataset is named as ‘MyData’. 
LINEAR REGRESSION 
Previous studies show that linear regression models appear to be of comparable predictive accuracies as other more 
complicated statistical models (Qi and Zhao, 2011; Bellotti and Crook, 2012) even though there is the potential risk to 
make predictions out of the range between 0 and 1. The linear regression model is defined 
 β 0
2 ~ (0, )
T
i ii
i
y
N
b e
e s
=+ + x .



