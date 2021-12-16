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
  ![\Large](<https://latex.codecogs.com/svg.latex?I%20%3D%20(T-O)*R>)  
  Where:

      - I = YBX Issuance on a given day
      - T = Total YBX Issuance (currently 1.5 billion)
      - R = YBX Issuance Rate

- An issuance rate of .00075 will issue 167,126,751.68 YBX over the first year which means total YBX outstanding will be 857,126,751.68 (most of this will not be circulating). At this issuance rate 1,447,581,612 YBX will be outstanding after 10 years.
- Assuming a constant YBX price and that APR for lenders stabilizes at 25%, this issuance rate targets a TVL of $ 501,380,255.04.
- This issuance rate guarantees that team and investor token allocations will be the minority of voting power after the first year. Total team and founder allocations are 117,500,000 YBX (most is still locked after the first year).

## Implementation

This governance proposal will set a variable in the initial YBX protocol release
