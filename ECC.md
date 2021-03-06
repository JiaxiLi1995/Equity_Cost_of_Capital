Industry Equity Cost of Capital
================
Mike Aguilar, Bob Connolly, and Jiaxi Li

  - [S1 Introduction](#s1-introduction)
  - [S2 Data](#s2-data)
      - [S2-1 Industry Return and Fama French Five
        Factors](#s2-1-industry-return-and-fama-french-five-factors)
      - [S2-2 Traded PRS Five Factors](#s2-2-traded-prs-five-factors)
  - [S3 First-Pass Regression](#s3-first-pass-regression)
      - [S3-1 Fama French Five Factor
        Model](#s3-1-fama-french-five-factor-model)
          - [S3-1-1 Full Sample
            Estimation](#s3-1-1-full-sample-estimation)
          - [S3-1-2 Rolling Window
            Estimation](#s3-1-2-rolling-window-estimation)
          - [S3-1-3 Full Sample Estimation with STL
            Trend](#s3-1-3-full-sample-estimation-with-stl-trend)
          - [S3-1-4 Rolling Window Estimation with STL
            Trend](#s3-1-4-rolling-window-estimation-with-stl-trend)
          - [S3-1-5 Full Sample Estimation with Panel
            Regression](#s3-1-5-full-sample-estimation-with-panel-regression)
          - [S3-1-6 Rolling Window Estimation with Panel
            Regression](#s3-1-6-rolling-window-estimation-with-panel-regression)
      - [S3-2 PRS Five Factor Model](#s3-2-prs-five-factor-model)
          - [S3-2-1 Full Sample
            Estimation](#s3-2-1-full-sample-estimation)
          - [S3-2-2 Rolling Window
            Estimation](#s3-2-2-rolling-window-estimation)
          - [S3-2-3 Full Sample Estimation with STL
            Trend](#s3-2-3-full-sample-estimation-with-stl-trend)
          - [S3-2-4 Rolling Window Estimation with STL
            Trend](#s3-2-4-rolling-window-estimation-with-stl-trend)
  - [S4 Factor Premium Estimation](#s4-factor-premium-estimation)
      - [S4-1 Arithmetic Mean](#s4-1-arithmetic-mean)
      - [S4-2 Geometric Mean](#s4-2-geometric-mean)
      - [S4-3 Fama Macbeth Second Step
        Regression](#s4-3-fama-macbeth-second-step-regression)
      - [S4-4 Fama Macbeth Second Step Regression with STL Deseaoned
        Data](#s4-4-fama-macbeth-second-step-regression-with-stl-deseaoned-data)
          - [S4-4-1 STL Filtering](#s4-4-1-stl-filtering)
          - [S4-4-2 Filtered Seasonality and Trend
            Strength](#s4-4-2-filtered-seasonality-and-trend-strength)
          - [S4-4-3 Beta Decomposition](#s4-4-3-beta-decomposition)
          - [S4-4-4 Filtered Second Pass
            Regression](#s4-4-4-filtered-second-pass-regression)
          - [S4-4-5 Regression Standard
            Error](#s4-4-5-regression-standard-error)
          - [S4-4-6 Unfiltered and Filtered
            Lambdas](#s4-4-6-unfiltered-and-filtered-lambdas)
          - [S4-4-7 KS test and Stats](#s4-4-7-ks-test-and-stats)
      - [S4-5 Why filtering might improve Esimated
        Lamdba?](#s4-5-why-filtering-might-improve-esimated-lamdba)
          - [S4-5-1 Biased Regression](#s4-5-1-biased-regression)
          - [S4-5-2 Simulation](#s4-5-2-simulation)
              - [S4-5-2-1 Simulation with Random Parameters and Sin
                Lamdba](#s4-5-2-1-simulation-with-random-parameters-and-sin-lamdba)
              - [S4-5-2-2 Simulation with Random Parameter and Random
                Smooth
                Lambda](#s4-5-2-2-simulation-with-random-parameter-and-random-smooth-lambda)
              - [S4-5-2-3 Simulation with Actual Parameters and Smooth
                Lambdas](#s4-5-2-3-simulation-with-actual-parameters-and-smooth-lambdas)
              - [S4-5-2-4 Regression Analysis of Simulation
                Results](#s4-5-2-4-regression-analysis-of-simulation-results)
  - [S5 Equity Cost of Captial](#s5-equity-cost-of-captial)
      - [S5-1 Estimated Equity Cost of
        Captial](#s5-1-estimated-equity-cost-of-captial)
          - [S5-1-1 Arithmetic Mean](#s5-1-1-arithmetic-mean)
          - [S5-1-2 Geometric Mean](#s5-1-2-geometric-mean)
          - [S5-1-3 Fama Macbeth Second Step
            Regression](#s5-1-3-fama-macbeth-second-step-regression)
          - [S5-1-4 Fama Macbeth Second Step Regression with STL Trend
            Data](#s5-1-4-fama-macbeth-second-step-regression-with-stl-trend-data)
      - [S5-2 Comparative Statics](#s5-2-comparative-statics)
      - [S5-3 Bootstrap Standard Error](#s5-3-bootstrap-standard-error)
      - [S5-4 Decomposition of the Equity Cost of
        Captial](#s5-4-decomposition-of-the-equity-cost-of-captial)
      - [S5-5 Forcasting???](#s5-5-forcasting)
      - [S5-6 ECC with Consumption
        Growth???](#s5-6-ecc-with-consumption-growth)
      - [S5-7 Improve AM GM with Markov-switching
        model???](#s5-7-improve-am-gm-with-markov-switching-model)
      - [S5-8 Levi-Welch Beta???](#s5-8-levi-welch-beta)
      - [S5-9 Filtering Method in Other Second-pass
        Regression???](#s5-9-filtering-method-in-other-second-pass-regression)

# S1 Introduction

In 1997, Fama and French attempted to calculate the equity cost of
capital (ECC) for the industry portfolios. They employed the CAPM and
Fama French three-factor model and applied various techniques to
estimate the factor loadings. The conclusion was the ECC estimation is
not reliable due to the imprecise factor risk premium and the uncertain
risk loadings. It has been 23 years and we will try to find a possible
improvement of the ECC estimation in this paper.

For the model selection, we will apply the Fama French five-factor model
(2013) and the PRS five-factor model (2018). Since the five-factor model
is an update of the three-factor model, it should work better than the
three-factor model. Pukthuanthong et al. (2018) showed that there are 5
factors are reasonable: the market factor, profitability factor, and
traded version of credit spread, term spread, and unexpected inflation.
We will also use their result to form the Industry Equity Cost of
Capital.

We will use the 5-year rolling window to estimate the factor loadings of
the ECC. Many other methods such as Bayes shrinkage, and Levi-Welch
(2017) method. Levi and Welch tried to estimate the ECC while focusing
on the factor exposure estimation and let the reader choose their own
methods of expected factor premium. However, we found that the factor
risk premiums is the more important piece in ECC estimation. In this
paper, we will focus on finding a way to estimate the expected factor
premium better.

Many papers mentioned that the expected factor premiums are evolving. We
will therefore apply the Fama Macbeth (1973) method to estimate the
expected factor premium. Since the 2nd step regression result is
extremely volatile, we will apply the STL filtering to smooth the
result.

# S2 Data

We get the monthly industry return, Fama French five-factor, and the
risk-free rate for the Fama French five factors data from the [Ken
French Data
Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html).
The market factor and profitability factor of the PRS five factors are
from the Fama French five factors. The other 3 traded macro factors and
risk-free rates are extracted from the [Federal Reserve Bank of
St. Louis Economic Data (FRED)](https://fred.stlouisfed.org/) and
constructed based on Pukthuanthong et al. (2018).

## S2-1 Industry Return and Fama French Five Factors

The [Fama French Five
Factors](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)
are simple returns from July 1963 to June 2020. They are as follows:
Rm-Rf, SMB, HML, RMW, CMA. The 49 Industry Portfolios are value-weighted
simple returns July 1926 to June 2020. The 49 Industry Portfolios
without any missing values started in July 1969, so we will start the
analysis in July 1969. The risk-free rate is one-month Treasury bill
rate.

## S2-2 Traded PRS Five Factors

In order to construct the traded version of PRS Factor, we first obtain
the risk-free rate and the raw CRR Five Factors: the Default Premium
(dDP), the Industrial Production Growth Rate (dIP), the Term Premium
(dTS), the Unexpected Inflation (UNEXPI), and the Change in Expected
Inflation (dEI). We obtained following macro variables from the Federal
Reserve Bank of St. Louis Economic Data: [Moody’s Seasoned Aaa Corporate
Bond Yield (Aaa)](https://fred.stlouisfed.org/series/AAA), [Moody’s
Seasoned Baa Corporate Bond Yield
(Baa)](https://fred.stlouisfed.org/series/BAA), [Industrial Production
Index (IP)](https://fred.stlouisfed.org/series/INDPRO), [10-Year
Treasury Constant Maturity Rate
(GS10)](https://fred.stlouisfed.org/series/GS10), [1-Year Treasury
Constant Maturity Rate (GS1)](https://fred.stlouisfed.org/series/GS1),
[Seasonally Adjusted CPI derived Inflation Rate
(INF)](https://fred.stlouisfed.org/series/CPIAUCSL), [University of
Michigan Inflation Expectation
(MICH)](https://fred.stlouisfed.org/series/MICH), [3-Month Treasury
Bill: Secondary Market Rate
(TB3MS)](https://fred.stlouisfed.org/series/TB3MS).

Here are the ways that the raw factors are calculated:

  
![dDP\_{raw,t} = Baa\_t -
Aaa\_t](https://latex.codecogs.com/png.latex?dDP_%7Braw%2Ct%7D%20%3D%20Baa_t%20-%20Aaa_t
"dDP_{raw,t} = Baa_t - Aaa_t")  

  
![dIP\_{raw, t} = ln(IP\_t) -
ln(IP\_{t-1})](https://latex.codecogs.com/png.latex?dIP_%7Braw%2C%20t%7D%20%3D%20ln%28IP_t%29%20-%20ln%28IP_%7Bt-1%7D%29
"dIP_{raw, t} = ln(IP_t) - ln(IP_{t-1})")  

  
![dTS\_{raw, t} = GS10\_t -
GS1\_t](https://latex.codecogs.com/png.latex?dTS_%7Braw%2C%20t%7D%20%3D%20GS10_t%20-%20GS1_t
"dTS_{raw, t} = GS10_t - GS1_t")  

  
![EXPINF\_{raw, t} =
E\_{t-12}\[MICH\_t\]](https://latex.codecogs.com/png.latex?EXPINF_%7Braw%2C%20t%7D%20%3D%20E_%7Bt-12%7D%5BMICH_t%5D
"EXPINF_{raw, t} = E_{t-12}[MICH_t]")  

  
![UNEXPI\_{raw, t} = INF\_t - EXPINF\_{raw,
t}](https://latex.codecogs.com/png.latex?UNEXPI_%7Braw%2C%20t%7D%20%3D%20INF_t%20-%20EXPINF_%7Braw%2C%20t%7D
"UNEXPI_{raw, t} = INF_t - EXPINF_{raw, t}")  

  
![dEI\_t = EXPINF\_{raw, t} - EXPINF\_{raw,
t-1}](https://latex.codecogs.com/png.latex?dEI_t%20%3D%20EXPINF_%7Braw%2C%20t%7D%20-%20EXPINF_%7Braw%2C%20t-1%7D
"dEI_t = EXPINF_{raw, t} - EXPINF_{raw, t-1}")  

The Default Premium started in Janurary 1919; the Industrial Production
Growth Rate stared in Feburary 1919; the Term Premium started in April
1953; the Unexpected Inflation started in Janurary 1979; and the Change
in Expected Inflation started in Feburary 1979; 3-Month Treasury Bill:
Secondary Market Rate (TB3MS) started in Janurary 1934. Therefore, the
raw PRS factors would start in Feburary 1979. The Default Premium (dDP),
the Term Premium (dTS), the Unexpected Inflation (UNEXPI), the Change in
Expected Inflation (dEI), and 3-month Treasury Rate are annual rates so
they need to be converted to monthly frequency.

After obtaining the raw factors, we need to create the traded version of
these 5 factors. Similar to the Pukthuanthong et al. (2018) procedure,
we applied the 50 portfolios,
![R](https://latex.codecogs.com/png.latex?R "R"), (the ten
equal-weighted size portfolios, ten equal-weighted book-to-market
portfolios, ten equal-weighted investment portfolios and ten
equal-weighted operating profitability portfolios, and ten
value-weighted momentum portfolios) from the [Ken French Data
Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)
to construct the mimicking portfolios. These 50 portfolios all exist
after July 1963. We first regress each of the 50 assets against the raw
factors to get the coefficient matrix B (50x5) and the diagonal matrix
of the covariance matrix of the error term V (50x50). The weight of the
factor mimicking portfolio is
![w=(B'V^{-1}B)^{-1}B'V^{-1}](https://latex.codecogs.com/png.latex?w%3D%28B%27V%5E%7B-1%7DB%29%5E%7B-1%7DB%27V%5E%7B-1%7D
"w=(B'V^{-1}B)^{-1}B'V^{-1}"). The traded factors are PRS = wR, and they
would start in July 1963.

# S3 First-Pass Regression

In this section, we will try to apply the simple first-pass regression
to estimate the betas of the 49 industry portfolios. The period would be
from July 1969 to June 2020. Since the focus of this paper is about the
factor risk premium estimation, we will use the most basic first pass
regressions (full sample and 5-year rolling window) to estimate the
betas and compare which lambda method would work better.

## S3-1 Fama French Five Factor Model

We will first apply the Fama French Five Factor Model to estimate the
betas. We will use the Five Factor Model as the base model.

### S3-1-1 Full Sample Estimation

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama French Five Factors

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Coefficients

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Std. Error

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

Aero

</td>

<td style="text-align:center;">

\-0.0017060

</td>

<td style="text-align:center;">

1.2085983

</td>

<td style="text-align:center;">

0.2931223

</td>

<td style="text-align:center;">

0.2753853

</td>

<td style="text-align:center;">

0.4994864

</td>

<td style="text-align:center;">

0.0879383

</td>

<td style="text-align:center;">

0.0017527

</td>

<td style="text-align:center;">

0.0418819

</td>

<td style="text-align:center;">

0.0607440

</td>

<td style="text-align:center;">

0.0786255

</td>

<td style="text-align:center;">

0.0832089

</td>

<td style="text-align:center;">

0.1241392

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Agric

</td>

<td style="text-align:center;">

\-0.0003846

</td>

<td style="text-align:center;">

0.8254045

</td>

<td style="text-align:center;">

0.4258726

</td>

<td style="text-align:center;">

\-0.0810419

</td>

<td style="text-align:center;">

0.2175820

</td>

<td style="text-align:center;">

0.1406175

</td>

<td style="text-align:center;">

0.0020985

</td>

<td style="text-align:center;">

0.0501455

</td>

<td style="text-align:center;">

0.0727292

</td>

<td style="text-align:center;">

0.0941389

</td>

<td style="text-align:center;">

0.0996267

</td>

<td style="text-align:center;">

0.1486328

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Autos

</td>

<td style="text-align:center;">

\-0.0036580

</td>

<td style="text-align:center;">

1.2273182

</td>

<td style="text-align:center;">

0.2149694

</td>

<td style="text-align:center;">

0.5925738

</td>

<td style="text-align:center;">

0.0694061

</td>

<td style="text-align:center;">

0.0348842

</td>

<td style="text-align:center;">

0.0018550

</td>

<td style="text-align:center;">

0.0443260

</td>

<td style="text-align:center;">

0.0642888

</td>

<td style="text-align:center;">

0.0832137

</td>

<td style="text-align:center;">

0.0880647

</td>

<td style="text-align:center;">

0.1313835

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Banks

</td>

<td style="text-align:center;">

\-0.0015445

</td>

<td style="text-align:center;">

1.1722823

</td>

<td style="text-align:center;">

\-0.1066541

</td>

<td style="text-align:center;">

0.8167257

</td>

<td style="text-align:center;">

0.1229449

</td>

<td style="text-align:center;">

\-0.3985589

</td>

<td style="text-align:center;">

0.0012937

</td>

<td style="text-align:center;">

0.0309150

</td>

<td style="text-align:center;">

0.0448380

</td>

<td style="text-align:center;">

0.0580372

</td>

<td style="text-align:center;">

0.0614205

</td>

<td style="text-align:center;">

0.0916330

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Beer

</td>

<td style="text-align:center;">

\-0.0000880

</td>

<td style="text-align:center;">

0.8635333

</td>

<td style="text-align:center;">

\-0.0050819

</td>

<td style="text-align:center;">

\-0.1625288

</td>

<td style="text-align:center;">

0.6717286

</td>

<td style="text-align:center;">

0.4416518

</td>

<td style="text-align:center;">

0.0015715

</td>

<td style="text-align:center;">

0.0375532

</td>

<td style="text-align:center;">

0.0544658

</td>

<td style="text-align:center;">

0.0704991

</td>

<td style="text-align:center;">

0.0746089

</td>

<td style="text-align:center;">

0.1113088

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BldMt

</td>

<td style="text-align:center;">

\-0.0039339

</td>

<td style="text-align:center;">

1.2552070

</td>

<td style="text-align:center;">

0.3907534

</td>

<td style="text-align:center;">

0.3157648

</td>

<td style="text-align:center;">

0.4904084

</td>

<td style="text-align:center;">

0.2082103

</td>

<td style="text-align:center;">

0.0012156

</td>

<td style="text-align:center;">

0.0290481

</td>

<td style="text-align:center;">

0.0421303

</td>

<td style="text-align:center;">

0.0545323

</td>

<td style="text-align:center;">

0.0577113

</td>

<td style="text-align:center;">

0.0860993

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Books

</td>

<td style="text-align:center;">

\-0.0038772

</td>

<td style="text-align:center;">

1.0984117

</td>

<td style="text-align:center;">

0.3571583

</td>

<td style="text-align:center;">

0.2266649

</td>

<td style="text-align:center;">

0.4282332

</td>

<td style="text-align:center;">

0.0268060

</td>

<td style="text-align:center;">

0.0013279

</td>

<td style="text-align:center;">

0.0317302

</td>

<td style="text-align:center;">

0.0460204

</td>

<td style="text-align:center;">

0.0595676

</td>

<td style="text-align:center;">

0.0630401

</td>

<td style="text-align:center;">

0.0940494

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Boxes

</td>

<td style="text-align:center;">

\-0.0002691

</td>

<td style="text-align:center;">

0.9980460

</td>

<td style="text-align:center;">

\-0.0347087

</td>

<td style="text-align:center;">

0.1279435

</td>

<td style="text-align:center;">

0.2836173

</td>

<td style="text-align:center;">

\-0.0943480

</td>

<td style="text-align:center;">

0.0015530

</td>

<td style="text-align:center;">

0.0371104

</td>

<td style="text-align:center;">

0.0538236

</td>

<td style="text-align:center;">

0.0696680

</td>

<td style="text-align:center;">

0.0737293

</td>

<td style="text-align:center;">

0.1099965

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BusSv

</td>

<td style="text-align:center;">

\-0.0004619

</td>

<td style="text-align:center;">

1.0772166

</td>

<td style="text-align:center;">

0.4047467

</td>

<td style="text-align:center;">

\-0.1044015

</td>

<td style="text-align:center;">

0.1547087

</td>

<td style="text-align:center;">

\-0.0578629

</td>

<td style="text-align:center;">

0.0008560

</td>

<td style="text-align:center;">

0.0204539

</td>

<td style="text-align:center;">

0.0296656

</td>

<td style="text-align:center;">

0.0383984

</td>

<td style="text-align:center;">

0.0406368

</td>

<td style="text-align:center;">

0.0606260

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chems

</td>

<td style="text-align:center;">

\-0.0024657

</td>

<td style="text-align:center;">

1.1597086

</td>

<td style="text-align:center;">

0.0465431

</td>

<td style="text-align:center;">

0.2367452

</td>

<td style="text-align:center;">

0.3082250

</td>

<td style="text-align:center;">

0.2301914

</td>

<td style="text-align:center;">

0.0012458

</td>

<td style="text-align:center;">

0.0297682

</td>

<td style="text-align:center;">

0.0431747

</td>

<td style="text-align:center;">

0.0558843

</td>

<td style="text-align:center;">

0.0591421

</td>

<td style="text-align:center;">

0.0882339

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chips

</td>

<td style="text-align:center;">

0.0039846

</td>

<td style="text-align:center;">

1.1798212

</td>

<td style="text-align:center;">

0.2389137

</td>

<td style="text-align:center;">

\-0.3144479

</td>

<td style="text-align:center;">

\-0.5561211

</td>

<td style="text-align:center;">

\-0.3200445

</td>

<td style="text-align:center;">

0.0015209

</td>

<td style="text-align:center;">

0.0363424

</td>

<td style="text-align:center;">

0.0527097

</td>

<td style="text-align:center;">

0.0682262

</td>

<td style="text-align:center;">

0.0722034

</td>

<td style="text-align:center;">

0.1077201

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Clths

</td>

<td style="text-align:center;">

\-0.0023532

</td>

<td style="text-align:center;">

1.1145901

</td>

<td style="text-align:center;">

0.5484879

</td>

<td style="text-align:center;">

0.3320528

</td>

<td style="text-align:center;">

0.6946888

</td>

<td style="text-align:center;">

\-0.1286381

</td>

<td style="text-align:center;">

0.0016247

</td>

<td style="text-align:center;">

0.0388233

</td>

<td style="text-align:center;">

0.0563079

</td>

<td style="text-align:center;">

0.0728835

</td>

<td style="text-align:center;">

0.0771323

</td>

<td style="text-align:center;">

0.1150735

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Cnstr

</td>

<td style="text-align:center;">

\-0.0043263

</td>

<td style="text-align:center;">

1.2827549

</td>

<td style="text-align:center;">

0.5336958

</td>

<td style="text-align:center;">

0.2138833

</td>

<td style="text-align:center;">

0.3989391

</td>

<td style="text-align:center;">

0.0171826

</td>

<td style="text-align:center;">

0.0017163

</td>

<td style="text-align:center;">

0.0410122

</td>

<td style="text-align:center;">

0.0594826

</td>

<td style="text-align:center;">

0.0769928

</td>

<td style="text-align:center;">

0.0814811

</td>

<td style="text-align:center;">

0.1215614

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Coal

</td>

<td style="text-align:center;">

\-0.0038319

</td>

<td style="text-align:center;">

1.1819738

</td>

<td style="text-align:center;">

0.4471589

</td>

<td style="text-align:center;">

0.2479553

</td>

<td style="text-align:center;">

0.0066664

</td>

<td style="text-align:center;">

0.2912234

</td>

<td style="text-align:center;">

0.0039763

</td>

<td style="text-align:center;">

0.0950160

</td>

<td style="text-align:center;">

0.1378078

</td>

<td style="text-align:center;">

0.1783749

</td>

<td style="text-align:center;">

0.1887733

</td>

<td style="text-align:center;">

0.2816303

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Drugs

</td>

<td style="text-align:center;">

0.0017628

</td>

<td style="text-align:center;">

0.8716268

</td>

<td style="text-align:center;">

\-0.2811213

</td>

<td style="text-align:center;">

\-0.5057393

</td>

<td style="text-align:center;">

0.2873540

</td>

<td style="text-align:center;">

0.4640041

</td>

<td style="text-align:center;">

0.0013488

</td>

<td style="text-align:center;">

0.0322301

</td>

<td style="text-align:center;">

0.0467453

</td>

<td style="text-align:center;">

0.0605060

</td>

<td style="text-align:center;">

0.0640332

</td>

<td style="text-align:center;">

0.0955309

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

ElcEq

</td>

<td style="text-align:center;">

0.0002728

</td>

<td style="text-align:center;">

1.2175987

</td>

<td style="text-align:center;">

0.0801531

</td>

<td style="text-align:center;">

0.0226345

</td>

<td style="text-align:center;">

0.1260678

</td>

<td style="text-align:center;">

0.0175188

</td>

<td style="text-align:center;">

0.0013435

</td>

<td style="text-align:center;">

0.0321036

</td>

<td style="text-align:center;">

0.0465619

</td>

<td style="text-align:center;">

0.0602686

</td>

<td style="text-align:center;">

0.0637820

</td>

<td style="text-align:center;">

0.0951561

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FabPr

</td>

<td style="text-align:center;">

\-0.0038979

</td>

<td style="text-align:center;">

1.0036897

</td>

<td style="text-align:center;">

0.7297908

</td>

<td style="text-align:center;">

0.3474556

</td>

<td style="text-align:center;">

0.2546453

</td>

<td style="text-align:center;">

\-0.3305400

</td>

<td style="text-align:center;">

0.0021110

</td>

<td style="text-align:center;">

0.0504432

</td>

<td style="text-align:center;">

0.0731610

</td>

<td style="text-align:center;">

0.0946978

</td>

<td style="text-align:center;">

0.1002182

</td>

<td style="text-align:center;">

0.1495152

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fin

</td>

<td style="text-align:center;">

0.0019238

</td>

<td style="text-align:center;">

1.1770110

</td>

<td style="text-align:center;">

0.0106150

</td>

<td style="text-align:center;">

0.4035061

</td>

<td style="text-align:center;">

\-0.4091644

</td>

<td style="text-align:center;">

\-0.3845337

</td>

<td style="text-align:center;">

0.0011090

</td>

<td style="text-align:center;">

0.0265001

</td>

<td style="text-align:center;">

0.0384348

</td>

<td style="text-align:center;">

0.0497490

</td>

<td style="text-align:center;">

0.0526491

</td>

<td style="text-align:center;">

0.0785471

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Food

</td>

<td style="text-align:center;">

\-0.0003939

</td>

<td style="text-align:center;">

0.8133815

</td>

<td style="text-align:center;">

\-0.0524832

</td>

<td style="text-align:center;">

\-0.0945994

</td>

<td style="text-align:center;">

0.5802765

</td>

<td style="text-align:center;">

0.5053513

</td>

<td style="text-align:center;">

0.0012587

</td>

<td style="text-align:center;">

0.0300785

</td>

<td style="text-align:center;">

0.0436247

</td>

<td style="text-align:center;">

0.0564667

</td>

<td style="text-align:center;">

0.0597585

</td>

<td style="text-align:center;">

0.0891535

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fun

</td>

<td style="text-align:center;">

0.0018343

</td>

<td style="text-align:center;">

1.2499559

</td>

<td style="text-align:center;">

0.4911755

</td>

<td style="text-align:center;">

0.1628531

</td>

<td style="text-align:center;">

0.2417360

</td>

<td style="text-align:center;">

\-0.2880831

</td>

<td style="text-align:center;">

0.0019544

</td>

<td style="text-align:center;">

0.0467018

</td>

<td style="text-align:center;">

0.0677346

</td>

<td style="text-align:center;">

0.0876739

</td>

<td style="text-align:center;">

0.0927848

</td>

<td style="text-align:center;">

0.1384255

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Gold

</td>

<td style="text-align:center;">

0.0011335

</td>

<td style="text-align:center;">

0.5837386

</td>

<td style="text-align:center;">

0.3634198

</td>

<td style="text-align:center;">

\-0.2602619

</td>

<td style="text-align:center;">

0.0036185

</td>

<td style="text-align:center;">

0.5086043

</td>

<td style="text-align:center;">

0.0044154

</td>

<td style="text-align:center;">

0.1055100

</td>

<td style="text-align:center;">

0.1530279

</td>

<td style="text-align:center;">

0.1980754

</td>

<td style="text-align:center;">

0.2096222

</td>

<td style="text-align:center;">

0.3127349

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Guns

</td>

<td style="text-align:center;">

0.0006980

</td>

<td style="text-align:center;">

0.9055074

</td>

<td style="text-align:center;">

0.3202853

</td>

<td style="text-align:center;">

0.2902131

</td>

<td style="text-align:center;">

0.7185617

</td>

<td style="text-align:center;">

0.1268888

</td>

<td style="text-align:center;">

0.0021436

</td>

<td style="text-align:center;">

0.0512228

</td>

<td style="text-align:center;">

0.0742917

</td>

<td style="text-align:center;">

0.0961613

</td>

<td style="text-align:center;">

0.1017670

</td>

<td style="text-align:center;">

0.1518259

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hardw

</td>

<td style="text-align:center;">

0.0032294

</td>

<td style="text-align:center;">

1.0267954

</td>

<td style="text-align:center;">

\-0.0011180

</td>

<td style="text-align:center;">

\-0.3041928

</td>

<td style="text-align:center;">

\-0.5806640

</td>

<td style="text-align:center;">

\-0.4430579

</td>

<td style="text-align:center;">

0.0017661

</td>

<td style="text-align:center;">

0.0422015

</td>

<td style="text-align:center;">

0.0612076

</td>

<td style="text-align:center;">

0.0792255

</td>

<td style="text-align:center;">

0.0838440

</td>

<td style="text-align:center;">

0.1250866

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hlth

</td>

<td style="text-align:center;">

\-0.0039421

</td>

<td style="text-align:center;">

1.0854593

</td>

<td style="text-align:center;">

0.8942400

</td>

<td style="text-align:center;">

\-0.0598781

</td>

<td style="text-align:center;">

1.0988021

</td>

<td style="text-align:center;">

0.0571197

</td>

<td style="text-align:center;">

0.0023503

</td>

<td style="text-align:center;">

0.0561630

</td>

<td style="text-align:center;">

0.0814568

</td>

<td style="text-align:center;">

0.1054356

</td>

<td style="text-align:center;">

0.1115819

</td>

<td style="text-align:center;">

0.1664688

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hshld

</td>

<td style="text-align:center;">

\-0.0020860

</td>

<td style="text-align:center;">

0.8901395

</td>

<td style="text-align:center;">

\-0.0414269

</td>

<td style="text-align:center;">

\-0.1871243

</td>

<td style="text-align:center;">

0.5605051

</td>

<td style="text-align:center;">

0.3581377

</td>

<td style="text-align:center;">

0.0011536

</td>

<td style="text-align:center;">

0.0275659

</td>

<td style="text-align:center;">

0.0399806

</td>

<td style="text-align:center;">

0.0517499

</td>

<td style="text-align:center;">

0.0547667

</td>

<td style="text-align:center;">

0.0817063

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Insur

</td>

<td style="text-align:center;">

\-0.0004908

</td>

<td style="text-align:center;">

1.0621447

</td>

<td style="text-align:center;">

\-0.1112492

</td>

<td style="text-align:center;">

0.3811060

</td>

<td style="text-align:center;">

0.1961882

</td>

<td style="text-align:center;">

0.0288185

</td>

<td style="text-align:center;">

0.0013260

</td>

<td style="text-align:center;">

0.0316868

</td>

<td style="text-align:center;">

0.0459574

</td>

<td style="text-align:center;">

0.0594861

</td>

<td style="text-align:center;">

0.0629538

</td>

<td style="text-align:center;">

0.0939206

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

LabEq

</td>

<td style="text-align:center;">

0.0011405

</td>

<td style="text-align:center;">

1.1592554

</td>

<td style="text-align:center;">

0.4285268

</td>

<td style="text-align:center;">

\-0.5027346

</td>

<td style="text-align:center;">

\-0.1441310

</td>

<td style="text-align:center;">

0.1545286

</td>

<td style="text-align:center;">

0.0014500

</td>

<td style="text-align:center;">

0.0346498

</td>

<td style="text-align:center;">

0.0502549

</td>

<td style="text-align:center;">

0.0650487

</td>

<td style="text-align:center;">

0.0688407

</td>

<td style="text-align:center;">

0.1027032

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mach

</td>

<td style="text-align:center;">

\-0.0011806

</td>

<td style="text-align:center;">

1.1894700

</td>

<td style="text-align:center;">

0.2848769

</td>

<td style="text-align:center;">

0.0982099

</td>

<td style="text-align:center;">

0.0105856

</td>

<td style="text-align:center;">

0.0159399

</td>

<td style="text-align:center;">

0.0012917

</td>

<td style="text-align:center;">

0.0308666

</td>

<td style="text-align:center;">

0.0447679

</td>

<td style="text-align:center;">

0.0579464

</td>

<td style="text-align:center;">

0.0613244

</td>

<td style="text-align:center;">

0.0914897

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Meals

</td>

<td style="text-align:center;">

\-0.0025867

</td>

<td style="text-align:center;">

1.0812673

</td>

<td style="text-align:center;">

0.3762794

</td>

<td style="text-align:center;">

\-0.0105822

</td>

<td style="text-align:center;">

0.8105843

</td>

<td style="text-align:center;">

0.1622857

</td>

<td style="text-align:center;">

0.0014646

</td>

<td style="text-align:center;">

0.0349971

</td>

<td style="text-align:center;">

0.0507585

</td>

<td style="text-align:center;">

0.0657006

</td>

<td style="text-align:center;">

0.0695306

</td>

<td style="text-align:center;">

0.1037325

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

MedEq

</td>

<td style="text-align:center;">

0.0016029

</td>

<td style="text-align:center;">

0.8744119

</td>

<td style="text-align:center;">

0.1031781

</td>

<td style="text-align:center;">

\-0.3305774

</td>

<td style="text-align:center;">

0.2731120

</td>

<td style="text-align:center;">

0.1035343

</td>

<td style="text-align:center;">

0.0013851

</td>

<td style="text-align:center;">

0.0330982

</td>

<td style="text-align:center;">

0.0480045

</td>

<td style="text-align:center;">

0.0621358

</td>

<td style="text-align:center;">

0.0657580

</td>

<td style="text-align:center;">

0.0981042

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mines

</td>

<td style="text-align:center;">

\-0.0022027

</td>

<td style="text-align:center;">

1.1386038

</td>

<td style="text-align:center;">

0.3314773

</td>

<td style="text-align:center;">

0.1934266

</td>

<td style="text-align:center;">

0.0714566

</td>

<td style="text-align:center;">

0.3088411

</td>

<td style="text-align:center;">

0.0023607

</td>

<td style="text-align:center;">

0.0564106

</td>

<td style="text-align:center;">

0.0818159

</td>

<td style="text-align:center;">

0.1059004

</td>

<td style="text-align:center;">

0.1120738

</td>

<td style="text-align:center;">

0.1672027

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Oil

</td>

<td style="text-align:center;">

\-0.0023745

</td>

<td style="text-align:center;">

1.0014272

</td>

<td style="text-align:center;">

\-0.0682213

</td>

<td style="text-align:center;">

0.2534753

</td>

<td style="text-align:center;">

0.2765152

</td>

<td style="text-align:center;">

0.3031233

</td>

<td style="text-align:center;">

0.0018314

</td>

<td style="text-align:center;">

0.0437622

</td>

<td style="text-align:center;">

0.0634711

</td>

<td style="text-align:center;">

0.0821554

</td>

<td style="text-align:center;">

0.0869447

</td>

<td style="text-align:center;">

0.1297125

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Other

</td>

<td style="text-align:center;">

\-0.0068442

</td>

<td style="text-align:center;">

1.1388078

</td>

<td style="text-align:center;">

0.2549218

</td>

<td style="text-align:center;">

0.0668335

</td>

<td style="text-align:center;">

0.1832071

</td>

<td style="text-align:center;">

0.0732465

</td>

<td style="text-align:center;">

0.0018194

</td>

<td style="text-align:center;">

0.0434749

</td>

<td style="text-align:center;">

0.0630544

</td>

<td style="text-align:center;">

0.0816160

</td>

<td style="text-align:center;">

0.0863738

</td>

<td style="text-align:center;">

0.1288608

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Paper

</td>

<td style="text-align:center;">

\-0.0030838

</td>

<td style="text-align:center;">

1.0826153

</td>

<td style="text-align:center;">

0.0947014

</td>

<td style="text-align:center;">

0.1514737

</td>

<td style="text-align:center;">

0.4096624

</td>

<td style="text-align:center;">

0.3961297

</td>

<td style="text-align:center;">

0.0013249

</td>

<td style="text-align:center;">

0.0316596

</td>

<td style="text-align:center;">

0.0459180

</td>

<td style="text-align:center;">

0.0594350

</td>

<td style="text-align:center;">

0.0628998

</td>

<td style="text-align:center;">

0.0938401

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PerSv

</td>

<td style="text-align:center;">

\-0.0067203

</td>

<td style="text-align:center;">

1.0680857

</td>

<td style="text-align:center;">

0.6052475

</td>

<td style="text-align:center;">

0.0264087

</td>

<td style="text-align:center;">

0.6561786

</td>

<td style="text-align:center;">

0.0508338

</td>

<td style="text-align:center;">

0.0017252

</td>

<td style="text-align:center;">

0.0412259

</td>

<td style="text-align:center;">

0.0597926

</td>

<td style="text-align:center;">

0.0773940

</td>

<td style="text-align:center;">

0.0819057

</td>

<td style="text-align:center;">

0.1221949

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

RlEst

</td>

<td style="text-align:center;">

\-0.0085585

</td>

<td style="text-align:center;">

1.1825155

</td>

<td style="text-align:center;">

0.9911820

</td>

<td style="text-align:center;">

0.7245494

</td>

<td style="text-align:center;">

0.4083650

</td>

<td style="text-align:center;">

\-0.2667029

</td>

<td style="text-align:center;">

0.0018547

</td>

<td style="text-align:center;">

0.0443193

</td>

<td style="text-align:center;">

0.0642791

</td>

<td style="text-align:center;">

0.0832012

</td>

<td style="text-align:center;">

0.0880514

</td>

<td style="text-align:center;">

0.1313636

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rtail

</td>

<td style="text-align:center;">

0.0001220

</td>

<td style="text-align:center;">

1.0154299

</td>

<td style="text-align:center;">

0.1914579

</td>

<td style="text-align:center;">

\-0.0531875

</td>

<td style="text-align:center;">

0.4601537

</td>

<td style="text-align:center;">

0.0368127

</td>

<td style="text-align:center;">

0.0012751

</td>

<td style="text-align:center;">

0.0304706

</td>

<td style="text-align:center;">

0.0441935

</td>

<td style="text-align:center;">

0.0572030

</td>

<td style="text-align:center;">

0.0605376

</td>

<td style="text-align:center;">

0.0903159

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rubbr

</td>

<td style="text-align:center;">

\-0.0019858

</td>

<td style="text-align:center;">

1.0381702

</td>

<td style="text-align:center;">

0.6421157

</td>

<td style="text-align:center;">

0.1301219

</td>

<td style="text-align:center;">

0.3957909

</td>

<td style="text-align:center;">

0.1384205

</td>

<td style="text-align:center;">

0.0013032

</td>

<td style="text-align:center;">

0.0311415

</td>

<td style="text-align:center;">

0.0451666

</td>

<td style="text-align:center;">

0.0584624

</td>

<td style="text-align:center;">

0.0618705

</td>

<td style="text-align:center;">

0.0923044

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Ships

</td>

<td style="text-align:center;">

\-0.0038423

</td>

<td style="text-align:center;">

1.2237949

</td>

<td style="text-align:center;">

0.3197487

</td>

<td style="text-align:center;">

0.2578553

</td>

<td style="text-align:center;">

0.5764006

</td>

<td style="text-align:center;">

0.3599753

</td>

<td style="text-align:center;">

0.0021729

</td>

<td style="text-align:center;">

0.0519227

</td>

<td style="text-align:center;">

0.0753069

</td>

<td style="text-align:center;">

0.0974753

</td>

<td style="text-align:center;">

0.1031576

</td>

<td style="text-align:center;">

0.1539006

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Smoke

</td>

<td style="text-align:center;">

0.0014748

</td>

<td style="text-align:center;">

0.8539572

</td>

<td style="text-align:center;">

\-0.1365032

</td>

<td style="text-align:center;">

\-0.2084596

</td>

<td style="text-align:center;">

0.7146263

</td>

<td style="text-align:center;">

0.8267503

</td>

<td style="text-align:center;">

0.0021751

</td>

<td style="text-align:center;">

0.0519762

</td>

<td style="text-align:center;">

0.0753844

</td>

<td style="text-align:center;">

0.0975757

</td>

<td style="text-align:center;">

0.1032638

</td>

<td style="text-align:center;">

0.1540590

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Soda

</td>

<td style="text-align:center;">

\-0.0006067

</td>

<td style="text-align:center;">

0.9415169

</td>

<td style="text-align:center;">

\-0.0162179

</td>

<td style="text-align:center;">

0.0905335

</td>

<td style="text-align:center;">

0.6206460

</td>

<td style="text-align:center;">

0.2508099

</td>

<td style="text-align:center;">

0.0021578

</td>

<td style="text-align:center;">

0.0515622

</td>

<td style="text-align:center;">

0.0747840

</td>

<td style="text-align:center;">

0.0967985

</td>

<td style="text-align:center;">

0.1024413

</td>

<td style="text-align:center;">

0.1528319

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Softw

</td>

<td style="text-align:center;">

0.0022694

</td>

<td style="text-align:center;">

1.2036278

</td>

<td style="text-align:center;">

0.9190520

</td>

<td style="text-align:center;">

\-0.3505056

</td>

<td style="text-align:center;">

0.0324944

</td>

<td style="text-align:center;">

\-0.8756008

</td>

<td style="text-align:center;">

0.0029187

</td>

<td style="text-align:center;">

0.0697435

</td>

<td style="text-align:center;">

0.1011535

</td>

<td style="text-align:center;">

0.1309305

</td>

<td style="text-align:center;">

0.1385631

</td>

<td style="text-align:center;">

0.2067220

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Steel

</td>

<td style="text-align:center;">

\-0.0038405

</td>

<td style="text-align:center;">

1.2570695

</td>

<td style="text-align:center;">

0.3171997

</td>

<td style="text-align:center;">

0.3274615

</td>

<td style="text-align:center;">

\-0.5210510

</td>

<td style="text-align:center;">

0.0716646

</td>

<td style="text-align:center;">

0.0018950

</td>

<td style="text-align:center;">

0.0452826

</td>

<td style="text-align:center;">

0.0656762

</td>

<td style="text-align:center;">

0.0850096

</td>

<td style="text-align:center;">

0.0899652

</td>

<td style="text-align:center;">

0.1342189

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Telcm

</td>

<td style="text-align:center;">

0.0013014

</td>

<td style="text-align:center;">

0.8432036

</td>

<td style="text-align:center;">

\-0.2434141

</td>

<td style="text-align:center;">

0.1086228

</td>

<td style="text-align:center;">

\-0.2459422

</td>

<td style="text-align:center;">

0.1025583

</td>

<td style="text-align:center;">

0.0012521

</td>

<td style="text-align:center;">

0.0299193

</td>

<td style="text-align:center;">

0.0433939

</td>

<td style="text-align:center;">

0.0561679

</td>

<td style="text-align:center;">

0.0594422

</td>

<td style="text-align:center;">

0.0886817

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Toys

</td>

<td style="text-align:center;">

\-0.0057075

</td>

<td style="text-align:center;">

1.1643575

</td>

<td style="text-align:center;">

0.6314689

</td>

<td style="text-align:center;">

\-0.0221004

</td>

<td style="text-align:center;">

0.6875766

</td>

<td style="text-align:center;">

0.2072822

</td>

<td style="text-align:center;">

0.0018874

</td>

<td style="text-align:center;">

0.0451021

</td>

<td style="text-align:center;">

0.0654144

</td>

<td style="text-align:center;">

0.0846707

</td>

<td style="text-align:center;">

0.0896066

</td>

<td style="text-align:center;">

0.1336839

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Trans

</td>

<td style="text-align:center;">

\-0.0027263

</td>

<td style="text-align:center;">

1.0973879

</td>

<td style="text-align:center;">

0.2882354

</td>

<td style="text-align:center;">

0.2579734

</td>

<td style="text-align:center;">

0.4191563

</td>

<td style="text-align:center;">

0.0252591

</td>

<td style="text-align:center;">

0.0013084

</td>

<td style="text-align:center;">

0.0312659

</td>

<td style="text-align:center;">

0.0453469

</td>

<td style="text-align:center;">

0.0586958

</td>

<td style="text-align:center;">

0.0621175

</td>

<td style="text-align:center;">

0.0926730

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Txtls

</td>

<td style="text-align:center;">

\-0.0055147

</td>

<td style="text-align:center;">

1.1833862

</td>

<td style="text-align:center;">

0.7780645

</td>

<td style="text-align:center;">

0.6083072

</td>

<td style="text-align:center;">

0.5672194

</td>

<td style="text-align:center;">

0.0656111

</td>

<td style="text-align:center;">

0.0019001

</td>

<td style="text-align:center;">

0.0454044

</td>

<td style="text-align:center;">

0.0658530

</td>

<td style="text-align:center;">

0.0852384

</td>

<td style="text-align:center;">

0.0902074

</td>

<td style="text-align:center;">

0.1345801

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Util

</td>

<td style="text-align:center;">

\-0.0000637

</td>

<td style="text-align:center;">

0.6404511

</td>

<td style="text-align:center;">

\-0.1488908

</td>

<td style="text-align:center;">

0.2200972

</td>

<td style="text-align:center;">

0.1418424

</td>

<td style="text-align:center;">

0.2881115

</td>

<td style="text-align:center;">

0.0013268

</td>

<td style="text-align:center;">

0.0317044

</td>

<td style="text-align:center;">

0.0459830

</td>

<td style="text-align:center;">

0.0595192

</td>

<td style="text-align:center;">

0.0629889

</td>

<td style="text-align:center;">

0.0939729

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Whlsl

</td>

<td style="text-align:center;">

\-0.0024485

</td>

<td style="text-align:center;">

1.0192465

</td>

<td style="text-align:center;">

0.5300667

</td>

<td style="text-align:center;">

\-0.0255673

</td>

<td style="text-align:center;">

0.4426080

</td>

<td style="text-align:center;">

0.1441173

</td>

<td style="text-align:center;">

0.0009947

</td>

<td style="text-align:center;">

0.0237680

</td>

<td style="text-align:center;">

0.0344722

</td>

<td style="text-align:center;">

0.0446199

</td>

<td style="text-align:center;">

0.0472211

</td>

<td style="text-align:center;">

0.0704490

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Full_FF5-1.png)<!-- -->![](ECC_files/figure-gfm/Full_FF5-2.png)<!-- -->![](ECC_files/figure-gfm/Full_FF5-3.png)<!-- -->

### S3-1-2 Rolling Window Estimation

We will show examples of the Real Estate Portfolio (RlEst), Construction
Portfolio (Cnstr), and Food Portfolio (Food) Rolling Betas evolution
here. The smoothing line is based on the loess smoothing. It seems that
the betas are evolving overtime.

![](ECC_files/figure-gfm/Rolling_FF5-1.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5-2.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5-3.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5-4.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5-5.png)<!-- -->

### S3-1-3 Full Sample Estimation with STL Trend

Here, we would try to conduct the STL decomposition before the first
step regression with full sample.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama French Five Factors

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Coefficients

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Std. Error

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

Aero

</td>

<td style="text-align:center;">

\-0.0012744

</td>

<td style="text-align:center;">

1.2746023

</td>

<td style="text-align:center;">

0.7838737

</td>

<td style="text-align:center;">

0.4368438

</td>

<td style="text-align:center;">

0.1528035

</td>

<td style="text-align:center;">

\-0.2526696

</td>

<td style="text-align:center;">

0.0005832

</td>

<td style="text-align:center;">

0.0398914

</td>

<td style="text-align:center;">

0.0505159

</td>

<td style="text-align:center;">

0.0552370

</td>

<td style="text-align:center;">

0.0617538

</td>

<td style="text-align:center;">

0.0964317

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Agric

</td>

<td style="text-align:center;">

0.0016461

</td>

<td style="text-align:center;">

0.5825164

</td>

<td style="text-align:center;">

0.1940582

</td>

<td style="text-align:center;">

0.3703844

</td>

<td style="text-align:center;">

0.4506982

</td>

<td style="text-align:center;">

\-0.6421949

</td>

<td style="text-align:center;">

0.0006801

</td>

<td style="text-align:center;">

0.0465185

</td>

<td style="text-align:center;">

0.0589079

</td>

<td style="text-align:center;">

0.0644133

</td>

<td style="text-align:center;">

0.0720127

</td>

<td style="text-align:center;">

0.1124515

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Autos

</td>

<td style="text-align:center;">

\-0.0063620

</td>

<td style="text-align:center;">

1.5229823

</td>

<td style="text-align:center;">

0.0053461

</td>

<td style="text-align:center;">

\-0.0961469

</td>

<td style="text-align:center;">

0.0515546

</td>

<td style="text-align:center;">

1.0865335

</td>

<td style="text-align:center;">

0.0006652

</td>

<td style="text-align:center;">

0.0455002

</td>

<td style="text-align:center;">

0.0576183

</td>

<td style="text-align:center;">

0.0630033

</td>

<td style="text-align:center;">

0.0704363

</td>

<td style="text-align:center;">

0.1099899

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Banks

</td>

<td style="text-align:center;">

\-0.0035956

</td>

<td style="text-align:center;">

1.2475803

</td>

<td style="text-align:center;">

0.0222035

</td>

<td style="text-align:center;">

0.6482096

</td>

<td style="text-align:center;">

0.4262404

</td>

<td style="text-align:center;">

\-0.0975272

</td>

<td style="text-align:center;">

0.0003985

</td>

<td style="text-align:center;">

0.0272579

</td>

<td style="text-align:center;">

0.0345176

</td>

<td style="text-align:center;">

0.0377435

</td>

<td style="text-align:center;">

0.0421965

</td>

<td style="text-align:center;">

0.0658919

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Beer

</td>

<td style="text-align:center;">

0.0000426

</td>

<td style="text-align:center;">

0.9099867

</td>

<td style="text-align:center;">

\-0.3158099

</td>

<td style="text-align:center;">

\-0.1920509

</td>

<td style="text-align:center;">

0.8565533

</td>

<td style="text-align:center;">

0.2840211

</td>

<td style="text-align:center;">

0.0004848

</td>

<td style="text-align:center;">

0.0331595

</td>

<td style="text-align:center;">

0.0419910

</td>

<td style="text-align:center;">

0.0459154

</td>

<td style="text-align:center;">

0.0513324

</td>

<td style="text-align:center;">

0.0801582

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BldMt

</td>

<td style="text-align:center;">

\-0.0038180

</td>

<td style="text-align:center;">

1.2256726

</td>

<td style="text-align:center;">

0.2746096

</td>

<td style="text-align:center;">

0.2072977

</td>

<td style="text-align:center;">

0.4985308

</td>

<td style="text-align:center;">

0.3151551

</td>

<td style="text-align:center;">

0.0003777

</td>

<td style="text-align:center;">

0.0258339

</td>

<td style="text-align:center;">

0.0327143

</td>

<td style="text-align:center;">

0.0357717

</td>

<td style="text-align:center;">

0.0399920

</td>

<td style="text-align:center;">

0.0624495

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Books

</td>

<td style="text-align:center;">

\-0.0071925

</td>

<td style="text-align:center;">

1.4360719

</td>

<td style="text-align:center;">

0.4600670

</td>

<td style="text-align:center;">

0.1423312

</td>

<td style="text-align:center;">

0.3140638

</td>

<td style="text-align:center;">

0.6229898

</td>

<td style="text-align:center;">

0.0004771

</td>

<td style="text-align:center;">

0.0326318

</td>

<td style="text-align:center;">

0.0413227

</td>

<td style="text-align:center;">

0.0451847

</td>

<td style="text-align:center;">

0.0505155

</td>

<td style="text-align:center;">

0.0788825

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Boxes

</td>

<td style="text-align:center;">

\-0.0016011

</td>

<td style="text-align:center;">

0.8638515

</td>

<td style="text-align:center;">

0.0407416

</td>

<td style="text-align:center;">

0.1523267

</td>

<td style="text-align:center;">

0.8222496

</td>

<td style="text-align:center;">

\-0.0022294

</td>

<td style="text-align:center;">

0.0005539

</td>

<td style="text-align:center;">

0.0378871

</td>

<td style="text-align:center;">

0.0479777

</td>

<td style="text-align:center;">

0.0524616

</td>

<td style="text-align:center;">

0.0586510

</td>

<td style="text-align:center;">

0.0915865

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BusSv

</td>

<td style="text-align:center;">

0.0003938

</td>

<td style="text-align:center;">

1.0525691

</td>

<td style="text-align:center;">

0.4724090

</td>

<td style="text-align:center;">

\-0.1246758

</td>

<td style="text-align:center;">

0.0187068

</td>

<td style="text-align:center;">

\-0.2174015

</td>

<td style="text-align:center;">

0.0002714

</td>

<td style="text-align:center;">

0.0185617

</td>

<td style="text-align:center;">

0.0235054

</td>

<td style="text-align:center;">

0.0257021

</td>

<td style="text-align:center;">

0.0287344

</td>

<td style="text-align:center;">

0.0448703

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chems

</td>

<td style="text-align:center;">

\-0.0020329

</td>

<td style="text-align:center;">

1.0479814

</td>

<td style="text-align:center;">

0.0398632

</td>

<td style="text-align:center;">

0.0610439

</td>

<td style="text-align:center;">

0.3658636

</td>

<td style="text-align:center;">

0.3650244

</td>

<td style="text-align:center;">

0.0004627

</td>

<td style="text-align:center;">

0.0316450

</td>

<td style="text-align:center;">

0.0400731

</td>

<td style="text-align:center;">

0.0438183

</td>

<td style="text-align:center;">

0.0489880

</td>

<td style="text-align:center;">

0.0764972

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chips

</td>

<td style="text-align:center;">

0.0051885

</td>

<td style="text-align:center;">

1.1028458

</td>

<td style="text-align:center;">

0.3129494

</td>

<td style="text-align:center;">

\-0.4482885

</td>

<td style="text-align:center;">

\-0.9646289

</td>

<td style="text-align:center;">

\-0.1232898

</td>

<td style="text-align:center;">

0.0005198

</td>

<td style="text-align:center;">

0.0355509

</td>

<td style="text-align:center;">

0.0450192

</td>

<td style="text-align:center;">

0.0492267

</td>

<td style="text-align:center;">

0.0550344

</td>

<td style="text-align:center;">

0.0859390

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Clths

</td>

<td style="text-align:center;">

\-0.0051112

</td>

<td style="text-align:center;">

1.3268703

</td>

<td style="text-align:center;">

0.7822894

</td>

<td style="text-align:center;">

\-0.2454161

</td>

<td style="text-align:center;">

0.8865135

</td>

<td style="text-align:center;">

0.5414965

</td>

<td style="text-align:center;">

0.0005851

</td>

<td style="text-align:center;">

0.0400219

</td>

<td style="text-align:center;">

0.0506811

</td>

<td style="text-align:center;">

0.0554176

</td>

<td style="text-align:center;">

0.0619558

</td>

<td style="text-align:center;">

0.0967471

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Cnstr

</td>

<td style="text-align:center;">

\-0.0051172

</td>

<td style="text-align:center;">

1.2153172

</td>

<td style="text-align:center;">

0.6550769

</td>

<td style="text-align:center;">

\-0.1314116

</td>

<td style="text-align:center;">

0.5204695

</td>

<td style="text-align:center;">

0.4787251

</td>

<td style="text-align:center;">

0.0007152

</td>

<td style="text-align:center;">

0.0489177

</td>

<td style="text-align:center;">

0.0619460

</td>

<td style="text-align:center;">

0.0677354

</td>

<td style="text-align:center;">

0.0757268

</td>

<td style="text-align:center;">

0.1182512

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Coal

</td>

<td style="text-align:center;">

\-0.0018927

</td>

<td style="text-align:center;">

0.5321811

</td>

<td style="text-align:center;">

0.7143574

</td>

<td style="text-align:center;">

0.6932167

</td>

<td style="text-align:center;">

\-0.5017013

</td>

<td style="text-align:center;">

0.7875115

</td>

<td style="text-align:center;">

0.0017543

</td>

<td style="text-align:center;">

0.1199887

</td>

<td style="text-align:center;">

0.1519456

</td>

<td style="text-align:center;">

0.1661462

</td>

<td style="text-align:center;">

0.1857480

</td>

<td style="text-align:center;">

0.2900548

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Drugs

</td>

<td style="text-align:center;">

0.0013358

</td>

<td style="text-align:center;">

0.8796435

</td>

<td style="text-align:center;">

\-0.4621804

</td>

<td style="text-align:center;">

\-0.3018292

</td>

<td style="text-align:center;">

0.5003218

</td>

<td style="text-align:center;">

0.3002915

</td>

<td style="text-align:center;">

0.0004381

</td>

<td style="text-align:center;">

0.0299632

</td>

<td style="text-align:center;">

0.0379434

</td>

<td style="text-align:center;">

0.0414896

</td>

<td style="text-align:center;">

0.0463845

</td>

<td style="text-align:center;">

0.0724317

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

ElcEq

</td>

<td style="text-align:center;">

0.0013447

</td>

<td style="text-align:center;">

1.1252624

</td>

<td style="text-align:center;">

0.1206725

</td>

<td style="text-align:center;">

\-0.1124701

</td>

<td style="text-align:center;">

\-0.0878487

</td>

<td style="text-align:center;">

0.1209728

</td>

<td style="text-align:center;">

0.0003518

</td>

<td style="text-align:center;">

0.0240609

</td>

<td style="text-align:center;">

0.0304691

</td>

<td style="text-align:center;">

0.0333167

</td>

<td style="text-align:center;">

0.0372474

</td>

<td style="text-align:center;">

0.0581637

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FabPr

</td>

<td style="text-align:center;">

\-0.0022332

</td>

<td style="text-align:center;">

0.8453990

</td>

<td style="text-align:center;">

0.7941666

</td>

<td style="text-align:center;">

0.3626176

</td>

<td style="text-align:center;">

0.1845480

</td>

<td style="text-align:center;">

\-0.6243901

</td>

<td style="text-align:center;">

0.0007540

</td>

<td style="text-align:center;">

0.0515686

</td>

<td style="text-align:center;">

0.0653031

</td>

<td style="text-align:center;">

0.0714062

</td>

<td style="text-align:center;">

0.0798306

</td>

<td style="text-align:center;">

0.1246596

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fin

</td>

<td style="text-align:center;">

\-0.0002833

</td>

<td style="text-align:center;">

1.2562560

</td>

<td style="text-align:center;">

0.3107899

</td>

<td style="text-align:center;">

0.5251945

</td>

<td style="text-align:center;">

\-0.0987906

</td>

<td style="text-align:center;">

\-0.3650579

</td>

<td style="text-align:center;">

0.0004104

</td>

<td style="text-align:center;">

0.0280679

</td>

<td style="text-align:center;">

0.0355434

</td>

<td style="text-align:center;">

0.0388652

</td>

<td style="text-align:center;">

0.0434505

</td>

<td style="text-align:center;">

0.0678501

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Food

</td>

<td style="text-align:center;">

\-0.0017027

</td>

<td style="text-align:center;">

0.8819056

</td>

<td style="text-align:center;">

\-0.1021610

</td>

<td style="text-align:center;">

0.1128245

</td>

<td style="text-align:center;">

0.7741909

</td>

<td style="text-align:center;">

0.4490797

</td>

<td style="text-align:center;">

0.0004269

</td>

<td style="text-align:center;">

0.0291978

</td>

<td style="text-align:center;">

0.0369741

</td>

<td style="text-align:center;">

0.0404297

</td>

<td style="text-align:center;">

0.0451995

</td>

<td style="text-align:center;">

0.0705813

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fun

</td>

<td style="text-align:center;">

\-0.0013404

</td>

<td style="text-align:center;">

1.4377854

</td>

<td style="text-align:center;">

0.5898860

</td>

<td style="text-align:center;">

\-0.0394015

</td>

<td style="text-align:center;">

0.3859710

</td>

<td style="text-align:center;">

0.4124550

</td>

<td style="text-align:center;">

0.0007257

</td>

<td style="text-align:center;">

0.0496341

</td>

<td style="text-align:center;">

0.0628533

</td>

<td style="text-align:center;">

0.0687275

</td>

<td style="text-align:center;">

0.0768359

</td>

<td style="text-align:center;">

0.1199831

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Gold

</td>

<td style="text-align:center;">

0.0003135

</td>

<td style="text-align:center;">

0.3543018

</td>

<td style="text-align:center;">

0.7289414

</td>

<td style="text-align:center;">

\-1.0938949

</td>

<td style="text-align:center;">

0.2666569

</td>

<td style="text-align:center;">

1.4469401

</td>

<td style="text-align:center;">

0.0013482

</td>

<td style="text-align:center;">

0.0922090

</td>

<td style="text-align:center;">

0.1167674

</td>

<td style="text-align:center;">

0.1276803

</td>

<td style="text-align:center;">

0.1427438

</td>

<td style="text-align:center;">

0.2229017

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Guns

</td>

<td style="text-align:center;">

\-0.0000274

</td>

<td style="text-align:center;">

0.8382648

</td>

<td style="text-align:center;">

0.5745523

</td>

<td style="text-align:center;">

0.3837487

</td>

<td style="text-align:center;">

0.9507868

</td>

<td style="text-align:center;">

\-0.0017038

</td>

<td style="text-align:center;">

0.0007288

</td>

<td style="text-align:center;">

0.0498491

</td>

<td style="text-align:center;">

0.0631255

</td>

<td style="text-align:center;">

0.0690251

</td>

<td style="text-align:center;">

0.0771686

</td>

<td style="text-align:center;">

0.1205027

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hardw

</td>

<td style="text-align:center;">

0.0029049

</td>

<td style="text-align:center;">

1.0231410

</td>

<td style="text-align:center;">

\-0.0714698

</td>

<td style="text-align:center;">

\-0.3301447

</td>

<td style="text-align:center;">

\-0.7731021

</td>

<td style="text-align:center;">

\-0.0904900

</td>

<td style="text-align:center;">

0.0006809

</td>

<td style="text-align:center;">

0.0465711

</td>

<td style="text-align:center;">

0.0589745

</td>

<td style="text-align:center;">

0.0644861

</td>

<td style="text-align:center;">

0.0720941

</td>

<td style="text-align:center;">

0.1125786

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hlth

</td>

<td style="text-align:center;">

\-0.0037975

</td>

<td style="text-align:center;">

0.9715977

</td>

<td style="text-align:center;">

1.7326988

</td>

<td style="text-align:center;">

\-0.4383371

</td>

<td style="text-align:center;">

0.8772680

</td>

<td style="text-align:center;">

0.3348111

</td>

<td style="text-align:center;">

0.0008389

</td>

<td style="text-align:center;">

0.0573801

</td>

<td style="text-align:center;">

0.0726623

</td>

<td style="text-align:center;">

0.0794532

</td>

<td style="text-align:center;">

0.0888270

</td>

<td style="text-align:center;">

0.1387078

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hshld

</td>

<td style="text-align:center;">

\-0.0031805

</td>

<td style="text-align:center;">

0.9866357

</td>

<td style="text-align:center;">

\-0.1890740

</td>

<td style="text-align:center;">

\-0.0956830

</td>

<td style="text-align:center;">

0.7730199

</td>

<td style="text-align:center;">

0.3177266

</td>

<td style="text-align:center;">

0.0003387

</td>

<td style="text-align:center;">

0.0231688

</td>

<td style="text-align:center;">

0.0293394

</td>

<td style="text-align:center;">

0.0320815

</td>

<td style="text-align:center;">

0.0358664

</td>

<td style="text-align:center;">

0.0560072

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Insur

</td>

<td style="text-align:center;">

\-0.0013155

</td>

<td style="text-align:center;">

1.1047316

</td>

<td style="text-align:center;">

0.2299386

</td>

<td style="text-align:center;">

0.4954510

</td>

<td style="text-align:center;">

0.3090722

</td>

<td style="text-align:center;">

\-0.1726943

</td>

<td style="text-align:center;">

0.0003704

</td>

<td style="text-align:center;">

0.0253312

</td>

<td style="text-align:center;">

0.0320778

</td>

<td style="text-align:center;">

0.0350757

</td>

<td style="text-align:center;">

0.0392139

</td>

<td style="text-align:center;">

0.0612345

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

LabEq

</td>

<td style="text-align:center;">

0.0027968

</td>

<td style="text-align:center;">

0.9891841

</td>

<td style="text-align:center;">

0.4782318

</td>

<td style="text-align:center;">

\-0.3755583

</td>

<td style="text-align:center;">

\-0.4922250

</td>

<td style="text-align:center;">

0.0922078

</td>

<td style="text-align:center;">

0.0004329

</td>

<td style="text-align:center;">

0.0296092

</td>

<td style="text-align:center;">

0.0374951

</td>

<td style="text-align:center;">

0.0409993

</td>

<td style="text-align:center;">

0.0458364

</td>

<td style="text-align:center;">

0.0715758

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mach

</td>

<td style="text-align:center;">

\-0.0008106

</td>

<td style="text-align:center;">

1.0301561

</td>

<td style="text-align:center;">

0.3575171

</td>

<td style="text-align:center;">

\-0.0547854

</td>

<td style="text-align:center;">

\-0.0325099

</td>

<td style="text-align:center;">

0.2949105

</td>

<td style="text-align:center;">

0.0005178

</td>

<td style="text-align:center;">

0.0354144

</td>

<td style="text-align:center;">

0.0448464

</td>

<td style="text-align:center;">

0.0490377

</td>

<td style="text-align:center;">

0.0548231

</td>

<td style="text-align:center;">

0.0856091

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Meals

</td>

<td style="text-align:center;">

\-0.0016492

</td>

<td style="text-align:center;">

1.0737487

</td>

<td style="text-align:center;">

0.5459601

</td>

<td style="text-align:center;">

0.1001046

</td>

<td style="text-align:center;">

0.6242171

</td>

<td style="text-align:center;">

\-0.1737008

</td>

<td style="text-align:center;">

0.0005212

</td>

<td style="text-align:center;">

0.0356514

</td>

<td style="text-align:center;">

0.0451466

</td>

<td style="text-align:center;">

0.0493659

</td>

<td style="text-align:center;">

0.0551901

</td>

<td style="text-align:center;">

0.0861821

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

MedEq

</td>

<td style="text-align:center;">

0.0014561

</td>

<td style="text-align:center;">

0.8053431

</td>

<td style="text-align:center;">

\-0.0565824

</td>

<td style="text-align:center;">

\-0.3375237

</td>

<td style="text-align:center;">

0.5326186

</td>

<td style="text-align:center;">

0.1033913

</td>

<td style="text-align:center;">

0.0005539

</td>

<td style="text-align:center;">

0.0378871

</td>

<td style="text-align:center;">

0.0479777

</td>

<td style="text-align:center;">

0.0524616

</td>

<td style="text-align:center;">

0.0586510

</td>

<td style="text-align:center;">

0.0915865

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mines

</td>

<td style="text-align:center;">

0.0014572

</td>

<td style="text-align:center;">

0.7813628

</td>

<td style="text-align:center;">

0.2534132

</td>

<td style="text-align:center;">

0.1187663

</td>

<td style="text-align:center;">

\-0.2251123

</td>

<td style="text-align:center;">

0.0825557

</td>

<td style="text-align:center;">

0.0009507

</td>

<td style="text-align:center;">

0.0650268

</td>

<td style="text-align:center;">

0.0823456

</td>

<td style="text-align:center;">

0.0900415

</td>

<td style="text-align:center;">

0.1006645

</td>

<td style="text-align:center;">

0.1571928

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Oil

</td>

<td style="text-align:center;">

\-0.0004014

</td>

<td style="text-align:center;">

0.7991301

</td>

<td style="text-align:center;">

0.2298170

</td>

<td style="text-align:center;">

0.4364659

</td>

<td style="text-align:center;">

0.0717533

</td>

<td style="text-align:center;">

\-0.1674800

</td>

<td style="text-align:center;">

0.0006965

</td>

<td style="text-align:center;">

0.0476356

</td>

<td style="text-align:center;">

0.0603226

</td>

<td style="text-align:center;">

0.0659602

</td>

<td style="text-align:center;">

0.0737421

</td>

<td style="text-align:center;">

0.1151521

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Other

</td>

<td style="text-align:center;">

\-0.0095963

</td>

<td style="text-align:center;">

1.4180793

</td>

<td style="text-align:center;">

0.4039311

</td>

<td style="text-align:center;">

0.0269255

</td>

<td style="text-align:center;">

0.4086910

</td>

<td style="text-align:center;">

0.1984780

</td>

<td style="text-align:center;">

0.0006627

</td>

<td style="text-align:center;">

0.0453283

</td>

<td style="text-align:center;">

0.0574007

</td>

<td style="text-align:center;">

0.0627653

</td>

<td style="text-align:center;">

0.0701702

</td>

<td style="text-align:center;">

0.1095744

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Paper

</td>

<td style="text-align:center;">

\-0.0025994

</td>

<td style="text-align:center;">

0.9960178

</td>

<td style="text-align:center;">

0.0411842

</td>

<td style="text-align:center;">

0.1656356

</td>

<td style="text-align:center;">

0.1961619

</td>

<td style="text-align:center;">

0.5961679

</td>

<td style="text-align:center;">

0.0004124

</td>

<td style="text-align:center;">

0.0282042

</td>

<td style="text-align:center;">

0.0357159

</td>

<td style="text-align:center;">

0.0390538

</td>

<td style="text-align:center;">

0.0436613

</td>

<td style="text-align:center;">

0.0681794

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PerSv

</td>

<td style="text-align:center;">

\-0.0087342

</td>

<td style="text-align:center;">

1.0919539

</td>

<td style="text-align:center;">

1.1387105

</td>

<td style="text-align:center;">

0.2900208

</td>

<td style="text-align:center;">

0.8993240

</td>

<td style="text-align:center;">

\-0.0887214

</td>

<td style="text-align:center;">

0.0006290

</td>

<td style="text-align:center;">

0.0430207

</td>

<td style="text-align:center;">

0.0544786

</td>

<td style="text-align:center;">

0.0595700

</td>

<td style="text-align:center;">

0.0665980

</td>

<td style="text-align:center;">

0.1039962

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

RlEst

</td>

<td style="text-align:center;">

\-0.0107579

</td>

<td style="text-align:center;">

1.4524244

</td>

<td style="text-align:center;">

1.4426993

</td>

<td style="text-align:center;">

0.3381476

</td>

<td style="text-align:center;">

0.5862133

</td>

<td style="text-align:center;">

\-0.1133795

</td>

<td style="text-align:center;">

0.0006743

</td>

<td style="text-align:center;">

0.0461230

</td>

<td style="text-align:center;">

0.0584070

</td>

<td style="text-align:center;">

0.0638657

</td>

<td style="text-align:center;">

0.0714005

</td>

<td style="text-align:center;">

0.1114954

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rtail

</td>

<td style="text-align:center;">

\-0.0006359

</td>

<td style="text-align:center;">

1.0737444

</td>

<td style="text-align:center;">

\-0.0120757

</td>

<td style="text-align:center;">

\-0.2910815

</td>

<td style="text-align:center;">

0.4432776

</td>

<td style="text-align:center;">

0.4689517

</td>

<td style="text-align:center;">

0.0004659

</td>

<td style="text-align:center;">

0.0318637

</td>

<td style="text-align:center;">

0.0403500

</td>

<td style="text-align:center;">

0.0441211

</td>

<td style="text-align:center;">

0.0493264

</td>

<td style="text-align:center;">

0.0770257

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rubbr

</td>

<td style="text-align:center;">

\-0.0030373

</td>

<td style="text-align:center;">

1.1609331

</td>

<td style="text-align:center;">

0.3844679

</td>

<td style="text-align:center;">

\-0.0232771

</td>

<td style="text-align:center;">

0.5958614

</td>

<td style="text-align:center;">

0.2990171

</td>

<td style="text-align:center;">

0.0004376

</td>

<td style="text-align:center;">

0.0299333

</td>

<td style="text-align:center;">

0.0379055

</td>

<td style="text-align:center;">

0.0414481

</td>

<td style="text-align:center;">

0.0463381

</td>

<td style="text-align:center;">

0.0723593

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Ships

</td>

<td style="text-align:center;">

\-0.0014874

</td>

<td style="text-align:center;">

0.9450218

</td>

<td style="text-align:center;">

0.4640843

</td>

<td style="text-align:center;">

0.5768058

</td>

<td style="text-align:center;">

0.3004754

</td>

<td style="text-align:center;">

\-0.0191941

</td>

<td style="text-align:center;">

0.0007598

</td>

<td style="text-align:center;">

0.0519653

</td>

<td style="text-align:center;">

0.0658053

</td>

<td style="text-align:center;">

0.0719554

</td>

<td style="text-align:center;">

0.0804446

</td>

<td style="text-align:center;">

0.1256183

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Smoke

</td>

<td style="text-align:center;">

\-0.0005108

</td>

<td style="text-align:center;">

0.8046435

</td>

<td style="text-align:center;">

\-0.1273409

</td>

<td style="text-align:center;">

0.0620524

</td>

<td style="text-align:center;">

1.2041922

</td>

<td style="text-align:center;">

0.8914597

</td>

<td style="text-align:center;">

0.0006825

</td>

<td style="text-align:center;">

0.0466837

</td>

<td style="text-align:center;">

0.0591171

</td>

<td style="text-align:center;">

0.0646421

</td>

<td style="text-align:center;">

0.0722685

</td>

<td style="text-align:center;">

0.1128509

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Soda

</td>

<td style="text-align:center;">

\-0.0027393

</td>

<td style="text-align:center;">

1.0846754

</td>

<td style="text-align:center;">

\-0.2058664

</td>

<td style="text-align:center;">

0.3111747

</td>

<td style="text-align:center;">

1.0775496

</td>

<td style="text-align:center;">

0.1498779

</td>

<td style="text-align:center;">

0.0006174

</td>

<td style="text-align:center;">

0.0422302

</td>

<td style="text-align:center;">

0.0534775

</td>

<td style="text-align:center;">

0.0584754

</td>

<td style="text-align:center;">

0.0653743

</td>

<td style="text-align:center;">

0.1020853

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Softw

</td>

<td style="text-align:center;">

\-0.0000276

</td>

<td style="text-align:center;">

1.3867136

</td>

<td style="text-align:center;">

0.9454751

</td>

<td style="text-align:center;">

\-0.9717346

</td>

<td style="text-align:center;">

0.1336157

</td>

<td style="text-align:center;">

0.0082342

</td>

<td style="text-align:center;">

0.0009466

</td>

<td style="text-align:center;">

0.0647470

</td>

<td style="text-align:center;">

0.0819912

</td>

<td style="text-align:center;">

0.0896540

</td>

<td style="text-align:center;">

0.1002313

</td>

<td style="text-align:center;">

0.1565162

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Steel

</td>

<td style="text-align:center;">

\-0.0002085

</td>

<td style="text-align:center;">

0.9130251

</td>

<td style="text-align:center;">

0.2016566

</td>

<td style="text-align:center;">

0.4352389

</td>

<td style="text-align:center;">

\-1.0450994

</td>

<td style="text-align:center;">

\-0.0849308

</td>

<td style="text-align:center;">

0.0007098

</td>

<td style="text-align:center;">

0.0485491

</td>

<td style="text-align:center;">

0.0614794

</td>

<td style="text-align:center;">

0.0672251

</td>

<td style="text-align:center;">

0.0751563

</td>

<td style="text-align:center;">

0.1173603

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Telcm

</td>

<td style="text-align:center;">

0.0025699

</td>

<td style="text-align:center;">

0.8743257

</td>

<td style="text-align:center;">

\-0.4497129

</td>

<td style="text-align:center;">

0.3961693

</td>

<td style="text-align:center;">

\-0.6882968

</td>

<td style="text-align:center;">

\-0.1586806

</td>

<td style="text-align:center;">

0.0004282

</td>

<td style="text-align:center;">

0.0292864

</td>

<td style="text-align:center;">

0.0370863

</td>

<td style="text-align:center;">

0.0405524

</td>

<td style="text-align:center;">

0.0453367

</td>

<td style="text-align:center;">

0.0707955

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Toys

</td>

<td style="text-align:center;">

\-0.0087620

</td>

<td style="text-align:center;">

1.3071589

</td>

<td style="text-align:center;">

0.5646103

</td>

<td style="text-align:center;">

\-0.1051569

</td>

<td style="text-align:center;">

0.8874877

</td>

<td style="text-align:center;">

0.8351548

</td>

<td style="text-align:center;">

0.0005863

</td>

<td style="text-align:center;">

0.0401014

</td>

<td style="text-align:center;">

0.0507818

</td>

<td style="text-align:center;">

0.0555278

</td>

<td style="text-align:center;">

0.0620789

</td>

<td style="text-align:center;">

0.0969393

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Trans

</td>

<td style="text-align:center;">

\-0.0031360

</td>

<td style="text-align:center;">

1.0916931

</td>

<td style="text-align:center;">

0.5913613

</td>

<td style="text-align:center;">

0.2065672

</td>

<td style="text-align:center;">

0.4650208

</td>

<td style="text-align:center;">

\-0.0213421

</td>

<td style="text-align:center;">

0.0004102

</td>

<td style="text-align:center;">

0.0280594

</td>

<td style="text-align:center;">

0.0355325

</td>

<td style="text-align:center;">

0.0388533

</td>

<td style="text-align:center;">

0.0434372

</td>

<td style="text-align:center;">

0.0678293

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Txtls

</td>

<td style="text-align:center;">

\-0.0074781

</td>

<td style="text-align:center;">

1.3437515

</td>

<td style="text-align:center;">

0.6048901

</td>

<td style="text-align:center;">

0.4749820

</td>

<td style="text-align:center;">

0.5932878

</td>

<td style="text-align:center;">

0.5394235

</td>

<td style="text-align:center;">

0.0007141

</td>

<td style="text-align:center;">

0.0488452

</td>

<td style="text-align:center;">

0.0618543

</td>

<td style="text-align:center;">

0.0676351

</td>

<td style="text-align:center;">

0.0756146

</td>

<td style="text-align:center;">

0.1180760

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Util

</td>

<td style="text-align:center;">

\-0.0007362

</td>

<td style="text-align:center;">

0.7831676

</td>

<td style="text-align:center;">

0.0052637

</td>

<td style="text-align:center;">

0.4875585

</td>

<td style="text-align:center;">

0.1963733

</td>

<td style="text-align:center;">

\-0.1634922

</td>

<td style="text-align:center;">

0.0003874

</td>

<td style="text-align:center;">

0.0264995

</td>

<td style="text-align:center;">

0.0335572

</td>

<td style="text-align:center;">

0.0366934

</td>

<td style="text-align:center;">

0.0410224

</td>

<td style="text-align:center;">

0.0640586

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Whlsl

</td>

<td style="text-align:center;">

\-0.0024205

</td>

<td style="text-align:center;">

1.0757804

</td>

<td style="text-align:center;">

0.5633473

</td>

<td style="text-align:center;">

0.0179133

</td>

<td style="text-align:center;">

0.1885198

</td>

<td style="text-align:center;">

0.1895158

</td>

<td style="text-align:center;">

0.0003568

</td>

<td style="text-align:center;">

0.0244072

</td>

<td style="text-align:center;">

0.0309077

</td>

<td style="text-align:center;">

0.0337962

</td>

<td style="text-align:center;">

0.0377835

</td>

<td style="text-align:center;">

0.0590008

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Full_STL_FF5-1.png)<!-- -->

### S3-1-4 Rolling Window Estimation with STL Trend

Here, we would try to conduct the STL decomposition before the first
step regression with full sample.

![](ECC_files/figure-gfm/Rolling_STL_FF5-1.png)<!-- -->

### S3-1-5 Full Sample Estimation with Panel Regression

There are three sets of regressions here: Panel Regression at 49
Industry Level, Panel Regression at 49 Industry Level and clustering at
5 Industry Level, Micro-Macro Multilevel Linear Models.

![](ECC_files/figure-gfm/Full_FF5_Panel-1.png)<!-- -->![](ECC_files/figure-gfm/Full_FF5_Panel-2.png)<!-- -->![](ECC_files/figure-gfm/Full_FF5_Panel-3.png)<!-- -->

Next, we get the panel regression clustering at 5 Industry Level.

### S3-1-6 Rolling Window Estimation with Panel Regression

We will show examples of the Real Estate Portfolio (RlEst), Construction
Portfolio (Cnstr), and Food Portfolio (Food) Rolling Betas evolution
here. The smoothing line is based on the loess smoothing. It seems that
the betas are evolving overtime.

![](ECC_files/figure-gfm/Rolling_FF5_Panel-1.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5_Panel-2.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5_Panel-3.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5_Panel-4.png)<!-- -->![](ECC_files/figure-gfm/Rolling_FF5_Panel-5.png)<!-- -->

## S3-2 PRS Five Factor Model

We will then apply the PRS Five Factor Model to estimate the betas.

### S3-2-1 Full Sample Estimation

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

PRS Five Factors

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Coefficients

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Std. Error

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

Aero

</td>

<td style="text-align:center;">

\-0.0007264

</td>

<td style="text-align:center;">

1.2147906

</td>

<td style="text-align:center;">

0.4597678

</td>

<td style="text-align:center;">

\-1.8739102

</td>

<td style="text-align:center;">

2.6544959

</td>

<td style="text-align:center;">

0.0695108

</td>

<td style="text-align:center;">

0.0017926

</td>

<td style="text-align:center;">

0.0413396

</td>

<td style="text-align:center;">

0.0827289

</td>

<td style="text-align:center;">

1.6994957

</td>

<td style="text-align:center;">

0.7471528

</td>

<td style="text-align:center;">

0.5863563

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Agric

</td>

<td style="text-align:center;">

0.0000335

</td>

<td style="text-align:center;">

0.8921762

</td>

<td style="text-align:center;">

0.0717091

</td>

<td style="text-align:center;">

\-0.4604342

</td>

<td style="text-align:center;">

2.0589033

</td>

<td style="text-align:center;">

0.3395515

</td>

<td style="text-align:center;">

0.0021284

</td>

<td style="text-align:center;">

0.0490841

</td>

<td style="text-align:center;">

0.0982271

</td>

<td style="text-align:center;">

2.0178759

</td>

<td style="text-align:center;">

0.8871230

</td>

<td style="text-align:center;">

0.6962031

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Autos

</td>

<td style="text-align:center;">

\-0.0030572

</td>

<td style="text-align:center;">

1.1977989

</td>

<td style="text-align:center;">

0.0672278

</td>

<td style="text-align:center;">

6.3544567

</td>

<td style="text-align:center;">

4.1598356

</td>

<td style="text-align:center;">

\-0.1737414

</td>

<td style="text-align:center;">

0.0019354

</td>

<td style="text-align:center;">

0.0446335

</td>

<td style="text-align:center;">

0.0893205

</td>

<td style="text-align:center;">

1.8349080

</td>

<td style="text-align:center;">

0.8066844

</td>

<td style="text-align:center;">

0.6330759

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Banks

</td>

<td style="text-align:center;">

\-0.0017131

</td>

<td style="text-align:center;">

1.1446243

</td>

<td style="text-align:center;">

0.3036716

</td>

<td style="text-align:center;">

\-0.2118326

</td>

<td style="text-align:center;">

1.6994764

</td>

<td style="text-align:center;">

0.8416676

</td>

<td style="text-align:center;">

0.0015119

</td>

<td style="text-align:center;">

0.0348658

</td>

<td style="text-align:center;">

0.0697734

</td>

<td style="text-align:center;">

1.4333525

</td>

<td style="text-align:center;">

0.6301478

</td>

<td style="text-align:center;">

0.4945321

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Beer

</td>

<td style="text-align:center;">

0.0013533

</td>

<td style="text-align:center;">

0.8163077

</td>

<td style="text-align:center;">

0.6502316

</td>

<td style="text-align:center;">

\-2.7713156

</td>

<td style="text-align:center;">

\-0.3550530

</td>

<td style="text-align:center;">

0.5748237

</td>

<td style="text-align:center;">

0.0015697

</td>

<td style="text-align:center;">

0.0361980

</td>

<td style="text-align:center;">

0.0724395

</td>

<td style="text-align:center;">

1.4881224

</td>

<td style="text-align:center;">

0.6542264

</td>

<td style="text-align:center;">

0.5134287

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BldMt

</td>

<td style="text-align:center;">

\-0.0030308

</td>

<td style="text-align:center;">

1.2794322

</td>

<td style="text-align:center;">

0.3978284

</td>

<td style="text-align:center;">

3.0432575

</td>

<td style="text-align:center;">

3.2402758

</td>

<td style="text-align:center;">

1.2188895

</td>

<td style="text-align:center;">

0.0013397

</td>

<td style="text-align:center;">

0.0308961

</td>

<td style="text-align:center;">

0.0618293

</td>

<td style="text-align:center;">

1.2701560

</td>

<td style="text-align:center;">

0.5584013

</td>

<td style="text-align:center;">

0.4382264

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Books

</td>

<td style="text-align:center;">

\-0.0036651

</td>

<td style="text-align:center;">

1.1403166

</td>

<td style="text-align:center;">

0.3344491

</td>

<td style="text-align:center;">

3.5192625

</td>

<td style="text-align:center;">

2.8975915

</td>

<td style="text-align:center;">

0.3071983

</td>

<td style="text-align:center;">

0.0013751

</td>

<td style="text-align:center;">

0.0317113

</td>

<td style="text-align:center;">

0.0634607

</td>

<td style="text-align:center;">

1.3036699

</td>

<td style="text-align:center;">

0.5731351

</td>

<td style="text-align:center;">

0.4497893

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Boxes

</td>

<td style="text-align:center;">

\-0.0012003

</td>

<td style="text-align:center;">

1.0266425

</td>

<td style="text-align:center;">

0.3245770

</td>

<td style="text-align:center;">

3.6059226

</td>

<td style="text-align:center;">

0.9489560

</td>

<td style="text-align:center;">

1.1834596

</td>

<td style="text-align:center;">

0.0015292

</td>

<td style="text-align:center;">

0.0352642

</td>

<td style="text-align:center;">

0.0705708

</td>

<td style="text-align:center;">

1.4497331

</td>

<td style="text-align:center;">

0.6373492

</td>

<td style="text-align:center;">

0.5001837

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BusSv

</td>

<td style="text-align:center;">

\-0.0009844

</td>

<td style="text-align:center;">

1.1808188

</td>

<td style="text-align:center;">

0.0052199

</td>

<td style="text-align:center;">

1.8003838

</td>

<td style="text-align:center;">

1.5340027

</td>

<td style="text-align:center;">

0.5431220

</td>

<td style="text-align:center;">

0.0009649

</td>

<td style="text-align:center;">

0.0222521

</td>

<td style="text-align:center;">

0.0445309

</td>

<td style="text-align:center;">

0.9147962

</td>

<td style="text-align:center;">

0.4021738

</td>

<td style="text-align:center;">

0.3156210

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chems

</td>

<td style="text-align:center;">

\-0.0010222

</td>

<td style="text-align:center;">

1.0942887

</td>

<td style="text-align:center;">

0.3027224

</td>

<td style="text-align:center;">

1.0268845

</td>

<td style="text-align:center;">

0.9222256

</td>

<td style="text-align:center;">

\-0.2436988

</td>

<td style="text-align:center;">

0.0013039

</td>

<td style="text-align:center;">

0.0300690

</td>

<td style="text-align:center;">

0.0601741

</td>

<td style="text-align:center;">

1.2361550

</td>

<td style="text-align:center;">

0.5434534

</td>

<td style="text-align:center;">

0.4264955

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chips

</td>

<td style="text-align:center;">

0.0020900

</td>

<td style="text-align:center;">

1.3194837

</td>

<td style="text-align:center;">

\-0.6845575

</td>

<td style="text-align:center;">

2.9293268

</td>

<td style="text-align:center;">

\-0.4209634

</td>

<td style="text-align:center;">

0.4134730

</td>

<td style="text-align:center;">

0.0016303

</td>

<td style="text-align:center;">

0.0375961

</td>

<td style="text-align:center;">

0.0752373

</td>

<td style="text-align:center;">

1.5455977

</td>

<td style="text-align:center;">

0.6794943

</td>

<td style="text-align:center;">

0.5332587

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Clths

</td>

<td style="text-align:center;">

\-0.0025929

</td>

<td style="text-align:center;">

1.2208061

</td>

<td style="text-align:center;">

0.5499887

</td>

<td style="text-align:center;">

4.4649420

</td>

<td style="text-align:center;">

3.2403675

</td>

<td style="text-align:center;">

1.3608807

</td>

<td style="text-align:center;">

0.0017273

</td>

<td style="text-align:center;">

0.0398331

</td>

<td style="text-align:center;">

0.0797139

</td>

<td style="text-align:center;">

1.6375599

</td>

<td style="text-align:center;">

0.7199239

</td>

<td style="text-align:center;">

0.5649873

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Cnstr

</td>

<td style="text-align:center;">

\-0.0036864

</td>

<td style="text-align:center;">

1.3485988

</td>

<td style="text-align:center;">

0.2583720

</td>

<td style="text-align:center;">

\-0.0810328

</td>

<td style="text-align:center;">

3.2723505

</td>

<td style="text-align:center;">

0.0993218

</td>

<td style="text-align:center;">

0.0018049

</td>

<td style="text-align:center;">

0.0416221

</td>

<td style="text-align:center;">

0.0832942

</td>

<td style="text-align:center;">

1.7111086

</td>

<td style="text-align:center;">

0.7522582

</td>

<td style="text-align:center;">

0.5903629

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Coal

</td>

<td style="text-align:center;">

\-0.0008261

</td>

<td style="text-align:center;">

1.1302559

</td>

<td style="text-align:center;">

\-0.1563914

</td>

<td style="text-align:center;">

\-2.7173567

</td>

<td style="text-align:center;">

1.2220000

</td>

<td style="text-align:center;">

\-1.5478331

</td>

<td style="text-align:center;">

0.0039984

</td>

<td style="text-align:center;">

0.0922079

</td>

<td style="text-align:center;">

0.1845265

</td>

<td style="text-align:center;">

3.7907201

</td>

<td style="text-align:center;">

1.6665222

</td>

<td style="text-align:center;">

1.3078659

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Drugs

</td>

<td style="text-align:center;">

0.0032083

</td>

<td style="text-align:center;">

0.7726803

</td>

<td style="text-align:center;">

0.2510342

</td>

<td style="text-align:center;">

\-0.4654955

</td>

<td style="text-align:center;">

\-3.7993545

</td>

<td style="text-align:center;">

\-0.9603198

</td>

<td style="text-align:center;">

0.0014020

</td>

<td style="text-align:center;">

0.0323307

</td>

<td style="text-align:center;">

0.0647001

</td>

<td style="text-align:center;">

1.3291320

</td>

<td style="text-align:center;">

0.5843291

</td>

<td style="text-align:center;">

0.4585742

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

ElcEq

</td>

<td style="text-align:center;">

\-0.0000093

</td>

<td style="text-align:center;">

1.2472556

</td>

<td style="text-align:center;">

0.1235728

</td>

<td style="text-align:center;">

0.2140381

</td>

<td style="text-align:center;">

1.1146499

</td>

<td style="text-align:center;">

0.7610827

</td>

<td style="text-align:center;">

0.0013272

</td>

<td style="text-align:center;">

0.0306063

</td>

<td style="text-align:center;">

0.0612494

</td>

<td style="text-align:center;">

1.2582444

</td>

<td style="text-align:center;">

0.5531646

</td>

<td style="text-align:center;">

0.4341167

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FabPr

</td>

<td style="text-align:center;">

\-0.0038139

</td>

<td style="text-align:center;">

1.1266090

</td>

<td style="text-align:center;">

0.0762499

</td>

<td style="text-align:center;">

\-1.1887465

</td>

<td style="text-align:center;">

3.9521467

</td>

<td style="text-align:center;">

\-0.6579375

</td>

<td style="text-align:center;">

0.0022501

</td>

<td style="text-align:center;">

0.0518909

</td>

<td style="text-align:center;">

0.1038441

</td>

<td style="text-align:center;">

2.1332653

</td>

<td style="text-align:center;">

0.9378519

</td>

<td style="text-align:center;">

0.7360145

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fin

</td>

<td style="text-align:center;">

0.0014107

</td>

<td style="text-align:center;">

1.1949440

</td>

<td style="text-align:center;">

\-0.3613530

</td>

<td style="text-align:center;">

1.4712697

</td>

<td style="text-align:center;">

0.1935016

</td>

<td style="text-align:center;">

0.1564705

</td>

<td style="text-align:center;">

0.0011564

</td>

<td style="text-align:center;">

0.0266671

</td>

<td style="text-align:center;">

0.0533662

</td>

<td style="text-align:center;">

1.0962993

</td>

<td style="text-align:center;">

0.4819683

</td>

<td style="text-align:center;">

0.3782428

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Food

</td>

<td style="text-align:center;">

0.0008191

</td>

<td style="text-align:center;">

0.7514778

</td>

<td style="text-align:center;">

0.5673559

</td>

<td style="text-align:center;">

1.8782697

</td>

<td style="text-align:center;">

0.3299690

</td>

<td style="text-align:center;">

0.8080283

</td>

<td style="text-align:center;">

0.0012865

</td>

<td style="text-align:center;">

0.0296684

</td>

<td style="text-align:center;">

0.0593724

</td>

<td style="text-align:center;">

1.2196840

</td>

<td style="text-align:center;">

0.5362122

</td>

<td style="text-align:center;">

0.4208127

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fun

</td>

<td style="text-align:center;">

0.0016971

</td>

<td style="text-align:center;">

1.3425092

</td>

<td style="text-align:center;">

0.0975973

</td>

<td style="text-align:center;">

\-0.0121777

</td>

<td style="text-align:center;">

1.9774675

</td>

<td style="text-align:center;">

\-0.7540465

</td>

<td style="text-align:center;">

0.0020157

</td>

<td style="text-align:center;">

0.0464845

</td>

<td style="text-align:center;">

0.0930248

</td>

<td style="text-align:center;">

1.9110044

</td>

<td style="text-align:center;">

0.8401388

</td>

<td style="text-align:center;">

0.6593305

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Gold

</td>

<td style="text-align:center;">

0.0052923

</td>

<td style="text-align:center;">

0.4542444

</td>

<td style="text-align:center;">

\-0.1285761

</td>

<td style="text-align:center;">

\-15.0501707

</td>

<td style="text-align:center;">

2.1213699

</td>

<td style="text-align:center;">

\-6.1825022

</td>

<td style="text-align:center;">

0.0043092

</td>

<td style="text-align:center;">

0.0993757

</td>

<td style="text-align:center;">

0.1988707

</td>

<td style="text-align:center;">

4.0853923

</td>

<td style="text-align:center;">

1.7960695

</td>

<td style="text-align:center;">

1.4095331

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Guns

</td>

<td style="text-align:center;">

0.0010587

</td>

<td style="text-align:center;">

0.9491310

</td>

<td style="text-align:center;">

0.7103798

</td>

<td style="text-align:center;">

\-1.9627985

</td>

<td style="text-align:center;">

3.9500245

</td>

<td style="text-align:center;">

1.5746902

</td>

<td style="text-align:center;">

0.0021537

</td>

<td style="text-align:center;">

0.0496656

</td>

<td style="text-align:center;">

0.0993908

</td>

<td style="text-align:center;">

2.0417807

</td>

<td style="text-align:center;">

0.8976323

</td>

<td style="text-align:center;">

0.7044507

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hardw

</td>

<td style="text-align:center;">

0.0010566

</td>

<td style="text-align:center;">

1.1242786

</td>

<td style="text-align:center;">

\-0.6145549

</td>

<td style="text-align:center;">

1.5620568

</td>

<td style="text-align:center;">

\-1.0228818

</td>

<td style="text-align:center;">

\-0.7295942

</td>

<td style="text-align:center;">

0.0018602

</td>

<td style="text-align:center;">

0.0428974

</td>

<td style="text-align:center;">

0.0858462

</td>

<td style="text-align:center;">

1.7635356

</td>

<td style="text-align:center;">

0.7753068

</td>

<td style="text-align:center;">

0.6084512

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hlth

</td>

<td style="text-align:center;">

\-0.0030009

</td>

<td style="text-align:center;">

1.2233483

</td>

<td style="text-align:center;">

0.7843342

</td>

<td style="text-align:center;">

\-1.8573374

</td>

<td style="text-align:center;">

3.0130115

</td>

<td style="text-align:center;">

\-0.1316979

</td>

<td style="text-align:center;">

0.0025321

</td>

<td style="text-align:center;">

0.0583941

</td>

<td style="text-align:center;">

0.1168583

</td>

<td style="text-align:center;">

2.4006146

</td>

<td style="text-align:center;">

1.0553872

</td>

<td style="text-align:center;">

0.8282548

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hshld

</td>

<td style="text-align:center;">

\-0.0009809

</td>

<td style="text-align:center;">

0.8439563

</td>

<td style="text-align:center;">

0.5432179

</td>

<td style="text-align:center;">

\-1.7767449

</td>

<td style="text-align:center;">

\-0.4698350

</td>

<td style="text-align:center;">

0.0327638

</td>

<td style="text-align:center;">

0.0011595

</td>

<td style="text-align:center;">

0.0267387

</td>

<td style="text-align:center;">

0.0535094

</td>

<td style="text-align:center;">

1.0992423

</td>

<td style="text-align:center;">

0.4832622

</td>

<td style="text-align:center;">

0.3792582

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Insur

</td>

<td style="text-align:center;">

0.0001100

</td>

<td style="text-align:center;">

1.0042571

</td>

<td style="text-align:center;">

0.2872893

</td>

<td style="text-align:center;">

0.9704142

</td>

<td style="text-align:center;">

0.8232041

</td>

<td style="text-align:center;">

0.4140088

</td>

<td style="text-align:center;">

0.0014004

</td>

<td style="text-align:center;">

0.0322959

</td>

<td style="text-align:center;">

0.0646306

</td>

<td style="text-align:center;">

1.3277031

</td>

<td style="text-align:center;">

0.5837009

</td>

<td style="text-align:center;">

0.4580812

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

LabEq

</td>

<td style="text-align:center;">

0.0011880

</td>

<td style="text-align:center;">

1.2527348

</td>

<td style="text-align:center;">

\-0.3991746

</td>

<td style="text-align:center;">

2.1224497

</td>

<td style="text-align:center;">

\-0.3740978

</td>

<td style="text-align:center;">

\-0.2522120

</td>

<td style="text-align:center;">

0.0016004

</td>

<td style="text-align:center;">

0.0369063

</td>

<td style="text-align:center;">

0.0738569

</td>

<td style="text-align:center;">

1.5172389

</td>

<td style="text-align:center;">

0.6670269

</td>

<td style="text-align:center;">

0.5234744

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mach

</td>

<td style="text-align:center;">

\-0.0008258

</td>

<td style="text-align:center;">

1.2250799

</td>

<td style="text-align:center;">

\-0.0896013

</td>

<td style="text-align:center;">

1.9578641

</td>

<td style="text-align:center;">

1.1650949

</td>

<td style="text-align:center;">

0.1923083

</td>

<td style="text-align:center;">

0.0013205

</td>

<td style="text-align:center;">

0.0304529

</td>

<td style="text-align:center;">

0.0609424

</td>

<td style="text-align:center;">

1.2519381

</td>

<td style="text-align:center;">

0.5503921

</td>

<td style="text-align:center;">

0.4319409

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Meals

</td>

<td style="text-align:center;">

\-0.0020684

</td>

<td style="text-align:center;">

1.1345247

</td>

<td style="text-align:center;">

0.6679509

</td>

<td style="text-align:center;">

1.7897837

</td>

<td style="text-align:center;">

1.4627125

</td>

<td style="text-align:center;">

0.8186635

</td>

<td style="text-align:center;">

0.0015086

</td>

<td style="text-align:center;">

0.0347892

</td>

<td style="text-align:center;">

0.0696202

</td>

<td style="text-align:center;">

1.4302044

</td>

<td style="text-align:center;">

0.6287637

</td>

<td style="text-align:center;">

0.4934460

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

MedEq

</td>

<td style="text-align:center;">

0.0018862

</td>

<td style="text-align:center;">

0.8900137

</td>

<td style="text-align:center;">

0.1622762

</td>

<td style="text-align:center;">

0.2737107

</td>

<td style="text-align:center;">

\-1.1681905

</td>

<td style="text-align:center;">

\-0.8031269

</td>

<td style="text-align:center;">

0.0014125

</td>

<td style="text-align:center;">

0.0325740

</td>

<td style="text-align:center;">

0.0651871

</td>

<td style="text-align:center;">

1.3391359

</td>

<td style="text-align:center;">

0.5887271

</td>

<td style="text-align:center;">

0.4620257

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mines

</td>

<td style="text-align:center;">

0.0009360

</td>

<td style="text-align:center;">

1.0444750

</td>

<td style="text-align:center;">

\-0.0554772

</td>

<td style="text-align:center;">

\-3.3840685

</td>

<td style="text-align:center;">

1.4138771

</td>

<td style="text-align:center;">

\-3.0440866

</td>

<td style="text-align:center;">

0.0023771

</td>

<td style="text-align:center;">

0.0548194

</td>

<td style="text-align:center;">

0.1097047

</td>

<td style="text-align:center;">

2.2536587

</td>

<td style="text-align:center;">

0.9907807

</td>

<td style="text-align:center;">

0.7775524

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Oil

</td>

<td style="text-align:center;">

\-0.0004856

</td>

<td style="text-align:center;">

0.8956570

</td>

<td style="text-align:center;">

0.3585764

</td>

<td style="text-align:center;">

\-4.3787781

</td>

<td style="text-align:center;">

1.5466725

</td>

<td style="text-align:center;">

\-0.7985525

</td>

<td style="text-align:center;">

0.0018671

</td>

<td style="text-align:center;">

0.0430567

</td>

<td style="text-align:center;">

0.0861651

</td>

<td style="text-align:center;">

1.7700861

</td>

<td style="text-align:center;">

0.7781867

</td>

<td style="text-align:center;">

0.6107112

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Other

</td>

<td style="text-align:center;">

\-0.0061774

</td>

<td style="text-align:center;">

1.1533966

</td>

<td style="text-align:center;">

0.1540438

</td>

<td style="text-align:center;">

\-4.6901175

</td>

<td style="text-align:center;">

2.6412491

</td>

<td style="text-align:center;">

\-0.7101488

</td>

<td style="text-align:center;">

0.0018041

</td>

<td style="text-align:center;">

0.0416042

</td>

<td style="text-align:center;">

0.0832583

</td>

<td style="text-align:center;">

1.7103711

</td>

<td style="text-align:center;">

0.7519340

</td>

<td style="text-align:center;">

0.5901085

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Paper

</td>

<td style="text-align:center;">

\-0.0016085

</td>

<td style="text-align:center;">

1.0257733

</td>

<td style="text-align:center;">

0.3793307

</td>

<td style="text-align:center;">

2.1978096

</td>

<td style="text-align:center;">

1.5520329

</td>

<td style="text-align:center;">

0.3980158

</td>

<td style="text-align:center;">

0.0013812

</td>

<td style="text-align:center;">

0.0318518

</td>

<td style="text-align:center;">

0.0637418

</td>

<td style="text-align:center;">

1.3094453

</td>

<td style="text-align:center;">

0.5756742

</td>

<td style="text-align:center;">

0.4517819

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PerSv

</td>

<td style="text-align:center;">

\-0.0071988

</td>

<td style="text-align:center;">

1.1968124

</td>

<td style="text-align:center;">

0.4656690

</td>

<td style="text-align:center;">

4.3326170

</td>

<td style="text-align:center;">

3.8521636

</td>

<td style="text-align:center;">

1.3106456

</td>

<td style="text-align:center;">

0.0017981

</td>

<td style="text-align:center;">

0.0414669

</td>

<td style="text-align:center;">

0.0829835

</td>

<td style="text-align:center;">

1.7047271

</td>

<td style="text-align:center;">

0.7494527

</td>

<td style="text-align:center;">

0.5881612

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

RlEst

</td>

<td style="text-align:center;">

\-0.0083295

</td>

<td style="text-align:center;">

1.3301310

</td>

<td style="text-align:center;">

0.1860782

</td>

<td style="text-align:center;">

4.1323916

</td>

<td style="text-align:center;">

6.8929026

</td>

<td style="text-align:center;">

0.6621041

</td>

<td style="text-align:center;">

0.0022064

</td>

<td style="text-align:center;">

0.0508823

</td>

<td style="text-align:center;">

0.1018256

</td>

<td style="text-align:center;">

2.0917989

</td>

<td style="text-align:center;">

0.9196219

</td>

<td style="text-align:center;">

0.7217079

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rtail

</td>

<td style="text-align:center;">

\-0.0004245

</td>

<td style="text-align:center;">

1.0816559

</td>

<td style="text-align:center;">

0.3691614

</td>

<td style="text-align:center;">

4.7293914

</td>

<td style="text-align:center;">

0.4775361

</td>

<td style="text-align:center;">

1.5513571

</td>

<td style="text-align:center;">

0.0012589

</td>

<td style="text-align:center;">

0.0290323

</td>

<td style="text-align:center;">

0.0580994

</td>

<td style="text-align:center;">

1.1935331

</td>

<td style="text-align:center;">

0.5247154

</td>

<td style="text-align:center;">

0.4117902

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rubbr

</td>

<td style="text-align:center;">

\-0.0012600

</td>

<td style="text-align:center;">

1.1204273

</td>

<td style="text-align:center;">

0.2024823

</td>

<td style="text-align:center;">

1.1525221

</td>

<td style="text-align:center;">

3.8552101

</td>

<td style="text-align:center;">

0.3925701

</td>

<td style="text-align:center;">

0.0014645

</td>

<td style="text-align:center;">

0.0337735

</td>

<td style="text-align:center;">

0.0675875

</td>

<td style="text-align:center;">

1.3884468

</td>

<td style="text-align:center;">

0.6104058

</td>

<td style="text-align:center;">

0.4790389

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Ships

</td>

<td style="text-align:center;">

\-0.0017210

</td>

<td style="text-align:center;">

1.1840183

</td>

<td style="text-align:center;">

0.4887253

</td>

<td style="text-align:center;">

\-0.4676993

</td>

<td style="text-align:center;">

2.2800247

</td>

<td style="text-align:center;">

\-0.0147524

</td>

<td style="text-align:center;">

0.0022415

</td>

<td style="text-align:center;">

0.0516923

</td>

<td style="text-align:center;">

0.1034467

</td>

<td style="text-align:center;">

2.1251006

</td>

<td style="text-align:center;">

0.9342624

</td>

<td style="text-align:center;">

0.7331976

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Smoke

</td>

<td style="text-align:center;">

0.0038290

</td>

<td style="text-align:center;">

0.7342582

</td>

<td style="text-align:center;">

0.6814776

</td>

<td style="text-align:center;">

2.1172818

</td>

<td style="text-align:center;">

\-0.9495259

</td>

<td style="text-align:center;">

0.9852468

</td>

<td style="text-align:center;">

0.0022145

</td>

<td style="text-align:center;">

0.0510683

</td>

<td style="text-align:center;">

0.1021978

</td>

<td style="text-align:center;">

2.0994464

</td>

<td style="text-align:center;">

0.9229840

</td>

<td style="text-align:center;">

0.7243464

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Soda

</td>

<td style="text-align:center;">

0.0007333

</td>

<td style="text-align:center;">

0.8879369

</td>

<td style="text-align:center;">

0.5872698

</td>

<td style="text-align:center;">

1.9990626

</td>

<td style="text-align:center;">

\-1.2181298

</td>

<td style="text-align:center;">

0.6465674

</td>

<td style="text-align:center;">

0.0021502

</td>

<td style="text-align:center;">

0.0495866

</td>

<td style="text-align:center;">

0.0992326

</td>

<td style="text-align:center;">

2.0385321

</td>

<td style="text-align:center;">

0.8962041

</td>

<td style="text-align:center;">

0.7033299

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Softw

</td>

<td style="text-align:center;">

\-0.0012332

</td>

<td style="text-align:center;">

1.5437263

</td>

<td style="text-align:center;">

\-0.2288175

</td>

<td style="text-align:center;">

\-4.4606805

</td>

<td style="text-align:center;">

3.7256163

</td>

<td style="text-align:center;">

\-0.6181143

</td>

<td style="text-align:center;">

0.0032146

</td>

<td style="text-align:center;">

0.0741315

</td>

<td style="text-align:center;">

0.1483520

</td>

<td style="text-align:center;">

3.0475892

</td>

<td style="text-align:center;">

1.3398180

</td>

<td style="text-align:center;">

1.0514726

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Steel

</td>

<td style="text-align:center;">

\-0.0024949

</td>

<td style="text-align:center;">

1.2518243

</td>

<td style="text-align:center;">

\-0.5835215

</td>

<td style="text-align:center;">

\-1.4425826

</td>

<td style="text-align:center;">

2.1058460

</td>

<td style="text-align:center;">

\-0.2147757

</td>

<td style="text-align:center;">

0.0019541

</td>

<td style="text-align:center;">

0.0450640

</td>

<td style="text-align:center;">

0.0901821

</td>

<td style="text-align:center;">

1.8526069

</td>

<td style="text-align:center;">

0.8144654

</td>

<td style="text-align:center;">

0.6391824

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Telcm

</td>

<td style="text-align:center;">

0.0014088

</td>

<td style="text-align:center;">

0.7826801

</td>

<td style="text-align:center;">

\-0.1491935

</td>

<td style="text-align:center;">

1.9576403

</td>

<td style="text-align:center;">

0.0525512

</td>

<td style="text-align:center;">

0.1988381

</td>

<td style="text-align:center;">

0.0012836

</td>

<td style="text-align:center;">

0.0296019

</td>

<td style="text-align:center;">

0.0592394

</td>

<td style="text-align:center;">

1.2169531

</td>

<td style="text-align:center;">

0.5350116

</td>

<td style="text-align:center;">

0.4198705

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Toys

</td>

<td style="text-align:center;">

\-0.0049002

</td>

<td style="text-align:center;">

1.2423499

</td>

<td style="text-align:center;">

0.4384848

</td>

<td style="text-align:center;">

3.7911029

</td>

<td style="text-align:center;">

2.6697370

</td>

<td style="text-align:center;">

0.2016174

</td>

<td style="text-align:center;">

0.0019887

</td>

<td style="text-align:center;">

0.0458612

</td>

<td style="text-align:center;">

0.0917775

</td>

<td style="text-align:center;">

1.8853811

</td>

<td style="text-align:center;">

0.8288740

</td>

<td style="text-align:center;">

0.6504900

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Trans

</td>

<td style="text-align:center;">

\-0.0023420

</td>

<td style="text-align:center;">

1.1269764

</td>

<td style="text-align:center;">

0.3679268

</td>

<td style="text-align:center;">

0.9930022

</td>

<td style="text-align:center;">

2.5143142

</td>

<td style="text-align:center;">

0.5442995

</td>

<td style="text-align:center;">

0.0013575

</td>

<td style="text-align:center;">

0.0313043

</td>

<td style="text-align:center;">

0.0626462

</td>

<td style="text-align:center;">

1.2869388

</td>

<td style="text-align:center;">

0.5657796

</td>

<td style="text-align:center;">

0.4440168

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Txtls

</td>

<td style="text-align:center;">

\-0.0046482

</td>

<td style="text-align:center;">

1.2693006

</td>

<td style="text-align:center;">

0.3614604

</td>

<td style="text-align:center;">

7.2068573

</td>

<td style="text-align:center;">

5.2671998

</td>

<td style="text-align:center;">

1.5925489

</td>

<td style="text-align:center;">

0.0021527

</td>

<td style="text-align:center;">

0.0496440

</td>

<td style="text-align:center;">

0.0993477

</td>

<td style="text-align:center;">

2.0408952

</td>

<td style="text-align:center;">

0.8972430

</td>

<td style="text-align:center;">

0.7041452

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Util

</td>

<td style="text-align:center;">

0.0008933

</td>

<td style="text-align:center;">

0.5729589

</td>

<td style="text-align:center;">

0.2307885

</td>

<td style="text-align:center;">

0.0242462

</td>

<td style="text-align:center;">

0.5461290

</td>

<td style="text-align:center;">

1.3811901

</td>

<td style="text-align:center;">

0.0013890

</td>

<td style="text-align:center;">

0.0320330

</td>

<td style="text-align:center;">

0.0641045

</td>

<td style="text-align:center;">

1.3168958

</td>

<td style="text-align:center;">

0.5789497

</td>

<td style="text-align:center;">

0.4543525

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Whlsl

</td>

<td style="text-align:center;">

\-0.0019210

</td>

<td style="text-align:center;">

1.0903428

</td>

<td style="text-align:center;">

0.2602262

</td>

<td style="text-align:center;">

1.1158367

</td>

<td style="text-align:center;">

2.9195005

</td>

<td style="text-align:center;">

\-0.0552985

</td>

<td style="text-align:center;">

0.0011282

</td>

<td style="text-align:center;">

0.0260184

</td>

<td style="text-align:center;">

0.0520680

</td>

<td style="text-align:center;">

1.0696306

</td>

<td style="text-align:center;">

0.4702439

</td>

<td style="text-align:center;">

0.3690416

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Full_PRS-1.png)<!-- -->![](ECC_files/figure-gfm/Full_PRS-2.png)<!-- -->![](ECC_files/figure-gfm/Full_PRS-3.png)<!-- -->

### S3-2-2 Rolling Window Estimation

We will show an example of the Real Estate Portfolio (RlEst),
Construction Portfolio (Cnstr), and Food Portfolio (Food) Rolling Betas
evolution here. The smoothing line is based on the loess smoothing. It
seems that the betas are evolving overtime.

![](ECC_files/figure-gfm/Rolling_PRS-1.png)<!-- -->![](ECC_files/figure-gfm/Rolling_PRS-2.png)<!-- -->![](ECC_files/figure-gfm/Rolling_PRS-3.png)<!-- -->![](ECC_files/figure-gfm/Rolling_PRS-4.png)<!-- -->![](ECC_files/figure-gfm/Rolling_PRS-5.png)<!-- -->

### S3-2-3 Full Sample Estimation with STL Trend

Here, we would try to conduct the STL decomposition before the first
step regression with full sample.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

PRS Five Factors

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Coefficients

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="6">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Std. Error

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

<th style="text-align:center;">

Alpha

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

Aero

</td>

<td style="text-align:center;">

\-0.0004699

</td>

<td style="text-align:center;">

1.2559452

</td>

<td style="text-align:center;">

0.2550885

</td>

<td style="text-align:center;">

\-7.4904243

</td>

<td style="text-align:center;">

3.7497689

</td>

<td style="text-align:center;">

1.0467663

</td>

<td style="text-align:center;">

0.0006237

</td>

<td style="text-align:center;">

0.0452933

</td>

<td style="text-align:center;">

0.0759007

</td>

<td style="text-align:center;">

1.3705160

</td>

<td style="text-align:center;">

0.5758848

</td>

<td style="text-align:center;">

0.5059989

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Agric

</td>

<td style="text-align:center;">

0.0004289

</td>

<td style="text-align:center;">

0.6602813

</td>

<td style="text-align:center;">

0.5519335

</td>

<td style="text-align:center;">

\-10.5637483

</td>

<td style="text-align:center;">

2.3202084

</td>

<td style="text-align:center;">

1.2059518

</td>

<td style="text-align:center;">

0.0005833

</td>

<td style="text-align:center;">

0.0423558

</td>

<td style="text-align:center;">

0.0709782

</td>

<td style="text-align:center;">

1.2816316

</td>

<td style="text-align:center;">

0.5385360

</td>

<td style="text-align:center;">

0.4731825

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Autos

</td>

<td style="text-align:center;">

\-0.0022983

</td>

<td style="text-align:center;">

1.1866378

</td>

<td style="text-align:center;">

0.0706379

</td>

<td style="text-align:center;">

5.1144455

</td>

<td style="text-align:center;">

3.2693485

</td>

<td style="text-align:center;">

\-3.1890841

</td>

<td style="text-align:center;">

0.0005963

</td>

<td style="text-align:center;">

0.0433027

</td>

<td style="text-align:center;">

0.0725650

</td>

<td style="text-align:center;">

1.3102834

</td>

<td style="text-align:center;">

0.5505753

</td>

<td style="text-align:center;">

0.4837609

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Banks

</td>

<td style="text-align:center;">

\-0.0023066

</td>

<td style="text-align:center;">

1.1340974

</td>

<td style="text-align:center;">

0.5477567

</td>

<td style="text-align:center;">

\-4.1858170

</td>

<td style="text-align:center;">

2.3093520

</td>

<td style="text-align:center;">

0.9979255

</td>

<td style="text-align:center;">

0.0004533

</td>

<td style="text-align:center;">

0.0329203

</td>

<td style="text-align:center;">

0.0551666

</td>

<td style="text-align:center;">

0.9961262

</td>

<td style="text-align:center;">

0.4185678

</td>

<td style="text-align:center;">

0.3677730

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Beer

</td>

<td style="text-align:center;">

\-0.0000519

</td>

<td style="text-align:center;">

0.9326617

</td>

<td style="text-align:center;">

0.7531810

</td>

<td style="text-align:center;">

6.4028660

</td>

<td style="text-align:center;">

\-2.1259455

</td>

<td style="text-align:center;">

1.3059932

</td>

<td style="text-align:center;">

0.0004315

</td>

<td style="text-align:center;">

0.0313359

</td>

<td style="text-align:center;">

0.0525115

</td>

<td style="text-align:center;">

0.9481834

</td>

<td style="text-align:center;">

0.3984225

</td>

<td style="text-align:center;">

0.3500724

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BldMt

</td>

<td style="text-align:center;">

\-0.0019669

</td>

<td style="text-align:center;">

1.0769237

</td>

<td style="text-align:center;">

0.5483939

</td>

<td style="text-align:center;">

\-4.9986259

</td>

<td style="text-align:center;">

4.6113079

</td>

<td style="text-align:center;">

0.0258730

</td>

<td style="text-align:center;">

0.0003546

</td>

<td style="text-align:center;">

0.0257533

</td>

<td style="text-align:center;">

0.0431563

</td>

<td style="text-align:center;">

0.7792595

</td>

<td style="text-align:center;">

0.3274414

</td>

<td style="text-align:center;">

0.2877051

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Books

</td>

<td style="text-align:center;">

\-0.0040879

</td>

<td style="text-align:center;">

1.2287919

</td>

<td style="text-align:center;">

0.3504133

</td>

<td style="text-align:center;">

3.0017092

</td>

<td style="text-align:center;">

2.7518012

</td>

<td style="text-align:center;">

\-1.0957991

</td>

<td style="text-align:center;">

0.0005248

</td>

<td style="text-align:center;">

0.0381116

</td>

<td style="text-align:center;">

0.0638659

</td>

<td style="text-align:center;">

1.1532078

</td>

<td style="text-align:center;">

0.4845729

</td>

<td style="text-align:center;">

0.4257681

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Boxes

</td>

<td style="text-align:center;">

\-0.0015721

</td>

<td style="text-align:center;">

0.8139235

</td>

<td style="text-align:center;">

0.8367810

</td>

<td style="text-align:center;">

\-0.9577129

</td>

<td style="text-align:center;">

3.2508488

</td>

<td style="text-align:center;">

0.0998758

</td>

<td style="text-align:center;">

0.0004751

</td>

<td style="text-align:center;">

0.0345003

</td>

<td style="text-align:center;">

0.0578141

</td>

<td style="text-align:center;">

1.0439323

</td>

<td style="text-align:center;">

0.4386558

</td>

<td style="text-align:center;">

0.3854232

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BusSv

</td>

<td style="text-align:center;">

\-0.0007538

</td>

<td style="text-align:center;">

1.1558261

</td>

<td style="text-align:center;">

\-0.0259993

</td>

<td style="text-align:center;">

3.7142979

</td>

<td style="text-align:center;">

0.4987557

</td>

<td style="text-align:center;">

0.1792919

</td>

<td style="text-align:center;">

0.0003057

</td>

<td style="text-align:center;">

0.0222009

</td>

<td style="text-align:center;">

0.0372033

</td>

<td style="text-align:center;">

0.6717694

</td>

<td style="text-align:center;">

0.2822746

</td>

<td style="text-align:center;">

0.2480194

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chems

</td>

<td style="text-align:center;">

\-0.0001862

</td>

<td style="text-align:center;">

0.9111439

</td>

<td style="text-align:center;">

0.4126744

</td>

<td style="text-align:center;">

\-5.4355384

</td>

<td style="text-align:center;">

2.5115703

</td>

<td style="text-align:center;">

\-0.4099628

</td>

<td style="text-align:center;">

0.0004079

</td>

<td style="text-align:center;">

0.0296201

</td>

<td style="text-align:center;">

0.0496361

</td>

<td style="text-align:center;">

0.8962647

</td>

<td style="text-align:center;">

0.3766065

</td>

<td style="text-align:center;">

0.3309038

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chips

</td>

<td style="text-align:center;">

0.0037892

</td>

<td style="text-align:center;">

1.2177130

</td>

<td style="text-align:center;">

\-1.0302893

</td>

<td style="text-align:center;">

2.7482944

</td>

<td style="text-align:center;">

\-0.3555615

</td>

<td style="text-align:center;">

\-1.1093865

</td>

<td style="text-align:center;">

0.0005194

</td>

<td style="text-align:center;">

0.0377145

</td>

<td style="text-align:center;">

0.0632005

</td>

<td style="text-align:center;">

1.1411924

</td>

<td style="text-align:center;">

0.4795240

</td>

<td style="text-align:center;">

0.4213319

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Clths

</td>

<td style="text-align:center;">

\-0.0039466

</td>

<td style="text-align:center;">

1.3081654

</td>

<td style="text-align:center;">

0.7554029

</td>

<td style="text-align:center;">

6.5128374

</td>

<td style="text-align:center;">

2.7042652

</td>

<td style="text-align:center;">

1.3524681

</td>

<td style="text-align:center;">

0.0006108

</td>

<td style="text-align:center;">

0.0443520

</td>

<td style="text-align:center;">

0.0743232

</td>

<td style="text-align:center;">

1.3420319

</td>

<td style="text-align:center;">

0.5639159

</td>

<td style="text-align:center;">

0.4954825

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Cnstr

</td>

<td style="text-align:center;">

\-0.0015415

</td>

<td style="text-align:center;">

1.0555971

</td>

<td style="text-align:center;">

0.6562803

</td>

<td style="text-align:center;">

\-13.6327199

</td>

<td style="text-align:center;">

1.3012961

</td>

<td style="text-align:center;">

\-2.1860200

</td>

<td style="text-align:center;">

0.0006611

</td>

<td style="text-align:center;">

0.0480090

</td>

<td style="text-align:center;">

0.0804515

</td>

<td style="text-align:center;">

1.4526890

</td>

<td style="text-align:center;">

0.6104135

</td>

<td style="text-align:center;">

0.5363375

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Coal

</td>

<td style="text-align:center;">

0.0057387

</td>

<td style="text-align:center;">

0.2554940

</td>

<td style="text-align:center;">

\-0.2389224

</td>

<td style="text-align:center;">

\-21.9551176

</td>

<td style="text-align:center;">

\-2.8332555

</td>

<td style="text-align:center;">

2.6347515

</td>

<td style="text-align:center;">

0.0016160

</td>

<td style="text-align:center;">

0.1173455

</td>

<td style="text-align:center;">

0.1966428

</td>

<td style="text-align:center;">

3.5507193

</td>

<td style="text-align:center;">

1.4919966

</td>

<td style="text-align:center;">

1.3109370

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Drugs

</td>

<td style="text-align:center;">

0.0020116

</td>

<td style="text-align:center;">

0.8733368

</td>

<td style="text-align:center;">

0.4747889

</td>

<td style="text-align:center;">

5.4946034

</td>

<td style="text-align:center;">

\-5.8223245

</td>

<td style="text-align:center;">

\-1.0432201

</td>

<td style="text-align:center;">

0.0003703

</td>

<td style="text-align:center;">

0.0268932

</td>

<td style="text-align:center;">

0.0450666

</td>

<td style="text-align:center;">

0.8137531

</td>

<td style="text-align:center;">

0.3419355

</td>

<td style="text-align:center;">

0.3004403

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

ElcEq

</td>

<td style="text-align:center;">

0.0016198

</td>

<td style="text-align:center;">

1.1213096

</td>

<td style="text-align:center;">

\-0.1062051

</td>

<td style="text-align:center;">

1.7791092

</td>

<td style="text-align:center;">

\-0.1628531

</td>

<td style="text-align:center;">

\-0.2540949

</td>

<td style="text-align:center;">

0.0003164

</td>

<td style="text-align:center;">

0.0229739

</td>

<td style="text-align:center;">

0.0384987

</td>

<td style="text-align:center;">

0.6951593

</td>

<td style="text-align:center;">

0.2921029

</td>

<td style="text-align:center;">

0.2566551

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FabPr

</td>

<td style="text-align:center;">

\-0.0035111

</td>

<td style="text-align:center;">

0.9279794

</td>

<td style="text-align:center;">

0.2515102

</td>

<td style="text-align:center;">

\-8.1150405

</td>

<td style="text-align:center;">

5.6433532

</td>

<td style="text-align:center;">

1.2928447

</td>

<td style="text-align:center;">

0.0007046

</td>

<td style="text-align:center;">

0.0511691

</td>

<td style="text-align:center;">

0.0857471

</td>

<td style="text-align:center;">

1.5483088

</td>

<td style="text-align:center;">

0.6505926

</td>

<td style="text-align:center;">

0.5716406

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fin

</td>

<td style="text-align:center;">

0.0001692

</td>

<td style="text-align:center;">

1.2144583

</td>

<td style="text-align:center;">

0.0400154

</td>

<td style="text-align:center;">

\-2.7327489

</td>

<td style="text-align:center;">

1.3834701

</td>

<td style="text-align:center;">

\-0.3724981

</td>

<td style="text-align:center;">

0.0004437

</td>

<td style="text-align:center;">

0.0322228

</td>

<td style="text-align:center;">

0.0539976

</td>

<td style="text-align:center;">

0.9750189

</td>

<td style="text-align:center;">

0.4096986

</td>

<td style="text-align:center;">

0.3599801

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Food

</td>

<td style="text-align:center;">

\-0.0002847

</td>

<td style="text-align:center;">

0.8098713

</td>

<td style="text-align:center;">

0.7171661

</td>

<td style="text-align:center;">

4.8026349

</td>

<td style="text-align:center;">

\-0.4076987

</td>

<td style="text-align:center;">

1.9825689

</td>

<td style="text-align:center;">

0.0003966

</td>

<td style="text-align:center;">

0.0287972

</td>

<td style="text-align:center;">

0.0482571

</td>

<td style="text-align:center;">

0.8713647

</td>

<td style="text-align:center;">

0.3661436

</td>

<td style="text-align:center;">

0.3217107

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fun

</td>

<td style="text-align:center;">

0.0008011

</td>

<td style="text-align:center;">

1.3192623

</td>

<td style="text-align:center;">

0.4148489

</td>

<td style="text-align:center;">

\-2.2314608

</td>

<td style="text-align:center;">

2.8780558

</td>

<td style="text-align:center;">

\-0.9222569

</td>

<td style="text-align:center;">

0.0006951

</td>

<td style="text-align:center;">

0.0504778

</td>

<td style="text-align:center;">

0.0845887

</td>

<td style="text-align:center;">

1.5273919

</td>

<td style="text-align:center;">

0.6418034

</td>

<td style="text-align:center;">

0.5639180

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Gold

</td>

<td style="text-align:center;">

0.0059198

</td>

<td style="text-align:center;">

\-0.0184240

</td>

<td style="text-align:center;">

0.3556824

</td>

<td style="text-align:center;">

\-10.2539918

</td>

<td style="text-align:center;">

4.0421823

</td>

<td style="text-align:center;">

\-9.0223432

</td>

<td style="text-align:center;">

0.0011985

</td>

<td style="text-align:center;">

0.0870313

</td>

<td style="text-align:center;">

0.1458435

</td>

<td style="text-align:center;">

2.6334526

</td>

<td style="text-align:center;">

1.1065652

</td>

<td style="text-align:center;">

0.9722792

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Guns

</td>

<td style="text-align:center;">

0.0017087

</td>

<td style="text-align:center;">

0.7157908

</td>

<td style="text-align:center;">

1.0838225

</td>

<td style="text-align:center;">

\-12.4773141

</td>

<td style="text-align:center;">

5.7094248

</td>

<td style="text-align:center;">

0.0230467

</td>

<td style="text-align:center;">

0.0006620

</td>

<td style="text-align:center;">

0.0480717

</td>

<td style="text-align:center;">

0.0805566

</td>

<td style="text-align:center;">

1.4545860

</td>

<td style="text-align:center;">

0.6112106

</td>

<td style="text-align:center;">

0.5370378

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hardw

</td>

<td style="text-align:center;">

0.0019391

</td>

<td style="text-align:center;">

1.0782956

</td>

<td style="text-align:center;">

\-0.7935466

</td>

<td style="text-align:center;">

5.4459169

</td>

<td style="text-align:center;">

\-2.2299181

</td>

<td style="text-align:center;">

\-2.1960074

</td>

<td style="text-align:center;">

0.0006066

</td>

<td style="text-align:center;">

0.0440517

</td>

<td style="text-align:center;">

0.0738200

</td>

<td style="text-align:center;">

1.3329457

</td>

<td style="text-align:center;">

0.5600979

</td>

<td style="text-align:center;">

0.4921279

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hlth

</td>

<td style="text-align:center;">

\-0.0025195

</td>

<td style="text-align:center;">

1.0682492

</td>

<td style="text-align:center;">

0.7689546

</td>

<td style="text-align:center;">

4.6726386

</td>

<td style="text-align:center;">

0.8368552

</td>

<td style="text-align:center;">

0.8415230

</td>

<td style="text-align:center;">

0.0010472

</td>

<td style="text-align:center;">

0.0760429

</td>

<td style="text-align:center;">

0.1274297

</td>

<td style="text-align:center;">

2.3009592

</td>

<td style="text-align:center;">

0.9668529

</td>

<td style="text-align:center;">

0.8495216

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hshld

</td>

<td style="text-align:center;">

\-0.0027500

</td>

<td style="text-align:center;">

0.9358847

</td>

<td style="text-align:center;">

0.7169600

</td>

<td style="text-align:center;">

3.3111882

</td>

<td style="text-align:center;">

0.7387057

</td>

<td style="text-align:center;">

0.3448121

</td>

<td style="text-align:center;">

0.0003055

</td>

<td style="text-align:center;">

0.0221867

</td>

<td style="text-align:center;">

0.0371795

</td>

<td style="text-align:center;">

0.6713395

</td>

<td style="text-align:center;">

0.2820939

</td>

<td style="text-align:center;">

0.2478607

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Insur

</td>

<td style="text-align:center;">

\-0.0004874

</td>

<td style="text-align:center;">

1.0369537

</td>

<td style="text-align:center;">

0.4156527

</td>

<td style="text-align:center;">

\-4.2397802

</td>

<td style="text-align:center;">

2.3745069

</td>

<td style="text-align:center;">

0.5483219

</td>

<td style="text-align:center;">

0.0003994

</td>

<td style="text-align:center;">

0.0290049

</td>

<td style="text-align:center;">

0.0486052

</td>

<td style="text-align:center;">

0.8776499

</td>

<td style="text-align:center;">

0.3687846

</td>

<td style="text-align:center;">

0.3240312

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

LabEq

</td>

<td style="text-align:center;">

0.0027187

</td>

<td style="text-align:center;">

1.0611236

</td>

<td style="text-align:center;">

\-0.5446032

</td>

<td style="text-align:center;">

0.1077402

</td>

<td style="text-align:center;">

\-0.5408806

</td>

<td style="text-align:center;">

\-0.2223122

</td>

<td style="text-align:center;">

0.0004507

</td>

<td style="text-align:center;">

0.0327320

</td>

<td style="text-align:center;">

0.0548510

</td>

<td style="text-align:center;">

0.9904271

</td>

<td style="text-align:center;">

0.4161731

</td>

<td style="text-align:center;">

0.3656689

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mach

</td>

<td style="text-align:center;">

0.0011451

</td>

<td style="text-align:center;">

0.9103207

</td>

<td style="text-align:center;">

0.0461087

</td>

<td style="text-align:center;">

\-9.8508194

</td>

<td style="text-align:center;">

3.1017060

</td>

<td style="text-align:center;">

\-1.2805745

</td>

<td style="text-align:center;">

0.0004428

</td>

<td style="text-align:center;">

0.0321551

</td>

<td style="text-align:center;">

0.0538843

</td>

<td style="text-align:center;">

0.9729722

</td>

<td style="text-align:center;">

0.4088386

</td>

<td style="text-align:center;">

0.3592245

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Meals

</td>

<td style="text-align:center;">

\-0.0026947

</td>

<td style="text-align:center;">

1.1458673

</td>

<td style="text-align:center;">

0.5586733

</td>

<td style="text-align:center;">

3.2747786

</td>

<td style="text-align:center;">

3.5601241

</td>

<td style="text-align:center;">

1.8281175

</td>

<td style="text-align:center;">

0.0004796

</td>

<td style="text-align:center;">

0.0348248

</td>

<td style="text-align:center;">

0.0583579

</td>

<td style="text-align:center;">

1.0537511

</td>

<td style="text-align:center;">

0.4427816

</td>

<td style="text-align:center;">

0.3890483

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

MedEq

</td>

<td style="text-align:center;">

0.0012338

</td>

<td style="text-align:center;">

0.8622370

</td>

<td style="text-align:center;">

0.4855784

</td>

<td style="text-align:center;">

2.5380903

</td>

<td style="text-align:center;">

\-2.9326052

</td>

<td style="text-align:center;">

\-0.4160593

</td>

<td style="text-align:center;">

0.0004975

</td>

<td style="text-align:center;">

0.0361277

</td>

<td style="text-align:center;">

0.0605413

</td>

<td style="text-align:center;">

1.0931762

</td>

<td style="text-align:center;">

0.4593478

</td>

<td style="text-align:center;">

0.4036042

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mines

</td>

<td style="text-align:center;">

0.0042946

</td>

<td style="text-align:center;">

0.5793633

</td>

<td style="text-align:center;">

0.0318880

</td>

<td style="text-align:center;">

\-18.0068969

</td>

<td style="text-align:center;">

2.3640705

</td>

<td style="text-align:center;">

\-4.2438814

</td>

<td style="text-align:center;">

0.0007668

</td>

<td style="text-align:center;">

0.0556814

</td>

<td style="text-align:center;">

0.0933086

</td>

<td style="text-align:center;">

1.6848449

</td>

<td style="text-align:center;">

0.7079644

</td>

<td style="text-align:center;">

0.6220502

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Oil

</td>

<td style="text-align:center;">

0.0008542

</td>

<td style="text-align:center;">

0.7436052

</td>

<td style="text-align:center;">

0.2107170

</td>

<td style="text-align:center;">

\-12.6711069

</td>

<td style="text-align:center;">

1.8771948

</td>

<td style="text-align:center;">

1.0703727

</td>

<td style="text-align:center;">

0.0006051

</td>

<td style="text-align:center;">

0.0439435

</td>

<td style="text-align:center;">

0.0736387

</td>

<td style="text-align:center;">

1.3296709

</td>

<td style="text-align:center;">

0.5587218

</td>

<td style="text-align:center;">

0.4909188

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Other

</td>

<td style="text-align:center;">

\-0.0083802

</td>

<td style="text-align:center;">

1.3825021

</td>

<td style="text-align:center;">

0.4180106

</td>

<td style="text-align:center;">

\-2.7136657

</td>

<td style="text-align:center;">

1.1897278

</td>

<td style="text-align:center;">

0.6766868

</td>

<td style="text-align:center;">

0.0006164

</td>

<td style="text-align:center;">

0.0447613

</td>

<td style="text-align:center;">

0.0750091

</td>

<td style="text-align:center;">

1.3544174

</td>

<td style="text-align:center;">

0.5691202

</td>

<td style="text-align:center;">

0.5000553

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Paper

</td>

<td style="text-align:center;">

0.0007505

</td>

<td style="text-align:center;">

0.7635057

</td>

<td style="text-align:center;">

0.2889981

</td>

<td style="text-align:center;">

\-4.3612924

</td>

<td style="text-align:center;">

1.7959683

</td>

<td style="text-align:center;">

\-1.2592816

</td>

<td style="text-align:center;">

0.0004240

</td>

<td style="text-align:center;">

0.0307880

</td>

<td style="text-align:center;">

0.0515933

</td>

<td style="text-align:center;">

0.9316049

</td>

<td style="text-align:center;">

0.3914563

</td>

<td style="text-align:center;">

0.3439515

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PerSv

</td>

<td style="text-align:center;">

\-0.0085266

</td>

<td style="text-align:center;">

1.1011684

</td>

<td style="text-align:center;">

0.8807493

</td>

<td style="text-align:center;">

\-2.0986592

</td>

<td style="text-align:center;">

7.1662356

</td>

<td style="text-align:center;">

2.2502485

</td>

<td style="text-align:center;">

0.0006989

</td>

<td style="text-align:center;">

0.0507508

</td>

<td style="text-align:center;">

0.0850461

</td>

<td style="text-align:center;">

1.5356511

</td>

<td style="text-align:center;">

0.6452738

</td>

<td style="text-align:center;">

0.5669674

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

RlEst

</td>

<td style="text-align:center;">

\-0.0097201

</td>

<td style="text-align:center;">

1.3200730

</td>

<td style="text-align:center;">

0.6904919

</td>

<td style="text-align:center;">

\-0.2395192

</td>

<td style="text-align:center;">

10.0352215

</td>

<td style="text-align:center;">

\-2.7040297

</td>

<td style="text-align:center;">

0.0007521

</td>

<td style="text-align:center;">

0.0546143

</td>

<td style="text-align:center;">

0.0915204

</td>

<td style="text-align:center;">

1.6525555

</td>

<td style="text-align:center;">

0.6943966

</td>

<td style="text-align:center;">

0.6101288

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rtail

</td>

<td style="text-align:center;">

\-0.0004636

</td>

<td style="text-align:center;">

1.0932934

</td>

<td style="text-align:center;">

0.2826147

</td>

<td style="text-align:center;">

10.6826872

</td>

<td style="text-align:center;">

\-1.1567588

</td>

<td style="text-align:center;">

1.5732409

</td>

<td style="text-align:center;">

0.0003793

</td>

<td style="text-align:center;">

0.0275450

</td>

<td style="text-align:center;">

0.0461587

</td>

<td style="text-align:center;">

0.8334744

</td>

<td style="text-align:center;">

0.3502223

</td>

<td style="text-align:center;">

0.3077215

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rubbr

</td>

<td style="text-align:center;">

\-0.0016398

</td>

<td style="text-align:center;">

1.0561186

</td>

<td style="text-align:center;">

0.6175342

</td>

<td style="text-align:center;">

\-1.5214037

</td>

<td style="text-align:center;">

3.3120986

</td>

<td style="text-align:center;">

\-1.0184067

</td>

<td style="text-align:center;">

0.0004080

</td>

<td style="text-align:center;">

0.0296295

</td>

<td style="text-align:center;">

0.0496519

</td>

<td style="text-align:center;">

0.8965495

</td>

<td style="text-align:center;">

0.3767261

</td>

<td style="text-align:center;">

0.3310090

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Ships

</td>

<td style="text-align:center;">

0.0011604

</td>

<td style="text-align:center;">

0.7126336

</td>

<td style="text-align:center;">

0.5420701

</td>

<td style="text-align:center;">

\-12.3165184

</td>

<td style="text-align:center;">

5.7767870

</td>

<td style="text-align:center;">

\-2.4924140

</td>

<td style="text-align:center;">

0.0007008

</td>

<td style="text-align:center;">

0.0508907

</td>

<td style="text-align:center;">

0.0852805

</td>

<td style="text-align:center;">

1.5398844

</td>

<td style="text-align:center;">

0.6470526

</td>

<td style="text-align:center;">

0.5685303

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Smoke

</td>

<td style="text-align:center;">

0.0029894

</td>

<td style="text-align:center;">

0.6355655

</td>

<td style="text-align:center;">

1.1680262

</td>

<td style="text-align:center;">

1.4176844

</td>

<td style="text-align:center;">

\-1.4322792

</td>

<td style="text-align:center;">

1.9889754

</td>

<td style="text-align:center;">

0.0006519

</td>

<td style="text-align:center;">

0.0473369

</td>

<td style="text-align:center;">

0.0793252

</td>

<td style="text-align:center;">

1.4323514

</td>

<td style="text-align:center;">

0.6018677

</td>

<td style="text-align:center;">

0.5288288

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Soda

</td>

<td style="text-align:center;">

\-0.0022793

</td>

<td style="text-align:center;">

0.9911956

</td>

<td style="text-align:center;">

1.0694227

</td>

<td style="text-align:center;">

5.2613134

</td>

<td style="text-align:center;">

2.1772782

</td>

<td style="text-align:center;">

0.7586857

</td>

<td style="text-align:center;">

0.0005562

</td>

<td style="text-align:center;">

0.0403896

</td>

<td style="text-align:center;">

0.0676833

</td>

<td style="text-align:center;">

1.2221367

</td>

<td style="text-align:center;">

0.5135365

</td>

<td style="text-align:center;">

0.4512168

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Softw

</td>

<td style="text-align:center;">

\-0.0017483

</td>

<td style="text-align:center;">

1.6128358

</td>

<td style="text-align:center;">

\-0.0324200

</td>

<td style="text-align:center;">

7.5734792

</td>

<td style="text-align:center;">

\-2.1058664

</td>

<td style="text-align:center;">

\-1.5315760

</td>

<td style="text-align:center;">

0.0009934

</td>

<td style="text-align:center;">

0.0721372

</td>

<td style="text-align:center;">

0.1208846

</td>

<td style="text-align:center;">

2.1827758

</td>

<td style="text-align:center;">

0.9171928

</td>

<td style="text-align:center;">

0.8058879

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Steel

</td>

<td style="text-align:center;">

0.0016226

</td>

<td style="text-align:center;">

0.8085927

</td>

<td style="text-align:center;">

\-0.8737290

</td>

<td style="text-align:center;">

\-13.4512154

</td>

<td style="text-align:center;">

1.9169273

</td>

<td style="text-align:center;">

0.0860896

</td>

<td style="text-align:center;">

0.0006183

</td>

<td style="text-align:center;">

0.0448969

</td>

<td style="text-align:center;">

0.0752364

</td>

<td style="text-align:center;">

1.3585217

</td>

<td style="text-align:center;">

0.5708448

</td>

<td style="text-align:center;">

0.5015706

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Telcm

</td>

<td style="text-align:center;">

0.0021548

</td>

<td style="text-align:center;">

0.8264663

</td>

<td style="text-align:center;">

\-0.6534422

</td>

<td style="text-align:center;">

2.0158826

</td>

<td style="text-align:center;">

1.1726066

</td>

<td style="text-align:center;">

0.6936346

</td>

<td style="text-align:center;">

0.0004396

</td>

<td style="text-align:center;">

0.0319220

</td>

<td style="text-align:center;">

0.0534936

</td>

<td style="text-align:center;">

0.9659184

</td>

<td style="text-align:center;">

0.4058747

</td>

<td style="text-align:center;">

0.3566202

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Toys

</td>

<td style="text-align:center;">

\-0.0065508

</td>

<td style="text-align:center;">

1.1544288

</td>

<td style="text-align:center;">

0.7702303

</td>

<td style="text-align:center;">

5.6743488

</td>

<td style="text-align:center;">

5.6704359

</td>

<td style="text-align:center;">

1.0876180

</td>

<td style="text-align:center;">

0.0005625

</td>

<td style="text-align:center;">

0.0408470

</td>

<td style="text-align:center;">

0.0684498

</td>

<td style="text-align:center;">

1.2359770

</td>

<td style="text-align:center;">

0.5193521

</td>

<td style="text-align:center;">

0.4563267

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Trans

</td>

<td style="text-align:center;">

\-0.0028268

</td>

<td style="text-align:center;">

1.0578052

</td>

<td style="text-align:center;">

0.4748986

</td>

<td style="text-align:center;">

\-1.8906329

</td>

<td style="text-align:center;">

5.0980038

</td>

<td style="text-align:center;">

0.7725197

</td>

<td style="text-align:center;">

0.0004092

</td>

<td style="text-align:center;">

0.0297138

</td>

<td style="text-align:center;">

0.0497932

</td>

<td style="text-align:center;">

0.8991006

</td>

<td style="text-align:center;">

0.3777981

</td>

<td style="text-align:center;">

0.3319509

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Txtls

</td>

<td style="text-align:center;">

\-0.0045459

</td>

<td style="text-align:center;">

1.1023490

</td>

<td style="text-align:center;">

0.6308306

</td>

<td style="text-align:center;">

0.2432470

</td>

<td style="text-align:center;">

7.5846808

</td>

<td style="text-align:center;">

0.6360910

</td>

<td style="text-align:center;">

0.0007338

</td>

<td style="text-align:center;">

0.0532891

</td>

<td style="text-align:center;">

0.0892998

</td>

<td style="text-align:center;">

1.6124589

</td>

<td style="text-align:center;">

0.6775481

</td>

<td style="text-align:center;">

0.5953250

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Util

</td>

<td style="text-align:center;">

\-0.0005086

</td>

<td style="text-align:center;">

0.7759086

</td>

<td style="text-align:center;">

0.2346717

</td>

<td style="text-align:center;">

\-2.9536624

</td>

<td style="text-align:center;">

1.2216997

</td>

<td style="text-align:center;">

2.7335259

</td>

<td style="text-align:center;">

0.0003740

</td>

<td style="text-align:center;">

0.0271553

</td>

<td style="text-align:center;">

0.0455057

</td>

<td style="text-align:center;">

0.8216826

</td>

<td style="text-align:center;">

0.3452674

</td>

<td style="text-align:center;">

0.3033679

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Whlsl

</td>

<td style="text-align:center;">

\-0.0018305

</td>

<td style="text-align:center;">

1.0649944

</td>

<td style="text-align:center;">

0.1370349

</td>

<td style="text-align:center;">

4.8040164

</td>

<td style="text-align:center;">

2.0207975

</td>

<td style="text-align:center;">

0.8860007

</td>

<td style="text-align:center;">

0.0003900

</td>

<td style="text-align:center;">

0.0283217

</td>

<td style="text-align:center;">

0.0474603

</td>

<td style="text-align:center;">

0.8569768

</td>

<td style="text-align:center;">

0.3600979

</td>

<td style="text-align:center;">

0.3163986

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Full_STL_PRS-1.png)<!-- -->

### S3-2-4 Rolling Window Estimation with STL Trend

Here, we would try to conduct the STL decomposition before the first
step regression with full sample.

![](ECC_files/figure-gfm/Rolling_STL_PRS-1.png)<!-- -->

It seems that the STL decomposition does not help the first step
regression.

# S4 Factor Premium Estimation

In this section, we will describe different ways to estimate the Factor
Premium.

## S4-1 Arithmetic Mean

First, one can take the arithmetic mean of the factors to generate the
expected factor premium. To allow the factor premium to evolve, we also
estimated RAM which is a 5-year Rolling Arithmetic Mean.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Athrithmetic Mean of Fama French Five Factors Premium

</caption>

<thead>

<tr>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

0.0053662

</td>

<td style="text-align:center;">

0.0021664

</td>

<td style="text-align:center;">

0.0025373

</td>

<td style="text-align:center;">

0.0025544

</td>

<td style="text-align:center;">

0.0026045

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Athrithmetic Mean of PRS Five Factors Premium

</caption>

<thead>

<tr>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

0.0053662

</td>

<td style="text-align:center;">

0.0025544

</td>

<td style="text-align:center;">

8.5e-06

</td>

<td style="text-align:center;">

0.0003148

</td>

<td style="text-align:center;">

0.000189

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/AM-1.png)<!-- -->![](ECC_files/figure-gfm/AM-2.png)<!-- -->

## S4-2 Geometric Mean

Levi and Welch mentioned in their 2017 paper that geometric mean might
perform better. So in this section, we will calculate the Geometric Mean
as the factor premium. To allow the factor premium to evolve, we also
estimated RAM which is a 5-year Rolling Geometric Mean.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Geometric Mean of Fama French Five Factors Premium

</caption>

<thead>

<tr>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

0.0043649

</td>

<td style="text-align:center;">

0.0017141

</td>

<td style="text-align:center;">

0.0021243

</td>

<td style="text-align:center;">

0.002322

</td>

<td style="text-align:center;">

0.0024072

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Geometric Mean of PRS Five Factors Premium

</caption>

<thead>

<tr>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

0.0043649

</td>

<td style="text-align:center;">

0.002322

</td>

<td style="text-align:center;">

7.9e-06

</td>

<td style="text-align:center;">

0.0003117

</td>

<td style="text-align:center;">

0.000184

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/GM-1.png)<!-- -->![](ECC_files/figure-gfm/GM-2.png)<!-- -->

## S4-3 Fama Macbeth Second Step Regression

Fama-Macbeth second regression estimated lambda represents the expected
factor risk premium. In this section, we will apply the second step
regression to estimate the factor risk premium.

![](ECC_files/figure-gfm/FM-1.png)<!-- -->![](ECC_files/figure-gfm/FM-2.png)<!-- -->

Now, we decompose the standard error of the second-step regression
lambdas. At each time t,

  
![r\_i = \\lambda\_0 + \\lambda\_1\*\\hat\\beta\_i +
\\lambda\_2\*\\hat\\theta\_i+e\_i](https://latex.codecogs.com/png.latex?r_i%20%3D%20%5Clambda_0%20%2B%20%5Clambda_1%2A%5Chat%5Cbeta_i%20%2B%20%5Clambda_2%2A%5Chat%5Ctheta_i%2Be_i
"r_i = \\lambda_0 + \\lambda_1*\\hat\\beta_i + \\lambda_2*\\hat\\theta_i+e_i")  

  
![se(\\hat{\\lambda}) =
\\hat{\\sigma}\_e\*\\frac{1}{\\sqrt{SST\_{\\hat\\beta}}}\*\\frac{1}{\\sqrt{1-R^2\_{\\hat\\beta}}}](https://latex.codecogs.com/png.latex?se%28%5Chat%7B%5Clambda%7D%29%20%3D%20%5Chat%7B%5Csigma%7D_e%2A%5Cfrac%7B1%7D%7B%5Csqrt%7BSST_%7B%5Chat%5Cbeta%7D%7D%7D%2A%5Cfrac%7B1%7D%7B%5Csqrt%7B1-R%5E2_%7B%5Chat%5Cbeta%7D%7D%7D
"se(\\hat{\\lambda}) = \\hat{\\sigma}_e*\\frac{1}{\\sqrt{SST_{\\hat\\beta}}}*\\frac{1}{\\sqrt{1-R^2_{\\hat\\beta}}}")  

where
![\\hat{\\sigma}\_e](https://latex.codecogs.com/png.latex?%5Chat%7B%5Csigma%7D_e
"\\hat{\\sigma}_e") represents the variation of errors,
![\\sqrt{SST\_{\\hat\\beta}}](https://latex.codecogs.com/png.latex?%5Csqrt%7BSST_%7B%5Chat%5Cbeta%7D%7D
"\\sqrt{SST_{\\hat\\beta}}") represents intra-group beta variation, and
![\\sqrt{1-R^2\_{\\hat\\beta}}](https://latex.codecogs.com/png.latex?%5Csqrt%7B1-R%5E2_%7B%5Chat%5Cbeta%7D%7D
"\\sqrt{1-R^2_{\\hat\\beta}}") represents inter-group beta variation. We
can clearly see that with the seasonality and time-series noise in the
error term, we would get a larger standard error for estimated
![\\lambda](https://latex.codecogs.com/png.latex?%5Clambda "\\lambda").

  
![SST\_{\\hat\\beta} = \\sum\_{i=1}^N (\\hat\\beta\_i -
\\bar\\beta)^2](https://latex.codecogs.com/png.latex?SST_%7B%5Chat%5Cbeta%7D%20%3D%20%5Csum_%7Bi%3D1%7D%5EN%20%28%5Chat%5Cbeta_i%20-%20%5Cbar%5Cbeta%29%5E2
"SST_{\\hat\\beta} = \\sum_{i=1}^N (\\hat\\beta_i - \\bar\\beta)^2")  

  
![R^2\_{\\hat\\beta} = 1 -
\\frac{\\hat\\theta^2\_u}{SST\_{\\hat\\beta}}](https://latex.codecogs.com/png.latex?R%5E2_%7B%5Chat%5Cbeta%7D%20%3D%201%20-%20%5Cfrac%7B%5Chat%5Ctheta%5E2_u%7D%7BSST_%7B%5Chat%5Cbeta%7D%7D
"R^2_{\\hat\\beta} = 1 - \\frac{\\hat\\theta^2_u}{SST_{\\hat\\beta}}")  

where
![\\hat\\theta^2\_u](https://latex.codecogs.com/png.latex?%5Chat%5Ctheta%5E2_u
"\\hat\\theta^2_u") comes from auxiliary regression (aka Factor Spanning
Regression)

  
![\\beta\_i = \\gamma\_0 +
\\gamma\_1\*\\hat\\theta\_i+u\_i](https://latex.codecogs.com/png.latex?%5Cbeta_i%20%3D%20%5Cgamma_0%20%2B%20%5Cgamma_1%2A%5Chat%5Ctheta_i%2Bu_i
"\\beta_i = \\gamma_0 + \\gamma_1*\\hat\\theta_i+u_i")  

We will rewrite the terms as:

  
![se(\\hat{\\lambda}) =
\\hat{\\sigma}\_e\*\\frac{1}{\\hat{\\sigma}\_{\\beta,intra}}\*\\frac{1}{\\hat{\\sigma}\_{\\beta,inter}}](https://latex.codecogs.com/png.latex?se%28%5Chat%7B%5Clambda%7D%29%20%3D%20%5Chat%7B%5Csigma%7D_e%2A%5Cfrac%7B1%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%7D%2A%5Cfrac%7B1%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%7D
"se(\\hat{\\lambda}) = \\hat{\\sigma}_e*\\frac{1}{\\hat{\\sigma}_{\\beta,intra}}*\\frac{1}{\\hat{\\sigma}_{\\beta,inter}}")  

The decomposition would be:

  
![1 =
\\frac{ln(\\hat{\\sigma}\_e)}{ln(se(\\hat\\lambda))}-\\frac{ln(\\hat{\\sigma}\_{\\beta,intra})}{ln(se(\\hat\\lambda))}-\\frac{ln(\\hat{\\sigma}\_{\\beta,inter})}{ln(se(\\hat\\lambda))}](https://latex.codecogs.com/png.latex?1%20%3D%20%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_e%29%7D%7Bln%28se%28%5Chat%5Clambda%29%29%7D-%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%29%7D%7Bln%28se%28%5Chat%5Clambda%29%29%7D-%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%29%7D%7Bln%28se%28%5Chat%5Clambda%29%29%7D
"1 = \\frac{ln(\\hat{\\sigma}_e)}{ln(se(\\hat\\lambda))}-\\frac{ln(\\hat{\\sigma}_{\\beta,intra})}{ln(se(\\hat\\lambda))}-\\frac{ln(\\hat{\\sigma}_{\\beta,inter})}{ln(se(\\hat\\lambda))}")  

And each term is the effect of variation to the
![se(\\hat\\lambda)](https://latex.codecogs.com/png.latex?se%28%5Chat%5Clambda%29
"se(\\hat\\lambda)") and this effect is associated with the sensitivity
of
![se(\\hat\\lambda)](https://latex.codecogs.com/png.latex?se%28%5Chat%5Clambda%29
"se(\\hat\\lambda)") to the specific variation:

  
![\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}\_e} =
\\frac{1}{\\hat{\\sigma}\_{\\beta,intra}}\*\\frac{1}{\\hat{\\sigma}\_{\\beta,inter}}
= \\frac{se(\\hat\\lambda)}{\\hat{\\sigma}\_e} =
se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}\_e)}{ln(se(\\hat\\lambda))}}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bd%20se%28%5Chat%5Clambda%29%7D%7Bd%5Chat%7B%5Csigma%7D_e%7D%20%3D%20%5Cfrac%7B1%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%7D%2A%5Cfrac%7B1%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%7D%20%3D%20%5Cfrac%7Bse%28%5Chat%5Clambda%29%7D%7B%5Chat%7B%5Csigma%7D_e%7D%20%3D%20se%28%5Chat%5Clambda%29%5E%7B1-%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_e%29%7D%7Bln%28se%28%5Chat%5Clambda%29%29%7D%7D
"\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}_e} = \\frac{1}{\\hat{\\sigma}_{\\beta,intra}}*\\frac{1}{\\hat{\\sigma}_{\\beta,inter}} = \\frac{se(\\hat\\lambda)}{\\hat{\\sigma}_e} = se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}_e)}{ln(se(\\hat\\lambda))}}")  

  
![\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}\_{\\beta,intra}} =
\\frac{-1}{\\hat{\\sigma}^2\_{\\beta,intra}}\*\\frac{\\hat{\\sigma}\_e}{\\hat{\\sigma}\_{\\beta,inter}}
= -\\frac{se(\\hat\\lambda)}{\\hat{\\sigma}\_{\\beta,intra}} =
-se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}\_{\\beta,intra})}{se(\\hat\\lambda)}}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bd%20se%28%5Chat%5Clambda%29%7D%7Bd%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%7D%20%3D%20%5Cfrac%7B-1%7D%7B%5Chat%7B%5Csigma%7D%5E2_%7B%5Cbeta%2Cintra%7D%7D%2A%5Cfrac%7B%5Chat%7B%5Csigma%7D_e%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%7D%20%3D%20-%5Cfrac%7Bse%28%5Chat%5Clambda%29%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%7D%20%3D%20-se%28%5Chat%5Clambda%29%5E%7B1-%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%29%7D%7Bse%28%5Chat%5Clambda%29%7D%7D
"\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}_{\\beta,intra}} = \\frac{-1}{\\hat{\\sigma}^2_{\\beta,intra}}*\\frac{\\hat{\\sigma}_e}{\\hat{\\sigma}_{\\beta,inter}} = -\\frac{se(\\hat\\lambda)}{\\hat{\\sigma}_{\\beta,intra}} = -se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}_{\\beta,intra})}{se(\\hat\\lambda)}}")  

Similarly,

  
![\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}\_{\\beta,inter}} =
\\frac{-1}{\\hat{\\sigma}^2\_{\\beta,inter}}\*\\frac{\\hat{\\sigma}\_e}{\\hat{\\sigma}\_{\\beta,intra}}
= -\\frac{se(\\hat\\lambda)}{\\hat{\\sigma}\_{\\beta,inter}} =
-se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}\_{\\beta,inter})}{se(\\hat\\lambda)}}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bd%20se%28%5Chat%5Clambda%29%7D%7Bd%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%7D%20%3D%20%5Cfrac%7B-1%7D%7B%5Chat%7B%5Csigma%7D%5E2_%7B%5Cbeta%2Cinter%7D%7D%2A%5Cfrac%7B%5Chat%7B%5Csigma%7D_e%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cintra%7D%7D%20%3D%20-%5Cfrac%7Bse%28%5Chat%5Clambda%29%7D%7B%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%7D%20%3D%20-se%28%5Chat%5Clambda%29%5E%7B1-%5Cfrac%7Bln%28%5Chat%7B%5Csigma%7D_%7B%5Cbeta%2Cinter%7D%29%7D%7Bse%28%5Chat%5Clambda%29%7D%7D
"\\frac{d se(\\hat\\lambda)}{d\\hat{\\sigma}_{\\beta,inter}} = \\frac{-1}{\\hat{\\sigma}^2_{\\beta,inter}}*\\frac{\\hat{\\sigma}_e}{\\hat{\\sigma}_{\\beta,intra}} = -\\frac{se(\\hat\\lambda)}{\\hat{\\sigma}_{\\beta,inter}} = -se(\\hat\\lambda)^{1-\\frac{ln(\\hat{\\sigma}_{\\beta,inter})}{se(\\hat\\lambda)}}")  

We only care about the magnitude of this sensitivity, since
![se(\\hat\\lambda)\<1](https://latex.codecogs.com/png.latex?se%28%5Chat%5Clambda%29%3C1
"se(\\hat\\lambda)\<1"), the magnitude of the sensitivity is an
increasing function of the decomposition component.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama Macbeth lambda SE Decomposition Percent

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="2">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="5">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

stats

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Factor

</th>

<th style="text-align:center;">

Type

</th>

<th style="text-align:center;">

mean

</th>

<th style="text-align:center;">

median

</th>

<th style="text-align:center;">

variance

</th>

<th style="text-align:center;">

skewness

</th>

<th style="text-align:center;">

kurtosis

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

Mkt-RF

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.9197951

</td>

<td style="text-align:center;">

0.9239368

</td>

<td style="text-align:center;">

0.0048730

</td>

<td style="text-align:center;">

0.1822824

</td>

<td style="text-align:center;">

2.203515

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0547342

</td>

<td style="text-align:center;">

0.0518618

</td>

<td style="text-align:center;">

0.0005520

</td>

<td style="text-align:center;">

0.5918467

</td>

<td style="text-align:center;">

3.228067

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.1349391

</td>

<td style="text-align:center;">

\-0.1322494

</td>

<td style="text-align:center;">

0.0048024

</td>

<td style="text-align:center;">

0.1920204

</td>

<td style="text-align:center;">

2.244849

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

SMB

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.7938181

</td>

<td style="text-align:center;">

0.7955540

</td>

<td style="text-align:center;">

0.0009902

</td>

<td style="text-align:center;">

\-0.1072860

</td>

<td style="text-align:center;">

3.282732

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0420830

</td>

<td style="text-align:center;">

0.0391009

</td>

<td style="text-align:center;">

0.0004051

</td>

<td style="text-align:center;">

1.0027584

</td>

<td style="text-align:center;">

3.799921

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.2482649

</td>

<td style="text-align:center;">

\-0.2447258

</td>

<td style="text-align:center;">

0.0007381

</td>

<td style="text-align:center;">

\-0.4879583

</td>

<td style="text-align:center;">

2.873762

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

HML

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.7863110

</td>

<td style="text-align:center;">

0.7815925

</td>

<td style="text-align:center;">

0.0009377

</td>

<td style="text-align:center;">

0.5832375

</td>

<td style="text-align:center;">

3.632477

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0720098

</td>

<td style="text-align:center;">

0.0690313

</td>

<td style="text-align:center;">

0.0008303

</td>

<td style="text-align:center;">

1.1057488

</td>

<td style="text-align:center;">

5.330316

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.2856988

</td>

<td style="text-align:center;">

\-0.2869396

</td>

<td style="text-align:center;">

0.0010530

</td>

<td style="text-align:center;">

0.0336732

</td>

<td style="text-align:center;">

3.189743

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

RMW

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.7534711

</td>

<td style="text-align:center;">

0.7584274

</td>

<td style="text-align:center;">

0.0010153

</td>

<td style="text-align:center;">

\-0.8269255

</td>

<td style="text-align:center;">

3.912337

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0610090

</td>

<td style="text-align:center;">

0.0591732

</td>

<td style="text-align:center;">

0.0007948

</td>

<td style="text-align:center;">

0.5879833

</td>

<td style="text-align:center;">

3.094051

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.3075379

</td>

<td style="text-align:center;">

\-0.3045390

</td>

<td style="text-align:center;">

0.0021026

</td>

<td style="text-align:center;">

\-0.1064799

</td>

<td style="text-align:center;">

2.212334

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

CMA

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.7474306

</td>

<td style="text-align:center;">

0.7421545

</td>

<td style="text-align:center;">

0.0022749

</td>

<td style="text-align:center;">

0.9534038

</td>

<td style="text-align:center;">

4.229216

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0671794

</td>

<td style="text-align:center;">

0.0672564

</td>

<td style="text-align:center;">

0.0007139

</td>

<td style="text-align:center;">

0.8082294

</td>

<td style="text-align:center;">

5.336149

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.3197487

</td>

<td style="text-align:center;">

\-0.3263410

</td>

<td style="text-align:center;">

0.0019805

</td>

<td style="text-align:center;">

0.6957077

</td>

<td style="text-align:center;">

3.577028

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="3">

Overall

</td>

<td style="text-align:center;">

sig\_e

</td>

<td style="text-align:center;">

0.8001652

</td>

<td style="text-align:center;">

0.7832446

</td>

<td style="text-align:center;">

0.0059177

</td>

<td style="text-align:center;">

1.2304489

</td>

<td style="text-align:center;">

4.479720

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Inter

</td>

<td style="text-align:center;">

0.0594031

</td>

<td style="text-align:center;">

0.0573691

</td>

<td style="text-align:center;">

0.0007671

</td>

<td style="text-align:center;">

0.8566761

</td>

<td style="text-align:center;">

4.451245

</td>

</tr>

<tr>

<td style="text-align:center;">

sig\_Intra

</td>

<td style="text-align:center;">

\-0.2592379

</td>

<td style="text-align:center;">

\-0.2713270

</td>

<td style="text-align:center;">

0.0065869

</td>

<td style="text-align:center;">

1.0257907

</td>

<td style="text-align:center;">

4.054408

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/FM_Lambda_Decomp-1.png)<!-- -->

## S4-4 Fama Macbeth Second Step Regression with STL Deseaoned Data

As we can see, Fama Macbeth method would generate an evolving
time-series of factor risk premium, but the volatility in lambda is
unreasonably large. We will try to apply the STL trend in the second
step regression to smooth the lambda.

### S4-4-1 STL Filtering

STL method (Cleveland et al. 1990) would try decompose the time-series
into 3 components: trend, seasonality, and noise. It applies an
iterative smoothing method to extract the trend and seasonality
components. At the same time, one can choose to use a robust weighting
scheme to reduce the effect of large noise to the trend and seasonality
extraction.

We will extract the trend of risk premium of the industry portfolios and
the trend of the betas with the STL method, and then conduct the second
step regression. There are two options with the STL method: the loess
window for seasonal extraction (s\_window, large value means no rapidly
evolving seasonal component, needs to be odd and at least 7) and robust
weights for noise (downweight the noisy data in smoothing if
non-Gaussian behavior in the time-series leads to extreme, transient
variation). We will first show the STL decomposition of betas and
returns.

![](ECC_files/figure-gfm/Filtering-1.png)<!-- -->![](ECC_files/figure-gfm/Filtering-2.png)<!-- -->![](ECC_files/figure-gfm/Filtering-3.png)<!-- -->![](ECC_files/figure-gfm/Filtering-4.png)<!-- -->![](ECC_files/figure-gfm/Filtering-5.png)<!-- -->![](ECC_files/figure-gfm/Filtering-6.png)<!-- -->![](ECC_files/figure-gfm/Filtering-7.png)<!-- -->![](ECC_files/figure-gfm/Filtering-8.png)<!-- -->

The robustness weighting seems not be appropriate for the Industry Risk
Premiums since the returns variation are mostly caused by Gaussian
behavior. One example is the end of the trend curve: there was a market
crash at the beginning of 2020, so the trend should go down. However,
with the robust weighting, the market crash was given little wight and
disappeared. At the same time, we might just choose s\_window = 7, since
there could be changing seasonal patterns in the short-term.

Now, we would compare the cross-sectional distribution before and after
filtering.

![](ECC_files/figure-gfm/cross_sectional_distribution-1.png)<!-- -->

### S4-4-2 Filtered Seasonality and Trend Strength

Now we estimate the strength of trend and strength of seasonality. The
Strength of the trend is defined as:

  
![F\_T =
max(0,1-\\frac{Var(R\_t)}{Var(T\_t+R\_t)})](https://latex.codecogs.com/png.latex?F_T%20%3D%20max%280%2C1-%5Cfrac%7BVar%28R_t%29%7D%7BVar%28T_t%2BR_t%29%7D%29
"F_T = max(0,1-\\frac{Var(R_t)}{Var(T_t+R_t)})")  

  
![F\_S =
max(0,1-\\frac{Var(R\_t)}{Var(S\_t+R\_t)})](https://latex.codecogs.com/png.latex?F_S%20%3D%20max%280%2C1-%5Cfrac%7BVar%28R_t%29%7D%7BVar%28S_t%2BR_t%29%7D%29
"F_S = max(0,1-\\frac{Var(R_t)}{Var(S_t+R_t)})")  

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

STL Decomposition Component Strength for Portfolio Risk Premium

</caption>

<thead>

<tr>

<th style="text-align:center;">

Strength

</th>

<th style="text-align:center;">

method

</th>

<th style="text-align:center;">

Aero

</th>

<th style="text-align:center;">

Agric

</th>

<th style="text-align:center;">

Autos

</th>

<th style="text-align:center;">

Banks

</th>

<th style="text-align:center;">

Beer

</th>

<th style="text-align:center;">

BldMt

</th>

<th style="text-align:center;">

Books

</th>

<th style="text-align:center;">

Boxes

</th>

<th style="text-align:center;">

BusSv

</th>

<th style="text-align:center;">

Chems

</th>

<th style="text-align:center;">

Chips

</th>

<th style="text-align:center;">

Clths

</th>

<th style="text-align:center;">

Cnstr

</th>

<th style="text-align:center;">

Coal

</th>

<th style="text-align:center;">

Drugs

</th>

<th style="text-align:center;">

ElcEq

</th>

<th style="text-align:center;">

FabPr

</th>

<th style="text-align:center;">

Fin

</th>

<th style="text-align:center;">

Food

</th>

<th style="text-align:center;">

Fun

</th>

<th style="text-align:center;">

Gold

</th>

<th style="text-align:center;">

Guns

</th>

<th style="text-align:center;">

Hardw

</th>

<th style="text-align:center;">

Hlth

</th>

<th style="text-align:center;">

Hshld

</th>

<th style="text-align:center;">

Insur

</th>

<th style="text-align:center;">

LabEq

</th>

<th style="text-align:center;">

Mach

</th>

<th style="text-align:center;">

Meals

</th>

<th style="text-align:center;">

MedEq

</th>

<th style="text-align:center;">

Mines

</th>

<th style="text-align:center;">

Oil

</th>

<th style="text-align:center;">

Other

</th>

<th style="text-align:center;">

Paper

</th>

<th style="text-align:center;">

PerSv

</th>

<th style="text-align:center;">

RlEst

</th>

<th style="text-align:center;">

Rtail

</th>

<th style="text-align:center;">

Rubbr

</th>

<th style="text-align:center;">

Ships

</th>

<th style="text-align:center;">

Smoke

</th>

<th style="text-align:center;">

Soda

</th>

<th style="text-align:center;">

Softw

</th>

<th style="text-align:center;">

Steel

</th>

<th style="text-align:center;">

Telcm

</th>

<th style="text-align:center;">

Toys

</th>

<th style="text-align:center;">

Trans

</th>

<th style="text-align:center;">

Txtls

</th>

<th style="text-align:center;">

Util

</th>

<th style="text-align:center;">

Whlsl

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="6">

FS

</td>

<td style="text-align:center;">

s07 norobust

</td>

<td style="text-align:center;">

0.3911851

</td>

<td style="text-align:center;">

0.3725901

</td>

<td style="text-align:center;">

0.4018774

</td>

<td style="text-align:center;">

0.4123642

</td>

<td style="text-align:center;">

0.3927234

</td>

<td style="text-align:center;">

0.4078828

</td>

<td style="text-align:center;">

0.3910922

</td>

<td style="text-align:center;">

0.3648795

</td>

<td style="text-align:center;">

0.3812723

</td>

<td style="text-align:center;">

0.3675350

</td>

<td style="text-align:center;">

0.3616610

</td>

<td style="text-align:center;">

0.4190785

</td>

<td style="text-align:center;">

0.3798464

</td>

<td style="text-align:center;">

0.3773576

</td>

<td style="text-align:center;">

0.3700809

</td>

<td style="text-align:center;">

0.3704741

</td>

<td style="text-align:center;">

0.3684705

</td>

<td style="text-align:center;">

0.3673023

</td>

<td style="text-align:center;">

0.3680159

</td>

<td style="text-align:center;">

0.4094499

</td>

<td style="text-align:center;">

0.3472977

</td>

<td style="text-align:center;">

0.3537860

</td>

<td style="text-align:center;">

0.3597511

</td>

<td style="text-align:center;">

0.3807114

</td>

<td style="text-align:center;">

0.3932478

</td>

<td style="text-align:center;">

0.3934480

</td>

<td style="text-align:center;">

0.3332523

</td>

<td style="text-align:center;">

0.3668646

</td>

<td style="text-align:center;">

0.3629374

</td>

<td style="text-align:center;">

0.3584366

</td>

<td style="text-align:center;">

0.3371663

</td>

<td style="text-align:center;">

0.3550115

</td>

<td style="text-align:center;">

0.3970981

</td>

<td style="text-align:center;">

0.3472353

</td>

<td style="text-align:center;">

0.3540942

</td>

<td style="text-align:center;">

0.4210761

</td>

<td style="text-align:center;">

0.3944570

</td>

<td style="text-align:center;">

0.3988149

</td>

<td style="text-align:center;">

0.3716232

</td>

<td style="text-align:center;">

0.3130075

</td>

<td style="text-align:center;">

0.3659172

</td>

<td style="text-align:center;">

0.3278624

</td>

<td style="text-align:center;">

0.3442852

</td>

<td style="text-align:center;">

0.3609891

</td>

<td style="text-align:center;">

0.3592305

</td>

<td style="text-align:center;">

0.3992945

</td>

<td style="text-align:center;">

0.4088416

</td>

<td style="text-align:center;">

0.3775854

</td>

<td style="text-align:center;">

0.3694408

</td>

</tr>

<tr>

<td style="text-align:center;">

s07 robust

</td>

<td style="text-align:center;">

0.1935022

</td>

<td style="text-align:center;">

0.1330849

</td>

<td style="text-align:center;">

0.1373592

</td>

<td style="text-align:center;">

0.1786056

</td>

<td style="text-align:center;">

0.1579393

</td>

<td style="text-align:center;">

0.1348414

</td>

<td style="text-align:center;">

0.1442415

</td>

<td style="text-align:center;">

0.1368121

</td>

<td style="text-align:center;">

0.1622529

</td>

<td style="text-align:center;">

0.1123085

</td>

<td style="text-align:center;">

0.1806169

</td>

<td style="text-align:center;">

0.1924230

</td>

<td style="text-align:center;">

0.1737184

</td>

<td style="text-align:center;">

0.1818465

</td>

<td style="text-align:center;">

0.1716535

</td>

<td style="text-align:center;">

0.1602079

</td>

<td style="text-align:center;">

0.1653442

</td>

<td style="text-align:center;">

0.1365543

</td>

<td style="text-align:center;">

0.2150892

</td>

<td style="text-align:center;">

0.1515594

</td>

<td style="text-align:center;">

0.1352441

</td>

<td style="text-align:center;">

0.1784574

</td>

<td style="text-align:center;">

0.1794134

</td>

<td style="text-align:center;">

0.1686052

</td>

<td style="text-align:center;">

0.1177779

</td>

<td style="text-align:center;">

0.1909530

</td>

<td style="text-align:center;">

0.1055538

</td>

<td style="text-align:center;">

0.1627177

</td>

<td style="text-align:center;">

0.0888803

</td>

<td style="text-align:center;">

0.1570241

</td>

<td style="text-align:center;">

0.0914811

</td>

<td style="text-align:center;">

0.1353939

</td>

<td style="text-align:center;">

0.2213339

</td>

<td style="text-align:center;">

0.1559026

</td>

<td style="text-align:center;">

0.1508374

</td>

<td style="text-align:center;">

0.1097639

</td>

<td style="text-align:center;">

0.1847783

</td>

<td style="text-align:center;">

0.2223238

</td>

<td style="text-align:center;">

0.1754397

</td>

<td style="text-align:center;">

0.1644021

</td>

<td style="text-align:center;">

0.1154241

</td>

<td style="text-align:center;">

0.0835594

</td>

<td style="text-align:center;">

0.1388996

</td>

<td style="text-align:center;">

0.1721490

</td>

<td style="text-align:center;">

0.1827868

</td>

<td style="text-align:center;">

0.2070766

</td>

<td style="text-align:center;">

0.1616175

</td>

<td style="text-align:center;">

0.1465886

</td>

<td style="text-align:center;">

0.1340354

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 norobust

</td>

<td style="text-align:center;">

0.1715220

</td>

<td style="text-align:center;">

0.1542386

</td>

<td style="text-align:center;">

0.1466074

</td>

<td style="text-align:center;">

0.1530480

</td>

<td style="text-align:center;">

0.1629970

</td>

<td style="text-align:center;">

0.1507389

</td>

<td style="text-align:center;">

0.1425589

</td>

<td style="text-align:center;">

0.1462846

</td>

<td style="text-align:center;">

0.1499812

</td>

<td style="text-align:center;">

0.1554518

</td>

<td style="text-align:center;">

0.1437995

</td>

<td style="text-align:center;">

0.1732677

</td>

<td style="text-align:center;">

0.1592202

</td>

<td style="text-align:center;">

0.1584251

</td>

<td style="text-align:center;">

0.1356105

</td>

<td style="text-align:center;">

0.1468336

</td>

<td style="text-align:center;">

0.1364764

</td>

<td style="text-align:center;">

0.1302110

</td>

<td style="text-align:center;">

0.1434273

</td>

<td style="text-align:center;">

0.1684885

</td>

<td style="text-align:center;">

0.1532860

</td>

<td style="text-align:center;">

0.1455716

</td>

<td style="text-align:center;">

0.1570901

</td>

<td style="text-align:center;">

0.1521780

</td>

<td style="text-align:center;">

0.1346499

</td>

<td style="text-align:center;">

0.1337293

</td>

<td style="text-align:center;">

0.1358997

</td>

<td style="text-align:center;">

0.1452397

</td>

<td style="text-align:center;">

0.1303147

</td>

<td style="text-align:center;">

0.1455287

</td>

<td style="text-align:center;">

0.1229566

</td>

<td style="text-align:center;">

0.1441907

</td>

<td style="text-align:center;">

0.1853615

</td>

<td style="text-align:center;">

0.1412987

</td>

<td style="text-align:center;">

0.1435338

</td>

<td style="text-align:center;">

0.1646089

</td>

<td style="text-align:center;">

0.1462893

</td>

<td style="text-align:center;">

0.1754984

</td>

<td style="text-align:center;">

0.1499311

</td>

<td style="text-align:center;">

0.1391745

</td>

<td style="text-align:center;">

0.1533818

</td>

<td style="text-align:center;">

0.1506773

</td>

<td style="text-align:center;">

0.1417627

</td>

<td style="text-align:center;">

0.1533034

</td>

<td style="text-align:center;">

0.1544247

</td>

<td style="text-align:center;">

0.1641945

</td>

<td style="text-align:center;">

0.1755422

</td>

<td style="text-align:center;">

0.1608538

</td>

<td style="text-align:center;">

0.1414738

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 robust

</td>

<td style="text-align:center;">

0.0932133

</td>

<td style="text-align:center;">

0.0630820

</td>

<td style="text-align:center;">

0.0636732

</td>

<td style="text-align:center;">

0.0817096

</td>

<td style="text-align:center;">

0.0697414

</td>

<td style="text-align:center;">

0.0525724

</td>

<td style="text-align:center;">

0.0654441

</td>

<td style="text-align:center;">

0.0697971

</td>

<td style="text-align:center;">

0.0682196

</td>

<td style="text-align:center;">

0.0665752

</td>

<td style="text-align:center;">

0.0817959

</td>

<td style="text-align:center;">

0.1038690

</td>

<td style="text-align:center;">

0.0931980

</td>

<td style="text-align:center;">

0.0929010

</td>

<td style="text-align:center;">

0.0748362

</td>

<td style="text-align:center;">

0.0922239

</td>

<td style="text-align:center;">

0.0735943

</td>

<td style="text-align:center;">

0.0615121

</td>

<td style="text-align:center;">

0.0560796

</td>

<td style="text-align:center;">

0.0896648

</td>

<td style="text-align:center;">

0.0709464

</td>

<td style="text-align:center;">

0.0728823

</td>

<td style="text-align:center;">

0.0856320

</td>

<td style="text-align:center;">

0.0734410

</td>

<td style="text-align:center;">

0.0392797

</td>

<td style="text-align:center;">

0.0729093

</td>

<td style="text-align:center;">

0.0600954

</td>

<td style="text-align:center;">

0.0791513

</td>

<td style="text-align:center;">

0.0629090

</td>

<td style="text-align:center;">

0.0719507

</td>

<td style="text-align:center;">

0.0405025

</td>

<td style="text-align:center;">

0.0672994

</td>

<td style="text-align:center;">

0.0831488

</td>

<td style="text-align:center;">

0.0756608

</td>

<td style="text-align:center;">

0.0719348

</td>

<td style="text-align:center;">

0.0549216

</td>

<td style="text-align:center;">

0.1015209

</td>

<td style="text-align:center;">

0.1059332

</td>

<td style="text-align:center;">

0.0761996

</td>

<td style="text-align:center;">

0.0945961

</td>

<td style="text-align:center;">

0.0624700

</td>

<td style="text-align:center;">

0.0397197

</td>

<td style="text-align:center;">

0.0834692

</td>

<td style="text-align:center;">

0.0966527

</td>

<td style="text-align:center;">

0.0892999

</td>

<td style="text-align:center;">

0.0813360

</td>

<td style="text-align:center;">

0.0726407

</td>

<td style="text-align:center;">

0.0763601

</td>

<td style="text-align:center;">

0.0562639

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 norobust

</td>

<td style="text-align:center;">

0.0601633

</td>

<td style="text-align:center;">

0.0475928

</td>

<td style="text-align:center;">

0.0765333

</td>

<td style="text-align:center;">

0.0434124

</td>

<td style="text-align:center;">

0.0579168

</td>

<td style="text-align:center;">

0.0552060

</td>

<td style="text-align:center;">

0.0386767

</td>

<td style="text-align:center;">

0.0649526

</td>

<td style="text-align:center;">

0.0409870

</td>

<td style="text-align:center;">

0.0739656

</td>

<td style="text-align:center;">

0.0395210

</td>

<td style="text-align:center;">

0.0581979

</td>

<td style="text-align:center;">

0.0514092

</td>

<td style="text-align:center;">

0.0598806

</td>

<td style="text-align:center;">

0.0303644

</td>

<td style="text-align:center;">

0.0567801

</td>

<td style="text-align:center;">

0.0596509

</td>

<td style="text-align:center;">

0.0341185

</td>

<td style="text-align:center;">

0.0403368

</td>

<td style="text-align:center;">

0.0688779

</td>

<td style="text-align:center;">

0.0462200

</td>

<td style="text-align:center;">

0.0607677

</td>

<td style="text-align:center;">

0.0491420

</td>

<td style="text-align:center;">

0.0502315

</td>

<td style="text-align:center;">

0.0405826

</td>

<td style="text-align:center;">

0.0413409

</td>

<td style="text-align:center;">

0.0437884

</td>

<td style="text-align:center;">

0.0599790

</td>

<td style="text-align:center;">

0.0544320

</td>

<td style="text-align:center;">

0.0421698

</td>

<td style="text-align:center;">

0.0489724

</td>

<td style="text-align:center;">

0.0491735

</td>

<td style="text-align:center;">

0.0641968

</td>

<td style="text-align:center;">

0.0637719

</td>

<td style="text-align:center;">

0.0418764

</td>

<td style="text-align:center;">

0.0671636

</td>

<td style="text-align:center;">

0.0499496

</td>

<td style="text-align:center;">

0.0782749

</td>

<td style="text-align:center;">

0.0561672

</td>

<td style="text-align:center;">

0.0422292

</td>

<td style="text-align:center;">

0.0467096

</td>

<td style="text-align:center;">

0.0500458

</td>

<td style="text-align:center;">

0.0678029

</td>

<td style="text-align:center;">

0.0453633

</td>

<td style="text-align:center;">

0.0563154

</td>

<td style="text-align:center;">

0.0566933

</td>

<td style="text-align:center;">

0.0613601

</td>

<td style="text-align:center;">

0.0558211

</td>

<td style="text-align:center;">

0.0480012

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 robust

</td>

<td style="text-align:center;">

0.0195290

</td>

<td style="text-align:center;">

0.0251790

</td>

<td style="text-align:center;">

0.0436084

</td>

<td style="text-align:center;">

0.0206615

</td>

<td style="text-align:center;">

0.0184751

</td>

<td style="text-align:center;">

0.0271615

</td>

<td style="text-align:center;">

0.0184102

</td>

<td style="text-align:center;">

0.0451552

</td>

<td style="text-align:center;">

0.0161600

</td>

<td style="text-align:center;">

0.0406732

</td>

<td style="text-align:center;">

0.0254891

</td>

<td style="text-align:center;">

0.0289817

</td>

<td style="text-align:center;">

0.0398457

</td>

<td style="text-align:center;">

0.0294088

</td>

<td style="text-align:center;">

0.0173966

</td>

<td style="text-align:center;">

0.0393771

</td>

<td style="text-align:center;">

0.0358616

</td>

<td style="text-align:center;">

0.0173265

</td>

<td style="text-align:center;">

0.0129435

</td>

<td style="text-align:center;">

0.0496558

</td>

<td style="text-align:center;">

0.0325875

</td>

<td style="text-align:center;">

0.0330893

</td>

<td style="text-align:center;">

0.0326774

</td>

<td style="text-align:center;">

0.0252610

</td>

<td style="text-align:center;">

0.0195269

</td>

<td style="text-align:center;">

0.0293054

</td>

<td style="text-align:center;">

0.0302699

</td>

<td style="text-align:center;">

0.0410299

</td>

<td style="text-align:center;">

0.0383096

</td>

<td style="text-align:center;">

0.0285954

</td>

<td style="text-align:center;">

0.0365749

</td>

<td style="text-align:center;">

0.0225854

</td>

<td style="text-align:center;">

0.0280083

</td>

<td style="text-align:center;">

0.0411606

</td>

<td style="text-align:center;">

0.0199753

</td>

<td style="text-align:center;">

0.0302439

</td>

<td style="text-align:center;">

0.0300381

</td>

<td style="text-align:center;">

0.0465594

</td>

<td style="text-align:center;">

0.0432242

</td>

<td style="text-align:center;">

0.0279197

</td>

<td style="text-align:center;">

0.0230431

</td>

<td style="text-align:center;">

0.0100405

</td>

<td style="text-align:center;">

0.0457963

</td>

<td style="text-align:center;">

0.0332615

</td>

<td style="text-align:center;">

0.0369541

</td>

<td style="text-align:center;">

0.0330005

</td>

<td style="text-align:center;">

0.0367820

</td>

<td style="text-align:center;">

0.0359658

</td>

<td style="text-align:center;">

0.0233252

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="6">

FT

</td>

<td style="text-align:center;">

s07 norobust

</td>

<td style="text-align:center;">

0.1747301

</td>

<td style="text-align:center;">

0.1218548

</td>

<td style="text-align:center;">

0.1722092

</td>

<td style="text-align:center;">

0.1530624

</td>

<td style="text-align:center;">

0.1444809

</td>

<td style="text-align:center;">

0.1299203

</td>

<td style="text-align:center;">

0.1915024

</td>

<td style="text-align:center;">

0.1342552

</td>

<td style="text-align:center;">

0.1548790

</td>

<td style="text-align:center;">

0.1323798

</td>

<td style="text-align:center;">

0.1731102

</td>

<td style="text-align:center;">

0.1781217

</td>

<td style="text-align:center;">

0.1544956

</td>

<td style="text-align:center;">

0.1934636

</td>

<td style="text-align:center;">

0.1346082

</td>

<td style="text-align:center;">

0.1277598

</td>

<td style="text-align:center;">

0.1373339

</td>

<td style="text-align:center;">

0.1621637

</td>

<td style="text-align:center;">

0.1402085

</td>

<td style="text-align:center;">

0.1668559

</td>

<td style="text-align:center;">

0.1174218

</td>

<td style="text-align:center;">

0.1392205

</td>

<td style="text-align:center;">

0.1688858

</td>

<td style="text-align:center;">

0.1965993

</td>

<td style="text-align:center;">

0.1523608

</td>

<td style="text-align:center;">

0.1570573

</td>

<td style="text-align:center;">

0.1306660

</td>

<td style="text-align:center;">

0.1365207

</td>

<td style="text-align:center;">

0.1473765

</td>

<td style="text-align:center;">

0.1511585

</td>

<td style="text-align:center;">

0.1497665

</td>

<td style="text-align:center;">

0.1316594

</td>

<td style="text-align:center;">

0.1699624

</td>

<td style="text-align:center;">

0.1222298

</td>

<td style="text-align:center;">

0.1515716

</td>

<td style="text-align:center;">

0.2029502

</td>

<td style="text-align:center;">

0.1425971

</td>

<td style="text-align:center;">

0.1441369

</td>

<td style="text-align:center;">

0.1251990

</td>

<td style="text-align:center;">

0.1381937

</td>

<td style="text-align:center;">

0.1379424

</td>

<td style="text-align:center;">

0.1290404

</td>

<td style="text-align:center;">

0.1376526

</td>

<td style="text-align:center;">

0.1838286

</td>

<td style="text-align:center;">

0.1301331

</td>

<td style="text-align:center;">

0.1520290

</td>

<td style="text-align:center;">

0.1622098

</td>

<td style="text-align:center;">

0.1708918

</td>

<td style="text-align:center;">

0.1498722

</td>

</tr>

<tr>

<td style="text-align:center;">

s07 robust

</td>

<td style="text-align:center;">

0.0615722

</td>

<td style="text-align:center;">

0.0310825

</td>

<td style="text-align:center;">

0.0513790

</td>

<td style="text-align:center;">

0.0051914

</td>

<td style="text-align:center;">

0.0480184

</td>

<td style="text-align:center;">

0.0108255

</td>

<td style="text-align:center;">

0.0755777

</td>

<td style="text-align:center;">

0.0000000

</td>

<td style="text-align:center;">

0.0617244

</td>

<td style="text-align:center;">

0.0317907

</td>

<td style="text-align:center;">

0.0788905

</td>

<td style="text-align:center;">

0.0470572

</td>

<td style="text-align:center;">

0.0623079

</td>

<td style="text-align:center;">

0.0886780

</td>

<td style="text-align:center;">

0.0386053

</td>

<td style="text-align:center;">

0.0212144

</td>

<td style="text-align:center;">

0.0290154

</td>

<td style="text-align:center;">

0.0314009

</td>

<td style="text-align:center;">

0.0609016

</td>

<td style="text-align:center;">

0.0495621

</td>

<td style="text-align:center;">

0.0458769

</td>

<td style="text-align:center;">

0.0429066

</td>

<td style="text-align:center;">

0.0669126

</td>

<td style="text-align:center;">

0.0657843

</td>

<td style="text-align:center;">

0.0016019

</td>

<td style="text-align:center;">

0.0502745

</td>

<td style="text-align:center;">

0.0000000

</td>

<td style="text-align:center;">

0.0365109

</td>

<td style="text-align:center;">

0.0552708

</td>

<td style="text-align:center;">

0.0375878

</td>

<td style="text-align:center;">

0.0047704

</td>

<td style="text-align:center;">

0.0351032

</td>

<td style="text-align:center;">

0.0507331

</td>

<td style="text-align:center;">

0.0294042

</td>

<td style="text-align:center;">

0.0800777

</td>

<td style="text-align:center;">

0.0567200

</td>

<td style="text-align:center;">

0.0456076

</td>

<td style="text-align:center;">

0.0515451

</td>

<td style="text-align:center;">

0.0251869

</td>

<td style="text-align:center;">

0.0375225

</td>

<td style="text-align:center;">

0.0453823

</td>

<td style="text-align:center;">

0.0023200

</td>

<td style="text-align:center;">

0.0252830

</td>

<td style="text-align:center;">

0.0698966

</td>

<td style="text-align:center;">

0.0704611

</td>

<td style="text-align:center;">

0.0167496

</td>

<td style="text-align:center;">

0.0664586

</td>

<td style="text-align:center;">

0.0025032

</td>

<td style="text-align:center;">

0.0457656

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 norobust

</td>

<td style="text-align:center;">

0.1407848

</td>

<td style="text-align:center;">

0.1029359

</td>

<td style="text-align:center;">

0.1354323

</td>

<td style="text-align:center;">

0.1209299

</td>

<td style="text-align:center;">

0.1143252

</td>

<td style="text-align:center;">

0.1003318

</td>

<td style="text-align:center;">

0.1502053

</td>

<td style="text-align:center;">

0.1105516

</td>

<td style="text-align:center;">

0.1281721

</td>

<td style="text-align:center;">

0.1114761

</td>

<td style="text-align:center;">

0.1419507

</td>

<td style="text-align:center;">

0.1352655

</td>

<td style="text-align:center;">

0.1278098

</td>

<td style="text-align:center;">

0.1614405

</td>

<td style="text-align:center;">

0.1074691

</td>

<td style="text-align:center;">

0.1046091

</td>

<td style="text-align:center;">

0.1142497

</td>

<td style="text-align:center;">

0.1322714

</td>

<td style="text-align:center;">

0.1098999

</td>

<td style="text-align:center;">

0.1320479

</td>

<td style="text-align:center;">

0.1008032

</td>

<td style="text-align:center;">

0.1114172

</td>

<td style="text-align:center;">

0.1402189

</td>

<td style="text-align:center;">

0.1674478

</td>

<td style="text-align:center;">

0.1172914

</td>

<td style="text-align:center;">

0.1240296

</td>

<td style="text-align:center;">

0.1111200

</td>

<td style="text-align:center;">

0.1148631

</td>

<td style="text-align:center;">

0.1169995

</td>

<td style="text-align:center;">

0.1288658

</td>

<td style="text-align:center;">

0.1301918

</td>

<td style="text-align:center;">

0.1043315

</td>

<td style="text-align:center;">

0.1362260

</td>

<td style="text-align:center;">

0.1029547

</td>

<td style="text-align:center;">

0.1200181

</td>

<td style="text-align:center;">

0.1597103

</td>

<td style="text-align:center;">

0.1105676

</td>

<td style="text-align:center;">

0.1161866

</td>

<td style="text-align:center;">

0.1039593

</td>

<td style="text-align:center;">

0.1200972

</td>

<td style="text-align:center;">

0.1113521

</td>

<td style="text-align:center;">

0.1110099

</td>

<td style="text-align:center;">

0.1156434

</td>

<td style="text-align:center;">

0.1492082

</td>

<td style="text-align:center;">

0.1104237

</td>

<td style="text-align:center;">

0.1213890

</td>

<td style="text-align:center;">

0.1256044

</td>

<td style="text-align:center;">

0.1371936

</td>

<td style="text-align:center;">

0.1203757

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 robust

</td>

<td style="text-align:center;">

0.0697357

</td>

<td style="text-align:center;">

0.0377960

</td>

<td style="text-align:center;">

0.0695943

</td>

<td style="text-align:center;">

0.0444541

</td>

<td style="text-align:center;">

0.0643411

</td>

<td style="text-align:center;">

0.0181430

</td>

<td style="text-align:center;">

0.0962614

</td>

<td style="text-align:center;">

0.0000000

</td>

<td style="text-align:center;">

0.0574438

</td>

<td style="text-align:center;">

0.0420824

</td>

<td style="text-align:center;">

0.0881330

</td>

<td style="text-align:center;">

0.0849883

</td>

<td style="text-align:center;">

0.0770077

</td>

<td style="text-align:center;">

0.1030379

</td>

<td style="text-align:center;">

0.0671929

</td>

<td style="text-align:center;">

0.0481982

</td>

<td style="text-align:center;">

0.0477861

</td>

<td style="text-align:center;">

0.0127605

</td>

<td style="text-align:center;">

0.0360501

</td>

<td style="text-align:center;">

0.0535708

</td>

<td style="text-align:center;">

0.0591903

</td>

<td style="text-align:center;">

0.0614146

</td>

<td style="text-align:center;">

0.0539884

</td>

<td style="text-align:center;">

0.0736465

</td>

<td style="text-align:center;">

0.0315696

</td>

<td style="text-align:center;">

0.0272153

</td>

<td style="text-align:center;">

0.0372867

</td>

<td style="text-align:center;">

0.0646442

</td>

<td style="text-align:center;">

0.0446057

</td>

<td style="text-align:center;">

0.0334147

</td>

<td style="text-align:center;">

0.0578639

</td>

<td style="text-align:center;">

0.0509970

</td>

<td style="text-align:center;">

0.0502580

</td>

<td style="text-align:center;">

0.0502323

</td>

<td style="text-align:center;">

0.0820566

</td>

<td style="text-align:center;">

0.0540329

</td>

<td style="text-align:center;">

0.0797632

</td>

<td style="text-align:center;">

0.0579009

</td>

<td style="text-align:center;">

0.0385608

</td>

<td style="text-align:center;">

0.0580475

</td>

<td style="text-align:center;">

0.0615840

</td>

<td style="text-align:center;">

0.0340669

</td>

<td style="text-align:center;">

0.0293688

</td>

<td style="text-align:center;">

0.0958803

</td>

<td style="text-align:center;">

0.0777113

</td>

<td style="text-align:center;">

0.0384853

</td>

<td style="text-align:center;">

0.0531726

</td>

<td style="text-align:center;">

0.0310471

</td>

<td style="text-align:center;">

0.0478614

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 norobust

</td>

<td style="text-align:center;">

0.1392491

</td>

<td style="text-align:center;">

0.1061359

</td>

<td style="text-align:center;">

0.1370404

</td>

<td style="text-align:center;">

0.1228059

</td>

<td style="text-align:center;">

0.1128373

</td>

<td style="text-align:center;">

0.1046560

</td>

<td style="text-align:center;">

0.1527875

</td>

<td style="text-align:center;">

0.1122508

</td>

<td style="text-align:center;">

0.1315556

</td>

<td style="text-align:center;">

0.1136538

</td>

<td style="text-align:center;">

0.1424726

</td>

<td style="text-align:center;">

0.1297128

</td>

<td style="text-align:center;">

0.1314119

</td>

<td style="text-align:center;">

0.1663026

</td>

<td style="text-align:center;">

0.1058051

</td>

<td style="text-align:center;">

0.1075340

</td>

<td style="text-align:center;">

0.1211150

</td>

<td style="text-align:center;">

0.1374774

</td>

<td style="text-align:center;">

0.1093715

</td>

<td style="text-align:center;">

0.1351366

</td>

<td style="text-align:center;">

0.0999502

</td>

<td style="text-align:center;">

0.1145405

</td>

<td style="text-align:center;">

0.1379634

</td>

<td style="text-align:center;">

0.1762155

</td>

<td style="text-align:center;">

0.1224816

</td>

<td style="text-align:center;">

0.1257258

</td>

<td style="text-align:center;">

0.1160512

</td>

<td style="text-align:center;">

0.1197718

</td>

<td style="text-align:center;">

0.1240796

</td>

<td style="text-align:center;">

0.1310452

</td>

<td style="text-align:center;">

0.1339221

</td>

<td style="text-align:center;">

0.1046548

</td>

<td style="text-align:center;">

0.1344719

</td>

<td style="text-align:center;">

0.1031931

</td>

<td style="text-align:center;">

0.1191116

</td>

<td style="text-align:center;">

0.1628746

</td>

<td style="text-align:center;">

0.1128658

</td>

<td style="text-align:center;">

0.1215241

</td>

<td style="text-align:center;">

0.1089579

</td>

<td style="text-align:center;">

0.1198918

</td>

<td style="text-align:center;">

0.1094232

</td>

<td style="text-align:center;">

0.1117915

</td>

<td style="text-align:center;">

0.1187315

</td>

<td style="text-align:center;">

0.1438505

</td>

<td style="text-align:center;">

0.1144191

</td>

<td style="text-align:center;">

0.1202181

</td>

<td style="text-align:center;">

0.1212746

</td>

<td style="text-align:center;">

0.1337691

</td>

<td style="text-align:center;">

0.1221408

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 robust

</td>

<td style="text-align:center;">

0.0620425

</td>

<td style="text-align:center;">

0.0524872

</td>

<td style="text-align:center;">

0.0787254

</td>

<td style="text-align:center;">

0.0299023

</td>

<td style="text-align:center;">

0.0653389

</td>

<td style="text-align:center;">

0.0345767

</td>

<td style="text-align:center;">

0.1057528

</td>

<td style="text-align:center;">

0.0325341

</td>

<td style="text-align:center;">

0.0764593

</td>

<td style="text-align:center;">

0.0490294

</td>

<td style="text-align:center;">

0.1017065

</td>

<td style="text-align:center;">

0.0784469

</td>

<td style="text-align:center;">

0.0940683

</td>

<td style="text-align:center;">

0.1243466

</td>

<td style="text-align:center;">

0.0745595

</td>

<td style="text-align:center;">

0.0610655

</td>

<td style="text-align:center;">

0.0637757

</td>

<td style="text-align:center;">

0.0645653

</td>

<td style="text-align:center;">

0.0460254

</td>

<td style="text-align:center;">

0.0605526

</td>

<td style="text-align:center;">

0.0686601

</td>

<td style="text-align:center;">

0.0708301

</td>

<td style="text-align:center;">

0.0756040

</td>

<td style="text-align:center;">

0.1048584

</td>

<td style="text-align:center;">

0.0531525

</td>

<td style="text-align:center;">

0.0459628

</td>

<td style="text-align:center;">

0.0578484

</td>

<td style="text-align:center;">

0.0792166

</td>

<td style="text-align:center;">

0.0643925

</td>

<td style="text-align:center;">

0.0663802

</td>

<td style="text-align:center;">

0.0841352

</td>

<td style="text-align:center;">

0.0527248

</td>

<td style="text-align:center;">

0.0639323

</td>

<td style="text-align:center;">

0.0601636

</td>

<td style="text-align:center;">

0.0855092

</td>

<td style="text-align:center;">

0.0640592

</td>

<td style="text-align:center;">

0.0843181

</td>

<td style="text-align:center;">

0.0763113

</td>

<td style="text-align:center;">

0.0602987

</td>

<td style="text-align:center;">

0.0718530

</td>

<td style="text-align:center;">

0.0629026

</td>

<td style="text-align:center;">

0.0356287

</td>

<td style="text-align:center;">

0.0470413

</td>

<td style="text-align:center;">

0.0859378

</td>

<td style="text-align:center;">

0.0830256

</td>

<td style="text-align:center;">

0.0734112

</td>

<td style="text-align:center;">

0.0606631

</td>

<td style="text-align:center;">

0.0579499

</td>

<td style="text-align:center;">

0.0611395

</td>

</tr>

</tbody>

</table>

It seems that the both the trend and seasonal components are weak. No
robust is stronger than robust, and smaller s\_window would yield
stronger components.

### S4-4-3 Beta Decomposition

![](ECC_files/figure-gfm/Beta_Decomposition-1.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-2.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-3.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-4.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-5.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-6.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-7.png)<!-- -->![](ECC_files/figure-gfm/Beta_Decomposition-8.png)<!-- -->

Beta estimation’s noise or seasonal pattern is much smaller than trend
so the noise weight or the s\_window does not impact the result as much.

Now, we will take the desired no robust weighting, s\_window = 7 trend
results of the Industry Risk Premium to estimate the factor risk
premium.

### S4-4-4 Filtered Second Pass Regression

![](ECC_files/figure-gfm/Filtered_FM-1.png)<!-- -->![](ECC_files/figure-gfm/Filtered_FM-2.png)<!-- -->

For robustness check, we also computed the factor risk premium based on
other filtering.

### S4-4-5 Regression Standard Error

![](ECC_files/figure-gfm/Regression_SE-1.png)<!-- -->

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Average Cross-sectional Regression Lambda Error

</caption>

<thead>

<tr>

<th style="text-align:center;">

Factors

</th>

<th style="text-align:center;">

FM

</th>

<th style="text-align:center;">

FM\_STL

</th>

<th style="text-align:center;">

ratio

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

Mkt-RF

</td>

<td style="text-align:center;">

0.0240154

</td>

<td style="text-align:center;">

0.0066808

</td>

<td style="text-align:center;">

0.2781904

</td>

</tr>

<tr>

<td style="text-align:center;">

SMB

</td>

<td style="text-align:center;">

0.0134733

</td>

<td style="text-align:center;">

0.0037066

</td>

<td style="text-align:center;">

0.2751085

</td>

</tr>

<tr>

<td style="text-align:center;">

HML

</td>

<td style="text-align:center;">

0.0126575

</td>

<td style="text-align:center;">

0.0035400

</td>

<td style="text-align:center;">

0.2796793

</td>

</tr>

<tr>

<td style="text-align:center;">

RMW

</td>

<td style="text-align:center;">

0.0105174

</td>

<td style="text-align:center;">

0.0029243

</td>

<td style="text-align:center;">

0.2780437

</td>

</tr>

<tr>

<td style="text-align:center;">

CMA

</td>

<td style="text-align:center;">

0.0101584

</td>

<td style="text-align:center;">

0.0028341

</td>

<td style="text-align:center;">

0.2789863

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Regression_SE-2.png)<!-- -->

### S4-4-6 Unfiltered and Filtered Lambdas

Let’s plot the unfiltered lambda together with filtered lambda to see
the effect of filtering on lambda.

![](ECC_files/figure-gfm/Lambda_Comparison-1.png)<!-- -->![](ECC_files/figure-gfm/Lambda_Comparison-2.png)<!-- -->

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Correlation between FM lambda and STL filtered FM lambda

</caption>

<thead>

<tr>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

FF5

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

PRS

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Factors

</th>

<th style="text-align:center;">

FF5

</th>

<th style="text-align:center;">

Factors

</th>

<th style="text-align:center;">

PRS

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

Mkt-RF

</td>

<td style="text-align:center;">

0.3058557

</td>

<td style="text-align:center;">

Mkt-RF

</td>

<td style="text-align:center;">

0.3374587

</td>

</tr>

<tr>

<td style="text-align:center;">

SMB

</td>

<td style="text-align:center;">

0.3216449

</td>

<td style="text-align:center;">

RMW

</td>

<td style="text-align:center;">

0.3601626

</td>

</tr>

<tr>

<td style="text-align:center;">

HML

</td>

<td style="text-align:center;">

0.4158492

</td>

<td style="text-align:center;">

dDP

</td>

<td style="text-align:center;">

0.3611585

</td>

</tr>

<tr>

<td style="text-align:center;">

RMW

</td>

<td style="text-align:center;">

0.3228094

</td>

<td style="text-align:center;">

dTS

</td>

<td style="text-align:center;">

0.3914243

</td>

</tr>

<tr>

<td style="text-align:center;">

CMA

</td>

<td style="text-align:center;">

0.3644662

</td>

<td style="text-align:center;">

UNEXPI

</td>

<td style="text-align:center;">

0.3885955

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Lambda_Comparison-3.png)<!-- -->![](ECC_files/figure-gfm/Lambda_Comparison-4.png)<!-- -->![](ECC_files/figure-gfm/Lambda_Comparison-5.png)<!-- -->![](ECC_files/figure-gfm/Lambda_Comparison-6.png)<!-- -->

### S4-4-7 KS test and Stats

We also performed a KS test to test the FM lambdas and STL FM lambdas
for different factors. It seems that their distributions are different.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

KS Test for Fama Mecbeth Lambdas and STL FM Lambdas

</caption>

<thead>

<tr>

<th style="text-align:center;">

model

</th>

<th style="text-align:center;">

Factors

</th>

<th style="text-align:center;">

statistic

</th>

<th style="text-align:center;">

p.value

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="5">

FF5

</td>

<td style="text-align:center;">

Mkt-RF

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

SMB

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

HML

</td>

<td style="text-align:center;">

0.2712477

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

RMW

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

CMA

</td>

<td style="text-align:center;">

0.2658228

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="5">

PRS

</td>

<td style="text-align:center;">

Mkt-RF

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

RMW

</td>

<td style="text-align:center;">

0.2875226

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

dDP

</td>

<td style="text-align:center;">

0.3001808

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

dTS

</td>

<td style="text-align:center;">

0.2585895

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;">

UNEXPI

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

</tr>

</tbody>

</table>

Here is a comparison of the lambda statistics of the Normal Fama Macbeth
and Fama Macbeth Second Step Regression with STL Trend Data.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama Macbeth/STL Fama Macbeth Lambda0 Stats

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="2">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="5">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

stats

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

model

</th>

<th style="text-align:center;">

method

</th>

<th style="text-align:center;">

mean

</th>

<th style="text-align:center;">

variance

</th>

<th style="text-align:center;">

skewness

</th>

<th style="text-align:center;">

kurtosis

</th>

<th style="text-align:center;">

z\_score

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="2">

FF5

</td>

<td style="text-align:center;">

FM

</td>

<td style="text-align:center;">

0.0055707

</td>

<td style="text-align:center;">

0.0013966

</td>

<td style="text-align:center;">

\-0.2170809

</td>

<td style="text-align:center;">

3.768015

</td>

<td style="text-align:center;">

3.505384

</td>

</tr>

<tr>

<td style="text-align:center;">

FM\_STL

</td>

<td style="text-align:center;">

0.0055743

</td>

<td style="text-align:center;">

0.0001028

</td>

<td style="text-align:center;">

\-0.2492236

</td>

<td style="text-align:center;">

5.278078

</td>

<td style="text-align:center;">

12.926188

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="2">

PRS

</td>

<td style="text-align:center;">

FM

</td>

<td style="text-align:center;">

0.0036899

</td>

<td style="text-align:center;">

0.0014401

</td>

<td style="text-align:center;">

\-0.1204099

</td>

<td style="text-align:center;">

3.625933

</td>

<td style="text-align:center;">

2.286575

</td>

</tr>

<tr>

<td style="text-align:center;">

FM\_STL

</td>

<td style="text-align:center;">

0.0040573

</td>

<td style="text-align:center;">

0.0001250

</td>

<td style="text-align:center;">

0.1192528

</td>

<td style="text-align:center;">

2.876564

</td>

<td style="text-align:center;">

8.534376

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama French Five Factors Lambdas

</caption>

<thead>

<tr>

<th style="text-align:center;">

method

</th>

<th style="text-align:center;">

stats

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0009206

</td>

<td style="text-align:center;">

0.0008839

</td>

<td style="text-align:center;">

\-0.0001184

</td>

<td style="text-align:center;">

0.0000019

</td>

<td style="text-align:center;">

0.0016968

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0035331

</td>

<td style="text-align:center;">

0.0011442

</td>

<td style="text-align:center;">

0.0012661

</td>

<td style="text-align:center;">

0.0007741

</td>

<td style="text-align:center;">

0.0006425

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0613148

</td>

<td style="text-align:center;">

0.0164253

</td>

<td style="text-align:center;">

\-0.3765078

</td>

<td style="text-align:center;">

\-0.1904382

</td>

<td style="text-align:center;">

0.0781917

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.7140032

</td>

<td style="text-align:center;">

5.3531912

</td>

<td style="text-align:center;">

5.3248040

</td>

<td style="text-align:center;">

6.6515963

</td>

<td style="text-align:center;">

4.8082920

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_7\_N\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0009566

</td>

<td style="text-align:center;">

0.0009989

</td>

<td style="text-align:center;">

0.0004335

</td>

<td style="text-align:center;">

0.0000172

</td>

<td style="text-align:center;">

0.0013575

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0001520

</td>

<td style="text-align:center;">

0.0000776

</td>

<td style="text-align:center;">

0.0001157

</td>

<td style="text-align:center;">

0.0000382

</td>

<td style="text-align:center;">

0.0000610

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1550185

</td>

<td style="text-align:center;">

\-0.5120027

</td>

<td style="text-align:center;">

\-0.6922562

</td>

<td style="text-align:center;">

0.1981961

</td>

<td style="text-align:center;">

\-0.3779798

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.7953765

</td>

<td style="text-align:center;">

3.7026879

</td>

<td style="text-align:center;">

5.2279827

</td>

<td style="text-align:center;">

4.7247995

</td>

<td style="text-align:center;">

4.0414197

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_7\_R\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0019549

</td>

<td style="text-align:center;">

0.0019510

</td>

<td style="text-align:center;">

0.0017124

</td>

<td style="text-align:center;">

0.0005276

</td>

<td style="text-align:center;">

0.0013168

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0002194

</td>

<td style="text-align:center;">

0.0001205

</td>

<td style="text-align:center;">

0.0001202

</td>

<td style="text-align:center;">

0.0000567

</td>

<td style="text-align:center;">

0.0000778

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.9560655

</td>

<td style="text-align:center;">

0.1356300

</td>

<td style="text-align:center;">

\-0.0032643

</td>

<td style="text-align:center;">

1.4479085

</td>

<td style="text-align:center;">

\-0.2019692

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

6.8650921

</td>

<td style="text-align:center;">

3.7082069

</td>

<td style="text-align:center;">

3.9002004

</td>

<td style="text-align:center;">

6.2655494

</td>

<td style="text-align:center;">

3.7179920

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_15\_N\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0009559

</td>

<td style="text-align:center;">

0.0010388

</td>

<td style="text-align:center;">

0.0004248

</td>

<td style="text-align:center;">

0.0000193

</td>

<td style="text-align:center;">

0.0013788

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0001671

</td>

<td style="text-align:center;">

0.0000815

</td>

<td style="text-align:center;">

0.0001250

</td>

<td style="text-align:center;">

0.0000419

</td>

<td style="text-align:center;">

0.0000651

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1165010

</td>

<td style="text-align:center;">

\-0.5211631

</td>

<td style="text-align:center;">

\-0.7019668

</td>

<td style="text-align:center;">

0.1619697

</td>

<td style="text-align:center;">

\-0.3576490

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.8691101

</td>

<td style="text-align:center;">

3.7525148

</td>

<td style="text-align:center;">

5.3854968

</td>

<td style="text-align:center;">

4.6711588

</td>

<td style="text-align:center;">

4.1704342

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_15\_R\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0010667

</td>

<td style="text-align:center;">

0.0006087

</td>

<td style="text-align:center;">

0.0029786

</td>

<td style="text-align:center;">

0.0003642

</td>

<td style="text-align:center;">

0.0020707

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0002392

</td>

<td style="text-align:center;">

0.0001316

</td>

<td style="text-align:center;">

0.0001367

</td>

<td style="text-align:center;">

0.0000678

</td>

<td style="text-align:center;">

0.0000913

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.4970782

</td>

<td style="text-align:center;">

\-0.1411555

</td>

<td style="text-align:center;">

0.2945888

</td>

<td style="text-align:center;">

1.5817513

</td>

<td style="text-align:center;">

\-0.2289187

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.8182672

</td>

<td style="text-align:center;">

4.4954640

</td>

<td style="text-align:center;">

4.0525142

</td>

<td style="text-align:center;">

6.6975906

</td>

<td style="text-align:center;">

3.5949859

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_40\_N\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0009346

</td>

<td style="text-align:center;">

0.0010411

</td>

<td style="text-align:center;">

0.0004122

</td>

<td style="text-align:center;">

0.0000229

</td>

<td style="text-align:center;">

0.0014039

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0001905

</td>

<td style="text-align:center;">

0.0000883

</td>

<td style="text-align:center;">

0.0001380

</td>

<td style="text-align:center;">

0.0000475

</td>

<td style="text-align:center;">

0.0000708

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1040944

</td>

<td style="text-align:center;">

\-0.5276172

</td>

<td style="text-align:center;">

\-0.7021418

</td>

<td style="text-align:center;">

0.0748384

</td>

<td style="text-align:center;">

\-0.3171385

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.9256029

</td>

<td style="text-align:center;">

3.7886325

</td>

<td style="text-align:center;">

5.5700599

</td>

<td style="text-align:center;">

4.6621086

</td>

<td style="text-align:center;">

4.4242504

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_40\_R\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001875

</td>

<td style="text-align:center;">

0.0003927

</td>

<td style="text-align:center;">

0.0029093

</td>

<td style="text-align:center;">

0.0013233

</td>

<td style="text-align:center;">

0.0023770

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0003007

</td>

<td style="text-align:center;">

0.0001405

</td>

<td style="text-align:center;">

0.0001607

</td>

<td style="text-align:center;">

0.0000938

</td>

<td style="text-align:center;">

0.0001034

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.2388522

</td>

<td style="text-align:center;">

\-0.1610710

</td>

<td style="text-align:center;">

0.4864388

</td>

<td style="text-align:center;">

1.9358443

</td>

<td style="text-align:center;">

\-0.1106050

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.9478722

</td>

<td style="text-align:center;">

4.1071754

</td>

<td style="text-align:center;">

4.9416716

</td>

<td style="text-align:center;">

8.0162557

</td>

<td style="text-align:center;">

4.0449030

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

RAM\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0051121

</td>

<td style="text-align:center;">

0.0022967

</td>

<td style="text-align:center;">

0.0032389

</td>

<td style="text-align:center;">

0.0027066

</td>

<td style="text-align:center;">

0.0030245

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0000280

</td>

<td style="text-align:center;">

0.0000284

</td>

<td style="text-align:center;">

0.0000156

</td>

<td style="text-align:center;">

0.0000075

</td>

<td style="text-align:center;">

0.0000093

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0223254

</td>

<td style="text-align:center;">

0.3948825

</td>

<td style="text-align:center;">

0.1498031

</td>

<td style="text-align:center;">

0.1038219

</td>

<td style="text-align:center;">

0.5005268

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.3686070

</td>

<td style="text-align:center;">

2.2736340

</td>

<td style="text-align:center;">

2.9118074

</td>

<td style="text-align:center;">

3.4515945

</td>

<td style="text-align:center;">

3.1245590

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

RGM\_FF5

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0041103

</td>

<td style="text-align:center;">

0.0018484

</td>

<td style="text-align:center;">

0.0028396

</td>

<td style="text-align:center;">

0.0024631

</td>

<td style="text-align:center;">

0.0028268

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0000300

</td>

<td style="text-align:center;">

0.0000280

</td>

<td style="text-align:center;">

0.0000152

</td>

<td style="text-align:center;">

0.0000070

</td>

<td style="text-align:center;">

0.0000089

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0270841

</td>

<td style="text-align:center;">

0.3753467

</td>

<td style="text-align:center;">

0.1104960

</td>

<td style="text-align:center;">

\-0.0376499

</td>

<td style="text-align:center;">

0.4463740

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.2899895

</td>

<td style="text-align:center;">

2.2857798

</td>

<td style="text-align:center;">

2.9634918

</td>

<td style="text-align:center;">

3.3248415

</td>

<td style="text-align:center;">

3.0420264

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

PRS Five Factors Lambdas

</caption>

<thead>

<tr>

<th style="text-align:center;">

method

</th>

<th style="text-align:center;">

stats

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0030404

</td>

<td style="text-align:center;">

\-0.0003644

</td>

<td style="text-align:center;">

\-0.0000901

</td>

<td style="text-align:center;">

\-0.0002660

</td>

<td style="text-align:center;">

0.0001747

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0035777

</td>

<td style="text-align:center;">

0.0007241

</td>

<td style="text-align:center;">

0.0000028

</td>

<td style="text-align:center;">

0.0000140

</td>

<td style="text-align:center;">

0.0000281

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0273199

</td>

<td style="text-align:center;">

\-0.3864678

</td>

<td style="text-align:center;">

\-0.0642360

</td>

<td style="text-align:center;">

\-0.2376992

</td>

<td style="text-align:center;">

\-0.1347035

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5708798

</td>

<td style="text-align:center;">

8.2197855

</td>

<td style="text-align:center;">

4.0558342

</td>

<td style="text-align:center;">

5.1619650

</td>

<td style="text-align:center;">

4.1129898

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_7\_N\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0026861

</td>

<td style="text-align:center;">

0.0000776

</td>

<td style="text-align:center;">

\-0.0000664

</td>

<td style="text-align:center;">

\-0.0001300

</td>

<td style="text-align:center;">

0.0001296

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0001805

</td>

<td style="text-align:center;">

0.0000419

</td>

<td style="text-align:center;">

0.0000002

</td>

<td style="text-align:center;">

0.0000012

</td>

<td style="text-align:center;">

0.0000023

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2365869

</td>

<td style="text-align:center;">

0.6982985

</td>

<td style="text-align:center;">

\-0.5648704

</td>

<td style="text-align:center;">

\-0.2633246

</td>

<td style="text-align:center;">

\-0.2289524

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.7136550

</td>

<td style="text-align:center;">

5.4140502

</td>

<td style="text-align:center;">

3.7941270

</td>

<td style="text-align:center;">

3.6190017

</td>

<td style="text-align:center;">

4.1463703

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_7\_R\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0040933

</td>

<td style="text-align:center;">

0.0005148

</td>

<td style="text-align:center;">

\-0.0000272

</td>

<td style="text-align:center;">

0.0000271

</td>

<td style="text-align:center;">

0.0001136

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0003168

</td>

<td style="text-align:center;">

0.0000771

</td>

<td style="text-align:center;">

0.0000003

</td>

<td style="text-align:center;">

0.0000020

</td>

<td style="text-align:center;">

0.0000026

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

1.1864085

</td>

<td style="text-align:center;">

1.3208387

</td>

<td style="text-align:center;">

\-0.0556996

</td>

<td style="text-align:center;">

\-0.2569690

</td>

<td style="text-align:center;">

\-0.1674264

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.9317575

</td>

<td style="text-align:center;">

5.9467606

</td>

<td style="text-align:center;">

3.9837431

</td>

<td style="text-align:center;">

3.2185529

</td>

<td style="text-align:center;">

3.4344196

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_15\_N\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0027072

</td>

<td style="text-align:center;">

0.0000770

</td>

<td style="text-align:center;">

\-0.0000655

</td>

<td style="text-align:center;">

\-0.0001314

</td>

<td style="text-align:center;">

0.0001317

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0001992

</td>

<td style="text-align:center;">

0.0000462

</td>

<td style="text-align:center;">

0.0000002

</td>

<td style="text-align:center;">

0.0000013

</td>

<td style="text-align:center;">

0.0000025

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2085670

</td>

<td style="text-align:center;">

0.6842127

</td>

<td style="text-align:center;">

\-0.5876918

</td>

<td style="text-align:center;">

\-0.1975122

</td>

<td style="text-align:center;">

\-0.2390837

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.7694297

</td>

<td style="text-align:center;">

5.4629924

</td>

<td style="text-align:center;">

3.8749536

</td>

<td style="text-align:center;">

3.4308913

</td>

<td style="text-align:center;">

4.3714310

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_15\_R\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0023440

</td>

<td style="text-align:center;">

0.0004156

</td>

<td style="text-align:center;">

\-0.0000282

</td>

<td style="text-align:center;">

0.0000208

</td>

<td style="text-align:center;">

0.0001299

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0003423

</td>

<td style="text-align:center;">

0.0000924

</td>

<td style="text-align:center;">

0.0000004

</td>

<td style="text-align:center;">

0.0000016

</td>

<td style="text-align:center;">

0.0000033

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.6855439

</td>

<td style="text-align:center;">

1.7330418

</td>

<td style="text-align:center;">

\-0.1023556

</td>

<td style="text-align:center;">

\-0.4342521

</td>

<td style="text-align:center;">

\-0.3922152

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2542720

</td>

<td style="text-align:center;">

7.4877396

</td>

<td style="text-align:center;">

4.8062028

</td>

<td style="text-align:center;">

3.8857504

</td>

<td style="text-align:center;">

3.3965484

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_40\_N\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0026991

</td>

<td style="text-align:center;">

0.0000660

</td>

<td style="text-align:center;">

\-0.0000650

</td>

<td style="text-align:center;">

\-0.0001375

</td>

<td style="text-align:center;">

0.0001347

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0002284

</td>

<td style="text-align:center;">

0.0000527

</td>

<td style="text-align:center;">

0.0000002

</td>

<td style="text-align:center;">

0.0000014

</td>

<td style="text-align:center;">

0.0000028

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1510075

</td>

<td style="text-align:center;">

0.6507755

</td>

<td style="text-align:center;">

\-0.6011059

</td>

<td style="text-align:center;">

\-0.1771874

</td>

<td style="text-align:center;">

\-0.2583973

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.8915768

</td>

<td style="text-align:center;">

5.5378452

</td>

<td style="text-align:center;">

3.9652704

</td>

<td style="text-align:center;">

3.4296390

</td>

<td style="text-align:center;">

4.5700563

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FM\_STL\_40\_R\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0016035

</td>

<td style="text-align:center;">

0.0013089

</td>

<td style="text-align:center;">

\-0.0000197

</td>

<td style="text-align:center;">

0.0000013

</td>

<td style="text-align:center;">

0.0001102

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0004042

</td>

<td style="text-align:center;">

0.0001089

</td>

<td style="text-align:center;">

0.0000004

</td>

<td style="text-align:center;">

0.0000020

</td>

<td style="text-align:center;">

0.0000036

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.3177321

</td>

<td style="text-align:center;">

2.0133797

</td>

<td style="text-align:center;">

\-0.1706345

</td>

<td style="text-align:center;">

\-0.4332321

</td>

<td style="text-align:center;">

\-0.3567612

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2242287

</td>

<td style="text-align:center;">

8.4693602

</td>

<td style="text-align:center;">

4.5946688

</td>

<td style="text-align:center;">

4.4758122

</td>

<td style="text-align:center;">

3.2996522

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

RAM\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0051121

</td>

<td style="text-align:center;">

0.0027066

</td>

<td style="text-align:center;">

0.0000226

</td>

<td style="text-align:center;">

0.0003300

</td>

<td style="text-align:center;">

0.0002188

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0000280

</td>

<td style="text-align:center;">

0.0000075

</td>

<td style="text-align:center;">

0.0000001

</td>

<td style="text-align:center;">

0.0000002

</td>

<td style="text-align:center;">

0.0000002

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0223254

</td>

<td style="text-align:center;">

0.1038219

</td>

<td style="text-align:center;">

\-0.0597998

</td>

<td style="text-align:center;">

\-0.3634110

</td>

<td style="text-align:center;">

\-0.4190866

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.3686070

</td>

<td style="text-align:center;">

3.4515945

</td>

<td style="text-align:center;">

3.4759408

</td>

<td style="text-align:center;">

2.9208853

</td>

<td style="text-align:center;">

3.2613141

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

RGM\_PRS

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0041103

</td>

<td style="text-align:center;">

0.0024631

</td>

<td style="text-align:center;">

0.0000220

</td>

<td style="text-align:center;">

0.0003271

</td>

<td style="text-align:center;">

0.0002139

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0000300

</td>

<td style="text-align:center;">

0.0000070

</td>

<td style="text-align:center;">

0.0000001

</td>

<td style="text-align:center;">

0.0000002

</td>

<td style="text-align:center;">

0.0000002

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0270841

</td>

<td style="text-align:center;">

\-0.0376499

</td>

<td style="text-align:center;">

\-0.0610550

</td>

<td style="text-align:center;">

\-0.3657935

</td>

<td style="text-align:center;">

\-0.4211790

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

2.2899895

</td>

<td style="text-align:center;">

3.3248415

</td>

<td style="text-align:center;">

3.4770569

</td>

<td style="text-align:center;">

2.9162949

</td>

<td style="text-align:center;">

3.2639812

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Fama Macbeth/STL Lambda Variance Ratio

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="5">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

FF5

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="5">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

PRS

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

choice

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

SMB

</th>

<th style="text-align:center;">

HML

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

CMA

</th>

<th style="text-align:center;">

Mkt-RF

</th>

<th style="text-align:center;">

RMW

</th>

<th style="text-align:center;">

dDP

</th>

<th style="text-align:center;">

dTS

</th>

<th style="text-align:center;">

UNEXPI

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

s7 norobust

</td>

<td style="text-align:center;">

23.24452

</td>

<td style="text-align:center;">

14.751162

</td>

<td style="text-align:center;">

10.944878

</td>

<td style="text-align:center;">

20.269394

</td>

<td style="text-align:center;">

10.525081

</td>

<td style="text-align:center;">

19.820988

</td>

<td style="text-align:center;">

17.276849

</td>

<td style="text-align:center;">

13.889648

</td>

<td style="text-align:center;">

11.299347

</td>

<td style="text-align:center;">

12.368107

</td>

</tr>

<tr>

<td style="text-align:center;">

s7 robust

</td>

<td style="text-align:center;">

16.10298

</td>

<td style="text-align:center;">

9.493088

</td>

<td style="text-align:center;">

10.529444

</td>

<td style="text-align:center;">

13.644140

</td>

<td style="text-align:center;">

8.255695

</td>

<td style="text-align:center;">

11.294073

</td>

<td style="text-align:center;">

9.386693

</td>

<td style="text-align:center;">

10.024348

</td>

<td style="text-align:center;">

6.972330

</td>

<td style="text-align:center;">

10.848982

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 norobust

</td>

<td style="text-align:center;">

21.14075

</td>

<td style="text-align:center;">

14.032428

</td>

<td style="text-align:center;">

10.129817

</td>

<td style="text-align:center;">

18.476326

</td>

<td style="text-align:center;">

9.862964

</td>

<td style="text-align:center;">

17.962607

</td>

<td style="text-align:center;">

15.675084

</td>

<td style="text-align:center;">

12.893170

</td>

<td style="text-align:center;">

10.747707

</td>

<td style="text-align:center;">

11.274582

</td>

</tr>

<tr>

<td style="text-align:center;">

s15 robust

</td>

<td style="text-align:center;">

14.77027

</td>

<td style="text-align:center;">

8.696222

</td>

<td style="text-align:center;">

9.259585

</td>

<td style="text-align:center;">

11.419013

</td>

<td style="text-align:center;">

7.036368

</td>

<td style="text-align:center;">

10.453411

</td>

<td style="text-align:center;">

7.837674

</td>

<td style="text-align:center;">

7.551489

</td>

<td style="text-align:center;">

8.521270

</td>

<td style="text-align:center;">

8.479725

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 norobust

</td>

<td style="text-align:center;">

18.54984

</td>

<td style="text-align:center;">

12.957591

</td>

<td style="text-align:center;">

9.171545

</td>

<td style="text-align:center;">

16.291649

</td>

<td style="text-align:center;">

9.074355

</td>

<td style="text-align:center;">

15.665184

</td>

<td style="text-align:center;">

13.751996

</td>

<td style="text-align:center;">

11.698110

</td>

<td style="text-align:center;">

9.824846

</td>

<td style="text-align:center;">

10.021593

</td>

</tr>

<tr>

<td style="text-align:center;">

s40 robust

</td>

<td style="text-align:center;">

11.74827

</td>

<td style="text-align:center;">

8.145603

</td>

<td style="text-align:center;">

7.878220

</td>

<td style="text-align:center;">

8.252691

</td>

<td style="text-align:center;">

6.214028

</td>

<td style="text-align:center;">

8.852425

</td>

<td style="text-align:center;">

6.646871

</td>

<td style="text-align:center;">

6.810901

</td>

<td style="text-align:center;">

7.138181

</td>

<td style="text-align:center;">

7.884968

</td>

</tr>

</tbody>

</table>

## S4-5 Why filtering might improve Esimated Lamdba?

### S4-5-1 Biased Regression

There is no need for trend extraction for 1st step regression, no matter
if we use the full sample or rolling window. The window should be large
enough to mitigate the seasonality effect. The second step regression,
however, is a cross sectional regression. A seasonal component in the
time series would disrupt the cross-sectional regression significantly.
So it is possible the the large volatility observed in the second step
regression is due to the seasonality.

Now, assume the return (or risk premium) is formed by the following
equation:

  
![r\_{it} =
\\beta\_{it}\*\\lambda\_t+\\eta\_{it}](https://latex.codecogs.com/png.latex?r_%7Bit%7D%20%3D%20%5Cbeta_%7Bit%7D%2A%5Clambda_t%2B%5Ceta_%7Bit%7D
"r_{it} = \\beta_{it}*\\lambda_t+\\eta_{it}")  

Where beta is the sector specific risk exposure, lambda is the factor
premium, and eta is the idiosyncratic noise.

  
![E\[\\eta\_{it}|i\]
= 0](https://latex.codecogs.com/png.latex?E%5B%5Ceta_%7Bit%7D%7Ci%5D%20%3D%200
"E[\\eta_{it}|i] = 0")  

However, the eta might actually contain 3 components:
![\\epsilon\_t](https://latex.codecogs.com/png.latex?%5Cepsilon_t
"\\epsilon_t"),
![s\_{im}](https://latex.codecogs.com/png.latex?s_%7Bim%7D "s_{im}"),
and
![epsilon\_{it}](https://latex.codecogs.com/png.latex?epsilon_%7Bit%7D
"epsilon_{it}").

  
![\\eta\_{it} = \\epsilon\_t + s\_{im} +
\\epsilon\_{it}](https://latex.codecogs.com/png.latex?%5Ceta_%7Bit%7D%20%3D%20%5Cepsilon_t%20%2B%20s_%7Bim%7D%20%2B%20%5Cepsilon_%7Bit%7D
"\\eta_{it} = \\epsilon_t + s_{im} + \\epsilon_{it}")  

eps\_t is the universal time-series error, s\_i is the sector-specific
seasonality, and eps\_it is the idiosyncratic error. Therefore, the
equation is actually:

  
![r\_{it} = \\beta\_{it}\*\\lambda\_t+\\epsilon\_t + s\_{im} +
\\epsilon\_{it}](https://latex.codecogs.com/png.latex?r_%7Bit%7D%20%3D%20%5Cbeta_%7Bit%7D%2A%5Clambda_t%2B%5Cepsilon_t%20%2B%20s_%7Bim%7D%20%2B%20%5Cepsilon_%7Bit%7D
"r_{it} = \\beta_{it}*\\lambda_t+\\epsilon_t + s_{im} + \\epsilon_{it}")  

Again, we would have:

  
![E\[\\epsilon\_t + s\_{im} + \\epsilon\_{it}|i\]
= 0](https://latex.codecogs.com/png.latex?E%5B%5Cepsilon_t%20%2B%20s_%7Bim%7D%20%2B%20%5Cepsilon_%7Bit%7D%7Ci%5D%20%3D%200
"E[\\epsilon_t + s_{im} + \\epsilon_{it}|i] = 0")  

However, the cross-sectional regression error at each time t:

  
![E\[\\epsilon\_t + s\_{im} + \\epsilon\_{it}|t\] =
\\epsilon\_t+s\_{im}](https://latex.codecogs.com/png.latex?E%5B%5Cepsilon_t%20%2B%20s_%7Bim%7D%20%2B%20%5Cepsilon_%7Bit%7D%7Ct%5D%20%3D%20%5Cepsilon_t%2Bs_%7Bim%7D
"E[\\epsilon_t + s_{im} + \\epsilon_{it}|t] = \\epsilon_t+s_{im}")  

The unbiased least square estimation requires the error term expected to
be 0. The existence of ![( \\epsilon\_t + s\_{im} |
t)](https://latex.codecogs.com/png.latex?%28%20%5Cepsilon_t%20%2B%20s_%7Bim%7D%20%7C%20t%29
"( \\epsilon_t + s_{im} | t)") in each cross-sectional regression,
therefore, would randomly bias the estimated lambda. (Biasness is the
last thing we want from a regression.) This might be why we see the FM
method lambdas behave so “abruptly”. If we randomly bias the lambda, the
regression error of lambda is similar to the one without bias at each t.
However, this bias is changing over time, which would add to the
regression error of the lambdas. And therefore, bias might manifest
itself in a higher standard error in the resulting ECC estimates.

The universal time-series error and the seasonality would actually bias
the lambda estimation. Filtering out the universal time-series noise and
seasonality would improve the lambda estimated. Now, I will illustrate
the effect of seasonality and universal time-series noise in the second
step regression through a simulation.

### S4-5-2 Simulation

We will perform 3 different simulations to possible illustrate how the
filtered method would help with the second step regression.

#### S4-5-2-1 Simulation with Random Parameters and Sin Lamdba

Suppose the true 49 sector betas are given (since our focus is lambda)
and each of them follows an ARIMA(1,1,0) process, with AR coefficient
0.9. For demonstration purpose, the Factor Premiums follows a sin
function lambda = sin(t/60\*pi)/10+0.5. The universal time-series noise
is the same for all the sectors, following N(0, 1^2); a sector-specific
seasonality is randomly generated for each sector following N(0,1^2),
and repeats each year; and the idiosyncratic error is also generated
following N(0, 0.3^2). The first value of 49 sector betas are generated
from N(1, 0.3^2). There are 600 data generated to represent monthly data
in 50 years.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

STL Decomposition Component Strength for Simulated Portfolio Risk
Premium: Random Beta and Noise + Sin Lambda

</caption>

<thead>

<tr>

<th style="text-align:center;">

Strength

</th>

<th style="text-align:center;">

V1

</th>

<th style="text-align:center;">

V10

</th>

<th style="text-align:center;">

V11

</th>

<th style="text-align:center;">

V12

</th>

<th style="text-align:center;">

V13

</th>

<th style="text-align:center;">

V14

</th>

<th style="text-align:center;">

V15

</th>

<th style="text-align:center;">

V16

</th>

<th style="text-align:center;">

V17

</th>

<th style="text-align:center;">

V18

</th>

<th style="text-align:center;">

V19

</th>

<th style="text-align:center;">

V2

</th>

<th style="text-align:center;">

V20

</th>

<th style="text-align:center;">

V21

</th>

<th style="text-align:center;">

V22

</th>

<th style="text-align:center;">

V23

</th>

<th style="text-align:center;">

V24

</th>

<th style="text-align:center;">

V25

</th>

<th style="text-align:center;">

V26

</th>

<th style="text-align:center;">

V27

</th>

<th style="text-align:center;">

V28

</th>

<th style="text-align:center;">

V29

</th>

<th style="text-align:center;">

V3

</th>

<th style="text-align:center;">

V30

</th>

<th style="text-align:center;">

V31

</th>

<th style="text-align:center;">

V32

</th>

<th style="text-align:center;">

V33

</th>

<th style="text-align:center;">

V34

</th>

<th style="text-align:center;">

V35

</th>

<th style="text-align:center;">

V36

</th>

<th style="text-align:center;">

V37

</th>

<th style="text-align:center;">

V38

</th>

<th style="text-align:center;">

V39

</th>

<th style="text-align:center;">

V4

</th>

<th style="text-align:center;">

V40

</th>

<th style="text-align:center;">

V41

</th>

<th style="text-align:center;">

V42

</th>

<th style="text-align:center;">

V43

</th>

<th style="text-align:center;">

V44

</th>

<th style="text-align:center;">

V45

</th>

<th style="text-align:center;">

V46

</th>

<th style="text-align:center;">

V47

</th>

<th style="text-align:center;">

V48

</th>

<th style="text-align:center;">

V49

</th>

<th style="text-align:center;">

V5

</th>

<th style="text-align:center;">

V6

</th>

<th style="text-align:center;">

V7

</th>

<th style="text-align:center;">

V8

</th>

<th style="text-align:center;">

V9

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

FS

</td>

<td style="text-align:center;">

0.2731571

</td>

<td style="text-align:center;">

0.3040972

</td>

<td style="text-align:center;">

0.2748374

</td>

<td style="text-align:center;">

0.3346482

</td>

<td style="text-align:center;">

0.2828263

</td>

<td style="text-align:center;">

0.2989162

</td>

<td style="text-align:center;">

0.3284608

</td>

<td style="text-align:center;">

0.2911029

</td>

<td style="text-align:center;">

0.2851915

</td>

<td style="text-align:center;">

0.2917426

</td>

<td style="text-align:center;">

0.2707331

</td>

<td style="text-align:center;">

0.3121570

</td>

<td style="text-align:center;">

0.2784612

</td>

<td style="text-align:center;">

0.2766135

</td>

<td style="text-align:center;">

0.3145189

</td>

<td style="text-align:center;">

0.2831406

</td>

<td style="text-align:center;">

0.3016792

</td>

<td style="text-align:center;">

0.3352061

</td>

<td style="text-align:center;">

0.3147627

</td>

<td style="text-align:center;">

0.2881136

</td>

<td style="text-align:center;">

0.3284747

</td>

<td style="text-align:center;">

0.2986409

</td>

<td style="text-align:center;">

0.3066383

</td>

<td style="text-align:center;">

0.3351108

</td>

<td style="text-align:center;">

0.3149059

</td>

<td style="text-align:center;">

0.2921494

</td>

<td style="text-align:center;">

0.3092182

</td>

<td style="text-align:center;">

0.2689717

</td>

<td style="text-align:center;">

0.3131285

</td>

<td style="text-align:center;">

0.3170629

</td>

<td style="text-align:center;">

0.2815998

</td>

<td style="text-align:center;">

0.3017937

</td>

<td style="text-align:center;">

0.2887340

</td>

<td style="text-align:center;">

0.2853677

</td>

<td style="text-align:center;">

0.3043975

</td>

<td style="text-align:center;">

0.2924982

</td>

<td style="text-align:center;">

0.3170491

</td>

<td style="text-align:center;">

0.3175839

</td>

<td style="text-align:center;">

0.2786202

</td>

<td style="text-align:center;">

0.3085931

</td>

<td style="text-align:center;">

0.2939152

</td>

<td style="text-align:center;">

0.2808100

</td>

<td style="text-align:center;">

0.3004393

</td>

<td style="text-align:center;">

0.2749622

</td>

<td style="text-align:center;">

0.3510999

</td>

<td style="text-align:center;">

0.2881941

</td>

<td style="text-align:center;">

0.2672899

</td>

<td style="text-align:center;">

0.2885976

</td>

<td style="text-align:center;">

0.3059426

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FT

</td>

<td style="text-align:center;">

0.1764298

</td>

<td style="text-align:center;">

0.1571544

</td>

<td style="text-align:center;">

0.1512509

</td>

<td style="text-align:center;">

0.1497350

</td>

<td style="text-align:center;">

0.1611235

</td>

<td style="text-align:center;">

0.1685881

</td>

<td style="text-align:center;">

0.1911624

</td>

<td style="text-align:center;">

0.1595961

</td>

<td style="text-align:center;">

0.1881474

</td>

<td style="text-align:center;">

0.1956984

</td>

<td style="text-align:center;">

0.1679824

</td>

<td style="text-align:center;">

0.1641449

</td>

<td style="text-align:center;">

0.2074312

</td>

<td style="text-align:center;">

0.1616034

</td>

<td style="text-align:center;">

0.1620607

</td>

<td style="text-align:center;">

0.1730118

</td>

<td style="text-align:center;">

0.1766091

</td>

<td style="text-align:center;">

0.1711152

</td>

<td style="text-align:center;">

0.1612262

</td>

<td style="text-align:center;">

0.1629164

</td>

<td style="text-align:center;">

0.1384298

</td>

<td style="text-align:center;">

0.1733320

</td>

<td style="text-align:center;">

0.1466235

</td>

<td style="text-align:center;">

0.1670197

</td>

<td style="text-align:center;">

0.1696323

</td>

<td style="text-align:center;">

0.1736013

</td>

<td style="text-align:center;">

0.1404461

</td>

<td style="text-align:center;">

0.1576189

</td>

<td style="text-align:center;">

0.1670335

</td>

<td style="text-align:center;">

0.1750563

</td>

<td style="text-align:center;">

0.1614590

</td>

<td style="text-align:center;">

0.1946870

</td>

<td style="text-align:center;">

0.1617112

</td>

<td style="text-align:center;">

0.1359685

</td>

<td style="text-align:center;">

0.1536370

</td>

<td style="text-align:center;">

0.1532254

</td>

<td style="text-align:center;">

0.1585231

</td>

<td style="text-align:center;">

0.1609291

</td>

<td style="text-align:center;">

0.1726524

</td>

<td style="text-align:center;">

0.2076426

</td>

<td style="text-align:center;">

0.1779242

</td>

<td style="text-align:center;">

0.1803091

</td>

<td style="text-align:center;">

0.1984144

</td>

<td style="text-align:center;">

0.1659429

</td>

<td style="text-align:center;">

0.2190146

</td>

<td style="text-align:center;">

0.1655844

</td>

<td style="text-align:center;">

0.1723806

</td>

<td style="text-align:center;">

0.1763398

</td>

<td style="text-align:center;">

0.1660019

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Sim1-1.png)<!-- -->

#### S4-5-2-2 Simulation with Random Parameter and Random Smooth Lambda

Now, we are going to replace the sin function with a random smooth
function. The truly expected factor premium should not behave too
crazily so it should be roughly a smooth curve, and for any smooth curve
on earth, we can apply a Fourier Transformation to convert it to a
linear combination of sin and cos equations. If you do not believe that
the truly expected factor premium is smooth, at least it is an impulse
response process (it shifts when information hits it) and therefore can
be Fourier Transformed. So, we can apply a Fourier transformation
equation to simulate a random curve as the true factor premium.

The ramdom Fourier Lambdas are generated by the following Fourier
Equations:

  
![f(t) = a\_0+\\sum\_{i=1}^n(a\_i
cos(it)+b\_isin(it))](https://latex.codecogs.com/png.latex?f%28t%29%20%3D%20a_0%2B%5Csum_%7Bi%3D1%7D%5En%28a_i%20cos%28it%29%2Bb_isin%28it%29%29
"f(t) = a_0+\\sum_{i=1}^n(a_i cos(it)+b_isin(it))")  

The ![a\_0](https://latex.codecogs.com/png.latex?a_0 "a_0") is from a
normal distribution N(0.01,0.002^2), both
![a\_i](https://latex.codecogs.com/png.latex?a_i "a_i") and
![b\_i](https://latex.codecogs.com/png.latex?b_i "b_i") are following a
normal distribution N(0,0.025^2), and the n is a random integer between
20 and 100. This is a random smooth function and
![f(t)](https://latex.codecogs.com/png.latex?f%28t%29 "f(t)") is the
random Fourier Lambda.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

STL Decomposition Component Strength for Simulated Portfolio Risk
Premium: Random Beta and Noise + Random Fourier Lambda

</caption>

<thead>

<tr>

<th style="text-align:center;">

Strength

</th>

<th style="text-align:center;">

V1

</th>

<th style="text-align:center;">

V10

</th>

<th style="text-align:center;">

V11

</th>

<th style="text-align:center;">

V12

</th>

<th style="text-align:center;">

V13

</th>

<th style="text-align:center;">

V14

</th>

<th style="text-align:center;">

V15

</th>

<th style="text-align:center;">

V16

</th>

<th style="text-align:center;">

V17

</th>

<th style="text-align:center;">

V18

</th>

<th style="text-align:center;">

V19

</th>

<th style="text-align:center;">

V2

</th>

<th style="text-align:center;">

V20

</th>

<th style="text-align:center;">

V21

</th>

<th style="text-align:center;">

V22

</th>

<th style="text-align:center;">

V23

</th>

<th style="text-align:center;">

V24

</th>

<th style="text-align:center;">

V25

</th>

<th style="text-align:center;">

V26

</th>

<th style="text-align:center;">

V27

</th>

<th style="text-align:center;">

V28

</th>

<th style="text-align:center;">

V29

</th>

<th style="text-align:center;">

V3

</th>

<th style="text-align:center;">

V30

</th>

<th style="text-align:center;">

V31

</th>

<th style="text-align:center;">

V32

</th>

<th style="text-align:center;">

V33

</th>

<th style="text-align:center;">

V34

</th>

<th style="text-align:center;">

V35

</th>

<th style="text-align:center;">

V36

</th>

<th style="text-align:center;">

V37

</th>

<th style="text-align:center;">

V38

</th>

<th style="text-align:center;">

V39

</th>

<th style="text-align:center;">

V4

</th>

<th style="text-align:center;">

V40

</th>

<th style="text-align:center;">

V41

</th>

<th style="text-align:center;">

V42

</th>

<th style="text-align:center;">

V43

</th>

<th style="text-align:center;">

V44

</th>

<th style="text-align:center;">

V45

</th>

<th style="text-align:center;">

V46

</th>

<th style="text-align:center;">

V47

</th>

<th style="text-align:center;">

V48

</th>

<th style="text-align:center;">

V49

</th>

<th style="text-align:center;">

V5

</th>

<th style="text-align:center;">

V6

</th>

<th style="text-align:center;">

V7

</th>

<th style="text-align:center;">

V8

</th>

<th style="text-align:center;">

V9

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

FS

</td>

<td style="text-align:center;">

0.2731564

</td>

<td style="text-align:center;">

0.3040592

</td>

<td style="text-align:center;">

0.2748405

</td>

<td style="text-align:center;">

0.3346912

</td>

<td style="text-align:center;">

0.2827652

</td>

<td style="text-align:center;">

0.2986763

</td>

<td style="text-align:center;">

0.3284916

</td>

<td style="text-align:center;">

0.2910822

</td>

<td style="text-align:center;">

0.2851167

</td>

<td style="text-align:center;">

0.2917340

</td>

<td style="text-align:center;">

0.2706293

</td>

<td style="text-align:center;">

0.3121695

</td>

<td style="text-align:center;">

0.2783417

</td>

<td style="text-align:center;">

0.2766421

</td>

<td style="text-align:center;">

0.3145199

</td>

<td style="text-align:center;">

0.2831407

</td>

<td style="text-align:center;">

0.3017363

</td>

<td style="text-align:center;">

0.3351779

</td>

<td style="text-align:center;">

0.3146133

</td>

<td style="text-align:center;">

0.2881331

</td>

<td style="text-align:center;">

0.3285781

</td>

<td style="text-align:center;">

0.2983129

</td>

<td style="text-align:center;">

0.306487

</td>

<td style="text-align:center;">

0.3349439

</td>

<td style="text-align:center;">

0.3149940

</td>

<td style="text-align:center;">

0.2921347

</td>

<td style="text-align:center;">

0.3091281

</td>

<td style="text-align:center;">

0.2689724

</td>

<td style="text-align:center;">

0.3132159

</td>

<td style="text-align:center;">

0.316953

</td>

<td style="text-align:center;">

0.2816797

</td>

<td style="text-align:center;">

0.301810

</td>

<td style="text-align:center;">

0.2887089

</td>

<td style="text-align:center;">

0.2852283

</td>

<td style="text-align:center;">

0.3043262

</td>

<td style="text-align:center;">

0.2924702

</td>

<td style="text-align:center;">

0.3169784

</td>

<td style="text-align:center;">

0.3175624

</td>

<td style="text-align:center;">

0.2788053

</td>

<td style="text-align:center;">

0.3081793

</td>

<td style="text-align:center;">

0.2938226

</td>

<td style="text-align:center;">

0.2808753

</td>

<td style="text-align:center;">

0.3004236

</td>

<td style="text-align:center;">

0.2747320

</td>

<td style="text-align:center;">

0.3510811

</td>

<td style="text-align:center;">

0.2880763

</td>

<td style="text-align:center;">

0.2671374

</td>

<td style="text-align:center;">

0.2883794

</td>

<td style="text-align:center;">

0.3058941

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FT

</td>

<td style="text-align:center;">

0.1789011

</td>

<td style="text-align:center;">

0.1608041

</td>

<td style="text-align:center;">

0.1729239

</td>

<td style="text-align:center;">

0.1637743

</td>

<td style="text-align:center;">

0.1777141

</td>

<td style="text-align:center;">

0.2063206

</td>

<td style="text-align:center;">

0.1981820

</td>

<td style="text-align:center;">

0.1675661

</td>

<td style="text-align:center;">

0.2161320

</td>

<td style="text-align:center;">

0.2342431

</td>

<td style="text-align:center;">

0.1941462

</td>

<td style="text-align:center;">

0.1591451

</td>

<td style="text-align:center;">

0.2232872

</td>

<td style="text-align:center;">

0.1651869

</td>

<td style="text-align:center;">

0.1590148

</td>

<td style="text-align:center;">

0.1766445

</td>

<td style="text-align:center;">

0.1708795

</td>

<td style="text-align:center;">

0.1698330

</td>

<td style="text-align:center;">

0.1677709

</td>

<td style="text-align:center;">

0.1662717

</td>

<td style="text-align:center;">

0.1397884

</td>

<td style="text-align:center;">

0.2185614

</td>

<td style="text-align:center;">

0.164172

</td>

<td style="text-align:center;">

0.1910380

</td>

<td style="text-align:center;">

0.1763263

</td>

<td style="text-align:center;">

0.1817187

</td>

<td style="text-align:center;">

0.1631998

</td>

<td style="text-align:center;">

0.1588962

</td>

<td style="text-align:center;">

0.1615658

</td>

<td style="text-align:center;">

0.180404

</td>

<td style="text-align:center;">

0.1887229

</td>

<td style="text-align:center;">

0.229928

</td>

<td style="text-align:center;">

0.1781281

</td>

<td style="text-align:center;">

0.1497735

</td>

<td style="text-align:center;">

0.1740979

</td>

<td style="text-align:center;">

0.1639747

</td>

<td style="text-align:center;">

0.1750800

</td>

<td style="text-align:center;">

0.1698794

</td>

<td style="text-align:center;">

0.2088770

</td>

<td style="text-align:center;">

0.2757677

</td>

<td style="text-align:center;">

0.1812242

</td>

<td style="text-align:center;">

0.1754777

</td>

<td style="text-align:center;">

0.2063588

</td>

<td style="text-align:center;">

0.2022364

</td>

<td style="text-align:center;">

0.2441731

</td>

<td style="text-align:center;">

0.1838192

</td>

<td style="text-align:center;">

0.1883577

</td>

<td style="text-align:center;">

0.2133397

</td>

<td style="text-align:center;">

0.1872009

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Sim2-1.png)<!-- -->

    ## [1] 0.6060643

#### S4-5-2-3 Simulation with Actual Parameters and Smooth Lambdas

Finally, we would like to apply the actual Betas, Seasonality,
Time-series Error, and Idiosyncratic Error with a Fourier Smoothed
Lambda assumed to be the true lambda. This will illustrate how the
lambda estimation in the real data can be possibly improved.

We will extract the Seasonality and Noise from STL method, and then the
idiosyncratic noise from cross-sectional regression. The betas we use
are the 5-year rolling window beta.

![](ECC_files/figure-gfm/Sim3-1.png)<!-- -->![](ECC_files/figure-gfm/Sim3-2.png)<!-- -->

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

49 Industry Portfolio Error Component Summary Statistics

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="2">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Error Component

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

stats

</th>

<th style="text-align:center;">

Noise

</th>

<th style="text-align:center;">

Resid

</th>

<th style="text-align:center;">

Seasonal

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Aero

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000509

</td>

<td style="text-align:center;">

0.0022259

</td>

<td style="text-align:center;">

\-0.0001170

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0023188

</td>

<td style="text-align:center;">

0.0000747

</td>

<td style="text-align:center;">

0.0010712

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2969914

</td>

<td style="text-align:center;">

\-0.5638626

</td>

<td style="text-align:center;">

\-0.5072681

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4499248

</td>

<td style="text-align:center;">

3.6241683

</td>

<td style="text-align:center;">

4.3562388

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Agric

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000531

</td>

<td style="text-align:center;">

\-0.0002923

</td>

<td style="text-align:center;">

0.0001342

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0022339

</td>

<td style="text-align:center;">

0.0001178

</td>

<td style="text-align:center;">

0.0009227

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0493232

</td>

<td style="text-align:center;">

1.0637032

</td>

<td style="text-align:center;">

\-0.0490256

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5829899

</td>

<td style="text-align:center;">

7.6110927

</td>

<td style="text-align:center;">

3.7269152

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Autos

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0002450

</td>

<td style="text-align:center;">

\-0.0017010

</td>

<td style="text-align:center;">

\-0.0000215

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0027580

</td>

<td style="text-align:center;">

0.0001365

</td>

<td style="text-align:center;">

0.0011692

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0612042

</td>

<td style="text-align:center;">

2.1757614

</td>

<td style="text-align:center;">

0.7016818

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.3855323

</td>

<td style="text-align:center;">

15.2461417

</td>

<td style="text-align:center;">

7.2443446

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Banks

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000370

</td>

<td style="text-align:center;">

\-0.0007434

</td>

<td style="text-align:center;">

\-0.0000132

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0020135

</td>

<td style="text-align:center;">

0.0000512

</td>

<td style="text-align:center;">

0.0008918

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1460466

</td>

<td style="text-align:center;">

0.2418990

</td>

<td style="text-align:center;">

\-0.1401175

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.1473485

</td>

<td style="text-align:center;">

3.1144526

</td>

<td style="text-align:center;">

3.5677840

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Beer

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000378

</td>

<td style="text-align:center;">

0.0004433

</td>

<td style="text-align:center;">

\-0.0000568

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0014941

</td>

<td style="text-align:center;">

0.0000646

</td>

<td style="text-align:center;">

0.0006644

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0669276

</td>

<td style="text-align:center;">

0.2147800

</td>

<td style="text-align:center;">

\-0.2354574

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5023577

</td>

<td style="text-align:center;">

3.1534173

</td>

<td style="text-align:center;">

5.3104241

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

BldMt

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000117

</td>

<td style="text-align:center;">

\-0.0005241

</td>

<td style="text-align:center;">

\-0.0000278

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0021939

</td>

<td style="text-align:center;">

0.0000406

</td>

<td style="text-align:center;">

0.0010086

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1908276

</td>

<td style="text-align:center;">

\-0.5989819

</td>

<td style="text-align:center;">

0.2074275

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.1165517

</td>

<td style="text-align:center;">

4.6313633

</td>

<td style="text-align:center;">

4.7278995

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Books

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000251

</td>

<td style="text-align:center;">

\-0.0012003

</td>

<td style="text-align:center;">

\-0.0000183

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0017959

</td>

<td style="text-align:center;">

0.0000741

</td>

<td style="text-align:center;">

0.0007603

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0023874

</td>

<td style="text-align:center;">

\-0.0538865

</td>

<td style="text-align:center;">

0.1670989

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4111684

</td>

<td style="text-align:center;">

3.3343380

</td>

<td style="text-align:center;">

3.7284200

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Boxes

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000374

</td>

<td style="text-align:center;">

0.0006711

</td>

<td style="text-align:center;">

\-0.0000503

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0019637

</td>

<td style="text-align:center;">

0.0000766

</td>

<td style="text-align:center;">

0.0007687

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1912494

</td>

<td style="text-align:center;">

\-0.1090312

</td>

<td style="text-align:center;">

\-0.1700891

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2168868

</td>

<td style="text-align:center;">

3.9709776

</td>

<td style="text-align:center;">

3.5053433

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

BusSv

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000387

</td>

<td style="text-align:center;">

0.0003667

</td>

<td style="text-align:center;">

0.0000439

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0017141

</td>

<td style="text-align:center;">

0.0000252

</td>

<td style="text-align:center;">

0.0007256

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.3637742

</td>

<td style="text-align:center;">

\-0.5282809

</td>

<td style="text-align:center;">

\-0.0578777

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.9642851

</td>

<td style="text-align:center;">

4.5837665

</td>

<td style="text-align:center;">

3.8274163

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Chems

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000742

</td>

<td style="text-align:center;">

0.0004161

</td>

<td style="text-align:center;">

\-0.0000688

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0019577

</td>

<td style="text-align:center;">

0.0000453

</td>

<td style="text-align:center;">

0.0007803

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1609509

</td>

<td style="text-align:center;">

0.0383387

</td>

<td style="text-align:center;">

0.0341466

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.3013758

</td>

<td style="text-align:center;">

2.7969448

</td>

<td style="text-align:center;">

3.2591208

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Chips

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000839

</td>

<td style="text-align:center;">

0.0024218

</td>

<td style="text-align:center;">

\-0.0000833

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0031496

</td>

<td style="text-align:center;">

0.0000829

</td>

<td style="text-align:center;">

0.0012757

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2092896

</td>

<td style="text-align:center;">

0.7517270

</td>

<td style="text-align:center;">

\-0.1999405

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.2964874

</td>

<td style="text-align:center;">

3.3760411

</td>

<td style="text-align:center;">

5.1716138

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Clths

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000441

</td>

<td style="text-align:center;">

0.0015859

</td>

<td style="text-align:center;">

0.0000168

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0021819

</td>

<td style="text-align:center;">

0.0000666

</td>

<td style="text-align:center;">

0.0010723

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1497544

</td>

<td style="text-align:center;">

\-0.3436015

</td>

<td style="text-align:center;">

0.1227580

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.3011460

</td>

<td style="text-align:center;">

3.4566785

</td>

<td style="text-align:center;">

4.3749283

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Cnstr

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000039

</td>

<td style="text-align:center;">

\-0.0014165

</td>

<td style="text-align:center;">

0.0000496

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0029290

</td>

<td style="text-align:center;">

0.0001029

</td>

<td style="text-align:center;">

0.0012349

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2163360

</td>

<td style="text-align:center;">

0.3687560

</td>

<td style="text-align:center;">

\-0.0872456

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4963979

</td>

<td style="text-align:center;">

2.6957705

</td>

<td style="text-align:center;">

3.2430720

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Coal

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0002183

</td>

<td style="text-align:center;">

\-0.0006145

</td>

<td style="text-align:center;">

\-0.0001057

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0064209

</td>

<td style="text-align:center;">

0.0003568

</td>

<td style="text-align:center;">

0.0028125

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0270895

</td>

<td style="text-align:center;">

0.2056046

</td>

<td style="text-align:center;">

0.3194791

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.1617681

</td>

<td style="text-align:center;">

4.3122373

</td>

<td style="text-align:center;">

4.3935656

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Drugs

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000338

</td>

<td style="text-align:center;">

0.0001103

</td>

<td style="text-align:center;">

\-0.0000760

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0014868

</td>

<td style="text-align:center;">

0.0000343

</td>

<td style="text-align:center;">

0.0005663

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.1254102

</td>

<td style="text-align:center;">

\-0.0131004

</td>

<td style="text-align:center;">

0.2480485

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.0264767

</td>

<td style="text-align:center;">

2.5228340

</td>

<td style="text-align:center;">

4.6515378

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

ElcEq

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000278

</td>

<td style="text-align:center;">

0.0014950

</td>

<td style="text-align:center;">

\-0.0000792

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0023444

</td>

<td style="text-align:center;">

0.0000323

</td>

<td style="text-align:center;">

0.0009608

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2035731

</td>

<td style="text-align:center;">

0.2924939

</td>

<td style="text-align:center;">

\-0.0545667

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.7279423

</td>

<td style="text-align:center;">

3.6421570

</td>

<td style="text-align:center;">

3.3886519

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

FabPr

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000267

</td>

<td style="text-align:center;">

\-0.0015361

</td>

<td style="text-align:center;">

0.0000545

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0031162

</td>

<td style="text-align:center;">

0.0001092

</td>

<td style="text-align:center;">

0.0011838

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0153191

</td>

<td style="text-align:center;">

\-0.5039808

</td>

<td style="text-align:center;">

0.2170739

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.8933118

</td>

<td style="text-align:center;">

3.4574168

</td>

<td style="text-align:center;">

4.1327760

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Fin

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000200

</td>

<td style="text-align:center;">

0.0027705

</td>

<td style="text-align:center;">

0.0000032

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0021970

</td>

<td style="text-align:center;">

0.0000583

</td>

<td style="text-align:center;">

0.0008348

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.3539270

</td>

<td style="text-align:center;">

0.1163922

</td>

<td style="text-align:center;">

\-0.1894040

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.7631864

</td>

<td style="text-align:center;">

3.0904909

</td>

<td style="text-align:center;">

3.6709092

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Food

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000007

</td>

<td style="text-align:center;">

0.0002871

</td>

<td style="text-align:center;">

\-0.0000014

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0011213

</td>

<td style="text-align:center;">

0.0000320

</td>

<td style="text-align:center;">

0.0004580

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0665311

</td>

<td style="text-align:center;">

0.1702553

</td>

<td style="text-align:center;">

0.0942918

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.9314600

</td>

<td style="text-align:center;">

2.3552912

</td>

<td style="text-align:center;">

3.6390364

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Fun

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000099

</td>

<td style="text-align:center;">

0.0030918

</td>

<td style="text-align:center;">

\-0.0000588

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0029659

</td>

<td style="text-align:center;">

0.0001216

</td>

<td style="text-align:center;">

0.0014381

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.3528272

</td>

<td style="text-align:center;">

\-0.3158363

</td>

<td style="text-align:center;">

0.2147968

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5632775

</td>

<td style="text-align:center;">

3.2285774

</td>

<td style="text-align:center;">

4.1082462

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Gold

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001407

</td>

<td style="text-align:center;">

0.0009518

</td>

<td style="text-align:center;">

0.0000422

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0073743

</td>

<td style="text-align:center;">

0.0001921

</td>

<td style="text-align:center;">

0.0027980

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.2656551

</td>

<td style="text-align:center;">

0.1998028

</td>

<td style="text-align:center;">

0.9138509

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.7344656

</td>

<td style="text-align:center;">

3.1893606

</td>

<td style="text-align:center;">

6.4728123

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Guns

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000038

</td>

<td style="text-align:center;">

0.0028052

</td>

<td style="text-align:center;">

\-0.0000550

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0023550

</td>

<td style="text-align:center;">

0.0001017

</td>

<td style="text-align:center;">

0.0008961

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1970840

</td>

<td style="text-align:center;">

\-0.0817453

</td>

<td style="text-align:center;">

0.0706345

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.8834997

</td>

<td style="text-align:center;">

2.6346640

</td>

<td style="text-align:center;">

4.0091202

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Hardw

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000209

</td>

<td style="text-align:center;">

\-0.0003425

</td>

<td style="text-align:center;">

\-0.0000647

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0031082

</td>

<td style="text-align:center;">

0.0000948

</td>

<td style="text-align:center;">

0.0011867

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0016452

</td>

<td style="text-align:center;">

\-0.3979724

</td>

<td style="text-align:center;">

0.0536588

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5292911

</td>

<td style="text-align:center;">

2.3767986

</td>

<td style="text-align:center;">

4.3799688

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Hlth

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001546

</td>

<td style="text-align:center;">

0.0006959

</td>

<td style="text-align:center;">

0.0000052

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0027862

</td>

<td style="text-align:center;">

0.0001256

</td>

<td style="text-align:center;">

0.0011752

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1300384

</td>

<td style="text-align:center;">

\-0.0624674

</td>

<td style="text-align:center;">

\-0.1366119

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.8259132

</td>

<td style="text-align:center;">

2.7791679

</td>

<td style="text-align:center;">

4.0781697

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Hshld

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000138

</td>

<td style="text-align:center;">

\-0.0012966

</td>

<td style="text-align:center;">

\-0.0000795

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0012039

</td>

<td style="text-align:center;">

0.0000342

</td>

<td style="text-align:center;">

0.0005051

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1787213

</td>

<td style="text-align:center;">

\-1.2013780

</td>

<td style="text-align:center;">

0.1067881

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.9298907

</td>

<td style="text-align:center;">

8.3324932

</td>

<td style="text-align:center;">

4.1481763

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Insur

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000685

</td>

<td style="text-align:center;">

0.0005357

</td>

<td style="text-align:center;">

0.0000243

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0015070

</td>

<td style="text-align:center;">

0.0000408

</td>

<td style="text-align:center;">

0.0006940

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0145023

</td>

<td style="text-align:center;">

0.0293405

</td>

<td style="text-align:center;">

\-0.2234665

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2261243

</td>

<td style="text-align:center;">

3.3735439

</td>

<td style="text-align:center;">

3.5291096

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

LabEq

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000549

</td>

<td style="text-align:center;">

0.0012150

</td>

<td style="text-align:center;">

\-0.0000852

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0029874

</td>

<td style="text-align:center;">

0.0000569

</td>

<td style="text-align:center;">

0.0010425

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0369663

</td>

<td style="text-align:center;">

0.9909747

</td>

<td style="text-align:center;">

\-0.1640833

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.7963501

</td>

<td style="text-align:center;">

8.0454289

</td>

<td style="text-align:center;">

3.7443458

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Mach

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000226

</td>

<td style="text-align:center;">

0.0005770

</td>

<td style="text-align:center;">

\-0.0000116

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0024020

</td>

<td style="text-align:center;">

0.0000459

</td>

<td style="text-align:center;">

0.0009513

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2205315

</td>

<td style="text-align:center;">

\-0.3871431

</td>

<td style="text-align:center;">

\-0.3288396

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2940837

</td>

<td style="text-align:center;">

3.5446108

</td>

<td style="text-align:center;">

4.5528673

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Meals

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000235

</td>

<td style="text-align:center;">

\-0.0006733

</td>

<td style="text-align:center;">

\-0.0000784

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0017919

</td>

<td style="text-align:center;">

0.0000472

</td>

<td style="text-align:center;">

0.0007285

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2842865

</td>

<td style="text-align:center;">

\-0.6210854

</td>

<td style="text-align:center;">

\-0.3432362

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4797076

</td>

<td style="text-align:center;">

3.4393104

</td>

<td style="text-align:center;">

4.6594096

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

MedEq

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000708

</td>

<td style="text-align:center;">

\-0.0005863

</td>

<td style="text-align:center;">

\-0.0000258

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0016007

</td>

<td style="text-align:center;">

0.0000543

</td>

<td style="text-align:center;">

0.0006379

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1789201

</td>

<td style="text-align:center;">

\-0.5380144

</td>

<td style="text-align:center;">

\-0.1061039

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.5525295

</td>

<td style="text-align:center;">

4.3585728

</td>

<td style="text-align:center;">

3.2731740

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Mines

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001195

</td>

<td style="text-align:center;">

0.0021742

</td>

<td style="text-align:center;">

0.0000704

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0036296

</td>

<td style="text-align:center;">

0.0001080

</td>

<td style="text-align:center;">

0.0011863

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2408983

</td>

<td style="text-align:center;">

\-0.1412697

</td>

<td style="text-align:center;">

\-0.1343639

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.5478862

</td>

<td style="text-align:center;">

3.4744899

</td>

<td style="text-align:center;">

3.7039445

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Oil

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001127

</td>

<td style="text-align:center;">

0.0006244

</td>

<td style="text-align:center;">

0.0000597

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0021707

</td>

<td style="text-align:center;">

0.0000801

</td>

<td style="text-align:center;">

0.0007774

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0853560

</td>

<td style="text-align:center;">

0.2850402

</td>

<td style="text-align:center;">

0.5660070

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.8979075

</td>

<td style="text-align:center;">

3.6946531

</td>

<td style="text-align:center;">

4.0835170

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Other

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000187

</td>

<td style="text-align:center;">

\-0.0038102

</td>

<td style="text-align:center;">

0.0000225

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0022094

</td>

<td style="text-align:center;">

0.0000710

</td>

<td style="text-align:center;">

0.0009034

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2100342

</td>

<td style="text-align:center;">

\-0.0997927

</td>

<td style="text-align:center;">

\-0.1168204

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.1664205

</td>

<td style="text-align:center;">

3.6205541

</td>

<td style="text-align:center;">

3.7191726

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Paper

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000109

</td>

<td style="text-align:center;">

\-0.0006315

</td>

<td style="text-align:center;">

\-0.0000070

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0017939

</td>

<td style="text-align:center;">

0.0000397

</td>

<td style="text-align:center;">

0.0006619

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1241207

</td>

<td style="text-align:center;">

0.2433596

</td>

<td style="text-align:center;">

0.0460775

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.0556531

</td>

<td style="text-align:center;">

3.8311483

</td>

<td style="text-align:center;">

3.7241459

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

PerSv

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000197

</td>

<td style="text-align:center;">

\-0.0029905

</td>

<td style="text-align:center;">

0.0000706

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0022614

</td>

<td style="text-align:center;">

0.0000609

</td>

<td style="text-align:center;">

0.0008197

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0550326

</td>

<td style="text-align:center;">

\-0.3457587

</td>

<td style="text-align:center;">

\-0.1294835

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.3823429

</td>

<td style="text-align:center;">

4.0853947

</td>

<td style="text-align:center;">

3.5645186

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

RlEst

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000263

</td>

<td style="text-align:center;">

\-0.0041926

</td>

<td style="text-align:center;">

\-0.0000286

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0030640

</td>

<td style="text-align:center;">

0.0000960

</td>

<td style="text-align:center;">

0.0014537

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.4457618

</td>

<td style="text-align:center;">

\-0.2090267

</td>

<td style="text-align:center;">

0.9107560

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

12.2099242

</td>

<td style="text-align:center;">

3.1283550

</td>

<td style="text-align:center;">

10.4326386

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Rtail

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0001676

</td>

<td style="text-align:center;">

0.0003611

</td>

<td style="text-align:center;">

\-0.0000538

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0016388

</td>

<td style="text-align:center;">

0.0000536

</td>

<td style="text-align:center;">

0.0007233

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1453546

</td>

<td style="text-align:center;">

0.9721966

</td>

<td style="text-align:center;">

\-0.1461251

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.6774274

</td>

<td style="text-align:center;">

4.2817150

</td>

<td style="text-align:center;">

3.3283238

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Rubbr

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000359

</td>

<td style="text-align:center;">

\-0.0002457

</td>

<td style="text-align:center;">

\-0.0000427

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0019398

</td>

<td style="text-align:center;">

0.0000588

</td>

<td style="text-align:center;">

0.0009062

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1957441

</td>

<td style="text-align:center;">

\-0.6240663

</td>

<td style="text-align:center;">

\-0.0274027

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.0034896

</td>

<td style="text-align:center;">

3.1667420

</td>

<td style="text-align:center;">

4.7857813

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Ships

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001153

</td>

<td style="text-align:center;">

0.0002391

</td>

<td style="text-align:center;">

0.0000176

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0032555

</td>

<td style="text-align:center;">

0.0001026

</td>

<td style="text-align:center;">

0.0013427

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0528730

</td>

<td style="text-align:center;">

\-0.4668965

</td>

<td style="text-align:center;">

0.1819941

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.7834371

</td>

<td style="text-align:center;">

3.0733748

</td>

<td style="text-align:center;">

4.3282648

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Smoke

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000073

</td>

<td style="text-align:center;">

0.0026287

</td>

<td style="text-align:center;">

\-0.0000428

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0024284

</td>

<td style="text-align:center;">

0.0001164

</td>

<td style="text-align:center;">

0.0008113

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1024922

</td>

<td style="text-align:center;">

0.3531009

</td>

<td style="text-align:center;">

0.0545842

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.0838472

</td>

<td style="text-align:center;">

4.2393495

</td>

<td style="text-align:center;">

3.3913118

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Soda

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000417

</td>

<td style="text-align:center;">

\-0.0007619

</td>

<td style="text-align:center;">

\-0.0001151

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0025064

</td>

<td style="text-align:center;">

0.0000959

</td>

<td style="text-align:center;">

0.0010048

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.3384673

</td>

<td style="text-align:center;">

0.1025095

</td>

<td style="text-align:center;">

0.2385755

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

5.5470605

</td>

<td style="text-align:center;">

3.2006697

</td>

<td style="text-align:center;">

5.4499185

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Softw

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0001408

</td>

<td style="text-align:center;">

0.0029051

</td>

<td style="text-align:center;">

\-0.0000703

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0043342

</td>

<td style="text-align:center;">

0.0000755

</td>

<td style="text-align:center;">

0.0019265

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0120298

</td>

<td style="text-align:center;">

\-1.0155414

</td>

<td style="text-align:center;">

0.8398891

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4094943

</td>

<td style="text-align:center;">

5.9593268

</td>

<td style="text-align:center;">

9.6853614

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Steel

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000530

</td>

<td style="text-align:center;">

\-0.0012017

</td>

<td style="text-align:center;">

0.0000132

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0036254

</td>

<td style="text-align:center;">

0.0000875

</td>

<td style="text-align:center;">

0.0012876

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0563650

</td>

<td style="text-align:center;">

0.6331663

</td>

<td style="text-align:center;">

0.0447428

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.1953108

</td>

<td style="text-align:center;">

4.1851287

</td>

<td style="text-align:center;">

4.0433686

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Telcm

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000567

</td>

<td style="text-align:center;">

0.0000172

</td>

<td style="text-align:center;">

\-0.0000059

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0012521

</td>

<td style="text-align:center;">

0.0000876

</td>

<td style="text-align:center;">

0.0004921

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.1646993

</td>

<td style="text-align:center;">

\-0.1494092

</td>

<td style="text-align:center;">

\-0.1258483

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.4441432

</td>

<td style="text-align:center;">

4.2764916

</td>

<td style="text-align:center;">

3.3439989

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Toys

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000289

</td>

<td style="text-align:center;">

\-0.0023062

</td>

<td style="text-align:center;">

\-0.0000270

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0028384

</td>

<td style="text-align:center;">

0.0001107

</td>

<td style="text-align:center;">

0.0011627

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2376400

</td>

<td style="text-align:center;">

\-0.4244271

</td>

<td style="text-align:center;">

\-0.3036611

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.6166223

</td>

<td style="text-align:center;">

3.9513239

</td>

<td style="text-align:center;">

3.9330825

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Trans

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000263

</td>

<td style="text-align:center;">

\-0.0008331

</td>

<td style="text-align:center;">

\-0.0000225

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0017235

</td>

<td style="text-align:center;">

0.0000332

</td>

<td style="text-align:center;">

0.0008057

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.2809391

</td>

<td style="text-align:center;">

\-0.0827198

</td>

<td style="text-align:center;">

\-0.0885051

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.2412440

</td>

<td style="text-align:center;">

2.4166943

</td>

<td style="text-align:center;">

3.5668781

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Txtls

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0000065

</td>

<td style="text-align:center;">

\-0.0028270

</td>

<td style="text-align:center;">

0.0000378

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0030480

</td>

<td style="text-align:center;">

0.0001027

</td>

<td style="text-align:center;">

0.0014408

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

0.0112919

</td>

<td style="text-align:center;">

0.0254405

</td>

<td style="text-align:center;">

0.7155881

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

8.0332361

</td>

<td style="text-align:center;">

3.9966608

</td>

<td style="text-align:center;">

8.0101321

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Util

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

0.0001290

</td>

<td style="text-align:center;">

\-0.0003070

</td>

<td style="text-align:center;">

0.0000300

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0008705

</td>

<td style="text-align:center;">

0.0000521

</td>

<td style="text-align:center;">

0.0003717

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.0739852

</td>

<td style="text-align:center;">

\-0.2547901

</td>

<td style="text-align:center;">

0.1238850

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

3.3162753

</td>

<td style="text-align:center;">

3.8200972

</td>

<td style="text-align:center;">

3.4544205

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;vertical-align: middle !important;" rowspan="4">

Whlsl

</td>

<td style="text-align:center;">

mean

</td>

<td style="text-align:center;">

\-0.0000326

</td>

<td style="text-align:center;">

\-0.0005815

</td>

<td style="text-align:center;">

\-0.0000055

</td>

</tr>

<tr>

<td style="text-align:center;">

variance

</td>

<td style="text-align:center;">

0.0015439

</td>

<td style="text-align:center;">

0.0000353

</td>

<td style="text-align:center;">

0.0006297

</td>

</tr>

<tr>

<td style="text-align:center;">

skewness

</td>

<td style="text-align:center;">

\-0.3479152

</td>

<td style="text-align:center;">

\-0.1174412

</td>

<td style="text-align:center;">

\-0.2212298

</td>

</tr>

<tr>

<td style="text-align:center;">

kurtosis

</td>

<td style="text-align:center;">

4.8313939

</td>

<td style="text-align:center;">

4.8494597

</td>

<td style="text-align:center;">

3.9759001

</td>

</tr>

</tbody>

</table>

The Noise component is the time-series noise; the Seasonal component is
the Seasonality; the Resid component is the idiosyncratic noise. From
the standard deviation part, we can see in real data, the time-series
noise and seasonality is a large part of noise. Our assumptions about
large seasonality and time-series noise in the previous simulations are
valid.

In this simulation, I performed 100 simulations of random Fourier Fama
French 5 Factor Lambdas. In order to make the lambdas similar to the
estimated lambda, I adjusted the standard deviation of simulated lambdas
to be the same as standard deviation of the Estimated filtered Fama
Macbeth Lambdas.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

STL Decomposition Component Strength for Simulated Portfolio Risk
Premium: Acutal Beta and Noise + Random Fourier Lambda

</caption>

<thead>

<tr>

<th style="text-align:center;">

Strength

</th>

<th style="text-align:center;">

Aero

</th>

<th style="text-align:center;">

Agric

</th>

<th style="text-align:center;">

Autos

</th>

<th style="text-align:center;">

Banks

</th>

<th style="text-align:center;">

Beer

</th>

<th style="text-align:center;">

BldMt

</th>

<th style="text-align:center;">

Books

</th>

<th style="text-align:center;">

Boxes

</th>

<th style="text-align:center;">

BusSv

</th>

<th style="text-align:center;">

Chems

</th>

<th style="text-align:center;">

Chips

</th>

<th style="text-align:center;">

Clths

</th>

<th style="text-align:center;">

Cnstr

</th>

<th style="text-align:center;">

Coal

</th>

<th style="text-align:center;">

Drugs

</th>

<th style="text-align:center;">

ElcEq

</th>

<th style="text-align:center;">

FabPr

</th>

<th style="text-align:center;">

Fin

</th>

<th style="text-align:center;">

Food

</th>

<th style="text-align:center;">

Fun

</th>

<th style="text-align:center;">

Gold

</th>

<th style="text-align:center;">

Guns

</th>

<th style="text-align:center;">

Hardw

</th>

<th style="text-align:center;">

Hlth

</th>

<th style="text-align:center;">

Hshld

</th>

<th style="text-align:center;">

Insur

</th>

<th style="text-align:center;">

LabEq

</th>

<th style="text-align:center;">

Mach

</th>

<th style="text-align:center;">

Meals

</th>

<th style="text-align:center;">

MedEq

</th>

<th style="text-align:center;">

Mines

</th>

<th style="text-align:center;">

Oil

</th>

<th style="text-align:center;">

Other

</th>

<th style="text-align:center;">

Paper

</th>

<th style="text-align:center;">

PerSv

</th>

<th style="text-align:center;">

RlEst

</th>

<th style="text-align:center;">

Rtail

</th>

<th style="text-align:center;">

Rubbr

</th>

<th style="text-align:center;">

Ships

</th>

<th style="text-align:center;">

Smoke

</th>

<th style="text-align:center;">

Soda

</th>

<th style="text-align:center;">

Softw

</th>

<th style="text-align:center;">

Steel

</th>

<th style="text-align:center;">

Telcm

</th>

<th style="text-align:center;">

Toys

</th>

<th style="text-align:center;">

Trans

</th>

<th style="text-align:center;">

Txtls

</th>

<th style="text-align:center;">

Util

</th>

<th style="text-align:center;">

Whlsl

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

FS

</td>

<td style="text-align:center;">

0.4020201

</td>

<td style="text-align:center;">

0.3828984

</td>

<td style="text-align:center;">

0.4054573

</td>

<td style="text-align:center;">

0.4082312

</td>

<td style="text-align:center;">

0.3976898

</td>

<td style="text-align:center;">

0.4160108

</td>

<td style="text-align:center;">

0.3983799

</td>

<td style="text-align:center;">

0.3625758

</td>

<td style="text-align:center;">

0.3891262

</td>

<td style="text-align:center;">

0.3718857

</td>

<td style="text-align:center;">

0.3738292

</td>

<td style="text-align:center;">

0.4179890

</td>

<td style="text-align:center;">

0.3900986

</td>

<td style="text-align:center;">

0.3947077

</td>

<td style="text-align:center;">

0.3570130

</td>

<td style="text-align:center;">

0.3831629

</td>

<td style="text-align:center;">

0.3626465

</td>

<td style="text-align:center;">

0.3764355

</td>

<td style="text-align:center;">

0.3693705

</td>

<td style="text-align:center;">

0.4163183

</td>

<td style="text-align:center;">

0.3486968

</td>

<td style="text-align:center;">

0.3500392

</td>

<td style="text-align:center;">

0.3449402

</td>

<td style="text-align:center;">

0.3847559

</td>

<td style="text-align:center;">

0.3868054

</td>

<td style="text-align:center;">

0.4196529

</td>

<td style="text-align:center;">

0.3256755

</td>

<td style="text-align:center;">

0.3729274

</td>

<td style="text-align:center;">

0.3825072

</td>

<td style="text-align:center;">

0.3686946

</td>

<td style="text-align:center;">

0.3389983

</td>

<td style="text-align:center;">

0.3614319

</td>

<td style="text-align:center;">

0.3751450

</td>

<td style="text-align:center;">

0.3546682

</td>

<td style="text-align:center;">

0.3464305

</td>

<td style="text-align:center;">

0.4124311

</td>

<td style="text-align:center;">

0.3923469

</td>

<td style="text-align:center;">

0.4065176

</td>

<td style="text-align:center;">

0.3823389

</td>

<td style="text-align:center;">

0.3195475

</td>

<td style="text-align:center;">

0.3722978

</td>

<td style="text-align:center;">

0.3586688

</td>

<td style="text-align:center;">

0.3508761

</td>

<td style="text-align:center;">

0.3695746

</td>

<td style="text-align:center;">

0.3755067

</td>

<td style="text-align:center;">

0.4065055

</td>

<td style="text-align:center;">

0.4090120

</td>

<td style="text-align:center;">

0.3791374

</td>

<td style="text-align:center;">

0.3775596

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FT

</td>

<td style="text-align:center;">

0.1428494

</td>

<td style="text-align:center;">

0.1472960

</td>

<td style="text-align:center;">

0.1712486

</td>

<td style="text-align:center;">

0.1741679

</td>

<td style="text-align:center;">

0.1544587

</td>

<td style="text-align:center;">

0.1277345

</td>

<td style="text-align:center;">

0.1572968

</td>

<td style="text-align:center;">

0.1439276

</td>

<td style="text-align:center;">

0.1179586

</td>

<td style="text-align:center;">

0.1382169

</td>

<td style="text-align:center;">

0.1293600

</td>

<td style="text-align:center;">

0.1427692

</td>

<td style="text-align:center;">

0.1438046

</td>

<td style="text-align:center;">

0.1562804

</td>

<td style="text-align:center;">

0.1372406

</td>

<td style="text-align:center;">

0.1124601

</td>

<td style="text-align:center;">

0.1299934

</td>

<td style="text-align:center;">

0.1529140

</td>

<td style="text-align:center;">

0.1460946

</td>

<td style="text-align:center;">

0.1320239

</td>

<td style="text-align:center;">

0.1050698

</td>

<td style="text-align:center;">

0.1236652

</td>

<td style="text-align:center;">

0.1173722

</td>

<td style="text-align:center;">

0.1538252

</td>

<td style="text-align:center;">

0.1534018

</td>

<td style="text-align:center;">

0.1574408

</td>

<td style="text-align:center;">

0.1114699

</td>

<td style="text-align:center;">

0.1289561

</td>

<td style="text-align:center;">

0.1312438

</td>

<td style="text-align:center;">

0.1457866

</td>

<td style="text-align:center;">

0.1422623

</td>

<td style="text-align:center;">

0.1379026

</td>

<td style="text-align:center;">

0.1290666

</td>

<td style="text-align:center;">

0.1306973

</td>

<td style="text-align:center;">

0.1252609

</td>

<td style="text-align:center;">

0.1396282

</td>

<td style="text-align:center;">

0.1412953

</td>

<td style="text-align:center;">

0.1451990

</td>

<td style="text-align:center;">

0.1203995

</td>

<td style="text-align:center;">

0.1570057

</td>

<td style="text-align:center;">

0.1381827

</td>

<td style="text-align:center;">

0.1054866

</td>

<td style="text-align:center;">

0.1289831

</td>

<td style="text-align:center;">

0.1872276

</td>

<td style="text-align:center;">

0.1224745

</td>

<td style="text-align:center;">

0.1361467

</td>

<td style="text-align:center;">

0.1460563

</td>

<td style="text-align:center;">

0.2004986

</td>

<td style="text-align:center;">

0.1275598

</td>

</tr>

</tbody>

</table>

![](ECC_files/figure-gfm/Sim3_Figures-1.png)<!-- -->![](ECC_files/figure-gfm/Sim3_Figures-2.png)<!-- -->

#### S4-5-2-4 Regression Analysis of Simulation Results

We want two sets of regressions here:

1.  SSE Improvement of Estimated ECC vs. variance of Seasonal, Noise,
    and Resid

2.  ![\\sqrt{SSE}](https://latex.codecogs.com/png.latex?%5Csqrt%7BSSE%7D
    "\\sqrt{SSE}") vs. standard deviation of Seasonal, Noise, and Resid

<!-- end list -->

    ## 
    ## Call:
    ## lm(formula = Improvement ~ Seasonal + Noise + Resid, data = SSE_Error)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.7316 -0.3410  0.0198  0.3678  2.7770 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  1.095e+00  2.149e-02   50.96   <2e-16 ***
    ## Seasonal     2.293e+03  8.496e+01   26.99   <2e-16 ***
    ## Noise       -4.242e+02  3.376e+01  -12.56   <2e-16 ***
    ## Resid       -5.372e+03  2.881e+02  -18.65   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6283 on 4896 degrees of freedom
    ## Multiple R-squared:  0.3267, Adjusted R-squared:  0.3263 
    ## F-statistic: 791.9 on 3 and 4896 DF,  p-value: < 2.2e-16

    ##              var_Seasonal var_Noise var_Resid
    ## var_Seasonal    1.0000000 0.9733714 0.8022295
    ## var_Noise       0.9733714 1.0000000 0.7887358
    ## var_Resid       0.8022295 0.7887358 1.0000000

    ##             sd_Seasonal  sd_Noise  sd_Resid
    ## sd_Seasonal   1.0000000 0.9718994 0.7690278
    ## sd_Noise      0.9718994 1.0000000 0.7760378
    ## sd_Resid      0.7690278 0.7760378 1.0000000

    ## 
    ## Call:
    ## lm(formula = Improvement ~ Seasonal, data = SSE_Error)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.7660 -0.3711  0.0396  0.4134  2.2838 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)   1.11869    0.02235   50.05   <2e-16 ***
    ## Seasonal    810.31128   19.88290   40.75   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6615 on 4898 degrees of freedom
    ## Multiple R-squared:  0.2532, Adjusted R-squared:  0.2531 
    ## F-statistic:  1661 on 1 and 4898 DF,  p-value: < 2.2e-16

    ## 
    ## Call:
    ## lm(formula = Improvement ~ Resid, data = SSE_Error)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.7605 -0.4841  0.0101  0.4757  2.6700 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 1.627e+00  1.942e-02   83.79   <2e-16 ***
    ## Resid       3.922e+03  2.016e+02   19.46   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.7376 on 4898 degrees of freedom
    ## Multiple R-squared:  0.07175,    Adjusted R-squared:  0.07156 
    ## F-statistic: 378.6 on 1 and 4898 DF,  p-value: < 2.2e-16

    ## 
    ## Call:
    ## lm(formula = Improvement ~ Noise, data = SSE_Error)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -5.7849 -0.3945  0.0379  0.4296  2.5611 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)    1.203      0.023   52.32   <2e-16 ***
    ## Noise        298.548      8.393   35.57   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6824 on 4898 degrees of freedom
    ## Multiple R-squared:  0.2053, Adjusted R-squared:  0.2051 
    ## F-statistic:  1265 on 1 and 4898 DF,  p-value: < 2.2e-16

However, Seasonal, Noise, and Resid variances are really highly
correlated, the linear regression encounter a multicollinearity problem.
Since we have both Seasonal and Noise causing bias in cross-sectional
regression in our theoretical explanation, we combine the Seasonal and
Noise as Bias.

    ##           var_Bias var_Resid
    ## var_Bias  1.000000  0.802556
    ## var_Resid 0.802556  1.000000

    ##            sd_Bias  sd_Resid
    ## sd_Bias  1.0000000 0.7787272
    ## sd_Resid 0.7787272 1.0000000

    ## 
    ## Call:
    ## lm(formula = Improvement ~ Bias + Resid, data = SSE_Error2)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.0800 -0.3376  0.0352  0.3739  3.0285 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  1.068e+00  2.288e-02   46.67   <2e-16 ***
    ## Bias         3.157e+02  8.537e+00   36.98   <2e-16 ***
    ## Resid       -4.944e+03  2.988e+02  -16.55   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.6522 on 4897 degrees of freedom
    ## Multiple R-squared:  0.2744, Adjusted R-squared:  0.2741 
    ## F-statistic: 925.8 on 2 and 4897 DF,  p-value: < 2.2e-16

    ## 
    ## Call:
    ## lm(formula = sign(Improvement) * sqrt(abs(Improvement)) ~ sqrt(Bias) + 
    ##     sqrt(Resid), data = SSE_Error2)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.4536 -0.0980  0.0358  0.1405  0.7944 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)   0.65705    0.01867   35.19   <2e-16 ***
    ## sqrt(Bias)   18.41704    0.46706   39.43   <2e-16 ***
    ## sqrt(Resid) -51.07808    2.47531  -20.64   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.2632 on 4897 degrees of freedom
    ## Multiple R-squared:  0.2701, Adjusted R-squared:  0.2698 
    ## F-statistic: 906.3 on 2 and 4897 DF,  p-value: < 2.2e-16

The correlation of Bias and Resid variances (0.8) is not as much a
problem and we have two new sets of regressions:

1.  SSE Improvement of Estimated ECC vs. variance of Bias and Resid

2.  ![\\sqrt{SSE}](https://latex.codecogs.com/png.latex?%5Csqrt%7BSSE%7D
    "\\sqrt{SSE}") vs. standard deviation of Bias and Resid

From both regression results, we can see that the combined Bias term
encourage the filtering method.

Finally, to further address the Multicollinearity issue, we conducted a
principle component regression.

    ## Importance of components:
    ##                           PC1    PC2
    ## Standard deviation     1.3337 0.4704
    ## Proportion of Variance 0.8894 0.1106
    ## Cumulative Proportion  0.8894 1.0000

    ##              PC1        PC2
    ## Bias  -0.7071068 -0.7071068
    ## Resid -0.7071068  0.7071068

    ## 
    ## Call:
    ## lm(formula = Improvement ~ ., data = data.frame(Improvement = sign(SSE_Error2$Improvement) * 
    ##     sqrt(abs(SSE_Error2$Improvement)), (-SSE_Error2.pca$x)))
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.4536 -0.0980  0.0358  0.1405  0.7944 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 1.361612   0.003760  362.13   <2e-16 ***
    ## PC1         0.079666   0.002820   28.25   <2e-16 ***
    ## PC2         0.254581   0.007994   31.85   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.2632 on 4897 degrees of freedom
    ## Multiple R-squared:  0.2701, Adjusted R-squared:  0.2698 
    ## F-statistic: 906.3 on 2 and 4897 DF,  p-value: < 2.2e-16

  
![PC1 =
-0.707\*(Bias+Resid)](https://latex.codecogs.com/png.latex?PC1%20%3D%20-0.707%2A%28Bias%2BResid%29
"PC1 = -0.707*(Bias+Resid)")  
  
![PC2 =
-0.707\*(Bias-Resid)](https://latex.codecogs.com/png.latex?PC2%20%3D%20-0.707%2A%28Bias-Resid%29
"PC2 = -0.707*(Bias-Resid)")  

where Bias and Resid are standard deviations of Bias and Resid, To make
it easier to interpret, we flipped the sign such that ![PC1
= 0.707(Bias+Resid)](https://latex.codecogs.com/png.latex?PC1%20%3D%200.707%28Bias%2BResid%29
"PC1 = 0.707(Bias+Resid)"), which is approximately 0.707 times the total
Error of the return, and ![PC2
= 0.707(Bias-Resid)](https://latex.codecogs.com/png.latex?PC2%20%3D%200.707%28Bias-Resid%29
"PC2 = 0.707(Bias-Resid)"), which represents excess error from bias.

From the regression, we can see the PC1 (total Error) would cost the
accuracy of the ECC estimation and the PC2 (excess error from bias)
would also cost the accuracy of the ECC estimation. The Principal
Component Regression result further confirms our theoretical analysis
that the large bias from Seasonality and Time-series Noise relative to
the idiosyncratic noise (Resid) would cost the accuracy of the
cross-sectional regression.

# S5 Equity Cost of Captial

## S5-1 Estimated Equity Cost of Captial

As the equation indicates, ![ECC = \\sum\_{i \\in F}
\\beta\_i\*E\[F\_i\] +
R\_f](https://latex.codecogs.com/png.latex?ECC%20%3D%20%5Csum_%7Bi%20%5Cin%20F%7D%20%5Cbeta_i%2AE%5BF_i%5D%20%2B%20R_f
"ECC = \\sum_{i \\in F} \\beta_i*E[F_i] + R_f"). We will ignore the risk
free rate part and the Equity Cost of Capital in this section refers to
the estimated risk premium.

### S5-1-1 Arithmetic Mean

![](ECC_files/figure-gfm/AM_ECC-1.png)<!-- -->![](ECC_files/figure-gfm/AM_ECC-2.png)<!-- -->

### S5-1-2 Geometric Mean

![](ECC_files/figure-gfm/GM_ECC-1.png)<!-- -->![](ECC_files/figure-gfm/GM_ECC-2.png)<!-- -->

### S5-1-3 Fama Macbeth Second Step Regression

![](ECC_files/figure-gfm/FM_ECC-1.png)<!-- -->![](ECC_files/figure-gfm/FM_ECC-2.png)<!-- -->![](ECC_files/figure-gfm/FM_ECC-3.png)<!-- -->![](ECC_files/figure-gfm/FM_ECC-4.png)<!-- -->

### S5-1-4 Fama Macbeth Second Step Regression with STL Trend Data

![](ECC_files/figure-gfm/Filtered_FM_ECC-1.png)<!-- -->![](ECC_files/figure-gfm/Filtered_FM_ECC-2.png)<!-- -->![](ECC_files/figure-gfm/Filtered_FM_ECC-3.png)<!-- -->![](ECC_files/figure-gfm/Filtered_FM_ECC-4.png)<!-- -->

## S5-2 Comparative Statics

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Different Lambda Method Estimated ECC SSE

</caption>

<thead>

<tr>

<th style="text-align:center;">

Model

</th>

<th style="text-align:center;">

AM

</th>

<th style="text-align:center;">

GM

</th>

<th style="text-align:center;">

RAM

</th>

<th style="text-align:center;">

RGM

</th>

<th style="text-align:center;">

FM

</th>

<th style="text-align:center;">

FM\_STL\_7\_N

</th>

<th style="text-align:center;">

FM\_STL\_7\_R

</th>

<th style="text-align:center;">

FM\_STL\_15\_N

</th>

<th style="text-align:center;">

FM\_STL\_15\_R

</th>

<th style="text-align:center;">

FM\_STL\_40\_N

</th>

<th style="text-align:center;">

FM\_STL\_40\_R

</th>

<th style="text-align:center;">

0

</th>

<th style="text-align:center;">

Total Mean

</th>

<th style="text-align:center;">

Industry Mean

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

FF5

</td>

<td style="text-align:center;">

121.1423

</td>

<td style="text-align:center;">

121.1661

</td>

<td style="text-align:center;">

120.6818

</td>

<td style="text-align:center;">

120.8422

</td>

<td style="text-align:center;">

68.08107

</td>

<td style="text-align:center;">

114.0470

</td>

<td style="text-align:center;">

122.5339

</td>

<td style="text-align:center;">

113.2199

</td>

<td style="text-align:center;">

122.6380

</td>

<td style="text-align:center;">

111.9498

</td>

<td style="text-align:center;">

121.7451

</td>

<td style="text-align:center;">

122.2910

</td>

<td style="text-align:center;">

120.8953

</td>

<td style="text-align:center;">

120.738

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PRS

</td>

<td style="text-align:center;">

120.9655

</td>

<td style="text-align:center;">

121.0273

</td>

<td style="text-align:center;">

120.6923

</td>

<td style="text-align:center;">

120.9091

</td>

<td style="text-align:center;">

70.06878

</td>

<td style="text-align:center;">

114.3946

</td>

<td style="text-align:center;">

125.9188

</td>

<td style="text-align:center;">

113.6452

</td>

<td style="text-align:center;">

125.5487

</td>

<td style="text-align:center;">

112.5325

</td>

<td style="text-align:center;">

123.6739

</td>

<td style="text-align:center;">

122.2386

</td>

<td style="text-align:center;">

120.8257

</td>

<td style="text-align:center;">

120.738

</td>

</tr>

</tbody>

</table>

Based on the Sum Squared Error, the Fama Macbeth Method has the lowest
error explaining the Portfolio Risk Premium (This is because the FM
second step regression applied the least square method). The STL
decomposition with no robust weight works better than the one with
robust weight; the FM\_STL lambda works slightly better than the
Arithmetic Mean and the Geometric Mean.

Here we would compare the Estimated ECC from FM method and Filtered FM
method:

![](ECC_files/figure-gfm/Compare_Plots-1.png)<!-- -->![](ECC_files/figure-gfm/Compare_Plots-2.png)<!-- -->![](ECC_files/figure-gfm/Compare_Plots-3.png)<!-- -->

We also performed a KS test to test the FM ECC and STL FM ECC for
different sectors. It seems that the distributions are different from FM
ECC and STL FM ECC.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

KS Test for Fama Mecbeth ECC and STL FM ECC

</caption>

<thead>

<tr>

<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

FF5

</div>

</th>

<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

PRS

</div>

</th>

</tr>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

statistic

</th>

<th style="text-align:center;">

p.value

</th>

<th style="text-align:center;">

statistic

</th>

<th style="text-align:center;">

p.value

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;font-weight: bold;">

Aero

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Agric

</td>

<td style="text-align:center;">

0.2947559

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Autos

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2748644

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Banks

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Beer

</td>

<td style="text-align:center;">

0.3236890

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3074141

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BldMt

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2694394

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Books

</td>

<td style="text-align:center;">

0.3037975

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2730561

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Boxes

</td>

<td style="text-align:center;">

0.3037975

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2929476

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

BusSv

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2694394

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chems

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Chips

</td>

<td style="text-align:center;">

0.2983725

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2784810

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Clths

</td>

<td style="text-align:center;">

0.3128391

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2947559

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Cnstr

</td>

<td style="text-align:center;">

0.3164557

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3001808

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Coal

</td>

<td style="text-align:center;">

0.2676311

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2441230

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Drugs

</td>

<td style="text-align:center;">

0.3164557

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3164557

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

ElcEq

</td>

<td style="text-align:center;">

0.2929476

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2875226

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

FabPr

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3146474

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fin

</td>

<td style="text-align:center;">

0.2947559

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2694394

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Food

</td>

<td style="text-align:center;">

0.2929476

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2893309

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Fun

</td>

<td style="text-align:center;">

0.2893309

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2893309

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Gold

</td>

<td style="text-align:center;">

0.2694394

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2585895

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Guns

</td>

<td style="text-align:center;">

0.2730561

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3001808

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hardw

</td>

<td style="text-align:center;">

0.2983725

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2857143

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hlth

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3074141

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Hshld

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Insur

</td>

<td style="text-align:center;">

0.2875226

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2730561

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

LabEq

</td>

<td style="text-align:center;">

0.3146474

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2784810

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mach

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Meals

</td>

<td style="text-align:center;">

0.3327306

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3019892

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

MedEq

</td>

<td style="text-align:center;">

0.3128391

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Mines

</td>

<td style="text-align:center;">

0.2802893

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2983725

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Oil

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Other

</td>

<td style="text-align:center;">

0.2875226

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2965642

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Paper

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

PerSv

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2730561

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

RlEst

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2694394

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rtail

</td>

<td style="text-align:center;">

0.3254973

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.3056058

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Rubbr

</td>

<td style="text-align:center;">

0.3182640

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2784810

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Ships

</td>

<td style="text-align:center;">

0.2947559

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2802893

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Smoke

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2875226

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Soda

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2911392

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Softw

</td>

<td style="text-align:center;">

0.2766727

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2513562

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Steel

</td>

<td style="text-align:center;">

0.2965642

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2983725

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Telcm

</td>

<td style="text-align:center;">

0.2893309

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2947559

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Toys

</td>

<td style="text-align:center;">

0.3092224

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2820976

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Trans

</td>

<td style="text-align:center;">

0.3001808

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2766727

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Txtls

</td>

<td style="text-align:center;">

0.2839060

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2766727

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Util

</td>

<td style="text-align:center;">

0.3019892

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2730561

</td>

<td style="text-align:center;">

0

</td>

</tr>

<tr>

<td style="text-align:center;font-weight: bold;">

Whlsl

</td>

<td style="text-align:center;">

0.3019892

</td>

<td style="text-align:center;">

0

</td>

<td style="text-align:center;">

0.2857143

</td>

<td style="text-align:center;">

0

</td>

</tr>

</tbody>

</table>

Next, we plot the plots for FM vs. STL Filtered FM statistics.

![](External_plots/RP_mean.png) ![](External_plots/RP_median.png)
![](External_plots/RP_std.png) ![](External_plots/RP_skew.png)
![](External_plots/RP_kurt.png)

## S5-3 Bootstrap Standard Error

In this section, we would apply the bootstrap method to estimated the
standard error of estimated ECC’s with different methods.

First, we estimate the average ECC across 48 Sectors (without Other)
statistics from simulation; simulate 1000 samples of 250 average ECCs
with replacement; and calculate the mean from each sample; then the
standard error is the standard deviation of sample mean.

Second, we simulated 1000 samples of 250 average ECCs with replacement
for each Industry; calculate the mean from each sample; then the
standard error for each Industry ECC is the standard deviation of sample
mean.

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Bootstrap Estimated ECC Standard Error

</caption>

<thead>

<tr>

<th style="text-align:center;">

AM

</th>

<th style="text-align:center;">

GM

</th>

<th style="text-align:center;">

RAM

</th>

<th style="text-align:center;">

RGM

</th>

<th style="text-align:center;">

FM

</th>

<th style="text-align:center;">

FM\_STL\_7\_N

</th>

<th style="text-align:center;">

FM\_STL\_7\_R

</th>

<th style="text-align:center;">

FM\_STL\_15\_N

</th>

<th style="text-align:center;">

FM\_STL\_15\_R

</th>

<th style="text-align:center;">

FM\_STL\_40\_N

</th>

<th style="text-align:center;">

FM\_STL\_40\_R

</th>

<th style="text-align:center;">

RP

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

5.25e-05

</td>

<td style="text-align:center;">

4.57e-05

</td>

<td style="text-align:center;">

0.0003272

</td>

<td style="text-align:center;">

0.0003409

</td>

<td style="text-align:center;">

0.0038211

</td>

<td style="text-align:center;">

0.0008115

</td>

<td style="text-align:center;">

0.0009876

</td>

<td style="text-align:center;">

0.0008553

</td>

<td style="text-align:center;">

0.0010556

</td>

<td style="text-align:center;">

0.0009168

</td>

<td style="text-align:center;">

0.0011204

</td>

<td style="text-align:center;">

0.0030506

</td>

</tr>

</tbody>

</table>

<table class="table table-striped" style="font-size: 10px; width: auto !important; margin-left: auto; margin-right: auto;">

<caption style="font-size: initial !important;">

Bootstrap Estimated Industry ECC Standard Error

</caption>

<thead>

<tr>

<th style="text-align:center;">

Industry

</th>

<th style="text-align:center;">

AM

</th>

<th style="text-align:center;">

GM

</th>

<th style="text-align:center;">

RAM

</th>

<th style="text-align:center;">

RGM

</th>

<th style="text-align:center;">

FM

</th>

<th style="text-align:center;">

FM\_STL\_7\_N

</th>

<th style="text-align:center;">

FM\_STL\_7\_R

</th>

<th style="text-align:center;">

FM\_STL\_15\_N

</th>

<th style="text-align:center;">

FM\_STL\_15\_R

</th>

<th style="text-align:center;">

FM\_STL\_40\_N

</th>

<th style="text-align:center;">

FM\_STL\_40\_R

</th>

<th style="text-align:center;">

RP

</th>

</tr>

</thead>

<tbody>

<tr>

<td style="text-align:center;">

Aero

</td>

<td style="text-align:center;">

0.0001584

</td>

<td style="text-align:center;">

0.0001368

</td>

<td style="text-align:center;">

0.0004144

</td>

<td style="text-align:center;">

0.0004147

</td>

<td style="text-align:center;">

0.0045832

</td>

<td style="text-align:center;">

0.0009917

</td>

<td style="text-align:center;">

0.0011807

</td>

<td style="text-align:center;">

0.0010409

</td>

<td style="text-align:center;">

0.0012696

</td>

<td style="text-align:center;">

0.0011083

</td>

<td style="text-align:center;">

0.0012489

</td>

<td style="text-align:center;">

0.0042458

</td>

</tr>

<tr>

<td style="text-align:center;">

Agric

</td>

<td style="text-align:center;">

0.0002068

</td>

<td style="text-align:center;">

0.0001780

</td>

<td style="text-align:center;">

0.0004868

</td>

<td style="text-align:center;">

0.0004809

</td>

<td style="text-align:center;">

0.0036828

</td>

<td style="text-align:center;">

0.0007931

</td>

<td style="text-align:center;">

0.0009749

</td>

<td style="text-align:center;">

0.0008349

</td>

<td style="text-align:center;">

0.0010621

</td>

<td style="text-align:center;">

0.0008989

</td>

<td style="text-align:center;">

0.0010892

</td>

<td style="text-align:center;">

0.0041157

</td>

</tr>

<tr>

<td style="text-align:center;">

Autos

</td>

<td style="text-align:center;">

0.0002127

</td>

<td style="text-align:center;">

0.0001856

</td>

<td style="text-align:center;">

0.0003623

</td>

<td style="text-align:center;">

0.0003740

</td>

<td style="text-align:center;">

0.0047951

</td>

<td style="text-align:center;">

0.0011508

</td>

<td style="text-align:center;">

0.0011103

</td>

<td style="text-align:center;">

0.0012026

</td>

<td style="text-align:center;">

0.0012312

</td>

<td style="text-align:center;">

0.0012813

</td>

<td style="text-align:center;">

0.0013669

</td>

<td style="text-align:center;">

0.0044525

</td>

</tr>

<tr>

<td style="text-align:center;">

Banks

</td>

<td style="text-align:center;">

0.0001536

</td>

<td style="text-align:center;">

0.0001318

</td>

<td style="text-align:center;">

0.0005544

</td>

<td style="text-align:center;">

0.0005603

</td>

<td style="text-align:center;">

0.0046824

</td>

<td style="text-align:center;">

0.0009245

</td>

<td style="text-align:center;">

0.0011730

</td>

<td style="text-align:center;">

0.0009671

</td>

<td style="text-align:center;">

0.0012490

</td>

<td style="text-align:center;">

0.0010350

</td>

<td style="text-align:center;">

0.0012260

</td>

<td style="text-align:center;">

0.0039556

</td>

</tr>

<tr>

<td style="text-align:center;">

Beer

</td>

<td style="text-align:center;">

0.0001674

</td>

<td style="text-align:center;">

0.0001450

</td>

<td style="text-align:center;">

0.0004221

</td>

<td style="text-align:center;">

0.0004131

</td>

<td style="text-align:center;">

0.0033473

</td>

<td style="text-align:center;">

0.0006515

</td>

<td style="text-align:center;">

0.0009848

</td>

<td style="text-align:center;">

0.0006794

</td>

<td style="text-align:center;">

0.0009211

</td>

<td style="text-align:center;">

0.0007266

</td>

<td style="text-align:center;">

0.0008985

</td>

<td style="text-align:center;">

0.0033264

</td>

</tr>

<tr>

<td style="text-align:center;">

BldMt

</td>

<td style="text-align:center;">

0.0001603

</td>

<td style="text-align:center;">

0.0001388

</td>

<td style="text-align:center;">

0.0003486

</td>

<td style="text-align:center;">

0.0003564

</td>

<td style="text-align:center;">

0.0046382

</td>

<td style="text-align:center;">

0.0009015

</td>

<td style="text-align:center;">

0.0011660

</td>

<td style="text-align:center;">

0.0009490

</td>

<td style="text-align:center;">

0.0011911

</td>

<td style="text-align:center;">

0.0010142

</td>

<td style="text-align:center;">

0.0012895

</td>

<td style="text-align:center;">

0.0040398

</td>

</tr>

<tr>

<td style="text-align:center;">

Books

</td>

<td style="text-align:center;">

0.0001190

</td>

<td style="text-align:center;">

0.0001026

</td>

<td style="text-align:center;">

0.0003623

</td>

<td style="text-align:center;">

0.0003777

</td>

<td style="text-align:center;">

0.0039078

</td>

<td style="text-align:center;">

0.0008434

</td>

<td style="text-align:center;">

0.0009908

</td>

<td style="text-align:center;">

0.0008915

</td>

<td style="text-align:center;">

0.0010359

</td>

<td style="text-align:center;">

0.0009580

</td>

<td style="text-align:center;">

0.0011198

</td>

<td style="text-align:center;">

0.0035939

</td>

</tr>

<tr>

<td style="text-align:center;">

Boxes

</td>

<td style="text-align:center;">

0.0002107

</td>

<td style="text-align:center;">

0.0001814

</td>

<td style="text-align:center;">

0.0003978

</td>

<td style="text-align:center;">

0.0003948

</td>

<td style="text-align:center;">

0.0037521

</td>

<td style="text-align:center;">

0.0007750

</td>

<td style="text-align:center;">

0.0008334

</td>

<td style="text-align:center;">

0.0008204

</td>

<td style="text-align:center;">

0.0008558

</td>

<td style="text-align:center;">

0.0008837

</td>

<td style="text-align:center;">

0.0008990

</td>

<td style="text-align:center;">

0.0035907

</td>

</tr>

<tr>

<td style="text-align:center;">

BusSv

</td>

<td style="text-align:center;">

0.0000593

</td>

<td style="text-align:center;">

0.0000533

</td>

<td style="text-align:center;">

0.0003936

</td>

<td style="text-align:center;">

0.0004065

</td>

<td style="text-align:center;">

0.0042525

</td>

<td style="text-align:center;">

0.0009120

</td>

<td style="text-align:center;">

0.0010655

</td>

<td style="text-align:center;">

0.0009622

</td>

<td style="text-align:center;">

0.0011336

</td>

<td style="text-align:center;">

0.0010311

</td>

<td style="text-align:center;">

0.0012582

</td>

<td style="text-align:center;">

0.0034894

</td>

</tr>

<tr>

<td style="text-align:center;">

Chems

</td>

<td style="text-align:center;">

0.0001273

</td>

<td style="text-align:center;">

0.0001132

</td>

<td style="text-align:center;">

0.0003055

</td>

<td style="text-align:center;">

0.0003178

</td>

<td style="text-align:center;">

0.0043523

</td>

<td style="text-align:center;">

0.0009068

</td>

<td style="text-align:center;">

0.0011556

</td>

<td style="text-align:center;">

0.0009581

</td>

<td style="text-align:center;">

0.0012193

</td>

<td style="text-align:center;">

0.0010296

</td>

<td style="text-align:center;">

0.0012681

</td>

<td style="text-align:center;">

0.0038913

</td>

</tr>

<tr>

<td style="text-align:center;">

Chips

</td>

<td style="text-align:center;">

0.0001530

</td>

<td style="text-align:center;">

0.0001315

</td>

<td style="text-align:center;">

0.0005662

</td>

<td style="text-align:center;">

0.0005699

</td>

<td style="text-align:center;">

0.0051429

</td>

<td style="text-align:center;">

0.0012138

</td>

<td style="text-align:center;">

0.0014390

</td>

<td style="text-align:center;">

0.0012710

</td>

<td style="text-align:center;">

0.0015425

</td>

<td style="text-align:center;">

0.0013465

</td>

<td style="text-align:center;">

0.0018505

</td>

<td style="text-align:center;">

0.0046930

</td>

</tr>

<tr>

<td style="text-align:center;">

Clths

</td>

<td style="text-align:center;">

0.0001660

</td>

<td style="text-align:center;">

0.0001407

</td>

<td style="text-align:center;">

0.0003047

</td>

<td style="text-align:center;">

0.0003261

</td>

<td style="text-align:center;">

0.0042421

</td>

<td style="text-align:center;">

0.0008270

</td>

<td style="text-align:center;">

0.0009541

</td>

<td style="text-align:center;">

0.0008769

</td>

<td style="text-align:center;">

0.0009750

</td>

<td style="text-align:center;">

0.0009477

</td>

<td style="text-align:center;">

0.0010649

</td>

<td style="text-align:center;">

0.0039804

</td>

</tr>

<tr>

<td style="text-align:center;">

Cnstr

</td>

<td style="text-align:center;">

0.0002019

</td>

<td style="text-align:center;">

0.0001731

</td>

<td style="text-align:center;">

0.0004860

</td>

<td style="text-align:center;">

0.0004877

</td>

<td style="text-align:center;">

0.0048911

</td>

<td style="text-align:center;">

0.0010602

</td>

<td style="text-align:center;">

0.0012830

</td>

<td style="text-align:center;">

0.0011171

</td>

<td style="text-align:center;">

0.0013958

</td>

<td style="text-align:center;">

0.0012070

</td>

<td style="text-align:center;">

0.0014702

</td>

<td style="text-align:center;">

0.0045027

</td>

</tr>

<tr>

<td style="text-align:center;">

Coal

</td>

<td style="text-align:center;">

0.0003020

</td>

<td style="text-align:center;">

0.0002687

</td>

<td style="text-align:center;">

0.0005115

</td>

<td style="text-align:center;">

0.0005102

</td>

<td style="text-align:center;">

0.0059714

</td>

<td style="text-align:center;">

0.0013972

</td>

<td style="text-align:center;">

0.0014475

</td>

<td style="text-align:center;">

0.0014509

</td>

<td style="text-align:center;">

0.0015857

</td>

<td style="text-align:center;">

0.0015401

</td>

<td style="text-align:center;">

0.0016936

</td>

<td style="text-align:center;">

0.0069547

</td>

</tr>

<tr>

<td style="text-align:center;">

Drugs

</td>

<td style="text-align:center;">

0.0000982

</td>

<td style="text-align:center;">

0.0000874

</td>

<td style="text-align:center;">

0.0004109

</td>

<td style="text-align:center;">

0.0004107

</td>

<td style="text-align:center;">

0.0035921

</td>

<td style="text-align:center;">

0.0007333

</td>

<td style="text-align:center;">

0.0008624

</td>

<td style="text-align:center;">

0.0007683

</td>

<td style="text-align:center;">

0.0008768

</td>

<td style="text-align:center;">

0.0008199

</td>

<td style="text-align:center;">

0.0009169

</td>

<td style="text-align:center;">

0.0032738

</td>

</tr>

<tr>

<td style="text-align:center;">

ElcEq

</td>

<td style="text-align:center;">

0.0001818

</td>

<td style="text-align:center;">

0.0001583

</td>

<td style="text-align:center;">

0.0004926

</td>

<td style="text-align:center;">

0.0004990

</td>

<td style="text-align:center;">

0.0047915

</td>

<td style="text-align:center;">

0.0010129

</td>

<td style="text-align:center;">

0.0012305

</td>

<td style="text-align:center;">

0.0010644

</td>

<td style="text-align:center;">

0.0012958

</td>

<td style="text-align:center;">

0.0011379

</td>

<td style="text-align:center;">

0.0014622

</td>

<td style="text-align:center;">

0.0040325

</td>

</tr>

<tr>

<td style="text-align:center;">

FabPr

</td>

<td style="text-align:center;">

0.0002428

</td>

<td style="text-align:center;">

0.0002100

</td>

<td style="text-align:center;">

0.0003993

</td>

<td style="text-align:center;">

0.0003925

</td>

<td style="text-align:center;">

0.0045842

</td>

<td style="text-align:center;">

0.0009752

</td>

<td style="text-align:center;">

0.0011600

</td>

<td style="text-align:center;">

0.0010271

</td>

<td style="text-align:center;">

0.0012428

</td>

<td style="text-align:center;">

0.0011085

</td>

<td style="text-align:center;">

0.0013489

</td>

<td style="text-align:center;">

0.0044812

</td>

</tr>

<tr>

<td style="text-align:center;">

Fin

</td>

<td style="text-align:center;">

0.0001187

</td>

<td style="text-align:center;">

0.0001025

</td>

<td style="text-align:center;">

0.0004950

</td>

<td style="text-align:center;">

0.0005062

</td>

<td style="text-align:center;">

0.0046654

</td>

<td style="text-align:center;">

0.0010105

</td>

<td style="text-align:center;">

0.0010955

</td>

<td style="text-align:center;">

0.0010538

</td>

<td style="text-align:center;">

0.0011828

</td>

<td style="text-align:center;">

0.0011276

</td>

<td style="text-align:center;">

0.0013406

</td>

<td style="text-align:center;">

0.0039428

</td>

</tr>

<tr>

<td style="text-align:center;">

Food

</td>

<td style="text-align:center;">

0.0001632

</td>

<td style="text-align:center;">

0.0001463

</td>

<td style="text-align:center;">

0.0003837

</td>

<td style="text-align:center;">

0.0003779

</td>

<td style="text-align:center;">

0.0030312

</td>

<td style="text-align:center;">

0.0006786

</td>

<td style="text-align:center;">

0.0007859

</td>

<td style="text-align:center;">

0.0007049

</td>

<td style="text-align:center;">

0.0007880

</td>

<td style="text-align:center;">

0.0007474

</td>

<td style="text-align:center;">

0.0008119

</td>

<td style="text-align:center;">

0.0028799

</td>

</tr>

<tr>

<td style="text-align:center;">

Fun

</td>

<td style="text-align:center;">

0.0001841

</td>

<td style="text-align:center;">

0.0001588

</td>

<td style="text-align:center;">

0.0004539

</td>

<td style="text-align:center;">

0.0004817

</td>

<td style="text-align:center;">

0.0051544

</td>

<td style="text-align:center;">

0.0011173

</td>

<td style="text-align:center;">

0.0011696

</td>

<td style="text-align:center;">

0.0011770

</td>

<td style="text-align:center;">

0.0012967

</td>

<td style="text-align:center;">

0.0012584

</td>

<td style="text-align:center;">

0.0014052

</td>

<td style="text-align:center;">

0.0047852

</td>

</tr>

<tr>

<td style="text-align:center;">

Gold

</td>

<td style="text-align:center;">

0.0003343

</td>

<td style="text-align:center;">

0.0003025

</td>

<td style="text-align:center;">

0.0004871

</td>

<td style="text-align:center;">

0.0004718

</td>

<td style="text-align:center;">

0.0050488

</td>

<td style="text-align:center;">

0.0011574

</td>

<td style="text-align:center;">

0.0012295

</td>

<td style="text-align:center;">

0.0012119

</td>

<td style="text-align:center;">

0.0013364

</td>

<td style="text-align:center;">

0.0012845

</td>

<td style="text-align:center;">

0.0014837

</td>

<td style="text-align:center;">

0.0071254

</td>

</tr>

<tr>

<td style="text-align:center;">

Guns

</td>

<td style="text-align:center;">

0.0001903

</td>

<td style="text-align:center;">

0.0001655

</td>

<td style="text-align:center;">

0.0003364

</td>

<td style="text-align:center;">

0.0003283

</td>

<td style="text-align:center;">

0.0037697

</td>

<td style="text-align:center;">

0.0008304

</td>

<td style="text-align:center;">

0.0010566

</td>

<td style="text-align:center;">

0.0008662

</td>

<td style="text-align:center;">

0.0011286

</td>

<td style="text-align:center;">

0.0009177

</td>

<td style="text-align:center;">

0.0011544

</td>

<td style="text-align:center;">

0.0041205

</td>

</tr>

<tr>

<td style="text-align:center;">

Hardw

</td>

<td style="text-align:center;">

0.0002035

</td>

<td style="text-align:center;">

0.0001798

</td>

<td style="text-align:center;">

0.0004727

</td>

<td style="text-align:center;">

0.0004700

</td>

<td style="text-align:center;">

0.0047868

</td>

<td style="text-align:center;">

0.0011814

</td>

<td style="text-align:center;">

0.0014452

</td>

<td style="text-align:center;">

0.0012244

</td>

<td style="text-align:center;">

0.0015359

</td>

<td style="text-align:center;">

0.0012862

</td>

<td style="text-align:center;">

0.0018024

</td>

<td style="text-align:center;">

0.0047711

</td>

</tr>

<tr>

<td style="text-align:center;">

Hlth

</td>

<td style="text-align:center;">

0.0002788

</td>

<td style="text-align:center;">

0.0002448

</td>

<td style="text-align:center;">

0.0006298

</td>

<td style="text-align:center;">

0.0006036

</td>

<td style="text-align:center;">

0.0047348

</td>

<td style="text-align:center;">

0.0010285

</td>

<td style="text-align:center;">

0.0012674

</td>

<td style="text-align:center;">

0.0010811

</td>

<td style="text-align:center;">

0.0013559

</td>

<td style="text-align:center;">

0.0011591

</td>

<td style="text-align:center;">

0.0012934

</td>

<td style="text-align:center;">

0.0046224

</td>

</tr>

<tr>

<td style="text-align:center;">

Hshld

</td>

<td style="text-align:center;">

0.0001279

</td>

<td style="text-align:center;">

0.0001098

</td>

<td style="text-align:center;">

0.0003738

</td>

<td style="text-align:center;">

0.0003785

</td>

<td style="text-align:center;">

0.0034634

</td>

<td style="text-align:center;">

0.0006736

</td>

<td style="text-align:center;">

0.0008772

</td>

<td style="text-align:center;">

0.0007027

</td>

<td style="text-align:center;">

0.0008786

</td>

<td style="text-align:center;">

0.0007495

</td>

<td style="text-align:center;">

0.0009078

</td>

<td style="text-align:center;">

0.0029608

</td>

</tr>

<tr>

<td style="text-align:center;">

Insur

</td>

<td style="text-align:center;">

0.0001801

</td>

<td style="text-align:center;">

0.0001607

</td>

<td style="text-align:center;">

0.0004260

</td>

<td style="text-align:center;">

0.0004274

</td>

<td style="text-align:center;">

0.0040661

</td>

<td style="text-align:center;">

0.0007903

</td>

<td style="text-align:center;">

0.0010065

</td>

<td style="text-align:center;">

0.0008342

</td>

<td style="text-align:center;">

0.0011036

</td>

<td style="text-align:center;">

0.0009055

</td>

<td style="text-align:center;">

0.0010727

</td>

<td style="text-align:center;">

0.0034270

</td>

</tr>

<tr>

<td style="text-align:center;">

LabEq

</td>

<td style="text-align:center;">

0.0001803

</td>

<td style="text-align:center;">

0.0001562

</td>

<td style="text-align:center;">

0.0005065

</td>

<td style="text-align:center;">

0.0005116

</td>

<td style="text-align:center;">

0.0048147

</td>

<td style="text-align:center;">

0.0010174

</td>

<td style="text-align:center;">

0.0011800

</td>

<td style="text-align:center;">

0.0010703

</td>

<td style="text-align:center;">

0.0012817

</td>

<td style="text-align:center;">

0.0011393

</td>

<td style="text-align:center;">

0.0014424

</td>

<td style="text-align:center;">

0.0044467

</td>

</tr>

<tr>

<td style="text-align:center;">

Mach

</td>

<td style="text-align:center;">

0.0001688

</td>

<td style="text-align:center;">

0.0001441

</td>

<td style="text-align:center;">

0.0004165

</td>

<td style="text-align:center;">

0.0004227

</td>

<td style="text-align:center;">

0.0049308

</td>

<td style="text-align:center;">

0.0009243

</td>

<td style="text-align:center;">

0.0011315

</td>

<td style="text-align:center;">

0.0009867

</td>

<td style="text-align:center;">

0.0012390

</td>

<td style="text-align:center;">

0.0010790

</td>

<td style="text-align:center;">

0.0013487

</td>

<td style="text-align:center;">

0.0042228

</td>

</tr>

<tr>

<td style="text-align:center;">

Meals

</td>

<td style="text-align:center;">

0.0001552

</td>

<td style="text-align:center;">

0.0001314

</td>

<td style="text-align:center;">

0.0003983

</td>

<td style="text-align:center;">

0.0004101

</td>

<td style="text-align:center;">

0.0039387

</td>

<td style="text-align:center;">

0.0007819

</td>

<td style="text-align:center;">

0.0010218

</td>

<td style="text-align:center;">

0.0008234

</td>

<td style="text-align:center;">

0.0010677

</td>

<td style="text-align:center;">

0.0008942

</td>

<td style="text-align:center;">

0.0010635

</td>

<td style="text-align:center;">

0.0035498

</td>

</tr>

<tr>

<td style="text-align:center;">

MedEq

</td>

<td style="text-align:center;">

0.0001309

</td>

<td style="text-align:center;">

0.0001179

</td>

<td style="text-align:center;">

0.0003897

</td>

<td style="text-align:center;">

0.0003904

</td>

<td style="text-align:center;">

0.0036980

</td>

<td style="text-align:center;">

0.0007583

</td>

<td style="text-align:center;">

0.0009166

</td>

<td style="text-align:center;">

0.0007990

</td>

<td style="text-align:center;">

0.0009582

</td>

<td style="text-align:center;">

0.0008526

</td>

<td style="text-align:center;">

0.0009907

</td>

<td style="text-align:center;">

0.0033273

</td>

</tr>

<tr>

<td style="text-align:center;">

Mines

</td>

<td style="text-align:center;">

0.0002300

</td>

<td style="text-align:center;">

0.0002032

</td>

<td style="text-align:center;">

0.0004895

</td>

<td style="text-align:center;">

0.0004879

</td>

<td style="text-align:center;">

0.0049870

</td>

<td style="text-align:center;">

0.0011971

</td>

<td style="text-align:center;">

0.0013691

</td>

<td style="text-align:center;">

0.0012637

</td>

<td style="text-align:center;">

0.0014830

</td>

<td style="text-align:center;">

0.0013573

</td>

<td style="text-align:center;">

0.0015869

</td>

<td style="text-align:center;">

0.0049717

</td>

</tr>

<tr>

<td style="text-align:center;">

Oil

</td>

<td style="text-align:center;">

0.0001838

</td>

<td style="text-align:center;">

0.0001608

</td>

<td style="text-align:center;">

0.0004077

</td>

<td style="text-align:center;">

0.0004012

</td>

<td style="text-align:center;">

0.0036670

</td>

<td style="text-align:center;">

0.0008488

</td>

<td style="text-align:center;">

0.0011824

</td>

<td style="text-align:center;">

0.0008885

</td>

<td style="text-align:center;">

0.0012309

</td>

<td style="text-align:center;">

0.0009476

</td>

<td style="text-align:center;">

0.0012554

</td>

<td style="text-align:center;">

0.0037882

</td>

</tr>

<tr>

<td style="text-align:center;">

Paper

</td>

<td style="text-align:center;">

0.0001519

</td>

<td style="text-align:center;">

0.0001338

</td>

<td style="text-align:center;">

0.0003441

</td>

<td style="text-align:center;">

0.0003407

</td>

<td style="text-align:center;">

0.0039022

</td>

<td style="text-align:center;">

0.0008508

</td>

<td style="text-align:center;">

0.0010359

</td>

<td style="text-align:center;">

0.0008942

</td>

<td style="text-align:center;">

0.0010656

</td>

<td style="text-align:center;">

0.0009567

</td>

<td style="text-align:center;">

0.0010963

</td>

<td style="text-align:center;">

0.0034934

</td>

</tr>

<tr>

<td style="text-align:center;">

PerSv

</td>

<td style="text-align:center;">

0.0001797

</td>

<td style="text-align:center;">

0.0001542

</td>

<td style="text-align:center;">

0.0004724

</td>

<td style="text-align:center;">

0.0004680

</td>

<td style="text-align:center;">

0.0040981

</td>

<td style="text-align:center;">

0.0008692

</td>

<td style="text-align:center;">

0.0010403

</td>

<td style="text-align:center;">

0.0009155

</td>

<td style="text-align:center;">

0.0010957

</td>

<td style="text-align:center;">

0.0009841

</td>

<td style="text-align:center;">

0.0011288

</td>

<td style="text-align:center;">

0.0039313

</td>

</tr>

<tr>

<td style="text-align:center;">

RlEst

</td>

<td style="text-align:center;">

0.0001884

</td>

<td style="text-align:center;">

0.0001599

</td>

<td style="text-align:center;">

0.0004342

</td>

<td style="text-align:center;">

0.0004507

</td>

<td style="text-align:center;">

0.0052713

</td>

<td style="text-align:center;">

0.0012062

</td>

<td style="text-align:center;">

0.0014243

</td>

<td style="text-align:center;">

0.0012653

</td>

<td style="text-align:center;">

0.0014701

</td>

<td style="text-align:center;">

0.0013516

</td>

<td style="text-align:center;">

0.0015905

</td>

<td style="text-align:center;">

0.0048584

</td>

</tr>

<tr>

<td style="text-align:center;">

Rtail

</td>

<td style="text-align:center;">

0.0001058

</td>

<td style="text-align:center;">

0.0000923

</td>

<td style="text-align:center;">

0.0003246

</td>

<td style="text-align:center;">

0.0003463

</td>

<td style="text-align:center;">

0.0037912

</td>

<td style="text-align:center;">

0.0007759

</td>

<td style="text-align:center;">

0.0008304

</td>

<td style="text-align:center;">

0.0008125

</td>

<td style="text-align:center;">

0.0008516

</td>

<td style="text-align:center;">

0.0008624

</td>

<td style="text-align:center;">

0.0009733

</td>

<td style="text-align:center;">

0.0035357

</td>

</tr>

<tr>

<td style="text-align:center;">

Rubbr

</td>

<td style="text-align:center;">

0.0001245

</td>

<td style="text-align:center;">

0.0001100

</td>

<td style="text-align:center;">

0.0003672

</td>

<td style="text-align:center;">

0.0003799

</td>

<td style="text-align:center;">

0.0041319

</td>

<td style="text-align:center;">

0.0008241

</td>

<td style="text-align:center;">

0.0009804

</td>

<td style="text-align:center;">

0.0008685

</td>

<td style="text-align:center;">

0.0010193

</td>

<td style="text-align:center;">

0.0009259

</td>

<td style="text-align:center;">

0.0010961

</td>

<td style="text-align:center;">

0.0037432

</td>

</tr>

<tr>

<td style="text-align:center;">

Ships

</td>

<td style="text-align:center;">

0.0002733

</td>

<td style="text-align:center;">

0.0002400

</td>

<td style="text-align:center;">

0.0004757

</td>

<td style="text-align:center;">

0.0004662

</td>

<td style="text-align:center;">

0.0045939

</td>

<td style="text-align:center;">

0.0009038

</td>

<td style="text-align:center;">

0.0012084

</td>

<td style="text-align:center;">

0.0009511

</td>

<td style="text-align:center;">

0.0012953

</td>

<td style="text-align:center;">

0.0010204

</td>

<td style="text-align:center;">

0.0013087

</td>

<td style="text-align:center;">

0.0048598

</td>

</tr>

<tr>

<td style="text-align:center;">

Smoke

</td>

<td style="text-align:center;">

0.0002471

</td>

<td style="text-align:center;">

0.0002188

</td>

<td style="text-align:center;">

0.0004687

</td>

<td style="text-align:center;">

0.0004457

</td>

<td style="text-align:center;">

0.0033104

</td>

<td style="text-align:center;">

0.0008517

</td>

<td style="text-align:center;">

0.0010409

</td>

<td style="text-align:center;">

0.0008769

</td>

<td style="text-align:center;">

0.0010195

</td>

<td style="text-align:center;">

0.0009186

</td>

<td style="text-align:center;">

0.0010544

</td>

<td style="text-align:center;">

0.0038224

</td>

</tr>

<tr>

<td style="text-align:center;">

Soda

</td>

<td style="text-align:center;">

0.0002252

</td>

<td style="text-align:center;">

0.0001936

</td>

<td style="text-align:center;">

0.0005185

</td>

<td style="text-align:center;">

0.0005043

</td>

<td style="text-align:center;">

0.0040478

</td>

<td style="text-align:center;">

0.0007807

</td>

<td style="text-align:center;">

0.0010911

</td>

<td style="text-align:center;">

0.0008269

</td>

<td style="text-align:center;">

0.0010734

</td>

<td style="text-align:center;">

0.0008971

</td>

<td style="text-align:center;">

0.0009381

</td>

<td style="text-align:center;">

0.0041634

</td>

</tr>

<tr>

<td style="text-align:center;">

Softw

</td>

<td style="text-align:center;">

0.0003608

</td>

<td style="text-align:center;">

0.0003143

</td>

<td style="text-align:center;">

0.0008863

</td>

<td style="text-align:center;">

0.0008670

</td>

<td style="text-align:center;">

0.0061314

</td>

<td style="text-align:center;">

0.0014685

</td>

<td style="text-align:center;">

0.0019262

</td>

<td style="text-align:center;">

0.0015227

</td>

<td style="text-align:center;">

0.0020502

</td>

<td style="text-align:center;">

0.0016041

</td>

<td style="text-align:center;">

0.0022655

</td>

<td style="text-align:center;">

0.0057091

</td>

</tr>

<tr>

<td style="text-align:center;">

Steel

</td>

<td style="text-align:center;">

0.0002063

</td>

<td style="text-align:center;">

0.0001788

</td>

<td style="text-align:center;">

0.0004330

</td>

<td style="text-align:center;">

0.0004438

</td>

<td style="text-align:center;">

0.0054230

</td>

<td style="text-align:center;">

0.0011833

</td>

<td style="text-align:center;">

0.0012761

</td>

<td style="text-align:center;">

0.0012451

</td>

<td style="text-align:center;">

0.0013467

</td>

<td style="text-align:center;">

0.0013284

</td>

<td style="text-align:center;">

0.0015372

</td>

<td style="text-align:center;">

0.0048519

</td>

</tr>

<tr>

<td style="text-align:center;">

Telcm

</td>

<td style="text-align:center;">

0.0001357

</td>

<td style="text-align:center;">

0.0001198

</td>

<td style="text-align:center;">

0.0004089

</td>

<td style="text-align:center;">

0.0004019

</td>

<td style="text-align:center;">

0.0033856

</td>

<td style="text-align:center;">

0.0007413

</td>

<td style="text-align:center;">

0.0008422

</td>

<td style="text-align:center;">

0.0007712

</td>

<td style="text-align:center;">

0.0008403

</td>

<td style="text-align:center;">

0.0008158

</td>

<td style="text-align:center;">

0.0009701

</td>

<td style="text-align:center;">

0.0030401

</td>

</tr>

<tr>

<td style="text-align:center;">

Toys

</td>

<td style="text-align:center;">

0.0002237

</td>

<td style="text-align:center;">

0.0001951

</td>

<td style="text-align:center;">

0.0004063

</td>

<td style="text-align:center;">

0.0004103

</td>

<td style="text-align:center;">

0.0046504

</td>

<td style="text-align:center;">

0.0009849

</td>

<td style="text-align:center;">

0.0011553

</td>

<td style="text-align:center;">

0.0010348

</td>

<td style="text-align:center;">

0.0011953

</td>

<td style="text-align:center;">

0.0011003

</td>

<td style="text-align:center;">

0.0012604

</td>

<td style="text-align:center;">

0.0043925

</td>

</tr>

<tr>

<td style="text-align:center;">

Trans

</td>

<td style="text-align:center;">

0.0001295

</td>

<td style="text-align:center;">

0.0001158

</td>

<td style="text-align:center;">

0.0003229

</td>

<td style="text-align:center;">

0.0003320

</td>

<td style="text-align:center;">

0.0040644

</td>

<td style="text-align:center;">

0.0008029

</td>

<td style="text-align:center;">

0.0010300

</td>

<td style="text-align:center;">

0.0008418

</td>

<td style="text-align:center;">

0.0010653

</td>

<td style="text-align:center;">

0.0008929

</td>

<td style="text-align:center;">

0.0010894

</td>

<td style="text-align:center;">

0.0034197

</td>

</tr>

<tr>

<td style="text-align:center;">

Txtls

</td>

<td style="text-align:center;">

0.0002215

</td>

<td style="text-align:center;">

0.0001855

</td>

<td style="text-align:center;">

0.0003394

</td>

<td style="text-align:center;">

0.0003536

</td>

<td style="text-align:center;">

0.0047407

</td>

<td style="text-align:center;">

0.0010239

</td>

<td style="text-align:center;">

0.0012050

</td>

<td style="text-align:center;">

0.0010771

</td>

<td style="text-align:center;">

0.0012229

</td>

<td style="text-align:center;">

0.0011515

</td>

<td style="text-align:center;">

0.0013547

</td>

<td style="text-align:center;">

0.0047777

</td>

</tr>

<tr>

<td style="text-align:center;">

Util

</td>

<td style="text-align:center;">

0.0001408

</td>

<td style="text-align:center;">

0.0001281

</td>

<td style="text-align:center;">

0.0002368

</td>

<td style="text-align:center;">

0.0002337

</td>

<td style="text-align:center;">

0.0025746

</td>

<td style="text-align:center;">

0.0006354

</td>

<td style="text-align:center;">

0.0007636

</td>

<td style="text-align:center;">

0.0006633

</td>

<td style="text-align:center;">

0.0008100

</td>

<td style="text-align:center;">

0.0007109

</td>

<td style="text-align:center;">

0.0008185

</td>

<td style="text-align:center;">

0.0026138

</td>

</tr>

<tr>

<td style="text-align:center;">

Whlsl

</td>

<td style="text-align:center;">

0.0000836

</td>

<td style="text-align:center;">

0.0000741

</td>

<td style="text-align:center;">

0.0003453

</td>

<td style="text-align:center;">

0.0003549

</td>

<td style="text-align:center;">

0.0038369

</td>

<td style="text-align:center;">

0.0008330

</td>

<td style="text-align:center;">

0.0010031

</td>

<td style="text-align:center;">

0.0008726

</td>

<td style="text-align:center;">

0.0010812

</td>

<td style="text-align:center;">

0.0009280

</td>

<td style="text-align:center;">

0.0011221

</td>

<td style="text-align:center;">

0.0031538

</td>

</tr>

</tbody>

</table>

## S5-4 Decomposition of the Equity Cost of Captial

In this section, we would try to decompose the ECC.

Based on the Model, at each period t, the estimated Risk Premium is
calculated as follows:

  
![E\[RP\] =
\\vec\\beta\*\\vec\\lambda'](https://latex.codecogs.com/png.latex?E%5BRP%5D%20%3D%20%5Cvec%5Cbeta%2A%5Cvec%5Clambda%27
"E[RP] = \\vec\\beta*\\vec\\lambda'")  

![\\vec\\beta](https://latex.codecogs.com/png.latex?%5Cvec%5Cbeta
"\\vec\\beta") is the 1xk vecotr which represents k factor exposures;
![\\vec\\lambda](https://latex.codecogs.com/png.latex?%5Cvec%5Clambda
"\\vec\\lambda") is the 1xk Matrix which represents k factor premium
across T periods. In order to decompose the
![E\[RP\]](https://latex.codecogs.com/png.latex?E%5BRP%5D "E[RP]") into
one ![\\beta](https://latex.codecogs.com/png.latex?%5Cbeta "\\beta") and
one ![\\lambda](https://latex.codecogs.com/png.latex?%5Clambda
"\\lambda") components, we apply the property of vector product:

  
![E\[RP\] =
|\\vec\\beta|\*|\\vec\\lambda|\*cos(\\vec\\beta,\\vec\\lambda)](https://latex.codecogs.com/png.latex?E%5BRP%5D%20%3D%20%7C%5Cvec%5Cbeta%7C%2A%7C%5Cvec%5Clambda%7C%2Acos%28%5Cvec%5Cbeta%2C%5Cvec%5Clambda%29
"E[RP] = |\\vec\\beta|*|\\vec\\lambda|*cos(\\vec\\beta,\\vec\\lambda)")  

We would call the
![cos(\\vec\\beta,\\vec\\lambda)](https://latex.codecogs.com/png.latex?cos%28%5Cvec%5Cbeta%2C%5Cvec%5Clambda%29
"cos(\\vec\\beta,\\vec\\lambda)") part projection parameter (![-1 \\leq
PP
\\leq 1](https://latex.codecogs.com/png.latex?-1%20%5Cleq%20PP%20%5Cleq%201
"-1 \\leq PP \\leq 1")), since it is how effective the L2 norms,
![|\\vec\\beta|](https://latex.codecogs.com/png.latex?%7C%5Cvec%5Cbeta%7C
"|\\vec\\beta|") and
![|\\vec\\lambda|](https://latex.codecogs.com/png.latex?%7C%5Cvec%5Clambda%7C
"|\\vec\\lambda|"), work together to form the expected risk premium. If
![cos(\\vec\\beta,\\vec\\lambda)=0](https://latex.codecogs.com/png.latex?cos%28%5Cvec%5Cbeta%2C%5Cvec%5Clambda%29%3D0
"cos(\\vec\\beta,\\vec\\lambda)=0"), no matter how large
![|\\vec\\beta|](https://latex.codecogs.com/png.latex?%7C%5Cvec%5Cbeta%7C
"|\\vec\\beta|") and
![|\\vec\\lambda|](https://latex.codecogs.com/png.latex?%7C%5Cvec%5Clambda%7C
"|\\vec\\lambda|") are, the expected risk premium would be 0.

  
![E\[RP\] =
|\\vec\\beta|\*|\\vec\\lambda|\*PP](https://latex.codecogs.com/png.latex?E%5BRP%5D%20%3D%20%7C%5Cvec%5Cbeta%7C%2A%7C%5Cvec%5Clambda%7C%2APP
"E[RP] = |\\vec\\beta|*|\\vec\\lambda|*PP")  

and, ![|E\[RP\]| =
|\\vec\\beta|\*|\\vec\\lambda|\*|PP|](https://latex.codecogs.com/png.latex?%7CE%5BRP%5D%7C%20%3D%20%7C%5Cvec%5Cbeta%7C%2A%7C%5Cvec%5Clambda%7C%2A%7CPP%7C
"|E[RP]| = |\\vec\\beta|*|\\vec\\lambda|*|PP|")

The decomposition would be more intuitive with an additive form. We take
the log of both sides:

  
![ln(|E\[RP\]|) = ln(|\\vec\\beta|\*|\\vec\\lambda|\*|PP|) =
ln(|\\vec\\beta|) + ln(|\\vec\\lambda|) +
ln(|PP|)](https://latex.codecogs.com/png.latex?ln%28%7CE%5BRP%5D%7C%29%20%3D%20ln%28%7C%5Cvec%5Cbeta%7C%2A%7C%5Cvec%5Clambda%7C%2A%7CPP%7C%29%20%3D%20ln%28%7C%5Cvec%5Cbeta%7C%29%20%2B%20ln%28%7C%5Cvec%5Clambda%7C%29%20%2B%20ln%28%7CPP%7C%29
"ln(|E[RP]|) = ln(|\\vec\\beta|*|\\vec\\lambda|*|PP|) = ln(|\\vec\\beta|) + ln(|\\vec\\lambda|) + ln(|PP|)")  

Therefore,

  
![1 = \\frac{ln(|\\vec\\beta|)}{ln(|E\[RP\]|)} +
\\frac{ln(|\\vec\\lambda|))}{ln(|E\[RP\]|)} +
\\frac{ln(|PP|)}{ln(|E\[RP\]|)}](https://latex.codecogs.com/png.latex?1%20%3D%20%5Cfrac%7Bln%28%7C%5Cvec%5Cbeta%7C%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D%20%2B%20%5Cfrac%7Bln%28%7C%5Cvec%5Clambda%7C%29%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D%20%2B%20%5Cfrac%7Bln%28%7CPP%7C%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D
"1 = \\frac{ln(|\\vec\\beta|)}{ln(|E[RP]|)} + \\frac{ln(|\\vec\\lambda|))}{ln(|E[RP]|)} + \\frac{ln(|PP|)}{ln(|E[RP]|)}")  

The
![\\frac{ln(|\\vec\\beta|)}{ln(|E\[RP\]|)}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bln%28%7C%5Cvec%5Cbeta%7C%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D
"\\frac{ln(|\\vec\\beta|)}{ln(|E[RP]|)}") can be interpreted as
importance of ![\\beta](https://latex.codecogs.com/png.latex?%5Cbeta
"\\beta") in forming the expected risk premium; the
![\\frac{ln(|\\vec\\lambda|)}{ln(|E\[RP\]|)}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bln%28%7C%5Cvec%5Clambda%7C%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D
"\\frac{ln(|\\vec\\lambda|)}{ln(|E[RP]|)}") can be interpreted as
importance of ![\\lambda](https://latex.codecogs.com/png.latex?%5Clambda
"\\lambda") in forming the expected risk premium; the
![\\frac{ln(|PP|)}{ln(|E\[RP\]|)}](https://latex.codecogs.com/png.latex?%5Cfrac%7Bln%28%7CPP%7C%29%7D%7Bln%28%7CE%5BRP%5D%7C%29%7D
"\\frac{ln(|PP|)}{ln(|E[RP]|)}") can be interpreted as importance of
projection parameter (PP) in forming the expected risk premium.

![](ECC_files/figure-gfm/ECC_Decomp-1.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-2.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-3.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-4.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-5.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-6.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-7.png)<!-- -->![](ECC_files/figure-gfm/ECC_Decomp-8.png)<!-- -->

![](ECC_files/figure-gfm/ECC_Decomp2-1.png)<!-- -->

## S5-5 Forcasting???

We can try to apply the previous methods to forecast the ECC and compare
the accuracy. There is a STL method of forecasting so we might be able
to use STL to forcast betas and industry risk premium and perform the
second step regression to obtain the lambda. Then we can calculate the
ECC.

## S5-6 ECC with Consumption Growth???

We might look at whether the filter affects the correlation of ECC with
consumption growth or the volatility of consumption growth. In some
asset pricing models, premia should vary across time in response to
consumption growth, and in some models, the volatility of consumption
growth. Maybe we should preemptively look at whether the filter
increases the correlation with these measures in the aggregate.

The focus of the original Fama-French (JFE, 1997) paper was whether
factor models and existing modeling technology could generate relatively
precise estimates of ECC at the industry level. The answer was a
resounding no. I think we are showing that a different model can change
this answer to yes.

To me, a logical next question is whether the resulting premia move over
the cycle as theory suggests.

## S5-7 Improve AM GM with Markov-switching model???

We might ‘improve’ on the simple AM/GM approach by filtering the data,
and then using a two-state Markov-switching model on these filtered
series to capture changes in factor premia over time in a compact way.
In effect, we are saying that we think the factor premiums are either
high or low, and we are going to estimate the values in these states and
estimate which periods have high vs. low premia.

## S5-8 Levi-Welch Beta???

In this section, we will combine the Levi-Welch Betas with our Filtered
Estimated Lambdas to construct the ECC and compare it with other method
estimated ECC. Welch has published estimated betas for the entire CRSP
universe in his website: <https://www.ivo-welch.info/research/>. The
code is available here: <https://www.ivo-welch.info/research/betas/>.

## S5-9 Filtering Method in Other Second-pass Regression???

What we show is that using asset-pricing models to estimate the equity
cost of capital is compromised by these seasonal factors in the
second-pass regressions. The impact of this finding might actually be
far more widespread. The first stage is about estimating betas, but the
second stage is where we are trying to find whether something is being
priced: this involves the cross-sectional regressions of returns on
betas. This is the spot where what we are showing in the paper may be
particularly important.
