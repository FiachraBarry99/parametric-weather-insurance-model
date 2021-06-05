# Parametric Weather Insurance Model
A parametric weather insurance pricing model that can return information such as the premium, the required collateral and the sharpe ratio of the securatised insurance policy. For this example I used historical wind speed data from Met Éireann which is licensed under a [Creative Commons Attribution 4.0 license](http://creativecommons.org/licenses/by/4.0/). Though this example uses wind speed data this model could be used for any parametric weather condition insurance.
  
The policy is structured so that the client would choose strike and whether they want the policy to pay out when the actual value is higher or lower than that. They can also choose to have the policy only pay out if the actual value is above/below the strike for a certain number of days. This can significantly reduce the premium price. If there is the required number of days in a row the policy will pay out for each day. The premium is calculated as the amount required to pay out an average year of pay outs multiplied by a correction factor. The collateral is calculated as the maximum amount that would have had to be paid out over the simulated period. The securatisation of the policy is so that the initial investment is the collateral and the payments to the holder of the security are the premium amount minus any pay outs. The policy is defined as one year long.
  
The policy is defined as a class to allow easy access to information after initialisation. The properties of this class are the premium, the required collateral and the sharpe ratio of the securatised insurance policy. There are also additional properties but these are used for debugging or for the `InsurancePolicy.simulate()` method. This method shows a simulation of what the returns would be like if you held the securatised policy for a number of years. Either as a distribution of returns or a cumulative simulation of holding a securatised policy for a number of years  
  
At the moment this class calculates these properties by targeting a required return. It could be modified to target a required sharpe ratio but that would require iterating through the `__init__` function multiple times which would take an extremely long time. Also, if the eventual holder of the securatised policy holds a diversified portfolio of policies the volatility of the policy should become less of an issue.    
  
## `InusrancePolicy` class parameters:
`strike`: the value above/below which the policy pays out  
`amount`: the amount that is paid out to the insured (usually daily revenue value)  
`data`: the source of historical data (Pandas series)  
`high_or_low`: whether the client wants a policy to payout when the actual value is above/below strike  
`consec_days`: the amount of consecutive days of the actual value being above/below the strike for the policy to pay out  
`n`: number of samples taken from data during Monte Carlo simulation. Reduce this value if objects are taking too long too initialise but you will be sacrificing accuracy  
`tr`: the target return in decimal value  
  
#### `InsurancePolicy.simulate()` method parameters:  
`sim_type`: 'dist' for distribution of returns or 'cumul' for cumulative returns of holding a securatised policy for a number of years  
`sim_start`: where to start the simulation  
`sim_end`: where to end the simulation  
  
## License:  
This code may be remixed, used or altered for personal purposes as long as credit is given. If you wish to use this code for commerical purposes please feel free to contact me (fiachrabarry@gmail.com).
