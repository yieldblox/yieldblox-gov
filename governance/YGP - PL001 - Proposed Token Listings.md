## Preamble

```
YGP: PL(Pre-Launch)001
Title: Proposed Token Listings
Author: Markus Paulson-Luna
Status: Draft
Created: 2021-12-10
Discussion: https://discord.gg/kBPgCXFw
```

## Summary

Script3 performed an analysis of Stellar ecosystem assets to determine which should be supported by YieldBlox when the protocol launches. Our analysis focused on asset liquidity, volatility, oracle availability, relevance, volume, and trust. Based on our findings, we recommend that veYBX (formerly staked YBX), XLM, USDC, AQUA, BTC (UltraStellar), and ETH (UltraStellar) be onboarded as initially supported assets. veYBX and Aqua should have conservative risk factors.

## Motivation

The YieldBlox community needs to decide which assets to list initially in the YieldBlox genesis lending pool and their respective risk factors variables (loan-to-value ratios and liquidation incentives). In this proposal, Script3 will outline the assets and variables we believe to be safe and our reasoning. The wider community is encouraged to comment on this proposal.

## Specification

This goveranance proposal will decide which assets will be initially listed in the YieldBlox protocol

## Considerations

### Technical Notes:

- YieldBlox’s current implementation cannot support more than 12 assets in a single pool due to Stellar’s transaction limits. For simplicity, we do not think there should be more than 12 assets in a single pool anyway.
- All liquidations with collateral take place using path payments, so the withdrawn collateral is sold using either liquidity pools or the orderbook.
- When available, the YieldBlox protocol uses Coinbase, Binance, and FTX TWAP feeds as a price oracle. These prices are sanity checked with an SDEX TWAP to ensure no significant divergence.

### Analysis Criteria

Assets were assessed for listing using the following criteria on a 5 point scale:

1. _Liquidity:_ Liquidity is arguably the most important criterion. It ensures possible and profitable liquidations and insulates the protocol against oracle manipulation. Liquidity is measured by average orderbook buy-side depth and liquidity pool size. We consider liquidity pool size significantly more important than orderbook depth as it’s a much stickier form of liquidity.
2. _Volatility:_ High-volatility assets can lead to liquidations that require the default protection system to be initiated. As a result, asset volatility should be carefully considered when designating asset risk parameters.
3. _Oracle Availability:_ A wide range of available oracles makes it safer to list an asset as it’s much harder to manipulate asset price.
4. _Relevance:_ Assets initially listed in YieldBlox should be highly relevant to the Stellar and greater crypto ecosystems.
5. _Volume:_ Assets should have high volume as it means they will likely receive higher usage.
6. _Trust:_ Assets should be issued by trustworthy parties.

### Risk Parameter Definitions

- _Liquidation Incentive:_ The discount liquidators receive on the collateral they withdraw from liquidated accounts. For example, say an account is borrowing 90 USD with 400 XLM as collateral, XLM is trading at $0.25, XLM has a Loan-to-Value ratio of 80%, and XLM has a liquidation incentive of 6%. The account would be liquidated, and the liquidator would be able to repay 40 USD and withdraw 169.6 XLM.
- _Liquidation Fee:_ The liquidation fee is the percentage of the liquidation incentive that is sent to YBX Voting Escrowers. So if the total incentive for a liquidation was 10 USDC, and the liquidation fee is 10%, 1 USDC will be used to repurchase YBX and send it to the escrow pool.
- _Loan-to-Value:_ The loan to value ratio is the percentage of collateral value that can be borrowed. So if a user has $100 worth of collateral with an 80% loan to value ratio, they can borrow up to $80 worth of assets.

## Implementation

The following assets should be initially listed in the YieldBlox protocol with the described risk parameters.

### Proposed Assets

1. **veYBX** (previously sYBX)
   - **Overview:**
     Escrowed YBX (previously staked YBX) should be enabled for use as collateral immediately with a cautious loan to value ratio.
   - **Analysis:**
     1. _Liquidity:_ **(2/5)** - YBX liquidity has improved significantly since the airdrop distribution ended. We are now seeing almost $360,000 in the YBX/XLM liquidity pool. However, order book depth is relatively low.
     2. _Volatility:_ **(1/5)** - YBX is very, very volatile.
     3. _Oracle Availability:_ **(1/5)** - YBX currently only trades on the SDEX, so oracle availability is quite bad.
     4. _Relevance:_ **(5/5)** - YBX is extremely relevant to the YieldBlox protocol and Stellar ecosystem, given that it is YieldBlox’s platform/utility token.
     5. _Volume:_ **(2/5)** - YBX volume has heavily improved lately with a 7-day-volume of $1,437,849.
     6. _Trust:_ **(5/5)** - YBX is controlled by the same smart contracts that control YieldBlox and is relatively evenly distributed.
   - **Proposed Risk Parameters:**
     1. _Liquidation Incentive:_ **10%** - Getting liquidated while using veYBX as collateral damages the protocol and other YBX voting escrowers, especially given low liquidity. So it should be heavily penalized.
     2. _Liquidation Fee:_ **80%** - Liquidators should be incentivized to withdraw other types of collateral before they withdraw YBX. A liquidation fee of 80% results in the effective liquidation incentive being 2%, as 80% of liquidation profit will be paid to the escrow pool (formerly staking pool).
     3. _Loan-to-Value:_ **15%** - Oracle availability and liquidity are a significant concern for YBX. Unless either of these factors improves, it would be risky to implement a higher loan-to-value ratio. That being said, once YBX/XLM staking is added to the protocol, we think liquidity will reach a sufficient level to support higher loan-to-value ratios.
2. XLM
   - **Overview:**
     This is a no-brainer. YieldBlox is built on Stellar, so it should support Stellar’s native currency. XLM is also the most liquid and trustworthy asset in the network. That being said, XLM is a cryptocurrency, so it is volatile. We’re proposing implementing YBX with medium-risk parameters.
   - **Analysis:**
     1. _Liquidity:_ **(5/5)** - XLM is by far the most liquid asset in the Stellar ecosystem
     2. _Volatility:_ **(3/5)** - XLM is volatile with an avg StDev of 20%.
     3. _Oracle Availability:_ **(5/5)** - XLM trades on FTX, Coinbase, and Binance!
     4. _Relevance:_ **(5/5)** - XLM is Stellar’s utility token.
     5. _Volume:_ **(5/5)** - XLM has the highest volume of any asset in the Stellar ecosystem.
     6. _Trust:_ **(5/5)** - If you don’t trust XLM, you don’t trust Stellar.
   - **Proposed Risk Parameters:**
     1. _Liquidation Incentive:_ **6%** - Given XLM’s high volatility and liquidity, we think it’s logical to incentivize it to be withdrawn before other assets.
     2. _Liquidation Fee:_ **5%** - Ditto the above comment. Liquidators should want to withdraw XLM.
     3. _Loan-to-Value:_ **75%** - Good oracle availability and liquidity allow us to support a relatively high loan-to-value ratio for XLM. We think this could be as high as 85%, but given the new nature of YieldBlox, we want to start low to ensure that the liquidation mechanism can keep up during large sell-offs.
3. USDC
   - **Overview:**
     USDC is the most trustworthy and liquid stablecoin in the Stellar ecosystem. It’s a must-support asset for YieldBlox.
   - **Analysis:**
     1. _Liquidity:_ **(5/5)** - USDC is the second most liquid asset in the Stellar ecosystem, with a very deep liquidity pool and orderbook.
     2. _Volatility:_ **(5/5)** - USDC is pegged to $1.
     3. _Oracle Availability:_ **(5/5)** - USDC trades on FTX, Coinbase, and Binance!
     4. _Relevance:_ **(5/5)** - USDC is a hugely important asset on Stellar and elsewhere in the crypto ecosystem.
     5. _Volume:_ **(5/5)** USDC has high volume as it is the dominant stablecoin on the Stellar network.
     6. _Trust:_ **(5/5)** USDC is managed by Centre, which regularly publishes audits on USDC’s backing.
   - **Proposed Risk Parameters**
     1. _Liquidation Incentive:_ **4%** - USDC is the most stable asset in our protocol. As a result, we want to ensure it is the last to be liquidated to maintain the highest stability possible in the liquidatee’s position.
     2. _Liquidation Fee:_ **10%** - Standard liquidation fee. Normally most profits should go to the liquidator.
     3. _Loan-To-Value:_ **80%** - We think this could be as high as 95%, but YieldBlox’s liquidation engine is still unproven, so it’s better to start safe.
4. AQUA
   - **Overview:**
     Aqua is one of the few tokens on Stellar with real utility. It also has a huge amount of liquidity due to AQUA liquidity pool incentives. We think it’s one of the safest assets to onboard initially. That being said, given the extremely centralized supply, we suggest onboarding it with a Loan-to-Value ratio of 0%.
   - **Analysis:**
     1. _Liquidity:_ **(4/5)** - AQUA is very liquid thanks to its extremely large liquidity pools.
     2. _Volatility:_ **(2/5)** - AQUA is volatile, with an average standard deviation of 35%. This increases liquidation risk.
     3. _Oracle Availability:_ **(2/5)** - AQUA only trades on the Stellar DEX, but its large liquidity pools make its TWAP oracle fairly reliable.
     4. _Relevance:_ **(3/5)** - AQUA is an exciting new project that has made the Stellar DEX significantly more liquid.
     5. _Volume:_ **(4/5)** AQUA has very high volume, although this is in part due to the recent buzz surrounding the launch of AQUA voting.
     6. _Trust:_ **(1/5)** AQUA is currently completely centralized, and a few holders control the majority of the supply. Furthermore, the team is anonymous.
   - **Proposed Risk Parameters**
     1. _Liquidation Incentive:_ **0%** - AQUA should not be usable as collateral, so there should not be an incentive to withdraw it during a liquidation.
     2. _Liquidation Fee:_ **0%** -
     3. _Loan-To-Value:_ **0%** - Due to the lack of decentralization, we do not think it would be safe to allow AQUA to be used as collateral. Large AQUA holders would have far too much borrowing power.
5. BTC (UltraStellar)
6. ETH (UltraStellar)
   - **Overview:**
     We will cover UltraStellar anchored ETH and BTC together as they have roughly the same characteristics. Ultrastellar is a long-time member and core contributor to the Stellar community. LOBSTR is one of the most used applications in the Stellar ecosystem and one of the largest network validator groups. They have rightly earned a large amount of trust from the ecosystem. YieldBlox also needs to support a BTC and ETH anchor as they are the two most widely known and adopted cryptocurrencies. As a result, we think it makes a lot of sense to support Ultrastellar anchored ETH and BTC at protocol launch.
   - **Analysis:**
     1. _Liquidity:_ **(2/5)** - ETH and BTC are both fairly liquid due to large AMM pools and fairly deep order books.
     2. _Volatility:_ **(3/5)** - ETH and BTC are volatile as they are cryptocurrencies.
     3. _Oracle Availability:_ **(5/5)** - ETH and BTC are the most widely traded cryptocurrencies, so they have by far the highest oracle availability.
     4. _Relevance:_ **(5/5)** - ETH and BTC are extremely important assets in the greater cryptocurrency ecosystem.
     5. _Volume:_ **(1/5)** Neither of these assets has high DEX volume compared to the other proposed assets.
     6. _Trust:_ **(3/5)** Ultrastellar is an extremely well-known organization. In addition, these assets are SEP-006 and SEP-024 compatible, so on and off ramping is relatively easy.
   - **Proposed Risk Parameters**
     1. _Liquidation Incentive:_ **5%** - Given ETH’s and BTC’s high volatility, we think it’s logical to incentivize it to be withdrawn before other assets. This incentive is lower than XLM’s because XLM has much higher liquidity on-DEX than either ETH or BTC.
     2. _Liquidation Fee:_ **10%** - Standard liquidation fee. Normally most profits should go to the liquidator.
     3. _Loan-To-Value:_ **60%** - Due to ETH’s and BTC’s relatively low liquidity but similar volatility, we think a Loan-to-Value ratio slightly lower than XLM’s makes sense.

### But what about XYZ asset?????

This proposal is an open request for comment! Initial listings should be a community decision. This is a DeFi protocol after all! If you think we missed something, hop in discord and let us know!
