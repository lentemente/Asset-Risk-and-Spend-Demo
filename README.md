# Risk-Based Investment — Network Asset Demonstrator

An interactive, single-page demonstrator of a risk-based approach to electricity
distribution asset investment. It shows that, for the same budget, weighting renewal by
the **consequence** of failure (safety and reliability impact × zone) removes more
high-impact failures than renewing the worst-condition assets alone.

Three views:

1. **Current vs risk-based** — the same spend, allocated two ways, with the resulting
   safety and reliability failure matrices side by side.
2. **Move the investment** — scale the programme up or down by a percentage and watch
   risk respond and the spend redistribute across fleets.
3. **Set a risk target** — choose a maximum acceptable number of high-impact failures
   and get the minimum investment that meets it.

The figures are illustrative. The subject is the method, not a model of any real
network — an internal synthetic fleet of ~64,700 assets across seven volumetric types
(transformers, 11 kV and 33 kV overhead lines and cables, support structures, and
switchgear) is generated once and held fixed.

## View it locally

Open `index.html` in any modern browser. No build step, no dependencies, no server.

## Publish on GitHub Pages

1. Create a repository and add `index.html` (and this `README.md`) to it.
2. In the repository, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose your
   default branch (e.g. `main`) and the `/ (root)` folder, then **Save**.
4. After a minute, the site is live at `https://<your-username>.github.io/<repo-name>/`.

## How the model works

Failure follows a Weibull hazard (shape 3) whose characteristic life is each fleet's
expected life, scaled so year-0 expected failures match a target (~245 total), across a
realistic spread of ages. Each asset has a fixed safety and reliability impact grade and
a zone (1–5); 33 kV assets sit mostly in higher reliability zones. Matrix cells are
grouped into three risk bands (Low / Medium / High) by impact and zone, and the figures
are expected failures per year per band.

Replacement uses real unit rates (transformers $30k, switchgear $35k, overhead $100k/km,
cables $1M/km, support structures $10k). The base spend is set from fleet lives — about
three-quarters of the steady-state renewal rate, ~18% of the fleet over ten years. The
**end-of-life** method renews the most life-expired assets first; the **risk-based**
method renews highest risk-reduction-per-pound first. At the same budget the end-of-life
method replaces far more (cheaper) assets, while risk-based concentrates on
high-consequence overhead and clears the zone-5 corner. The ten-year plan ages the fleet
each year and sizes the smallest risk-based investment that holds the chosen zone-5
target. A **deliverability cap** (no fleet renewed faster than 3× its natural life-based
rate) keeps the risk-based programme from concentrating entirely on overhead and spreads
it across cables, supports and switchgear; the **Move the investment** view also lets you
toggle individual fleets in or out of the spend. The constant `DELIVERABILITY` near the
top of the script is the single tuning point for that cap.
