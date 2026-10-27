# ECO731 Research Proposal — Working Notes

_Last updated: 2026-10-09. Summary of planning sessions with Claude._

## Assignment (from FCH + instructor email, both PDFs in this repo)

- **Deadline:** 11:59 PM IST, **Saturday 14 Nov 2026** (hard; −5 points per late day). Worth **40%**.
- No word limit. Individual or group of 2–3 (default = referee-report group).
- **Required sections:**
  1. **Introduction** — precise research question + why it matters (data, anecdotes, policy relevance).
  2. **Literature review** — closest papers; how my question/approach differs.
  3. **Analysis overview** — no results needed, but must be logically sound and achievable.
     - Theory: model setup (agents, objectives, constraints), **mechanism** (the key component per instructor), solution steps, likely roadblocks.
     - Empirics: dataset + source, variables, identification strategy.
- Office hours for feedback: **Wednesdays 4–5 PM, 428 ESB2**.
- Academic misconduct = automatic F → writing must be my own.

## Topic direction: public debt / front-loading

**Starting point (from lectures):** in the planner's solution (Battaglini & Coate 2008; also Aiyagari, Marcet, Sargent & Seppälä 2002), the government front-loads taxes and accumulates assets until the interest on them finances the public good, after which taxes are zero.

**Puzzle:** real governments almost never do this. Most carry debt (India general government debt about 80% of GDP). Exceptions: Norway's sovereign wealth fund (about 3% spending rule), Gulf funds, Chile's stabilisation fund.

### Comparative statics of the planner benchmark

Why front-loading happens (Euler condition: MCPF_t = β(1+r) E[MCPF_{t+1}]):
- Case 1: β(1+r) > 1 (planner more patient than market) → MCPF falls → taxes fall to 0.
- Case 2: β(1+r) = 1 + spending uncertainty (BC 2008) → precautionary accumulation.
- If deterministic with β(1+r) = 1 → pure Barro tax smoothing, no accumulation.
- **TODO: check which version my lecture notes use.**

MCPF with linear labour tax: MCPF(τ) = (1−τ) / (1 − τ(1+ε)); revenue-max tax = 1/(1+ε).

Asset target: r · a* = p · g_S(A_H) (interest covers Samuelson level in high-need state).

| Parameter ↑ | Asset target a* | Speed to zero taxes |
|---|---|---|
| Interest rate r | ↓ (∝ 1/r) | ↑ faster |
| Labour elasticity ε | no change | ↓ slower (higher deadweight loss of front-loading); at ε→0 no reason to accumulate at all |
| Value of public good A, α | ↑ | ↓ |
| Spending volatility | ↑ | ↓ |
| Wage / tax base w | no change | ↑ |
| Initial debt b₀ | no change | ↓ |
| Patience β (case 1) | — | ↑ |

Link: at low r the target explodes → connects to Blanchard (2019) r < g debate.

## Proposed proposal structure (recommended option)

**Research question:** Why don't governments accumulate assets to finance public goods as the optimal-taxation benchmark prescribes, and what institutional features let some (e.g. Norway) do so?

**Contribution / extension:** political turnover + fund-raiding risk.
- Incumbent survives with probability q.
- Successor can divert fraction φ of accumulated assets (φ = institutional protection of the fund; low for Norway).

**Model sketch:**
- Citizens: u = c + A·v(g) − h(l), labour elasticity ε.
- Budget: p·g_t + (1+r)·b_t = τ_t·w·l(τ_t) + b_{t+1} (b < 0 means assets).
- Two parties differing in public-good valuation or rents; Markov-perfect equilibrium (as in BC 2008).

**Mechanism:** effective return on saving for the incumbent ≈ (1+r)[q + (1−q)(1−φ)]. If this falls below 1/β, front-loading stops being optimal → may even borrow; zero-tax endowment never reached.

**Predictions to derive:**
- Threshold q (or φ) above which governments accumulate.
- Lower r raises that threshold.
- Effect of ε — need to work out the sign.
- Policy: optimal fund-protection rule φ.

**Solution steps:** (1) two-period closed form → threshold condition; (2) infinite horizon generalised Euler equation; (3) numerical value function iteration for comparative statics in r, ε, q.

**Roadblocks:** existence/uniqueness of Markov equilibria; generalised Euler equation hard analytically; endogenising q via probabilistic voting (Lecture 20) adds complexity.

**India angle:** states' Consolidated Sinking Fund (CSF) at RBI = small-scale version. (Alternative empirical idea: do higher CSF contributions lower SDL spreads? Data: RBI *State Finances*, SDL auction results; verify CSF guideline change dates.)

### Literature (verify every citation before using)

| Group | Papers | How mine differs |
|---|---|---|
| Benchmarks | Barro (1979), Lucas & Stokey (1983), Aiyagari et al. (2002) | add politics to the planner |
| Political economy of debt | Persson & Svensson (1989), Alesina & Tabellini (1990), Battaglini & Coate (2008) | focus on why *assets* aren't built up; role of φ |
| Common pool / fiscal rules | Tornell & Lane (1999), Halac & Yared (2014), Azzimonti (2011) | not about the zero-tax endowment path |

**Closest paper: Alesina & Tabellini (1990)** — must clearly state how mine differs.

**Overlap warning (2026-10-21): Battaglini & Coate (2008) already partly answers "why no zero-tax endowment".** In their political equilibrium (legislative bargaining, pork for minimum winning coalitions), debt settles at a level above the planner's and the asset-accumulation path is not followed. Their mechanism is *within-period* (common pool / pork makes extra revenue go to pork instead of saving). Mine is *between-period* (turnover + raiding of the stock of assets, φ). Must say this explicitly in the lit review and the intro. Re-read BC (2008) Sections on the planner vs political equilibrium to confirm.
- No 2025 Battaglini paper on debt found (searched 2026-10-21; his site was not reachable from the session). Recent items found: tax evasion/tax professionals (JEEA, accepted 2025), ML tax auditing (J. Econometrics 2025), volunteer's dilemma (JPubE 2025), "Bargaining over taxes and entitlements" (IER, 2023). Ask the student for the exact title if they meant a specific one.

### Other ideas considered (backups)
- Time inconsistency: a government holding assets is tempted to change policy (Lecture 11, Lucas–Stokey).
- Credit-constrained heterogeneous households → positive optimal debt (Aiyagari & McGrattan 1998).
- General equilibrium: asset accumulation pushes down r in a closed economy.

## Model build: version 1 (two-period, started 2026-10-21)

**Simplifications:** 2 periods; spending fixed at G each period (no g choice yet); start with zero debt; period-1 government is benevolent; it survives with prob q, and if it loses, the successor takes share φ of the fund (lost to citizens). Debt cannot be "raided", so φ applies only to positive assets.

**Blocks:**
- Household: max (1−τ)wl − h(l) → l(τ) = (w(1−τ))^ε; revenue R(τ) = τ·w·l(τ).
- Cost of raising one more rupee: λ(τ) = MCPF = (1−τ)/(1−τ(1+ε)), rising in τ → reason to smooth taxes.
- Budgets: R(τ₁) = G + s; R(τ₂) = G − (1+r)s if the incumbent survives, G − (1−φ)(1+r)s if not.
- Optimal saving (s > 0): λ(τ₁) = β(1+r)[q·λ(τ₂^stay) + (1−q)(1−φ)·λ(τ₂^lose)].

**Threshold (evaluate at s = 0, where τ₁ = τ₂):** saves iff (1−q)·φ < κ, where κ = 1 − 1/(β(1+r)).
- (1−q)φ = expected share of the fund lost; κ = how much more patient the planner is than the market.
- Lower r → smaller κ → harder to save. ε does **not** enter the threshold (it only changes *how much* is saved).
- Numbers: β = 0.96, r = 5% → κ ≈ 0.8%, so even a tiny expected loss stops saving. Checked numerically (Claude, scratch script): matches.

**Logic check: version 1 gives "no saving", not "debt".** Above the threshold the government sits at s = 0 (balanced budget), because borrowing still costs the full (1+r). To explain *debt* (India), version 2 needs one more ingredient, e.g. successor values spending differently (Alesina & Tabellini 1990) or β(1+r) < 1. Sharpens the contrast: A&T explain debt; this model explains the absence of assets.

**Next:** (1) student re-derives the Euler condition and threshold in own words; (2) pick the version-2 ingredient; (3) add the choice of g; (4) infinite horizon / Markov.

## Model build: version 2 (disagreeing successor, 2026-10-22)

**Change from v1:** two parties, A and B, each values only its own public good (Alesina–Tabellini style); both care about tax distortions. Government now chooses g each period: A·v′(g) = λ(τ). A governs in period 1; in period 2, A with prob q, B with prob 1−q. If B wins and there are assets, B takes share φ first (as before). Same A, v, ε for both parties (symmetry), so at b = 0 all tax rates are equal.

**Key new object, s (share paid by taxes):** when the period-2 government has to repay one more rupee of debt, it covers a share s by raising taxes and 1−s by cutting its own spending. 0 < s < 1. Define **d = 1 − s** (polarisation / disagreement: the share of the debt burden that lands on spending A doesn't value).
- From B's FOC: s = 1 / (1 + λ′(τ) / (−A·v″(g)·R′(τ))).

**Euler (A in period 1):** λ(τ₁) = β(1+r)[q·λ(τ₂^A) + (1−q)·s·λ(τ₂^B)], with (1−φ) on the B-term when b < 0.

**Three regimes (evaluated at b = 0), κ = 1 − 1/(β(1+r)):**
- **Borrow** (India) iff (1−q)·d > κ
- **Save** (Norway) iff (1−q)·[d + φ(1−d)] < κ
- **Balanced budget** in between. The band exists only because φ > 0, and it widens with φ.
- v1 is the special case d = 0.

**Results to state:**
- Turnover (low q) and polarisation (high d) → debt. Raiding risk (φ) → no assets, but φ alone cannot create debt.
- Disagreement alone (φ = 0) already lowers the value of saving: the successor spends part of the fund on its own good.
- φ is an institutional/legal parameter (can be legislated); d and q are political → the policy lever is φ.
- ε now matters: higher ε → λ rises faster → s smaller → d larger → more debt. (Numerically: d ≈ 0.014, 0.028, 0.058 for ε = 0.25, 0.5, 1 with v = log, A = 0.05.) Sign is clear in this example; check whether it holds generally.
- β(1+r) = 1 (κ = 0): any q < 1 gives debt (pure A&T result).

**Checked numerically** (Claude, scratch script, β = 0.96, r = 5%, v = log): predicted regime matched the grid-search optimum in all 17 cases tried.

**Contrast with literature:** A&T (1990) = d channel (debt). BC (2008) = within-period pork. New piece = φ (raiding of the stock) and the balanced-budget band it creates; plus combining both to get all three regimes in one model.

**Next:** student re-derives s and the three conditions; draw the regime map (q on x-axis, φ on y-axis); then (c) infinite horizon / Markov.

## Model build: version 3 (infinite horizon, Markov, 2026-10-22)

**State:** debt b (negative = assets). Parties symmetric, so we only need two value functions:
- V(b) = value to the party **in power** facing debt b.
- W(b) = value to the party **out of power** when debt is b.

**Timing each period:** election (incumbent stays w.p. q; on turnover, assets shrink to (1−φ)·b) → party in power picks τ, g, b′ → budget g + (1+r)b = R(τ) + b′.

**Bellman equations:** T(b) = (1−φ)b if b < 0, else b.
- V(b) = max over (τ, g, b′) of U(τ) + A·v(g) + β[q·V(b′) + (1−q)·W(T(b′))]
- W(b) = U(τ*(b)) + β[q·W(b*(b)) + (1−q)·V(T(b*(b)))], using the incumbent's choices τ*, b*.

**Markov-perfect equilibrium:** a policy rule b*(b) such that, when everyone expects all future governments to use it, today's government finds it optimal to use it too.

**Generalised Euler equation (idea):** λ(τ_t) = β(1+r)·E[λ(τ_{t+1}) × (share of repayment paid through taxes, with (1−φ) after turnover)], plus a **strategic term**: how today's b′ changes what tomorrow's government will do. The strategic term is what makes it hard to solve analytically.

**Solution method:** value-function iteration on a grid (code/mpe_solver.py, exploratory, written by Claude): guess V and W → incumbent's best b′ for each b → update V and W → repeat.

**What the numbers showed (A = 0.15, ε = 0.5, r = 5%):**
- β(1+r) > 1 and φ > 0: long-run debt stuck at **exactly zero** (balanced budget) → the v1/v2 "band" survives in infinite horizon. Clearest result.
- β(1+r) = 1, φ = 0: q = 1 stays at b = 0 (Barro); q < 1 gives positive debt (A&T). Sensible.
- **Problems:** several cases did not converge (cycling); some cases jump to the debt limit; with β(1+r) > 1 and q = 1 the planner saves **without limit** (hits the grid edge).

**Logic issue found:** with β(1+r) > 1 and no uncertainty, the planner never stops saving (once taxes hit zero, extra assets fund ever more g). The "accumulate until interest pays for g, then stop" planner comes from BC (2008): β(1+r) = 1 **plus spending shocks** (precautionary saving). → For the infinite-horizon model, use BC's set-up (β(1+r) = 1 + shocks to A). Then φ works by **cutting the value of precautionary saving**. Keep the two-period κ > 0 version as the simple analytical illustration. Ask professor whether this is fine.

**Contraction? (2026-10-26):** not guaranteed in general (V and W feed into each other through the other party's choices). Options:
- **Special case that is a contraction:** no disagreement (d = 0), raiding = pure resource loss → W = V and one Bellman equation V(b) = max S + β[q·V(b′) + (1−q)·V(T(b′))] → Blackwell's conditions hold. Use as a benchmark (infinite-horizon version of v1).
- **Successor follows a fixed rule** (e.g. a fiscal rule / FRBM-style balanced budget after turnover) → incumbent's problem is single-agent → contraction. Links to extension 3.
- **Limit of finite-horizon equilibria:** undamped VFI from V = W = 0 *is* backward induction of a T-period game; each step is well defined, the question is whether it settles as T → ∞. Standard selection device.
- **Numerical aids (no guarantee):** damping, finer grid, small taste shocks to smooth choices, several starting guesses to check for multiple equilibria.

**Roadblocks (for the proposal):** (1) existence/uniqueness of MPE (non-convergence suggests possible multiple equilibria); (2) generalised Euler not solvable in closed form → numerical; (3) kink at b = 0 from φ (value function not smooth); (4) need shocks for a stationary distribution; (5) endogenous q (probabilistic voting) left for later.

## Professor's reply (email 2026-10-13, PDF in repo)

- Drop request accepted on Pingala (student has finished credit requirements). **Check:** does the 14 Nov course deadline still apply, or is this now an independent project with the professor?
- Sent Battaglini (2014, TE) and Battaglini (2026, TE) — both by the professor's doctoral advisor; the professor is thanked as an RA on the 2026 paper.
- Asked for forward/backward citation searches on Google Scholar from these two papers.
- Happy to talk after the mid-sem break; "continue polishing the idea".
- Student's own email framed the benchmark as **β(1+r) = 1 + spending uncertainty** (buffer motive) and focused on **Indian states** (CSF, Old Pension Scheme, anti-incumbency, alignment with the Centre). Consistent with the v3 logic fix.

## Tools from Battaglini (2014) and (2026) (read 2026-10-27)

**Battaglini (2014), "A dynamic theory of electoral competition" (TE 9: 515–554)**
- Economy = BC (2008): u = c + A·g^α − l^(1+1/ε)/(1+ε); δ(1+ρ) = 1; i.i.d. shocks to A; MCPF = (1−r)/(1−r(1+ε)); debt in [x_low, x_high], asset cap = −g_S(A)/ρ. → **adopt this economy for our infinite-horizon model** (fixes the β(1+r) > 1 problem).
- Planner: MCPF is a supermartingale → converges to full self-insurance (Prop 1).
- Elections: dynamic probabilistic voting (Lindbeck–Weibull / Persson–Tabellini 1999), uniform ideology shocks → party's problem reduces to a weighted-welfare problem (eq 13).
- **Political Euler = planner's Euler minus a wedge** (eqs 20–21: MCPF_t ≤ E[MCPF_{t+1}]). → write our result the same way: wedge from (q, φ, d).
- Value-function derivative as a probability-weighted mix of regimes (eq 18). → template for our kink at b = 0 (φ applies only to assets).
- Existence of a "well-behaved" (continuous, concave v) Markov equilibrium via a fixed-point theorem (Glicksberg–Fan), **not** a contraction (Prop 2).
- Key message: the political distortion shows up as **more volatile policies / imperfect self-insurance**, not necessarily higher debt (Prop 5). → matches our expected φ result.
- Institutions (district size m) as comparative statics. → analogue: φ.

**Battaglini (2026), "Chaos and unpredictability with time inconsistent policy makers" (TE 21: 241–280)**
- Two parties alternate in power (prob 1/2); durable state x_{t+1} = (1−γ)x_t + p_t; utility α·K·p − e(x), **α = how much the out-party values the in-party's spending** (α = 1: no conflict). ≈ our d (roughly α ↔ 1 − d).
- **Method:** split v(x) = [incumbent's objective] − [wedge (1−α)K/2·(y(x) − (1−γ)x)] (eq 7); envelope theorem on the first part → v′(x) depends on future policy slope y′(x) (eq 8); combine with FOC → **ODE for the policy function**, closed-form ψ(x, c) up to a constant c (eqs 9–11). Works with quasilinear utility.
- α = 1 → unique, well-behaved equilibrium (≈ our "no disagreement" contraction case). α < 1 → **continuum of equilibria** (indexed by c), possibly cycles of any period and chaos. → our non-converging VFI cases may be real cycling equilibria, not just numerical noise.
- Comparative statics need an equilibrium-selection assumption (fn 29: pick the "nearby" equilibrium).
- Sec 4.2: turnover ≈ a single agent with quasi-hyperbolic (β–δ) discounting. → our incumbent behaves like a present-biased agent with bias factor ≈ q + (1−q)(1−φ)·s; links to Harris–Laibson (2001) generalized Euler equations.
- Mapping to debt is not automatic: for us x = assets/debt grows at interest (γ = −r), and raiding makes the transition depend on turnover. Must check their conditions.

**Citation leads to check (from these papers; verify each):** Azzimonti (2011, AER, polarization + turnover → underinvestment, likely very close), Bai & Lagunoff (2011, policies affect turnover), Yared (2010), Klein, Krusell & Ríos-Rull (2008, GEE method), Krusell & Smith (2003, multiplicity), Harris & Laibson (2001), Persson & Tabellini (1999), Lindbeck & Weibull (1987), Battaglini & Coate (2007), Battaglini, Nunnari & Palfrey (2014), Barseghyan & Battaglini (2016). Also search: Azzimonti, Battaglini & Coate (balanced budget rules) for the FRBM extension.

## Citation search results (verified 2026-10-27)

**Backward (checked against the reference lists of the two papers; journal details match):**
Azzimonti (2011) AER 101: 2182–2204 · Bai & Lagunoff (2011) RES 78: 17–48 · Yared (2010) RES 77: 806–840 · Klein, Krusell & Ríos-Rull (2008) RES 75: 789–808 · Krusell & Smith (2003) Ecta 71: 53–73 · Harris & Laibson (2001) Ecta 69: 935–957 · Persson & Tabellini (1999) EER 43: 699–735 · Persson & Tabellini (2004) AER 94: 25–45 · Lindbeck & Weibull (1987) Public Choice 52: 273–297 · Battaglini & Coate (2007) AER 97: 118–149 · Battaglini, Nunnari & Palfrey (2014) AER 104: 2858–2871 · Persson & Svensson (1989) QJE 104: 325–345 · Lizzeri (1999) RES 66: 909–928 · Cao & Werning (2018) Ecta 86: 805–857 (hyperbolic discounting) · Cao & Werning, "Dynamic savings choices with disagreements", NBER WP 22007.
- Not in either list (dropped): Barseghyan & Battaglini (2016) — only a 2012 WP "Growth and fiscal policy" is cited.

**Content checked via search (abstracts):**
| Paper | What it does | Overlap with us |
|---|---|---|
| **Cao & Werning, NBER WP 22007 (2016)** | Alternating office-holders save/dissave; "disagreement index"; high disagreement → dissaving, low → saving; constant disagreement = hyperbolic discounting | **Very high** with v2 (d channel). Must read & cite. |
| **Amador (2003 MIT thesis; SED 2004 paper on sovereign debt repayment)** | Parties alternate; incumbent likely to lose is impatient → won't save; asset accumulation unsustainable | **Very high** with v1 (turnover → no saving). Exact title to confirm. |
| **Azzimonti (2011) AER** | Disagreement over spending composition → over-taxation, under-investment; worse with polarization; political stability mitigates | High (d and q), but about public capital, not a fund |
| **Azzimonti, Battaglini & Coate (2016) JPubE 136: 45–61** | Balanced-budget rule in the BC (2008) model: debt falls gradually; costs = more volatile taxes | Direct base for the FRBM extension |
| Bai & Lagunoff (2011) RES | Today's policy changes who holds power tomorrow | Base for endogenous q |
| **Futter (2025) Legislative Studies Quarterly 50(4) e70038** | Majority party saves more in rainy-day fund when likely to keep majority; supermajority rules encourage saving | Supports q effect; veto rules ≈ low φ |
| Rose (2008), State Politics & Policy Quarterly | US states withdraw ~3× more from rainy-day funds in election years; veto-player rules on withdrawals work better than rules on economic conditions | **Evidence that φ (withdrawal protection) matters** |
| Pope & Leland (2019), Social Science Quarterly | RDF balances lower in election years and under unified party control | Motivation |
| Khemani (2004) JDE 73(1): 125–154 | Elections in 14 Indian states 1960–96: lower commodity taxes, more roads, no effect on deficits | India motivation (cited in student's email) |

**Forward citations:** Google Scholar "Cited by" not reachable from the session — student to run it. EconPapers showed ~33 citations of Battaglini (2014). The 2026 paper is new; its earlier version is "Chaos and Unpredictability in Dynamic Social Problems" (NBER WP 28347 / CEPR DP15662) — search "Cited by" for that title too.

**Implication for novelty:** "turnover → no saving" (Amador; A&T) and "disagreement → dissaving" (Cao & Werning; Azzimonti) are already known. What remains ours: **φ, institutional protection of the stock, separate from preferences**; the **balanced-budget band** it creates; φ vs fiscal rules (ABC 2016); interaction with the **precautionary buffer** in the BC economy; the **Indian states** application (CSF fungibility, OPS, Centre alignment). Rose (2008) and Futter (2025) give empirical support that withdrawal rules matter.

## Candidate extensions (2026-10-22, not yet chosen)

1. **Spending shocks (BC 2008 style)**: needed to fix the β(1+r) > 1 logic issue. Expected: φ cuts precautionary saving → taxes more volatile.
2. **Resource windfall (oil, Norway/Gulf)**: temporary income boost. Expected: high φ → windfall spent at once; low φ → saved in a fund. Links to Tornell & Lane (1999) voracity effect.
3. **Fiscal rule vs fund protection (FRBM Act, Lecture 19)**: debt ceiling vs low φ. Expected: ceiling stops borrowing but doesn't create saving; protection does the opposite → complements. India angle.
4. **Choosing φ (who protects the fund?)**: constitutional stage. Expected (to derive): behind a veil of ignorance both parties want φ = 0, but an incumbent may not adopt it alone.
5. **Endogenous q (probabilistic voting, Lecture 20)**: saving raises taxes today → lowers re-election chance → less saving. Harder.

Recommended: 1 (must) + 2 or 3 (headline result). Leave 4 and 5 as "future work".

## Timeline

| By | Task | Done |
|---|---|---|
| Oct 16 | Fix question; read BC (2008) + Alesina & Tabellini (1990) | [ ] |
| Oct 23 | Lit review + motivation data | [ ] |
| Oct 30 | Write model; solve two-period version | [ ] |
| Nov 6 | Mechanism, comparative statics, roadblocks; optional simulation figure | [ ] |
| Nov 10 | Polish and submit (exams from Nov 16) | [ ] |

## Open next steps (offered by Claude)
- Work through the two-period model together to derive the threshold.
- Python simulation of planner path with/without raiding risk (for a figure).
- LaTeX/Word skeleton with section headings in this repo.
- Pitch idea at office hours.
