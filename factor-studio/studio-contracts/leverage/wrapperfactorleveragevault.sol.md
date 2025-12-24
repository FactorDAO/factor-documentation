# WrapperFactorLeverageVault.sol

{% hint style="info" %}
**Contract Overview**

`WrapperFactorLeverageVault.sol` functions as a wrapper contract for `FactorLeverageVault.sol` thereby enabling vault depositors to benefit from various Factor reward distribution mechanisms such as [Factor Scale](../../../governance/factor-scale/) and [Factor Boost](../../../governance/factor-boost/).

By implementing a wrapper, users can stake their liquidity by locking underlying Leverage Vault (i.e. `ERC20Augmented`) shares in the wrapper contract. This staked amount will then dictate their gauge voting power as well as accrued rewards.

The vault implements [OpenZeppelin's upgradeable proxy pattern](https://docs.openzeppelin.com/contracts/5.x/api/proxy).&#x20;
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="182">Property</th><th width="133">Type</th><th width="100">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>stakedNFT</td><td>mapping(uint256 => address)</td><td>public</td><td>A mapping of the wrapper vault NFT id to the owner address.</td></tr><tr><td>snapshotBalance</td><td>mapping(uint256 => uint256)</td><td>public</td><td>A snapshot  that maps the <code>positionID</code> with the  <code>ERC20Augmented</code> token balances(which represent underlying Leverage Vault tokens).</td></tr><tr><td>factorLeverageVaultAddress</td><td>address</td><td>public</td><td>The address of the underlying Leverage Vault which this contract wraps.</td></tr><tr><td>allowedAsset</td><td>address</td><td>public</td><td>The address of the Strategy <code>asset</code> which the Wrapper Vault contract supports.</td></tr><tr><td>allowedDebt</td><td>address</td><td>public</td><td>The address of the Strategy <code>debt</code> which the Wrapper Vault contract supports.</td></tr></tbody></table>

## Events

### LeverageAdded()

Emitted when leverage is added to a position.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that was added to the position.</td></tr><tr><td>debt</td><td>uint256</td><td>The amount of <code>debt</code> that was borrowed to open the leverage position.</td></tr></tbody></table>

### LeverageRemoved()

Emitted when leverage is removed from a position.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that was removed from the leveraged position and returned to the owner.</td></tr></tbody></table>

### LeverageClosed()

Emitted when a leveraged position is closed and all of the related `asset` and `debt` is returned to the owner.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>assetBalance</td><td>uint256</td><td>The remaining amount of <code>asset</code> in the Strategy contract after the leveraged position is closed.</td></tr><tr><td>debtBalance</td><td>uint256</td><td>The remaining amount of <code>debt</code> in the Strategy contract after the leveraged position is closed.</td></tr></tbody></table>

### Stake()

Emitted when underlying vault tokens are staked into the wrapper vault contract.

#### Arguments

<table><thead><tr><th width="145">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies the position from the underlying Leverage Vault that was staked into the Wrapper contract.</td></tr></tbody></table>

### CreatePosition()

Emitted when a new position is created on the underlying Leverage Vault contract.

#### Arguments

<table><thead><tr><th width="145">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies the position that was created in underlying Leverage Vault.</td></tr><tr><td>vault</td><td>address</td><td>The address of the Strategy contract implemented for the position.</td></tr></tbody></table>

### UnStake()

Emitted when underlying vault tokens are unstaked and removed from the wrapper vault contract.

#### Arguments

<table><thead><tr><th width="145">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies the position from the underlying Leverage Vault that was unstaked from the Wrapper contract.</td></tr></tbody></table>

### Withdraw()

Emitted when `asset` is withdrawn from a position.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The number of <code>asset</code> that is withdrawn from the position.</td></tr></tbody></table>

### UpdateBalance()

Emitted when the Wrapper Vault contract balance for a position is updated with the Strategy contract balances.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>oldBalance</td><td>uint256</td><td>The previous debt balance of the position on the Wrapper Vault contract.</td></tr><tr><td>newBalance</td><td>uint256</td><td>Thew updated balance of the poisiotn on the Wrapper Vault contract.</td></tr></tbody></table>

### Repay()

Emitted when the `positionId`'s debt is repaid.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> that was repaid.</td></tr></tbody></table>

### Supply()

Emitted when `asset` is supplied to the Strategy contract.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> supplied to the position. </td></tr></tbody></table>

### UpgradeStrategy()

Emitted when the Strategy implementation contract for the `positionId` is upgraded.

#### Arguments

<table><thead><tr><th width="182">Argument</th><th width="121">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionStrategy</td><td>address</td><td>The address of the strategy contract that was previously implemented by the position.</td></tr><tr><td>positionId</td><td>uint256</td><td>The position identifier that uniquely identifies every position on the underlying Leverage Vault.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the new Strategy contract implemented by the position.</td></tr></tbody></table>

## Structs

### InitParams

A struct that defines the Leverage Vault initalization format.



<table><thead><tr><th width="199">Variables</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>_name</td><td>string</td><td>The name of the vault. This will be used as the name of the <code>ERC20Augmented</code> token representing vault shares.</td></tr><tr><td>_symbol</td><td>string</td><td>The symbol of the vault. This will be used as the symbol of the <code>ERC20Augmented</code> token representing vault shares.</td></tr><tr><td>_allowedAsset</td><td>address</td><td>The address of the underlying vault <code>asset</code> that can be facilitated by the wrapper contract.</td></tr><tr><td>_allowedDebt</td><td>address</td><td>The address of the underlying vault <code>debt</code> that can be facilitated by the wrapper contract.</td></tr><tr><td>_factorLeverageVaultAddress</td><td>address</td><td>The address of the underlying Factor vault that is wrapped by this contract (i.e. deployed <a href="/broken/pages/5drOVuWJQozmQfCm4DE7"><code>FactorVault.sol</code></a> address)</td></tr><tr><td>_veFctr</td><td>address</td><td>The address of the <a href="../../../governance/fctr-token/#vefctr">veFCTR</a> contract.</td></tr><tr><td>_gaugeController</td><td>address</td><td>The address of the Factor Gauge Controller contract.</td></tr><tr><td>_boostController</td><td>address</td><td>The address of the <a href="../../../governance/factor-boost/">Factor Boost</a> Controller contract.</td></tr><tr><td>_rewardDuration</td><td>uint256</td><td>The reward duration which the <a href="../../../governance/factor-boost/">Factor Boost</a> rewards for this wrapper vault will be initalized with.</td></tr></tbody></table>

## Constructor

Factor Vault contracts implements OpenZeppelin's upgradeable contracts design and locks the Vault contract upon initialization to avoid contract takeover by an attacker. More info can be found on [OpenZeppelin Docs](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializing_the_implementation_contract).

## Methods

### initialize() - `public` `initializer`&#x20;

The contract initialization function which initializes the contract with the  underlying Leverage Vault configurations as well as the Factor ecosystem contract addresses.&#x20;

The ERC20 and ERC721 token contracts that respectively represent Wrapper Vault shares and Wrapper Position NFTs are initialized as part of this function. The related Factor Gauge and [Factor Boost ](../../../governance/factor-boost/contracts/factor-boost-contract-addresses.md)contracts are also initialized for the Leverage Vault.

#### Parameters

<table><thead><tr><th width="197">Params</th><th width="126">Type</th><th>Description</th></tr></thead><tbody><tr><td>initParams</td><td><a href="wrapperfactorleveragevault.sol.md#initparams">InitParams</a></td><td>Memory data that contains the initialization data for the wrapper vault.</td></tr></tbody></table>

### transferFrom() - `public` `virtual` `override`

Transfers the position NFT with the specified `id` from the `from` address to the `to` address. The caller of this function must either be the owner of the NFT or  have the necessary allowances to spend the owner's NFT.

The underlying debt of the position NFT is also transferred to the `to` address.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>from</td><td>address</td><td>The address of the NFT owner from which to debit the position NFT.</td></tr><tr><td>to</td><td>address</td><td>The address to transfer the position NFT to.</td></tr><tr><td>id</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to be transferred.</td></tr></tbody></table>

### stakePosition() - `external` `nonReentrant`

Stakes the provided `positionId` NFT in the wrapper contract by transferring it from the `msg.sender` to the Wrapper Vault contract address. Wrapper Vault NFTs representing the underlying Leverage Vault position are minted to the `msg.sender`.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to be staked.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#stake">Stake()</a></td><td>Emits the identifier of the position that was staked.</td></tr></tbody></table>

### createPosition() - `external` `nonReentrant` `returns`

Creates a new position representing the configurations of a depositor's position in the underlying Leverage Vault (only consists of the position structure and not actual liquidity).&#x20;

To create the position, a new instance of the `strategyImplementation` contract is initalized with every newly created position ID for this vault.

The underlying Leverage Vault position NFT is minted to the Wrapper Vault contract while a newly created Wrapper Vault position NFT is sent to the Wrapper Vault contract `msg.sender`.

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The newly created position ID.</td></tr><tr><td>strategy</td><td>The address of the newly deployed strategy contract which was implemented for the position.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#createposition">CreatePosition()</a></td><td>Emits the newly created position ID and the implemented strategy address.</td></tr></tbody></table>

### unstakePosition() - `external` `nonReentrant`

Allows the owner the staked Wrapper Vault position to unstake their position from the Wrapper Vault contract (i.e. underlying Leverage Vault position NFT is transferred back to the staker).

The Wrapper Vault position NFT is burned with the corresponding wrapper virtual debt balance (represented by the \`ERC20Augmented) is also destroyed.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to be unstaked.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#unstake">UnStake()</a></td><td>Emits the identifier of the position that was unstaked.</td></tr></tbody></table>

### addLeverage() - `external` `nonReentrant`

Allows the position `owner` to add leverage towards their specified `positionId`.

* Transfers the specified `amount` of `asset` from `msg.sender` (i.e. user) to the Wrapper Vault contract
* Adds leverage to the provided `positionId` by calling `addLeverage()` from the implemented Strategy contract
* Updates the Wrapper Vault balances which is being tracked via the `ERC20Augmented` token
* Updates the the `positionId` debt balance on the Wrapper Vault contract

#### Parameters

<table><thead><tr><th width="139">Params</th><th width="125">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to add leverage to.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> to supply as collateral for the loan.</td></tr><tr><td>debt</td><td>uint256</td><td>The amount of <code>debt</code> to flash loan to increase position leverage.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#leverageadded">LeverageAdded()</a></td><td>Emits the results of the leverage addition.</td></tr></tbody></table>

### supply() - `external` `nonReentrant`

Allows the position `owner` to supply a specified `amount` of `asset` to the Wrapper Vault contract which  is then supplied to the Strategy lending pool.

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to which <code>asset</code> is being supplied.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> to be supplied as collateral for the position.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#supply">Supply()</a></td><td>Emits the result of the supply which includes the address of the corresponding Strategy contract.</td></tr></tbody></table>

### removeLeverage() - `external` `nonReentrant`

Allows the position `owner` to remove leverage from their specified `positionId`.

* Removes the specified `amount` of `asset` by calling `removeLeverage()` from the implemented Strategy contract
* Transfer the removed `asset` amount to the `msg.sender` (i.e. user)
* Updates the Wrapper Vault balances which is being tracked via the `ERC20Augmented` token
* Updates the the `positionId` debt balance on the Wrapper Vault contract

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to remove leverage from.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> being removed.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#leverageremoved">LeverageRemoved()</a></td><td>Emits the results of the leverage removal.</td></tr></tbody></table>

### \_operationAugmented() - `internal`

An internal function that facilitates the burning and minting of `ERC20Augmented` tokens representing the number of underlying Leverage Vault tokens in the Wrapper Vault contract.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>newBalance</td><td>uint256</td><td>The updated balance maintained by the Wrapper Vault contract.</td></tr><tr><td>oldBalance</td><td>uint256</td><td>The previous virtual balance maintained by the Wrapper Vault contract.</td></tr></tbody></table>

### updateBalance() - `external` `nonReentrant`

Allows the position `owner` to synchronize debt balances between the Wrapper Vault contract and the Strategy contract. The debt balance on the Strategy contract is used to update the Wrapper Vault contract.

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT whose balance is to be synced.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#updatebalance">UpdateBalance()</a></td><td>Emits the results of the debt balance update.</td></tr></tbody></table>

### closeLeverage() - `external` `onlyOwner`

Allows the position `owner` to close their specified `positionId` and receive the underlying `asset` and `debt`. If the `asset` `amount` specified is greater than the debt value, the position value will be returned in `debt` tokens.

* Closes the `positionId` by calling `closeLeverage()` from the implemented Strategy contract
* Transfers the `asset` and `debt` from the closed position to the `msg.sender` (i.e. owner)&#x20;
* Updates the Wrapper Vault balances which is being tracked via the `ERC20Augmented` token
* Updates the the `positionId` debt balance on the Wrapper Vault contract

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to be closed.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that will be swapped for <code>debt</code>.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#leverageclosed">LeverageClosed()</a></td><td>Emits the results of the leverage position closure.</td></tr></tbody></table>

### withdraw() - `external` `nonReentrant`

Allows the position `owner` to withdraw a specified `amount` of their collateralized `asset` from the Strategy contract . The withdrawn `asset` is credited to the `msg.sender` (i.e. user) address.

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT to withdraw from.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that will be withdrawn.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#withdraw">Withdraw()</a></td><td>Emits the withdrawal details.</td></tr></tbody></table>

### repay() - `external` [`onlyOwner`](wrapperfactorleveragevault.sol.md#onlyowner)

Allows the position `owner` to repay a specified `amount` of their `positionId`'s `debt` on the Strategy contract. The `ERC20Augmented` balances are burned with the Wrapper Vault contract balances being updated.

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier of the underlying Leverage Vault position NFT whose debt is being repaid.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> to be repaid.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#repay">Repay()</a></td><td>Emits the amount of <code>debt</code> that was repaid as well as the Strategy contract address.</td></tr></tbody></table>

### \_beforeTokenTransfer() - `internal` `override`

An internal function that updates [Factor Scale](../../../governance/factor-scale/) and [Factor Boost](../../../governance/factor-boost/) rewards prior to a related token transfer.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>from</td><td>address</td><td>The address of the <code>msg.sender</code>.</td></tr><tr><td>to</td><td>address</td><td>The address of the token receiver.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of tokens to be transferred.</td></tr></tbody></table>

### \_afterTokenTransfer() - `internal` `override`

An internal function that updates the `msg.sender`'s active balance in the gauge.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>from</td><td>address</td><td>The address of the <code>msg.sender</code>.</td></tr><tr><td>to</td><td>address</td><td>The address of the token receiver.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of tokens to be transferred.</td></tr></tbody></table>

### \_stakedBalance() - `internal` `view` `override`

Returns the amount of `ERC20Augmented` tokens (i.e. underlying Leverage Vault tokens) that a `user` (i.e. staker) has staked into the Wrapper Vault contract.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>user</td><td>address</td><td>The address of the <code>user</code>.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The amount of underlying Leverage Vault tokens staked.</td></tr></tbody></table>

### \_totalStaked() - `internal` `view` `override`

Returns the total amount of underlying vault tokens held by (i.e. staked into) the Wrapper Vault contract.

#### Returns

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The total amount of underlying Leverage Vault tokens held by the wrapper vault contract.</td></tr></tbody></table>

### tokenURI() - `public` `view` `virtual` `override` `returns`

Returns the encoded Uniform Resource Identifier (URI) of the position `id` that is being queried.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The <code>positionId</code> of the position whose URI data is being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The encoded URI for the token representing the position in the leverage vault.</td></tr></tbody></table>

### redeemRewards() - `public` `nonReentrant` `returns`

Enables stakers to claim their accrued [Factor Scale](../../../governance/factor-scale/) rewards.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>user</td><td>address</td><td>The address of the user that has accured rewards.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256[]</td><td>An array containing the amount of reward tokens redeemed, in the same order as <a href="wrapperfactorleveragevault.sol.md#getrewardtokens-external-view-returns"><code>getRewardTokens()</code></a>.</td></tr></tbody></table>

### getRewardTokens() - `external` `view` `returns`

Returns the ordered list of reward tokens that have accrued to the user.&#x20;

#### Returns

<table><thead><tr><th width="176">Type</th><th>Description</th></tr></thead><tbody><tr><td>address[]</td><td>An array containing the amount of reward tokens redeemed.</td></tr></tbody></table>

### claimRewards() - `external` `nonReentrant`

Allows the position `owner` to claim the Strategy rewards which has accrued to their `positionId`. The reward tokens are transferred to the `msg.sender`'s (i.e. `owner`) address.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>address</td><td>The identifier of the underlying Leverage Vault position NFT whose debt is being repaid.</td></tr><tr><td>token</td><td>address</td><td>The address of the token receiver.</td></tr></tbody></table>

### upgradeStrategy() - `public`

Enables the position `owner` to update the underlying Leverage Vault's `strategyImplementation` with a newly provided `upgradeImplemantation` address.

#### Parameters

<table><thead><tr><th width="145">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>address</td><td>The identifier of the underlying Leverage Vault position NFT whos estrategy implementation is being updated.</td></tr><tr><td>upgradeImplemantation</td><td>address</td><td>The address of the new Strategy implementation contract.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="249">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="wrapperfactorleveragevault.sol.md#upgradestrategy">UpgradeStrategy()</a></td><td>Emits the address of the newly implemented strategy.</td></tr></tbody></table>
