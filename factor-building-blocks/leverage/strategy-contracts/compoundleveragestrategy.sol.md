# CompoundLeverageStrategy.sol

{% hint style="info" %}
Compound Docs: [https://docs.compound.finance/](https://docs.compound.finance/)
{% endhint %}

## Properties

<table><thead><tr><th width="160">Property</th><th width="97">Type</th><th width="101">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>balancerVault</td><td>address</td><td>public; constant</td><td>The address of the <a href="https://docs.balancer.fi/reference/contracts/deployment-addresses/arbitrum.html#core">Balancer Vault contract</a> (to facilitate flash loans).</td></tr><tr><td>weth</td><td>address</td><td>public; constant</td><td>The address of the <a href="https://arbiscan.io/token/0x82af49447d8a07e3bd95bd0d56f35241523fbab1">WETH token</a>.</td></tr><tr><td>_positionId</td><td>uint256</td><td>private</td><td>The identifier for the strategy position that is maintained by the Factor Leverage Vault.</td></tr><tr><td>_vaultManager</td><td>IERC721</td><td>private</td><td>The address of the Vault Manager contract which facilitates vault admin operations (the underlying Leverage Vault contract in this instance).</td></tr><tr><td>_asset</td><td>IERC20</td><td>private</td><td>The address of the asset token (i.e. collateral and token being levered).</td></tr><tr><td>_debtToken</td><td>IERC20</td><td>private</td><td>The address of the debt token (i.e. borrow asset for flash loan).</td></tr><tr><td>_assetPool</td><td>address</td><td>public</td><td>The address of the <code>asset</code> lending pool.</td></tr><tr><td>_debtPool</td><td>address</td><td>public</td><td>The address of the <code>debt</code> lending pool.</td></tr><tr><td>flMode</td><td>uint8</td><td>private</td><td><p>The flash loan mode used to determine the relevant operations to receive the flash loan:</p><p><code>1</code> = addLeverage<br><code>2</code> = removeLeverage<br><code>3</code> = switchAsset<br><code>4</code> = switchDebt<br><code>5</code> = closeLeverage</p></td></tr></tbody></table>

## Events

### LeverageAdded()

Emitted when leverage is added to the position (i.e. this Leverage Strategy contract).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that was supplied to the lending pool.</td></tr><tr><td>debt</td><td>uint256</td><td>The amount of <code>debt</code> that was taken out as a flash loan denominated in <code>_debtToken</code>.</td></tr></tbody></table>

### LeverageRemoved()

Emitted when leverage is removed from the leveraged position (i.e. this Leverage Strategy contract).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>debt</td><td>uint256</td><td>The amount of <code>debt</code> that was repaid.</td></tr></tbody></table>

### LeverageClosed()

Emitted when the leveraged position is closed (i.e. fully repaid).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>assetBalance</td><td>uint256</td><td>The amount of <code>asset</code> that was returned after closing the position.</td></tr><tr><td>debtBalance</td><td>uint256</td><td>The amount of <code>debt</code> that was returned after closing the position.</td></tr></tbody></table>

### AssetSwitched()

Emitted when the underlying collateral asset for the leveraged position is switched.

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>newAsset</td><td>address</td><td>The address of the token used to collateralize the newly switched leverage position.</td></tr><tr><td>balance</td><td>uint256</td><td>The amount of <code>newAsset</code> that was collateralized.</td></tr></tbody></table>

### Withdraw()

Emitted when `asset` is withdrawn from the Compound lending pool.

#### Arguments

<table><thead><tr><th width="138">Argument</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> withdrawn from the Compound lending pool.</td></tr></tbody></table>

### Repay()

Emitted when the Compound lending pool `debt` is repaid.

#### Arguments

<table><thead><tr><th width="138">Argument</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> that was repaid.</td></tr></tbody></table>

### Supply()

Emitted when `asset` is supplied to the Compound lending pool.

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> supplied to the Compound lending pool.</td></tr></tbody></table>

### Borrow()

Emitted when `debt` is borrowed from the Compound lending pool (which collateralizes the provided `asset`).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> that was borrowed from the Compound lending pool.</td></tr></tbody></table>

### WithdrawTokenInCaseStuck()

Emitted when stuck tokens are withdrawn from the Strategy contract.

#### Arguments

<table><thead><tr><th width="176">Argument</th><th width="122">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenAddress</td><td>address</td><td>The address of the token to be withdrawn.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> withdrawn from the Compound lending pool.</td></tr></tbody></table>

### RewardClaimed()

Emitted when Compound rewards are claimed as COMP tokens and transferred to the `msg.sender` (i.e. user).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of rewards claimed denominated in COMP tokens.</td></tr></tbody></table>

### RewardClaimedSupply()

Emitted when Compound rewards are claimed as `asset` tokens and transferred to the `msg.sender` (i.e. user).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of rewards claimed denominated in COMP tokens.</td></tr></tbody></table>

### RewardClaimedRepay()

Emitted when Compound rewards are claimed as `debt` tokens and transferred to the `msg.sender` (i.e. user).

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of rewards claimed denominated in COMP tokens.</td></tr></tbody></table>

### LeverageChargeFee()

Emitted when a leverage fee is charged.

#### Arguments

<table><thead><tr><th width="169">Argument</th><th width="134">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The leverage fee charged denominated in <code>token</code> passed in <a href="compoundleveragestrategy.sol.md#leveragefeecharge-internal-returns"><code>leverageFeeCharge()</code></a>.</td></tr></tbody></table>

## Constructor

Factor Strategy contracts implements OpenZeppelin's upgradeable contracts design and locks the strategy contract upon initialization to avoid contract takeover by an attacker. More info can be found on [OpenZeppelin Docs](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializing\_the\_implementation\_contract).

## Modifiers

### onlyOwner()

Checks if the `msg.sender` address is equal to the `owner` of the position as maintained by the Leverage Vault contract.

## Methods

### initialize() - `public` `initializer`

Initializes the Strategy contract with the `__positionId` and initial address configurations.

#### Parameters

<table><thead><tr><th width="190">Params</th><th width="102">Type</th><th>Description</th></tr></thead><tbody><tr><td>__positionId</td><td>uint256</td><td>The identifier of the leveraged position as maintained by the underlying Leverage Vault contract.</td></tr><tr><td>_vaultManagerAddress</td><td>address</td><td>The address of the Vault Manager contract (the underlying Leverage Vault contract in this instance).</td></tr><tr><td>_assetAddress</td><td>address</td><td>The address of the Strategy's asset token (i.e. collateral and token being levered).</td></tr><tr><td>_debtAddress</td><td>address</td><td>The address of the Strategy's debt token (i.e. borrow asset for flash loan).</td></tr><tr><td>_assetPoolAddress</td><td>address</td><td>The address of the <code>asset</code> lending pool.</td></tr><tr><td>_debtPoolAddress</td><td>address</td><td>The address of the <code>debt</code> lending pool.</td></tr></tbody></table>

### vaultManager() - `public` `view` `returns`

Returns the address of the Factor Vault Manager contract which contains vault admin functions (e.g. upgrade strategy, set fees, etc.).

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Factor Vault Manager.</td></tr></tbody></table>

### positionId() - `public` `view` `returns`

Returns the position identifier maintained by the underlying Leverage Vault contract. Each strategy implementation (such as this contract) is tied to a `positionId`.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The identifier of the position on the underlying Leverage Vault contract.</td></tr></tbody></table>

### asset() - `public` `view` `returns`

Returns the address of the token configured as the main asset for this leverage Strategy contract (i.e. collateralized asset).

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Strategy's  <code>_asset</code>.</td></tr></tbody></table>

### debtToken() - `public` `view` `returns`

Returns the address of the debt token which is used for taking out a flash loan (i.e. borrow token) for this Strategy contract.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Strategy's <code>_debtToken</code> .</td></tr></tbody></table>

### assetPool() - `public` `view` `returns`

Returns the address of the Compound lending pool where the `_asset` is being collateralized.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Strategy's <code>_assetPool</code>.</td></tr></tbody></table>

### debtPool() - `public` `view` `returns`

Returns the address of the Compound lending pool where the `_debtToken` was borrowed from.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Strategy's  <code>_debtPool</code>.</td></tr></tbody></table>

### assetBalance() - `public` `view` `returns`

Returns the total collateralized balance (i.e. `_asset` supplied) of the Strategy contract that is held by the Compound lending pool.

Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The total <code>_asset</code> supplied to the Compound lending pool.</td></tr></tbody></table>

### debtBalance() - `public` `view` `returns`

Returns the outstanding debt balance (i.e. `_debtToken` borrowed) which the Strategy contract owes to the Compound lending contract.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The total <code>_debtToken</code> that needs to be repaid to the Compound lending pool.</td></tr></tbody></table>

### owner() - `public` `view` `returns`

Returns the address of the `owner` of the leveraged position.

#### Returns

<table><thead><tr><th width="138">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the <code>owner</code> of the position.</td></tr></tbody></table>

### addLeverage() - `external` `payable`

Adds leverage to a position by executing the following:

1. Transfer `asset` from `owner` to the Strategy contract
2. Supply `asset` to the Compound pool
3. If `debt` is specified, executes a flash loan to borrow configured `debt` amount on Balancer vault
4. Balancer vault calls [`receiveFlashLoan()`](compoundleveragestrategy.sol.md#receiveflashloan-external-override) to trigger flash swap and flash loan debt repayment via [`_flAddLeverage()`](compoundleveragestrategy.sol.md#fladdleverage-internal)

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>_asset</code> being supplied.</td></tr><tr><td>debt</td><td>uint256</td><td>The amount of <code>_debtToken</code> to be flash loaned.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="187">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#leverageadded">LeverageAdded()</a></td><td>Emits the results of the leverage addition.</td></tr></tbody></table>

### \_flAddLeverage() - `internal`

An internal function which is meant to be called by the Balancer vault contract which repays the flash loan on Balancer by borrowing `debt` against the new `asset` collateralized amount on Compound.

1. Swap `debt` for `asset` (via [swapBySelf()](compoundleveragestrategy.sol.md#swapbyself-public-returns))
2. Supply newly acquired `asset` to the Compound pool (i.e. increase total collateral value)
3. Borrow `_debtToken` from the Compound pool to repay Balancer flash loan
4. Repay the Balancer flash loan

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td>bytes</td><td>Encoded bytes data which consists of:<br><code>amount</code> = The number of <code>_debtToken</code> that was flash loaned.<br><code>data</code> = The Balancer <code>userData</code>.</td></tr><tr><td>feeAmount</td><td>uint256</td><td>The flash loan fee amount to be repaid denominated in <code>_debtToken</code>.</td></tr></tbody></table>

### removeLeverage() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Removes a specified amount of leverage from the Strategy contract by executing the following:

1. Query the outstanding `debt` on the Compound lending pool
2. Executes a flash loan to borrow `debt` from the Balancer vault equivalent to the outstanding `debt` on the Compound pool
3. Balancer vault calls [`receiveFlashLoan()`](compoundleveragestrategy.sol.md#receiveflashloan-external-override) to trigger flash swap and flash loan debt repayment via [`_flRemoveLeverage()`](compoundleveragestrategy.sol.md#flremoveleverage-internal)
4. Transfer withdrawn `asset` to the `owner`

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> being removed.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#leverageremoved">LeverageRemoved()</a></td><td>Emits the results of the leverage removal.</td></tr></tbody></table>

### \_flRemoveLeverage() - `internal`

An internal function which is meant to be called by the Balancer vault contract which repays the flash loan on Balancer by withdrawing `asset` from the Compound lending pool.

1. Queries the outstanding `debt` on the Compound lending pool
2. Repays all of the outstanding `debt` on Compound&#x20;
3. Withdraws the specified `amount` of `asset` (as per [`removeLeverage()`](compoundleveragestrategy.sol.md#removeleverage-external-payable))
4. Swap the withdrawn `asset` for `debt` (via [swapBySelf()](compoundleveragestrategy.sol.md#swapbyself-public-returns))
5. Calculates the remaining Balancer flash loan `debt` outstanding
6. Borrow the oustanding flash loan `debt` amount (including fees) from Compound lending pool
7. Repay the Balancer flash loan

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td>bytes</td><td>Encoded bytes data which consists of:<br><code>amount</code> = The number of <code>_asset</code> that is being removed from  the Strategy contract.<br><code>data</code> = The Balancer <code>userData</code>.</td></tr><tr><td>feeAmount</td><td>uint256</td><td>The flash loan fee amount to be repaid denominated in <code>_debtToken</code>.</td></tr></tbody></table>

### swapBySelf() - `public` `returns`

Allows the `msg.sender` to conduct a swap via the OpenOcean aggregator.

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenIn</td><td>address</td><td>The address of the token being swapped from.</td></tr><tr><td>tokenOut</td><td>address</td><td>The address of the token being swapped to.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>tokenIn</code> being swapped.</td></tr><tr><td>data</td><td>bytes</td><td>The bytes data which consists of the swap method and params.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="189">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The amount of <code>tokenOut</code> resulting from the swap minus the leverage strategy fees.</td></tr></tbody></table>

### supply() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Enables the `owner` to transfer strategy `asset` from the `msg.sender`(i.e. depositor) to the Strategy contract which is then supplied to the Compound lending pool. The Strategy contract will hold the balance on behalf of the `owner`.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that was used for leverage.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#supply">Supply()</a></td><td>Emits the amount of <code>asset</code> that was supplied.</td></tr></tbody></table>

### leverageFeeCharge() - `internal` `returns`

Charges the fee for the leverage strategy and transfers the fee to the fee recipient. The fee configs are maintained by the Vault Manager contract.

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>token</code> that was used for leverage.</td></tr><tr><td>token</td><td>address</td><td>The token which will be collected as fees (i.e. the <code>tokenOut</code> from <a href="compoundleveragestrategy.sol.md#swapbyself-public-returns">swapBySelf()</a>).</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="239">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#leveragechargefee">LeverageChargeFee()</a></td><td>Emits the leverage fee that was charged.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="189">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The leverage fee charged denominated in <code>token</code>.</td></tr></tbody></table>

### borrow() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Enables the `owner` to utilize the collateralized `asset` in the Compound lending pool to borrow the specified `amount` of `debt`. The `debt` is transferred to the `msg.owner` (i.e. `owner`) with the Strategy contract holding the debt on behalf of the `owner`.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> to be borrowed.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#borrow">Borrow()</a></td><td>Emits the amount of <code>debt</code> that was borrowed.</td></tr></tbody></table>

### repay() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Enables the `owner` to repay a specified `amount` of the `debt` for a borrow position on the Compound lending pool. The `debt` is repaid on behalf of the Strategy contract which holds the `owner`'s debt obligations.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> to be repaid.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#repay">Repay()</a></td><td>Emits the amount of <code>debt</code> that was repaid.</td></tr></tbody></table>

### withdraw() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Enables the `owner` to withdraw a specified `amount` of `asset` from the Compound lending pool. The Strategy contract executes the withdrawal as it holds deposit balance on behalf of the `owner`. The corresponding `amount` of `asset` is transferred to the `owner` address.

Note that due to accrued fees to the iToken, the amount returned by the Compound lending pool might be higher than the given `amount`. In such cases, the higher of the expected amount or final amount is returned to the `owner`.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> to be withdrawn.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="241">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#withdraw">Withdraw()</a></td><td>Emits the amount of <code>asset</code> that was withdrawn.</td></tr></tbody></table>

### switchAsset() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Switches the position's underlying `asset` to a newly specified `newAsset` token.

1. Query the outstanding `debt` on the Compound lending pool
2. Executes a flash loan to borrow `debt` from the Balancer vault equivalent to the outstanding debt on the Compound vault
3. Balancer vault calls [`receiveFlashLoan()`](compoundleveragestrategy.sol.md#receiveflashloan-external-override) to trigger flash swap and flash loan debt repayment via [`_flSwitchAsset()`](compoundleveragestrategy.sol.md#flswitchasset-internal)

{% hint style="info" %}
**Allowed New Asset Tokens**

The `newAsset` address must have been registered by the Vault Manager. The list of approved debt tokens is maintained by the Leverage Vault contract.
{% endhint %}

{% hint style="info" %}
**Amount Validation**

The Factor SDK provides convenience functions for the safe handling of the specified `amount`. By utilizing the Factor SDK, you can avoid spending gas on misconfigured amounts and minimize dust amounts from swaps.&#x20;
{% endhint %}

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>newAsset</td><td>address</td><td>The address of the token which will be switched with the current <code>asset</code>.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of existing <code>asset</code> that is being switched for the <code>newAsset</code>.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

### \_flSwitchAsset() - `internal`

An internal function which is meant to be called by the Balancer vault contract which switches the `asset` collateralizing the leveraged position.

1. Queries the outstanding `debt` on the Compound lending pool
2. Repays all of the outstanding `debt` on Compound
3. Withdraws all of the `asset` from the existing position on Compound
4. Swaps the specified `amount` (per [`switchAsset()`](compoundleveragestrategy.sol.md#switchasset-external-payable)) of the withdrawn `asset` for `newAsset` (via [swapBySelf()](compoundleveragestrategy.sol.md#swapbyself-public-returns))
5. Change the Factor Strategy contract properties to align with the `newAsset`
6. Supply the swapped `newAsset` to the `newAsset` Compound lending pool
7. Borrow the initial `debt` balance from Compound using the `newAsset` as collateral
8. Repay the Balancer flash loan

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td>bytes</td><td>Encoded bytes data which consists of:<br><code>newAsset</code> = The address of the token that is being used as the new collateral<br><code>amount</code> = The number of <code>_asset</code> that is being switched.<br><code>data</code> = The Balancer <code>userData</code>.</td></tr><tr><td>feeAmount</td><td>uint256</td><td>The flash loan fee amount to be repaid denominated in <code>_debtToken</code>.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#assetswitched">AssetSwitched()</a></td><td>Emits the results of the asset switch and new asset balance denominated in <code>newAsset</code>.</td></tr></tbody></table>

### closeLeverage() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Closes the leveraged position and transfers the remaining `asset` and `debt` amounts to the `owner`. If the `asset` `amount` specified is greater than the debt value, the position value will be returned in `debt` tokens.

1. Executes a flash loan to borrow existing `debt` from the Balancer vault equivalent to the outstanding debt on the Compound lending pool
2. Balancer vault calls [`receiveFlashLoan()`](compoundleveragestrategy.sol.md#receiveflashloan-external-override) to trigger flash swap and flash loan debt repayment via [`_flCloseLeverage()`](compoundleveragestrategy.sol.md#flcloseleverage-internal)
3. Transfers the remaining `asset`  and `debt` tokens to the `owner` (i.e. depositor)

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> that will be swapped for <code>debt</code>.</td></tr><tr><td>data</td><td>bytes</td><td>The Balancer <code>userData</code> which in this context is used for pool-specific instructions needed to do the calculations.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#leverageclosed">LeverageClosed()</a></td><td>Emits the results of the leverage position closure.</td></tr></tbody></table>

### \_flCloseLeverage() - `internal`

An internal function which is meant to be called by the Balancer vault contract which switches the `debt` of the leveraged position with a provided `newDebtToken`.

1. Queries the outstanding `debt` on the Compound lending pool
2. Repays all of the outstanding `debt` on Compound
3. Withdraws all of the `asset` from the existing position on Compound
4. Swaps the specified `amount` of `asset` (per [`closeLeverage()`](compoundleveragestrategy.sol.md#closeleverage-external-onlyowner)) for `debt` (via [swapBySelf()](compoundleveragestrategy.sol.md#swapbyself-public-returns))
5. Repay the Balancer flash loan using the acquired `debt`

#### Parameters

<table><thead><tr><th width="138">Params</th><th width="117">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td>bytes</td><td>Encoded bytes data which consists of:<br><code>amount</code> = The number of <code>asset</code> that is swapped for <code>debt</code><br><code>data</code> = The Balancer <code>userData</code>.</td></tr><tr><td>feeAmount</td><td>uint256</td><td>The flash loan fee amount to be repaid denominated in the old <code>debt</code>.</td></tr></tbody></table>

### withdrawTokenInCaseStuck() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Enables the `owner` to withdraw any `tokenAddress` that is stuck in the Strategy contract.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenAddress</td><td>address</td><td>The address of the token to withdraw.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>tokenAddress</code> to be withdrawn.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="278">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#withdrawtokenincasestuck">WithdrawTokenInCaseStuck()</a></td><td>Emits the amount of <code>tokenAddress</code> that was withdrawn as well as the <code>tokenAddress</code>.</td></tr></tbody></table>

### version() - `external` `pure` `returns`

Returns the strategy version which is hardcoded based on contract deployment.

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The Strategy contract version.</td></tr></tbody></table>

### \_authorizeUpgrade() - `internal` `view` `override` [`onlyOnwer`](compoundleveragestrategy.sol.md#onlyowner)

An internal function that is meant to be called by the [UUPSUpgradeable contract](https://docs.openzeppelin.com/contracts/5.x/api/proxy#UUPSUpgradeable) that checks if the new implementation is registered by the Factor Vault Manager.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="201">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>newImplementation</td><td>address</td><td>The address of the proposed Strategy contract.</td></tr></tbody></table>

### receiveFlashLoan() - `external` `override` `nonReentrant`

An external function meant to be called by the Balancer vault contract to check the validity of the vault receiving the flash loan (i.e. can the flash loan be repaid). Reads the configured `flMode` at the time of execution to determine the correct operation to call.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>nonReentrant</td><td>Ensures that there are no nested (reentrant calls). More info on <a href="https://docs.openzeppelin.com/contracts/4.x/api/security#ReentrancyGuard">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="169">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokens</td><td>address[]</td><td>The list of token addresses associated with the flash loan operations.</td></tr><tr><td>amounts</td><td>uint256[]</td><td>The amount of each token in <code>tokens</code> to be used for the flash loan operation. The order of each token amount must correspond with the order of the token address in <code>tokens</code>.</td></tr><tr><td>feeAmounts</td><td>uint256[]</td><td>The flash loan fee amount of each token in <code>tokens</code> to be used for the flash loan operation. The order of each token amount must correspond with the order of the token address in <code>tokens</code>.</td></tr><tr><td>params</td><td>bytes</td><td>The Balancer <code>userData</code> passed in as calldata.</td></tr></tbody></table>

### claimRewards() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Allows the position `owner` to claim Compound rewards in COMP tokens.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="224">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#rewardclaimed">RewardClaimed()</a></td><td>Emits the amount of rewards claimed. Denominated in COMP.</td></tr></tbody></table>

### claimRewardsSupply() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Allows the position `owner` to claim Compound rewards in `asset` tokens.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="223">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amountOutMinimum</td><td>uint256</td><td>The minimum amount of <code>asset</code> received from the claim else the transaction reverts.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="242">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#rewardclaimedsupply">RewardClaimedSupply()</a></td><td>Emits the amount of rewards claimed. Denominated in COMP.</td></tr></tbody></table>

### claimRewardsRepay() - `external` [`onlyOwner`](compoundleveragestrategy.sol.md#onlyowner)

Allows the position `owner` to claim Compound rewards in `debt` tokens.

#### Modifiers

<table><thead><tr><th width="220">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>onlyOwner</td><td>Ensures that only the specified <code>owner</code> of the contract is able to execute administrative tasks. More info on <a href="https://docs.openzeppelin.com/contracts/5.x/api/access#Ownable-onlyOwner--">OpenZeppelin Docs</a>.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="223">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>amountOutMinimum</td><td>uint256</td><td>The minimum amount of <code>debt</code> received from the claim else the transaction reverts.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="242">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="compoundleveragestrategy.sol.md#rewardclaimedrepay">RewardClaimedRepay()</a></td><td>Emits the amount of rewards claimed. Denominated in COMP.</td></tr></tbody></table>
