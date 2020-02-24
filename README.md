# Yijun Wang 
# (Feb 10 - 14, 2020)

### Model 1: Estimation of R<sub>0</sub>
- Purpose
  * Estimate the value of basic reproduction number
- Usage
  * Download my Jupyter notebook file: [Estimation of R0.ipynb](https://github.com/yijunwang0805/YijunWang/blob/master/Estimation%20of%20R0_Yijun/Estimation%20of%20R0.ipynb).
  
  * ```R0Func()``` is the function that calculates the basic reproduction number. Its ```inputs``` are the number of ```confirm``` cases, the number of ```suspect``` cases, and days ```t``` since the start of the epidemic. Here, we use the December 1st, 2019 as the start of the epidemic, which is the first nCoV case reported. 

- Summary
  * This study seeks to estimate the basic reproduction number by deriving R<sub>0</sub> from the SEIR model. As of 2020-02-14, R<sub>0</sub> is estimated to be 2.41.
- Model
  * <a href="https://www.codecogs.com/eqnedit.php?latex=R_0&space;=&space;1&space;&plus;&space;\lambda&space;T_G&space;&plus;&space;\rho(1&space;-&space;\rho)&space;(\lambda&space;T_G)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R_0&space;=&space;1&space;&plus;&space;\lambda&space;T_G&space;&plus;&space;\rho(1&space;-&space;\rho)&space;(\lambda&space;T_G)^2" title="R_0 = 1 + \lambda T_G + \rho(1 - \rho) (\lambda T_G)^2" /></a>
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; where,

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  lambda is the growth rate of estimated infectious

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  rho is the ratio of latent period over generation period.
  
### Model 2: Forecasting Using SEIR model
- Purpose
  * Forecast the SARS-CoV-2 epidemic peak time in metropolis by applying a deterministic SEIR metapopulation transmission model
- Usage
  * Download my Jupyter notebook file: [SEIR.ipynb](https://github.com/yijunwang0805/YijunWang/blob/master/SEIR%20Forecast_Yijun%20Wang%20%26%20Owen%20Xu/SEIR.ipynb).
  
  * ```R0Func()``` is the function that calculates the newest basic reproduction number given up to date statistics. Its ```inputs``` are the number of ```confirm``` cases, the number of ```suspect``` cases, and days ```t``` since the start of the epidemic. Here, we use the December 1st, 2019 as the start of the epidemic, which is the first nCoV case reported. 
  * ```SEIR()``` is the epidemic model that describes the system of differential equations.
  * ```betaFunc()``` and ```gammaFunc()``` calculate the value of transmissibility and removal rate, respectively.
  * ```spi.odeint()``` solves the system of differential equations. Its ```inputs``` are the epidemic model ```SEIR()```, initial value of susceptible, exposed, infectious, removal ```INI```, and the number of days since the epidemic ```Time```
  * Please note the **several assumptions** will limit the use of this model, for instance, assumption of consistent behaviors before and during the epidemic means that people do **not** implement social or non-pharmaceutical intervention.
- Summary
  * This study seeks to forecast the peak time of SARS-CoV-2 cases. We find, under the assumptions of no quaratine intervention, Wuhan reach peak infectiouson March 3, 2020; Beijing, Shanghai, and Guangzhou would each peak infectious in the middle of May. 
  * Sensitivity analysis shows that reducing half of the number of catchment size and the reproductive number would reduce the magnitude of epidemic by more than 60%, while lengthening the peak to June and duration of the epidemic to August.
- Model
  * A typical **SEIR** (susceptible, exposed, infectious, removed) model can be described as a system of differential equations

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  <a href="https://www.codecogs.com/eqnedit.php?latex=\small&space;\frac{dS}{dt}&space;=&space;-\beta&space;frac{S(t)I(t)}{N}&space;\newline&space;\frac{dE}{dt}&space;=&space;\beta&space;\frac{S(t)I(t)}{N}&space;-&space;\alpha&space;E(t)&space;\newline&space;\frac{dI}{dt}&space;=&space;\alpha&space;E(t)&space;-&space;\gamma&space;I(t)&space;\newline&space;\frac{dR(t)}{dt}&space;=&space;\gamma&space;I(t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\small&space;\frac{dS}{dt}&space;=&space;-\beta&space;\frac{S(t)I(t)}{N}&space;\newline&space;\frac{dE}{dt}&space;=&space;\beta&space;\frac{S(t)I(t)}{N}&space;-&space;\alpha&space;E(t)&space;\newline&space;\frac{dI}{dt}&space;=&space;\alpha&space;E(t)&space;-&space;\gamma&space;I(t)&space;\newline&space;\frac{dR(t)}{dt}&space;=&space;\gamma&space;I(t)" title="\small \frac{dS}{dt} = -\beta \frac{S(t)I(t)}{N} \newline \frac{dE}{dt} = \beta \frac{S(t)I(t)}{N} - \alpha E(t) \newline \frac{dI}{dt} = \alpha E(t) - \gamma I(t) \newline \frac{dR(t)}{dt} = \gamma I(t)" /></a>

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; where,
   
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; S(t) is the number of susceptible at time t

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; E(t) is the number of exposed at time t

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; I(t) is the number of infectious at time t

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; R(t) is the number of removed, which includes the number of recovered and dead at time t

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; N(t) is the population at time t

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; N(t) = S(t) + E(t) + I(t) + R(t)

### Model 3: Impact on Economic Growth (In progress)
- A panel approach for external shock: 
  - exploiting the dependence among cross-sectional units to construct the counterfactuals
- Look for data! 寻求高频率或跨区域的经济相关的数据，如航班，交通，货运量，酒店入住率，邮政，就业，服装，淘宝等能反应经济相关的数据，如您有相关数据，请联系我。只用于学术用途且标明出处。


### Special Thanks to 
- [Wuhan 2020](https://github.com/wuhan2020/nCov-2019-data-science)'s data science team
- [BlankerL](https://github.com/BlankerL/DXY-COVID-19-Crawler)'s Crawler
