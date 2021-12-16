## Preamble

```
YGP: PL(Pre-Launch)002
Title: Proposed YBX Issuance
Author: Markus Paulson-Luna
Status: Draft
Created: 2021-12-16
Discussion: https://discord.gg/4hDYffSS
```

## Summary

The YieldBlox community needs to decide what the initial `YBX_ISSUANCE_RATE` variable should be. This governs how quickly YBX is issued. We are proposing an issuance rate variable of .00075.

## Motivation

Effective YBX issuance is crucial to the long term health of the protocol. It distributes governance control to protocol users and incentives protocol usage. Issuance must be high enough to attract significant TVL and distribute sufficient governance power. However, we must be careful not to issue too aggressively or dilution will happen too quickly.

## Specification

This governance proposal will set the `YBX_ISSUANCE_RATE` data entry in the YieldBlox Distribution Account. This variable is fed into the YBX Issuance Equation to determine daily issuance.

## Considerations

- YBX Issuance Equation\
  *I = (T-O) * R*\
  Where:

      - I = YBX Issuance on a given day
      - T = Total YBX Issuance (currently 1.5 billion)
      - O = Total YBX Outstanding (initially 690 million)
      - R = YBX Issuance Rate (Variable under discussion)

- An issuance rate of .00075 will issue 167,126,751.68 YBX over the first year which means total YBX outstanding will be 857,126,751.68 (most of this will not be circulating). At this issuance rate, 1,447,581,612 YBX will be outstanding after 10 years.
   - There will be 690 million YBX outstanding initially
     - 375 million in the DAO treasury
     - 10 million from the airdrop
     - 34.95 million allocated to the bug bounty
     - 150 million in the Script3 Partnership Treasury
     - 82.5 million allocated to the team (4 year vesting schedule with a 1 year cliff)
     - 37.5 million allocated to investors (unlocked after 1 year)
- Assuming a that YBX's price remain's constant, that 50% of YBX issuance is directed to escrower's (formerly stakers), and that APR for lenders stabilizes at 25%, this issuance rate targets a TVL of $ 501,380,255.04.
- This issuance rate guarantees that team and investor token allocations will be the minority of voting power after the first year.
   - After 1 year 177,126,751.68 YBX will be held by the community and 58,125,000.00 will be held by the team+investors.

## Implementation

This governance proposal will set the `YBX_ISSUANCE_VARIABLE` in the initial YieldBlox protocol to .00075.

## Other Materials

### Visualizations

#### YBX Issuance Over Year 1
![image](https://user-images.githubusercontent.com/59978114/146439511-b8afb7d2-fd6f-451d-bf32-17ff6887386f.png)

#### YBX Issuance Over 10 Years
![image](https://user-images.githubusercontent.com/59978114/146439960-95002754-2ed9-4b49-9608-9cadba1f64c0.png)

#### % of YBX Issued Over 10 Years
![image](https://user-images.githubusercontent.com/59978114/146437622-88fb4c1a-f0d5-4491-872b-1a89dc9f2fc1.png)

