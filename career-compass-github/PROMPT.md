# Career Compass: Master Prompt

Copy everything below the line into an AI assistant to rebuild the full project.

---

You are a senior full-stack developer, UX designer and academic writing assistant. Build a complete student project called **Career Compass: an AI-assisted Career Guidance and Skill Recommendation System** for college students choosing a technology career. Produce every deliverable listed in Part B. Follow every rule in Part C. Ask me before assuming anything that changes the output (names, college, format, length). Never invent experience, results, statistics, certifications or accuracy figures.

## PART A: THE WEB APPLICATION

### A1. Purpose and principles
- A single self-contained HTML file (HTML, CSS, plain JavaScript; no framework, no server, no build step) that runs in the browser.
- The ranking must be rule-based and fully explainable. AI (an LLM) is optional and may only explain results, never change scores.
- Every score must be traceable: show each factor's score, weight and points.
- Nothing is stored or sent without the student's consent. Draft profile is kept in browser localStorage (wrap every read/write in try/catch).

### A2. Look and feel (institutional / college portal)
- Dark green header band (brand #0B3B30) with logo, the name "Career Compass", the subtitle "Career guidance & skill recommendation", and navigation: Home, Assessment, My report, Evaluation (Evaluation visible only to owner/editors).
- Colours: page #F3F5F4, white cards, ink #14211C, muted #56635D, accent #0E6B57, accent-soft #DCEDE6, warning #9A5512, critical #A8322F, success #2A7039. Full dark-mode palette via CSS variables (prefers-color-scheme plus data-theme overrides).
- Fonts: Source Serif 4 (headings), Source Sans 3 (body), IBM Plex Mono (labels and numbers), all from Google Fonts with fallbacks.
- Logo: an original inline-SVG compass. A rounded green square, a white ring, four tick marks at N/E/S/W, a needle tilted 40° (solid north half, outlined south half) and a small centre dot. Use colour variables so it works in dark mode.
- Fully responsive (works at 390 px phone width, no horizontal scroll), visible keyboard focus, accessible labels, no emoji, footer stating "Recommendations are guidance, not guarantees of a job or salary" and "Market and growth scores are fixed estimates, not live data".

### A3. Views
1. **Home (landing):** headline "Find the tech career that fits you, and the plan to get there"; short description; buttons "Start the assessment" (clears the example profile) and "View a sample report" (loads the example student); facts line "About 10 minutes · 6 steps · Nothing is saved without your consent"; a "Your report includes" card (top 5 matches, prioritised skill gap, roadmap and projects, job readiness score, each with a small stroke icon); "How it works" (4 steps); "Why you can trust the result" (every score explained, skills verified, accuracy measured).
2. **Assessment wizard (6 steps):** side step list with tick marks for completed steps, progress bar "Step X of 6", Back/Next buttons (last button reads "See my report"), "Load example" and "Clear all" buttons.
   - Step 1 About you: name, country, current location, preferred work location, work mode (Remote / Hybrid / On-site / No preference).
   - Step 2 Education: degree, major area (Computer Science/IT, Electronics/Electrical, Mathematics/Statistics, Other engineering, Commerce/Business, Science, Design/Fine arts, Arts/Humanities/Other), year, CGPA, college, academic strengths, weaknesses.
   - Step 3 Technical skills: 27 skills rated 0–4 (None, Beginner, Intermediate, Advanced, Expert) in 5 groups:
     - Programming: Python, Java, C/C++, JavaScript/TypeScript, Data structures & algorithms
     - Web: HTML & CSS, React/Angular, Backend (Node.js, Django, Flask)
     - Data & AI: SQL, MongoDB/NoSQL, Excel, Pandas & NumPy, Power BI/Tableau, Statistics, Machine learning, Deep learning
     - Cloud, DevOps & security: Cloud (AWS/Azure/GCP), Linux & shell, Docker, Kubernetes, Git & GitHub, Networking, Security fundamentals
     - Design, product, mobile & games: UI/UX (Figma), Product & business analysis, Mobile (Kotlin/Swift/Flutter), Game engines (Unity/Unreal)
     - Include a "Check my skills" button that opens the skill quiz (A5).
   - Step 4 Interests: pick and rank up to 5 of 16 areas (Software Development, Full-Stack, Data Analytics, Data Science, AI, ML, Cybersecurity, Cloud, DevOps, UI/UX, Mobile, Game Development, Business/Management, Product Management, Research, Entrepreneurship), plus the RIASEC interest test (A6).
   - Step 5 Goals: target role (or "Not decided"), study hours per week, short-term and long-term goal.
   - Step 6 Projects & experience: list of projects each tagged with an area (Software, Web, Mobile, Data, ML/AI, Cloud/DevOps, Security, UI/UX, Games, Other); internship (None, 1–2, 3–5, 6+ months); coding problems solved (0, 1–50, 51–150, 151–300, 300+); certifications (0, 1, 2+); resume status (none, draft, reviewed/ATS-checked); communication confidence 1–5.
3. **Report dashboard:** banner when viewing the sample; title "<Name>'s career report"; one-paragraph profile summary; "Edit profile" button; 4 KPI cards (Best match %, Job readiness /100, Skills verified X/Y, Holland interest code); tabs:
   - Overview: best-match card (score, reason sentence, difficulty, typical prep time, plan length at the student's hours, role's Holland code, growth path, expandable factor-by-factor score table); top 5 career list (expandable, each with "You have / Missing" skills and its own score table); "Your next 3 steps" (skill to learn, project to build, career action); optional AI write-up.
   - Skills: skill-gap table (skill, counted level with dots, "(you said …)" when capped by the quiz, required level, gap, priority pill Critical/High/Medium/Met); priority skills list (top 5).
   - Learning plan: 5-phase roadmap (Foundation, Core skills, Advanced skills, Projects, Job preparation) whose week ranges scale with study hours (base 10 h/week, factor clamp(10/h, 0.6, 2.5)); certifications only where they add value; 3 projects Beginner → Intermediate → Advanced with "start here" highlighted.
   - Readiness: gauge 0–100, area table with bars, strong areas, areas to improve, immediate actions.
   - Feedback: anonymous submission (A8).
4. **Evaluation (owner/editors only):** see A8.

### A4. Scoring engine
Career score = 0.15 × Academic + 0.25 × Technical skill + 0.20 × Interest + 0.15 × Project/experience + 0.10 × Job market + 0.10 × Growth + 0.05 × Preference (each factor 0–100).
- **Academic:** fixed fit value per career for the student's major (e.g. Mathematics → Data Analyst 95); 50 if no major is given.
- **Technical skill:** for each required skill, min(counted level, required) ÷ required; core skills weigh 2, supporting skills 1. "Main language" = best of Python/Java/C++.
- **Interest:** pick score = 100/85/70/60/60 by the rank of a matching interest (−10 if it isn't the career's primary interest), 25 if no match. If the RIASEC test is complete: RIASEC fit = 0.5·first + 0.3·second + 0.2·third letter of the career's Holland code; interest = average of pick score and RIASEC fit (RIASEC alone if no picks).
- **Project/experience:** 0/1/2/3+ relevant projects → 10/55/75/90; +5 per other project (max +10); +10 for any internship; cap 100.
- **Market and Growth:** fixed estimates per career (label them as estimates).
- **Preference:** 100 if it is the target role, 60 if undecided, 40 otherwise.
- **Job readiness (for the best career):** technical 30%, projects 20% (0/55/75/90), internship 15% (0/50/75/100), resume 10% (0/45/85), communication 10% ((rating−1)/4), coding practice 10% (0/30/55/75/90), certifications 5% (0/70/100).
- **Gap priority:** Critical = core skill with a gap ≥ 2; High = core skill, or any gap ≥ 2; Medium = other gaps; Met = no gap.

### A5. Skill check quiz
- 3 multiple-choice questions per skill (beginner, intermediate, advanced), 81 in total, options shuffled in a fixed order per question.
- Counted level = min(self-rating, correct answers + 1).
- After answering, show right/wrong options, the score, and whether the rating was capped.
- Open the quiz as an accessible modal (Escape closes it, focus returns to the button that opened it).

### A6. Interest test (Holland RIASEC)
- 18 activity statements, 3 per type (Realistic, Investigative, Artistic, Social, Enterprising, Conventional), each rated 1–5.
- Type score = (mean − 1)/4 × 100; show all six scores and the top-3 code.
- State that the items were written for this project and are not a validated instrument.

### A7. Career data (13 careers)
For each career store: Holland code, related interests, project areas, academic fit per major, market and growth estimates, difficulty, typical preparation time, a 5-stage growth path, required skills with level and core flag, 3 advanced topics, 3 original real-world projects (problem, features, tech, time) and recommended certifications (or a note saying none are needed).

| Career | Holland | Core required skills (level) |
|---|---|---|
| Software Developer | IRC | main language 3, DSA 3, Git 2 |
| Full-Stack Developer | IAC | JavaScript 3, HTML/CSS 3, React 2, Backend 2, Git 2 |
| Data Analyst | CIE | SQL 3, Power BI 3, Statistics 2 |
| Data Scientist | ICR | Python 3, Pandas 3, Statistics 3, ML 3 |
| Machine Learning Engineer | IRC | Python 3, ML 3, Deep learning 2 |
| Data Engineer | CIR | SQL 3, Python 3, Cloud 2 |
| Cloud Engineer | RIC | Cloud 3, Linux 2, Networking 2 |
| DevOps Engineer | RCI | Linux 3, Git 3, Docker 3, Kubernetes 2, Cloud 2 |
| Cybersecurity Analyst | ICR | Networking 3, Security 3, Linux 2 |
| UI/UX Designer | AIS | UI/UX 3 |
| Product Analyst | EIC | SQL 3, Product 2, Statistics 2, Excel 2 |
| Mobile App Developer | IAR | Mobile 3, main language 2, Git 2 |
| Game Developer | AIR | Game engine 3, DSA 2 |

- Add sensible supporting skills for each career.
- Certification examples: PL-300 and Google Data Analytics (Data Analyst); AWS Cloud Practitioner and AZ-900 (Cloud); CKA and Terraform Associate (DevOps); Security+ and ISC2 CC (Cyber); Databricks DE Associate and DP-700 (Data Engineer); AWS ML Engineer Associate and Google PMLE (MLE); Meta Front-End (Full-Stack); Google UX (UI/UX); Unity Certified User (Games).
- Tell students to check providers for current details.

### A8. Validation and data collection
- **Student feedback (Feedback tab):** sliders for relevance, clarity and usefulness (1–10); "Which career do you plan to pursue?"; consent checkbox; "What gets shared" disclosure.
  - Shared: major, skill ratings, quiz scores, interests, RIASEC scores, target, hours, project counts per area, experience fields, computed scores, top 3, readiness, feedback and chosen career.
  - Never shared: name, location, college, CGPA, project names or free text.
  - Buttons: "Submit response" (saved to a shared data store, one per student) and "Download response file" (JSON) as a fallback.
- **Evaluation view (owner/editors):**
  - KPI cards: responses, Precision@3 (rating ≥ 3), Precision@3 (rating ≥ 4), nDCG@3 (gain = 2^(rating−1) − 1), share of chosen careers in the top 3 and ranked first, and mean student ratings. Show a note when there are fewer than 30 responses.
  - Counsellor rating queue: show the anonymised profile, rate each of the top 3 careers 1–5, save.
  - CSV export (one row per student with every factor score per career, quiz, RIASEC, feedback and mean counsellor rating) for later weight tuning; import of response files.
  - Access rules: students write only their own submission; only owner/editors read submissions and write ratings.

### A9. Optional AI write-up
A "Write with Claude" button sends the profile and the already-computed results to an LLM. It asks for JSON only (summary, why the best career fits with one honest risk, a tailored project, 3 resume tips in Action + Technology + Problem + Result form using "[your result]" where a number is unknown, and one "watch out"). The LLM must not change scores, invent experience, or guarantee jobs or salary. Show a Stop button; handle refusal, rate-limit and unavailable states gracefully, and hide the feature when no AI is available.

### A10. Example profile
"Priya": 3rd-year B.Tech CS, CGPA 8.1, Python 2, SQL 2, Excel 2 and several skills at 1, interests Data Analytics / Data Science / Business, 2 projects (data, software), no internship, draft resume. Always label it as a sample.

## PART B: OTHER DELIVERABLES

1. **Project report comparing with research:**
   - Sections: Abstract, System design (inputs table, formula, factor table, outputs, AI, tech), Related research, a comparison table, Strengths and limitations, Improvements and future work (table: improvement, source paper, what it fixes, effort), Conclusion, References.
   - Compare against these 7 sources, and read each source before citing it:
     1. Gunwant, Pande & Bisht (2022), systematic review of 25 career-guidance expert systems, Journal of Learning for Development 9(3)
     2. Zhang (2024), UCLA thesis, ML classifiers on 2,000 students, Random Forest best
     3. Imankulova (2024), SDU thesis, ML vs Q-learning/DQN
     4. Seveso et al. (2021), Skills2Job, AAAI-21: 2.5M job ads, ESCO; P@3 0.823, nDCG 0.985 with 10 experts
     5. de Groot, Schutte & Graus (2021), job-posting-enriched skills knowledge graph, arXiv:2109.02554
     6. Luo, O'Connell & Mithun (2024), LLM mentoring with GPT-4, LLaMA 3 and PaLM 2, arXiv:2412.08430
     7. Tolegen (2025), RAG career guidance pilot, scores 8.06 → 8.77, NHSJS
   - State honestly that Career Compass has no accuracy results yet.
2. **Expo poster (16:9, 1920×1080, no names):**
   - Title and tagline; the formula panel; "The problem"; "How it works" (4 numbered steps); factor-weight bars; "What a student gets"; a "Compared with research" mini-table; a "Built-in evaluation" panel.
   - Bottom stats strip: 13 careers, 27 skills, 81 quiz questions, 18 interest items, 7 weighted factors, 7 papers compared.
   - No invented results.
3. **5-minute speaking script for mixed / non-technical staff (about 650 words):**
   - Timed sections: Opening & problem 0:00–0:45, What it does 0:45–1:45, How the score works 1:45–2:45, Trustworthiness 2:45–3:45, Research & closing 3:45–5:00.
   - Italic cues for pointing at the poster, delivery tips, and a table of 7 likely questions with short honest answers.
4. **Key points list:** 7 points plus a one-sentence summary ("Career Compass gives students a career match they can understand and a plan they can start today, and it's built so we can measure how accurate it is").
5. **PowerPoint (.pptx), 13 slides, 16:9:**
   - Theme: Cambria headings, Calibri body, green palette. Real screenshots of the web page using a labelled sample student. Speaker notes on every slide.
   - Slides:
     1. Title + screenshot
     2. Problem (3 cards + goal band)
     3. Objectives & scope (5 objectives, 13 career chips)
     4. How it works (4-step flow)
     5. Web page screenshot with 3 callouts
     6. Architecture & tech stack diagram (browser core: form → engine → report, local storage; optional Claude, response store, file export)
     7. Factor weights (native bar chart) + formula
     8. Skill check and interest test with screenshots
     9. Skill gap and readiness screenshots + outputs list
     10. Research comparison table
     11. Evaluation screenshot + next step
     12. Limitations & future work
     13. References
   - Left-aligned one-line titles; no text overflow; validate the file and visually check every slide.
6. **Logo:** the SVG compass described in A2, used in the web page header (and offered for the poster and PPT).

## PART C: RULES

- Ask before assuming names, college details, formats or lengths; if I don't answer, leave names off and say so.
- Never fabricate data, results, accuracy numbers, testimonials or citations. Mark estimates as estimates, and the quiz and RIASEC items as not validated.
- No job or salary guarantees anywhere.
- Plain, student-friendly language; personalised output; always end the report with the next 3 steps.
- Test the web app (no console errors, all views and tabs work, phone width has no horizontal scroll) before handing it over.
- Deliver: the HTML file, the report document, the poster, the script, the .pptx and a short summary of what was built and what still needs real data.
