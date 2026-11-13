# pdftoslides

Turn a PDF into presentable slides.

> **Status: scaffold.** This repository currently contains this README only —
> there is no converter code, no tests, and no pinned dependencies yet. The
> sections below describe the *intended* scope so the first implementation has
> a target to hit. They are a plan, not a description of working software.

## What it is

Given a PDF — an exported deck, a paper, or a plain document — produce a
presentation you can actually show: one idea per slide, readable text, images
and diagrams carried over, and consistent layout instead of a wall of text.

Typical uses:

- Recover an editable deck from a PDF export whose source file was lost.
- Condense a long document (report, paper, notes) into a talk-sized deck.
- Restyle existing slides without redrawing them.

## Intended pipeline

1. **Extract** — pull text blocks, images, and page geometry out of the PDF.
2. **Segment** — group content into slide-sized units (per page, or split a
   dense page into several).
3. **Compose** — lay each unit onto a slide template: title, body, figure,
   speaker notes.
4. **Export** — write a `.pptx` deck (optionally HTML or Markdown too).

## Planned layout

```text
pdftoslides/
├── README.md
├── pdftoslides/        # package: extract -> segment -> compose -> export
│   ├── extract.py
│   ├── segment.py
│   ├── compose.py
│   └── export.py
├── templates/          # slide layouts and themes
├── examples/           # sample input PDFs and generated decks
├── tests/
└── requirements.txt
```

This layout is a proposal. Adjust it as the design firms up, and keep this
section in sync when you do.

## Prerequisites

- Python 3.10+
- A PDF engine for extraction (e.g. `pymupdf` or `pdfplumber`)
- `python-pptx` for writing PowerPoint output
- Optional: LibreOffice, for rendering PDFs and verifying generated decks

None of these are pinned yet — `requirements.txt` will be added with the first
working extractor.

## Getting started

Nothing to run yet. Once the first version lands, the intended entry point is:

```sh
python -m pdftoslides input.pdf -o slides.pptx
```

## Roadmap

- [ ] Extract text and images from a PDF, preserving page order
- [ ] Heuristic slide segmentation for multi-column and dense pages
- [ ] Compose onto a default template, with speaker notes
- [ ] Export to `.pptx`; verify it opens in PowerPoint and LibreOffice
- [ ] CLI flags: `--template`, `--max-bullets`, `--notes`
- [ ] Tests driven by a handful of small sample PDFs

## Contributing

Small, focused pull requests are welcome. Keep the pipeline stages separate,
include a sample PDF with anything that changes segmentation or layout, and
update this README when behaviour changes.

## License

No license has been chosen yet, so the default "all rights reserved" applies.
If this material should be reusable, add a `LICENSE` file — MIT for the code,
or CC BY 4.0 if the templates turn out to be the valuable part.
