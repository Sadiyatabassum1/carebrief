# Video Script (about 3 minutes) – say it in your own words

Record your screen with your voice (face optional). Open the live app in a normal Chrome tab: https://sadiyatabassum1.github.io/carebrief/

0:00 – Introduction (20s)
Hello, my name is Sadiya Tabassum. This is my submission for the AI Growth and Automation Associate assessment. I built CareBrief, a healthcare web app that helps patients prepare for a doctor's visit by turning their symptoms, medicines and questions into a clear one-page summary.

0:20 – Why this project and my approach (30s)
Doctor appointments are short, and people forget how long they've had symptoms, which medicines they take and what they wanted to ask. I chose the website option in healthcare. My background in Python, JavaScript and data work made me choose a simple, reliable design where everything runs in the browser, so no personal data is sent or stored anywhere.

0:50 – AI tools (20s)
I used Claude to plan the features, write the code, review the safety wording and help me plan tests. I chose it because I could build and review in one conversation and ask it to explain its changes. I directed the work, ran the tests in the browser and fixed what failed. *(Mention any other tool only if you really used it.)*

1:10 – Prompt engineering (30s)
Each prompt had a role, a task, constraints and an output format. Because this is healthcare, I asked for a safety review before adding more features. After that I used short, focused follow-up prompts: one for the question bank, one for accessibility and one for testing. For example, I asked for two plain-language, non-diagnostic questions per symptom, each under 20 words. All my prompts and what I did with the results are in my prompt document.

1:40 – Challenges and how I solved them (40s)
My main challenge was keeping the app useful without giving medical advice. I used red-flag warnings, no diagnosis anywhere, and a clear note that the warning rules are simple and not clinically validated.
Testing found real problems. When I saved the brief as a PDF, the buttons showed in the printout, because the page overrode my print style. I fixed it and tested again. The age box accepted values like 500, so I limited it to 0 to 120. And a question about connected symptoms appeared even with only one symptom, so it now appears only with two or more.

2:20 – Demo (40s)
1. Type "headaches" as the main concern, select Headache and Fatigue, set the severity and add a medicine.
2. Click Generate my brief. Point out the symptom questions and the medicine-interaction question.
3. Select Chest pain and generate again to show the red urgent warning.
4. Click Print / Save as PDF to show the clean summary.

3:00 –  next steps (15s)
The red-flag list has not been reviewed by a clinician, and I did not complete a keyboard-only test, so I'm not claiming either. Next steps are clinician review, AI-generated questions from free-text symptoms, and Telugu and Hindi support. Thank you for watching.
