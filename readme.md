## Build Instructions

Previously, the resume was built using Overleaf. Since Overleaf now requires a paid plan, the project has been pulled locally and the required LaTeX SDKs have been installed to build the resume and cover letter offline.

The codebase has been updated to support local builds using XeLaTeX.

## Project Structure

```
.
├── resume.tex              # Resume build entrypoint (personal info, sections, layout)
├── coverletter.tex          # Cover letter build entrypoint (same header/footer as resume.tex)
├── russell.cls              # LaTeX class powering both documents (styles, commands)
├── cv/
│   ├── summary.tex          # Resume section content
│   ├── experience.tex
│   ├── education.tex
│   ├── projects.tex
│   ├── skills.tex
│   ├── languages.tex
│   ├── achievements.tex
│   ├── publications.tex
│   ├── interests.tex
│   ├── references.bib       # Bibliography source (if publications are cited)
│   ├── coverletter.tex       # Cover letter metadata: recipient, subject, opening/closing
│   └── coverletter_body.tex  # Cover letter body text
├── font/                    # Fonts used by russell.cls
└── resume.bbl                # Compiled bibliography (tracked so builds don't require biber)
```

## How to Create/Update a Resume

1. Clean previous build artifacts:
   ```bash
   latexmk -C
   ```
2. Build the resume PDF using XeLaTeX:
   ```bash
   xelatex resume.tex
   ```
3. (Optional) To generate the PDF with a custom output file name, skip Step 2 and run:
   ```bash
   xelatex -jobname=File_Name resume.tex
   ```
   Replace `File_Name` with the desired name for the generated PDF output.

The generated `resume.pdf` will be available in the project root directory.

## How to Create/Update a Cover Letter

The cover letter uses the same `russell` class and personal info block as the resume, so it stays visually consistent automatically.

1. Edit the recipient, title, and opening/closing lines in [cv/coverletter.tex](cv/coverletter.tex):
   - `\recipient{<name>}{<address>}`
   - `\lettertitle{<subject line>}`
   - `\letteropening{...}` / `\letterclosing{...}`
2. Edit the letter body in [cv/coverletter_body.tex](cv/coverletter_body.tex), inside the `cvletter` environment.
3. Build the PDF:
   ```bash
   xelatex coverletter.tex
   ```
4. (Optional) Custom output file name, per application:
   ```bash
   xelatex -jobname=CoverLetter_CompanyName coverletter.tex
   ```

The generated `coverletter.pdf` will be available in the project root directory.

## Notes

- Both `resume.tex` and `coverletter.tex` share the same personal info block (name, contact, social links). If you update one, update the other to keep them in sync.
- LaTeX build byproducts (`.aux`, `.bcf`, `.log`, `.run.xml`, `.fls`, `.fdb_latexmk`, `%OUTDIR%/`, and generated root-level `.pdf` files) are git-ignored — see [.gitignore](.gitignore). They're regenerated automatically on each build, so don't commit them.
- `resume.bbl` is intentionally tracked (not ignored) since it lets the resume build with `xelatex` alone, without needing to run `biber` first.
