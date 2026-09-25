# 🎓 AI Classroom

**10 in-class AI tasks for students** — build small AI-powered websites and tools with HTML, CSS & JS. A single static project, ready to host on **GitHub Pages**.

Based on the classroom worksheet *"10 In-Class AI Tasks for Students"* (Claude/ChatGPT + HTML/CSS/JS + Google Sheets).

---

## The 10 tasks

| # | Task | Page |
|---|------|------|
| 1 | AI Resume Builder — form → polished resume + PDF export | `pages/task-01-resume-builder.html` |
| 2 | AI Notes Generator — paste text → structured study notes | `pages/task-02-notes-generator.html` |
| 3 | AI Presentation Generator — topic → navigable slide deck | `pages/task-03-presentation-generator.html` |
| 4 | AI Mind Map Generator — syllabus → zoomable SVG mind map, click nodes for explanations | `pages/task-04-mindmap-generator.html` |
| 5 | Google Sheets Backend — live read/write via Apps Script + AI insights | `pages/task-05-sheets-backend.html` |
| 6 | AI Quiz Generator — notes → interactive MCQ quiz with scoring | `pages/task-06-quiz-generator.html` |
| 7 | AI Doubt-Solving Chatbot — mini tutor with conversation history | `pages/task-07-doubt-chatbot.html` |
| 8 | AI Flashcard Generator — chapter → flippable 3D flashcards | `pages/task-08-flashcards.html` |
| 9 | AI Study Planner — subjects + hours + exam date → color-coded timetable | `pages/task-09-study-planner.html` |
| 10 | AI Notes Summarizer (OCR) — photo of notes → extracted text → summary | `pages/task-10-ocr-summarizer.html` |

## Project structure

```
ai-classroom/
├── index.html                  # homepage with all 10 task cards
├── .nojekyll                   # tells GitHub Pages to serve files as-is
├── .gitignore
├── README.md
├── assets/
│   ├── css/style.css            # shared theme (light/dark), components
│   └── js/
│       ├── common.js            # layout, nav, theme, API-key modal, markdown renderer, mind-map SVG renderer
│       ├── local-ai.js          # built-in "demo AI" generators (100% client-side)
│       └── ai.js                # generateAI() dispatcher: live OpenAI API → fallback to demo AI
└── pages/
    ├── task-01-resume-builder.html
    ├── task-02-notes-generator.html
    ├── task-03-presentation-generator.html
    ├── task-04-mindmap-generator.html
    ├── task-05-sheets-backend.html
    ├── task-06-quiz-generator.html
    ├── task-07-doubt-chatbot.html
    ├── task-08-flashcards.html
    ├── task-09-study-planner.html
    └── task-10-ocr-summarizer.html
```

No build step, no dependencies to install, no backend. The only external CDN used is Tesseract.js (Task 10, loaded lazily on demand for in-browser OCR).

## How the AI works

- **Demo AI (default):** every page works immediately with zero setup. `assets/js/local-ai.js` implements real client-side generators — extractive summarization, template-based slide decks, fill-in-the-blank quiz construction from your text, a weighted study-timetable scheduler, an SVG mind-map parser, and a small tutor engine (including arithmetic solving).
- **Live AI (optional):** click **🔑 AI Key** in the header and paste an OpenAI API key. It is stored only in your browser's `localStorage` and sent only to `api.openai.com` — it is never committed to the repo. `assets/js/ai.js` then routes each task to the API (with `response_format: json_object` for structured tasks) and falls back to demo AI automatically if the call fails.

## Run locally

```bash
git clone <your-repo-url>
cd ai-classroom
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy to GitHub Pages

1. Create a repo on GitHub and push this folder:
   ```bash
   git init
   git add .
   git commit -m "AI Classroom: 10 in-class AI tasks"
   git branch -M main
   git remote add origin https://github.com/<user>/<repo>.git
   git push -u origin main
   ```
2. In the repo: **Settings → Pages → Deploy from a branch → `main` / `(root)` → Save.**
3. Your site goes live at `https://<user>.github.io/<repo>/` in about a minute.

## Notes

- Task 5 works in **demo mode** out of the box (sample data in `localStorage`). Connect your own Google Apps Script Web App URL on the page to go live — setup steps and copy-paste script are built into the page.
- Task 10 downloads the Tesseract.js OCR engine from a CDN on first use (~a few MB); everything else is dependency-free.
- Dark/light theme toggle is in the header and persists per browser.
