 # American-Option-Pricing-and-Greek-Calculation

# Overview

Hello,

This is a brand new project that I'm embarking on. I like to challenge myself on a daily basis, whether it's in sport or in my professional or personal projects. That's why I've set myself the challenge of carrying out a project combining market finance and the development of Python algorithms on a weekly basis.
The first project in this series focuses on a fundamental aspect of market finance: options pricing, with a particular emphasis on American options.

# American Options Description

American options are financial derivatives that give the holder the right, but not the obligation, to buy or sell an underlying asset at a specified price (the strike price) before or on a specified expiration date. Unlike European options, which can only be exercised at expiration, American options can be exercised at any time before the expiration date, providing greater flexibility and potential for strategic advantage.

### Key features of American options

Underlying Asset: The asset (stock, bond, commodity, etc.) on which the option is based.
Strike Price: The price at which the holder can buy (call option) or sell (put option) the underlying asset.
Expiration Date: The last date on which the option can be exercised.
Exercise: The act of buying or selling the underlying asset at the strike price.

# American Options Pricing : 

Pricing American options is more complex than pricing European options due to the flexibility of early exercise. Several methods can be used to determine the fair value of an American option:

## Binomial Tree Model

This model involves creating a tree of possible future prices for the underlying asset and evaluating the option at each node.
The tree accounts for the possibility of early exercise by comparing the immediate payoff with the expected value of holding the option.
Finite Difference Methods:

These numerical methods solve the partial differential equations (PDEs) governing the option's price.
The early exercise feature is incorporated by adjusting the boundary conditions of the PDEs.

## Monte Carlo Simulation

This method uses random sampling to simulate a large number of possible price paths for the underlying asset.
The option's value is estimated by averaging the payoffs of the simulated paths, considering the possibility of early exercise.
Black-Scholes-Merton Model:

While primarily used for European options, the Black-Scholes-Merton model can be adapted for American options with certain approximations or modifications.
Each of these methods has its advantages and limitations, and the choice of method can depend on factors such as the desired accuracy, computational resources, and the specific characteristics of the option being priced.

# Binomial Tree Model

Construct a binomial tree where each node represents a possible future asset price at each time step.

### Step 1: Calculate factors

$\Delta t = \frac{T}{N}$

$u = e^{\sigma \sqrt{\Delta t}}$

$d = \frac{1}{u}$

$p = \frac{e^{r \Delta t} - d}{u - d}$

### Step 2: Option Payoff Calculation

At maturity $T$ , calculate the payoff for each node:

$\text{Payoff}_{T} = \max(0, \text{strike} - S_T)$ for put option

$\text{Payoff}_{T} = \max(0, S_T - \text{strike})$ for call option


### Step 3: Backward Induction for Option Valuation

Start from the nodes at maturity$T$and move backward to $t = 0$ : 

$V_t = max(Payoff_t, e^{-r \Delta t} (p * V_{t+1}^{u} + q * V_{t+1}^{d}))$

where $V_{t+1}^{u}$ and $V_{t+1}^{d}$ are the option values at the next time step corresponding to up and down movements, respectively.


### Step 4: Calculate Option Price

The American option price is typically the value at the root of the binomial tree:
$\text{Option Price} = V_0 \$


# Option Greeks in Binomial Tree Model

Understanding the Greeks of options is essential for effectively managing and pricing these financial instruments. In the context of the binomial tree model, the Greeks provide valuable insights into how the price of an option reacts to changes in different factors such as the underlying asset's price, time decay, volatility, and interest rates.

By analyzing the Greeks, traders can make informed decisions regarding hedging strategies, portfolio risk management, and trading tactics.

### Delta : $\Delta$

Delta measures the sensitivity of the option price to changes in the price of the underlying asset.

Formula: $\Delta = \dfrac{V_u - V_d}{S_u - S_d}$

$V_u$ and $V_d$ are the option values at the up and down nodes of the underlying asset price.

$S_u$ and $S_d$ are the prices of the underlying asset at the up and down nodes. 

### Gamma : $\Gamma$

Gamma measures the rate of change of Delta with respect to changes in the price of the underlying asset.

Formula: $\Gamma = \dfrac{V_u - 2V_c + V_d}{(S_u - S_c)(S_c - S_d)}$

$V_c$ is the option value at the current node.

$S_c$ is the price of the underlying asset at the current node.

### Theta : $\Theta$

Theta measures the sensitivity of the option price to the passage of time.

Formula: $\Theta = \dfrac{V_u - V_d}{\Delta t}$

### Vega : $\nu$

Vega measures the sensitivity of the option price to changes in volatility.

Formula: $\nu = \dfrac{V_u - V_d}{2 \cdot \Delta \sigma}$


### Rho : $\rho$

Rho measures the sensitivity of the option price to changes in the risk-free interest rate.

Formula: $\rho = \dfrac{V_u - V_d}{2 \cdot \Delta r}$

# Monte Carlo Simulation

### Step 1: Asset Price Simulation

Simulate $M$ paths of the underlying asset price $S_t$ over $N$ discrete time steps.

Use GBM to model asset price evolution:

$S_{t+1} = S_t \exp \left( \left( r - \frac{1}{2} \sigma^2 \right) \Delta t + \sigma \sqrt{\Delta t} \cdot Z_t \right)$

where $Z_t \sim \mathcal{N}(0,1)$ are independent random variables.

### Step 2: Option Payoff Calculation

At each time step $t$ , calculate the payoff for each path:

$\text{Payoff}_t = \max(0, \text{strike} - S_t)$ for put option

$\text{Payoff}_t = \max(0, S_t - \text{strike})$ for call option

### Step 3: Backward Induction for Option Valuation

Start from the maturity $T$ and move backward to $t = 0$ :

$ V_t = \max \left( \text{Payoff}_t, \mathbb{E} \left (e^{-r \Delta t} V_{t+1} \mid \mathcal{F}_t \right) \right) $

where $\mathcal{F}_t$ is the information set at time $t$ , and $\mathbb{E}$ denotes the expectation.

### Step 4: Calculate Option Price

The American option price is typically the discounted expected value of the option payoff:
$\text{Option Price} = e^{-rT} \mathbb{E}[V_0]$

# Option Greeks in Monte Carlo Simulation

### Delta : $\Delta$

Delta measures the sensitivity of the option price to changes in the price of the underlying asset.

Formula: $\Delta_{\text{call}} = \frac{V(S_0 + \epsilon) - V(S_0)}{S_0 \cdot \epsilon}$  $\Delta_{\text{put}} = \frac{V(S_0) - V(S_0 - \epsilon)}{S_0 \cdot \epsilon}$

$S_0$ is the Underlying Asset price at the beginning.
$\epsilon$ is a pertubations in the price. 

### Gamma : $\Gamma$

Gamma measures the rate of change of Delta with respect to changes in the price of the underlying asset.

Formula: $\Gamma_{\text{call}} = \frac{V(S_0 + \epsilon) - 2V(S_0) + V(S_0 - \epsilon)}{S_0^2 \cdot \epsilon^2}$  $\Gamma_{\text{put}} = \frac{V(S_0 + \epsilon) - 2V(S_0) + V(S_0 - \epsilon)}{S_0^2 \cdot \epsilon^2}$

### Theta : $\Theta$

Theta measures the sensitivity of the option price to the passage of time.

Formula: $\Theta = \frac{V(t + \Delta t) - V(t)}{\Delta t}$

### Vega : $\nu$

Vega measures the sensitivity of the option price to changes in volatility.

Formula: $\nu_{\text{call}} = \frac{V(S_0, \sigma + \epsilon) - V(S_0, \sigma)}{\epsilon}$ $\nu_{\text{call}} = \frac{V(S_0, \sigma + \epsilon) - V(S_0, \sigma)}{\epsilon}$

### Rho : $\rho$

Rho measures the sensitivity of the option price to changes in the risk-free interest rate.

Formula: $\text{Rho} = T \cdot \epsilon \left[ V(S_0, r + \epsilon) - V(S_0, r) \right]$

# Conclusion

This project aims to implement and compare different methods for pricing American options and Greeks Calculations using Python. Through this, I hope to deepen my understanding of options pricing and enhance my Python programming skills. Stay tuned for more updates and insights as I progress through this exciting challenge!

## Contact
For any questions or further information, please feel free to reach out to me on linkedin : https://www.linkedin.com/in/maxime-le-floch-1ba66a1b1/ or by mail : maximebeguin02@gmail.com.

## Bibliogrphy Use 

https://homepage.ntu.edu.tw/~jryanwang/courses/Financial%20Computation%20or%20Financial%20Engineering%20(graduate%20level)/FE_Ch04%20Binomial%20Tree%20Model.pdf

https://en.wikipedia.org/wiki/Binomial_options_pricing_model

https://www.jeroenbouma.com/articles/binomial-trees

https://www.scirp.org/journal/paperinformation?paperid=77675


