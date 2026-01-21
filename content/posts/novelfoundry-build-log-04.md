+++
tags = ['NovelFoundry', 'SaaS', 'Build Notes']
title = 'NovelFoundry Alpha to Beta Refactor'
date = 2026-01-21T10:00:00-06:00
draft = false
+++

## How I Stabilized a 2500-Line Dashboard for Maintainable Beta Development

![NovelFoundry Alpha to Beta Refactor](https://pbrazeale.github.io/images/application-refactoring.webp)

NovelFoundry's Alpha proved the feature set worked. Users could upload manuscripts, run analysis for developmental edits, and get detailed reports. The feedback was positive.

But the codebase was becoming a liability.

The dashboard—the heart of the application—had ballooned to 2500 lines in a single file. Every bug fix risked breaking something else.

UI logic, state management, and side effects were tangled together. Auth layout and profile logic were duplicated across pages. Test coverage was minimal because the code was too coupled to test in isolation.

Beta meant opening the doors to more users. So I spent a week refactoring the entire frontend architecture. The result: modular components, standardized hooks and services, shared types, comprehensive tests, and zero lint errors.

The upfront time investment—one week—was significant. But it unlocked long-term velocity. Adding features is faster. Fixing bugs is safer. Deployments are predictable.

## What Alpha Taught Me

Alpha was about velocity. Ship fast, iterate, validate the product. The dashboard grew organically as features landed. Upload manuscripts, poll for analysis jobs, display reports, manage word allotments, handle subscriptions; all in one massive component.

The problems became obvious when I tried to add a new feature. I'd change a state hook and accidentally break the upload flow. Fix a bug in the manuscript list and introduce a regression in report downloads.

Every deploy was a gamble.

The tipping point was when I wanted to add a word tracker feature. There was no clean place to put it. The dashboard was a monolith that had absorbed everything, and adding one more responsibility would push it over the edge.

## Refactor Strategy

I needed a clear separation of concerns. The goal was to split the codebase into three layers:

1. **Presentational components**: pure UI with no side effects or state logic.
2. **Hooks**: isolated state management and effects.
3. **Services and types**: API access and shared domain models.

This pattern is common in React applications, but it's easy to let it slip during rapid prototyping. Alpha was the prototype. Beta requires discipline.

Gone are my days of ship fast and break things. Now I have to deliver reliability and value, so authors incorporate NovelFoundry into their publishing process.

I also standardized layout components across all pages. Auth pages, profile pages, and the dashboard would share the same navigation and visual structure. No more duplicated layout code.

## Dashboard

The dashboard was the biggest risk. I started by identifying the major UI sections and extracting them into separate components under `src/pages/dashboard/components/`:

- **Header**: navigation, user dropdown, subscription badge.
- **Upload card**: drag-and-drop upload with progress indicators.
- **Manuscript list and card**: display manuscripts with status, metadata, and action buttons.
- **Report list**: display analysis reports with download links.
- **Word allotment card**: show remaining words and tier limits.

Dialogs went into `src/pages/dashboard/dialogs/`. Status utilities—functions to determine manuscript state, display text, and action availability went into `src/pages/dashboard/status/`.

The result: the main dashboard file dropped from 2500 lines to ~600. Each component is focused, testable, and reusable.

## Hooks Layer

Side effects and state logic moved into dedicated hooks under `src/hooks/dashboard/`:

- **Subscription gating**: check user tier and enforce feature access.
- **Word allotment**: track remaining words and display tier limits.
- **Project and manuscript queries**: fetch and cache data from the API.
- **Job polling**: poll the backend for analysis job completion.
- **Report downloads**: handle download flows and error states.
- **Timer lockout**: prevent rapid re-submission of analysis jobs.
- **Upload flow**: manage file upload, validation, and progress.

## Services and Shared Types

Data consistency was another pain point in Alpha. Profile data was fetched in multiple places. Job status checks were duplicated across components.

I created `src/lib/profileService.ts` to centralize profile and word-count access. All components that need profile data import this service. If the API changes, there's one place to update.

I defined shared domain models in `src/types/index.ts`: `Profile`, `Project`, `Manuscript`, `Job`, `AnalysisReport`. These types are used everywhere: hooks, components, services. TypeScript catches mismatches at compile time instead of runtime.

## Testing Foundation

Alpha had almost no tests. That was fine for rapid prototyping, but Beta required confidence in deployments. I added Vitest and React Testing Library, then wrote unit tests for critical hooks:

- Subscription gating: does it enforce tier limits correctly?
- Word allotment: does it calculate remaining words accurately?
- Job polling: does it handle completion, failure, and timeout states?

The test suite runs in under five seconds. I can run it on every commit, and CI runs it on every pull request.

## What Beta Unlocks

The refactor establishes a pattern for future features:

1. Define types in `src/types/index.ts`.
2. Create services in `src/lib/` for API access.
3. Build hooks in `src/hooks/` for state and effects.
4. Extract presentational components.
5. Compose everything in the page.

This pattern scales. I can add a word tracker without touching the dashboard page. I can add achievements without refactoring the upload flow.

## What's Next

The foundation is solid, but there's more to build.

- I'll expand test coverage for upload and analysis flows.
- I'll add a new word tracker feature and achievements
- I'll continue optimizing performance, confident that the architecture can support it.

Alpha was about proving the product.
Beta is about scaling it!
