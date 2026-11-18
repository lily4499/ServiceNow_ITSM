# ServiceNow ITSM | End-to-End IT Operations

**Two-phase case study: Laptop request fulfillment + recurring Wi-Fi incident, problem, and change management.**

**Platform:** ServiceNow · **Focus:** IT Service Management (ITSM) · **Environment:** Training instance

> **Evidence status:** Screenshots are from my ServiceNow lab. The laptop request reached the approval/fulfillment stage; the Wi-Fi incident was escalated, its problem record was closed, and the related change reached **Authorize** with tasks still **Open**. I do not present pending work as completed deployment.

## Business scenario

In an office IT environment, I handled two different types of service-desk work:

- **Phase 1 — Employee service request:** A developer needs a MacBook Pro. IT must capture the order, obtain the required approval, and route the item for fulfillment.
- **Phase 2 — Service disruption:** An employee cannot connect to corporate Wi-Fi. IT triages and escalates the incident, investigates recurring failures as a problem, and plans a controlled network configuration change.

<img width="1071" height="443" alt="image" src="https://github.com/user-attachments/assets/25cb1ce1-3b96-4418-b0cb-ce66d0f7a4f9" />


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

<img width="1913" height="571" alt="image" src="https://github.com/user-attachments/assets/fc092749-ac2e-489f-8b93-19b442d4b870" />


*Evidence: ServiceNow confirmed the catalog order was submitted.*

### 2. Track the approval

I reviewed the approval associated with the request. The approval task initially displayed **Requested**; the requested-item form later displayed **Approved**.

<img width="1881" height="915" alt="image" src="https://github.com/user-attachments/assets/2dc4bb16-d5ec-4684-926f-46f36d640244" />


<img width="1868" height="829" alt="image" src="https://github.com/user-attachments/assets/3a14ee60-04fb-4a46-8fa8-c3a228291303" />


*Key distinction: An approval request is not the same as an approved request. These screenshots show the two displayed states; the approver's audit record is not shown.*

### 3. Confirm fulfillment routing

I opened the requested item and checked its **Catalog Tasks** related list. ServiceNow generated **SCTASK0010001**, assigned to **Procurement**, with the description **“Items ready to be fulfilled from stock.”**

<img width="1890" height="888" alt="image" src="https://github.com/user-attachments/assets/98ba7276-94b4-44e1-95e0-624ba7340cc8" />


**Phase 1 result:** Request submitted; approval displayed as Approved; fulfillment task created and still **Open**. **Delivery is not evidenced.**

---

## Phase 2 — Incident → Problem → Change Management

**Scenario:** An employee reports failed corporate Wi-Fi authentication. Because the issue could recur, IT records the immediate incident, investigates the broader problem, and prepares a controlled configuration change.

### 1. Triage and escalate the incident

I documented **INC0010007**, *“Employee unable to connect to corporate Wi-Fi.”* The record shows **Network** category, **High** impact and urgency, and calculated **P1 – Critical** priority. I assigned it to the network support group and recorded an escalation note in the activity stream.

<img width="1891" height="704" alt="image" src="https://github.com/user-attachments/assets/d524fa4b-7e62-40e0-a3af-1054e7df81fd" />


*Evidence: The incident was **In Progress** and assigned to the network team; resolution is not shown.*

### 2. Open the related problem

To investigate the repeated authentication failures, I created **PRB0040002** with **INC0010007** as its **Origin task**.

<img width="1899" height="786" alt="image" src="https://github.com/user-attachments/assets/04e1f729-a25e-496d-9022-f74e5cba3d20" />


*Why a problem record? An incident tracks interrupted service; a problem tracks the investigation into the underlying cause.*

### 3. Track investigation and problem closure

I progressed the problem through **Assess → Root Cause Analysis → Fix in Progress → Resolved → Closed**. The activity history shows **Fix Applied** as the resolution code.

<img width="1900" height="893" alt="image" src="https://github.com/user-attachments/assets/04fbd479-2e49-46a4-add4-98d9f4b5edd2" />


<img width="1900" height="876" alt="image" src="https://github.com/user-attachments/assets/8a05a73c-b844-4585-b9ec-099bcb190856" />


*Evidence: Workflow progression and closure are visible. These screenshots do **not** establish a specific technical root cause or provide test results for a deployed network correction.*

### 4. Create a controlled change

I created **CHG0030001**: *“Correct corporate Wi-Fi authentication configuration.”* The purpose was to document a planned network configuration correction rather than make an untracked change.

<img width="1905" height="879" alt="image" src="https://github.com/user-attachments/assets/7ee7bb1c-f3e5-463f-a311-06a784691e23" />


### 5. Record implementation and recovery plans

In **Planning**, I entered three parts of the proposed work:

- **Implement:** Back up current settings, apply authorized authentication settings, then validate connectivity.
- **Back out:** Restore the previous configuration if verification fails.
- **Test:** Confirm successful Wi-Fi authentication and required resource access; monitor for recurrence.

<img width="1903" height="886" alt="image" src="https://github.com/user-attachments/assets/dc74f78b-63ee-4645-8e37-aaf3b733c6c2" />


*The screenshot also shows blank Justification and Risk/Impact fields. These should be completed before implementation.*

### 6. Route for authorization

I moved **CHG0030001** to **Authorize**. The form explicitly displayed **“Change is waiting for approval.”**

<img width="1910" height="926" alt="image" src="https://github.com/user-attachments/assets/bd85e90e-3288-4034-b8ef-45446db41483" />


*Evidence: Authorization was requested, **not granted** in this screenshot.*

### 7. Organize the change tasks

I reviewed the three linked change tasks:

1. **CTASK0010001** — Back up wireless configuration
2. **CTASK0010002** — Apply approved settings
3. **CTASK0010003** — Validate connectivity and monitor authentication

<img width="1881" height="894" alt="image" src="https://github.com/user-attachments/assets/ecff7560-d95a-4b40-9e4c-1c4ab74ae817" />


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


