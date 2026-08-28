# UX Audit

Assesses whether the product genuinely works for the person using it.

## Task-flow analysis

For each primary task the product supports:

- Can the user complete it? Trace the full path, including error paths.
- Is the path short and predictable?
- Are the affordances obvious (does the user know what is clickable)?
- Is there appropriate feedback at every step?
- Can the user recover from errors and go back?

## Information architecture

- Is the content organized by user need, not by internal structure?
- Is the most important information visually dominant?
- Is progressive disclosure used where it helps (and absent where it hurts)?
- Is the vocabulary the user's vocabulary, not invented labels?

## States and feedback

- Loading: are loading states shown and are they honest (no fake progress)?
- Empty: does every collection/view have a designed empty state with a next
  step?
- Error: are errors clear, located, and recoverable?
- Success: is completion confirmed without being annoying?

## Content quality

- Is the copy specific and meaningful, or filler? (See
  `design/anti-generic.md`.)
- Are labels, buttons, and messages action-oriented and consistent?
- Is any content misleading or claim-like without basis?

## Consistency

- Do repeated patterns behave identically (search, filters, navigation)?
- Do repeated components use the same names, ordering, and behavior?
- Is the interaction model consistent (one way to do the same thing)?

## Dashboard, Data & CRUD UX Verification

For any data-dense or admin dashboard interfaces:

- **Boring Table Check**: Does the dashboard default to a full-screen, uninspired table? If yes, it fails. Data must be grouped into card-strips, Kanban status pipelines, or master-detail split panels.
- **Scroll & Viewport Constraints**: Does the interface require massive vertical scrolling to view related panels? (Dashboards should seek to maintain a single-screen executive viewport height `100vh` via tabbed overlays or sliding drawers).
- **CRUD Path Closeness**: Can a record be viewed, modified, or deleted without leaving the main dashboard context? (Requires side slide-overs or inline context drawers).
- **Data Visualizations**: Are the charts and sparklines interactive (hover tooltips, highlight links to list views)? Are numbers styled with tabular figures?

## Data Architecture & API-First Frontend Verification

For products with a backend, API, or data-driven concept. Read
`design/data-architecture.md` for full details.

- **Realistic data over decorative data**: Are dashboard numbers tied to
  real entity data (e.g. "42 active shipments, 8 requiring review") or
  are they fabricated metrics ("$42,391 Revenue, 12,483 Users")? Decorative
  data = blocking.
- **Entity relationships modeled**: Do the displayed data structures reflect
  real domain relationships (foreign keys, nested objects, arrays of
  related records) or flat name/status/value objects? Flat = blocking for
  CRUD products.
- **Full CRUD lifecycle**: If the product involves user-managed entities,
  is the full lifecycle implemented — create (form + validation + loading +
  feedback), read (list + detail + search + filter + sort + pagination),
  update (edit + dirty-state + save/cancel), delete (confirmation +
  loading + feedback)? Partial CRUD without workflow = major finding.
- **Interaction pattern matches task**: Are quick edits inline, complex
  creation in drawers/forms, dangerous deletion confirmed, bulk operations
  using selection + toolbar? One-size-fits-all modal for every action =
  major finding.
- **API states present**: Does every API-driven view handle loading,
  success (populated + empty), error, and retry? Missing states = blocking.
- **Mock API mode**: For marketplace templates, is there a mock API
  implementing the same data contract as the real API? Hardcoded data in
  components = major finding.
- **Domain workflows over generic CRUD**: If the domain has meaningful
  state transitions (e.g. reservation → seated → served → completed),
  are these implemented as workflows rather than generic create/edit/delete?
  Generic CRUD where domain workflows exist = major finding.
- **Dashboard designed around decisions**: Does the dashboard answer
  "What decisions does this user make?" or is it a collection of arbitrary
  KPI cards and charts? Arbitrary = major finding.
- **API configuration layer**: Can a marketplace buyer configure
  API_BASE_URL, endpoints, and auth without editing 30 files? Missing
  configuration = major finding for marketplace products.

## Heuristic Check

Nielsen's heuristics, applied fast: visibility of system status; match with the
real world; user control and freedom; consistency; error prevention; recognize
rather than recall; flexibility; aesthetic and minimalist design; help with
errors; help and documentation.

## Sign-off

**Blocking**:
- Any primary CRUD task that cannot be completed or redirects away from dashboard context unnecessarily.
- Use of uninspired raw flat tables with standard pagination without card or canvas alternatives.
- Infinite vertical scrolling layout for simple control panels.
- Missing hover tooltips or legends on primary charts.

**Major**: Inefficient flows, inconsistent behavior, missing states. Fix before ship.
