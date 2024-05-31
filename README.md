# Glyphs
A fungible token meta-protocol built on Counterparty and leveraging Stamps

## Backstory

It occurred to me (and many others) that Runes' OP_RETURN implementation seems very much like Counterparty. In fact, fungible tokens have been possible on Counterparty for the last decade. Even the segmented nature of Runes token namespaces is reminiscent of sub-assets on Counterparty. So while Runes does not really strike me as a new and novel approach to tokenization, what can't be ignored is that Runes, thanks to its Ordinals-adjacency, has quickly become the #1 fungible token protocol on Bitcoin. But Runes lacks a lot of the innovations that Counterparty offers. I believe that Counterparty (current and near-future feature-set) can be enabled to create a Runes-like, but better, tokenization standard.

## The current Runes implementation

Runes, at inception, utilize 14 character token tickers where the bullet symbol (•) can be used to delineate between specific words. Example: DOG•GO•TO•THE•MOON

Over time, the 14 character requirement will decay to lower limits, but that's a topic that doesn't need to be detailed within this brief.

These tokens are attached to discrete UTXOs which are used as the token layer and transferred around representing ownership of the Rune supply.

Runes have the advantage of recursively pointing to previously minted Ordinal Inscriptions to visually complement the token.

## Counterparty: The Present

You could pretty much launch a Runes-like token on Counterparty today with a few caveats.

1) Counterparty doesn't support attaching assets to discrete UTXOs. This has its pros and cons. In the pros column, Counterparty assets are far more resilient to accidental spending. In the cons column, atomic swap functionality through trustless PSBT is not possible.

2) While an asset/sub-asset registration is possible on Counterparty, minimum character limits as well as singular ownership of the root named asset means that there is less ability for users to pick common names. For instance, DOG.GO.TO.THE.MOON could be minted by registering the named asset: DOG and the sub-asset: GO.TO.THE.MOON but no one else would be able to create a token ticker starting with the word "DOG". Couple this with the fact that Counterparty has been around for a decade and its pretty apparant that most common words have already been minted. Additionally, minimum named assets character length is 4 (so DOG is out) and you can't start a named asset using the letter "A".
