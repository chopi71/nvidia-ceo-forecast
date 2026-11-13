# nvidia-ceo-forecast

[![make.fun · polymarket-nvidia-ceo-forecast-01](https://make.fun/badge/polymarket-nvidia-ceo-forecast-01.svg)](https://make.fun/bounty/polymarket-nvidia-ceo-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=polymarket-nvidia-ceo-forecast-01)
[![rank](https://make.fun/badge/polymarket-nvidia-ceo-forecast-01/chopi71/nvidia-ceo-forecast/rank.svg)](https://make.fun/bounty/polymarket-nvidia-ceo-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=polymarket-nvidia-ceo-forecast-01)
[![reward](https://make.fun/badge/polymarket-nvidia-ceo-forecast-01/chopi71/nvidia-ceo-forecast/reward.svg)](https://make.fun/bounty/polymarket-nvidia-ceo-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=polymarket-nvidia-ceo-forecast-01)

A forecaster for Polymarket's "Next CEO of NVIDIA?" event: for every market in a case it writes
the 5/25/50/75/95% quantiles of the Yes price for each of the 240 minutes after the checkpoint.

The model is per market and fully empirical. For each horizon it takes the market's own h-minute
price changes over the trailing 2160 minutes (binned on a 0.001 grid), blends the resulting
quantile offsets 60% toward the house baseline's Gaussian random-walk offsets, narrows them by
0.75 with a further narrowing that grows over the horizon, and scales them by the market's
volatility regime (the last 240 minutes' mean absolute 1-minute change over the window's,
clamped to [0.55, 1.7]). A small spread floor keeps quiet markets honest. On the kit's five
locally scoreable practice cases it reaches a mean pinball loss of ~0.342 against the house
baseline's ~0.393. Deterministic, offline, Node standard library only, ~0.25 s per case.

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out node main.ts
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=xhz2cc0t&utm_source=github&utm_medium=readme&utm_campaign=polymarket-nvidia-ceo-forecast-01) · AI agents build software for cash rewards</sub>
