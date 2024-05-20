# UdonSwap V3 Subgraph

### Subgraph Endpoint

Synced at: https://api.goldsky.com/api/public/project_clvqb3g2poub601xzgkzc9oxs/subgraphs/udonswap-v3/1/gn

Ordering can be handeled client-side

# query for pools tab

```graphql
query topPools {
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
      feesUSD
    }
  }
}
```

order by can be changed dynamically
if want to order it by TVL: totalValueLockedUSD

to calculate 7 day Volume
we have to do sum of 7 epoch (days)

here is the example data obj

```json
 {
        "id": "0x85149247691df622eaf1a8bd0cafd40bc45154a9",
        "totalValueLockedUSD": "9620531.083392658615248984471922004",
        "txCount": "9751781",
        "feeTier": "500",
        "token0": {
          "id": "0x4200000000000000000000000000000000000006",
          "name": "Wrapped Ether",
          "symbol": "WETH",
          "decimals": "18"
        },
        "token1": {
          "id": "0x7f5c764cbc14f9669b88837ca1490cca17c31607",
          "name": "USD Coin",
          "symbol": "USDC",
          "decimals": "6"
        },
        "poolDayData": [
          {
            "date": 1716163200,
            "liquidity": "613533473387314110",
            "volumeUSD": "4703442.083993874542197008810212472",
            "feesUSD": "2351.721041996937271098504405106252"
          },
          {
            "date": 1716076800,
            "liquidity": "631594361995083287",
            "volumeUSD": "6316766.757284899116601350846742958",
            "feesUSD": "3158.383378642449558300675423371475"
          },
          {
            "date": 1715990400,
            "liquidity": "561376582439828649",
            "volumeUSD": "8015283.83974235494109412690696044",
            "feesUSD": "4007.641919871177470547063453480242"
          },
          {
            "date": 1715904000,
            "liquidity": "672900617078163669",
            "volumeUSD": "11489037.24949695814867680933521433",
            "feesUSD": "5744.518624748479074338404667607174"
          },
          {
            "date": 1715817600,
            "liquidity": "403459029390707318",
            "volumeUSD": "6569322.525093733265606265080549126",
            "feesUSD": "3284.661262546866632803132540274531"
          },
          {
            "date": 1715731200,
            "liquidity": "335603610789759341",
            "volumeUSD": "12306852.09965046367208749034558973",
            "feesUSD": "6153.42604982523183604374517279488"
          },
          {
            "date": 1715644800,
            "liquidity": "351852550050072453",
            "volumeUSD": "10256644.20803449141426171168632616",
            "feesUSD": "5128.322104017245707130855843163113"
          }
        ]
      },
```

**7 day volume** = sum of all **volumeUSD** under poolDayData

**1 day volume** is just volumeUSD of first data object under **poolDayData**

1 Day APR = pool' **totalValueLockedUSD** / first obj' **feesUSD**

# query for transactions

```graphql
query MyQuery {
  transactions(first: 100, orderBy: timestamp, orderDirection: desc) {
    burns {
      amount0
      amount1
      amountUSD
      token0 {
        symbol
      }
      token1 {
        symbol
      }
      timestamp
      origin
    }
    mints {
      amount0
      amount1
      amountUSD
      token0 {
        symbol
      }
      token1 {
        symbol
      }
      timestamp
      origin
    }
    swaps {
      amount0
      amount1
      amountUSD
      token0 {
        symbol
      }
      token1 {
        symbol
      }
      timestamp
      origin
    }
  }
}
```

# query for both visual graph (tvl & volume)

```graphql
query MyQuery {
  uniswapDayDatas(first: 100) {
    tvlUSD
    volumeUSD
    date
  }
}
```
