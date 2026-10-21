# Specs

One subfolder per doc type: `850/`, `810/`, `855/`, `856/`, `852/`, `880-894/`.
Each holds `layout/` (client spec docs), `samples/` (raw EDI + matching flat files), `mapping.md` (ERMS field → Orderful JSON path, required?, transform, partner notes) and `questions.md`.

Approach: Concurrent reviews specs and samples offline, drafts maps with Claude, tests, and brings Shehadey only the questions that don't make sense.

## Received
- 850 mapping template (`850/layout/client-850-mapping-research.docx`): client research; maps flat file → client's own JSON, partial Orderful mapping. Not a build-ready spec. It references an original ERMS 850 layout doc and Park City layout docs — request those.

## Owed by client
- Outbound layouts: 810, 855, 856, 852, 880/894
- 850 production files
