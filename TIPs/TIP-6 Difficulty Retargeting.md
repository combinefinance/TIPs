---
TIP: 6
Title: Modify Difficulty Retargeting
Discussions-to: None
Status: Draft
Category: On-chain > Security
Author: Shepard (@ngc-3656)
Created: 2020-11-30
---

# TIP-6: Modify Difficulty Retargeting

### TLDR
* Change the difficulty retargeting algorithm to retarget based on slots 1-4. 
* Exclude slot 5 from the retargeting algorithm so the difficulty is not so volatile and does not collapse when the gas prices rise.

## Proposal
The current difficulty retargeting algorithm prevents the network from being open and fair, like the Bitcoin network has proven to be (excluding factors of economic inequality). This proposal would make the network more open and fair for all miners. It also makes it easier for new miners to make decisions about investing in running a node. The proposed changes are:
* Change the difficulty retargeting algorithm to retarget based on slots 1-4. 
* Exclude slot 5 from the retargeting algorithm so the difficulty is not so volatile and does not collapse when the gas prices rise.

# Motivation
Consider the definition of network difficulty originally proposed by Satoshi Nakamoto in the [Bitcoin Whitepaper](https://bitcoin.org/bitcoin.pdf):
> To compensate for increasing hardware speed and varying interest in running nodes over time, the proof-of-work difficulty is determined by a moving average targeting an average number of blocks per hour. If they're generated too fast, the difficulty increases. 

Under the definition, the network difficulty should compenstate for two factors: increasing hardware speed and changing in interest in running a node. The time it takes to generate blocks is a proxy for these two factors.

Currently, the network difficulty for mining Tellor is compenstating for Ethereum gas price. As a result, node operators decrease (increase) their hardware speed based on gas prices rising (falling). This coupling between network difficulty and gas price is shown in the chart below:

![Difficulty and Gas Price](./public/gas_price_difficulty.png)

The difficulty compenstates for gas prices rather than increasing hardware speed and changing in interest in running a node.

## The Impacts of Volatile Difficulty
The current retageting creates two main problems that prevent new miners from joining the network and give established miners an unfair advantage:
1. The difficulty is incredible volatile and makes it difficult to make business decisions around running a node. Return on investment calculations are effectively useless. As a result, Minerstat has delisted Tellor, new miners who find calculators are being mislead, and enterprises view Tellor as a high risk, low reward investment.
2. The official TellorMiner will only mine the 5th slot. New miners who run the TellorMiner will find they're often submitting for a lose, dispite using the profitablilityThreshold feature. Miners using custom mining software are able to mine slots 1-4 within 1 or 2 blocks (~30 seconds) after the previous challenge ends. The 5th slot is left for the newbies. 

# Risk Register
This section includes risks identified should this proposal be implemented:
| Description | Mitigating Factors | Potential Controls |
|-------------|--------------------|--------------------|
| There is a risk that a motivated actor mines slots 1-4 very quickly and leaves slot 5 to the other miners. The miner would greif the system by making the difficulty artificially high. As a result, the time between blocks would rise significantly. | This risk is present in all POW chains, including bitcoin, but becomes less of a risk as there are more miners join and add computer power. This proposal makes the network more open and fair so we can expect more miners to join. Overtime, this risk becomes minimized as the network grows larger because the cost to sustain such an attack would not be worthwhile. Currently, the network is griefed whenever the gas rises and the network handles it fine. | Roll up bonus rewards to the 5th slot when the reward is greater than 5 TRB for the five miners. For example when 10 minute round and reward is 10, the rewards are distributed as (1,1,1,1,6) for slots (1,2,3,4,5) respectively. |





