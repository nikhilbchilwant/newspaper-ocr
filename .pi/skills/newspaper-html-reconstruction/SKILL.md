---
name: newspaper-html-reconstruction
description: Reconstruct scanned newspaper PDFs as scrollable HTML pages with real headings, text, and newspaper-style columns; use when asked to OCR, transcribe, or recreate a newspaper page or issue from scans.
---

# Newspaper HTML reconstruction

Turn scanned newspaper pages into a readable HTML newspaper—not a full-page scan displayed as the webpage. Use scan imagery selectively for distinctive printed artwork or illustrations while keeping headlines, article text, and layout in HTML.

## Workflow

1. **Scope the request.** Identify the input PDF, requested page range, and requested output. Distinguish PDF pages from printed newspaper pages: a landscape PDF page may contain a two-page spread. Confirm the mapping before counting or generating HTML. If the user limits the work, process only that scope.
2. **Inspect the source.** Check page count, dimensions, orientation, and whether the PDF contains selectable text. Render low-resolution previews to identify page layouts, spreads, illustrations, and ad pages. Keep temporary renders and OCR artifacts in a temporary working directory.
3. **OCR using the requested compute environment.** Use Colab through the `colab` CLI when the user requests it or says local compute is inadequate; do not run OCR or other compute-heavy processing locally in that case. Otherwise prefer locally installed tools and models, and avoid downloading models or making network requests unless asked. Render at a resolution that makes small print legible. For spreads, split the rendered image into its printed pages before assigning text to columns. If OCR combines adjacent columns, OCR individual column crops instead.
4. **Reconstruct structure.** For each printed page, create semantic HTML for source-visible running headers, masthead, issue details, headlines, column text, notices, and advertisements. Match the source's column order, rules, hierarchy, and relative density. Transcribe only wording supported by the scan or OCR verified against it. Do not invent, paraphrase, summarize, or editorialize as if it were source text. Do not create or infer article headings from subject matter; use a heading only when it is legible in the source. If a short clarification is essential for understanding, add it sparingly in square brackets, clearly separated from the transcription. Otherwise omit it. Preserve uncertain or damaged wording as uncertain instead of guessing. Make page-specific layouts for unusual pages such as advertisements.
5. **Reuse imagery selectively.** Crop distinctive mastheads, engravings, or product illustrations from the PDF when useful. Reference those image assets from the HTML. Do not use a whole-page scan as the visual page when the task is an HTML reconstruction.
6. **Build the reading experience.** Put the requested printed pages in order in one HTML document, with responsive newspaper-style page sections and a page index or anchors when useful. Ensure all asset paths work locally and the page remains readable on narrow screens.
7. **Verify scope and output.** Check that every requested printed page appears once and in the right order, especially when PDF pages are spreads. Parse or open the generated HTML, verify referenced assets exist, and check that text and headlines are HTML rather than hidden OCR over a page image. Report any OCR limitations or deliberately condensed text.

## Layout and OCR guidance

- A newspaper page commonly has three narrow columns; preserve the column boundaries rather than sorting all detected text into one transcript.
- Group OCR lines into paragraphs using their positions and spacing. Merge fragments on the same baseline, keep distinct columns separate, and remove line-wrap hyphenation only when the scan supports it.
- Use semantic headings only for headings actually visible in the source. Preserve original spelling and wording where legible; do not fabricate headings or explanatory copy. Prefer omission to added prose; when essential clarification cannot be avoided, enclose only that clarification in square brackets. Flag scan damage briefly and in brackets only when readers need it to interpret an omission.
- Newspaper ads may use mixed orientations, illustrations, tables, and custom boxes. Rebuild them as HTML blocks and use cropped source illustrations as needed instead of forcing them into ordinary article columns.
- Keep first-page mastheads, issue metadata, and article headlines visibly prominent. Do not mistake a successful OCR transcript for a faithful layout reconstruction.

## Completion criteria

The result is complete when all requested printed pages—not merely all PDF files—are represented in the correct order in a scrollable HTML document; headlines and article text are actual HTML; the newspaper column structure is apparent; local images resolve; and OCR limitations are disclosed.
