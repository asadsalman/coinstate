# CoinState
CoinState is a log of the local state of a Bitcoin node. Get it [here](https://drive.google.com/drive/folders/1_taGoCphJeH4JspP5D3JuT7vwTRQp4MS?usp=sharing).

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
  ]
}
```