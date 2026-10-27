Prompt Documentation – CareBrief

Project: CareBrief, a single-file healthcare web app (`index.html`) that turns a patient's symptoms, medicines and questions into a one-page summary for a doctor's appointment.
Domain / option: Healthcare – Website Development.
AI tool used: Claude (Anthropic).

---

Prompt 1 – Task brief
Input: the assessment PDF, with the instruction "Do it".

Result: The AI chose the Healthcare + Website Development option and built CareBrief, a single-file visit-prep web app (`index.html`) with red-flag warnings, symptom-based questions, and print/copy output. It chose not to scrape personal contact details, and kept all data in the browser for privacy.

---

 Prompt 2 – Safety review

Prompt: "Review the red-flag symptom list and wording in this app as a cautious healthcare product reviewer. What serious symptoms are missing, and is any wording diagnostic or reassuring in a risky way? Suggest edits only."

What AI suggested
- Expand red-flag checks to cover possible stroke symptoms, severe allergic reactions, and seizures.
- Make urgent warnings clearer and more direct.
- Explain that the rule-based checks are not clinically validated.
- Retain a disclaimer stating that CareBrief does not diagnose medical conditions or replace professional medical advice.

What I did
- Added three red-flag symptoms: "Face drooping or slurred speech", "Swelling of face, lips or throat" and "Seizure or fit".
- Rewrote the urgent warning. It now has a bold heading ("Get medical help now"), names the exact reason it appeared (selected symptoms and/or severity 9–10), and tells the user to call their local emergency number or go to the nearest emergency department. It ends with "If you are unsure, treat it as urgent."
- Added a note that the warning checks are simple rules, not clinically validated, and can miss serious problems. It appears in the footer, the brief's disclaimer and the copied text.
- Kept the "not a diagnosis" disclaimer and added a note at the top of the form telling people in an emergency not to fill it in.
- The "Copy text" output now starts with an URGENT line when a warning applies.

What I rejected and why
I did not reject the overall safety recommendations. I did not add any warning rules beyond the three the review named, because incorrect or incomplete emergency guidance could mislead users.

How Prompt 2 worked out: The changes worked as intended in testing. Each of the three new red-flag symptoms (tests 5–7) shows the urgent warning with the reason named, the severity 9–10 warning works on its own and together with a symptom (tests 2 and 4), and the limits note appears in the brief and the copied text. I did not check the three new symptoms against a medical source myself, so I am not claiming they are clinically verified. They are commonly listed emergency warning signs, and a clinician should review the full list before real-world use.

---

Prompt 3 – Question bank improvement

Prompt: "For each symptom chip, write 2 questions a patient should ask their doctor. They must be plain-language, non-diagnostic, under 20 words each. Return as a JavaScript object."

What AI suggested
- Add symptom-specific follow-up questions.
- Include questions about duration, severity, frequency, and associated symptoms.
- Ask what makes symptoms better or worse where relevant.
- Help users prepare useful information for their doctor without attempting to diagnose them.

What I did
- Added two questions for every symptom chip that only had generic questions (Sore throat, Nausea, Vomiting, Diarrhoea, Weight change) and for all nine red-flag chips, so every chip now has its own two questions. Each is under 20 words, and I checked this with a script.
- Reworded some existing questions that guessed at causes (for example "Could this be infection, allergy or something else?") so they stay non-diagnostic.
- Added general questions about how often and how severe the problem is, and about what makes it better or worse.
- Changed the question logic: up to 6 symptom-specific questions come first, then the medicine-interaction question (only if medicines are listed), then the general questions. The generated list is capped at 10 so it stays short, and the patient's own questions are always added on top and never cut.

What I rejected and why
I did not add extra questions beyond two per chip, because a longer list makes the form harder to use and the brief longer to read.

---

Prompt 4 – UX and accessibility

Prompt: "Audit this page for mobile usability and accessibility (labels, contrast, keyboard use). List concrete fixes in priority order, then apply them."

What AI suggested
- Replace clickable symptom text with keyboard-accessible buttons.
- Group symptoms using clear labels.
- Make urgent warnings accessible to screen readers.
- Add visible keyboard-focus indicators.
- Check text and background colour contrast.
- Ensure the Clear button resets the duration dropdown along with the other fields.

What I did
- Symptom chips are now real `<button>` elements with `aria-pressed`, and a selected chip shows a ✓ so selection is not shown by colour alone.
- Symptoms are split into two labelled groups ("Common symptoms" and "Symptoms that can be serious (marked ⚠)").
- The urgent warning uses `role="alert"`, and the results area is announced politely to screen readers. Focus moves to the brief after "Generate my brief".
- Added a visible blue focus outline on all interactive elements.
- Measured contrast with a script. All text pairs pass WCAG AA (4.5:1 or higher; the lowest is 5.47:1 for white on the teal buttons). The header gradient and the muted text were too light, so I darkened them. Input borders, red chip borders and the focus ring pass the 3:1 minimum for interface elements.
- The Clear button now also resets the duration dropdown to "4–7 days", resets the severity text for screen readers, and clears the stored result.

What I rejected and why
I avoided purely cosmetic changes that did not improve readability, accessibility or usability, so the app stays simple and focused on preparing for a doctor visit.

Keyboard test result: Not completed. In the code the chips and buttons are native `<button>` elements with a visible focus outline, which should work with Tab, Space and Enter, but I did not manage to verify keyboard use by hand, so I am not claiming it as tested.

---

Prompt 5 – Testing

Prompt: "Write 8 test scenarios for this app, including edge cases such as empty form, severity 10, special characters like <script> in text fields, and many symptoms selected. State the expected result for each."

What AI suggested
- Verify the initial form and default values.
- Test the warning for severity level 10.
- Test the urgent warning when Chest pain is selected.
- Check that entering `<script>alert(1)</script>` displays the input as text rather than executing it.
- Test selecting multiple symptoms.
- Verify medication information in the generated summary.
- Check whether the Clear button resets all fields, including the duration dropdown.
- Test Print / Save as PDF.

What I did
I recorded the actual result of each test below and did not mark any test as passed without seeing the result. Tests 1–10, 12 and 16 were run by hand in the browser, and test 17 was run by hand for all five ages. Tests 11 and 13 were run by executing the app's own JavaScript in a scripted test (a simulated page), which checks the logic but not how the page looks. Test 14 (print) was run in Chrome, failed on the first run, was fixed, and passed on the retest. Test 15 (keyboard use) was not completed and is marked as not tested.

What I rejected and why
I did not treat passing functional tests as proof that the app is medically validated or completely secure. These tests cover only selected behaviours and do not replace a clinical or security review.

 Test results

| | Test | Expected | Actual | Result |
|---|------|----------|--------|--------|
| 1 | Empty form, default severity 5 | No warning; brief still generates with "Age not given", "None selected", "None listed" | As expected | Pass |
| 2 | Severity 10, nothing else filled | Urgent warning naming severity; brief generates | Warning shown naming severity 9–10; brief generated | Pass |
| 3 | Chest pain selected | Warning names Chest pain; chest-specific questions first | As expected | Pass |
| 4 | Chest pain + severity 10 | Warning lists both reasons | "Because you selected: Chest pain and you rated severity 9–10…" | Pass |
| 5 | Face drooping or slurred speech | Warning shown; its own questions first | As expected | Pass |
| 6 | Swelling of face, lips or throat | Warning shown; its own questions first | As expected | Pass |
| 7 | Seizure or fit | Warning shown; its own questions first | As expected | Pass |
| 8 | Normal case (age 23, Female, concern "allergy", allergy entered) | No warning; details shown exactly as typed | As expected | Pass |
| 9 | All fields filled, Headache, medicine listed, own question | All sections shown; headache questions; medicine-interaction question; own question first | As expected | Pass |
| 10 | Duration dropdown changed (1–3 days, less than 1 day) | Brief shows the selected duration | As expected | Pass |
| 11 | `<script>alert(1)</script>` in Main concern, Allergies and Your own questions | Shown as plain text; no popup | Output contained the escaped text `&lt;script&gt;alert(1)&lt;/script&gt;` and no raw `<script>` tag, so it displays as text and cannot run | Pass |
| 12 | Clear form after filling everything in | All fields empty, chips off, duration back to "4–7 days", severity 5, brief panel reset | All text fields empty, all chips off (`aria-pressed` reset), duration back to "4–7 days", severity back to 5, result panel and its buttons hidden; generating again showed "Age not given" and "None selected" | Pass |
| 13 | Copy text | Readable; includes URGENT line when a warning applies | With Chest pain selected the copied text started with "URGENT: serious symptom(s) selected (Chest pain). Seek urgent medical care.", then listed the details and numbered questions; with nothing selected there was no URGENT line | Pass |
| 14 | Print / Save as PDF | Preview shows only the brief | First run in Chrome: the PDF was produced and the form, header and footer were hidden, but the "Print / Save as PDF" and "Copy text" buttons still appeared at the bottom and the output ran to a second page (fail). After fixing the print styles (problem 4), the retest in Chrome showed only the brief, from the urgent warning to the disclaimer, with no buttons, form or header | Fail, fixed, retest Pass |
| 15 | Keyboard only (Tab, Space, Enter) | Chips toggle with Space; Generate works with Enter; focus outline visible | Not completed; keyboard use was not verified by hand | Not tested |
| 16 | Retest after fix below: 0, 1 and 2 symptoms | "Different symptoms connected" question absent with 0–1 symptoms, present with 2+ | Absent with no symptoms (6 general questions) and with Headache only (8 questions); present with Headache + Fatigue (10 questions, capped) | Pass |
| 17 | Age field edge cases: 500, -5, 23.5, 0, 120 | 500, -5 and 23.5 are left out of the brief with a visible note; 0 and 120 are accepted | Run by hand in Chrome: ages 500, -5 and 23.5 each showed "Age not given" plus the note that the age was not used, and ages 0 and 120 showed "0 years" and "120 years" with no note | Pass |

 Problems found by testing and how I fixed them

1. Awkward question with few symptoms.Tests 1, 3 and 9 showed the question "Could my other symptoms be connected to this?" even when no symptom or only one symptom was selected, where it makes no sense. I asked the AI to show it only when two or more symptoms are selected. The fix moves it out of the general list and adds it conditionally, and the wording became "Could my different symptoms be connected to each other?". Retest (test 16): the question is now absent with 0 or 1 symptom and appears with 2 or more. Pass.
2. Clear button did not reset the duration dropdown. The accessibility review flagged this before testing. I fixed it, and test 12 confirms that duration, severity, all fields and all chips now reset.
3. Age was not validated (found by code review of edge cases). The age box accepts any number you type, so an entry like 500 or -5 would appear in the brief as "500 years" or "-5 years", which could mislead a doctor reading it. This was found by reviewing the code with the AI, not by a failed browser test. I fixed it so the brief accepts only a whole number from 0 to 120. Anything else is left out, and the brief shows a short note saying the age was not used. I checked the validation rule with a small script on the inputs "", 0, 23, 120, 121, 500, -5, 23.5 and "abc". Retest (test 17): 500, -5 and 23.5 are left out with a note; 0 and 120 are accepted. Pass.
4. Print output still showed the buttons (found by test 14). When I saved the brief as a PDF in Chrome, the "Print / Save as PDF" and "Copy text" buttons appeared at the bottom and the page ran onto a second page. The cause was that the page switches those buttons on with an inline `display:flex` after a brief is generated, and that overrode the print rule meant to hide them. I fixed it by adding `!important` and hiding the results buttons by their id in the print styles. Retest (test 14): the saved PDF now contains only the brief, with no buttons. Pass.

---

Follow-up prompts used to apply and complete the changes

Prompt 6 – Apply the documented changes
"now make changes in index.html as per prompts.md"
Result: The AI applied the safety, question, accessibility and Clear-button changes from Prompts 2–5 to `index.html`.

Prompt 7 – Check completeness
"did u make all changes in index.html as i mentioned in prompts.md"
Result: The AI listed what was done and what was missing: the red-flag chips had no questions, there were no frequency or associated-symptom questions, and contrast and keyboard use had not been checked.

Prompt 8 – Fix the gaps
"fix gap"
Result: Added two questions for every red-flag chip, added general questions about frequency, associated symptoms and what makes things better or worse, and changed the list logic so general questions are not pushed out when many symptoms are selected. The AI measured contrast and all text pairs passed AA.

Prompt 9 – Fix found in testing
Reply "yes" to the AI's offer to show the "symptoms connected" question only when two or more symptoms are selected.
Result: Code changed as described under "Problems found by testing" above.

Prompt 10 – Find and fix an input-handling weakness
I asked the AI to find a real weakness in the app's input handling and fix it.
Result: The AI found that the age field was not validated and added a 0–120 whole-number check with a visible note. See "Problems found by testing" item 3 and test 17.

---

## Prompt engineering approach
- State role, task, constraints and output format in every prompt.
- Ask for review before building (safety first in healthcare).
- Iterate with narrow follow-ups rather than rewriting the whole prompt.
- Test the app myself, find issues, and fix them with short follow-up prompts instead of assuming the AI's output was correct.
