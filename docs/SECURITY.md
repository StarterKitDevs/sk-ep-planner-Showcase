# Security and Scope Review

## Intended Use

SK Episode Planner was designed as a local/browser-based production planning utility, not as a public multi-user SaaS application.

That distinction matters when evaluating its security architecture.

## Current Trust Boundary

The current application:

- Runs entirely in the browser
- Stores episode information in browser `localStorage`
- Does not require user accounts
- Does not expose a custom backend API
- Does not maintain a shared production database
- Uses user-supplied URLs and planning text as local application content

No API credentials, database credentials, authentication secrets, or private environment configuration are required by the core application architecture reviewed for this showcase.

## Dynamic Rendering Consideration

The original implementation generates portions of the history and spreadsheet interfaces using HTML string interpolation and `innerHTML`.

Because episode fields can contain user-entered values, this rendering strategy should **not** be carried unchanged into a shared or untrusted multi-user environment.

A production hardening pass should use one or more of the following:

- `textContent` for plain text
- Explicit DOM element creation
- A vetted sanitization library where rich HTML is actually required
- Framework-level escaping in a future component architecture

## User-Entered URLs

News/research links are user supplied. A production/shared version should validate allowed protocols and handle outbound links defensively.

Recommended controls include:

- Restricting URLs to expected protocols such as HTTPS
- Rejecting unexpected URI schemes
- Adding appropriate `rel` attributes to links opened in new tabs
- Validating imported data before rendering

## Local Storage

`localStorage` is appropriate for the original lightweight single-user use case, but it should not be treated as secure storage for sensitive information.

Users should avoid placing credentials, secrets, or sensitive personal information into episode notes.

A collaborative version should move persistence to an authenticated backend with appropriate authorization and database controls.

## Export Considerations

PDF, CSV, and email outputs reproduce information entered into the planner. Users should review exported content before distributing it.

A production version should additionally consider:

- Spreadsheet formula-injection protection for CSV exports
- Output encoding/escaping
- File naming validation
- Data classification rules
- Audit logging for shared exports

## Authentication and Authorization

The current version has no authentication because it is a browser-local utility.

If deployed as a shared service, authentication alone would not be sufficient. The application would also need authorization rules controlling which users can read, edit, duplicate, export, or delete each episode.

## Recommended Hardening Before Multi-User Deployment

1. Replace unsafe dynamic HTML rendering patterns.
2. Add centralized input validation.
3. Validate outbound URLs and protocols.
4. Protect CSV exports against formula injection.
5. Introduce authenticated server-side persistence.
6. Add per-resource authorization.
7. Add CSRF protections where applicable to the chosen architecture.
8. Add automated security and regression tests.
9. Add dependency monitoring for third-party browser libraries.
10. Define backup, recovery, and audit requirements.

## Portfolio Disclosure

This showcase presents the application according to its actual scope: a useful client-side productivity tool and prototype architecture.

It does not claim that the current browser-local version has the security controls required for storing sensitive information or supporting untrusted multi-user access.
