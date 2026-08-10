## Build Instructions

Previously, the resume was built using Overleaf. Since Overleaf now requires a paid plan, the project has been pulled locally and the required LaTeX SDKs have been installed to build the resume and cover letter offline.

The codebase has been updated to support local builds using XeLaTeX. All build output (PDFs and intermediate files) is written to `build/` so the project root stays clean — see [Build Output](#build-output) below.

## Project Structure

```
.
├── resume.tex                # Resume build entrypoint (personal info, sections, layout)
├── coverletter.tex           # Cover letter build entrypoint (same header/footer as resume.tex)
├── russell.cls                # LaTeX class powering both documents (styles, commands)
├── cv/
│   ├── summary.tex           # Resume section content
│   ├── experience.tex
│   ├── education.tex
│   ├── projects.tex
│   ├── skills.tex
│   ├── languages.tex
│   ├── achievements.tex
│   ├── publications.tex
│   ├── interests.tex
│   ├── references.bib        # Bibliography source (if publications are cited)
│   ├── coverletter.tex       # Cover letter metadata: recipient, subject, opening/closing
│   └── coverletter_body.tex  # Cover letter body text
├── font/                     # Fonts used by russell.cls
├── resume.bbl                 # Compiled bibliography (tracked so builds don't require biber)
└── build/                     # Git-ignored build output (PDFs + LaTeX byproducts)
    ├── resume/
    └── coverletter/
```

## How to Create/Update a Resume

1. Build the resume PDF using XeLaTeX, writing output to `build/resume/`:
   ```bash
   xelatex -output-directory=build/resume resume.tex
   ```
2. (Optional) To generate the PDF with a custom output file name, use `-jobname`:
   ```bash
   xelatex -output-directory=build/resume -jobname=File_Name resume.tex
   ```
   Replace `File_Name` with the desired name for the generated PDF output.
3. (Optional) To clean previous build artifacts before rebuilding:
   ```bash
   rm -f build/resume/*
   ```

The generated PDF will be available at `build/resume/resume.pdf` (or `build/resume/File_Name.pdf` if a custom jobname was used).

## How to Create/Update a Cover Letter

The cover letter uses the same `russell` class and personal info block as the resume, so it stays visually consistent automatically.

1. Edit the recipient, title, and opening/closing lines in [cv/coverletter.tex](cv/coverletter.tex):
   - `\recipient{<name>}{<address>}`
   - `\lettertitle{<subject line>}`
   - `\letteropening{...}` / `\letterclosing{...}`
2. Edit the letter body in [cv/coverletter_body.tex](cv/coverletter_body.tex), inside the `cvletter` environment.
3. Build the PDF, writing output to `build/coverletter/`:
   ```bash
   xelatex -output-directory=build/coverletter coverletter.tex
   ```
4. (Optional) Custom output file name, per application:
   ```bash
   xelatex -output-directory=build/coverletter -jobname=CoverLetter_CompanyName coverletter.tex
   ```

The generated PDF will be available at `build/coverletter/coverletter.pdf` (or `build/coverletter/CoverLetter_CompanyName.pdf` if a custom jobname was used).

## Build Output

Both `resume.tex` and `coverletter.tex` write their PDFs and all LaTeX byproducts (`.aux`, `.bcf`, `.log`, `.run.xml`, etc.) into `build/resume/` and `build/coverletter/` respectively, via the `-output-directory` flag. This keeps the project root free of clutter on every build.

`build/` is git-ignored (only empty `.gitkeep` placeholders are tracked so the folders exist after a fresh clone) — see [.gitignore](.gitignore). Regenerate PDFs locally whenever you need them; don't commit them.

## Notes

- Both `resume.tex` and `coverletter.tex` share the same personal info block (name, contact, social links). If you update one, update the other to keep them in sync.
- `resume.bbl` is intentionally tracked (not ignored) since it lets the resume build with `xelatex` alone, without needing to run `biber` first.
