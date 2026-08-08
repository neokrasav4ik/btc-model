# Bitcoin price model

An interactive page: three layers, four sliders, three diagnostics, six falsification criteria.

**Open the model →** https://neokrasav4ik.github.io/btc-model/en.html

**Русская версия →** https://neokrasav4ik.github.io/btc-model/ · [README на русском](README.md)

## What this is

Price is decomposed into three layers multiplied by one another.

**1. A power law** in network age, `P ∝ t^3β`. It runs the decades. The exponent 5.69 was never fitted to the chart: it is assembled from two separately measured quantities — address count against time (a cube) and value against address count (β = 1.897).

**2. Saturation** against a limiting number of owners. It decides how everything ends. The plateau level follows from the audience ceiling through `plateau = 657,000 · (W/1610)^β`; at the base ceiling of 1610 M owners that is $657k.

**3. Halving cycles** with the top and the bottom decaying independently. These are the four-year waves inside. Peak 18 months after the halving, trough at 26–30, return to trend by the next halving.

The third layer is tied to the second by a multiplier ζ:

```
ζ = d_e + (1 − d_e)·φ        φ = g(with saturation) / g(pure power law)
```

φ is the share of the inflow of new participants that survives saturation. The peak of the cycle is made by arrivals, so euphoria fades as the audience is exhausted. Swings among those who already own require no inflow, and the share of them that outlives the exhaustion is set by the euphoria decay slider. The link introduces no new constants. At all four historical epochs φ = 1.00 — saturation had not switched on before 2026, and the calibration of layers 1–2 is untouched.

## Sliders and scenarios

The sliders do not pick a desired number. They switch between hypotheses about what happened to the market in the last cycle: was the disappearance of euphoria an irreversible change or a fluke.

The four presets sit on a single axis — maturity on the left, speculation on the right:

| Scenario | Ceiling | Euphoria decay | Panic decay | Plateau | H5 peak | H5 trough | Drawdown |
|---|---|---|---|---|---|---|---|
| Cycle faded | 1800 | 0.00 | 1.00 | $812k | $384k | $303k | 21% |
| **Quiet cycle** (base) | 1610 | 0.15 | 0.50 | $657k | $394k | $245k | 38% |
| Cycle returns | 1350 | 0.50 | 0.25 | $470k | $408k | $201k | 51% |
| Cycle never broke | 1300 | 1.00 | 0.00 | $438k | $510k | $154k | 70% |

The column of peaks rises to the right along with the drawdown: a high peak in 2029 points to a live cycle, which will be followed by the customary crash.

## Diagnostics

Three indicators check the reader's settings while advising nothing.

**Decay consistency.** It catches one specific inconsistency: euphoria fading irreversibly while panic does not fade at all. The cause that killed the top is obliged sooner or later to reach the bottom, and no mechanism sits under such a pair.

**Share of amplitude by epoch.** Shows ζ for H5–H7: what the 2030s cycle rests on — the surviving inflow, or the premise that the speculative character of the asset survived on its own.

**Misses from the trend.** How many months lie further than ±0.5 dex from the trend. At the measured β there are 14 of 194; shifting β by one tenth brings that to 26. The claim that β was measured rather than chosen is not taken on trust.

## Data

194 monthly observations from July 2010 to early August 2026 — approximate month closes from public sources. The series sits in the page source in plain text, the array `OBS`. That is enough for the shape of the residual and not enough for anything requiring precision.

The Metcalfe exponent β = 1.897 comes from external work rather than from fitting.

The estimate of the number of owners (106 M as of August 2026) is a digest of industry estimates rather than a census, and it is the weakest point of the model. Different methodologies give anywhere from 106 M (on-chain and exchange accounts) to 450 M (surveys that include indirect exposure through funds). The multiplier ζ does not depend on that estimate: φ is a ratio of two growth rates, and the level anchoring does not enter it.

## What could falsify this

Six conditions, from the nearest to the most distant. Two are worth naming here.

**Price settles below $58,000.** Then late June 2026 was not the trough of the cycle, and with it collapses the lower node of H4 — the one the decay amplitude is set by.

**Non-zero addresses grow more slowly than `3/t` for more than two years.** The exponent 5.69 = 3 × 1.897 rests on the cubic growth of the network, so this checks the slope rather than cycle amplitude. At a network age of 17.6 years the model requires 17.0% per year: from today's 57 M to 68 M in a year and 80 M in two. The one criterion checked monthly, for free, and on-chain, with no argument about who counts as an owner.

The other four are on the page, in the "Falsification" section.

## How to run

The page is fully static and works offline. Open `index.html` (or `en.html`) in a browser — no build, no server, no dependency installation. All computation happens in the browser and no request leaves the page.

The model takes about fifty lines of JavaScript in the source. Key functions: `pure` (the power law), `sat` (the saturation envelope), `plateau` (plateau level from the number of owners), `phiAt` and `zetaAt` (the link between the cycle and the inflow), `amps` (projection of amplitudes onto H5–H8), `modAt` (the cycle overlay).

## Dependencies

- [Chart.js](https://www.chartjs.org) 4.4.1 (MIT) — rendering, file `chart.umd.js`
- [IBM Plex](https://github.com/IBM/plex) (SIL OFL 1.1) — fonts, folder `fonts/`

Both are bundled locally. The page makes no external requests.

## Sources

- Santostasi, G. & Perrenod, S. (2026). *A Mechanistic Derivation of the Bitcoin Price Power Law.* Zenodo. [10.5281/zenodo.19387099](https://doi.org/10.5281/zenodo.19387099)
- Brause, D. (2026). *The Information Coherence Hypothesis.* Zenodo. [10.5281/zenodo.18812955](https://doi.org/10.5281/zenodo.18812955)

## Licence

Text and model — [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The libraries keep their own licences.

**Disclaimer.** An analytical model, not investment advice. The forecast assumes the power-law regime holds and that no structural discontinuities occur in the adoption mechanism.
