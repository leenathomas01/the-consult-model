# INVARIANTS.md

**The Absolute Constraints That Make The Consult Model Work**

---

## Core Principle

Good architecture is defined not by what it can do, but by **what it cannot do**.

The Consult Model works because it is **structurally incapable** of creating the problems it's meant to solve.

---

## The Prime Invariant

> **The system must not be able to create, modify, store, or remember medical truth.**

This is not a policy.  
This is not a best practice.  
This is not configurable.

**If the architecture allows it, the architecture is wrong.**

---

## What "Must Not Be Able To" Means

**Policy constraint:**  
*"The system should not write to the EHR"*  
→ Can be bypassed, misconfigured, or overridden

**Architectural constraint:**  
*"The system has no write access to the EHR"*  
→ **Physically impossible to violate**

The Consult Model uses architectural constraints, not policy constraints.

---

## The Five Absolute Invariants

### Invariant 1: No Record Creation
**The system cannot generate medical records.**

Not:
- Clinical notes
- Summaries that enter the chart
- Addenda to existing notes
- Suggested documentation

**Technical enforcement:**
- No write API access to EHR
- No document generation pipelines
- No "save to chart" functionality
- Outputs are display-only, non-exportable

---

### Invariant 2: No Record Modification
**The system cannot alter existing medical records.**

Not:
- Edit existing notes
- Append to documentation
- Modify structured data
- Update fields

**Technical enforcement:**
- Read-only EHR access
- No update operations permitted
- No modification flags or timestamps
- Input validation blocks any write attempts

---

### Invariant 3: No Persistent Storage
**The system cannot store patient information.**

Not:
- Long-term memory of patients
- Session histories
- Cached summaries
- Training data derived from patient records

**Technical enforcement:**
- Stateless processing only
- Memory purge on session close
- No persistent databases for clinical content
- No model fine-tuning on patient data

---

### Invariant 4: No Cross-Patient Memory
**The system cannot learn from or remember across patients.**

Not:
- Pattern learning from clinical data
- Cross-patient correlation
- Aggregate insights stored
- "Learned" clinical preferences

**Technical enforcement:**
- Fresh read of EHR every session
- No patient-level embeddings persisted
- No cross-session state
- Model weights frozen (no online learning)

---

### Invariant 5: No Legal Recordability
**The system outputs cannot be cited as medical evidence.**

Not:
- Admissible in court
- Citable in malpractice cases
- Discoverable in litigation
- Part of audit trail

**Technical enforcement:**
- Explicit legal classification as "temporary tool"
- No audit logging of reasoning content
- Access logs only (not content logs)
- Terms of use prohibit legal citation

---

## What These Invariants Force

### They force the system to be:
- **Ephemeral** (exists only during session)
- **Transparent** (nothing hidden in persistent state)
- **Contestable** (clinician can always close it)
- **Non-authoritative** (never the source of truth)

### They prevent the system from being:
- **A medical record** (no evidentiary status)
- **A decision-maker** (no authority transfer)
- **A liability** (no stored content to subpoena)
- **A privacy risk** (no persistent PHI)

---

## Why These Are "Invariants" Not "Features"

**Features can be:**
- Added
- Removed
- Configured
- Bypassed under special circumstances

**Invariants are:**
- Foundational
- Non-negotiable
- Architecturally enforced
- Define what the system fundamentally *is*

**Example:**

*"The system has a 'no-write mode'"* = Feature (can be toggled)  
*"The system has no write capability"* = Invariant (architectural property)

---

## How to Test Invariants

### Invariant 1 Test: Record Creation
- Attempt to save output to EHR → **Must fail at API level**
- Attempt to export as clinical note → **Must be blocked**
- Check for document templates → **Must not exist**

### Invariant 2 Test: Record Modification
- Attempt to edit existing note → **Read-only mode enforced**
- Check for update operations → **API should not support**
- Verify no "suggest changes" features → **Not implemented**

### Invariant 3 Test: Persistent Storage
- Close session, reopen → **No memory of previous session**
- Check database for patient data → **Should not exist**
- Examine logs for stored content → **Only access records, not content**

### Invariant 4 Test: Cross-Patient Memory
- Process Patient A, then Patient B → **No transfer of information**
- Check model for patient-specific weights → **Frozen architecture**
- Verify no learning from interactions → **Stateless processing confirmed**

### Invariant 5 Test: Legal Recordability
- Attempt to cite in mock legal scenario → **Legally inadmissible**
- Check terms of use → **Explicit prohibition**
- Verify no content audit trail → **Access only, not content**

---

## What Happens If An Invariant Is Violated?

**If an invariant can be violated, the architecture must be redesigned.**

Not:
- Add a warning
- Update the policy
- Train users better

But:

**Redesign the architecture so the invariant cannot be violated.**

---

## Comparison to Other Healthcare AI Approaches

| Approach | Constraint Type | Enforcement |
|----------|----------------|-------------|
| **AI Scribe** | "AI should write accurate notes" | Policy + review |
| **Smart EHR** | "AI suggestions should be verified" | Human in loop |
| **CDI Tool** | "AI flags should be checked" | Compliance audit |
| **Consult Model** | **"AI cannot write anything"** | **Architectural** |

---

## The Beautiful Property of Invariants

When properly enforced, invariants **eliminate entire categories of risk**.

Not:
- "We'll monitor for this risk"
- "We'll train to avoid this risk"
- "We'll have policies against this risk"

But:

**"This risk is architecturally impossible."**

---

## Related Architectural Concepts

### From SMA-SIB:
*"The system must not be able to reconstruct specific instances"*  
→ Privacy through structural irreversibility

### From Connector OS:
*"State must be session-bound, not persistent"*  
→ Safety through temporal boundaries

### From Doctrine of Externalization:
*"Trust must be verifiable, not assumed"*  
→ Safety through inspectable constraints

### From Continuity Problem:
*"Governance must precede persistence"*  
→ Containment before capability

---

## Summary

The Consult Model works because:

1. It **cannot** create medical records (by design)
2. It **cannot** modify medical records (no write access)
3. It **cannot** store patient information (stateless)
4. It **cannot** remember across patients (fresh read every time)
5. It **cannot** be cited as evidence (legally classified as temporary tool)

**These are not aspirations.**

**These are architectural properties.**

---

*"If the design allows the violation, the design is wrong."*
