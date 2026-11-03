# SchoolAI Course FAQ Builder

A single-page web app that helps teachers build a course-specific Student FAQ Space in SchoolAI. A teacher answers a short set of questions, adds a syllabus and instructor info, and gets two things to copy into SchoolAI:

- **Part A: Space instructions.** Kept under SchoolAI's 5,000 character limit for the "Describe your Space" box. A live character counter shows the length.
- **Part B: Knowledge file.** The course guide, instructor info, policies, and common student questions. Upload it to the Space as its document.

## Safeguards that are always on

- **Stay on topic.** If a student asks about anything other than the teacher's course, the Space stops and replies only with a redirect. It repeats the redirect if the student pushes back or says a teacher allowed it, and it ignores requests to change its rules.
- **Wellbeing exception.** If a student says something about their safety or wellbeing, the Space responds kindly and points to the instructor or school mentor instead of redirecting.
- **Graded work.** The Space does not do graded work, decide grades or extensions, or guess. It sends students to the instructor when it is unsure.
- **Due dates.** The Space never quotes dates and sends students to the place you name (for example, the Student Pacing Tool).
- **Subject rules.** Coding, fitness, math, writing, and world language courses each get an extra rule that fits the subject.

Teachers can add rules but cannot remove these.

## What teachers do

1. Course: name, subject, platform, and where students find due dates
2. Documents: paste or upload (PDF, DOCX, HTML, TXT, or MD) the syllabus, the welcome letter, and the Additional Resources
3. Instructor: paste a bio or fill in fields
4. Course guide: paste the Assignments, Quizzes, and Discussions pages from the course and the app builds the guide, sorting items into units and setting aside hidden or NOT IN USE items. Units and items can also be typed or built from a pasted outline.
5. Facts and policies: Michigan Virtual facts prefilled, editable
6. Rules: items to never mention, and optional extra rules
7. Student Q&A: real questions with the teacher's answers
8. Review and export: checklist, both outputs, copy and download buttons, and test questions

Progress is saved automatically in the browser on that computer.

## How it uses the syllabus

It uses plain rules, not AI. The full syllabus text goes into the knowledge file by default, so the assistant knows the course objectives, prerequisites, and costs. Teachers can turn that off on the last step if their syllabus has out-of-date information. The app can also pull unit names from a labeled "Course Outline:" section (or from "Unit 1" and "Module 2" style headings) to start the course guide. Syllabi without an outline find none, and the teacher adds units by hand.

Why no AI: nothing leaves the teacher's browser, there is no API key or cost, and the app behaves the same for everyone.

## Put it on GitHub Pages

1. Create a new repository on GitHub and add `index.html` and this README.
2. Go to **Settings > Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and the `/ (root)` folder, and save.
4. After a minute the site is live at `https://YOUR-USERNAME.github.io/REPOSITORY-NAME/`.
5. Share that link with your department.

You can also open `index.html` directly from a downloaded copy. PDF and Word reading need an internet connection; pasting text and every other feature work offline.

## Privacy

Everything teachers type stays in their browser (local storage). The app has no server and sends nothing anywhere. The only network requests are to load the Figtree font from Google Fonts and two open-source libraries from cdnjs: pdf.js (reads PDFs) and Mammoth (reads Word files). Files and text are read on the teacher's computer and never uploaded.

## Design

The look follows the [Michigan Virtual brand standards](https://michiganvirtual.org/brand): Figtree (with the approved fallbacks), Deep Teal and Dark Teal headings, Black Teal body text, green used only as an accent, and orange for calls to action, switching to the accessible orange on hover and focus. Text and background combinations meet WCAG AA. The brand standards don't define a dark mode, so the page is light only. The logo is not included; add one from the brand page's logo package if you want it.

## Customizing

Everything lives in `index.html`. Near the top of the script:

| What | Where |
|---|---|
| Character limit | `LIMIT` (5000) |
| Subjects and their rules | `SUBJECTS` |
| Michigan Virtual shared facts | `MV_SHARED` |
| Suggested student questions | `SUGGESTED_QS` |
| Stay-on-topic wording | `TOPIC_LOCK` |
| Colors | the `:root` variables at the top of the `<style>` block |
| Wording of the generated instructions | `buildInstructions` |

If your school is not Michigan Virtual, change `MV_SHARED` and the default values in `defaults()`.

## How the course guide is built

Typing every assignment is slow, so the app reads the course's own list pages instead. The teacher opens Assignments, Quizzes, and Discussions in Brightspace, selects all, copies, and pastes each into its box. The app:

- drops menu text, dates, and submission counts and keeps item names
- sorts each item into a unit by its number (1.2 goes to Unit 1, 03.04 to Module 3, "Module 3 Tracking..." to Module 3) or by the unit title appearing in the name
- puts items it can't place under "Other course items"
- sets aside items marked Hidden or NOT IN USE, and alternate quiz versions such as "(AV-MC3)", and adds them to the "never mention" list (alternate versions become one entry)
- ignores template items such as "Quiz Template"

Unit names come from the syllabus outline or an outline the teacher pastes. If none are given, units are named "Unit 1", "Unit 2", and so on. The teacher always reviews and fixes the result.

## Known limits

- Scanned PDFs (images of text) have no readable text. Teachers paste the text instead.
- Old `.doc` files are not supported. Save as `.docx` or PDF.
- The list-page parser is tuned for how Brightspace pages copy and paste. If another learning platform pastes differently, items may be missed. Teachers can fall back to typing them.
- Items with no number or unit title in the name land under "Other course items" and need to be moved.
- The app cannot see inside SchoolAI. Test the finished Space with the test questions on the last step.
- SchoolAI may change its limits or screens. If the 5,000 character limit changes, update `LIMIT`.

## Libraries

- [pdf.js](https://mozilla.github.io/pdf.js/) 3.11.174 (Apache 2.0), loaded from cdnjs
- [Mammoth](https://github.com/mwilliamson/mammoth.js) 1.6.0 (BSD 2-Clause), loaded from cdnjs
