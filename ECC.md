Industry Equity Cost of Capital
================
Mike Aguilar, Bob Connolly, and Jiaxi Li

1. Introduction
---------------

In 1997, Fama and French attempted to calculate the equity cost of capital (ECC) for the industry portfolios. They employed the CAPM and Fama French three-factor model and applied various techniques to estimate the factor loadings. The conclusion was the ECC estimation is not reliable due to the imprecise factor risk premium and the uncertain risk loadings. It has been 23 years and we will try to find a possible improvement of the ECC estimation in this paper.

For the model selection, we will apply the Fama French five-factor model (2013) and the PRS five-factor model (2018). Since the five-factor model is an update of the three-factor model, it should work better than the three-factor model. Pukthuanthong et al. (2018) showed that there are 5 factors are reasonable: the market factor, profitability factor, and traded version of credit spread, term spread, and unexpected inflation. We will also use their result to form the Industry Equity Cost of Capital.

We will use the 5-year rolling window to estimate the factor loadings of the ECC. Many other methods such as Bayes shrinkage, and Levi-Welch (2017) method. Levi and Welch tried to estimate the ECC while focusing on the factor exposure estimation and let the reader choose their own methods of expected factor premium. However, we found that the factor risk premiums is the more important piece in ECC estimation. In this paper, we will focus on finding a way to estimate the expected factor premium better.

Many papers mentioned that the expected factor premiums are evolving. We will therefore apply the Fama Macbeth (1973) method to estimate the expected factor premium. Since the 2nd step regression result is extremely volatile, we will apply the STL filtering to smooth the result.

2. Data
-------

We get the monthly industry return, Fama French five-factor, and the risk-free rate for the Fama French five factors data from the [Ken French Data Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html). The market factor and profitability factor of the PRS five factors are from the Fama French five factors. The other 3 traded macro factors and risk-free rates are extracted from the [Federal Reserve Bank of St. Louis Economic Data (FRED)](https://fred.stlouisfed.org/) and constructed based on Pukthuanthong et al. (2018).

2.1 Industry Return and Fama French Five Factors
================================================

The [Fama French Five Factors](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html) are simple returns from July 1963 to June 2020. They are as follows: Rm-Rf, SMB, HML, RMW, CMA. The 49 Industry Portfolios are value-weighted simple returns July 1926 to June 2020. The 49 Industry Portfolios without any missing values started in July 1969, so we will start the analysis in July 1969. The risk-free rate is one-month Treasury bill rate.

2.2 Traded PRS Five Factors
===========================

In order to construct the traded version of PRS Factor, we first obtain the risk-free rate and the raw CRR Five Factors: the Default Premium (dDP), the Industrial Production Growth Rate (dIP), the Term Premium (dTS), the Unexpected Inflation (UNEXPI), and the Change in Expected Inflation (dEI). We obtained following macro variables from the Federal Reserve Bank of St. Louis Economic Data: [Moody's Seasoned Aaa Corporate Bond Yield (Aaa)](https://fred.stlouisfed.org/series/AAA), [Moody's Seasoned Baa Corporate Bond Yield (Baa)](https://fred.stlouisfed.org/series/BAA), [Industrial Production Index (IP)](https://fred.stlouisfed.org/series/INDPRO), [10-Year Treasury Constant Maturity Rate (GS10)](https://fred.stlouisfed.org/series/GS10), [1-Year Treasury Constant Maturity Rate (GS1)](https://fred.stlouisfed.org/series/GS1), [Seasonally Adjusted CPI derived Inflation Rate (INF)](https://fred.stlouisfed.org/series/CPIAUCSL), [University of Michigan Inflation Expectation (MICH)](https://fred.stlouisfed.org/series/MICH), [3-Month Treasury Bill: Secondary Market Rate (TB3MS)](https://fred.stlouisfed.org/series/TB3MS).

Here are the ways that the raw factors are calculated:

*d**D**P*<sub>*r**a**w*, *t*</sub> = *B**a**a*<sub>*t*</sub> − *A**a**a*<sub>*t*</sub>

*d**I**P*<sub>*r**a**w*, *t*</sub> = *l**n*(*I**P*<sub>*t*</sub>)−*l**n*(*I**P*<sub>*t* − 1</sub>)

*d**T**S*<sub>*r**a**w*, *t*</sub> = *G**S*10<sub>*t*</sub> − *G**S*1<sub>*t*</sub>

*E**X**P**I**N**F*<sub>*r**a**w*, *t*</sub> = *E*<sub>*t* − 12</sub>\[*M**I**C**H*<sub>*t*</sub>\]

*U**N**E**X**P**I*<sub>*r**a**w*, *t*</sub> = *I**N**F*<sub>*t*</sub> − *E**X**P**I**N**F*<sub>*r**a**w*, *t*</sub>

*d**E**I*<sub>*t*</sub> = *E**X**P**I**N**F*<sub>*r**a**w*, *t*</sub> − *E**X**P**I**N**F*<sub>*r**a**w*, *t* − 1</sub>

The Default Premium started in Janurary 1919; the Industrial Production Growth Rate stared in Feburary 1919; the Term Premium started in April 1953; the Unexpected Inflation started in Janurary 1979; and the Change in Expected Inflation started in Feburary 1979; 3-Month Treasury Bill: Secondary Market Rate (TB3MS) started in Janurary 1934. Therefore, the raw PRS factors would start in Feburary 1979. The Default Premium (dDP), the Term Premium (dTS), the Unexpected Inflation (UNEXPI), the Change in Expected Inflation (dEI), and 3-month Treasury Rate are annual rates so they need to be converted to monthly frequency.

After obtaining the raw factors, we need to create the traded version of these 5 factors. Similar to the Pukthuanthong et al. (2018) procedure, we applied the 50 portfolios, *R*, (the ten equal-weighted size portfolios, ten equal-weighted book-to-market portfolios, ten equal-weighted investment portfolios and ten equal-weighted operating profitability portfolios, and ten value-weighted momentum portfolios) from the [Ken French Data Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html) to construct the mimicking portfolios. These 50 portfolios all exist after July 1963. We first regress each of the 50 assets against the raw factors to get the coefficient matrix B (50x5) and the diagonal matrix of the covariance matrix of the error term V (50x50). The weight of the factor mimicking portfolio is *w* = (*B*′*V*<sup>−1</sup>*B*)<sup>−1</sup>*B*′*V*<sup>−1</sup>. The traded factors are *P**R**S* = *w**R*, and they would start in July 1963.
