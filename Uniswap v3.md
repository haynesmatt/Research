# Uniswap v3

> **Table of Contents**
> 

[](https://uniswap.org/whitepaper-v3.pdf)

[UNISWAP V3 - New Era Of AMMs? Architecture Explained](https://youtu.be/Ehm-OYBmlPM)

## Abstract

Uniswap v3 is a noncustodial automated market maker implemented for the Ethereum Virtual Machine. In comparison to earlier versions of the protocol, Uniswap v3 provides **[increased capital efficiency](Uniswap%20v3%20263925ade73946c29c23e1dd6cad6523.md)** and **[fine-tuned control to liquidity providers](Uniswap%20v3%20263925ade73946c29c23e1dd6cad6523.md)**, improves the accuracy and convenience of the price oracle, and has a more flexible fee structure.

- What is an Automated Market Maker (AMM)?
    - An algorithm that uses a liquidity pool to keep a balance of the two or more tokens in that pool using supply and demand
    - Benefits: This solution means that intermediaries are no longer required, and now you can directly swap from token to token. You can also cross-swap.

## V1

- Launched in Nov 2018
- ERC20-ETH liquidity pools

## V2

- Launched in May 2020
- Addition of ERC20-ERC20 liquidity pools
- Later 2020, saw rapid growth, its AMM became standard
    - Became most forked project in the DeFi space
- Sushiswap
    
    

## V3

- Launched in May 2021
    - on Ethereum Mainnet & Optimism (an Ethereum Layer 2 scaling solution)

### **focuses on maximizing capital efficiency**

- allows LP to earn a higher return on their capital
- also dramatically improves **trade execution** - its quality is comparable… or even surpasses centralized exchanges & stable coin focused AMMs

### **fine-tuned control to liquidity providers**

- LPs can also create overall portfolios that significantly increase exposure to **preferred assets** & **reduce** **downside risk**
    - in my words: LPs now have more freedom to choose how many and which coins to provide as liquidity - without worrying about downside risk!

### **improves price oracle**

- in essence, can detect coin prices more accurately and precisely

### **more flexible fee structure**

- Instead of just 0.3% trading fees, now have **4** **different fee tiers**
    - 0.01% 0.05% 0.3% 1%
    - Allows LPs to choose pools based on risk willing to take
    - Lower % intends for more **stable** pairs, higher % for more **exotic** pairs
- **THIS IS ALL POSSIBLE BECAUSE OF CONCENTRATED LIQUIDITY**
    - can add single assets as liquidity as to a price range (above or below the current market price)
        - creates a fee earning limit order that executes along a smooth curve

## What is concentrated liquidity?

### Let’s look at v2…

- When LPs provided liquidity to a v2 pool, liquidity was distributed **evenly** **along the price curve**
    - allows handling all price ranges (from 0 to ∞)
    - makes capital **inefficient**
        - because most assets only trade within a certain price range
            - Especially true for **stable coins**, such as USDC/DAI, where the range is from $0.99 to $1.01 for vast majority of trading activity, & where most trading fees will incur
                - in this example, theoretically **99.5%** of the remaining capital is never used!
    - basically, each pool only had **one curve**, need a new pool for new curve
        - routing a trade between multiple pools results in **high gas fees - inefficient**

### Now, let’s look at v3

- we now have **individualized price curves** for each LP (instead of distributing liquidity evenly along the curve)

<aside>
💡 Users trade against **combined liquidity** that is available at a **certain price point**
That liquidity comes from **all curves that overlap** at that certain price point

</aside>

- LPs only earn the trading fees proportional to the amount they provided in that liquidity range
    - This is why concentrating liquidity yields much better capital efficiency for LPs
- How much more efficient is v3 than v2?
    - Crunching some numbers, setting a range for 0.1% yields 4,000x more efficiency
    - a range as granular as 0.02% yields 20,000x more efficiency

## What is Active Liquidity?

- Well, what happens if the price of the coin moves outside of LP’s liquidity range?
    - The LP’s liquidity is **effectively removed** from the pool & stops earning fees
    - LPs liquidity shifts completely towards one of the assets / they end up holding only one of them
    - What are LP’s options?
        - Can **wait** until market price moves back to their liquidity range
        - Can **update** range to account for current prices
    - With concentrated liquidity, it’s possible that a specific price range will have **no liquidity**
        - This in turn creates **massive opportunity** for LPs to jump in and provide liquidity to that price range
            - If they’re the only ones providing liquidity, they can collect **all** trading fees at that range

## What are the types of liquidity providers we can now have?

1. Those who provide liquidity at common, narrow ranges
2. Those who provide liquidity at less likely, more profitable ranges
3. Those who adjust their ranges as the prices move out of range

## Multiple Price Ranges

<aside>
💡 LPs can provide liquidity to **multiple price ranges**, that **may or may not overlap**

</aside>

- Allows for approximating any price curve or even an order book
- Also in general, allows to create more sophisticated market making strategies

## What are Range Limit Orders?

- Allows LPs to provide a **single token** (token1) as liquidity in a custom price range **above** or **below** the **current market price**
    - When the price of the token1 hits that range, the token1 **converts to** token2, **along a smooth curve**, all while **still earning swap fees** in the process
        - When used with a narrow range, allows for achieving a similar goal to a **standard limit order** that can be set at a specific price
    - Must sell the token2 at this point, because if it leaves the range, token2 **converts back** to token1
- What’s the point? How do they earn money?

## Non fungible liquidity

- LPs’ liquidity positions are no longer fungible & cannot be represented by ERC20 LP tokens, since each LP can basically create their own price curve
    - Instead, providing liquidity is tracked by non-fungible ERC721 tokens
    - However, LP positions that fall within the same price can still be represented by peripheral contracts or through other partner protocols
- Trading fees are no longer reinvested back into the liquidity pool on LPs behalf
    - instead, peripheral contracts can be created to offer such functionality

# Unfamiliar Terms

peripheral contracts

limit order

price curve

- price range of a coin?

layer 1

layer 2