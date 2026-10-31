# resume-maker

Tailor a resume and cover letter for each job from one base resume, then file the application after it is submitted.

The resume in `Base/` is the only source of facts. Tailored documents reorder and rephrase that file for a specific job. They do not add employers, titles, dates, metrics, or tools that are not already there.

## Layout

```
Base/                                                                 # base resume
Ready To Apply/<company-name>/<position>/
  Resume/<company-name>-<position>-Amir-CV.md
  Cover Letter/<company-name>-<position>-Amir-CoverLetter.md
Applied/<company-name>/<position>/                                    # same files, after submission
```

Company and position names use hyphens. `Northwind Labs` and `Backend Engineer` become `Northwind-Labs` and `Backend-Engineer`.

## Workflow

1. Add the base resume under `Base/`.
2. Provide a job description and ask to prepare the application. That writes the resume and cover letter under `Ready To Apply`.
3. After submitting, ask to move that application to `Applied`. The position folder moves as-is:

```
Ready To Apply/Northwind-Labs/Backend-Engineer
→ Applied/Northwind-Labs/Backend-Engineer
```

## How documents are written

- `.cursor/rules/tailored-resume.mdc` keeps the base resume's sections, contact block, and voice, and shifts emphasis toward the job.
- `.cursor/rules/cover-letter.mdc` writes one letter for one company and role, using only the base resume and the job description.
- `.cursor/skills/prepare-application/` builds both files.
- `.cursor/skills/track-application/` moves a submitted application into `Applied`.
