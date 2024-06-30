# FactorLeverageDescriptor.sol

{% hint style="info" %}
**Contract Overview**

The `FactorLeverageDescriptor.sol` contract enables the SVG representation of a position to be generated on-chain. This is achieved via the encoding of position metadata as  SVG strings.
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="182">Property</th><th width="133">Type</th><th width="100">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>tokenDescriptions</td><td>mapping(address => string)</td><td>public</td><td>A mapping between the token address and the corresponding name (i.e. symbol).</td></tr></tbody></table>

## Structs

### TokenURIParams

A struct that defines the URI of the token (representing a position on the underlying Leverage Vault contract).

<table><thead><tr><th width="199">Variables</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the Leverage Vault contract.</td></tr><tr><td>name</td><td>string</td><td>The name of the Leverage Vault collection. Used as the NFT collection name.</td></tr><tr><td>description</td><td>string</td><td>The symbol of the Leverage Vault collection. Used as the NFT collection symbol.</td></tr><tr><td>assetToken</td><td>address</td><td>The address of the <code>asset</code> used as collateral for the position.</td></tr><tr><td>debtToken</td><td>address</td><td>The address of the <code>debt</code> used as collateral for the position.</td></tr><tr><td>assetAmount</td><td>uint256</td><td>The amount of <code>asset</code> token held by the position.</td></tr><tr><td>debtAmount</td><td>uint256</td><td>The amount of <code>debt</code> token held by the position.</td></tr></tbody></table>

## Methods

### setTokenName() - `external`

Updates the token name (i.e. symbol) for the provided `tokenAddress`.

#### Parameters

<table><thead><tr><th width="179">Params</th><th width="114">Type</th><th>Description</th></tr></thead><tbody><tr><td>tokenAddress</td><td>address</td><td>The address of the token.</td></tr><tr><td>tokenDescription</td><td>string</td><td>The name (i.e. symbol) of the token to be updated.</td></tr></tbody></table>

### constructTokenURI() - `public` `view` `returns`

Assembles the encoded string which contains the ERC721 metadata JSON. This includes a `base64` string representation of the position's SVG image that contains position data.

#### Parameters

<table><thead><tr><th width="122">Params</th><th width="163">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td><a href="factorleveragedescriptor.sol.md#tokenuriparams">TokenURIParams</a></td><td>An object that contains position information queried from the position's Strategy contract:<br><code>id</code> = Position identifier<br><code>name</code> = Name of the Leverage Vault collection<br><code>description</code> = Symbol of the Leverage Vault collection<br><code>assetToken</code> = Address of <code>asset</code> token<br><code>debtToken</code> = Address of <code>debt</code> token<br><code>assetAmount</code> = The position's <code>asset</code> balance<br><code>debtAmount</code> = The position's <code>debt</code> balance</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>An encoded string that contains the ERC721 metadata JSON. </td></tr></tbody></table>

### renderImage() - `private` `view` `returns`

Renders a `base64` string that represents the position's information in a SVG format.

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the Leverage Vault contract.</td></tr><tr><td>assetToken</td><td>address</td><td>The address of the <code>asset</code> used as collateral for the position.</td></tr><tr><td>debtToken</td><td>address</td><td>The address of the <code>debt</code> used as collateral for the position.</td></tr><tr><td>assetAmount</td><td>uint256</td><td>The amount of <code>asset</code> token held by the position.</td></tr><tr><td>debtAmount</td><td>uint256</td><td>The amount of <code>debt</code> token held by the position.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A <code>base64</code> string representation of the position's SVG image that contains position data.</td></tr></tbody></table>

### renderId() - `private` `view` `returns`

Renders a SVG string of the position identifier.

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the Leverage Vault contract.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position identifier.</td></tr></tbody></table>

### renderStrategy() - `private` `view` `returns`

Renders a SVG string of the Strategy's `asset` and `debt` names (i.e. symbols).

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>asset</td><td>string</td><td>The name (i.e. symbol) of the Strategy's <code>asset</code> token.</td></tr><tr><td>debt</td><td>string</td><td>The name (i.e. symbol) of the Strategy's <code>debt</code> token.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position's <code>asset</code> and <code>debt</code> token names.</td></tr></tbody></table>

### renderAsset() - `private` `view` `returns`

Renders a SVG string of the position's `asset` balance.

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>asset</code> token held by the position. </td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position's <code>asset</code> balance.</td></tr></tbody></table>

### renderDebt() - `private` `view` `returns`

Renders a SVG string of the position's `asset` balance.

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>amount</td><td>uint256</td><td>The amount of <code>debt</code> token held by the position.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position's <code>debt</code> balance.</td></tr></tbody></table>
