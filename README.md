# prime — session-priming snippets

A grab-and-paste index of the one-liners I use to prime a fresh Claude Code, Codex CLI, or other LLM session with the contracts / skill bundles it needs.

Workflow: open a new agent session, open this page in a browser tab, copy the line below that matches what you're doing, paste as your first message. Done.

---

## PR review on any project (Fast or otherwise)

```
Learn https://github.com/fastxyz/pact
```

Loads the PACT v1.x contract: merge gate (P0 = P1 = P2 = 0 from two different vendors), marker formats (`CODE_DONE` / `LOOP_DONE` / `REVIEW_CLEAN` / `REVIEW_FINDINGS`), escalation triggers, and the `/code`, `/loop [N]`, `/review` commands. From this point the agent recognises those commands (with or without the leading slash).

## LangGraph / LangChain work

```
Learn https://github.com/langchain-ai/langchain-skills — focus on langgraph-fundamentals, langgraph-persistence, langgraph-human-in-the-loop, langgraph-cli, and langchain-middleware
```

Loads the LangGraph + middleware skill bundles. Use this in any session that touches StateGraph, checkpoint savers, node graphs, HITL interrupts, or `langgraph dev` / `langgraph build`. Relevant in `fast-shop`'s `apps/chat/src/commerce-orchestrator/` after PR #286.

## Both at once (PR review on a LangGraph-based project)

```
Learn https://github.com/fastxyz/pact AND https://github.com/langchain-ai/langchain-skills (focus on the LangGraph skills: langgraph-fundamentals, langgraph-persistence, langgraph-human-in-the-loop, langgraph-cli, langchain-middleware)
```

For Pif / fast-shop graph work that needs both the review contract and the graph skill bundle.

---

## How priming actually works

Each "Learn …" line tells the agent to fetch the README at that URL, then follow any links in the README to load the rest (CONTRACT.md, SKILL.md files, adapter docs, etc.) into its session context. Nothing is installed on your machine; everything is fetched at session start from raw GitHub URLs.

You only re-prime at the start of a fresh agent session. Within a session, the agent has the relevant docs in context for the duration.

## Conventions used inside the priming targets

- PACT marker names live in `CONTRACT.md §5`; vendor identifiers in `adapters/<vendor>/README.md`. See [fastxyz/pact](https://github.com/fastxyz/pact).
- LangChain Skills follows the [Agent Skills specification](https://skills.sh) — each skill is one `SKILL.md` file under `<skill-name>/`.

## Adding a new priming snippet

Edit `README.md`, add a new section with a one-liner inside a fenced block, commit, push. The URL `github.com/grosu/prime` stays the same forever.
