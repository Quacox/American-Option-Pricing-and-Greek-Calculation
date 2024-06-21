# American-Option-Pricing-and-Greek-Calculation

## Overview

Hello,

This is a brand new project that I'm embarking on. I like to challenge myself on a daily basis, whether it's in sport or in my professional or personal projects. That's why I've set myself the challenge of carrying out a project combining market finance and the development of Python algorithms on a weekly basis.
The first project in this series focuses on a fundamental aspect of market finance: options pricing, with a particular emphasis on American options.

## American Options Description

American options are financial derivatives that give the holder the right, but not the obligation, to buy or sell an underlying asset at a specified price (the strike price) before or on a specified expiration date. Unlike European options, which can only be exercised at expiration, American options can be exercised at any time before the expiration date, providing greater flexibility and potential for strategic advantage.

## Key features of American options:

Underlying Asset: The asset (stock, bond, commodity, etc.) on which the option is based.
Strike Price: The price at which the holder can buy (call option) or sell (put option) the underlying asset.
Expiration Date: The last date on which the option can be exercised.
Exercise: The act of buying or selling the underlying asset at the strike price.

## American Options Pricing : 

Pricing American options is more complex than pricing European options due to the flexibility of early exercise. Several methods can be used to determine the fair value of an American option:

### Binomial Tree Model:

This model involves creating a tree of possible future prices for the underlying asset and evaluating the option at each node.
The tree accounts for the possibility of early exercise by comparing the immediate payoff with the expected value of holding the option.
Finite Difference Methods:

These numerical methods solve the partial differential equations (PDEs) governing the option's price.
The early exercise feature is incorporated by adjusting the boundary conditions of the PDEs.

### Monte Carlo Simulation:

This method uses random sampling to simulate a large number of possible price paths for the underlying asset.
The option's value is estimated by averaging the payoffs of the simulated paths, considering the possibility of early exercise.
Black-Scholes-Merton Model:

While primarily used for European options, the Black-Scholes-Merton model can be adapted for American options with certain approximations or modifications.
Each of these methods has its advantages and limitations, and the choice of method can depend on factors such as the desired accuracy, computational resources, and the specific characteristics of the option being priced.

# Conclusion

This project aims to implement and compare different methods for pricing American options using Python. Through this, I hope to deepen my understanding of options pricing and enhance my Python programming skills. Stay tuned for more updates and insights as I progress through this exciting challenge!

# Contact
For any questions or further information, please feel free to reach out to me on linkedin : https://www.linkedin.com/in/maxime-le-floch-1ba66a1b1/ or by mail : maximebeguin02@gmail.com.
