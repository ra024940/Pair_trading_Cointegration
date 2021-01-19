<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/ra024940/Pair_trading_Cointegration/White_noise.svg.png">
    <img src="Eletronic.jpg" alt="Logo" width="440" height="209">
  </a>

  <h3 align="center">Cointegration Trading w/ Machine Learning</h3>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open"> 
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
    </li>
    <li>
      <a href="#definition">Project Definition</a>
    </li>
      <ul>
        <li><a href="#background-and-statistical-concepts">Background and Statistical Concepts</a></li>
        <li><a href="#project-approach-and-definition">Approach and Specifications</a></li>
        <li><a href="#data-modeling-process">Data modeling process</a></li>
        <li><a href="#results">Results</a></li>
      </ul>
    </li>
    <li><a href="#development-details">Development Details</a></li>
    <li><a href="#challenges-and-issues">Challenges and Issues</a></li>
    <li><a href="#data-visualization">Data Visualization</a></li>
    <li><a href="#online-rollout">Online Rollout</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
    <li><a href="#references">References</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

The Project main objetive was to explore the statistical properties of cointegration applied to pairs of companies stocks (B3-Brazil Listed Companies) in a manner where the equities could be traded in a Long & Short fashion**, thus reducing capital required to trade and exposure to the market volatility. Secondary goal was to design and implement the framework to collect, store, manipulate and explore data from the B3 Database in the Cloud, building the path to other trading strategies that could benefit from the system backbone.

** long-short investment strategies are usually considered absolute return strategies, meaning that they have only negligible exposure with respect to a representative market index, since the procedure is to sell one stock and buy the other simultaneously.

### Built With

* Python
* SQL
* Google Cloud
* Scikit / Sklearn / Statsmodels (*)
* Matplotlib / Seaborn (*)

(*) Python libraries used for ML/Statitical Methods and Data Preparation/Data Visualization,  

<!-- GETTING STARTED -->
## Getting Started

** IMPORTANT     ** This project contains intellectual proprerty, thus, not all details are disclosed in this article. <br />
** IMPORTANT II  ** This Article does not have the pretension to be an academic publication, although it has some similarities in it's structure <br />
** IMPORTANT III ** The objective of this article is to provide overall unstanding of the concept and concepts used, the topics are not scrutinized at full lenght

<!-- GETTING STARTED -->
## Project Definition

<!-- Statistical -->
### Background and Statistical Concepts


  A pairs trading strategy that is based on statistical procedures is a special form of statistical arbitrage investment strategy. Cointegration, which is the main subject of this project, was largely introduced in the financial market by the work of Do, Faff, and Hamza (2006). The cointegration method is a model based, parametric approach that assumes the existence of a common stochastic trend in the price series of two financial assets. In order to understand the concept, it is important to be familiar
  with the idea behind stationary and non-stationary time series **[[Suggested Reference]](https://otexts.com/fpp2/stationarity.html)**. An important feature of two cointegrated time series is that there exists a linear combination of the two non-stationary time series that has a constant mean, which can be explored as a "mean reverting" trading strategy, betting that the relation between the two time-series will prevail and return to the mean, as long as the pair is cointegrated. The only problem that remains, is the issue that we do not know whether two time series, are actually cointegrated or not.

  There are several different approaches to address this issue, the method used on this project was to fit a ordinary least square regression (OLS) between the daily close prices of two stocks plus the time variable.

  To further explore this concept, consider that we have two time series composed by the daily close prices of Stocks A and B, for each pair A/B we performed regressions such as described below for multiple time-series sizes (E.g 100, 120, ..., N - Historical Daily Close Prices).
  <p align="center">
               Y(price A) = α(Time) + βX(Price B) + ε , for t = 1, . . . , T

  The idea behind this procedure is to get the regression error term (ε) for each T and this time-series could be assumed to be Stationary. To test this Null Hypothesis, it was  performed the augmented Dickey-Fuller test (ADF)**[[Suggested Reference]](https://en.wikipedia.org/wiki/Augmented_Dickey%E2%80%93Fuller_test)**, and considered as a candidate for trading those pairs that had a test statistic greater than the 5% critical value for multiple periods considered in the regression, as stated above we performe multiple regressions with different data collection sizes to achieve greater confidence ( Last 100, 120, ..., N daily closes), later the number os historical periodos cointegrated was used as a feature of the model.

  In the image below it is possible to see an example of the plotted Z-Score of the Error term from a pair of cointegrated Stocks; rigourously, the error term time-series from the regression of the Stocks is cointegrated, but in order to simplify, we will refer as a cointegrated pair of Stocks; 

  <br />
  <p align="center">
    <a href="https://github.com/ra024940/Pair_trading_Cointegration/Error-coint.png">
      <img src="Error-coint.png" alt="Logo" width="1152" height="276">
    </a>

  The main idea when cointegration is implemented as pair trading strategy is to constantly monitor the pairs and trade them whenever the Z-Score **[[Suggested Reference]](https://en.wikipedia.org/wiki/Standard_score)** of a cointegrated pair of stocks went further than 2 standard deviation, looking at the IMAGE 01, you can see that the latest point recorded was between +1 and +2 standard deviations, so it could not be traded at that moment.  When the Z-Score (for a given A/B pair) value gets smaller than zero, that implies that security A is undervalued in terms of security B, in which case we short-sell security B and purchase security A. If the Z-Score is larger than zero, we short-sell security A and purchase security B.

  Nevertheless, our project faced two major problems. For one, there is evidence that, due to the current heavy arbitrage activity in the financial market, simple cointegration trading returns are dwindled with tighter spreads and less trading opportunities, as stated by Hoel, 2013. Aditionally, there is no data-based approach available to provide wide understanding of how the cointegration investiment strategy performs applied to the Brazilian equity market. Our project proposition would have to address those  two major Issues, along with many other limitations, as we will see in the next sections.

<!-- Approach -->
### Project Approach and Definition

To Approach this scenario, our proposal was to create a consistent dataset that could shed some light into the brazilian stock market regarding cointegration investing and design a intelligent system that could benefit from such database and achieve higher accuracy than simple cointegration investing.

Creating a database to work with, meant to us that we needed to gather a representative historical dataset of cointegration trading candidates, along with its native characteristics and market conditions at the moment of the trade, and, of course, if the trading candidate was profitable or not. To achieve that, we could assemble, with financial market community, through a poll-like inventory, all cointegration trades performed in the last years and use this information to contruct the dataset. Obviouly, that endevour would never be succesfull, most players dont keep an accurate track of its investing history, and those who did would never disclose such sensitive information.

To address that, we decided to create our own historical dataset of cointegration trading, by running a massive exploration on the last years of all possible candidates to gather/construct its inherent cointegration information <a href="#1a">**(1)**</a> and market conditions for that moment. To accomplish that we had to plan what information would be usefull for the future model and scan each pair of stocks for every point in the timeseries (last 5 years), this proved to be a computational challenge since we had to run several regressions <a href="#1b">**(2)**</a>, statitical manipulations, which included the expensive (and primordial) cointegration test (ADF), for every datapoint, over all possible Ibovespa stock pairs (exactly 3906) for the last 5 years. The effort would be proportional to the timeframe considered in the historic data exploration, for instance, we could perform the search every 1, 5, 10, 15 minutes, or any other timeframe in accordance with the frequency of price data available in the database that we used. There was a trade-off between higher and lower frequencies to considered on the search, if the search were to be made on high frequency, we could bring to much "noise" to the dataset and the exploration could take weeks (if not months!!!) of computational time, based on the infrastructure that we had available on the cloud, in the other hand if the search were to be executed on higher frequencies, we faced the risk that the data could not be representative for building a model upon. 

With the dataset in hands <a href="#1c">**(3)**</a>, we had to increment it with aditional information required for the modeling we intended to create, this step was executed on a subset of the greater database, composed exclusively by actual trading candidates, which were selected based on a set of rules that defined the minimum requirements that a pair should meet at any given time. For example, we would not trade a given pair of stocks that were cointegrated only for the last 100 days or a pair that the Z-score spread were not beyond, at least, +/-2 standard deviations. The most important additions we made to the dataset were features capturing market conditions (e.g. historical volatility), cointegration stability (e.g is the Z-Score returning at that moment after a wider spread?) and the trade financial result, were the trade taken at that moment. To measure financial results, we had to came up with policies for when to take profits, loss or abandon the trade, for instance, we could decide, based on the total financial amount moved by the trade <a href="#1d">**(4)**</a>, to take profits with 2% and loss of 1% and abandon the trade if reaches its statistical half-life.

<br />
<p id="1a"> (1) By inherent cointegration information we mean all atributes and properties related to the cointegration at that moment, e.g. The T-statistic product of the ADF Test or the Z-Score of the regression error term at that moment, some os these information will be finally used as features consumed by the Machine Learning algorithm, we will further explore this subject in the next sections of this article. <br /></p>
<p id="1b"> (2) As Stated above, for every candidate, we decided to run several regressions considering different timeframes to achieve higher confidence (last 100 days, 120 days, ......, N Days), this would mean that the greater is the number of cointegrated periods the higher was the confidence that the candidate was indeed cointegrated at that moment.<br /></p>
<p id="1c"> (3) At that moment, the dataset was composed by a 5-year time-series for each pair, that included basic cointegration information along with statitical estimates produced concurrently, including, of course, the results of the cointegration test executed, which was the most basic information to determined if that pair could be traded at any given moment. <br /></p>
<p id="1d"> (4) Remember, this is a Long & Short financial operation, for example, consider the pair ITUB4/PETR4, if all requirement for trading are met we would long ITUB4 and short PETR4, or short ITUB4 and long PETR4, this would depend if the Z-score were positive or negative, for this particular example, if the Z-score is positive that means ITUB4 is overvalued in terms of PETR4, in that case we would short ITUB4 and purchase PETR4.</p>

<!-- Data -->
### Data Modeling Process

Concluded the stage of creating the project dataset, that, at that moment, consisted of trades for all possible Ibovespa pairs for the last 5 years which passed the cointegration test and met our rules of minimum requirements, the next step would be to take advantage of this data, we planned to create a model based on sistematic trading rules (learned by data exploration) and, in parallel, train Machine Learning algorithms to compare the performance to different market cycles.

First of all, we had to guarantee the integrity of the data we generated, some of those findings are listed in the data visualization section of this article, the data seem to be of good quality, with clear normal distribution among its many features, some outliers where dealt with, and all procedures required for data preparation were implemented, such as cleaning for missing values <a href="#1e">**(1)**</a>, normalization, encoding text and categorical atributes.

The sistematic trading rules system were the first to be implemented, different sets of trading rules (derived from the dataset features) were created based on expert financial knowledge, for instance, a simple trading rules would be to trade cointegrated pairs that have 1% of critical value as result of the ADF Test and Z-Score that exceeds +/- 3 standard deviations (that was not one of the Trading rules we used). The financial results, for each set of rules, were measured on historical data using a unique backtesting system that we design to simulate limitations that are intrinsic to real investiment, such as, limitation in the number of trades that could be open at the same time and limitation on cash available for margin guarantees required by the financial institutions, also, the results were computed averaging multiple randomized scenarios to mitigate the risk of overfitting. 

The next step was to train Machine Learning algorithms on our data, the appproach was to not make any assumptions on what learning method would be better or select features based on intuition, we followed the "No Free lunch Thoerem", as stated in the famous 1996 paper <a href="#1f">**(2)**</a>. Despite that, implementing showed to be a greater challenge than initially expected since most supervised learning methods expect i.i.d data **[[Suggested Reference]](https://statisticsbyjim.com/basics/independent-identically-distributed-data/)**, the initial results were disapointing, we were actually working with a multivariate time-series, most time series analysis methods, and even books on the topic, focus on univariate data. This is because it is the simplest to understand and work with. Multivariate data is often more difficult to work with. It is harder to model and often many of the classical methods do not perform well.

Time series forecasting can be re-framed as a supervised learning problem, and thats what we did, instead of treating the Z-Score as a signal and try to predict its behavior in the future <a href="#1g">**(3)**</a>, we framed the problem as a binary classification, training the model to predict if a trade would be profitable or not, based on the variables (features) at the very moment the trade would be opened. To do that, we had to get rid of all information that could expose our model to future-looking, since some features have a temporal dependency between observations, the model could only decorate these relationships and overfit the training set. To compensate that we incorporated some seasonal variables that reflected market condition as new features (Ex. Volatility, Number of trades generated by the pair in the last N days), this would provide the means for the algorithm to learn how seasonal market conditions affected the likelihood of trades being profitable. 

<p id="1e"> (1) You may wonder how could we have missing values since we created our own dataset, many of our procedures were implemented with paralell processing and took many days to finish, some of them (less than 0,1%) returned with missing values, due to particular reasons that are not worth exploring here.</p>

<p id="1f"> (2) David Wolpert demonstrated that if you make absolutely no assumption about the data, then there is no reason to prefer one model over any other. This is called the No Free Lunch (NFL) theorem. For some datasets the best model is a linear model, while for other datasets it is a neural network. There is no model that is a priori guaranteed to work better (hence the name of the theorem). The only way to know for sure which model is best is to evaluate them all. Since this is not possible, in practice you make some reasonable assumptions about the data and you evaluate only a few reasonable models.</p>

<p id="1g"> (3) Remember, the whole point of our approach to cointegration is that, once we have confirmed one pair of stocks to be cointegrated, we will take advantage of that and bet that every time one stock gets overvalued or undervalued in terms of the other, the spread (in our case Z-Score) will return to the average, as long as the pair remain cotintegrated.</p>

<!-- Results -->
### Results

To evaluate the results of our models, we did not use classical train/teste split of data. When dealing with time-related and dynamically changing environments, where the characteristics of the environment change throughout time, it is best to use time-based splitting to provide statistically robust model evaluation and best simulate real-life scenarios. For this we should use time-based cross validation, a method taken from the time-series field, which forms a type of “sliding window” training approach, as you can see represented in the image below.

<br />
<p align="center">
  <img src="sliding_window.png" alt="Logo" width="560" height="266">
<br />
 
<!-- Development -->
## Development Topics

<!-- Challenges & Issues -->
## Major Challenges

* Intraday vs Day Close
* Dataset creation Peformance Optimization
* Modelling Time Series (i.i.d)
* Sampling - Clusters on Data
* Recall vs Precision Trade-off

See the [open issues](https://github.com/ra024940/Pair_trading_Cointegration/issues) for a list of proposed features (and known issues).

<!-- Data -->
## Data Visualization

<br />
<p align="center">
  <img src="distribution_desvio.png" alt="Logo" width="370" height="270">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="desvio_adfstat.png" alt="Logo" width="426" height="407">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="adf_stat_percoint.png" alt="Logo" width="690" height="660">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="adfstat_periodo.png" alt="Logo" width="631" height="611">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="meia_vida_adfstat.png" alt="Logo" width="426" height="407">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="desvio_meiavida.png" alt="Logo" width="628" height="607">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<p align="center">
  <img src="adf_sign_desvio.png" alt="Logo" width="643" height="607">
</p>
Texto referente a imagem acima Texto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acimaTexto referente a imagem acima

<!-- Online -->
## Online Rollout


<!-- CONTACT -->
## Contact

Giovanni Rizzo - paiva.giovanni@gmail.com  <br />
Rafael Dias - [@rafael_rdias](https://twitter.com/rafael_rdias) - rrdias108@gmail.com

Project Link: [https://github.com/ra024940/Pair_trading_Cointegration](https://github.com/ra024940/Pair_trading_Cointegration)

<!-- References -->
## References

* Evan Gatev, 2006, Pairs Trading: Performance of a Relative Value Arbitrage Rule.
* Do, B., Faff, R. and Hamza, K. (2006) A New Approach to Modelling and Estimation for Pairs Trading.
* Hoel Christoffer Haakon, Statistical Arbitrage Pairs: Can Cointegration Capture Market Neutral Profits?
* Harlacher Markus, 2016, Cointegration Based Algorithmic - Pairs Trading, Dissertation of the University of St. Gallen

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/rafadias/
