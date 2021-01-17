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




<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
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
        <li><a href="#statistical-and-Background">Statistical Concept and Background</a></li>
        <li><a href="#project-approach-and-definition">Project Approach and Definition</a></li>
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

The Project main objetive was to explore the statistical properties of cointegration applied to pairs of companies stocks (B3-Brazil Listed Companies) in a manner where the equities could be traded in a Long & Short fashion, thus reducing capital required to trade and exposure to the market volatility. Secondary goal was to design and implement the framework to collect, store, manipulate and explore data from the B3 Database in the Cloud, building the path to other trading strategies that could benefit from the system backbone.

### Built With

* Python
* SQL
* Google Cloud
* Scikit / Sklearn / Statsmodels (*)
* Matplotlib / Seaborn (*)

(*) Python libraries used for ML/Statitical Methods and Data Preparation/Data Visualization,  

<!-- GETTING STARTED -->
## Getting Started

** IMPORTANT ** This project contains intellectual proprerty, thus, not all details are disclosed in this article.

<!-- Statistical -->
### Statistical Concept and Background

A pairs trading strategy that is based on statistical procedures is a special form of statistical arbitrage investment strategy. Cointegration, which is the main topic of this article, was largely introduced in the financial market by the work of Do, Faff, and Hamza (2006). The cointegration method is a model based, parametric approach that assumes the existence of a common stochastic trend in the price series of two financial assets. In order to understand the concept, it is important to be familiar
with the idea behind stationary and non-stationary time series **[Stationary Time Series](https://otexts.com/fpp2/stationarity.html)**. An important feature of two cointegrated time series is that there exists a linear combination of the two non-stationary time series that has a constant mean, which can be explored as a "mean reverting" Strategy. The only problem that remains, is the issue that we do not know whether two time series, are actually cointegrated or not.

long-short investment strategies are usually considered absolute return strategies, meaning that they have only negligible exposure with respect to a representative market index.
<!-- Approach -->
### Project Approach and Definition

Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_

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

Rafael Rodrigues Dias - [@rafael_rdias](https://twitter.com/rafael_rdias) - rrdias108@gmail.com

Project Link: [https://github.com/ra024940/Pair_trading_Cointegration](https://github.com/ra024940/Pair_trading_Cointegration)

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* []()
* []()
* []()

<!-- References -->
## References

* Celume MP, Besançon M & Zenasni F 2019, 'Fostering children and adolescents’ creative thinking in education: theoretical model of drama pedagogy training', Frontiers in Psychology, vol. 9, viewed 11 February 2019, <https://www.frontiersin.org/article/10.3389/fpsyg.2018.02611>
* Evan Gatev, 2006, 
* Do, Faff, and Hamza (2006)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/rafadias/
