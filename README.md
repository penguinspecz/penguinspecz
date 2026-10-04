# Howdy 🤠

I lead technical customer success (Linux, Kubernetes, AI) at an enterprise vendor. Off the clock I build and run production systems on bare-metal Kubernetes that I own end to end.

My projects are published under [Land O’ Clusters](https://github.com/Land-o-Clusters). They're small tools, and each one shows its work.

## Projects

<!-- New entries: "### Name: what it is", a short paragraph with real numbers if there are any, then 3 to 5 bullets that each lead with the claim and follow with the evidence. -->

### Floati: a fleet operating system for local coding agents (macOS)

If you run an agent in Codex, two in Claude and one in OpenCode, you are the bus, the scheduler and the person who checks whether anything died. Floati takes over those jobs. It came out in August 2026 as an early public cut at [Land-o-Clusters/floati](https://github.com/Land-o-Clusters/floati). You install it from source. It needs only Python 3's standard library, so there's no dependency tree to audit.

- Agents from different harnesses work one plan together. Each node registers whatever harness it runs in, and they all share one bus and one board, so a Codex worker, a Claude reviewer and an OpenCode scout can split a job.
- Every hand-off gets a receipt. Dispatches, messages and wakes are recorded on the bus, so you can check what the fleet actually did. The guarantees are a published contract, `TRUTH-GUARANTEES.md`.
- The product code is AGPL-3.0. The interchange schemas and bundle specs are Apache-2.0, so other tools can talk to the bus without taking on the copyleft.

### sleight: Claude Code drives your Mac apps in the background

[Land-o-Clusters/sleight](https://github.com/Land-o-Clusters/sleight) uses the computer-use engine bundled with the ChatGPT desktop app, so Claude Code can work in Mac apps while your cursor stays yours. Its benchmark publishes every run, failures included. It's early and unofficial.

### logijuice: Logitech battery levels on macOS

[Land-o-Clusters/logijuice](https://github.com/Land-o-Clusters/logijuice) shows battery levels and sends low-battery alerts for Logitech devices on a Logi Bolt receiver, from the menu bar, a widget or the command line.

### RoleGauge: deterministic hiring intelligence

RoleGauge tracks the job boards of 1,862 companies, global companies hiring in North America for now. It's being staged toward 20,000 providers, with fresh data at a flat marginal cost. No agent output is trusted: the gate re-derives every proposal itself instead of taking the agent's bytes, and scoring and ranking are deterministic. You wouldn't want the same career question answered two different ways, and RoleGauge won't do it.

- Every provider is under change control. A resolver chain (Wikidata → DBpedia → EDGAR → GitHub → Common Crawl) keeps careers URLs and ATS slugs current, and when a board moves, a healing engine finds it again. That produces a history of board migrations nobody else publishes.
- Determinism is enforced in the Kubernetes deployment itself: `PYTHONHASHSEED=0`, `TZ=UTC`, snapshot-mode scraping, and a replay-drift canary that checks two runs of the same input agree.
- Classification is rule-based. A versioned role taxonomy under change control gives the same title the same answer every time, so a model can't drift silently. ML only helps with the last mile.
- The archive is the product. Scrape artifacts are immutable and never treated as a cache, which is the only reason "what changed, and when" can be answered. It has 499 versioned migrations and no rewrites, row-level security, least-privilege roles, and exactly one audited path that can delete anything.

### Puddle: an honest meter for your AI agent fleet (macOS)

Puddle is a menu-bar city that meters every AI coding agent on your machine: usage, cost, context pressure, and the water it all theoretically drinks. It runs leaner than any of the tools it watches. It has 2,100+ tests, six providers and one deadpan municipal government. It launches publicly once its release checks pass. The CLI is `puddle` ([@puddlectl](https://twitter.com/puddlectl)).

- Every number in the app is stamped MEASURED, DERIVED or ESTIMATE. A CI check fails the build if any screen shows a number without a stamp.
- Zero telemetry is checked at release. The audit scans the binaries for network symbols and lists every allowed exception in a public ledger. Puddle only calls your own accounts, for features you turned on, and each call appears in a live log. The category leader put crash telemetry in an app advertised as "no telemetry." Puddle publishes its audit script.
- It won't guess. Unknown liveness shows as *idle*, never *zombie*. Spend it can't measure is left blank instead of showing $0.00, and every blank says why.
- Watching the whole fleet is budgeted at under 1% idle CPU in a published performance covenant, and it's re-measured on a 16 GB real-world corpus at every release check. The covenant includes the incident report that started it. Popular alternatives idle at 10× the memory.
- `puddle top sessions` works like `kubectl top` for your agents. You can approve agent actions without breaking flow and jump to the exact terminal pane that asked. The cross-harness bus on Puddle's roadmap grew into Floati. The water figures are cited to primary sources, and the almond is real.

## How I build

AI is a tool, and determinism is a principle. A check that can't go red tells you nothing, so a test has to be seen failing before I trust it to pass. Most of the hard bugs I find turn up when I attack the evidence. It's a beautiful world where smell counts as much as code-vision.

My projects are built by specialized AI agent lanes on a hub-and-spoke bus that spans harnesses. An architect agent makes the final call, a red team reviews the code adversarially, and I'm the operator and chief architect.

Cattle, not pets. 🦦
