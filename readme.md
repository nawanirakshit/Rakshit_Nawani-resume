## Build Instructions

Previously, the resume was built using Overleaf. Since Overleaf now requires a paid plan, the project has been pulled locally and the required LaTeX SDKs have been installed to build the resume offline.

The codebase has been updated to support local builds using XeLaTeX.

## How to Create an Updated Resume

1. Clean previous build artifacts:
   ```bash
   latexmk -C
2. Build the resume PDF using XeLaTeX:
   ```bash
   xelatex resume.tex

3. (Optional) To generate the PDF with a custom output file name, skip Step 2 and run:
   ```bash
   xelatex -jobname=File_Name resume.tex
Replace File_Name with the desired name for the generated PDF output.

The generated resume.pdf will be available in the project root directory.