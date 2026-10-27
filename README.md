CareBrief – Doctor Visit Prep (Healthcare web app)

A single-file web app that turns a patient's symptoms, medicines and questions into a clear one-page summary to bring to a doctor's appointment.

- Live app: https://sadiyatabassum1.github.io/carebrief/
- Repository: https://github.com/Sadiyatabassum1/carebrief

Why this project
Short GP appointments often go badly because patients forget details (how long, how severe, which medicines) and forget to ask their questions. CareBrief organises that information beforehand.

Features
- Guided form: age, sex, main concern, symptom buttons, duration, severity (1–10), triggers, medicines, allergies, history and the patient's own questions
- Red-flag check: serious symptoms (chest pain, shortness of breath, fainting, sudden weakness or numbness, confusion, vomiting blood, face drooping or slurred speech, swelling of face, lips or throat, seizure or fit) or severity 9–10 show a clear urgent-care warning that names the reason
- Suggested questions: two plain-language, non-diagnostic questions for every symptom, plus general questions about frequency, severity and what makes things better or worse, and the patient's own questions
- Adds a medicine-interaction question automatically when medicines are listed
- Age check: only whole numbers from 0 to 120 are accepted, otherwise the age is left out with a visible note
- Accessibility: symptom buttons work as real buttons with labelled groups, urgent warnings are announced to screen readers, visible focus outlines, checked text contrast
- Print / Save as PDF (prints only the brief) and Copy as text
- Privacy by design: runs fully in the browser, no server, nothing stored or sent

 Run it
Open `index.html` in a normal browser tab (Chrome, Edge or Firefox). No install or build step. Some preview windows block printing, so use a normal tab.

 Host it
GitHub Pages: upload `index.html` to a repository, then Settings → Pages → Deploy from branch `main` / root.

Limits (deliberate)
- It does not diagnose or recommend treatment.
- The red-flag rules and question bank are simple, hand-written lists. They have not been clinically validated or reviewed by a clinician and can miss serious problems. It is not a medical device.
- The keyboard-only test was not completed (see `PROMPTS.md`).

How AI was used
Claude was used to design the feature set, write the code, review the safety wording, improve accessibility and plan tests. I ran the tests, found problems (print output showing buttons, unchecked age values, a question that showed with too few symptoms) and fixed them with follow-up prompts. All prompts, results and test outcomes are in `PROMPTS.md`.

Possible next steps
Clinician review of the red-flag list, AI-generated questions from free-text symptoms, multilingual output (Telugu, Hindi), saved visit history.
