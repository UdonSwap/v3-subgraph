# UdonSwap V3 Subgraph

### Subgraph Endpoint

Synced at: https://api.goldsky.com/api/public/project_clvqb3g2poub601xzgkzc9oxs/subgraphs/udonswap-v3/1/gn


query to get top pools 
```shell
query TopPoolsWithRecentDayData {
  pools(first: 10, orderBy: txCount, orderDirection: desc) {
    id
    totalValueLockedUSD
    txCount
    feeTier
    token0 {
      id
      name
      symbol
      decimals
    }
    token1 {
      id
      name
      symbol
      decimals
    }
    poolDayData(first: 7, orderBy: date, orderDirection: desc) {
      date
      liquidity
      volumeUSD
    }
  }
}

```
