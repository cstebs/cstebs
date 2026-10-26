### Hi, I'm Colin 👋

I build and evaluate LLM systems, mostly retrieval and agents over regulated clinical content. My background is seven years in clinical lab operations, where I build automation and AI tooling for global project teams. Before that I worked as an analytical chemist (B.S. Chemistry, University of Pittsburgh). I like measuring things before I believe them, and I publish the negative results along with the wins.

**Currently:** experimenting with local models for a new project as well as endlessly tinkering on my home server.

---

### Clinical AI portfolio

These three repos share one corpus (127 FDA clinical research guidance documents, 2,980 pages) and one 85-question gold set, so every result can be compared against the others.

| Project | What it is | Headline result |
|---|---|---|
| [**clinical-rag-evals**](https://github.com/cstebs/clinical-rag-evals) [![CI](https://github.com/cstebs/clinical-rag-evals/actions/workflows/ci.yml/badge.svg)](https://github.com/cstebs/clinical-rag-evals/actions/workflows/ci.yml) | RAG evaluation harness. Runs 14 single-variable retrieval configs against a hand-authored gold set, with an LLM judge validated against human labels. | nDCG@10 0.738 → 0.830 from switching to hybrid retrieval. Judge agreement with my labels: Cohen's κ 0.81–1.00. Total API spend for every run: $4.78. |
| [**clinical_rag_agent**](https://github.com/cstebs/clinical_rag_agent) | Self-correcting RAG agent in LangGraph: document grading, query rewrite, grounding check, and a tool-calling loop, with 25 offline tests. | Groundedness 0.968 → 1.000. Correctness change was within noise, at 6.5x the LLM calls, and the README reports that. |
| [**clinical-guidance-mcp**](https://github.com/cstebs/clinical-guidance-mcp) | MCP server for searching and reading the corpus from any MCP client. Supports stdio and HTTP, and its tools return typed outputs. | Reuses the best retriever from the harness: recall@10 0.918, MRR 0.821. |

**One finding I like:** reranking made retrieval *worse*. Before testing why, I wrote down the prediction, then held the index fixed and shortened passages from 512 to 256 tokens. The effect flipped sign, which pinned the cause on the cross-encoder's 512-token input window rather than on reranking as a technique.

CI on the harness runs ruff, pytest on Python 3.11 and 3.12, and a prompt audit that fails the build if any committed run record no longer matches the prompt text on disk.

---

### Shipped products

- [**OpenCar**](https://github.com/cstebs/opencar): a free, self-hosted in-car dashboard for the Tesla browser. It runs on a Cloudflare Worker with KV and D1, and uses the Tesla Fleet API through OAuth. An adaptive poller has a hard cost ceiling written into the code and makes zero API calls while the car is parked.
- [**Serin Privacy Radar**](https://serinradar.com): an iOS and Android app that scans for hidden cameras, trackers, and monitoring devices over Bluetooth, Wi-Fi/mDNS, and IR detection through the phone's camera. Live on the App Store and Google Play.

---

**Stack:** Python · TypeScript/JavaScript · Swift · SQL · LangGraph · Anthropic and OpenAI APIs · MCP · BM25 / dense / hybrid retrieval · pandas · Docker · Cloudflare Workers · AWS Lambda · GitHub Actions
