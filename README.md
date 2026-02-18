# 📚 ObsidianDocsAgent — README

## What is it?

**ObsidianDocsAgent** is an agent for VS Code (GitHub Copilot / Copilot Chat) that analyzes any repository and generates comprehensive technical documentation in the form of an **Obsidian vault** — a network of interconnected markdown notes with wikilinks, tags, YAML frontmatter, and a structure optimized for graph navigation.

Instead of one massive documentation file, you get dozens of atomic notes that you can browse in [Obsidian](https://obsidian.md/) using the knowledge graph, search engine, tags, and dynamic Dataview queries.

## Requirements

* **VS Code** with the GitHub Copilot Chat extension (or a compatible agent supporting `.md` files in the `.github/agents/` folder).
* **Git** installed and available in the terminal (the agent uses `git log`).
* **Obsidian** (optional, for viewing the generated documentation — without it, the notes are simply standard `.md` files).

---

## Installation

### Step 1 — Create the agents folder

In the root directory of your repository, create the folder if it doesn't already exist:

```
.github/
└── agents/

```

### Step 2 — Copy the agent file

Place the `obsidian-docs-agent.md` file in the agents folder:

```
.github/
└── agents/
    └── obsidian-docs-agent.md

```

The agent file is the one with the YAML header starting with `name: ObsidianDocsAgent`.

### Step 3 — Restart VS Code

After adding the file, restart VS Code or reload the window (`Ctrl+Shift+P` → "Developer: Reload Window") so the agent can be detected.

---

## Usage

### Calling the Agent

Open Copilot Chat in VS Code and call the agent by providing a command:

```
@ObsidianDocsAgent full

```

You can also call the agent without a command — it will then ask which section to generate or suggest `full`.

### Available Commands

| Command | What it generates |
| --- | --- |
| `full` | The entire vault — all sections and notes |
| `overview` | HOME.md + 01-Overview/ folder |
| `architecture` | Architecture MOC + 02-Architecture/ folder |
| `structure` | 03-Structure/ folder |
| `data-model` | Data Model MOC + 04-Data-Model/ folder with separate notes per type and enum |
| `components` | Components MOC + 05-Components/ folder with separate notes per component |
| `state` | State Management MOC + 06-State/ folder with separate notes per slice |
| `api` | API MOC + 07-API/ folder with separate notes per resource and service |
| `integrations` | Integrations MOC + 08-Integrations/ folder with separate notes per service |
| `security` | Security MOC + 09-Security/ folder |
| `ux` | UX MOC + 10-UX/ folder |
| `changelog` | 11-Changelog/ folder |
| `glossary` | 12-Glossary/ folder |
| `todos` | 13-Roadmap/ folder |

### Examples

Full documentation of the entire repository:

```
@ObsidianDocsAgent full

```

Only project overview and tech stack:

```
@ObsidianDocsAgent overview

```

Only data model with types and enums:

```
@ObsidianDocsAgent data-model

```

Multiple sections at once (list them in the message):

```
@ObsidianDocsAgent architecture, components, state

```

If the vault already exists and you want to refresh one section:

```
@ObsidianDocsAgent api

```

The agent will overwrite only the notes in the API section — the rest of the vault remains untouched.

---

## What will be generated

The agent creates a `docs/` folder in the root directory of the repository with the following structure:

```
docs/
├── HOME.md                          — Main dashboard and entry point
├── 00-MOCs/                         — Index notes (Map of Content)
│   ├── Architecture MOC.md
│   ├── Components MOC.md
│   ├── Data Model MOC.md
│   ├── API MOC.md
│   ├── State Management MOC.md
│   ├── Security MOC.md
│   ├── Integrations MOC.md
│   └── UX MOC.md
├── 01-Overview/                     — Project overview
│   ├── Project Overview.md
│   ├── Tech Stack.md
│   ├── Scripts and Commands.md
│   └── Prerequisites.md
├── 02-Architecture/                 — System architecture
│   ├── High-Level Architecture.md
│   ├── Application Layers.md
│   ├── Data Flow.md
│   ├── Application Layout.md
│   └── Architectural Decisions.md
├── 03-Structure/                    — Project structure
│   ├── Directory Tree.md
│   ├── Organization Pattern.md
│   ├── Naming Conventions.md
│   └── Key Files.md
├── 04-Data-Model/                   — Data model
│   ├── Entity Relationships.md
│   ├── Core Types/
│   │   └── [TypeName].md            — Separate note per type
│   ├── Enums/
│   │   └── [EnumName].md            — Separate note per enum
│   ├── Type Relationships.md
│   ├── Database Schema.md
│   ├── API Types.md
│   └── Type Map.md
├── 05-Components/                   — UI Components
│   ├── Component Tree.md
│   ├── Components/
│   │   └── [ComponentName].md       — Separate note per component
│   └── Shared Components.md
├── 06-State/                        — State management
│   ├── State Overview.md
│   ├── Store Shape.md
│   ├── Slices/
│   │   └── [SliceName].md           — Separate note per slice/store
│   ├── Async Operations.md
│   ├── Middleware.md
│   ├── Side Effects.md
│   ├── Data Flow Diagram.md
│   ├── Component Connections.md
│   ├── State Persistence.md
│   └── State Reset Patterns.md
├── 07-API/                          — API Layer
│   ├── HTTP Client.md
│   ├── Interceptors.md
│   ├── Endpoints/
│   │   └── [ResourceGroup].md       — Separate note per resource group
│   ├── Services/
│   │   └── [ServiceName].md         — Separate note per service
│   ├── Error Handling.md
│   ├── Authentication in API.md
│   ├── Request Caching.md
│   ├── Real-time Communication.md
│   ├── File Operations.md
│   ├── API Constants.md
│   ├── API Layer Diagram.md
│   └── Endpoint Coverage Matrix.md
├── 08-Integrations/                 — External integrations and DevOps
│   ├── External Services Overview.md
│   ├── Services/
│   │   └── [ServiceName].md         — Separate note per service
│   ├── Internal Communication.md
│   ├── CI-CD Pipeline.md
│   ├── Deployment.md
│   └── Analytics and Monitoring.md
├── 09-Security/                     — Security
│   ├── Authentication Flow.md
│   ├── Authentication Implementation.md
│   ├── Authorization Model.md
│   ├── Token Management.md
│   ├── Route Protection.md
│   ├── Input Validation.md
│   ├── Environment Variables.md
│   ├── CORS and Headers.md
│   ├── Data Protection.md
│   └── Security Concerns.md
├── 10-UX/                           — UX decisions and design
│   ├── Design System.md
│   ├── Styling Approach.md
│   ├── UX Decisions.md
│   ├── Application Layout.md
│   ├── UI State Patterns.md
│   ├── Responsive Strategy.md
│   ├── Design Tokens.md
│   ├── Accessibility.md
│   └── Internationalization.md
├── 11-Changelog/                    — Change history
│   ├── Changelog Summary.md
│   ├── Timeline.md
│   ├── Feature Evolution.md
│   ├── Breaking Changes.md
│   └── Dependency Changes.md
├── 12-Glossary/                     — Glossary of terms
│   ├── Domain Terms.md
│   ├── Technical Terms.md
│   └── Code UI Mapping.md
└── 13-Roadmap/                      — TODOs and development plan
    ├── In-Code TODOs.md
    ├── Open Issues.md
    ├── Technical Debt.md
    ├── Improvement Suggestions.md
    └── Missing Documentation.md

```

The exact number of notes depends on the size of the repository. A small project might have 30-40 notes, while a large one can exceed 100.

---

## Browsing Documentation in Obsidian

### Step 1 — Open the vault

Open Obsidian and select "Open folder as vault". Point to the `docs/` folder generated by the agent.

### Step 2 — Start with HOME.md

The HOME.md file is the main dashboard with links to all sections. Click any wikilink (text in double square brackets) to navigate to a note.

### Step 3 — Use the Knowledge Graph

Press `Ctrl+G` (Windows/Linux) or `Cmd+G` (Mac) to open the graph view. You will see how all notes are interconnected. Click any node to navigate to the note.

### Step 4 — Filter with tags

Open the tags panel (# icon in the left sidebar). Tags are hierarchical:

* **docs/** — filter by section (docs/overview, docs/architecture, docs/components...)
* **type/** — filter by type (type/core-model, type/enum, type/component-props...)
* **layer/** — filter by layer (layer/frontend, layer/backend)
* **security/** — filter by security topic
* **tech-debt**, **todo**, **improvement** — quick access to areas needing improvement

### Step 5 — Install Dataview (optional)

The Dataview plugin allows for dynamic queries of note frontmatter. Once installed, you can create your own notes with queries.

Example — a list of all notes with high-priority technical debt:

```dataview
LIST
FROM #tech-debt
WHERE contains(tags, "priority/p0") OR contains(tags, "priority/p1")

```

Example — a table of all components with their source files:

```dataview
TABLE source-files AS "Source", status
FROM "docs/05-Components/Components"
SORT file.name ASC

```

---

## Key Features of Generated Documentation

### Wikilinks

Every mention of a component, type, service, state slice, or other concept that has its own note is a wikilink. Clicking takes you to the note. Hover your mouse to see a preview without leaving the current note.

### YAML Frontmatter

Each note starts with YAML metadata:

* **title** — the title of the note
* **created** / **updated** — generation dates
* **tags** — hierarchical tags for filtering
* **status** — complete, draft, or needs-review
* **scope** — which section the note belongs to
* **related** — wikilinks to related notes
* **source-files** — paths to the source files the note was based on

### Callouts

Important information is highlighted with Obsidian callouts:

* **note** — general information
* **warning** — security warnings, pitfalls
* **tip** — developer tips
* **important** — breaking changes
* **example** — usage examples
* **question** — open design questions
* **bug** — known issues
* **info** — context and background

### ASCII Diagrams

All architectural, data flow, and relationship diagrams are in ASCII art using box-drawing characters (┌ ┐ └ ┘ │ ─ ├ ┤ ┬ ┴ ┼). No Mermaid diagrams or images — everything is readable as plain text.

### MOC (Map of Content)

Index notes in the 00-MOCs/ folder serve as curated entry points for each section. Each MOC includes a topic overview, links to all notes in the section, and key takeaways.

---

## Idempotency — Updating Documentation

The agent is idempotent. If the vault already exists:

* Calling a specific section overwrites ONLY the notes in that section.
* Notes in other sections remain untouched.
* HOME.md is updated with a new date and statistics.

This allows you to generate documentation once with the `full` command and then update individual sections as the code changes.

---

## Browsing without Obsidian

The generated notes are standard markdown files. You can view them:

* **In VS Code** — markdown preview works normally, but wikilinks won't be clickable.
* **On GitHub** — YAML frontmatter renders as a table, content is readable, wikilinks appear as text.
* **In any markdown editor** — files are fully readable as text.

However, the full experience — knowledge graph, clickable wikilinks, Dataview, hover previews, tag panel — is only available in Obsidian.

---

## Differences from TechDocsAgent (Monolithic Version)

| Aspect | TechDocsAgent | ObsidianDocsAgent |
| --- | --- | --- |
| Output Format | One TECHNICAL-DOCS.md file | Dozens of files in docs/ folder |
| Navigation | TOC + scrolling | Wikilinks + Knowledge Graph |
| Metadata | None | YAML Frontmatter on every note |
| Filtering | Ctrl+F | Hierarchical Tags + Dataview |
| Granularity | 13 sections in one file | Separate note per component, type, service, slice |
| Connections | Manual search | Automatic wikilinks + Graph |
| Update | Overwrite section in file | Overwrite files in section folder |
| Viewing | Any markdown editor | Best in Obsidian |
| Size | One large file | Multiple small files |
| Onboarding | Read top-to-bottom | Explore non-linearly from HOME.md |

---

## Troubleshooting

### Agent does not generate notes

Ensure the agent file is in `.github/agents/` and has a correct YAML header. Restart VS Code after adding the file.

### Missing git history section

The agent needs access to Git. Check if `git log` works in the VS Code terminal. If the repo is a shallow clone (e.g., from CI), history will be limited.

### Wikilinks don't work

Wikilinks only work in Obsidian. In VS Code or GitHub, text in double brackets will be displayed as plain text. Open the `docs/` folder as a vault in Obsidian.

---

## License

MIT

---
