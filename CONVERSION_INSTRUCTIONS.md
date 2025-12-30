# Converting Marp Presentation to PDF

## Option 1: Marp CLI (Recommended)

Marp CLI is the official tool and handles all Marp features (backgrounds, custom CSS, etc.).

### Installation:
```bash
npm install -g @marp-team/marp-cli
```

### Convert to PDF:
```bash
marp Software_Architecture_Uncertainty.md --pdf --allow-local-files
```

### With custom output name:
```bash
marp Software_Architecture_Uncertainty.md --pdf --allow-local-files -o Software_Architecture_Uncertainty.pdf
```

### Additional options:
```bash
# Set theme (if using a theme)
marp Software_Architecture_Uncertainty.md --pdf --theme default --allow-local-files

# Set page size (default is A4)
marp Software_Architecture_Uncertainty.md --pdf --pdf-size A4 --allow-local-files

# For better quality
marp Software_Architecture_Uncertainty.md --pdf --allow-local-files --pdf-outlines
```

---

## Option 2: Pandoc (Alternative)

Pandoc can convert, but may not preserve all Marp-specific features like:
- Background images
- Custom CSS styling
- Marp-specific directives

### Basic conversion:
```bash
pandoc Software_Architecture_Uncertainty.md -o Software_Architecture_Uncertainty.pdf
```

### With better formatting:
```bash
pandoc Software_Architecture_Uncertainty.md \
  -o Software_Architecture_Uncertainty.pdf \
  --pdf-engine=pdflatex \
  -V geometry:margin=1in \
  -V fontsize=12pt
```

### Using xelatex (better for fonts):
```bash
pandoc Software_Architecture_Uncertainty.md \
  -o Software_Architecture_Uncertainty.pdf \
  --pdf-engine=xelatex \
  -V geometry:margin=1in
```

**Note:** Pandoc will convert the markdown to a document, but won't create slide-per-page format. For slides, you'd need to use beamer or another slide format.

---

## Option 3: Marp for VS Code (If using VS Code)

1. Install the "Marp for VS Code" extension
2. Open your `.md` file
3. Click the "Export slide deck" button in the top right
4. Choose PDF format

---

## Recommendation

**Use Marp CLI** - It's designed specifically for Marp presentations and will preserve:
- Background images
- Custom CSS styling
- Slide layouts
- Two-column layouts
- All Marp directives

The `--allow-local-files` flag is important because your presentation references local images in the `images/` directory.
