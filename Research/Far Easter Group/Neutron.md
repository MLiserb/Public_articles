# Neutron


---
### flipsidecrypto.xyz:

TABLE `crosschain.price.dim_asset_metadata`:

A comprehensive dimensional table holding asset metadata and other relevant details pertaining to each id, from multiple providers. This data set includes raw, non-transformed data coming directly from the provider APIs and rows are not intended to be unique. As a result, there may be data quality issues persisting in the APIs that flow through to this dimensional model. If you are interested in using a curated data set instead, please utilize ez_asset_metadata.



```sql
SELECT *
FROM crosschain.price.dim_asset_metadata
WHERE BLOCKCHAIN = 'neutron';
```
| TOKEN_ADDRESS                                                                 | ASSET_ID              | SYMBOL | NAME               | BLOCKCHAIN | BLOCKCHAIN_ID | PROVIDER   | INSERTED_TIMESTAMP          | MODIFIED_TIMESTAMP          | DIM_ASSET_METADATA_ID                     |
|------------------------------------------------------------------------------|-----------------------|--------|--------------------|------------|----------------|------------|-----------------------------|-----------------------------|-------------------------------------------|
| eclipse-fi                                                                   | eclipse-fi            | eclip  | Eclipse Fi         | neutron    | neutron        | coingecko  | 2024-06-03 20:16:18.425     | 2024-06-03 20:16:18.425     | f65aa2ec4e4e47daa60af28bca2591c6        |
| factory/neutron10sr06r3qkhn7xzpw3339wuj77hu06mzna6uht0/eclip              | eclipse-fi            | eclip  | Eclipse Fi         | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 36110163d32df8fd84386e7873355658        |
| newt                                                                         | newt                  | newt   | Newt               | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | b828560c19cc981ccda90cb5059d8cd8        |
| neutron1k6hr0f83e7un2wjf29cspk7j69jrnskk65k3ek2nj9dztrlzpj6q00rtsa        | drop-staked-atom     | datom  | Drop Staked ATOM   | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 618b7782ac50fda103b3499e1470d504        |
| ibc/4971C5E4786D5995EC7EF894FCFA9CF2E127E95D5D53A982F6A062F3F410EDB8     | levana-protocol      | lvn    | Levana             | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 777dd9105e6c1d8e9384b8e8873325d7        |
| ibc/58923AAE6E879D7CB5FB0F2F05550FD4F696099AB0F5CDF0A05CC0309DD8BC78      | cerberus-2           | crbrus | Cerberus           | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 42027b84715e8e932dd7f72e16946da6        |
| factory/neutron1ndu2wvkrxtane8se2tr48gv7nsm46y5gcqjhux/MARS                | mars-protocol-a7fcbcfb-fd61-4017-92f0-7ee9f9cc6da3 | mars   | Mars Protocol      | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 1ec8f88d6a006244d8f5a1587d86351f        |
| ibc/6C9E6701AC217C0FC7D74B0F7A6265B9B4E3C3CDA6E80AADE5F950A8F52F9972      | nolus                 | nls    | Nolus              | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | f9aa63af77c9e4dc71cbda4292b37fcd        |
| neutron154gg0wtm2v4h9ur8xg32ep64e8ef0g5twlsgvfeajqwghdryvyqsqhgk8e        | apollo-2             | apollo | Apollo             | neutron    | neutron        | coingecko  | 2024-09-28 14:41:34.745     | 2024-09-28 14:41:34.745     | 2dbb5170414156219e19997ef492ac1a        |

I notice the `PROVIDER` is `coingecko`. (API is very expensive) 

### Key Attributes

1. **Token Address**: Each asset has a unique identifier that likely represents its location or contract address on the blockchain.
2. **Asset ID**: This seems to be an internal identifier for each asset.
3. **Symbol**: A shorthand representation of the asset used for trading or referencing.
4. **Name**: The full name of the asset, providing clarity on what each token represents.
5. **Blockchain**: All entries are associated with the "neutron" blockchain, indicating they are part of the same network.
6. **Blockchain ID**: This is reiterated as "neutron," confirming the blockchain affiliation.
7. **Provider**: All assets are listed with "coingecko," suggesting that this data may be sourced from or related to listings on the CoinGecko platform, a popular cryptocurrency data aggregator.
8. **Timestamps**: Each asset has two timestamps: `INSERTED_TIMESTAMP` and `MODIFIED_TIMESTAMP`, which indicate when the asset was added and last updated in the dataset. This is important for tracking changes over time.
9. **Dimension Asset Metadata ID**: A unique identifier potentially used for linking this data to other databases or systems.

### Observations

- **Diversity of Assets**: The dataset includes a variety of tokens, such as "Eclipse Fi," "Newt," "Drop Staked ATOM," and others, indicating a diverse ecosystem of digital assets.
- **Standardization**: The consistent structure of the dataset suggests that it is designed for easy processing and querying, which is typical for blockchain asset management.
- **Recent Updates**: The most recent entries have been modified on September 28, 2024, indicating active management and updates within the blockchain ecosystem.

### Potential Uses

- **Market Analysis**: This dataset could be used for analyzing the performance and trends of various tokens within the Neutron blockchain.
- **Integration with Applications**: Developers could integrate this metadata into wallets, trading platforms, or other blockchain-based applications to provide users with detailed asset information.
- **Data Enrichment**: The dataset can serve as a foundation for further enrichment with additional data points, such as market prices or trading volumes.

### Conclusion

Overall, this dataset offers valuable insights into the Neutron blockchain's token ecosystem, providing essential information for developers, investors, and analysts interested in blockchain assets.

---
```SQL
SELECT DISTINCT LABEL
FROM cosmos.core.dim_labels
WHERE LABEL LIKE 'Neutron';
```

| | LABEL |
| --- | --- |
| 1 | Neutron |

---

TABLE `crosschain.cosmos.fact_transactions`:

| Column Name              | Data Type     |
|--------------------------|----------------|
| BLOCK_ID                 | TEXT           |
| BLOCK_TIMESTAMP          | TIMESTAMP_NTZ  |
| TX_ID                    | TEXT           |
| TX_FROM                  | TEXT           |
| CODESPACE                | VARIANT        |
| FEE                      | TEXT           |
| FEE_DENOM                | TEXT           |
| GAS_USED                 | NUMBER         |
| GAS_WANTED               | NUMBER         |
| TX_CODE                  | NUMBER         |
| TX_LOG                   | TEXT           |
| MSGS                     | VARIANT        |
| TX_SUCCEEDED             | BOOLEAN        |
| INSERTED_TIMESTAMP       | TIMESTAMP_NTZ  |
| MODIFIED_TIMESTAMP       | TIMESTAMP_NTZ  |
| FACT_TRANSACTIONS_ID     | TEXT           |

```SQL
SELECT DISTINCT BLOCKCHAIN
FROM crosschain.cosmos.fact_transactions;
```

| | BLOCKCHAIN |
| --- | --- |
| 1 | osmosis |
| 2 | cosmos |
| 3 | axelar |


