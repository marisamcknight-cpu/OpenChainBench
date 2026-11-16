# Pull request draft: add True Markets to the Hyperliquid frontends bench

Target repo: https://github.com/ChainBench/OpenChainBench
Base branch: `dev` (their rules say feature branches go to `dev`, not `main`)
Branch name: `feat/add-true-markets-builder`
Commit message: `add true markets to hyperliquid frontends registry`

---

## Title

add true markets to hyperliquid frontends (bench 030)

## Description

Adds True Markets as a tracked builder on the Hyperliquid frontends bench.

**Builder**

- Name: True Markets
- Site: https://truemarkets.co
- X: @truemarketsco
- Builder address: `0x7bc2baaf2c79d9be1f5c327b5fb5325583604734`
- Fee schedule: https://truemarkets.co/fees (last updated 2026-11-12). 0.25% per trade on the web and mobile app, 0.20% through the CLI, MCP server and Gateway API.
- Builder fee per fill on Hyperliquid: 0 according to True Markets, nothing is added on top of Hyperliquid's own fees. The address still shows about $172 of builder rewards, so some fills have carried a nonzero builder fee. I did not read the per-fill bp from the public bucket; please correct the note if the fills show something different.
- Address evidence: HypurrScan labels the address True Markets and shows about $172 of builder fee rewards (read 2026-11-16). https://hypurrscan.io/address/0x7bc2baaf2c79d9be1f5c327b5fb5325583604734

True Markets is a self-custodial trading app and API for tokenized stocks, crypto and perpetuals. The perp orders it routes to Hyperliquid carry this builder address. I am submitting this on behalf of True Markets, the operator.

**Changes**

- `harnesses/hyperliquid-frontends/builders.json`: new registry entry, slug `true-markets`.
- `benchmarks/hyperliquid-frontends.yml`: provider block for `true-markets`, same queries as the other builders.
- `src/data/provider-registry.ts`: url, description and X handle.
- `src/lib/logo-manifest.ts` and `public/logos/true-markets.png`: logo supplied by True Markets (200 px PNG).

**Verification**

- `valid_from` is 2026-06-10, the day the address was first funded on HyperCore: a system send of 199.96 USDC from HyperEVM at 21:38 UTC. https://hypurrscan.io/tx/0xc918b2bf21d362a1ca92043d6dae6002011d00a4bcd681736ce15e11e0d73c8c
- I did not check the public fills bucket. The first day with a file can only be 2026-06-10 or later, so please adjust `valid_from` if your check finds a later date.
- `pnpm validate` passes (249 specs valid). `pnpm typecheck` passes.

---

## Registry entry as drafted

```json
{
  "slug": "true-markets",
  "name": "True Markets",
  "address": "0x7bc2baaf2c79d9be1f5c327b5fb5325583604734",
  "valid_from": "2026-06-10",
  "notes": "True Markets (truemarkets.co), a self-custodial trading app and API for tokenized stocks, crypto and perpetuals; the perp orders it routes to Hyperliquid carry this builder address. Builder address from the operator; HypurrScan labels the address True Markets and Hyperliquid's referral info for it reports about $172 of builderRewards (read 2026-11-16). Fee schedule published at truemarkets.co/fees, last updated 2026-11-12: 0.25% per trade on the web and mobile app, 0.20% through the CLI, MCP server and Gateway API; builder fee from the operator: 0, nothing is added on top of Hyperliquid's own fees. The builderRewards figure means some fills have carried a nonzero builder fee; the bp per fill was not read from the public bucket. valid_from is from the operator: the day the address was first funded on HyperCore, a system send of 199.96 USDC from HyperEVM on 2026-06-10 at 21:38 UTC (tx 0xc918b2bf21d362a1ca92043d6dae6002011d00a4bcd681736ce15e11e0d73c8c). The first day the public fills bucket returns a file was not checked and can only be that day or later."
}
```

## How to open it

1. Fork https://github.com/ChainBench/OpenChainBench on GitHub.
2. Create the branch from `dev`: `git checkout dev && git pull && git checkout -b feat/add-true-markets-builder`
3. Apply the patch: `git apply add-true-markets-builder.patch`
4. Run `pnpm install && pnpm validate && pnpm typecheck`.
5. Commit, push to the fork, and open the pull request against `dev` with the title and description above.
