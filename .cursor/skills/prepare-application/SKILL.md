---
name: prepare-application
description: Build a tailored resume and cover letter from the base resume in Base/ and a job description. Use when the user asks to prepare, tailor, or draft an application, resume, CV, or cover letter for a job, company, or role.
---

# Prepare an application

Create a tailored resume and a cover letter for one job. Read and follow both rules before writing:

- `.cursor/rules/tailored-resume.mdc`
- `.cursor/rules/cover-letter.mdc`

## Inputs

1. Read every resume file in `Base/`. If that folder is missing or has no resume, stop and ask the user to add one.
2. Use the job description from the conversation or from a file path the user gives. If none is available, ask for it. Do not draft from a company name alone.

## Names

Take the employer and job title from the posting. Slug each one the same way for folders and filenames:

- Replace `&` with `and`.
- Turn slashes, backslashes, `|`, `:`, and whitespace into a single hyphen.
- Remove `* ? " < >`.
- Collapse repeated hyphens and trim hyphens from the ends.

`Northwind Labs` and `Backend Engineer` become `Northwind-Labs` and `Backend-Engineer`.

## Write these files

```
Ready To Apply/<company-name>/<position>/Resume/<company-name>-<position>-Amir-CV.md
Ready To Apply/<company-name>/<position>/Cover Letter/<company-name>-<position>-Amir-CoverLetter.md
```

Example:

```
Ready To Apply/Northwind-Labs/Backend-Engineer/Resume/Northwind-Labs-Backend-Engineer-Amir-CV.md
Ready To Apply/Northwind-Labs/Backend-Engineer/Cover Letter/Northwind-Labs-Backend-Engineer-Amir-CoverLetter.md
```

If either file already exists, stop and ask before replacing it.

## Done

Reply with both paths and two or three requirements you emphasized. Name any job requirement you left out because the base resume does not support it.
