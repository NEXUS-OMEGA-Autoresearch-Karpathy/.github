# 🧠 NEXUS-OMEGA — Autoresearch-Karpathy

> Self-learning AutoResearch architecture across three domains:
> **Sport-Wetten · Crypto-Trading · Prompt-Optimierung**

## Pattern
[Karpathy-AutoResearch](https://github.com/Pahuut420/pahuut-skills) — autonomous overnight loops generate hypotheses,
[RuVector](https://github.com/NEXUS-OMEGA-Autoresearch-Karpathy/omega-memory-core) persists patterns via HNSW similarity,
`nexus-omega-core` aggregates cross-domain scores, `omega-monitoring` publishes results.

## Architecture

```
nexus-omega-core          score_aggregator · shared infra · Docker Compose
│
├── Domain Loops (AutoResearch)
│   ├── omega-sports      ⚽ Dixon-Coles 5-model ensemble · Metric: ROI
│   ├── omega-crypto      📈 Freqtrade + Neural Trader   · Metric: Sharpe ≥ 1.65
│   └── omega-prompts     ✍️  Langfuse-scored evaluation  · overnight 100-iter
│
├── Memory (RuVector — HNSW per domain)
│   ├── omega-memory-core      cross-domain ReasoningBank
│   ├── omega-memory-sports    match patterns + odds movement
│   ├── omega-memory-crypto    trade patterns + signal cache
│   └── omega-memory-prompts   prompt versions + A/B history
│
├── Output Layer
│   ├── omega-monitoring       Telegram · OMEGA Score Dashboard · n8n webhooks
│   └── omega-trading-agents   TauricResearch fork — Multi-Agent LLM Trading
│
├── Strategy Hybrid
│   └── naumii-strategy        🧠 Sports Oracle + Crypto Vibes (intuitive sanity-check)
│
└── omega-lab                  🧪 Experiment Sandbox
```

## Constraints
- ¼-Kelly sizing on all bets (never full Kelly)
- 5.3% GGL Wettsteuer always factored
- Sharpe baseline 1.65 for Crypto — below → pause trading
- Strategy skill: [omega-sports-betting](https://github.com/Pahuut420/pahuut-skills)

## Owner
**Paul Gernt (Pahuut420)** · Krakow am See · [Meck-Pomm Elektronik](https://github.com/Pahuut420/meckpomm-website-v2)
