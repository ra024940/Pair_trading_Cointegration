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
      <ul>
        <li><a href="#background-and-statistical-concepts">Background and Statistical Concepts</a></li>
        <li><a href="#project-approach-and-definition">Project Approach and Definition</a></li>
        <li><a href="#data-modeling-process">Data modeling process</a></li>
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

** IMPORTANT    ** This project contains intellectual proprerty, thus, not all details are disclosed in this article. <br />
** IMPORTANT II ** This Article does not have the pretension to be an academic publication, although it has some similarities in it's structure

<!-- Statistical -->
<details open="open"> 
  <summary>### Background and Statistical Concepts</summary>


  A pairs trading strategy that is based on statistical procedures is a special form of statistical arbitrage investment strategy. Cointegration, which is the main subject of this project, was largely introduced in the financial market by the work of Do, Faff, and Hamza (2006). The cointegration method is a model based, parametric approach that assumes the existence of a common stochastic trend in the price series of two financial assets. In order to understand the concept, it is important to be familiar
  with the idea behind stationary and non-stationary time series **[[Suggested Reference]](https://otexts.com/fpp2/stationarity.html)**. An important feature of two cointegrated time series is that there exists a linear combination of the two non-stationary time series that has a constant mean, which can be explored as a "mean reverting" trading strategy, betting that the relation between the two time-series will prevail and return to the mean, as long as the pair is cointegrated. The only problem that remains, is the issue that we do not know whether two time series, are actually cointegrated or not.

  There are several different approaches to address this issue, the method used on this project was to fit a ordinary least square regression (OLS) between the daily close prices of two stocks plus the time variable.

  To further explore this concept, consider that we have two time series composed by the daily close prices of Stocks A and B, for each pair A/B we performed regressions such as described below for multiple time-series sizes (E.g 100, 120, ..., N - Historical Daily Close Prices).
  <p align="center">
               Y(price A) = α(Time) + βX(Price B) + ε , for t = 1, . . . , T

  The idea behind this procedure is to get the regression error term (ε) for each T and this time-series could be assumed to be Stationary. To test this Null Hypothesis, it was  performed the augmented Dickey-Fuller test (ADF)**[[Suggested Reference]](https://en.wikipedia.org/wiki/Augmented_Dickey%E2%80%93Fuller_test)**, and considered as a candidate for trading those pairs that had a test statistic greater than the 5% critical value for multiple periods considered in the regression, as stated above we performe multiple regressions with different data collection sizes to achieve greater confidence ( Last 100, 120, ..., N daily closes), later the number os historical periodos cointegrated was used as a feature of the model.

  In the image below (IMAGE 01) it is possible to see an example of the plotted Z-Score of the Error term from a pair of cointegrated Stocks; rigourously, the error term time-series from the regression of the Stocks is cointegrated, but in order to simplify, we will refer as a cointegrated pair of Stocks; 

  <br />
  <p align="center">
    <a href="https://github.com/ra024940/Pair_trading_Cointegration/Error-coint.png">
      <img src="Error-coint.png" alt="Logo" width="1152" height="276">
    </a>

  The main idea when cointegration is implemented as pair trading strategy is to constantly monitor the pairs and trade them whenever the Z-Score **[[Suggested Reference]](https://en.wikipedia.org/wiki/Standard_score)** of a cointegrated pair of stocks went further than 2 standard deviation, looking at the IMAGE 01, you can see that the latest point recorded was between +1 and +2 standard deviations, so it could not be traded at that moment.  When the Z-Score (for a given A/B pair) value gets smaller than zero, that implies that security A is undervalued in terms of security B, in which case we short-sell security B and purchase security A. If the Z-Score is larger than zero, we short-sell security A and purchase security B.

  Nevertheless, our project faced two major problems. For one, there is evidence that, due to the current heavy arbitrage activity in the financial market, simple cointegration trading returns are dwindled with tighter spreads and less trading opportunities, as stated by Hoel, 2013. Aditionally, there is no data-based approach available to provide wide understanding of how the cointegration investiment strategy performs applied to the Brazilian equity market. Our project proposition would have to address those  two major Issues, along with many other limitations, as we will see in the next sections.

</details>

<!-- Approach -->
### Project Approach and Definition

To Approach this scenario, our proposal was to create a consistent dataset that could shed some light into the brazilian stock market regarding cointegration investing and design a intelligent system that could benefit from such database and achieve higher accuracy than simple cointegration investing.

Creating a database to work with, meant to us that we needed to gather a representative historical dataset of cointegration trading candidates, along with its native characteristics and market conditions at the moment of the trade, and, of course, if the trading candidate was profitable or not. To achieve that, we could assemble, with financial market community, through a poll-like inventory, all cointegration trades performed in the last years and use this information to contruct the dataset. Obviouly, that endevour would never be succesfull, most players dont keep an accurate track of its investing history, and those who did would never disclose such sensitive information.

To address that, we decided to create our own historical dataset of cointegration trading candidates, by running a massive search in the last years of all possible candidates and gather/construct its inherent cointegration information (1) and market conditions for that moment. We planned what information would be usefull for the future model and this data would have to be calculated for each point in the timeseries (5 years) of all possible stock pairs listed in the main brazilian stock index (Ibovespa), this proved to be a computational challenge since we had to run several regressions (2) and statitical manipulations for every datapoint, for all possible IBovespa stock pairs (exactly 3906) for the last 5 years. The effort would be proportional to the timeframe considered in the historic data exploration, for instance, we could perform the search every 1, 5, 10, 15 minutes, or any other timeframe in accordance with the price data frequency available in the database where we collected. There was a trade-off between higher and lower frequencies to considered on the search, if the search were to be made on high frequency, we could bring to much "noise" to the dataset and the exploration could take weeks (if not months!!!) of computational time, based on the infrastructure that we had available on the cloud, in the other hand if the search were to be executed on higher frequencies, we faced the risk that the data could not be representative for building a model upon. 

<br />
(1) By inherent cointegration information we mean all atributes and properties related to the cointegration at that moment, e.g. The T-statistic product of the ADF Test or the Z-Score of the regression error term at that moment, some os these information will be finally used as features consumed by the Machine Learning algorithm, we will further explore this subject in the next sections of this article. <br />
(2) As Stated above, for every candidate, we decided to run several regressions considering different timeframes to achieve higher confidence (last 100 days, 120 days, ......, N Days), this would mean that the greater is the number of cointegrated periods the higher was the confidence that the candidate was indeed cointegrated at that moment.

<!-- Approach -->
### Data Modeling Process

<!-- Development -->
## Development Details

<!-- Challenges & Issues -->
## Challenges and Issues

See the [open issues](https://github.com/ra024940/Pair_trading_Cointegration/issues) for a list of proposed features (and known issues).

<!-- Data -->
## Data Visualization

<!-- Online -->
## Online Rollout

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

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
