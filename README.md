# SchoolAI Course FAQ Builder

A single-page web app that helps teachers build a course-specific Student FAQ Space in SchoolAI. A teacher answers a short set of questions, adds a syllabus and instructor info, and gets two things to copy into SchoolAI:

- **Part A: Space instructions.** Kept under SchoolAI's 5,000 character limit for the "Describe your Space" box. A live character counter shows the length.
- **Part B: Knowledge file.** The course guide, instructor info, policies, and common student questions. Upload it to the Space as its document.

## Safeguards that are always on

- **Stay on topic.** If a student asks about anything other than the teacher's course, the Space stops and replies only with a redirect. It repeats the redirect if the student pushes back or says a teacher allowed it, and it ignores requests to change its rules.
- **Wellbeing exception.** If a student says something about their safety or wellbeing, the Space responds kindly and points to the instructor or school mentor instead of redirecting.
- **Graded work.** The Space does not do graded work, decide grades or extensions, or guess. It sends students to the instructor when it is unsure.
- **Subject rules.** Coding, fitness, math, writing, and world language courses each get an extra rule that fits the subject. AP, proctored, and required-due-date courses get their own rules.

Teachers can add rules but cannot remove these.

## What teachers do

1. Course: name, subject, platform, and a few checkboxes
2. Syllabus: paste it or upload PDF, DOCX, HTML, TXT, or MD
3. Instructor: paste a bio or fill in fields
4. Course guide: units with assignments, quizzes, and discussions (paste an outline to split it automatically)
5. Facts and policies: Michigan Virtual facts prefilled, editable
6. Rules: items to never mention, and optional extra rules
7. Student Q&A: real questions with the teacher's answers
8. Review and export: checklist, both outputs, copy and download buttons, and test questions

Progress is saved in the browser. Teachers can also save a project file and reload it later, which is handy for a second section of the same course.

## How it reads a syllabus

It uses plain rules, not AI. It looks for common labeled sections ("Course Objectives:", "Prerequisites:", "Additional Costs:", "Scoring System:", "Technology Requirements:", "Course Outline:") and unit or module headings. It only fills fields that are still blank, and it tells the teacher what it found. Syllabi without labeled sections will fill in less, and the teacher fills in the rest by hand.

Why no AI: nothing leaves the teacher's browser, there is no API key or cost, and the app behaves the same for everyone.

## Put it on GitHub Pages

1. Create a new repository on GitHub and add `index.html` and this README.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and the `/ (root)` folder, and save.
4. After a minute the site is live at `https://YOUR-USERNAME.github.io/REPOSITORY-NAME/`.
5. Share that link with your department.

You can also open `index.html` directly from a downloaded copy. PDF and Word reading need an internet connection; pasting text and every other feature work offline.

## Privacy

Everything teachers type stays in their browser (local storage). The app has no server and sends nothing anywhere. The only network requests are to load two open-source libraries from cdnjs: pdf.js (reads PDFs) and Mammoth (reads Word files). Files are read on the teacher's computer.

## Customizing

Everything lives in `index.html`. Near the top of the script:

| What | Where |
|---|---|
| Character limit | `LIMIT` (5000) |
| Subjects and their rules | `SUBJECTS` |
| Michigan Virtual shared facts | `MV_SHARED` |
| Suggested student questions | `SUGGESTED_QS` |
| Stay-on-topic wording | `TOPIC_LOCK` |
| Wording of the generated instructions | `buildInstructions` |

If your school is not Michigan Virtual, change `MV_SHARED` and the default values in `defaults()`.

## Known limits

- Scanned PDFs (images of text) have no readable text. Teachers paste the text instead.
- Old `.doc` files are not supported. Save as `.docx` or PDF.
- Sorting items into assignments, quizzes, and discussions is based on wording, so teachers should check each unit.
- The app cannot see inside SchoolAI. Test the finished Space with the test questions on the last step.
- SchoolAI may change its limits or screens. If the 5,000 character limit changes, update `LIMIT`.

## Libraries

- [pdf.js](https://mozilla.github.io/pdf.js/) 3.11.174 (Apache 2.0), loaded from cdnjs
- [Mammoth](https://github.com/mwilliamson/mammoth.js) 1.6.0 (BSD 2-Clause), loaded from cdnjs
