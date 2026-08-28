# Data Architecture & API-First Frontend

How to design frontend products around real data contracts, not decorative
content. This separates screenshot-quality frontend from actual
product-quality frontend.

## Core principle

**Let API data shape the UI.** Don't start with "I need a dashboard, therefore
I'll make 6 cards and 2 charts." Start with:

```
What data exists?
       ↓
What relationships exist?
       ↓
What decisions does the user make?
       ↓
What information is most important?
       ↓
What interface best communicates it?
```

If the product has a backend/API concept, the frontend should be designed
around real data contracts — not arbitrary KPI cards and decorative numbers.

---

## 1. Replace fake dashboard data with realistic data architecture

Never generate:

```
Revenue: $42,391
Users: 12,483
Growth: +24%
```

just to fill space.

Instead, when the product has a backend/API concept, the frontend should be
designed around real data contracts:

- Identify the entities/resources
- Define the expected API responses
- Display realistic API-driven data
- Handle loading/error/empty/partial states
- Handle pagination/filtering/sorting
- Handle stale or unavailable data
- Clearly distinguish demo/mock data from API data

For example, a cold-chain monitoring product:

```
GET  /api/shipments
GET  /api/shipments/{id}
GET  /api/incidents
POST /api/incidents
PUT  /api/incidents/{id}
DELETE /api/incidents/{id}
```

Then the frontend is actually structured to consume those resources — not
decorated with fake numbers.

---

## 2. CRUD should be a first-class product behavior

If the product naturally involves entities that users manage, don't stop at
a beautiful table. The agent should implement the full lifecycle:

### Create
- Create form or drawer
- Validation (client-side + server-side)
- Submission/loading state
- Success feedback
- Server/API error handling
- Optimistic or pessimistic update where appropriate

### Read
- List view (card palette, rich list, or kanban — never raw table)
- Detail view (slide-over or expanded state)
- Search
- Filtering
- Sorting
- Pagination (infinite scroll, load-more, or virtual scroll)
- Relationships between entities

### Update
- Edit form or inline editing where appropriate
- Dirty-state handling (unsaved changes warning)
- Validation
- Save/cancel
- Success/error feedback

### Delete
- Confirmation dialog with clear destructive-action warning
- Loading state during deletion
- Success feedback (entity removed from view)
- Failure recovery (entity still present, error message)

So instead of: "Here's a beautiful Users table," create a **Users management
experience** with the actual workflow.

---

## 3. Generate API integration boundaries

For a template/product, create a clean API layer rather than scattering
`fetch()` everywhere.

### Structure

```
api/
├── client.js          # Base client with auth, interceptors, error handling
├── config.js          # API_BASE_URL, AUTH_ENDPOINT, RESOURCE_ENDPOINTS
├── shipments.js       # Shipment-specific API methods
├── incidents.js       # Incident-specific API methods
└── users.js           # User-specific API methods
```

### Conceptual interface

```js
shipmentApi.getAll({ filters, sort, page })
shipmentApi.getById(id)
shipmentApi.create(data)
shipmentApi.update(id, data)
shipmentApi.delete(id)
```

Then UI components don't need to know how HTTP works. This is particularly
valuable for marketplace buyers because they can replace the API
implementation without rebuilding the UI.

---

## 4. Provide a mock API mode

For a static marketplace template, this is extremely useful.

### Demo mode

```
Demo mode
   ↓
Mock API (same data contract)
   ↓
Same frontend
```

### Production mode

```
Production mode
   ↓
Real API
   ↓
Same frontend
```

So the buyer can see a functioning product immediately, while the
architecture remains ready for a real backend. That's far more valuable than
hardcoding 200 objects into JavaScript.

### Mock implementation

```js
// api/mock/shipments.js
const mockShipments = [
  {
    id: "SHP-20481",
    status: "temperature-excursion",
    temperature: 9.4,
    allowedRange: { min: 2, max: 8 },
    destination: "Milan Distribution Center",
    lastSensorUpdate: "2026-08-17T18:42:00Z",
    incidentId: "INC-1082"
  },
  // ... more realistic entities
];

export const mockShipmentApi = {
  getAll: (params) => delay(300).then(() => filterAndPaginate(mockShipments, params)),
  getById: (id) => delay(200).then(() => mockShipments.find(s => s.id === id)),
  // ...
};
```

---

## 5. Include API states in the design

Every API-driven view must consider these states. Not every product needs
every state, but the agent must reason about which ones apply.

### Required state coverage

| State | Description | UI treatment |
|---|---|---|
| **Initial** | No data loaded yet | Skeleton / shimmer |
| **Loading** | Request in progress | Skeleton with progress indicator |
| **Success — populated** | Data loaded | Content display |
| **Success — empty** | No data matches criteria | Empty state with next step |
| **Error** | Request failed | Error state with retry option |
| **Refreshing** | Background refetch | Subtle indicator (not full skeleton) |
| **Updating** | Mutating a record | Inline loading on affected element |
| **Deleting** | Removing a record | Confirmation → loading → removal |
| **Saving** | Creating or updating | Button spinner + disable |
| **Partial failure** | Some items in batch failed | Per-item error indicators |
| **Offline** | No network connection | Offline banner + cached data |
| **Unauthorized** | Session expired | Redirect to login |
| **Forbidden** | Insufficient permissions | Disabled controls + message |
| **Rate limited** | Too many requests | Backoff indicator |

### The state machine

```
Initial → Loading → Success (populated | empty)
                  → Error → Retry → Loading
Refreshing (background, content still visible)
Updating (optimistic or pessimistic)
Deleting (confirm → loading → remove or error)
Saving (button state → success feedback or error)
```

Not every view needs all of these, but the agent must reason about which
apply. A read-only analytics view needs fewer states than a CRUD management
interface.

---

## 6. Use realistic API data, not decorative data

Don't create data just because a card needs content. Create relationships
and domain context.

### Bad (decorative)

```json
{
  "name": "John Doe",
  "status": "Active",
  "value": "$12,000"
}
```

### Good (relational, domain-specific)

```json
{
  "id": "SHP-20481",
  "status": "temperature-excursion",
  "temperature": 9.4,
  "allowedRange": { "min": 2, "max": 8 },
  "destination": "Milan Distribution Center",
  "lastSensorUpdate": "2026-08-17T18:42:00Z",
  "incidentId": "INC-1082"
}
```

Now the UI has something meaningful to communicate. The status implies a
problem. The temperature vs. allowed range tells a story. The incident ID
creates a relationship. The timestamp implies urgency.

---

## 7. Make CRUD interactions visually intelligent

The interaction pattern should match the task, not default to the same
pattern for everything.

### Interaction mapping

| Task type | Pattern | Example |
|---|---|---|
| Quick property change | Inline editing | Toggle notification preference, change status |
| Single-field edit | Inline with confirmation | Change shipment destination |
| Complex creation | Dedicated form/drawer | Create new shipment with multiple fields |
| Dangerous deletion | Confirmation dialog with consequences | Delete customer record |
| Bulk operations | Selection + contextual toolbar | Archive multiple records at once |
| Detail-heavy object | Master-detail or slide-over | View shipment with timeline, incidents, telemetry |
| Simple form | Modal | Quick note or comment |
| Multi-step workflow | Full-page or large drawer | Onboarding, complex configuration |

Don't make every action: click button → generic modal → form. The interaction
pattern should feel intentional.

---

## 8. Add optimistic UI only when appropriate

The agent should reason about whether an action can safely update the UI
immediately.

### Safe for optimistic update

```
Toggle notification preference
        ↓
Optimistic UI update (instant)
        ↓
API call
        ↓
Rollback if failure
```

Other safe cases:
- Star/unstar a record
- Change a sort preference
- Expand/collapse a section
- Mark as read

### Not safe for optimistic update

```
Delete customer
        ↓
Confirm dialog
        ↓
API call
        ↓
Remove from view after success
```

Other cases requiring confirmation:
- Bulk operations
- Financial transactions
- Irreversible data changes
- Actions with downstream effects

This makes the generated application feel much more intentional.

---

## 9. Include API configuration

For marketplace products, provide a clean configuration layer.

### Structure

```
config/
├── api.config.js
└── environment.example.js
```

Or the equivalent for the chosen stack.

### What the buyer should be able to configure

```js
// api.config.js
export const apiConfig = {
  baseUrl: process.env.API_BASE_URL || "https://api.example.com/v1",
  authEndpoint: "/auth/login",
  resources: {
    shipments: "/shipments",
    incidents: "/incidents",
    users: "/users",
  },
  timeout: 10000,
  retries: 2,
};
```

The buyer should be able to configure these without hunting through 30 files.

---

## 10. Authentication should connect to the API architecture

Even if the demo is static, prepare the authentication flow:

```
Login
   ↓
Authentication service
   ↓
Token / session storage
   ↓
API client (attaches auth headers automatically)
   ↓
Authenticated requests
```

### Example

```js
// api/client.js
class ApiClient {
  constructor(config) {
    this.baseUrl = config.baseUrl;
    this.token = null;
  }

  setToken(token) {
    this.token = token;
  }

  async request(path, options = {}) {
    const headers = {
      "Content-Type": "application/json",
      ...(this.token && { Authorization: `Bearer ${this.token}` }),
      ...options.headers,
    };

    const response = await fetch(`${this.baseUrl}${path}`, {
      ...options,
      headers,
    });

    if (response.status === 401) {
      this.handleUnauthorized();
      return;
    }

    return response.json();
  }

  get(path) { return this.request(path); }
  post(path, data) { return this.request(path, { method: "POST", body: JSON.stringify(data) }); }
  put(path, data) { return this.request(path, { method: "PUT", body: JSON.stringify(data) }); }
  delete(path) { return this.request(path, { method: "DELETE" }); }
}
```

`apiClient.get("/shipments")` handles authentication automatically rather
than every component managing tokens. For a static demo, this can be mocked.

---

## 11. Don't force CRUD where CRUD doesn't make sense

This is critical. The skill should NOT become "EVERYTHING MUST HAVE CRUD."

A landing page doesn't need CRUD.
A marketing page doesn't need CRUD.
A read-only analytics product may not need CRUD.
A documentation site doesn't need CRUD.

**Instead:** Identify which domain entities are user-managed and implement
the appropriate lifecycle operations for those entities only.

---

## 12. Let the agent create domain-specific workflows

This is where the product becomes much better than generic frontend
generators. Domain workflows are not merely CRUD operations — they are
meaningful state transitions.

### Examples

**Restaurant:**
```
Reservation → seat guest → move table → mark no-show → complete service
```

**Cold chain:**
```
Incident → investigate → assign → attach evidence → resolve → close
```

**Research:**
```
Source → review → annotate → extract evidence → link to claim
```

**Healthcare:**
```
Patient admission → triage → diagnosis → treatment → discharge → follow-up
```

The skill should explicitly state:

> Prefer domain workflows over generic CRUD when the domain has meaningful
> state transitions. Each workflow step should have its own UI treatment,
> data requirements, and success/failure behavior.

---

## 13. Design the dashboard around decisions, not charts

Instead of "Build a dashboard," the agent should internally ask:

```
Who is using this?
        ↓
What are they responsible for?
        ↓
What can change?
        ↓
What requires attention?
        ↓
What decisions do they make?
        ↓
What data supports those decisions?
        ↓
What actions can they perform?
        ↓
Which actions modify data?
        ↓
Which API operations support those actions?
        ↓
What happens when each operation succeeds/fails?
        ↓
Design the interface.
```

This changes the output from "AI-generated frontend" to "AI-generated
frontend application architecture + product design."

For marketplace products, this is considerably more compelling because the
buyer isn't just getting pretty HTML — they're getting a frontend foundation
that can actually be connected to a real API and extended into a real
application.

---

## 14. Entity relationship map

Before designing any view, map the domain entities and their relationships.
This prevents arbitrary UI and ensures the interface reflects real data
structure.

### Example: Cold-chain monitoring

```
Shipment
 ├── status (active | delivered | excursion | archived)
 ├── destination
 ├── origin
 ├── temperature (current)
 ├── allowedRange (min, max)
 ├── sensor (id, type, lastUpdate)
 ├── events[] (timestamp, type, data)
 └── incidents[] (id, status, severity, assignedTo)

Incident
 ├── status (open | investigating | resolved | closed)
 ├── severity (low | medium | high | critical)
 ├── shipmentId (FK → Shipment)
 ├── assignedTo (FK → User)
 ├── evidence[] (type, url, timestamp)
 └── resolution (summary, action, timestamp)

User
 ├── role (admin | operator | viewer)
 ├── assignedIncidents[] (FK → Incident)
 └── activityLog[] (timestamp, action, entity)
```

This naturally suggests:
- **Shipment overview** with status, temperature, and incident count
- **Telemetry** showing temperature over time vs. allowed range
- **Event timeline** showing shipment history
- **Incident relationship** linking to shipment context
- **Incident management** with assignment, evidence, and resolution workflow

Rather than arbitrary KPI cards and generic charts.

---

## Summary

The difference between "AI-generated frontend" and "AI-generated frontend
application architecture + product design":

| Generic | Architecture-first |
|---|---|
| 6 KPI cards with fake numbers | Dashboard designed around user decisions |
| Beautiful Users table | User management experience with full CRUD |
| Static mock data hardcoded in components | API layer with mock mode and real-mode switch |
| Every action opens the same modal | Interaction patterns matched to task type |
| "Revenue: $42,391" | "42 active shipments, 8 requiring review" |
| No loading/error/empty states | Complete state machine for every view |
| Fetch scattered in components | Clean API boundary with auth integration |
| Same CRUD pattern everywhere | Domain-specific workflows with state transitions |
