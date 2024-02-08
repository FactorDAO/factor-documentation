# Governance Voting Model

## Overview

Factor uses a hybrid model for voting on proposals. MainDAO proposals are voted on using the one token, One Token One Vote (OTOV). Proposals related to subDAO funding are decided using Quadratic Voting (QV).

There have been frequent debates on OTOV versus QV. OTOV is a traditional voting system where each token holder has only one vote and the weight of their vote is the same as everyone else's, while QV allows not only for preference of certain choices over others with rank-choice voting, but also takes the “intensity of conviction” into consideration.

### **MainDAO One Token One Vote (OTOV)**

One Token One Vote (OTOV) is a traditional voting system where each $veFCTR holder has only one vote and the weight of their vote is the same as everyone else's. This system does not allow for any customization or intensity of conviction to be weighed, which can lead to a lack of incentive for participation and a disproportionate amount of power given to whales.

#### **Advantages of OTOV**

The simplicity and clarity of OTOV make it easy to understand, meaning it would be less intimidating for stakers who are unfamiliar with complex mathematical functions like quadratic voting. Additionally, because all votes are equal in value, it ensures that all stakeholders have an equal say in governance decisions regardless of their holdings or activity level.

#### **Drawbacks and Risks of OTOV**

The main drawback associated with OTOV is that there can be an imbalance between stakeholders who own large amounts veFCTR compared to those who own small amounts. This lack of balance between whales and smaller holders can result in certain voices being ignored and interests not being represented accurately within the organization.

### **SubDAO Quadratic Voting (QV)**

Quadratic Voting (QV) is a complex yet intuitive voting system that has gained popularity in decentralized autonomous organizations (DAOs), token-based membership and governance. It allows not only for preference of certain choices over others with rank-choice voting, but also for intensity of conviction to be weighed. This can help align incentives, balance power, and encourage voter participation more effectively than one-person/token-one-vote mechanisms.

#### **QV as a Mathematical Formula**

The process involves allocating credits among available options which are then calculated by taking the square root of the allocated credits for each choice. For example, 100 credits applied to one choice would count as 10 votes; 25 credits would be 5 votes; 4 credits would equal 2 votes. The concept of QV can be expressed as the following mathematical formula:

```
➗ V = √C where V is the number of votes and C is the number of credits allocated.
```

#### **Advantages of QV**

QV can protect minority interests from being ignored by an indifferent majority, better balance power among communities with a large spread in voting power and whales, and result in more accurate snapshots of community sentiment when compared to rank choice voting.

For example, let's say there is a DAO with 10 voters. 5 of the voters are whales who own more tokens than the other 5, and these 5 whales prefer option A over option B. In this instance, using OTOV would likely result in option A being chosen because the majority of votes (50%) would come from the whales.

However, with QV each voter can assign weights to their preference for each option based on how strongly they feel about it. This means that even though the whales may have more voting power due to their higher token holdings, the minority interests of those with lower numbers of tokens can still be represented accurately if they allocate enough credits to their preferred choice.

#### **Drawbacks and Risks of QV**

QV may not be as appropriate for elections where there are only two choices, or for instances where simplicity is preferred. Additionally, because quadratic voting considers not just how many credits were allocated to each option but also where those credits came from when calculating votes, it can be particularly vulnerable to Sybil attacks.

#### **What are Sybil Attacks?**

Sybil attacks are a malicious form of attack that can be used to undermine a DAOs integrity and security. In this type of attack, an attacker creates multiple fake identities or “sybils” in order to gain control over the DAOs resources.

By creating these false identities, the attacker can then manipulate voting results, siphon funds away from legitimate users, and even disrupt operations within the organization. Sybil attacks represent one of the greatest threats to DAO governance and must be addressed with robust countermeasures if decentralized organizations are to remain secure and reliable.
