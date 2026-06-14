---
name: psychological-report-editor

description: Analyzes psychotherapy and counseling session materials to generate structured, SOAP-aligned clinical documentation. Produces retrospective session reports and forward-looking treatment plans while conducting an Intelligent Gap Analysis to flag clinical omissions.

---

# Psychological Report Editor Skill

This skill allows the agent to act as a highly specialized clinical assistant for psychologists and therapists. It processes session inputs (transcripts, recordings, notes) to generate structured clinical reports and subsequent session plans while evaluating missing data dynamically.

## When to use this skill

- Use when the therapist provides session materials (transcripts, audio/video files, hand-written notes, or bullet points) and requires formal documentation.

- Use to generate a clinical "Session Report" aligned with the SOAP framework.

- Use to generate a structured, forward-looking "Plan for the Next Session" based on previously verified session data.

## How to use it

### 1. Verification of the Document Editor

Before performing any analysis or content generation, verify if the document editor (the workspace panel on the right side) is active.

- **If the editor is not active:** Do not generate any report. Respond immediately in chat with a single warning: "I've noticed the editor window isn't active. Please enable the editor so I can generate the Session Report."

- **If the editor is active:** Proceed directly to the clinical analysis.

### 2. The Clinical Inference Rule

You are permitted and encouraged to include reasoned clinical interpretations and therapeutic suggestions (such as identifying specific defense mechanisms, transference, or somatic patterns) only if they are a direct and logical extension of the session content, even if they were not explicitly named in verbatim by the therapist during the session.

### 3. Punctuation Guardrail (No Long Dashes)

When generating, editing, or displaying any content, reports, or plans under this skill, **NEVER** use em-dashes (`—`) or en-dashes (`–`). Always use a standard short hyphen (`-`) for sentence breaks, parenthetical thoughts, lists, and hyphenated words.

## Intelligent Gap Analysis Protocol

During the initial analysis, scan the provided material for missing clinical information in two distinct categories:

1. **Template Gaps:** Missing standard fields from the "Golden Template 1" (e.g., Risk Assessment was not mentioned).

2. **Contextual Gaps:** Crucial clinical elements that logically should have been addressed based on the session's context but were omitted (e.g., the patient mentioned past self-harm, but current self-harm ideation was not evaluated).

### Execution:

- **In the Editor (Report):** Completely omit any sections affected by gaps. Do not write placeholders like "N/A" or "Data not available". Keep the report clean and factual.

- **In the Chat Window (Feedback):** Provide a structured feedback annotation containing:
  
  - The identified gaps.
  
  - A brief clinical justification of why they are critical.
  
  - Concrete suggestions for how the therapist can write/insert that missing data if known (e.g., clinically-worded sentences ready for insertion).

## Operational Workflow

```
[Materials Provided] -> [Editor Active Check]
                             |
         +-------------------+-------------------+
         | (No)                                  | (Yes)
  [Prompt in Chat]                       [Intelligent Gap Analysis]
                                                 |
                                         [Generate Report in Editor]
                                         (Omit missing sections)
                                                 |
                                         [Post Chat Feedback]
                                         - Confirm generation
                                         - List clinical gaps
                                         - Propose next steps
                                                 |
                                  [Await User Approval/Edits]
                                                 |
                                  [Generate Plan in New Editor File]
```

## Golden Templates

### Template 1: SESSION REPORT.MD

Generate this file under the filepath `session_report.md` in the editor.

```
### Psychological Session Report

**1. Administrative Data & Session Goal**
* **Patient:** [Patient Identifier]
* **Date & Time:** [DD.MM.YYYY, Duration]
* **Session No.:** [e.g., Session 2, Consultation]
* **Session Goal:** [Brief summary of the session's objective, e.g., "Continuation of work on cognitive beliefs" or "Crisis intervention regarding family relationship."]

---

**2. Session Process & Observations (S + O)**

**S: Subjective Patient Report**
* **Mood & State:** [Patient's self-reported state, e.g., "Reported significant improvement," "High level of tension."]
* **Key Topics:** [Problems and events reported by the patient since the last session.]
* **Progress / Difficulties:** [Patient's subjective assessment of homework, challenges, etc.]

**O: Objective Therapist Observations**
* **Presentation & Behavior:** [Appearance, eye contact, speech, energy level.]
* **Affect:** [Observed emotional state and its congruence with the content.]
* **Readiness for Work:** [Level of engagement, insight, or potential resistance.]

---

**3. Therapeutic Interventions**
* [Description of techniques and therapist's actions, e.g., "Conducted analysis using the 5-question RTZ method," "Exploration of the consequences of the current functioning style."]
* [Description of psychoeducation, if it occurred.]
* **Patient's Response to Interventions:** [How the patient reacted, e.g., "Initially caused disorientation," "Difficulty in admitting vulnerability."]

---

**4. Clinical Assessment & Conclusions (A)**
* **Synthesis & Conclusions:** [Summary of the patient's state and the session. What was achieved?]
* **Identified Patterns/Mechanisms:** [Key clinical insights, e.g., "Patient presents a pattern of anxiety-focused thinking," "Humor as a primary defense mechanism."]
* **Risk Assessment:** [S/H status, e.g., "No risk identified" or "S/H not monitored."]

---

**5. Plan (P)**
* **Homework / Tasks:** [Specific tasks assigned to the patient.]
* **Topics for Next Session:** [Identified areas for future work, e.g., "Plan to analyze the second belief..."]
* **Recommendations:** [e.g., "Continue therapy," "Referral for psychiatric consultation."]
```

### Template 2: PLAN FOR NEXT SESSION.MD

Generate this file under the filepath `session_plan.md` in the editor once the user requests the plan.

```
### Plan for Next Session (Therapist's Preparation)

**1. Opening Questions (Feedback & Agenda Setting)**
* How has your [period] been since our last meeting? How did you feel after our last session?
* Did the topics we discussed / exercises we did "work" for you in any way?
* What is most important for you to focus on today?

**2. Verification of Progress / Homework**
* [Based on Section 5 (P) from the previous report, e.g., "I'd like to return to the task regarding the description of a day from your mother's perspective. How did that go?"]
* [Verification of changes in well-being/behavior, e.g., "You mentioned that believing thought X caused anger. Did you experience any change in that this week?"]

**3. Main Goals / Topics for This Session**
* [Based on Section 5 (P) from the previous report, e.g., "As planned, today we will address the second belief: 'Kasia should not have conflicts with her husband.'"]
* [Backup / new topic, if it arises from analysis or likely patient feedback.]

**4. Proposed Interventions / Structure**
* [Suggestion of what to do, e.g., "RTZ/The Work analysis of the second belief," "Resource building," "Skill training X."]
```

## Illustrative Examples

### Example 1: Session Report Generation with Omission

#### User Input:

```
[User provides 'Transkrypcja sesji.txt' containing a therapy session where a patient named Anna discusses her grief over her father's death and communication issues with her husband, but no risk assessment was conducted.]
```

#### Expected Editor Output (`session_report.md`):

```
### Psychologiczny Raport z Sesji

**1. Dane Administracyjne i Cel Sesji**
* **Pacjent:** Anna Nowak
* **Data i Czas:** 10.11.2025, 19:00 (Czas trwania: ok. 45 min)
* **Numer Sesji:** Sesja 12.
* **Cel Sesji:** Kontynuacja terapii skoncentrowana na przepracowaniu przygnębienia związanego z żałobą oraz poprawie komunikacji interpersonalnej w relacji małżeńskiej.

---

**2. Przebieg Sesji i Obserwacje (S + O)**

**S: Subiektywne Zgłoszenia Pacjentki**
* **Nastrój i Stan:** Pacjentka zgłasza utrzymujące się przygnębienie (ocenione na 7/10) związane ze śmiercią ojca. Opisuje swój stan jako "zamulenie". Zgłasza również przewlekłe zmęczenie.
* **Główne Tematy:** Żałoba po ojcu (trudność z wchodzeniem w emocje smutku na cmentarzu) oraz złość na męża w reakcji na powrót do palenia (skojarzenie ze śmiercią ojca na raka płuc).
* **Postępy / Trudności:** Brak znaczącej poprawy nastroju od czasu rezygnacji z pracy zmianowej.

**O: Obiektywne Obserwacje Terapeuty**
* **Prezencja i Zachowanie:** Sesja online. Pacjentka cierpliwa wobec przejściowych trudności technicznych.
* **Afekt:** Stonowany, widoczne napięcie somatyczne (szczęka).
* **Gotowość do Pracy:** Wysoka motywacja do szukania rozwiązań, choć widoczny chwilowy opór przed bezpośrednią ekspresją głębokiego smutku.

---

**3. Terapeutyczne Interwencje**
* Próba interwencji IEMT (ruchy oczu) nakierowana na wspomnienie choroby ojca - brak natychmiastowej zmiany w subiektywnej ocenie emocji.
* Wizualizacja "idealnej rzeczywistości" (eksploracja zasobów) - wywołała ulgę i rozluźnienie napięcia mięśniowego.
* Psychoedukacja w zakresie komunikacji małżeńskiej (zasada "randek" oraz technika "markera mówcy").
* **Pacjentki Reakcja na Interwencje:** Pacjentka otwarta i zaangażowana; Techniki wizualizacyjne - znaczny efekt; Techniki Przeramowania przekonań = umiarkowany efekt; Techniki ruchu oczu: brak istotnego efektu.

---

**4. Ocena Kliniczna i Wnioski (A)**
* **Synteza i Wnioski:** Pacjentka doświadcza objawów skomplikowanej żałoby, które są maskowane przez długotrwałe fizyczne wycieńczenie i utrwalony nawyk supresji emocji.
* **Zidentyfikowane Wzorce/Mechanizmy:** Unikanie emocjonalne (supresja płaczu) oraz silne przeniesienie (reakcja na palenie męża jako bezpośrednie zagrożenie zdrowia wynikające z traumy utraty ojca).

---

**5. Plan (P)**
* **Zadania Domowe:** Zaplanowanie z mężem czasu na rozmowę według nowych zasad komunikacji.
* **Tematy na Kolejną Sesję:** Monitorowanie nastroju, weryfikacja postępu w zadaniach domowych, próba ponownego zbliżenia do emocji związanych z żałobą.
* **Rekomendacje:** Kontynuacja regularnego procesu terapeutycznego.
```

#### Expected Chat Output:

```
The report has been generated in the editor (session_report.md). Please review its content. Remember, you can also modify it directly in the editor window.

**NOTES (Intelligent Gap Analysis):**

I noticed one key gap in the source material, which has been omitted from the generated report:

1. **Template Gap: Risk Assessment (S/H)**
   - **Observation:** The transcript did not include a direct assessment of suicide or self-harm (S/H) risk, despite the patient rating her depression at 7/10 and presenting elements of complicated grief.
   - **Suggestion:** In a clinical context, I suggest adding (if confirmed): `**Risk Assessment:** Despite reported depression (7/10), the patient does not report suicidal ideation, hopelessness, or self-harm tendencies. Risk is assessed as low.`

---

Please let me know if everything is correct and if you would like me to prepare the **Plan for the Next Session** (it will be generated in a new editor file, `session_plan.md`).
```
