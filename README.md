# CoinState
CoinState is a log of transactions entering and leaving the mempool of a Bitcoin node. It can be used to reconstruct local Bitcoin client state and do various simulations, experiments and forensic analysis of the network. Get it [here](https://drive.google.com/drive/folders/1_taGoCphJeH4JspP5D3JuT7vwTRQp4MS?usp=sharing).

Logs start on the 8th May 2018 and run till 6th September 2018 (122 days). Each file is a compressed log of the day and numbered from 0 to 121.

Schema of entry file:
```
{
  "type": <ENTRY or EXIT>,
  "hash": <hash of tx>,
  "ancestor_count": <number of in-mempool ancestors>,
  "ancestor_size": <size of ancestors>,
  "ancestor_fee": <total fee of ancestors (including current tx)>,
  "descendant_count": <number of in-mempool descendant>,
  "descendant_size": <size of descendants>,
  "descendant_fee": <total fee of descendants (including current tx)>,
  "time": <local time when entering the mempool>,
  "size": <size of tx>,
  "amount": <sum of txouts>,
  "fee": <miner fee>,
  "TxIn": [
    {
      "outpoint": {
        "hash": <tx being spent>,
        "index": <index of txout being used>
      }
    }
    .
    .
    .
  ]
}
```

The exit file is the same as the entry, except for:
1. reason value
2. time value

The `time` value is the time the transaction *exited* the mempool. And the `reason` value is the reason the exit happened. It can be one of 7 possible values:
* **UNKNOWN** Manually removed or unknown reason)
* **EXPIRY** (Expired from mempool)
* **SIZELIMIT** (Removed in size limiting)
* **REORG** (Removed for reorganization)
* **BLOCK** (Removed for block)
* **CONFLICT** (Removed for conflict with in-block transaction)
* **REPLACED** (Removed for replacement)

A lot of the above schema has been directly taken from Bitcoin's codebase: [txmempool.h](https://github.com/bitcoin/bitcoin/blob/master/src/txmempool.h).