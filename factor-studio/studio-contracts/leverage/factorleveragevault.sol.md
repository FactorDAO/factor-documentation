# FactorLeverageVault.sol

{% hint style="info" %}
**Contract Overview**

`FactorLeverageVault.sol` manages the Leverage Vault configurations as well as the positions created via this vault. Positions in the vault are represented via a ERC721 NFT which is uniquely identified via the `positionId`.&#x20;

All positions created on this vault share the same configurations such as `asset` and `debt` tokens/pools as well as fee configurations. Each `positionId` will implement strategy logic via a Strategy contract that is tied to the specific position NFT.

The vault implements [OpenZeppelin's upgradeable proxy pattern](https://docs.openzeppelin.com/contracts/5.x/api/proxy). The vault `owner` is able to propose a new strategy contract implementation for the vault and upgrade the vault's strategy implementation if the strategy has been registered.
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="205">Property</th><th width="103">Type</th><th width="112">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>FEE_SCALE</td><td>uint256</td><td>public; constant</td><td>The scale denominator for the fees. Default is <code>1e18</code>.</td></tr><tr><td>leverageFee</td><td>uint256</td><td>public</td><td>The fee that is charged on the leverage portion whenever a position's leverage is changed.</td></tr><tr><td>claimRewardFee</td><td>uint256</td><td>public</td><td>The fee that is charged on the harvested rewards whenever the accrued position rewards are claimed.</td></tr><tr><td>feeRecipient</td><td>address</td><td>public</td><td>The address of the fee recipient. </td></tr><tr><td>strategyImplementation</td><td>address</td><td>public</td><td>The address of the strategy contract that is implemented for this leverage vault.</td></tr><tr><td>factorLeverageDescriptor</td><td>address</td><td>public</td><td>The address of the leverage vault descriptor which facilitates sharing of encoded leverage vault token data (i.e. URI).</td></tr><tr><td>currentPositionId</td><td>uint256</td><td>public</td><td>An integer which is used to track the positions created via this Leverage Vault. Incremented by 1 with every new position created (i.e. always 1 more than the last created positionId).</td></tr><tr><td>positions</td><td>mapping(uint256 => address)</td><td>public</td><td>Maps the position to their implemented strategy contract address.</td></tr><tr><td>assets</td><td>mapping(address => address)</td><td>public</td><td>Maps the <code>asset</code> to the corresponding lending pool contract address.</td></tr><tr><td>debts</td><td>mapping(address => address)</td><td>public</td><td>Maps the <code>debt</code> to the corresponding lending pool contract address.</td></tr><tr><td>isUpgrade</td><td>mapping(address => mapping(address => bool))</td><td>internal</td><td>A nested mapping of strategy contracts which have been registered as eligible by the Vault Manager <code>owner</code>. Enables registered proposed strategies to be implemented.</td></tr></tbody></table>

## Events

### PositionCreated()

Emitted when a new position is created on the Leverage Vault.

#### Arguments

<table><thead><tr><th width="159">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the new position that was created.</td></tr><tr><td>vault</td><td>address</td><td>The address of the strategy implementation that was deployed with the newly created position.</td></tr></tbody></table>

### AssetChanged()

Emitted when the lending pool tied to the Leverage Vault `asset` is changed by the `owner` of the vault.

#### Arguments

<table><thead><tr><th width="159">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td>address</td><td>The address of the Leverage Vault <code>asset</code>.</td></tr><tr><td>pool</td><td>address</td><td>The address of the newly configured lending pool tied to the Leverage Vault's <code>asset</code>.</td></tr></tbody></table>

### DebtChanged()

Emitted when the lending pool tied to the Leverage Vault `debt` is changed by the `owner` of the vault.

#### Arguments

<table><thead><tr><th width="159">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td>address</td><td>The address of the Leverage Vault <code>debt</code>.</td></tr><tr><td>pool</td><td>address</td><td>The address of the newly configured lending pool tied to the Leverage Vault's <code>debt</code>.</td></tr></tbody></table>

### UpgradeRegistered()

Emitted when a proposed strategy implementation address is registered by the Leverage Vault `owner`.

#### Arguments

<table><thead><tr><th width="172">Argument</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImpl</td><td>address</td><td>The address of the existing strategy contract that is implemented by the vault.</td></tr><tr><td>upgradeImpl</td><td>address</td><td>The address of the proposed strategy contract to be implemented.</td></tr></tbody></table>

### UpgradeRemoved()

Emitted when a proposed strategy implementation is removed (i.e. deregistered)  from `isUpgrade` by the Leverage Vault `owner`.

#### Arguments

<table><thead><tr><th width="172">Argument</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImpl</td><td>address</td><td>The address of the existing strategy contract that is implemented by the vault.</td></tr><tr><td>upgradeImpl</td><td>address</td><td>The address of the proposed strategy contract to be implemented.</td></tr></tbody></table>

### DescriptorChanged()

Emitted when the leverage descriptor contract address is changed by the Leverage Vault owner.

#### Arguments

<table><thead><tr><th width="221">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>descriptor</td><td>address</td><td>The address of the <code>msg.sender</code> (i.e. depositor) that deposited into the vault.</td></tr></tbody></table>

## Constructor

Factor Vault contracts implements OpenZeppelin's upgradeable contracts design and locks the Vault contract upon initialization to avoid contract takeover by an attacker. More info can be found on [OpenZeppelin Docs](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializing\_the\_implementation\_contract).

## Methods

### initialize() - `public` `initializer`&#x20;

The contract initialization function which initializes the contract with the vault params and initial fee scale. Defaults the fee recipient to the `msg.sender` (i.e. leverage vault creator).&#x20;

#### Parameters

<table><thead><tr><th width="197">Params</th><th width="126">Type</th><th>Description</th></tr></thead><tbody><tr><td>_strategyImplementation</td><td>address</td><td>The address of the strategy contract to be implemented for this leverage vault.</td></tr><tr><td>_factorLeverageDescriptor</td><td>address</td><td>The address of the leverage vault descriptor that will describe the leverage vault token.</td></tr><tr><td>_name</td><td>string</td><td>The name of the leverage vault collection. Used as the NFT collection name.</td></tr><tr><td>_symbol</td><td>string</td><td>The symbol of the leverage vault collection. Used as the NFT collection symbol.</td></tr></tbody></table>

### createPosition() - `external` `returns`

Creates a new position representing the configurations of a depositor's position in the leverage vault (only consists of the position structure and not actual liquidity).&#x20;

To create the position, a new instance of the `strategyImplementation` contract is initalized with every newly created position ID for this vault.

The newly created position NFT is sent to the `msg.sender`.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>asset</td><td>address</td><td>The address of the token used to collateralize the position.</td></tr><tr><td>debt</td><td>address</td><td>The address of the debt token to be borrowed for leverage purposes.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The new <code>currentPositionId</code> after a position is created (i.e. newly created position ID plus 1).</td></tr><tr><td>address</td><td>The address of the newly deployed strategy contract which was implemented for the position.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#positioncreated">PositionCreated()</a></td><td>Emits the <code>currentPositionId</code> and the implemented strategy address.</td></tr></tbody></table>

### updateAsset() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the `owner` of the leverage vault contract to change the address of the lending pool tied to the vault's `asset`.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>asset</td><td>address</td><td>The address of the token used to collateralize the position.</td></tr><tr><td>pool</td><td>address</td><td>The address of the <code>asset</code> lending pool to be changed to.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="192">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#assetchanged">AssetChaged()</a></td><td>Emits the address of the newly configured lending pool tied to the Leverage Vault's <code>asset</code>.</td></tr></tbody></table>

### updateDebt() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the `owner` of the leverage vault contract to change the address of the lending pool tied to the vault's `debt`.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>debt</td><td>address</td><td>The address of the debt token to be borrowed for leverage purposes.</td></tr><tr><td>pool</td><td>address</td><td>The address of the <code>debt</code> lending pool to be changed to.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="207">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#debtchanged">DebtChanged()</a></td><td>Emits the address of the newly configured lending pool tied to the Leverage Vault's <code>debt</code>.</td></tr></tbody></table>

### burnPosition() - `external`

Allows the owner of the position to burn (i.e. removes) their zero balance positions.

#### Returns

<table><thead><tr><th width="208">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>The ID of the position to be burned.</td></tr></tbody></table>

### tokenURI() - `public` `view` `override` `returns`

Returns the encoded Uniform Resource Identifier (URI) of the position `id` that is being queried.

#### Parameters

<table><thead><tr><th width="156">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The <code>positionId</code> of the position whose URI data is being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The encoded URI for the token representing the position in the leverage vault.</td></tr></tbody></table>

### setDescriptor() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the owner of the leverage vault to change the address of the `factorLeverageDescriptor`.

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#descriptorchanged">DescriptorChanged()</a></td><td>Emits the address of the new leverage vault descriptor.</td></tr></tbody></table>

### isRegisteredUpgrade() - `external` `view` `returns`

Checks whether the upgrade from `baseImplementation` to `upgradeImplementation` has been registered by the Leverage Vault `owner`.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="99">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="208">Type</th><th>Description</th></tr></thead><tbody><tr><td>bool</td><td><code>true</code> = Proposed strategy has been registered by <code>owner</code>.<br><code>false</code> = Proposed strategy has not been registered by <code>owner</code>.</td></tr></tbody></table>

### registerUpgrade() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to register a strategy upgrade from `baseImplementation` to `upgradeImplementation`. Proposed strategies must be registered before it can be implemented.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#upgraderegistered">UpgradeRegistered()</a></td><td>Emits the registered strategy upgrade proposal.</td></tr></tbody></table>

### removeUpgrade() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to remove a previously registered strategy upgrade proposal from `isUpgrade`.

#### Parameters

<table><thead><tr><th width="227">Params</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorleveragevault.sol.md#upgraderemoved">UpgradeRemoved()</a></td><td>Emits the strategy upgrade proposal that was removed.</td></tr></tbody></table>

### updateImplementation() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to update the `strategyImplementation` with a newly provided address.

#### Parameters

<table><thead><tr><th width="244">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>_strategyImplementation</td><td>address</td><td>The address of the new strategy implementation contract.</td></tr></tbody></table>

### setFeeRecipient() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to update the `feeRecipient` with a newly provided address.

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>recipient</td><td>address</td><td>The address that receives the leverage fees.</td></tr></tbody></table>

### setLeverageFee() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to update the `leverageFee` that is charged on the leverage portion whenever a position's leverage is changed.

The `newFee` provided is scaled by the Leverage Vault contract's `FEE_SCALE` which is defaulted to `1e18` on vault initialization. That is, a `newFee` of `1e16` is equivalent to 1% fee (i.e. `1e16`/`1e18`).

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>newFee</td><td>uint256</td><td>The amount of leverage fee to charge. </td></tr></tbody></table>

### setClaimRewardFee() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the Leverage Vault `owner` to update the `claimRewardFee` that is charged on the harvested rewards whenever the accrued position rewards are claimed.

The `newFee` provided is scaled by the Leverage Vault contract's `FEE_SCALE` which is defaulted to `1e18` on vault initialization. That is, a `newFee` of `1e16` is equivalent to 1% fee (i.e. `1e16`/`1e18`).

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>newFee</td><td>uint256</td><td>The amount of claim reward fee to charge. </td></tr></tbody></table>

### version() - `external` `pure` `returns`

Returns the Leverage Vault version which is hardcoded based on contract deployment.

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The Leverage Vault version.</td></tr></tbody></table>

### \_increaseBalance() - `internal` `virtual` `override`

An internal function that overrides the ERC721 [\_increaseBalance()](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721#ERC721-\_increaseBalance-address-uint128-) function meant to increase the number of NFT collection tokens held by the `account`.

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>account</td><td>address</td><td>The address of the position holder.</td></tr><tr><td>amount</td><td>uint128</td><td>The amount of Leverage Vault token count to be added to the existing <code>account</code> balances.</td></tr></tbody></table>

### \_update() - `internal` `virtual` `override` `returns`

An internal function that overrides the ERC721  [\_update()](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721#ERC721-\_update-address-uint256-address-) function meant to update the owner of the `tokenId`.

#### Parameters

<table><thead><tr><th width="152">Params</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>to</td><td>address</td><td>The address to transfer ownership of <code>tokenId</code> to. Mints (or burns) the position NFT if the current owner (or to) is the zero address.</td></tr><tr><td>tokenId</td><td>uint128</td><td>The identifier for the Leverage Vault NFT to be updated.</td></tr><tr><td>auth</td><td>address</td><td>An optional params where passing in a non-zero value checks if the provided address has the rights to transfer the token (i.e. owner or approved).</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the LP Vault NFT (representing the position) before the update.</td></tr></tbody></table>

### supportsInterface() - `public` `view` `override` `returns`

An internal function that overrides the ERC721 [supportsInterface()](https://docs.openzeppelin.com/contracts/2.x/api/introspection#IERC165-supportsInterface-bytes4-) function that returns `true` if this Leverage Vault contract implements the interface defined by `interfaceId`.

#### Parameters

<table><thead><tr><th width="152">Params</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>interfaceId</td><td>bytes4</td><td>The encoded bytes data representing the interface being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>bool</td><td><code>true</code> = <code>interfaceId</code> is supported by the Leverage Vault contract<br><code>false</code> = <code>interfaceId</code> is not supported by the Leverage Vault contract</td></tr></tbody></table>
