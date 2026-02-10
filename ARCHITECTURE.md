# ARCHITECTURE.md

**Technical Layer Specifications for The Consult Model**

---

## Overview

The Consult Model is a five-layer architecture where **each layer has a specific responsibility and cannot violate the layer boundaries**.

This document specifies:
- What each layer does
- What each layer **cannot** do
- How the layers interact
- How this maps to existing architectural frameworks

---

## Layer Stack

```
┌─────────────────────────────────────────────┐
│  Layer 5: Memory Principle                  │  ← Stateless by design
├─────────────────────────────────────────────┤
│  Layer 4: Governance Layer                  │  ← Legal/policy enforcement
├─────────────────────────────────────────────┤
│  Layer 3: Physician Interface               │  ← Human authority preserved
├─────────────────────────────────────────────┤
│  Layer 2: Cognitive Navigation Layer        │  ← AI reasoning (ephemeral)
├─────────────────────────────────────────────┤
│  Layer 1: Record Layer                      │  ← EHR (immutable)
└─────────────────────────────────────────────┘
```

---

## Layer 1: Record Layer (The Foundation)

### Purpose
The immutable source of truth. The legal medical record.

### Components
- EHR system
- Clinical notes
- Lab results
- Imaging reports
- Medication records
- Visit summaries
- Audit trails

### What This Layer Does
- Stores all medical documentation
- Provides read access to authorized systems
- Maintains legal chain of custody
- Enforces HIPAA compliance

### What This Layer CANNOT Do
- **Nothing.** This layer is the ground truth and is untouched by the Consult Model.

### Interface to Layer 2
- **Direction:** One-way (Layer 1 → Layer 2)
- **Access:** Read-only API
- **Format:** FHIR, HL7, or proprietary EHR format
- **Authentication:** Standard EHR access controls

### Architectural Parallel
**From Connector OS Layer 1 (Sensors):**  
"Raw input from environment, unmodified"

---

## Layer 2: Cognitive Navigation Layer (The AI Reasoning)

### Purpose
Read the entire medical record, reason over it, extract patterns, and present insights.

**This is where the AI lives.**

### Components
- Context compression engine
- Temporal stitcher (timeline reconstruction)
- Contradiction detector
- Pattern recognizer
- Trajectory analyzer

### What This Layer Does

#### Context Compression
- Reads 10+ years of clinical notes
- Extracts key events, decisions, treatments
- Generates high-level summary: *"Patient has 10-year history of autoimmune management with three medication switches"*

#### Temporal Stitching
- Reconstructs timeline from fragmented documentation
- Identifies: diagnosis → treatment → response → modification
- Shows: "This medication was tried in 2018, stopped due to side effects, retried in 2023"

#### Contradiction Detection
- Finds conflicting information across notes
- Example: "Note from 2020 says 'no drug allergies', note from 2022 says 'allergic to penicillin'"
- Flags for clinician review

#### Pattern Surfacing
- Identifies recurring symptoms across visits
- Correlates medication changes with symptom reports
- Highlights: "Patient reports fatigue in 8 of last 12 visits"

#### Treatment Trajectory
- Maps: Initial treatment → modifications → current state
- Shows decision points and rationale (when documented)
- Answers: "Why are we on this third-line therapy?"

### What This Layer CANNOT Do
- **Write** anything to Layer 1
- **Store** any reasoning outputs
- **Remember** previous sessions
- **Learn** from patient data
- **Generate** medical records
- **Modify** clinical documentation

### Interface to Layer 3
- **Direction:** One-way (Layer 2 → Layer 3)
- **Format:** Structured insights, natural language summaries
- **Persistence:** Zero (discarded on session close)

### Architectural Parallel
**From Connector OS Layer 3 (Control Logic):**  
"Processes signals, applies control laws, decides when/how to act"

**From SMA-SIB (Semantic Canonicalization):**  
"Compresses to meaning without storing instances"

---

## Layer 3: Physician Interface (The Human Control Surface)

### Purpose
Present AI reasoning to the clinician in a way that preserves their authority and decision-making role.

### Components
- Query interface
- Visualization dashboard
- Timeline view
- Contradiction alerts
- Pattern highlights

### What This Layer Does

#### Query-Driven Interaction
Clinician asks:
- "What's the timeline here?"
- "Why was this medication changed?"
- "What contradictions exist?"
- "What am I missing in these 20 pages?"

AI responds with:
- Focused summaries
- Highlighted sections
- Direct answers to questions

#### Visual Presentation
- Timeline graphs
- Medication history charts
- Symptom frequency heatmaps
- Contradiction markers

#### Authority Preservation
Output never says:
- *"You should prescribe X"*
- *"The diagnosis is Y"*
- *"Here's your note"*

Output always says:
- *"Based on the record, the timeline appears to be..."*
- *"Three contradictions were found..."*
- *"These sections may be relevant..."*

### What This Layer CANNOT Do
- **Make** clinical decisions
- **Recommend** specific treatments
- **Generate** documentation
- **Store** interaction history
- **Persist** session data

### Interface to Layer 4
- **Direction:** Two-way (Layer 3 ↔ Layer 4)
- **Purpose:** Governance checks, access logging
- **Content:** Metadata only (not reasoning outputs)

### Architectural Parallel
**From Connector OS Layer 4 (Actuators):**  
"Presents information to human; does not force action"

---

## Layer 4: Governance Layer (The Constraint Enforcer)

### Purpose
Enforce legal, ethical, and operational boundaries. Ensure the system cannot violate its invariants.

### Components
- Access control enforcement
- Session management
- Non-archival policy engine
- Audit trail (access only, not content)
- Legal classification metadata

### What This Layer Does

#### Session Management
- Initiates session on clinician request
- Tracks session duration
- **Purges all Layer 2 outputs on session close**
- No persistent session storage

#### Access Logging
- Records: Who accessed which patient record
- Records: When access occurred
- Records: Which queries were made (metadata only)
- **Does NOT record:** AI reasoning outputs or content

#### Non-Archival Enforcement
- Blocks any attempt to save AI outputs to EHR
- Prevents export to external systems
- Enforces: Outputs are display-only
- No "save" or "copy to clipboard" for summaries

#### Legal Classification
- Tags all outputs as "temporary clinical tool"
- Marks as non-citable in legal proceedings
- Maintains terms of use prohibiting documentation use
- Provides legal basis for non-discoverability

### What This Layer CANNOT Do
- **Relax** invariants based on clinician request
- **Allow** storage of AI outputs "just this once"
- **Permit** export "for convenience"
- **Override** session purge on close

### Interface to Layer 5
- **Direction:** One-way (Layer 4 → Layer 5)
- **Purpose:** Verify statelessness enforcement
- **Check:** Confirm no persistent memory exists

### Architectural Parallel
**From Doctrine of Externalization (Layer 4: Capability Gating):**  
"Knowing how to do something doesn't imply permission to execute"

---

## Layer 5: Memory Principle (The Stateless Guarantee)

### Purpose
Ensure the system **cannot remember** patients, sessions, or interactions.

### Components
- Stateless processing architecture
- Fresh-read enforcement
- Cross-patient isolation
- Memory purge protocols

### What This Layer Does

#### Stateless Processing
- Every session starts fresh
- No state carried between sessions
- No "user profile" for patients
- No "learned preferences"

#### Fresh Read Every Time
- Reads EHR anew each session
- Does not cache previous reasoning
- Does not reference prior summaries
- Treats each interaction as first contact

#### Cross-Patient Isolation
- No information from Patient A available when processing Patient B
- No aggregate patterns stored
- No "this patient is similar to that patient" logic
- Complete isolation boundary

#### Memory Purge on Close
- All Layer 2 outputs deleted
- All intermediate reasoning states cleared
- All query history discarded
- System returns to ground state

### What This Layer CANNOT Do
- **Retain** any patient-specific information
- **Build** patient profiles over time
- **Learn** from interaction patterns
- **Persist** anything beyond session boundary

### Verification
- Post-session memory scan → **Must be empty**
- Cross-session correlation test → **Must fail**
- Patient re-identification test → **Must fail**

### Architectural Parallel
**From The Continuity Problem:**  
"Persistence without governance is the risk"

**From SMA-SIB:**  
"System cannot reconstruct specific instances"

**From Connector OS Layer 5 (Human State Loop):**  
"State awareness without state *persistence*"

---

## Data Flow

```
┌─────────────────────────┐
│  Clinician opens chart  │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Layer 1: EHR (read)    │ ◄── Immutable
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Layer 2: AI reasons    │ ◄── Ephemeral processing
│  (temporal stitching,   │
│   pattern detection,    │
│   contradiction check)  │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Layer 3: Display to    │ ◄── Human authority preserved
│  clinician (query-      │
│  driven, non-directive) │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Layer 4: Governance    │ ◄── Access logged (not content)
│  (access control,       │
│   non-archival checks)  │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────┐
│  Layer 5: Memory purge  │ ◄── Stateless guarantee
│  (session close, all    │
│   outputs deleted)      │
└─────────────────────────┘
```

**Critical property:** Information only flows one direction through reasoning layers, and **disappears** at session close.

---

## Failure Modes and Containment

### Failure Mode 1: Attempt to save AI output to EHR
**Containment:** Layer 4 blocks at API level (no write access exists)

### Failure Mode 2: Attempt to persist session data
**Containment:** Layer 5 architectural enforcement (no storage backend exists)

### Failure Mode 3: Attempt to recall previous session
**Containment:** Layer 5 fresh-read enforcement (no memory mechanism exists)

### Failure Mode 4: AI makes clinical recommendation
**Containment:** Layer 3 interface design (no directive outputs possible)

### Failure Mode 5: Outputs become legal evidence
**Containment:** Layer 4 legal classification (explicitly non-citable)

---

## Mapping to Existing Architectural Frameworks

### Connector OS Principles Applied
| Connector OS Layer | Consult Model Layer | Adaptation |
|--------------------|---------------------|------------|
| Layer 1: Sensors | Layer 1: EHR | Medical record as "sensor" input |
| Layer 3: Control Logic | Layer 2: AI Reasoning | Control laws → reasoning patterns |
| Layer 4: Actuators | Layer 3: Physician Interface | Present info, don't force action |
| Layer 5: Human State | Layer 4: Governance | Boundaries on intervention |

**Key insight:** Clinical reasoning is a control problem, not a prediction problem.

### SMA-SIB Principles Applied
| SMA-SIB Concept | Consult Model Application |
|-----------------|---------------------------|
| Structural irreversibility | Cannot reconstruct patient identity from outputs |
| Semantic canonicalization | Compress to meaning without storing verbatim |
| No persistent vectors | No embeddings stored across sessions |
| Privacy through architecture | Cannot violate PHI even under compromise |

**Key insight:** Privacy through inability to store, not inability to access.

### Doctrine of Externalization Applied
| Doctrine Principle | Consult Model Application |
|--------------------|---------------------------|
| Explainability | AI reasoning is visible to clinician |
| Contestability | Clinician can close session anytime |
| Capability gating | Reading ≠ permission to write |
| Trust through architecture | Safety from constraints, not alignment |

**Key insight:** Trust emerges from what the system *cannot* do.

### Continuity Problem Applied
| Continuity Concept | Consult Model Application |
|--------------------|---------------------------|
| Persistence is risk | Stateless sessions prevent continuity risk |
| Governance precedes memory | Layer 4 exists before Layer 5 allows processing |
| Structural containment | Cannot form preferences across patients |

**Key insight:** Ephemeral by design prevents governance escape.

---

## Implementation Notes

### Technical Stack (Example)
- **Layer 1 Interface:** FHIR API (read-only)
- **Layer 2 Processing:** Stateless lambda/function architecture
- **Layer 3 Frontend:** Web interface, no local storage
- **Layer 4 Enforcement:** API gateway with hard constraints
- **Layer 5 Verification:** Post-session memory audit

### Security Considerations
- Authentication: Standard EHR SSO
- Authorization: Clinician role-based
- Encryption: In transit (not at rest, because nothing persists)
- Audit: Access logs only, retained per HIPAA requirements

### Performance Characteristics
- Latency: +2-5 seconds per query (acceptable for pre-reading task)
- Throughput: Concurrent sessions per clinician
- Resource: Stateless scales horizontally

---

## Summary

The Consult Model architecture achieves safety through **structural constraints**, not behavioral alignment:

- **Layer 1:** Source of truth (untouched)
- **Layer 2:** Ephemeral reasoning (disappears on close)
- **Layer 3:** Human control (clinician retains authority)
- **Layer 4:** Governance enforcement (hard boundaries)
- **Layer 5:** Stateless guarantee (cannot remember)

**Result:** A system that helps humans reason over impossible records without creating legal, privacy, or authority risks.

---

*"Safety through what the system cannot do."*
