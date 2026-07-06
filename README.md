<div align="center">

<img src="SOULEYMAN.png" alt="SOULEYMAN — AI Tutor for Mauritanian Students" width="220">

# SOULEYMAN
### The AI Private Tutor, Native to Hassaniya

**Status:** 🟢 In Production &nbsp;·&nbsp; **Version:** 1.0 &nbsp;·&nbsp; **Built by** [Alborda AI](https://alborda.ai)

</div>

---

## 1. What is SOULEYMAN?

**SOULEYMAN** is Alborda AI's AI-powered private tutor for Mauritanian students preparing the **Brevet**, the **Baccalauréat**, or a **national entrance exam (Concours)**. Unlike generic international tutoring apps that translate content into approximate Arabic or French, SOULEYMAN is powered by **Dimeyz**, Alborda's proprietary large language model natively trained on **Hassaniya Arabic** — the everyday spoken language of Mauritania.

SOULEYMAN is not a static course library. It is a **configurable tutoring engine**: every student, regardless of level, stream, or subject, is served by the same core product, with content, difficulty, and exercises driven by configuration — not by code written per subject.

**Who it's for:** individual students (Brevet, Bac, Concours) studying independently, families wanting affordable native-language support, and schools/NGOs deploying tutoring at scale across a class or region.

---

## 2. Why SOULEYMAN is different

| # | Differentiator | What it means in practice |
|---|---|---|
| 01 | **Native Hassaniya teaching** | Explanations are generated directly in Hassaniya by Dimeyz — even for subjects taught at school in Standard Arabic or French — not machine-translated. |
| 02 | **Level × subject × chapter precision** | The same topic (e.g. "functions" in math) is taught differently for Brevet vs. Bac. SOULEYMAN's knowledge base is structured to reflect that, not flattened by subject alone. |
| 03 | **Production-language exercises** | For French and English, methodology is explained in Hassaniya, but exercises and corrections are done in the target language itself — mirroring real exam conditions. |
| 04 | **Voice-first accessibility** | Students can ask questions out loud and get a spoken answer back, powered entirely by Alborda's own Dimeyz Speech — no reliance on third-party ASR/TTS. |
| 05 | **"Explain it differently"** | A single tap gets a fresh explanation with a new analogy or example, instead of repeating the same wording. |
| 06 | **Exam-condition simulations** | Past-paper style tests run under real exam constraints (timed, graded), not just open-ended Q&A. |
| 07 | **Data sovereignty & child safety by design** | No student data trains third-party models; strict moderation and parental consent are built into the core, not bolted on. |

---

## 3. How it works — architecture overview

```
                         ┌─────────────────────────────┐
                         │   Student channels             │
                         │   Mobile App · Web · WhatsApp*  │
                         └──────────────┬────────────────┘
                                        │
                              Pedagogical Orchestration Layer
                    (progress tracking · level/subject/chapter routing ·
                                adaptive difficulty)
                                        │
                    ┌───────────────────┼───────────────────┐
                    │                   │                   │
          Voice question?      Text / written question   Exercise request
                    ▼                   ▼                   ▼
          ┌────────────────┐   ┌─────────────┐   ┌──────────────────────┐
          │ Dimeyz Speech   │   │  RAG layer   │   │ Exercise/Quiz         │
          │ (ASR)           │   │ (curriculum  │   │ Generator + Auto-     │
          │                 │   │  per level/  │   │ Correction Engine     │
          │                 │   │  subject)    │   │                       │
          └────────┬────────┘   └──────┬──────┘   └───────────┬───────────┘
                   └─────────┬──────────┘                      │
                             ▼                                 │
                   ┌───────────────────┐                       │
                   │   Dimeyz (LLM)      │◄──────────────────────┘
                   │ Hassaniya generation│
                   └─────────┬───────────┘
                             │
             Voice channel?  │  Text channel
                   ┌─────────┴─────────┐
                   ▼                   ▼
         ┌──────────────────┐   ┌─────────────┐
         │ Dimeyz Speech     │   │  Direct      │
         │ (TTS)             │   │  reply       │
         └────────┬──────────┘   └──────┬──────┘
                  └──────────┬───────────┘
                             ▼
                 ┌───────────────────────────────┐
                 │   Progress & Reporting            │
                 │  · Mastery status updated          │
                 │  · Weak points logged               │
                 │  · Parent report queued (n8n)        │
                 └───────────────────────────────┘
```

*WhatsApp access shares the same channel infrastructure built for SIDI.*

Every stage is decoupled: the orchestration layer knows the student's level and history, the LLM knows nothing about the channel, and the curriculum knowledge base is scoped per level × subject × chapter. This is what lets new subjects or exam types be added through configuration, not a product rebuild.

---

## 4. Core components

| Component | Role |
|---|---|
| **Dimeyz** | Proprietary LLM natively trained on Hassaniya Arabic. Generates all explanations, in the student's native language. |
| **Dimeyz Speech** | ASR/TTS module powering voice mode — for students more comfortable speaking than writing. |
| **Pedagogical Orchestration Layer** | Tracks each student's progress, routes to the right level/subject/chapter, and adapts exercise difficulty in real time. |
| **Exercise & Quiz Generator** | Produces leveled exercises and self-corrected quizzes with full explanations, not just right/wrong. |
| **RAG Layer** | Retrieves official curriculum content, past papers, and exam-style questions structured by level, stream, subject, and chapter. |
| **Supabase (self-hosted)** | Stores student profiles, progress, results, and session history under full data sovereignty. |
| **n8n Automation** | Generates and delivers periodic progress reports to parents and schools. |

---

## 5. Supported levels, subjects & modes

**Levels:** `BREVET` · `BAC` (by stream) · `CONCOURS`
**Subjects:** `MATHEMATICS` · `PHYSICS` · `FRENCH` · `ENGLISH` · `LIFE & EARTH SCIENCES (SVT)`
**Modes:** `TEXT` · `VOICE` · `EXAM SIMULATION`

---

## 6. Plans & feature flags

| Plan | Price | Feature flags unlocked |
|---|---|---|
| **Discovery** | Free | Limited daily access, text mode only |
| **Monthly** | 250 MRU/month | Full subject access, voice mode, progress tracking |
| **Annual** | 2,400 MRU/year | Same as Monthly, billed yearly |
| **School** | Custom quote | Multi-student accounts, school/class dashboard, aggregated analytics |

Feature flags (voice access, quotas, dashboard visibility) are modeled at the subscription/tenant level, on the same underlying architecture shared with SIDI — no per-student or per-school forked logic.

---

## 7. Data, security & child protection principles

- **No third-party training on student data.** All learning interactions stay within Alborda's own infrastructure.
- **Self-hosted core infrastructure** (Supabase, orchestration) for full control over data residency.
- **PII scrubbing and encryption at rest**, with reinforced minimization given that most users are minors.
- **Parental consent required** at account creation for minor students.
- **No student-to-student messaging** of any kind — SOULEYMAN is an individual learning tool, never a social feature.
- **Strict content moderation** across all explanations, examples, and analogies.
- **Read-only parental dashboard** on progress only — private student-AI exchanges are never exposed, except in case of a flagged concern.

---

## 8. Roadmap highlights

- Written-answer correction (photo or text submission for essay-style questions)
- Personalized pre-exam revision planning based on time available and weak points
- Gamification (badges, streaks) without competitive student rankings
- Offline mode for low-connectivity regions, with progress sync on reconnect
- School dashboard for class-wide performance insights
- Diaspora offering for Mauritanian families abroad

---

## 9. About Alborda AI

Founded in 2024 in Mauritania, Alborda AI is an international AI company democratizing artificial intelligence for underrepresented languages across the Middle East and North Africa (MENA). We develop language models and personalize them for a wide range of tasks, so millions can access advanced AI natively — in their own language, not a borrowed one.

**Products:** Dimeyz (LLM) · SIDI (B2B support agent) · MOUNA (executive assistant) · SOULEYMAN (AI tutor) · Dimeyz Chat (consumer chat)

---

## 10. Contact

📧 [contact@alborda.ai](mailto:contact@alborda.ai)
🌐 [alborda.ai](https://alborda.ai)

---

<div align="center">
<sub>© 2026 Alborda AI — Building AI that speaks your language.</sub>
</div>
