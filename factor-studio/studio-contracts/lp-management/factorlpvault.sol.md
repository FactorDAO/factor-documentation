# FactorLPVault.sol

{% hint style="info" %}
**Contract Overview**

`FactorLPVault.sol` manages the LP Vault configurations as well as the concentrated liquidity positions created via this vault. Positions in the vault are represented via a ERC721 NFT which is uniquely identified via the `positionId`.&#x20;

The LP Vault builds on top of the Leverage Vault to enable leveraged LP positions thereby significantly amplifying the potential returns. All positions created on this vault share the same initial strategy implementation and LP fees configuration.

The vault implements [OpenZeppelin's upgradeable proxy pattern](https://docs.openzeppelin.com/contracts/5.x/api/proxy). The vault `owner` is able to propose a new strategy contract implementation for the vault and upgrade the vault's strategy implementation if the strategy has been registered.
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="205">Property</th><th width="111">Type</th><th width="112">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>FEE_SCALE</td><td>uint256</td><td>public; constant</td><td>The scale denominator for the fees. Defaulted to <code>1e18</code>.</td></tr><tr><td>changeRangeFee</td><td>uint256</td><td>public</td><td>The fee that is charged on when the position's range is changed.</td></tr><tr><td>compoundFee</td><td>uint256</td><td>public</td><td>The fee that is charged on the harvested rewards whenever the accrued position rewards are claimed.</td></tr><tr><td>feeRecipient</td><td>address</td><td>public</td><td>The address of the fee recipient. </td></tr><tr><td>strategyImplementation</td><td>address</td><td>public</td><td>The address of the strategy contract that is implemented for this LP vault.</td></tr><tr><td>factorLPDescriptor</td><td>address</td><td>public</td><td>The address of the LP vault descriptor which facilitates sharing of encoded LP vault token data (i.e. URI).</td></tr><tr><td>currentPositionId</td><td>uint256</td><td>public</td><td>An integer which is used to track the positions created via this LP Vault. Incremented by 1 with every new position created (i.e. always 1 more than the last created positionId).</td></tr><tr><td>positions</td><td>mapping(uint256 => address)</td><td>public</td><td>Maps the position to their implemented strategy contract address.</td></tr><tr><td>isUpgrade</td><td>mapping(address => mapping(address => bool))</td><td>internal</td><td>A nested mapping of strategy contracts which have been registered as eligible by the Vault Manager <code>owner</code>. Enables registered proposed strategies to be implemented.</td></tr><tr><td>nonces</td><td>mapping(address => uint256)</td><td>public</td><td>An incremental counter which keeps track of the number of positions created by a depositor. Used to generate the  corresponding strategy address.</td></tr><tr><td>allowedLeverageVaults</td><td>mapping(address => bool)</td><td>public</td><td>A mapping of whitelisted leverage vaults which the LP strategy can utilize.</td></tr></tbody></table>

## Events

### PositionCreated()

Emitted when a new position is created on the LP Vault.

#### Arguments

<table><thead><tr><th width="159">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the new position that was created.</td></tr><tr><td>vault</td><td>address</td><td>The address of the strategy implementation that was deployed with the newly created position.</td></tr></tbody></table>

### UpgradeRegistered()

Emitted when a proposed strategy implementation address is registered by the LP Vault `owner`.

#### Arguments

<table><thead><tr><th width="172">Argument</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImpl</td><td>address</td><td>The address of the existing strategy contract that is implemented by the vault.</td></tr><tr><td>upgradeImpl</td><td>address</td><td>The address of the proposed strategy contract to be implemented.</td></tr></tbody></table>

### UpgradeRemoved()

Emitted when a proposed strategy implementation is removed from (i.e. deregistered) `isUpgrade` by the LP Vault `owner`.

#### Arguments

<table><thead><tr><th width="172">Argument</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImpl</td><td>address</td><td>The address of the existing strategy contract that is implemented by the vault.</td></tr><tr><td>upgradeImpl</td><td>address</td><td>The address of the proposed strategy contract to be implemented.</td></tr></tbody></table>

### DescriptorChanged()

Emitted when the leverage descriptor contract address is changed by the LP Vault owner.

#### Arguments

<table><thead><tr><th width="221">Argument</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>descriptor</td><td>address</td><td>The address of the <code>msg.sender</code> (i.e. depositor) that deposited into the vault.</td></tr></tbody></table>

## Structs

### PermitData

A struct that defines the signed permit signatures for the LP Vault `token0` and `token1`.

<table><thead><tr><th width="152">Variables</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>v0</td><td>uint8</td><td>The recovery id (recid) that enables faster verification of the permit signature.</td></tr><tr><td>r0</td><td>bytes32</td><td>One half of a pair of integers (<code>r</code> and <code>s</code>) that forms the output signature of a signed permit transaction.</td></tr><tr><td>s0</td><td>bytes32</td><td>One half of a pair of integers (<code>r</code> and <code>s</code>) that forms the output signature of a signed permit transaction.</td></tr><tr><td>v1</td><td>uint8</td><td>The recovery id (recid) that enables faster verification of the permit signature.</td></tr><tr><td>r1</td><td>bytes32</td><td>One half of a pair of integers (<code>r</code> and <code>s</code>) that forms the output signature of a signed permit transaction.</td></tr><tr><td>s1</td><td>bytes32</td><td>One half of a pair of integers (<code>r</code> and <code>s</code>) that forms the output signature of a signed permit transaction.</td></tr></tbody></table>

## Constructor

Factor Vault contracts implements OpenZeppelin's upgradeable contracts design and locks the Vault contract upon initialization to avoid contract takeover by an attacker. More info can be found on [OpenZeppelin Docs](https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializing\_the\_implementation\_contract).

## Methods

### initialize() - `public` `initializer`&#x20;

The contract initialization function which initializes the contract with the vault params and initial fee configurations. Defaults the fee recipient to the `msg.sender` (i.e. LP vault creator).&#x20;

#### Parameters

<table><thead><tr><th width="197">Params</th><th width="126">Type</th><th>Description</th></tr></thead><tbody><tr><td>_strategyImplementation</td><td>address</td><td>The address of the strategy contract to be implemented for this LP vault.</td></tr><tr><td>_factorLPDescriptor</td><td>address</td><td>The address of the LP vault descriptor that will describe the LP vault token.</td></tr><tr><td>_name</td><td>string</td><td>The name of the LP vault collection. Used as the NFT collection name.</td></tr><tr><td>_symbol</td><td>string</td><td>The symbol of the LP vault collection. Used as the NFT collection symbol.</td></tr><tr><td>_weth</td><td>address</td><td>The address of the WETH token.</td></tr></tbody></table>

### setAllowedLeverageVault() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the `owner` of the LP vault contract to configure the list of permitted underlying Leverage vaults. LP vaults are built atop of Leverage vaults to enable greater capital efficiency through utilizing leveraged positions for liquidity management.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>vault</td><td>address</td><td>The address of the underlying Leverage vault.</td></tr><tr><td>allowed</td><td>bool</td><td>The address of the <code>asset</code> lending pool to be changed to.</td></tr></tbody></table>

### createDepositAndExecute() - `external` `payable` `returns`

Creates a new position representing the configurations of a depositor's position in the leverage vault (only consists of the position structure and not actual liquidity).&#x20;

To create the position, a new instance of the `strategyImplementation` contract is initalized with every newly created position ID for this vault. The relevant token amounts are transferred to the newly created Strategy contract address.

The newly created position NFT (representing a position in the LP vault) is sent to the `msg.sender`.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>token0</td><td>address</td><td>The address of the liquidity position's token0 (i.e. 1 half of the token pair sorted alphabetically by address).</td></tr><tr><td>token1</td><td>address</td><td>The address of the liquidity position's token1 (i.e. the other half of the token pair sorted alphabetically by address).</td></tr><tr><td>amount0</td><td>uint256</td><td>The amount of <code>token0</code> being deposited into the LP vault.</td></tr><tr><td>amount1</td><td>uint256</td><td>The amount of <code>token1</code> being deposited into the LP vault.</td></tr><tr><td>data</td><td>bytes[]</td><td>A bytes array that contains the encoded liquidity position data (i.e. token amount, price range, etc.)</td></tr><tr><td>newNonce</td><td>uint256</td><td>The nonce for the <code>msg.sender</code> incremented by 1 that tracks the position count for the depositor.</td></tr><tr><td>leverageVault</td><td>address</td><td>The address of the underlying Leverage vault for the newly created position.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td>uint256</td><td>The new <code>currentPositionId</code> after a position is created (i.e. newly created position ID plus 1).</td></tr><tr><td>strategy</td><td>The address of the newly deployed strategy contract which was implemented for the position.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorlpvault.sol.md#positioncreated">PositionCreated()</a></td><td>Emits the <code>currentPositionId</code> and the implemented strategy address.</td></tr></tbody></table>

### permit() - `external` `payable`

Handles the ERC20 `permit()` function that enables the LP Vault to spend `token0` and `token1` from the `msg.sender` (i.e. depositor) address.

Leverages the Multicallable.sol contract.

#### Parameters

<table><thead><tr><th width="159">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td>address</td><td>The address of the token which is being permitted.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>token</code> which the LP Vault is allowed to spend.</td></tr><tr><td>paramsPermit</td><td>bytes</td><td>The <a href="https://docs.openzeppelin.com/contracts/4.x/api/token/erc20#ERC20Permit-permit-address-address-uint256-uint256-uint8-bytes32-bytes32-">ERC20 permit parameters</a>.</td></tr></tbody></table>

### refund() - `external` `payable` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the `owner` of the LP Vault to refund any remaining `tokenAddress` in the vault.

Leverages the Multicallable.sol contract.

#### Parameters

<table><thead><tr><th width="151">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenAddress</td><td>address</td><td>The address of the token remaining in the vault.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>token</code> to be refunded form the vault.</td></tr></tbody></table>

### deposit() - `external` `payable`

Allows the safe transfer of a specified `amount` of `token` from the `msg.sender` (i.e. depositor) to the LP Vault contract.

#### Parameters

<table><thead><tr><th width="159">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>token</td><td>address</td><td>The address of the token being deposited.</td></tr><tr><td>amount</td><td>uint256</td><td>The amount of <code>token</code> being deposited.</td></tr></tbody></table>

### \_decodeParamsPermit() - `internal` `pure` `returns`

An internal helper function that facilitates the decoding of permit parameters for LP vault `token0` and `token1`.

#### Parameters

<table><thead><tr><th width="159">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>paramsPermit</td><td>bytes</td><td>The encoded bytes representation of the permit signatures.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorlpvault.sol.md#permitdata">PermitData</a></td><td>The decoded permit signature parameters which includes the recovery id and output signatures.</td></tr></tbody></table>

### burnPosition() - `external`

Allows the `owner` of the position to burn the NFT representing their zero-balance position.

#### Parameters

<table><thead><tr><th width="159">Params</th><th width="123">Type</th><th>Description</th></tr></thead><tbody><tr><td>positionId</td><td>uint256</td><td>The identifier for the position to be burned.</td></tr></tbody></table>

### tokenURI() - `public` `view` `override` `returns`

Returns the encoded Uniform Resource Identifier (URI) of the position `id` that is being queried.

#### Parameters

<table><thead><tr><th width="156">Params</th><th width="140">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The <code>positionId</code> of the position whose URI data is being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="159">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The encoded URI for the token representing the position in the LP Vault.</td></tr></tbody></table>

### setDescriptor() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the owner of the LP Vault to change the address of the `factorLPDescriptor`.

#### Events

<table><thead><tr><th width="209">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorlpvault.sol.md#descriptorchanged">DescriptorChanged()</a></td><td>Emits the address of the new LP Vault descriptor.</td></tr></tbody></table>

### getNextStrategyAddress() - `public` `view` `returns`

Checks whether the upgrade from `baseImplementation` to `upgradeImplementation` has been registered by the Leverage Vault `owner`.

#### Parameters

<table><thead><tr><th width="146">Params</th><th width="99">Type</th><th>Description</th></tr></thead><tbody><tr><td>user</td><td>address</td><td>The address of user for which the Strategy contract will be deployed with the newly created position.</td></tr><tr><td>nonce</td><td>uint256</td><td>The internal tracker for the number of positions created by the <code>user</code>. To get the address of the next Strategy contract to be deployed, the current user nonce (tracked under the <code>nonces</code> mapping) must be incremented by 1.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="208">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the Strategy contract implemented for this LP Vault.</td></tr></tbody></table>

### isRegisteredUpgrade() - `external` `view` `returns`

Checks whether the upgrade from `baseImplementation` to `upgradeImplementation` has been registered by the LP Vault `owner`.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="99">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="208">Type</th><th>Description</th></tr></thead><tbody><tr><td>bool</td><td><code>true</code> = Proposed strategy has been registered by <code>owner</code>.<br><code>false</code> = Proposed strategy has not been registered by <code>owner</code>.</td></tr></tbody></table>

### registerUpgrade() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to register a strategy upgrade from `baseImplementation` to `upgradeImplementation`. Proposed strategies must be registered before it can be implemented.

#### Parameters

<table><thead><tr><th width="226">Params</th><th width="106">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorlpvault.sol.md#upgraderegistered">UpgradeRegistered()</a></td><td>Emits the registered strategy upgrade proposal.</td></tr></tbody></table>

### removeUpgrade() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to remove a previously registered strategy upgrade proposal from `isUpgrade`.

#### Parameters

<table><thead><tr><th width="227">Params</th><th width="93">Type</th><th>Description</th></tr></thead><tbody><tr><td>baseImplementation</td><td>address</td><td>The address of the previous strategy contract.</td></tr><tr><td>upgradeImplementation</td><td>address</td><td>The address of the proposed updated strategy contract.</td></tr></tbody></table>

#### Events

<table><thead><tr><th width="261">Events</th><th>Description</th></tr></thead><tbody><tr><td><a href="factorlpvault.sol.md#upgraderemoved">UpgradeRemoved()</a></td><td>Emits the strategy upgrade proposal that was removed.</td></tr></tbody></table>

### updateImplementation() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to update the `strategyImplementation` with a newly provided address.

#### Parameters

<table><thead><tr><th width="244">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>_strategyImplementation</td><td>address</td><td>The address of the new strategy implementation contract.</td></tr></tbody></table>

### setFeeRecipient() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to update the `feeRecipient` with a newly provided address.

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>recipient</td><td>address</td><td>The address that receives the LP fees.</td></tr></tbody></table>

### setChangeRangeFee() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to update the `changeRangeFee` that is charged on the collected trading fees that have accrued to the position whose range is being changed.

The original `changeRangeFee` is defaulted to `1e15` (i.e. 0.1%). The `newFee` provided is scaled by the LP Vault contract's `FEE_SCALE` which is defaulted to `1e18` on vault initialization. That is, a `newFee` of `1e16` is equivalent to 1% fee (i.e. `1e16`/`1e18`).

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>newFee</td><td>uint256</td><td>The amount of change range fee to charge. </td></tr></tbody></table>

### setCompoundFee() - `external` [`onlyOwner`](https://docs.openzeppelin.com/contracts/2.x/api/ownership#Ownable-onlyOwner--)

Allows the LP Vault `owner` to update the `compoundFee` that is charged on the accrued trading fees which is being reinvested (i.e. compounded) into the position.

The original `compoundFee` is defaulted to `1e15` (i.e. 0.1%). The `newFee` provided is scaled by the LP Vault contract's `FEE_SCALE` which is defaulted to `1e18` on vault initialization. That is, a `newFee` of `1e16` is equivalent to 1% fee (i.e. `1e16`/`1e18`).

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>newFee</td><td>uint256</td><td>The amount of compounding fee to charge. </td></tr></tbody></table>

### version() - `external` `pure` `returns`

Returns the LP  Vault version which is hardcoded based on contract deployment.

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>The LP Vault version.</td></tr></tbody></table>

### \_increaseBalance() - `internal` `virtual` `override`

An internal function that overrides the ERC721  [\_increaseBalance()](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721#ERC721-\_increaseBalance-address-uint128-) function meant to increase the number of NFT collection tokens held by the `account`.

#### Parameters

<table><thead><tr><th width="168">Params</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td>account</td><td>address</td><td>The address of the position holder.</td></tr><tr><td>amount</td><td>uint128</td><td>The amount of LP Vault token count to be added to the existing <code>account</code> balances.</td></tr></tbody></table>

### \_update() - `internal` `virtual` `override` `returns`

An internal function that overrides the ERC721  [\_update()](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721#ERC721-\_update-address-uint256-address-) function meant to update the owner of the `tokenId`.

#### Parameters

<table><thead><tr><th width="152">Params</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>to</td><td>address</td><td>The address to transfer ownership of <code>tokenId</code> to. Mints (or burns) the position NFT if the current owner (or to) is the zero address.</td></tr><tr><td>tokenId</td><td>uint128</td><td>The identifier for the LP Vault NFT to be updated.</td></tr><tr><td>auth</td><td>address</td><td>An optional params where passing in a non-zero value checks if the provided address has the rights to transfer the token (i.e. owner or approved).</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>address</td><td>The address of the LP Vault NFT (representing the position) before the update.</td></tr></tbody></table>

### supportsInterface() - `public` `view` `override` `returns`

An internal function that overrides the ERC721 [supportsInterface()](https://docs.openzeppelin.com/contracts/2.x/api/introspection#IERC165-supportsInterface-bytes4-) function that returns `true` if this LP  Vault contract implements the interface defined by `interfaceId`.

#### Parameters

<table><thead><tr><th width="152">Params</th><th width="100">Type</th><th>Description</th></tr></thead><tbody><tr><td>interfaceId</td><td>bytes4</td><td>The encoded bytes data representing the interface being queried.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="226">Type</th><th>Description</th></tr></thead><tbody><tr><td>bool</td><td><code>true</code> = <code>interfaceId</code> is supported by the LP Vault contract<br><code>false</code> = <code>interfaceId</code> is not supported by the LP Vault contract</td></tr></tbody></table>

### receive() - `public` `view` `override` `returns`

Fallback function that enables the contract to receive ETH.
