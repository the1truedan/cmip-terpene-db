# Conversation providers (design attribution)

**Purpose:** document which **AI conversation systems** contributed to *design discussion* for CMIP — not which databases supply chemistry rows. Chemistry provenance stays in [OPEN_DATA_SOURCE_PATHWAYS.md](OPEN_DATA_SOURCE_PATHWAYS.md).

CMIP’s public materials are human-edited architecture notes. Multi-provider chats were used for brainstorming schema shape, ETL layering, and open-data pivots. They are **not** authoritative for molecular facts, COA values, or medical claims.

## Provider table

| Provider | Role in CMIP design | Public product / docs |
|----------|---------------------|------------------------|
| **Grok** (xAI) | Architecture brainstorming, repo packaging, documentation cleanup, concept art prompts | [https://x.ai](https://x.ai) · [https://grok.x.ai](https://grok.x.ai) |
| **ChatGPT** (OpenAI) | Early schema brainstorms, spreadsheet-to-normalized-model ideation | [https://chatgpt.com](https://chatgpt.com) · [https://platform.openai.com/docs](https://platform.openai.com/docs) |
| **Claude** (Anthropic) | Long-context design reviews, cautious licensing language | [https://claude.ai](https://claude.ai) · [https://docs.anthropic.com](https://docs.anthropic.com) |
| **Local / self-hosted** | Offline drafting when cloud is off-limits (Ollama, LM Studio, vLLM, Comfy-local helpers, etc.) | [https://ollama.com](https://ollama.com) · [https://lmstudio.ai](https://lmstudio.ai) · [https://github.com/vllm-project/vllm](https://github.com/vllm-project/vllm) |
| **GitHub Copilot / coding assistants** | Optional IDE assistance for future loaders (none required for this docs-only repo) | [https://github.com/features/copilot](https://github.com/features/copilot) |

## What we do *not* treat as conversation providers

| System | Why it is different |
|--------|---------------------|
| PubChem, ChEBI, KEGG, ChEMBL, NIST, USDA, etc. | **Data / knowledge sources** — see open-data pathways |
| Private lab COAs or scraped strain dumps | **Out of scope** until license-reviewed; not conversation |
| Hippo / internal agent memory | Private ops tooling; not published here |

## Attribution rule

When a design decision in this repo was shaped by multi-provider chat:

1. The **human** remains responsible for the published text.
2. Providers are credited **collectively** via this page (or a short README pointer).
3. **No chat transcript dumps** or internal session IDs ship in this public repo.
4. Factual chemistry always needs a **citable open source**, never “the model said so.”

## Related

- [README.md](../README.md) — public architecture overview  
- [OPEN_DATA_SOURCE_PATHWAYS.md](OPEN_DATA_SOURCE_PATHWAYS.md) — named databases with URL hyperlinks  
