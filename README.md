# Glyphs
A fungible token meta-protocol built on Counterparty and leveraging Stamps

## Backstory

It occurred to me (and many others) that Runes' OP_RETURN implementation seems very much like Counterparty. In fact, fungible tokens have been possible on Counterparty for the last decade. Even the segmented nature of Runes token namespaces is reminiscent of sub-assets on Counterparty. So while Runes does not really strike me as a new and novel approach to tokenization, what can't be ignored is that Runes, thanks to its Ordinals-adjacency, has quickly become the #1 fungible token protocol on Bitcoin. But Runes lacks a lot of the innovations that Counterparty offers. I believe that Counterparty (current and near-future feature-set) can be enabled to create a Runes-like, but better, tokenization standard.

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

Fair Mint, is a BRC-20 innovation which has been adopted by many fungible token protocols in the last year including SRC-20 on Bitcoin Stamps. It's a method where users are able to mint "for free" by paying only a miner fee but not directly enriching the deployer of the token. This is considered to be "fair" and may also have a favorable structure from a legal stand-point as no direct sales are occuring.

## The Fair Mint model brought to Counterpary

In 2023, Joe Looney brought the Fair Mint model to Counterparty by setting-up a dispenser on a burn address and called it XCP-20 as a tongue in cheek reference to BRC-20. Buyers would send Bitcoin to the burn address and receive tokens in return. In this way, tokens got distributed, but the deployer was not directly enriched.

## Glyphs: The Proposal

The Deployer mints a Bitcoin Stamp on a numeric asset. Let's say: <code>A1717171717171717171</code> which contains the following base64-encoded image:<br><br>
<img src="https://stampchain.io/stamps/0dd5fb27837c8eff55321cecebfbddeb0a2f3136a4f82086568f4b0a0b8a0ed9.gif">

The Deployer then issues a sub-asset on the numeric: <code>A1717171717171717171.THE.KEY.TO.EVERYTHING</code>

The supply of the sub-asset can then be sent to a dispenser opened on a known burn address (more of that later). 

Buyers can then "mint" the token by buying them from the dispenser. Holders can then, optionally, attach/detach the tokens to discrete UTXOs and sell the tokens using PSBT/Atomic Swap. They also have the option to re-sell the tokens in dispensers which saves having to split/attach to UTXOs (a common gripe about Runes).

Glyphs-aware wallets/explorers will understand the relationship between the "Glyph" and the root numeric asset that its descended from and render the base64 art in some way in relation to the token. Glyphs-aware wallets/explorers can also suppress the numeric asset within the string itself so that <code>A1717171717171717171.THE.KEY.TO.EVERYTHING</code> appears as simply <code>THE.KEY.TO.EVERYTHING</code>. In fact, Glyphs-aware wallets/explorers can even substitute (•) for (.) in the string so that <code>THE.KEY.TO.EVERYTHING</code> appears as <code>THE•KEY•TO•EVERYTHING</code>. In this manner, we can perfectly replicate the Runes "aesthetic".

## The Provable Burn Address

While the XCP-20 protocol allowed deployers to choose their own burn address and encouraged to use a vanitygen, for user confidence a singular vanity burn address should be chosen for Glyphs. This also will allow a clean way for indexers to determine what is (or isn't) a Glyph based on intent. We propose: 
