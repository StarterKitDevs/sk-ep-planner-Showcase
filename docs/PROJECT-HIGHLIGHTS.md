# Project Highlights

## 1. Operational Workflow Converted Into Software

SK Episode Planner turns a recurring content-production process into a repeatable application workflow instead of relying on disconnected notes and spreadsheets.

The project demonstrates the ability to identify operational structure and represent it as software.

## 2. Structured Episode Data Model

Episode information is captured as structured data covering metadata, news stories, timestamps, technical segments, tutorials, and community notes.

This data model is the foundation for every downstream view and export.

## 3. Multiple Views From One Source of Truth

The same episode collection drives:

- Planner workflows
- Episode history
- Spreadsheet view
- PDF output
- CSV output
- Email briefs

This is a practical example of separating core data from presentation/output formats.

## 4. Browser Persistence

Episode collections are serialized to JSON and persisted in `localStorage` so the application can preserve state without a backend.

This was an intentional architecture decision for a lightweight single-user tool.

## 5. Autosave Behavior

The application listens for form changes and delays autosave until a short period of inactivity.

This demonstrates event-driven frontend logic and a basic debounce-style pattern rather than writing on every individual keystroke.

## 6. CRUD-Style Workflow

Users can:

- Create/save an episode
- Review saved episodes
- Edit existing episodes
- Duplicate an episode as a template for another show
- Delete episodes

Although implemented locally, these interactions mirror common CRUD product behavior.

## 7. Production Timeline Modeling

Segments include timestamps and specialized content categories, allowing the application to function as a lightweight run-of-show planning system rather than a generic note-taking form.

## 8. PDF Generation

Episode objects are transformed into a formatted timeline document and exported as PDF through a browser library.

This demonstrates transforming application state into a different presentation format for real operational use.

## 9. CSV Serialization

Multiple episode objects are flattened into tabular rows and converted into downloadable CSV content using browser-native APIs.

This supports spreadsheet workflows and demonstrates practical data interchange logic.

## 10. Email Workflow Generation

The planner transforms episode state into a readable production brief and constructs a pre-filled email action.

This reduces repetitive copy/paste work when sharing plans with collaborators.

## 11. Framework-Free Frontend Engineering

The project is implemented with HTML, CSS, and vanilla JavaScript rather than relying on React or another component framework.

That makes it useful portfolio evidence for:

- DOM manipulation
- Event listeners
- State handling
- Browser APIs
- Data serialization
- Dynamic rendering
- UI workflow design

## 12. Appropriate Architectural Restraint

Not every useful tool needs a backend or large framework. The original requirements could be solved as a static client-side application, reducing deployment and infrastructure complexity.

The project also documents where that architecture stops being appropriate—particularly for collaboration, sensitive data, and multi-user access.

## Hiring Signal

SK Episode Planner is strongest as evidence of practical frontend/product engineering: taking a real recurring workflow, modeling its data, automating repetitive outputs, and shipping it as a focused browser tool.

It complements larger full-stack and AI portfolio projects by demonstrating that technology choices were made according to the problem rather than by defaulting to the largest possible stack.
