### Data Analyst Practice Questions:

It is my opinion that you should be able to answer all of these questions to be a competent web3 analyst.

Some notes before you get started:

1. These questions assume you already have some SQL background. 
2. Bonus questions (and some hints) are within the toggles. 
3. “Using `x.table` ” just means this is the existing Dune table you should use (if you’re using Dune). All queries are to be made on Ethereum mainnet tables. 

<aside>
💡 Many of these questions do not give you an exact address or link, since in the real world you’re often chasing data off of someone’s random tweet or thread. Learning to sleuth around for the right data source is 50% of the challenge! 

Learn to use all the search tools at your disposal: Google, Dune search, Twitter advanced search, Etherscan, GitHub, Discourse forums, etc.

</aside>

- calculate the total ETH transfer value by block in the last week using `ethereum.transactions` and `ethereum.traces`. Why are the values different?
- look at an [example transaction](https://etherscan.io/tx/0xfa8aac1b4d50952f7cc711cd3959c05968ade2e538639c9555c5aa0d0fa6e76d) (of a token swap) using only `ethereum.transactions` and `ethereum.traces` tables. Don’t worry about understanding the protocol, just answer the following questions:
    - [diagram explaining every part of a tx on etherscan](https://github.com/andrewhong5297/web3-data-practice/blob/main/analyst/diagrams/tx_explained.jpg)
    - bonus question: how much gas was used in this swap?
        - hint on how gas breaks down
            - [reading resource](https://www.blocknative.com/blog/eip-1559-fees#:~:text=The%20New%20Terminology%20of%20EIP%2D1559%20Transactions&text=Instead%20of%20a%20singular%20Gas,is%20paid%20directly%20to%20miners.)
    - bonus question: how many contracts were involved?
    - bonus question: how do you remove double counts of proxy contracts? hint: lookup delegate calls (don’t confuse `call` and `call_type`!)
    - bonus question: how many of these contracts are under the same namespace on Dune (i.e. uniswap, mirror, aave)?
- find all the new DEX pairs created in the first month the [Uniswap V2 factory was deployed](https://docs.uniswap.org/protocol/V2/reference/smart-contracts/factory).
    - Bonus question: find each pair’s DEX volume, grouped by month.
- how can you figure out quickly which logs or functions to look at? Try and find the Uniswap V2 Pair contract for USDC/ETH. Run the analysis using `ethereum.logs` and `ethereum.transactions` tables only.
    - I have a list of utility queries out there somewhere with the answer to this one. Wonder if you can find them? 🙂
- what’s an ERC20 token standard and how can you find a `transfer` event or function call?
    - hint: keccak256 hash for transfer event `Transfer(address,address,uint256)`
        - [https://emn178.github.io/online-tools/keccak_256.html](https://emn178.github.io/online-tools/keccak_256.html)
    - bonus question: look at the COMP token, and examine the distribution of delegations.
        - compare this delegation across governance proposals (look for the Governor Bravo and Alpha contracts). Were there any periods of large voting power swings?
- how can you calculate ERC20 balances (use **USDC**) using events? Who are the top 100 holders?
    - use `ethereum.logs` and then `erc20.ERC20_evt_Transfer` table.
    - bonus question: how many times are there `approval` calls before a `transfer` call?
    - bonus question: can you look at the Ronin bridge hack and figure out when the hack started?
    - bonus question: calculate interest/aToken balance point in time? or rebasing token like OHM?
- how do you find someone’s LP balance and historical change in representation in the Uniswap v2 USDC/ETH pool?
    - bonus question: find the top 100 holders of USDC by adding raw balances (from last question) and liquidity pair balances together.
- What’s the historical DEX trading share of USDC/ETH by DEX protocol (not incl aggregators) using `dex.trades`?
    - bonus question: find the inflection points where shares drastically changed. What were the governance proposals that went through during that time?
- what are the top 100 NFT contracts spent the most gas to mint (before April 25th, 2022) using any combination of tables?
    - bonus question: same question but filter for failed transactions only
- how to calculate the floor price of NFTs based on recent sales (using just OpenSea data)?
    - bonus question: which collection has the maximum difference when you use daily sale minimum versus percentile?
    - bonus question: how do trends compare using 1 day, 1 week, and 1 month averages?
    - bonus question: fractional trading price as NFT token value?
- NFT trading share over time of BAYC (by the marketplace) using `nft.trades`?
