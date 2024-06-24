# Glyphs
A fungible token meta-protocol built on Counterparty and leveraging Bitcoin Stamps

## Backstory

It occurred to me (and many others) that Runes' OP_RETURN implementation seems very much like Counterparty. In fact, fungible tokens have been possible on Counterparty for the last decade. Even the segmented nature of Runes token namespaces is reminiscent of sub-assets on Counterparty. So while Runes does not really strike me as a new and novel approach to tokenization, what can't be ignored is that Runes, thanks to its Ordinals-adjacency, has quickly become the #1 fungible token protocol on Bitcoin. But Runes lacks a lot of the innovations that Counterparty offers. I believe that Counterparty (current and near-future feature-set) can be leveraged to create a Runes-like, but better, tokenization standard.

## The current Runes implementation

Runes, at inception, utilize 14 character token tickers where the bullet symbol (•) can be used to delineate between specific words. Example: <code>DOG•GO•TO•THE•MOON</code>

Over time, the 14 character requirement will decay to lower limits, but that's a topic that doesn't need to be detailed within this brief.

These tokens are attached to discrete UTXOs which are used as the token layer and transferred around representing ownership of the Rune supply.

Runes have the advantage of recursively pointing to previously minted Ordinal Inscriptions to visually complement the token.

## Counterparty: The Present

You could pretty much launch a Runes-like token on Counterparty today with a couple caveats.

1) Counterparty doesn't support attaching assets to discrete UTXOs. This has its pros and cons. In the pros column, Counterparty assets are far more resilient to accidental spending. In the cons column, atomic swap functionality through trustless PSBT is not possible.

2) While an asset/sub-asset registration is possible on Counterparty, minimum character limits as well as singular ownership of the root named asset means that there is less ability for users to pick common names. For instance, <code>DOG.GO.TO.THE.MOON</code> could be minted by registering the named asset: <code>DOG</code> and the sub-asset: <code>GO.TO.THE.MOON</code> but no one else would be able to create a token ticker starting with the word "DOG". Couple this with the fact that Counterparty has been around for a decade and its pretty apparant that most common words have already been minted. Additionally, minimum named assets character length is 4 (so DOG is out) and you can't start a named asset using the letter "A". In contrast, sub-assets are far more permissive.

## Counterparty: The Future

Future planned enhancements to Counterparty along with some specific proposals could make launching Runes-like tokens even more viable on Counterparty. Being able to attach/detach an asset to a discrete UTXO is on the Counterparty roadmap in the near future. Additionally, if sub-assets were to be issuable on a numeric asset, the sub-asset could inherent a recursive link to a specific Stamp in the same way that a Runes token can recursively point to an Inscription.

## The origination of the Fair Mint Model

Fair Mint likely originated with Counterparty itself where users sent Bitcoin to a burn address and received XCP in return. More recently, BRC-20 introduced a variant of the Fair Mint model and adopted by many fungible token protocols in the last year including SRC-20 on Bitcoin Stamps. It's a method where users are able to mint "for free" by paying only a miner fee but not directly enriching the deployer of the token. This is considered to be "fair" and may also have a favorable structure from a legal stand-point as no direct sales are occuring.

## The XCP-20 Fair Mint model

In 2023, Joe Looney introduced XCP-20's Fair Mint model (https://xcp20.wtf/) by setting-up a dispenser on a burn address and called it "XCP-20" as a tongue in cheek reference to BRC-20. Buyers, largely unaware that Counterparty already existed and this was not *new* in any way, sent massive amounts of Bitcoin to the burn address and received tokens in return. In this way, tokens got distributed, but the deployer was not directly enriched. The Bitcoin was burned.

## The all-new Counterparty Auto Mint functionality (name is TBD)

As non-source address dispensers will no longer be possible as of Counterparty Core 10.3, as solution has been proposed to bring a "Fair Mint" model to Counterparty natively. See: https://github.com/CounterpartyXCP/counterparty-core/issues/1843

## Glyphs: The Proposal

The Deployer mints a Bitcoin Stamp on a numeric asset. Let's say: <code>A5433937813514022010</code> which contains the following base64-encoded image:<br><br>
<img src="https://stampchain.io/stamps/88fab306902f27f2a2c5aabf8983f0ef1f4135c20c0cbf494546a611bc2692c6.png">

Source: https://stampchain.io/asset.html?asset=A5433937813514022010

The Deployer then issues a sub-asset on the numeric: <code>A5433937813514022010.A5433937813514022010</code> and opens an Auto Mint of the supply.

Relevant meta-data (ticker, supply, etc...) will be added through an onchain JSON envelope using OLGA-encoding. In this way, <code>A5433937813514022010.A5433937813514022010</code> can be represented by something like <code>JOIN•THE•FLOCK</code> in wallets and explorers.

Buyers can then "mint" the token through the Auto Mint. Holders can then, optionally, attach/detach the tokens to discrete UTXOs and sell the tokens using PSBT/Atomic Swap. They also have the option to re-sell the tokens in dispensers which saves having to split/attach to UTXOs (a common gripe about Runes).

Glyphs-aware wallets/explorers will understand the relationship between the "Glyph" and the root numeric asset that its descended from and render the base64 art in a standardized container using HTML and recursion to the ancestory Stamp. An early mock-up of the container design can be found below.<br><br>

<img src="https://i.imgur.com/hxmllWK.jpeg" width="200">   <img src="https://i.imgur.com/VUQuKqD.jpeg" width="200">   <img src="https://i.imgur.com/mriUIJM.jpeg" width="200">

## Glyphs are NOT Bitcoin Stamps

Glyphs, at the time of this writing, as not intended to be Bitcoin Stamps. However, they are very much "Bitcoin Stamps-adjacent" in the same way that Runes are "Ordinals-adjacent". What this means from a implementation perspective is that Glyphs will (hopefully) be supported within the Bitcoin Stamps ecosystem (integrated into wallets and explorers) and they do inherit the artwork and provenance of their linked ancestor, but they would not be assigned canonical Bitcoin Stamp numbers. They would have their own numbering scheme, starting at 0, and likely activated at a designated block height. Additionally, as their means of minting/trade would be native to Counterparty itself rather than requiring a "mint" or "transfer" minting, only the "deploy" itself would be included in the numbering scheme.
