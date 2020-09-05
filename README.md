# YANValue Smart-contracts
#### Bringing True Value to Yield Farming

[Full announcement](https://medium.com/@yan.finance)

YAN is the governance token of YANalue protocol. The project aims to bring the true value of yield farming finance accessible to all users, regardless of whether you are a big whale or small minnow, via its unique features, namely the voting of the inflationary rate of the supply and a referral system with automatic burning done fully on-chain.
- YAN.Finance is a DeFi yield aggregator
- First-ever Vote on-chain Supply Inflation rate to enable farmers to vote on-chain and automatic execution will be made based on the votes counted.
- YAN has a stable-coins pool which allows even small players to join the DeFi Yield Farming. The number of users will then be 100x or more compared to other DeFi Yield Farming Protocol.
- Referral and Burn On-chain to motivate the community who are giving a hand for bringing YAN to the public.
- Last but not least, the separated Elastic Supply Stable-coins vUSD and vETH are great add-on benefits for the farmers and the whole ecosystem later on along the road map.

### Smart contracts comparison with super-classes

[Diff checker: YFV and YAN](https://www.diffchecker.com/xmmWFRAg)

[Diff checker: YFVRewards and YANRewards (Seed Pool)](https://www.diffchecker.com/PT4d1PSC)
 - Seed Pool supports 4 stables coin instead of a single y coin from the original code

[Diff checker: YFVRewards and YAN_Rewards_PoolXXX (Balancer/Uni Pool)](https://www.diffchecker.com/PWyndemv)
 - Removed rewardDistribution
 - notifyRewardAmount() can only call once by owner and reward amount cant be over TOTAL_REWARD

[Diff checker: YAN_Stake and YAN_Stake_v2](https://www.diffchecker.com/ILtq1RZG)
 - Added whitelistedPools (so hackers can't attack via stakeOnBelf by penny amount anymore)
 - Added lowStakeDepositFee, highStakeDepositFee, unlockWithdrawFee (and disable all at the beginning. Will set by governance after VIP-1.1)
 - Set yanInsuranceFund to Governance Multisig Wallet (and move to deployed Insurance Fund contract later)
 - Owner (governance) can set epochReward to 0 to disable the pool with no harm
 - Check if the minter rights (vETH and vUSD) are revoked, and set epochReward to zero with no harm (in checkNextEpoch() modifier)
 - Use the same solidity version uniformly across the contract
 - Optimise gas usage for getReward() method
 - Add governanceRecoverUnsupported for recover any ERC20 sent in mess up
 - Governance can add more reward if needed via addTotalReward() but not more than 10 times
 - Ability to upgrade vUSD and vETH contract (v1 is still experimental, we may need vUSDv2 with rebase() function working soon)

 
**_Staking Deposit/Withdraw Fee system:_**
 - unlockWithdrawFee = 0.1%: stakers will need to pay 0.1% (sent to insurance fund)of amount they want to withdraw if the coin still frozen
 - lowStakeDepositFee = 0.1%: stakers still can stake with low amount but need to pay 0.1% (sent to insurance fund)
 - specially, if lowStakeDepositFee = 10000 -> low amount stakers will not pay anything (rich-men pay tax, not poor-men)
 - highStakeDepositFee = 0.1%: stakers need to pay 0.1% of extra amount more than 90 YAN (sent to insurance fund)
