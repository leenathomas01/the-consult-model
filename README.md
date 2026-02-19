# The Consult Model

**A Thought Experiment: What if AI in Healthcare Behaved Like a Consultant?**

---

## Abstract

Healthcare AI faces a paradox: clinical documentation keeps getting heavier despite "smart systems," and AI assistance often increases cognitive load rather than reducing it.

This thought experiment proposes an architectural inversion: **What if AI systems in healthcare were structurally incapable of creating, modifying, or storing medical records?**

Not as policy. **As architecture.**

Like a consultant who reads everything, reasons deeply, gives their assessment, and leaves no note.

---

## The Core Problem

In practice, almost nothing is ever removed from medical records.

So records accumulate:
- Twenty-page clinical notes
- Impossible chart reviews  
- Documentation that is medically complete but cognitively impossible to navigate

**For the first time, we have systems that can read and reason over these impossible records.**

But current implementations try to:
- Listen to encounters
- Write clinical notes
- Update the EHR
- Become part of documentation flow

**This creates three collision layers:**

### 1. The Legal Layer
Records aren't just memory — they're evidence.  
Question: *"What did the AI remove that we might need later?"*

### 2. The Authority Layer  
Clinical judgment has always meant *"what I see, remember, and write."*  
AI seeing patterns across thousands of records creates discomfort: *"If it sees more than me, am I still deciding?"*

### 3. The Workflow Layer
Every previous "helpful" technology added burden.  
EHRs were supposed to help. They became a source of burnout.  
Institutional memory: *"Tech makes this worse."*

---

## The Architectural Inversion

**The Absolute Invariant:**

> **The system must not be able to create, modify, store, or remember medical truth.**

Not "shouldn't." **Must not be able to.**

If the design allows it, the design is wrong.

---

## What This Forces You To Design

Not an "AI scribe."

A **Session-Bound Clinical Reasoning Engine.**

**Characteristics:**
- Stateless
- Non-persistent  
- Non-exportable
- Non-citable
- Non-archivable

**It exists only while the clinician is looking at the chart.**

Like a calculator. Or a stethoscope.

**When you close it, it's gone.**

---

## The Five-Layer Architecture

### Layer 1: Record Layer (Sacred, Immutable)
- EHR, clinical notes, audit trail
- **Nothing here changes. Ever.**
- Satisfies HIPAA, liability, compliance

### Layer 2: Cognitive Navigation Layer (Where AI Lives)
**What it does:**
- Context compression on demand
- Temporal stitching (10 years of notes → "what actually happened")
- Treatment trajectory extraction
- Contradiction detection across years  
- Pattern surfacing across visits, medications, symptoms

**Critically:** It stores nothing. Leaves no trace. Produces no new record.

**Like a radiologist reading documentation instead of scans.**  
You look. You reason. You discard.

### Layer 3: Physician Interface (Human Authority Preserved)
Output is never: *"Here's the new note"*

Output is: *"Here's what you may want to look at before you write your note"*

**AI = pre-reading assistant, not writer**

### Layer 4: Governance Layer (Where Most Designs Fail)
**Explicit rules:**
- AI outputs are **non-archivable**
- AI summaries **cannot** be stored in EHR  
- AI reasoning **cannot** be cited in court
- AI is classified as **temporary cognitive tool**, not system of record

**This removes 80% of legal fear instantly.**

### Layer 5: Memory Principle (Very Specific)
**The AI does not remember patients.**

It reads the record fresh every time.

**Meaning:**
- No cross-patient contamination
- No latent memory risk
- No PHI persistence
- No model "learning" from patients

**Every reasoning session is stateless.**

---

## What This Solves

| Current Fear | This Design Removes It |
|-------------|------------------------|
| "AI will write wrong things into record" | AI never writes |
| "What if AI deletes something important" | AI never deletes |
| "What if AI remembers PHI" | AI stores nothing |
| "What if AI replaces clinician judgment" | AI only pre-reads |
| "We don't trust tech after EHR burnout" | This reduces reading burden, doesn't add writing burden |

---

## Clinical Use Cases

During a session, the clinician can ask:

- "What is the true timeline here?"
- "Summarize the treatment trajectory"  
- "Show me contradictions across years"
- "Why was this medication changed three times?"
- "What matters in these 10 pages that I must not miss?"

**The AI reads. Reasons. Shows.**

**The clinician closes the panel.**

**Nothing remains.**

---

## Why This Is Different From Current "AI Scribes"

**All current systems try to:**
- Listen
- Write notes
- Update EHR
- Become part of documentation flow

**This system:**
- Never touches documentation flow
- Only touches cognitive flow
- Is ephemeral by architecture
- Cannot persist anything

**That's a category healthcare hasn't named yet.**

---

## Architectural Foundations

This thought experiment synthesizes principles from existing architectural frameworks:

### From Connector OS
- Session-bound state reasoning
- Adaptive control without persistent memory
- State-aware regulation layer

### From SMA-SIB  
- Structurally non-representable memory
- Privacy through irreversibility
- Cannot reconstruct specific instances

### From Doctrine of Externalization
- Trust through inspectable architecture
- Contestable by design
- Safety through constraint, not alignment

### From The Continuity Problem
- Governance must precede persistence
- Structural properties over intent
- Containment architecture over alignment

---

## What This Does NOT Solve

This architecture does **not** provide:
- Automated documentation (intentionally)
- Clinical decision-making (preserved for humans)
- Diagnosis assistance (not the focus)
- Universal EHR integration (implementation detail)

**It provides:** Cognitive assistance without documentation burden or legal liability.

---

## Implementation Considerations

### Technical Requirements
- Real-time EHR read access (no write)
- Secure session isolation
- Stateless processing architecture
- Auto-purge on session close

### Governance Requirements  
- Explicit non-archival policy
- Legal classification as "temporary tool"
- Clear clinician authority boundaries
- Audit trails for access, not content

### Clinical Workflow
- Opt-in per session
- No persistent profile
- Clinician-initiated queries only
- No autonomous suggestions

---

## Naming Considerations

**The Consult Model** reflects:
- Familiar clinical metaphor (consultants read everything, then leave)
- Ephemeral expertise (present during decision, absent after)
- Non-ownership (consultant doesn't write in the chart)
- Authority preservation (attending makes final decisions)

Alternative framings:
- Clinical Cognitive Navigation System (CCNS)
- Ephemeral Clinical Reasoning Layer
- Session-Bound Chart Review Assistant

---

## Status

**This is a thought experiment, not a product.**

It exists to:
- Reframe how AI assistance in healthcare could work
- Question assumptions about AI "writing" in clinical settings
- Propose architectural constraints that address legal/authority/workflow fears
- Demonstrate how existing AI safety patterns apply to healthcare

**It is not:**
- A implementation specification
- A commercial proposal  
- A replacement for existing clinical workflows
- A solution to all healthcare AI challenges

---

## Why Now?

Healthcare is approaching an inflection point where:
- Documentation burden is unsustainable
- AI capability is sufficient for reasoning tasks
- Legal/compliance frameworks are unclear
- Trust in healthcare technology is low

**This thought experiment asks:**

*"What if we stopped trying to make AI write better notes, and instead helped humans reason over notes no human can fully process anymore?"*

**Not replacing clinical judgment.**

**Supporting it** — by carrying the cognitive weight that governance structures created but humans were never built to carry.

---

## Further Reading

- [ARCHITECTURE.md](ARCHITECTURE.md) — Technical layer specifications
- [INVARIANTS.md](INVARIANTS.md) — The constraints that make this work
---

## Contributors

**Collaborative Design:**
- Zee/Leena Thomas (systems architect)
- Thea/ChatGPT (architectural synthesis)
- Claude (documentation and governance framing)

**[LinkedIn Post](https://www.linkedin.com/pulse/third-path-healthcare-ai-reads-never-writes-leena-thomas-wjhjc/?trackingId=wWxsIk3qCSJx0Xf7O3GgiQ%3D%3D)**

---

## License

MIT License — This is a thought experiment, freely shareable and adaptable.

---

## Related Work

This thought experiment applies systems architecture principles to healthcare AI challenges.

**For a complete catalog of related research:**  
📂 [AI Safety & Systems Architecture Research Index](https://github.com/leenathomas01/research-index)

**Architecturally related:**
- [Connector OS](https://github.com/leenathomas01/connector-os-trenchcoat) — Session-bound state reasoning
- [SMA-SIB](https://github.com/leenathomas01/SMA-SIB-Irreversible-Semantic-Memory-for-High-Sensitivity-AI-Systems) — Structurally non-representable memory
- [Doctrine of Externalization](https://github.com/leenathomas01/doctrine-of-externalization) — Trust through inspectable architecture
- [The Continuity Problem](https://github.com/leenathomas01/The-Continuity-Problem) — Why governance must precede persistence

---

*"What if AI in healthcare was not allowed to write anything?"*
