<p align="center">
  <img src="assets/banner.jpeg" alt="Cluby — credit against tokenized stocks" width="100%">
</p>

<h1 align="center">Cluby</h1>

<p align="center">
  <b>Credit against tokenized stocks.</b><br>
  Post NVDA, SPY or AAPL as collateral and borrow USDG — without selling the position.
</p>

<p align="center">
  <a href="https://cluby.cash"><img alt="cluby.cash" src="https://img.shields.io/badge/cluby.cash-03926B?style=for-the-badge&logoColor=white"></a>
  <a href="https://x.com/ClubyTech"><img alt="@ClubyTech" src="https://img.shields.io/badge/@ClubyTech-002C1E?style=for-the-badge&logo=x&logoColor=white"></a>
  <a href="https://github.com/clubytech/cluby"><img alt="source" src="https://img.shields.io/badge/source-40C09C?style=for-the-badge&logo=github&logoColor=002C1E"></a>
</p>

<p align="center">
  <img alt="Markets" src="https://img.shields.io/badge/markets-35_live_/_43_planned-0FAF83?style=flat-square">
  <img alt="Chain" src="https://img.shields.io/badge/chain-Robinhood_4663-03926B?style=flat-square">
  <img alt="Custody" src="https://img.shields.io/badge/custody-none-002C1E?style=flat-square">
  <img alt="Performance fee" src="https://img.shields.io/badge/performance_fee-0%25-40C09C?style=flat-square">
</p>

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/clubytech/clubytech/output/snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/clubytech/clubytech/output/snake-light.svg">
  <img alt="Contribution graph" src="https://raw.githubusercontent.com/clubytech/clubytech/output/snake-dark.svg">
</picture>

</div>

---

### We did not write a lending protocol

Deposits, collateral, debt and liquidations live inside **Morpho Blue** — immutable, audited, and impossible for us to upgrade or reach into. What we build is the curation layer above it: the markets, the oracles, the risk parameters, the routing.

Nothing here takes custody. Routers hold no balance between transactions, and the liquidator funds itself entirely from flash loans — which is why the protocol needs no treasury standing behind it.

> **Your money sits in code that cannot change, and our code cannot touch it.**

**35 isolated markets, live.** Liquidation thresholds and oracles are fixed when a market is created and cannot be edited by anyone, us included — an LLTV is part of a market's *identity*, not its storage, so changing one does not edit a market, it names a different market that does not exist.

---

### <img src="assets/mark.png" width="20" align="center"> [cluby](https://github.com/clubytech/cluby)

The whole thing. Three oracles, a flash-loan liquidator, a leverage router, a keeper, an MCP server, and 101 tests.

| | |
|---|---|
| **A TWAP that checks its own pool** | It refuses to deploy against a pool whose observation ring is too short for its own window. Most do not check, and a pool that cannot answer a thirty-minute question will happily answer a wrong one |
| **A liquidator with a floor** | It reads a price from the oracle *at the moment it acts* and will not sell collateral more than 8% below it. A liquidator with no floor dumps into a thin pool and hands the difference to whoever is on the other side |
| **A keeper that can only subtract** | It cannot open a position, move liquidity, change a parameter, or touch user funds. Every power it has reduces exposure |
| **An MCP server** | So an agent can read the protocol directly — markets, positions, and pre-trade quotes computed by the same arithmetic the interface signs against |

---

### Four things that cost real money to learn

Each of these is a comment in the code, not a blog post.

**A tokenized stock can lie about its own balance.** Twelve of the 203 tokenized equities on this chain carry a display multiplier that is not one — one holds a single unit and shows you four. Read it as a quantity and you misprice collateral fourfold, and never notice until a liquidation fails to clear.

**A Uniswap pool remembers about one minute by default.** A thirty-minute TWAP against a sixty-second observation ring is a number that looks like a price. Extending the ring is permissionless, not free, and nobody's job — so it does not get done.

**A call into an address with no code reverts with *empty* data.** No reason string, which reads downstream as "this market is broken" rather than "this deploy is broken".

**`cast send` exits 0 on a transaction that mined and reverted.** Over the node's per-transaction gas ceiling a transaction is not rejected — it is mined, burns the entire limit, and moves nothing.

---

<p align="center">
  <a href="https://cluby.cash"><b>cluby.cash</b></a> ·
  <a href="https://cluby.cash/docs">docs</a> ·
  <a href="https://github.com/clubytech/cluby">source</a> ·
  <a href="https://x.com/ClubyTech">@ClubyTech</a>
</p>
