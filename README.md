# Shehadey Foods — Project Brain

Single source of context for the Shehadey Foods (Producers Dairy) Orderful onboarding.
Concurrent-led: Concurrent builds the Tray.ai integration between Shehadey's flat files and the Orderful API.

## Folder map
```
README.md            guide for people
CLAUDE.md            guide for Claude (read first)
action-items.md      who owes what
build-log.md         dated build/testing progress
context/             living project facts: overview, systems/flow, partners, decisions, open questions
meetings/            one file per call: YYYY-MM-DD-topic.md
specs/<doc type>/    850, 810, 855, 856, 852, 880-894
  layout/            client spec documents
  samples/           raw EDI + matching flat files
  mapping.md         ERMS field -> Orderful JSON path
  questions.md       open mapping questions for Shehadey
source-docs/         originals, never edited
  from-client/
  from-orderful/
  internal/          Mark's notes, Concurrent process docs
outputs/             things we produce: agendas, diagrams, recap drafts
chats/               summaries of Claude conversations
```

## Two rules
1. Specs and sample files go in `specs/<doc type>/`. Everything else received goes in `source-docs/<who sent it>/`.
2. Start dated files with the date: `2026-10-21-...`. Use lowercase-with-hyphens names, no spaces.

## Working with Git
Pull before you start → make changes (yourself or with Claude) → review in GitHub Desktop → commit → push. Never commit credentials.

## Links
- Asana: https://app.asana.com/1/1210548484131647/project/1219659554232276
- Workflow diagram (live): https://claude.ai/artifact/75Ue3X9eWdQNKP5GEEKA8u (offline copy in `outputs/`)
