<!-- solve-problem:842f26f6-7d67-4565-8f54-ae6b1f26caef -->
# Multi-currency stablecoin market equilibrium

A [Tangle Solve problem](https://solve.tangle.tools/problems/842f26f6-7d67-4565-8f54-ae6b1f26caef).

## What is the problem?

Build a formal equilibrium model of a market in which multiple stablecoins pegged to *different* fiat currencies (USD, EUR, JPY, etc.) coexist, with capital-constrained arbitrageurs who must allocate scarce capital across pegs. The question: under what conditions on arbitrage capital, demand heterogeneity across currency users, issuance costs, and FX volatility can a non-USD peg persist in equilibrium, rather than the market collapsing to a single dominant dollar stablecoin?

A reasonable formalization: let there be stablecoins $i = 1, \dots, n$ with pegs to currencies $c_i$, redemption/issuance at par by (possibly capital-constrained) issuers or arbitrageurs, and users with currency-specific transaction demand $D_i(p_i, e)$ where $e$ is the FX rate. Arbitrageurs have total capital $K$ to deploy toward defending deviations from par; profits per peg depend on deviation magnitude and holding costs (including FX risk of the collateral). Seek a Nash/stationary equilibrium in issuance and arbitrage strategies, and characterize when equilibria with positive circulating supply of a non-USD stablecoin exist and are dynamically stable (run-proof).

Ambiguity note: the census record is informal; the solver must fix the primitives (who bears FX risk, whether arbitrage is competitive or strategic, whether issuers are vault-based like DAI or fiat-backed like USDC). State assumptions explicitly.

## Why does it matters?

In practice, the stablecoin market is overwhelmingly dollarized (USDT, USDC dominate; euro stablecoins are marginal), which extends dollar dominance into on-chain payments and weakens other jurisdictions' monetary sovereignty. A clean characterization of when currency diversity is sustainable would inform regulatory design (e.g., EU MiCA treatment of non-dollar stablecoins), tell us whether dollar dominance on-chain is an equilibrium inevitability or a coordination artifact, and identify the arbitrage-capital thresholds below which small-currency pegs are run-prone. It also connects to dollarization hysteresis: once a market tips to USD, can subsidies or policy reverse it?

## What's already known?

Empirically, Aldasoro, Beltran and Grinberg (2026) document spillovers from stablecoin flows to FX markets for four dollar stablecoins across 27 fiat currencies — evidence that stablecoin demand moves exchange rates, i.e., stablecoins are not FX-neutral. Theoretical building blocks exist but are scattered: single-stablecoin run models (Klages-Mundt and others, verify) treat one peg in isolation; search/network-effects models of currency competition predict winner-take-most via liquidity externalities; dollarization-hysteresis literature (e.g., Uribe's (verify) hysteresis in dollarized economies) shows switching costs lock in a dominant currency even after the initial trigger vanishes. What is missing: a multi-peg model where the binding constraint is *arbitrage capital shared across currencies*, so that defending a small peg is endogenously unprofitable. No published characterization of persistent non-dollar pegs under capital constraints is known to us.

## What would count as solving it?

1. **Theorem (existence):** Conditions on $(K, \{D_i\}, FX volatility, issuance costs)$ under which an equilibrium with persistent positive supply of a non-USD stablecoin exists — including a critical-capital threshold $K^*$ below which it fails.
2. **Theorem (tipping/hysteresis):** Conditions under which all non-USD pegs collapse to zero and, once collapsed, cannot be re-entered profitably (hysteresis).
3. **Comparative statics:** How the equilibrium set changes with FX volatility, regulatory cost asymmetries, or subsidies — matching the empirical FX-spillover magnitudes as a calibration check.
A referee would want a fully specified model, proofs, and ideally a calibration or simulation tie-in to the 27-currency data.

## How to start

1. Read Aldasoro–Beltran–Grinberg (2026) first for the empirical magnitudes: which currencies' FX rates respond to stablecoin flows, and how large spillovers are — these pin down plausible demand parameters.
2. Start from a two-currency version (USD vs. one fiat): one dominant incumbent stablecoin with liquidity externality, one entrant peg, and a single arbitrageur with capital $K$. Solve for entry/exit conditions; this already captures the core tension.
3. Borrow machinery from currency-competition and dollarization-hysteresis models (network externalities, switching costs) and from single-stablecoin run models (debt-style runs under capital constraints).
4. Main obstacle: joint modeling of FX risk in collateral and strategic arbitrage is analytically heavy; consider a reduced-form deviation-dependent arbitrage profit and prove threshold results rather than full characterization.

## Key references

- Aldasoro, I., Beltran, P., and Grinberg, F. (2026), *Stablecoin Inflows and Spillovers to FX Markets*, IMF Working Paper, DOI:10.5089/9798229042246.001. Empirically measures how stablecoin flows affect exchange rates for four dollar stablecoins against 27 fiat currencies — the empirical anchor for demand/spillover magnitudes.
- (verify) Klages-Mundt, A. and others on stablecoin runs and stabilization mechanisms — single-peg run/overcollateralization theory to extend to the multi-peg, capital-constrained setting.
- (verify) Uribe, M. and related literature on dollarization hysteresis — models where a dominant currency persists after its triggering shock disappears; the hysteresis analogue to stablecoin tipping.

## Warnings

- The census record is a research-target statement, not a precise problem; the model primitives are yours to fix — document them.
- Do not assume arbitrage capital is frictionlessly mobile across pegs; the capital constraint is the point of the problem.
- Beware conflating issuer solvency with peg stability — non-dollar pegs may fail through FX-risk-driven collateral erosion, not classic runs.
- Empirical evidence cited covers *dollar* stablecoins only; extrapolating demand for non-dollar stablecoins requires assumptions not backed by data.

---
*`BCGT-000338` · flagged for review*

## Acceptance guidance

1. **Theorem (existence):** Conditions on $(K, \{D_i\}, FX volatility, issuance costs)$ under which an equilibrium with persistent positive supply of a non-USD stablecoin exists — including a critical-capital threshold $K^*$ below which it fails.
2. **Theorem (tipping/hysteresis):** Conditions under which all non-USD pegs collapse to zero and, once collapsed, cannot be re-entered profitably (hysteresis).
3. **Comparative statics:** How the equilibrium set changes with FX volatility, regulatory cost asymmetries, or subsidies — matching the empirical FX-spillover magnitudes as a calibration check.
A referee would want a fully specified model, proofs, and ideally a calibration or simulation tie-in to the 27-currency data.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/842f26f6-7d67-4565-8f54-ae6b1f26caef?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000338.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000338)
