# Uniswapv3 position management (UPM)
The goal of this project is to help users manage their uniswapv3 positions.

## Compounding fees
Fee collection should only happen when the amount spent on gas is a small percentage (<5%) of the total fees collected. Usually, this means the amount collected needs to be at least $1,000, assuming a gas cost of around $50 for the transaction. Proposed workflow:
1. User will connect wallet so dApp can read all uniswapv3 nft positions
2. Site will display all positions by pair, total current value and accrued fees, provide manual `compound` button to test functionality
3. Monitor accrued fees
4. After $1,000 in fees has accrued, begin monitoring gas costs and process appropriate strategy (strategy doesn't exist in v0.1, proceed to 3)
5. When gas costs are less than 5% of total accrued fees, use the `collectFees()` function to collect fees from position
6. After fees are collected, monitor gas costs and begin to add liquidity once cost is <= $50
7. Add max amount of TokenA and corresponding amount of ETH using the `addLiquidity()` function, while ensuring there is at least 1 ETH left in wallet balance. If this transaction would result in a wallet balance with less than 1 ETH left, then add any ETH over 1 and the corresponding amount from TokenA.

---
## Future enhancements

### Strategies

#### Bullish (not included in v0.1)
If strategy is bullish TokenA and current token split is 60% ETH or more, follow these steps:
1. When gas costs are less than 5% of total accrued fees, remove position
2. Follow process for adding a bullish position to re-establish position

### Choosing a range (not included in v0.1)
There are various strategies one can use to establishing a trading range for any currency pair. For instance, in an ETH-TokenA pair, if one is bullish on tokenA, the range would skew high, leaving lots of room for TokenA to grow against ETH. A more neutral strategy using descriptive statistics could use bollinger bands to establish a tranding range. Because of the large number of different strategies and current subjective reliance on technical analysis (TA) interpretation, this functionality will not be included in the initial scope of the first version.