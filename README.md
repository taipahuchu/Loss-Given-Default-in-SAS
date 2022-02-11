**Loss Given Default for Loan Facilities**

Predicting loss given default (LGD) is playing an increasingly crucial role in quantitative credit risk modeling. In this 
project, we explore the mixed effects models to predict Loan facilities LGD, as well as other widely used LGD 
models. The empirical results show that mixed effects models are able to explain the unobservable heterogeneity and 
to make better predictions compared with linear regression and fractional response regression. All the statistical 
models are performed in SAS/STAT®, SAS® 9.2, using specifically PROC REG and PROC NLMIXED, and the 
model evaluation metrics are calculated in PROC IML. This project gives a detailed description on how to use PROC 
NLMIXED to build and estimate generalized linear models and mixed effects models. Lgd is Loss given default.
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

List of covariates		
		Debt Characteristics
		
Var1	Collateral Rank 	Instruments are ranked related to each other based on the structure prior to default, taking into consideration collateral and instrument type.
Var2 	Percent Above	Percentage of debt which is contractually senior to the current instrument. 
Var3	Issue Size	Face value of the relevant instrument. 
		
		Quick Ratio
		
Var4	 Total Asset 	Total assets of the obligor 
Var5	EBITDA	Earnings before interest, taxes, depreciation and amortization
Var6	Leverage	Ratio of total debt and total assets
Var7	Debt Ratio 	Ratio of current liabilities and long term debt
Var8	Book Value per Share	Book value of assets scaled by the total outstanding shares 
Var9	Asset Tangibility 	Ratio between intangible assets and tangible assets
Var10	Quick Ratio	"Sum of cash and short-term investment and total receivables divided by the 
current liabilities."
		
		Macroeconomic Variables 
		
Var12	 Growth Rate 	Annual GDP growth rate
Var13	 T-Bill Rate	Three months Treasury bill rate 
Var14	Aggregated Default Rates 	Annual issuer-weighted corporate default rates
Var15	Unemployment Rate	Annual unemployment rate 
![image](https://user-images.githubusercontent.com/39062372/147856797-8791a1b6-a3fe-4f49-8117-4e4a3d65b3f6.png)

MODELS AND SAS PROGRAMS 
This section gives an overview of the models in this study. The following mathematical notations are used through 
this paper. The recovery rate of instrument i is defined as i y and the vector of covariates is given as i x . 0 b and β
denote the intercept term and the vector of parameters respectively. In the following SAS programs we name the 
dependent variable as ‘RR’, and the independent covariates are indexed as ‘Var1-Var14’. The parameters of 
intercept term and all the covariates are named as ‘b0-b14’, and the cleaned dataset is named as ‘MyData’. 

**LINEAR REGRESSION **

Previous studies show that linear regression models appear to be of comparable predictive accuracies as other more 
complicated statistical models (Qi and Zhao, 2011; Bellotti and Crook, 2012) even though there is the potential risk to 
make predictions out of the range between 0 and 1. 

**FRACTIONAL RESPONSE REGRESSION **

Fractional response regression was first proposed by Papke and Wooldridge (1996) and has been widely applied in 
LGD modeling (Dermine and Carvalho, 2006; Bastos, 2010, Bellotti & Crook, 2012). In this model, the dependent 
variable is bounded between 0 and 1 by imposing a link function such as β 0 (|) ( ) T Ey G ii i x x = + b where G( )⋅
denotes a link function such as a logit or a complementary log-log transformation function and the quasi maximum 
likelihood function.

**Inflated beta regression **

Inflated beta regression is proposed by Ospina and Ferrari (2010) where the dependent variable is regarded as a 
mixture distribution of a beta distribution on (0, 1) and a Bernoulli distribution on boundaries 0 and 1. The probability 
density function is the beta density function and m and f are the mean and precision parameters. Here m can be 
reparameterized by imposing a logit transformation.

**CONCLUSION **

In this project we demonstrate that how to estimate both fixed and mixed effects models in SAS/STAT®. We also 
illustrate calculating performance metrics in PROC IML with common matrix operators. This study proposes to apply 
a linear mixed effects model to predict the US corporate bonds recovery rates. The purpose of using a mixed effects 
model is to better explain the unobservable heterogeneity in an empirical data set. Performances of the mixed effects 
models with the random effect term specified at obligor, seniority and time levels are examined. We build up linear 
regression model in PROC REG, and realize fractional response regression and inflated beta regression models in 
PROC NLMIXED. We provide details on how to estimate mixed effects models in PROC NLMIXED with a simple 
macro variable incorporated for convenience. Empirical evidence indicates that an obligor-varying mixed effects 
model significantly outperforms the others in terms of all the performance metrics we considered, which emphasizes 
the importance of including firm specific random effect. We provide a new angle to model corporate bonds recovery 
rates and show the conveniences to build up credit risk models in SAS/STAT® especially PROC NLMIXED. Further 
study will be conducted based on the existing findings. 


 

 





