# Redraft Trade Finder

Enter a player you're willing to trade away plus the position you need, and get ranked **fair 1-for-1 trade targets** priced off real redraft trade-calculator values.

## Data source
[FantasyCalc](https://fantasycalc.com/redraft-rankings) redraft market values — crowd-sourced from actual trades executed in Sleeper/MFL leagues, refreshed continuously. The app calls `api.fantasycalc.com/values/current?isDynasty=false&...` directly from the browser and adapts to your league settings (size, PPR, 1QB vs Superflex). If the API is unreachable it falls back to a bundled snapshot in `public/fallback-values.js`.

## Fairness model
`gap % = (target value − your player's value) / your player's value`

| Gap | Verdict |
|---|---|
| ≤ ±5% | Dead even |
| ±5–15% | One side wins slightly |
| ±15–25% | Likely counter-offer territory |
| > ±25% | Unlikely to be accepted 1-for-1 |

Three views: **Fairest** (smallest gap), **Slight win for me** (~9% in your favor — realistic to get accepted), **Biggest upgrade** (max value you can chase within 35%).

## Run
```bash
python3 -m http.server 3000 --directory public
```
Then open http://localhost:3000

Caveat: calculators price players against the market, not against your roster. Check bye weeks, injury status, and playoff schedules before sending.
