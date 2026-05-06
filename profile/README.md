# NEXUS-OMEGA | Autoresearch (Karpathy)

> Self-learning, multi-domain trading & prediction intelligence — Crypto × Sports × Prompts

---

## Architecture

```
DATA LAYER
  Crypto.com MCP ──→ Live prices, orderbook, candles
  Sports APIs    ──→ Fixtures, odds, live scores
  naumii-strategy──→ Human signal feed (Fabian Naumann)

AUTORESEARCH LOOPS  (independent, overnight 100 iterations)
  omega-crypto   ──→ Freqtrade + Neural Trader ensemble   metric: Sharpe [-1..+1]
  omega-sports   ──→ Dixon-Coles + 5-model ensemble       metric: ROI   [-1..+1]
  omega-prompts  ──→ Langfuse prompt scoring               metric: Score [0..1]

MEMORY LAYER  (RuVector per domain, HNSW similarity search)
  omega-memory-crypto   ──→ trade patterns, signal cache
  omega-memory-sports   ──→ match patterns, odds movement
  omega-memory-prompts  ──→ prompt versions, A/B history
  omega-memory-core     ──→ cross-domain ReasoningBank

INTELLIGENCE INPUTS
  omega-trading-agents  ──→ TradingAgents (29.9k★) multi-agent LLM council
  naumii-strategy       ──→ Fabian's sports + crypto intuition as prior signal

AGGREGATION
  nexus-omega-core  ──→  score_aggregator.py  →  OMEGA Score [-1..+1]

OUTPUT
  omega-monitoring  ──→ Telegram alerts, dashboard, n8n webhooks
  omega-lab         ──→ experiment sandbox (Co-Work plugins, spikes)
```

---

## Repos

| Repo | Domain | Status | Description |
|------|--------|--------|-------------|
| [nexus-omega-core](../nexus-omega-core) | Core | ✅ | score_aggregator, Docker, shared infra |
| [omega-crypto](../omega-crypto) | Crypto | ✅ | Freqtrade + Neural Trader AutoResearch |
| [omega-sports](../omega-sports) | Sports | ✅ | Dixon-Coles ensemble, walk-forward bt |
| [omega-prompts](../omega-prompts) | Prompts | ✅ | Langfuse scoring, prompt optimization |
| [omega-memory-crypto](../omega-memory-crypto) | Memory | ✅ | RuVector: crypto patterns |
| [omega-memory-sports](../omega-memory-sports) | Memory | ✅ | RuVector: match patterns |
| [omega-memory-prompts](../omega-memory-prompts) | Memory | ✅ | RuVector: prompt versions |
| [omega-memory-core](../omega-memory-core) | Memory | ✅ | Cross-domain ReasoningBank |
| [omega-trading-agents](../omega-trading-agents) | Intel | ✅ | TradingAgents fork, Bull/Bear/Risk council |
| [omega-monitoring](../omega-monitoring) | Output | ✅ | Telegram, dashboard, n8n |
| [omega-lab](../omega-lab) | Lab | ✅ | Experiments, spikes, Co-Work plugins |
| [naumii-strategy](../naumii-strategy) | Signal | ✅ | Fabian Naumann — human prior feed |

> Note: 4 empty archived repos (`zz-archived-*`) are pending manual deletion. They hold no code.

---

## Naumii Signal Pipeline

Fabian posts predictions as GitHub Issues in `naumii-strategy/sports/` and `naumii-strategy/crypto/`.
The OMEGA agent reads them and cross-checks against the model:

```
naumii-strategy/sports/ ──→ omega-memory-sports ──→ omega-sports  ─┐
                                                                     ├──→ OMEGA Score
naumii-strategy/crypto/ ──→ omega-memory-crypto ──→ omega-crypto  ─┘

Agreement  → confidence BOOST
Divergence → interesting signal to investigate
```

---

## Rules

1. **Council before live** — every signal needs ≥2 LLM confirmations
2. **Paper Trading first** — 30 days dry-run minimum before live execution
3. **¼-Kelly sizing** — max 20% of recommended Kelly stake
4. **1% portfolio risk max** per trade, any domain
5. **AutoResearch always backtested** — no strategy goes live without 5-year backtest
6. **Log everything to RuVector** — every decision, pattern, backtest result

---

*Owner: [Pahuut420](https://github.com/Pahuut420) · Collaborator: [Fabian Naumann](mailto:fabiannaumann1965@gmail.com)*
