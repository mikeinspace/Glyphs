# Glyphs
A fungible token meta-protocol built on Counterparty and leveraging Stamps

## Backstory

It occurred to me (and many others) that Runes' OP_RETURN implementation seems very much like Counterparty. In fact, fungible tokens have been possible on Counterparty for the last decade. Even the segmented nature of Runes token namespaces is reminiscent of sub-assets on Counterparty. So while Runes does not really strike me as a new and novel approach to tokenization, what can't be ignored is that Runes, thanks to its Ordinals-adjacency, has quickly become the #1 fungible token protocol on Bitcoin. But Runes lacks a lot of the innovations that Counterparty offers. I believe that Counterparty (current and near-future feature-set) can be enabled to create a Runes-like, but better, tokenization standard.

## The current Runes implementation

Runes, at inception, utilize 14 character token tickers where the bullet symbol (•) can be used to delineate between specific words. Example: DOG•GO•TO•THE•MOON

Over time, the 14 character requirement will decay to lower limits, but that's a topic that doesn't need to be detailed within this brief.

These tokens are attached to discrete UTXOs which are used as the token layer and transferred around representing ownership of the Rune supply.
