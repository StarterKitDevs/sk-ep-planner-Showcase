# Architecture

## Overview

SK Episode Planner is a client-side production operations application built with HTML, CSS, and vanilla JavaScript.

The architecture intentionally avoids a backend because the original workflow is designed for a single operator using one browser/device. Application state is persisted locally and transformed into several operational views and export formats.

## System Shape

```text
Browser
│
├── Planner View
│   ├── Episode metadata
│   ├── News/research segments
│   ├── Tech segment
│   ├── Tutorial segment
│   └── Community/Q&A segment
│
├── History View
│   ├── Review
│   ├── Edit
│   ├── Duplicate
│   └── Delete
│
├── Spreadsheet View
│   └── Multi-episode operational table
│
└── EpisodePlanner JavaScript Controller
    ├── Event handling
    ├── Form-to-object mapping
    ├── Persistence
    ├── View rendering
    ├── Autosave
    └── Export/share workflows
         ├── localStorage
         ├── PDF
         ├── CSV
         └── Email
```

## Episode Data Model

The central application concept is a structured episode object containing:

- Unique identifier
- Date
- Episode title
- Host notes
- Collection of news stories
  - title
  - URL
  - timestamp
  - summary
- Technology segment
  - topic
  - description
  - timestamp
- Tutorial segment
  - topic
  - description
  - timestamp
- Community segment
  - notes
  - timestamp

This structure allows multiple outputs to be generated from the same source data.

## State and Persistence

The application loads serialized episode data from browser `localStorage` during initialization and writes the current episode collection back after relevant changes.

This choice keeps the application deployable as static files and removes server/database requirements for the original single-user use case.

### Tradeoff

Local persistence is simple and inexpensive, but it is device/browser-specific and is not suitable as the persistence layer for a collaborative production team.

## UI Architecture

The application provides three primary views:

### Planner

The main data-entry experience. Form fields map into the episode object model.

### History

Transforms saved episode objects into review cards with edit, duplicate, and delete actions.

### Spreadsheet

Transforms the same saved data into a tabular operational view for scanning multiple episodes.

Tab navigation switches these surfaces without requiring page reloads.

## Autosave Flow

```text
User edits form
      │
      ▼
Input event
      │
      ▼
Reset short delay timer
      │
      ▼
No new input during delay
      │
      ▼
Read structured form data
      │
      ▼
Update eligible saved episode
      │
      ▼
Persist to localStorage
```

The delay prevents a storage write on every keystroke while preserving useful autosave behavior.

## Export Architecture

### PDF

The current episode object is transformed into a print-oriented HTML representation and passed to the PDF-generation library.

### CSV

All saved episodes are flattened into rows, serialized into CSV text, converted to a browser Blob, and downloaded locally.

### Email

The current episode is transformed into a plain-text production brief and URL-encoded into a `mailto:` action.

## Why Vanilla JavaScript

The application does not require a component framework to solve its original problem. Keeping the implementation framework-free provides:

- Minimal runtime dependencies
- Static hosting compatibility
- Direct browser API usage
- Straightforward deployment
- A small architectural footprint

It also demonstrates JavaScript fundamentals outside a framework abstraction.

## Production Evolution

For a multi-user production system, the architecture would evolve toward:

```text
Frontend Application
        │
        ▼
Authenticated API
        │
        ▼
Shared Database
        │
        ├── Episodes
        ├── Users / Roles
        ├── Version History
        └── Collaboration Data
```

Additional production layers would include validation, authorization, sanitization, observability, backups, testing, and collaborative conflict handling.
