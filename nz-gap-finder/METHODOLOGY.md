# NZ Gap Finder — Methodology

A repeatable process for finding empty niches and underserved needs in New
Zealand: things NZ imports but doesn't make, services it's short on, software
categories nobody's built for the local market, and roles it can't hire for.
Each run produces a dated report in `reports/`.

## Categories tracked

1. **Business / product gaps** — goods or services NZ relies on imports for,
   or where local supply is thin relative to demand.
2. **Startup / software gaps** — SaaS/product categories common overseas with
   no good NZ-specific equivalent, or ecosystem-support gaps for founders.
3. **Public / social gaps** — infrastructure, housing, healthcare, and other
   public-good shortfalls documented by government or research bodies.
4. **Job market gaps** — occupations with sustained shortages (a demand
   signal that often points to an adjacent business opportunity, not just a
   hiring problem).

## Sources per category

| Category | Primary sources |
|---|---|
| Business/product | Stats NZ overseas merchandise trade releases, MBIE productivity/industry reports, Commerce Commission, Consumer NZ, industry association reports |
| Startup/software | NZ startup ecosystem press (e.g. startup-news roundups), Tracxn/funding trackers, founder communities, sector reports (AgTech, fintech, healthtech) |
| Public/social | Treasury infrastructure reports, Te Waihanga (Infrastructure Commission), HUD/Ministry of Housing, NZ Initiative and other think-tank research |
| Jobs | Immigration NZ Green List & skill shortage checklist, MBIE labour market reports, recruiter reports (Hays, etc.) |

## Scoring a candidate niche

Each candidate gets scored 1–3 on three axes, plus a confidence label:

- **Demand signal** — how strong/recent is the evidence this is actually
  needed (official stats > industry report > anecdote).
- **Supply gap** — how clearly under-served is it today.
- **Feasibility** — how approachable for a small operator/startup vs.
  requiring large capital or policy change.
- **Confidence**: *Low / Medium / High* — High means the signal shows up
  independently in 2+ categories or sources (e.g. a shortage that appears in
  both the jobs list and startup-ecosystem commentary is more robust than
  either alone).

## Cadence

Re-run weekly. Because official trade/labour data updates monthly/quarterly,
most weeks will refine or reweight existing candidates rather than surface
entirely new ones — that's expected, not a failure of the process.

## Known limitation

Web search surfaces reports and commentary well but doesn't give
line-item Stats NZ trade-code data or Trade Me/Seek listing volumes directly.
Category 1 (business/product) is currently the weakest-evidenced category as
a result — a future improvement would be pulling Stats NZ's Infoshare trade
data directly for import-heavy/no-local-producer product codes.
