# ServiceNow ITSM | End-to-End IT Operations

**Two-phase case study: Laptop request fulfillment + recurring Wi-Fi incident, problem, and change management.**

**Platform:** ServiceNow · **Focus:** IT Service Management (ITSM) · **Environment:** Training instance

> **Evidence status:** Screenshots are from my ServiceNow lab. The laptop request reached the approval/fulfillment stage; the Wi-Fi incident was escalated, its problem record was closed, and the related change reached **Authorize** with tasks still **Open**. I do not present pending work as completed deployment.

## Business scenario

In an office IT environment, I handled two different types of service-desk work:

- **Phase 1 — Employee service request:** A developer needs a MacBook Pro. IT must capture the order, obtain the required approval, and route the item for fulfillment.
- **Phase 2 — Service disruption:** An employee cannot connect to corporate Wi-Fi. IT triages and escalates the incident, investigates recurring failures as a problem, and plans a controlled network configuration change.

![Diagram: Phase 1 follows Service Catalog → Approval → Fulfillment → Verify delivery; Phase 2 follows Incident → Problem → Change → Validate.](assets/itsm-workflow.png)

*The diagram shows the intended end-to-end process; screenshots below identify the stages actually evidenced.*

### ITSM record relationships

| Phase | Flow | Purpose |
|---|---|---|
| **1 · Request** | `REQ0010001` → `RITM0010001` → `SCTASK0010001` | One order, its requested laptop item, and the fulfillment task |
| **2 · Service restoration** | `INC0010007` → `PRB0040002` → `CHG0030001` → 3 change tasks | A reported Wi-Fi failure, problem investigation, and a planned permanent correction |

---

## Phase 1 — Service Request Fulfillment

**Scenario:** A developer requests a MacBook Pro through the ServiceNow catalog. The request requires authorization before IT can complete fulfillment.

### 1. Submit the laptop request

I opened **Service Catalog**, selected the developer laptop, submitted the order, and captured the generated **REQ0010001** request number.

![ServiceNow request confirmation with REQ0010001 and MacBook Pro](screenshots/01-request-submitted.png)

*Evidence: ServiceNow confirmed the catalog order was submitted.*

### 2. Track the approval

I reviewed the approval associated with the request. The approval task initially displayed **Requested**; the requested-item form later displayed **Approved**.

![Approval task for REQ0010001 in Requested state](screenshots/02-approval-requested.png)

![RITM0010001 requested item displaying the Approved field](screenshots/03-request-item-approved.png)

*Key distinction: An approval request is not the same as an approved request. These screenshots show the two displayed states; the approver's audit record is not shown.*

### 3. Confirm fulfillment routing

I opened the requested item and checked its **Catalog Tasks** related list. ServiceNow generated **SCTASK0010001**, assigned to **Procurement**, with the description **“Items ready to be fulfilled from stock.”**

![Catalog task SCTASK0010001 linked to RITM0010001](screenshots/04-catalog-task-created.png)

**Phase 1 result:** Request submitted; approval displayed as Approved; fulfillment task created and still **Open**. **Delivery is not evidenced.**

---

## Phase 2 — Incident → Problem → Change Management

**Scenario:** An employee reports failed corporate Wi-Fi authentication. Because the issue could recur, IT records the immediate incident, investigates the broader problem, and prepares a controlled configuration change.

### 1. Triage and escalate the incident

I documented **INC0010007**, *“Employee unable to connect to corporate Wi-Fi.”* The record shows **Network** category, **High** impact and urgency, and calculated **P1 – Critical** priority. I assigned it to the network support group and recorded an escalation note in the activity stream.

![INC0010007 incident showing priority, assignment and escalation activity](screenshots/05-incident-triage-escalation.png)

*Evidence: The incident was **In Progress** and assigned to the network team; resolution is not shown.*

### 2. Open the related problem

To investigate the repeated authentication failures, I created **PRB0040002** with **INC0010007** as its **Origin task**.

![PRB0040002 problem with INC0010007 as origin task](screenshots/06-problem-created.png)

*Why a problem record? An incident tracks interrupted service; a problem tracks the investigation into the underlying cause.*

### 3. Track investigation and problem closure

I progressed the problem through **Assess → Root Cause Analysis → Fix in Progress → Resolved → Closed**. The activity history shows **Fix Applied** as the resolution code.

![Problem PRB0040002 in Root Cause Analysis](screenshots/07-problem-root-cause-analysis.png)

![PRB0040002 activity history showing Fix Applied, Resolved and Closed](screenshots/08-problem-closure-history.png)

*Evidence: Workflow progression and closure are visible. These screenshots do **not** establish a specific technical root cause or provide test results for a deployed network correction.*

### 4. Create a controlled change

I created **CHG0030001**: *“Correct corporate Wi-Fi authentication configuration.”* The purpose was to document a planned network configuration correction rather than make an untracked change.

![CHG0030001 change request created for wireless authentication configuration](screenshots/09-change-request-created.png)

### 5. Record implementation and recovery plans

In **Planning**, I entered three parts of the proposed work:

- **Implement:** Back up current settings, apply authorized authentication settings, then validate connectivity.
- **Back out:** Restore the previous configuration if verification fails.
- **Test:** Confirm successful Wi-Fi authentication and required resource access; monitor for recurrence.

![Change planning section showing implementation, backout and test plans](screenshots/10-change-implementation-test-backout.png)

*The screenshot also shows blank Justification and Risk/Impact fields. These should be completed before implementation.*

### 6. Route for authorization

I moved **CHG0030001** to **Authorize**. The form explicitly displayed **“Change is waiting for approval.”**

![CHG0030001 at Authorize state waiting for approval](screenshots/11-change-awaiting-authorization.png)

*Evidence: Authorization was requested, **not granted** in this screenshot.*

### 7. Organize the change tasks

I reviewed the three linked change tasks:

1. **CTASK0010001** — Back up wireless configuration
2. **CTASK0010002** — Apply approved settings
3. **CTASK0010003** — Validate connectivity and monitor authentication

![Three open change tasks linked to CHG0030001](screenshots/12-change-tasks-open.png)

**Phase 2 result:** Incident escalated; problem record closed; change documented, linked, and awaiting authorization; all three change tasks still **Open**. A completed change implementation is **not** evidenced.

---

## Evidence summary

| Record | Verified stage | What would complete the story |
|---|---|---|
| `REQ0010001` / `RITM0010001` | Order submitted, approval displayed as Approved | Complete procurement task and verify delivery |
| `INC0010007` | In Progress, Network Support escalation | Record actual service restoration and resolution |
| `PRB0040002` | Closed; Fix Applied in activity history | Include documented technical root cause and validation evidence |
| `CHG0030001` | Authorize; approval pending; 3 open tasks | Add risk/justification, obtain authorization, execute/test tasks, and close |

## Skills demonstrated

**ServiceNow navigation · Request/Item/Task relationships · Approval tracking · Incident prioritization · Assignment and escalation · Problem lifecycle · Change planning · Backout and test plans · Linked records · Activity-history documentation**

**Key takeaway:** ITSM is more than creating tickets. A strong service desk makes every request, interruption, investigation, and planned change **traceable**, with clear ownership and evidence of what actually happened.

> **Portfolio note:** This project was completed in a simulated ServiceNow environment. Screenshots document the records and statuses shown, not a production system deployment.
