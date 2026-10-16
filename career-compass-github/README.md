# Career Compass

**AI career guidance and skill recommendation system for college students.**

Career Compass is a single-page web app. A student fills in a 6-step profile and gets:

- their top 5 matches among 13 technology careers
- a prioritised skill gap
- a learning roadmap sized to their study hours
- project ideas
- a job readiness score

Every score is rule-based and explained factor by factor.

## Features

- **6-step assessment:** About you, Education, Technical skills (27 skills rated 0–4), Interests, Goals, and Projects & experience.
- **Skill check quiz:** 3 questions per skill (81 in total). A skill counts at most one level above the number of correct answers.
- **Interest test:** 18 items based on Holland's six interest types (RIASEC), combined with the student's ranked interests.
- **Transparent scoring:** each career's score opens into a table of factor, score, weight and points.
- **Dashboard report:** cards for best match, job readiness, verified skills and interest code, plus tabs for Overview, Skills, Learning plan and Readiness.
- **Institutional design:** light and dark mode, works on phones, keyboard accessible.

## Scoring

```
Career score = 0.25 × Technical skills + 0.20 × Interests + 0.15 × Academics
             + 0.15 × Projects & experience + 0.10 × Market relevance
             + 0.10 × Growth potential + 0.05 × Career preference

Job readiness = 30% skills + 20% projects + 15% internship + 10% resume
              + 10% communication + 10% coding practice + 5% certifications
```

Market relevance and growth potential are fixed estimates per career, not live job-market data.

## Careers covered

Software Developer · Full-Stack Developer · Data Analyst · Data Scientist · Machine Learning Engineer · Data Engineer · Cloud Engineer · DevOps Engineer · Cybersecurity Analyst · UI/UX Designer · Product Analyst · Mobile App Developer · Game Developer

## Run it

No installation, server or build step is needed.

- **Locally:** download `index.html` and open it in any modern browser.
- **Online:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main` / root). The site will be at `https://<username>.github.io/<repo-name>/`.

The student's draft profile is stored only in their own browser (localStorage).

## Features that need the Claude-hosted version

The original version runs as a Claude artifact, which adds three features:

- an optional AI-written explanation of the results
- anonymous feedback submission
- an Evaluation view for counsellors (Precision@3, nDCG@3, CSV export)

These features need Claude's runtime. On GitHub Pages or a local copy they are hidden automatically, and everything else works.

## Tech stack

HTML, CSS and plain JavaScript in one file, with no framework or dependencies. Fonts come from Google Fonts: Source Serif 4, Source Sans 3 and IBM Plex Mono.

## Limitations

- The weights are fixed from the project brief and are not learned from data.
- The skill quiz and interest test were written for this project and are not validated instruments.
- No accuracy results have been collected yet.
- Recommendations are guidance, not a guarantee of a job or salary.

## Project prompt

[`PROMPT.md`](PROMPT.md) contains the full specification used to build this project: the web app, research comparison report, poster, speaking script and presentation.
