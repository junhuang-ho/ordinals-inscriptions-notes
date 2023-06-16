----- back story -----

- UTXOs are made up of inputs and outputs (bitcoin network does not track how much balance u have after a txn, it just tracks the inputs vs outputs)
- note: a txn may have multiple outputs
- every output can only be used by an input once, anymore than that and it will be considered as double spending - which is forbidden

---

## ------ ordinals ------

- pre ordinals, every bitcoin/satoshi (sat) are unmarked (indistinguishable from one another)
- ordinals now "pretends" the set an order of the inputs and outputs of each txn, and pretends to set first sat into txn is first sat out of txn (its like a convention that everyone (or majority) needs to agree upon for it to be "true").
- now the sats are ordered, they are distinugisable from one another
- note: the base bitcoin protocol doesn't really care about this "pretend" order and won't throw error with the addition of ordinals
- note: why do we order sat and not bitcoin? because each bitcoin is just made up of N sats

---

## ----- inscriptions ------

-- What was the segwit upgrade ------------------------

- Prior to segwit, the inputs have all sorts of data attached to it, including data for verifying (signature/proofs) which previous output does this input connect to/unlock
- These sigs/proofs part of the data pose some limitations
- So in segwit, the sigs/proofs part of the data (those not required to determine the txn effects) are moved to a new structure - "segregating all the witness data (segwit)"
- this effectively increases the space in the "non-witness" side of the block to ~4mb, doubling the txn throughput of network
- OLD: MAX_BLOCK_BASE_SIZE = 1000000 (~ 1mb)
- NEW: 4 \* non witness data (in bytes) + witness data (in bytes) < 4 million units

-- What was the taproot upgrade ------------------------

- improves privacy, efficiency, and flexibility of bitcoin's scripting capabilities.
- to do this it allows verification/scripts/proofs (witness data) to be a certain (bigger) size and allows increase complexity
- eg complexity - say have N different ways of unlocking/verifying an output, taproot allows that u dont have to show all N ways, just show say 1 is enough, and give a proof that it works (revealing the key)
- now the "key" to unlock the output of a UTXO is a witness verification data, and in the process of revealing the key, the data associated is "inscribed" on chain.

----- bringing it all together - bitcoin NFT Image example -----

- with ordinals, each sat is now unique, non-fungible --> nft trait
- with inscriptions, we can set the "image jpeg" as the proof needed to be revealed and inscribed on the blockchain
- thus: NFT Image
- technical caveats:
- 1.  to inscribe, we need to send a "stack" of sats to ourselfs. Why send a stack and not just 1 sat for 1 nft image? because there is a dust limit where and sats less than ~546 sats is not worth the txn fee / coin price ratio.
- 2.  we inscribe the NFT on the first sat of the stack
- 3.  note that a sat can be inscibed multiple times
      Q1: (as long as the 4million units limit not reached?)
      Q2: (can different owner inscribe on the same sat?)
