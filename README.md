# SK Episode Planner

**Browser-Based Content Production Operations Dashboard**

SK Episode Planner is a lightweight production-planning application built to organize recurring livestream or episodic content before it goes live. It turns show preparation into a structured workflow for episode topics, timestamps, research links, host notes, tutorials, and community segments.

> The original implementation is maintained separately. This public showcase documents the product workflow, frontend architecture, and engineering decisions without requiring recruiters or reviewers to sift through production-specific content.

## What the Project Solves

Recurring shows often rely on scattered notes, documents, spreadsheets, and last-minute communication. SK Episode Planner consolidates that preparation into a repeatable browser-based workflow.

The application supports:

- Structured episode planning
- Timestamped show segments
- News/research links
- Host notes
- Tutorial and technology segments
- Community/Q&A planning
- Autosave behavior
- Episode history
- Edit / duplicate / delete workflows
- Spreadsheet-style review
- PDF export
- CSV export
- Email sharing

## Engineering Scope

This project demonstrates work across:

- Semantic HTML
- Custom CSS
- Vanilla JavaScript application logic
- Browser persistence with `localStorage`
- CRUD-style client-side workflows
- Event-driven UI behavior
- Autosave/debouncing patterns
- Tabbed dashboard navigation
- Structured data modeling
- Dynamic table rendering
- PDF generation
- CSV serialization
- Mailto-based sharing
- Responsive operational UI

## Technology Stack

| Area | Technology |
| --- | --- |
| Markup | HTML5 |
| Styling | Custom CSS |
| Application logic | Vanilla JavaScript |
| Persistence | Browser `localStorage` |
| PDF export | html2pdf.js |
| CSV export | Browser Blob / download APIs |
| Email sharing | `mailto:` workflow |
| Architecture | Client-side single-page operations tool |

## High-Level Architecture

```text
                 ┌────────────────────────┐
                 │   Episode Planner UI   │
                 └────────────┬───────────┘
                              │
             ┌────────────────┼────────────────┐
             ▼                ▼                ▼
       Form / Timeline   Episode History   Spreadsheet View
             │                │                │
             └────────────────┼────────────────┘
                              │
                              ▼
                  ┌──────────────────────┐
                  │ JavaScript Data Model│
                  └───────────┬──────────┘
                              │
               ┌──────────────┼──────────────┐
               ▼              ▼              ▼
          localStorage     PDF Export     CSV / Email
```

The application intentionally stays client-side because its original use case does not require accounts, a shared database, or a backend service.

## Key Features

### Structured Episode Planning

Each episode can capture multiple categories of production information, including:

- Episode date and title
- Host notes
- Multiple news/research stories
- Story links and summaries
- Segment timestamps
- Technology discussion topic
- Tutorial topic
- Community/Q&A notes

The data is modeled as a structured episode object rather than one large unstructured text field.

### Autosave

Form activity triggers delayed autosave behavior after a short period of inactivity. This reduces unnecessary writes while helping protect in-progress planning work.

### Local Persistence

Saved episodes are serialized into browser `localStorage`, allowing the planner to preserve work without requiring an external database.

### Episode History

Saved episodes can be reviewed in a dedicated history interface and support common workflow actions such as:

- Edit
- Duplicate
- Delete

Duplicating an episode provides a useful starting point for recurring content formats.

### Spreadsheet View

Episode data can also be viewed in a table-oriented format for quick operational review across multiple episodes.

### PDF Export

A selected/current episode can be converted into a formatted production document containing the episode timeline, topics, summaries, and host notes.

### CSV Export

Saved episodes can be serialized into CSV for use in spreadsheets, archives, or downstream workflows.

### Email Sharing

The application can generate a pre-filled email containing the current episode plan through the browser's email client.

## Product and Engineering Decisions

### Client-Side Persistence

For a single-user planning tool, `localStorage` keeps deployment simple and removes unnecessary backend complexity. The tradeoff is that data remains browser/device-specific and is not designed for collaborative multi-user use.

### Structured Data Over Freeform Notes

Representing each episode with defined fields enables history views, duplication, tables, exports, and automation that would be difficult with an unstructured note document.

### Operational Views From One Data Model

Planner, history, spreadsheet, PDF, CSV, and email outputs all derive from the same core episode model. This reduces repeated manual formatting and creates a more consistent production workflow.

### Framework-Free Architecture

The application uses browser-native JavaScript because the scope does not require a larger frontend framework. This demonstrates direct DOM/event/state management and frontend fundamentals.

## My Contributions

My work includes:

- Product/workflow design
- Episode data modeling
- Frontend application development
- Dashboard information architecture
- Autosave logic
- Browser persistence
- CRUD-style episode workflows
- Spreadsheet/table rendering
- PDF generation workflow
- CSV export
- Email-sharing workflow
- Responsive interface development

## Development Status

**Functional browser-based planning tool / portfolio-ready prototype**

The application is suitable for personal or controlled production planning. A future collaborative version would benefit from a backend, authentication, shared persistence, validation hardening, and safer dynamic rendering patterns.

## Selected Engineering Highlights

- Stateful vanilla JavaScript application
- Browser persistence with JSON serialization
- Debounced autosave behavior
- Edit / duplicate / delete episode workflows
- Multiple UI views driven from one data model
- Dynamic HTML/table generation
- PDF export
- CSV export
- Structured mailto generation
- Responsive operations dashboard

## Security and Scope Notes

This application was originally designed as a local/browser-based productivity tool rather than a multi-user public SaaS product.

Important architectural boundaries include:

- Data is stored locally in the user's browser.
- There is no production authentication layer in this version.
- There is no shared server-side database.
- Some dynamic views in the original implementation interpolate user-entered content into HTML strings. A shared/public version should replace that pattern with safer text rendering or explicit sanitization.
- External URLs entered by users should receive stricter validation in a production multi-user environment.

See [`docs/SECURITY.md`](docs/SECURITY.md) for the full review boundary.

## Documentation

- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md)
- [`docs/PROJECT-HIGHLIGHTS.md`](docs/PROJECT-HIGHLIGHTS.md)
- [`docs/SECURITY.md`](docs/SECURITY.md)

## Known Limitations / Next Steps

A production collaborative version could add:

- Authentication
- Shared cloud database
- Team collaboration
- Server-side validation
- Safer rendering/sanitization
- Cloud autosave
- Version history
- Calendar integration
- Collaborative commenting
- Automated tests
- Accessibility audit
- Import/export validation

## Why This Repository Is a Showcase

This project demonstrates the ability to take a recurring operational process and convert it into a usable browser application with structured state, persistence, exports, and multiple workflow views.

For hiring review, it complements larger full-stack and AI systems by showing direct JavaScript fundamentals and practical workflow automation without unnecessary framework complexity.
