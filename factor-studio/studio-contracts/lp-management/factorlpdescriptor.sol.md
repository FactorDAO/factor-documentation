# FactorLPDescriptor.sol

{% hint style="info" %}
**Contract Overview**

The `FactorLPDescriptor.sol` contract enables the SVG representation of a position to be generated on-chain. This is achieved via the encoding of position metadata as  SVG strings.
{% endhint %}

## Properties

### Public

<table><thead><tr><th width="182">Property</th><th width="133">Type</th><th width="100">Modifier</th><th>Description</th></tr></thead><tbody><tr><td>tokenDescriptions</td><td>mapping(address => string)</td><td>public</td><td>A mapping between the token address and the corresponding name (i.e. symbol).</td></tr></tbody></table>

## Structs

### TokenURIParams

A struct that defines the URI of the token (representing a position on the underlying LP Vault contract).

<table><thead><tr><th width="149">Variables</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the LP Vault contract.</td></tr><tr><td>name</td><td>string</td><td>The name of the LP Vault collection. Used as the NFT collection name.</td></tr><tr><td>description</td><td>string</td><td>The symbol of the LP Vault collection. Used as the NFT collection symbol.</td></tr><tr><td>token0</td><td>address</td><td>The address of the liquidity position's token0 (i.e. 1 half of the token pair sorted alphabetically by address).</td></tr><tr><td>token1</td><td>address</td><td>The address of the liquidity position's token1 (i.e. the other half of the token pair sorted alphabetically by address).</td></tr></tbody></table>

## Methods

### constructTokenURI() - `public` `view` `returns`

Assembles the encoded string which contains the ERC721 metadata JSON. This includes a `base64` string representation of the position's SVG image that contains position data.

#### Parameters

<table><thead><tr><th width="122">Params</th><th width="163">Type</th><th>Description</th></tr></thead><tbody><tr><td>params</td><td><a href="factorlpdescriptor.sol.md#tokenuriparams">TokenURIParams</a></td><td>An object that contains position information queried from the position's Strategy contract:<br><code>id</code> = Position identifier<br><code>name</code> = Name of the LP Vault collection<br><code>description</code> = Symbol of the LP Vault collection<br><code>token0</code> = Address of liquidity position's token0<br><code>token1</code> = Address of liquidity position's token1</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>An encoded string that contains the ERC721 metadata JSON. This includes a <code>base64</code> string representation of the position's SVG image that contains position data.</td></tr></tbody></table>

### renderImage() - `private` `view` `returns`

Renders a `base64` string that represents the position's information in a SVG format.

#### Parameters

<table><thead><tr><th width="142">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the LP Vault contract.</td></tr><tr><td>token0</td><td>address</td><td>The address of the liquidity position's token0 (i.e. 1 half of the token pair sorted alphabetically by address).</td></tr><tr><td>token1</td><td>address</td><td>The address of the liquidity position's token1 (i.e. the other half of the token pair sorted alphabetically by address).</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A <code>base64</code> string representation of the position's SVG image that contains position data.</td></tr></tbody></table>

### renderId() - `private` `view` `returns`

Renders a SVG string of the position identifier.

#### Parameters

<table><thead><tr><th width="141">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>uint256</td><td>The identifier of the position managed by the LP Vault contract.</td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position identifier.</td></tr></tbody></table>

### renderStrategy() - `private` `view` `returns`

Renders a SVG string of the Strategy's `asset` and `debt` names (i.e. symbols).

#### Parameters

<table><thead><tr><th width="199">Params</th><th width="109">Type</th><th>Description</th></tr></thead><tbody><tr><td>token0</td><td>string</td><td>The name (i.e. symbol) of the Strategy's <code>token0</code></td></tr><tr><td>token1</td><td>string</td><td>The name (i.e. symbol) of the Strategy's <code>token1</code></td></tr></tbody></table>

#### Returns

<table><thead><tr><th width="166">Type</th><th>Description</th></tr></thead><tbody><tr><td>string</td><td>A SVG string representation of the position's <code>asset</code> and <code>debt</code> token names.</td></tr></tbody></table>
