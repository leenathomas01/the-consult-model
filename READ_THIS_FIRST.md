# CLINICAL_VIGNETTE.md

**A Day in the Life: How The Consult Model Works in Practice**

---

## Case: Complex Autoimmune Patient

**Patient:** 68-year-old with 12-year autoimmune history

**Documentation:**
- 146 clinical notes
- 9 medication changes
- 3 hospitalizations
- 4 specialists involved
- Last comprehensive review: 18 months ago

**Today:** Annual follow-up. You have 15 minutes to review before the appointment.

---

## Without The Consult Model

You open the chart.

146 notes. Where do you even start?

You skim the most recent visits:
- Fatigue complaints
- Steroid prescription
- Lab work ordered
- Follow-up scheduled

You check medication list:
- Current biologic
- Prednisone (again?)
- Several others

You piece together what you can remember from last time, hope the patient fills in gaps, and walk in somewhat uncertain about the full trajectory.

**Time spent: 10 minutes. Confidence: moderate.**

---

## With The Consult Model

You open the chart before the patient arrives.

You click "Consult."

### Query 1: "Give me the true treatment timeline"

**Response in 3 seconds:**

```
2013: Methotrexate initiated → partial response, stable 18 months
2015: Switched to Azathioprine → stopped after 4 months (elevated LFTs)
2016: Biologic (adalimumab) started → good response, symptom control
2019: Fatigue complaints begin appearing in notes
2021: Steroid bursts prescribed every 3-4 months
2023: Biologic switched (insurance) → current therapy
```

**What you suddenly realize:** This patient was stable for three years, and something changed in 2019 that nobody explicitly connected.

---

### Query 2: "Show me contradictions"

**Response in 2 seconds:**

```
Conflicting information found:

Documentation discrepancy - Drug allergies:
• 2018-03-12: "No known drug allergies" (Dr. Rodriguez, primary care)
• 2020-09-15: "Patient reports sulfa allergy, rash" (Dr. Chen, rheumatology)
• Current med list: No allergy documentation

Lab value pattern - Liver function:
• 2015: "Elevated LFTs led to azathioprine discontinuation"
• 2023: Biologic prescribing note mentions "normal LFTs throughout"
• Query: Were 2015 LFT elevations captured in problem list?
```

**What you suddenly realize:** There's an undocumented sulfa allergy and a missing piece of liver history from 2015 that could matter today.

---

### Query 3: "What patterns am I missing in the last 2 years?"

**Response in 4 seconds:**

```
Pattern noticed - Fatigue reporting:
• Mentioned in 9 of last 12 visits
• Average timing: ~3 weeks before steroid prescription
• Not consistently addressed in treatment plans

Pattern noticed - Steroid use:
• Prescribed 8 times in last 24 months
• Typical course: 20mg taper over 2 weeks
• No documented attempts to address underlying trigger

Pattern noticed - Specialist communication:
• 4 specialists involved
• No shared care plan visible
• Different terminology used for same symptoms
```

**What you suddenly realize:** The steroids aren't the treatment. They're a pattern hiding the real problem.

---

### Query 4: "Summarize the last hospitalization"

**Response in 2 seconds:**

```
Most recent admission: 2021-08-15 (3 days)

Reason: Disease flare, significant joint pain, unable to ambulate
Treatment: IV methylprednisolone, pain management
Discharge: Oral prednisone taper, rheumatology follow-up
Outcome note: "Patient improved, concern about steroid dependence noted"

Follow-up compliance: Attended rheumatology 2 weeks post-discharge
```

**What you suddenly remember:** That hospitalization was the inflection point, but the system never made that visible again.

---

## You Close The Consult Panel

Total time spent: 4 minutes.

**The panel closes. Nothing is saved. No new notes exist.**

But now you walk into that appointment with:
- Complete treatment timeline in your head
- Awareness of documentation gaps (sulfa allergy, liver history)
- Recognition of a pattern (fatigue → steroids, no root cause work)
- Context from the hospitalization 3 years ago
- Clear questions to ask the patient

**Confidence: high. Documentation burden: zero.**

---

## During The Visit

You ask the patient:
- "Tell me about the fatigue. Does it come in waves?"
- "Have we ever worked up why the flares keep recurring?"
- "Do you remember having a reaction to any sulfa drugs?"

The patient confirms:
- Yes, fatigue comes in 3-4 week cycles
- No, mostly just treated flares as they happen
- Yes, had a rash from Bactrim years ago (forgot to mention)

You write your note:
- Document sulfa allergy properly
- Order workup for cyclical fatigue pattern
- Refer to rheumatology for flare prevention strategy, not just flare management
- Discuss steroid minimization plan

**The Consult helped you ask better questions.**

**And that's where good medicine actually happens.**

**You made the clinical decisions.**

**The patient got better care.**

---

## After The Visit

The Consult Model session is gone.

Your note exists in the EHR. Your decisions are documented. Your clinical judgment is preserved.

The AI didn't write anything. It didn't recommend anything. It didn't diagnose anything.

**It just helped you see the 12-year forest instead of 146 individual trees.**

**In 4 minutes.**

**Before the appointment.**

---

## What This Isn't

This is **not**:
- AI making clinical decisions *(You decided on the workup)*
- AI writing documentation *(You wrote the note)*
- AI suggesting treatments *(You chose the plan)*
- AI replacing specialists *(You made the referrals)*

This **is**:
- AI pre-reading an impossible chart
- AI finding patterns across years
- AI flagging contradictions
- AI giving you context before you walk in

**Like a consultant who read everything overnight and caught you before rounds.**

**Except it takes 4 minutes, not 4 hours.**

---

## The Hidden Value

You probably prevented:
- Prescribing a sulfa-based drug (undocumented allergy)
- Another round of steroids without investigating the pattern
- Missing the coordination gap between specialists

You probably improved:
- Patient's understanding that this is a solvable pattern, not random bad luck
- Long-term steroid burden by addressing root cause
- Care coordination by explicitly bringing specialists into shared plan

**None of that came from "AI smarts."**

**It came from helping you see what was already documented but invisible in the noise.**

---

## Why This Works

**The medical record has always been complete.**

**It's just been cognitively impossible to read.**

The Consult Model doesn't make the record better.

**It makes the record readable again.**

Without becoming part of it.

---

*"Like a consultant who reads everything, thinks deeply, and leaves no note."*
