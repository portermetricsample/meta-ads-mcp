# Contributing

This is a documentation repository. There is no code to build or tests to run — the MCP server itself is hosted at `mcp.portermetrics.com`.

The most useful contributions are corrections.

## What helps most

**A field that behaves differently than documented.** If `06-reference/all-fields.md` describes a metric one way and Meta returns something else, that is the highest-value issue you can open. Include the exact question you asked and the response you got.

**An error we have not documented.** `06-reference/errors.md` lists real Meta error subcodes and their fixes. If you hit one that is not there, add it — the error text, what caused it, and what fixed it.

**A limitation we claim that is no longer true.** Platforms change. If `06-reference/what-it-cannot-do.md` says something is impossible and you have done it, we want to know.

**A prompt that does not work as written.** Every prompt in `docs/` is meant to work on first paste. If one fails, say which file and what came back.

## What we will not merge

- Marketing copy or unverified capability claims
- Screenshots or figures from a real ad account — no client data ever enters this repository
- Content copied from Meta's documentation

## How to open a change

1. Fork the repository
2. Make the edit
3. Open a pull request describing what you observed and how you verified it

Every factual claim in this repository traces to a real call against the live connector. Contributions are held to the same standard: if you cannot say how you verified it, write it as a question in an issue instead.

## Questions

Open an issue, or see [SUPPORT.md](SUPPORT.md).
