# bank-recon

OpenClaw / ClawHub skill for bank reconciliation.

## What it does

This skill reconciles bank statement activity to general ledger transactions and generates an Excel workbook with:

- `Summary`
- `Recon Results`
- `Unreconciled Bank`
- `Unreconciled GL`

## New capability

This version accepts either:
- a **bank statement Excel workbook**, or
- a **bank statement PDF**

When given a text-based bank statement PDF, the skill:
1. extracts `date`, `amount`, `description`, and `balance` from the statement table,
2. creates a structured companion workbook (`*_extracted.xlsx`), and
3. reconciles the extracted rows to the GL workbook.

## Example test case

Example inputs:
- `examples/chipmunk-bank-stmt.pdf`
- `examples/gl_data.xlsx`

Example command:

```bash
python skill/scripts/recon_logic.py examples/chipmunk-bank-stmt.pdf examples/gl_data.xlsx output/bank-recon-from-pdf.xlsx 5.00
```

Expected behavior for the bundled example:
- 100 bank rows extracted
- full reconciliation against the provided GL data
- companion extracted workbook created beside the PDF

## Notes

- Best for digital/text PDFs. Scanned image PDFs would require OCR or a multimodal extraction path.
- The skill itself lives under `skill/` so the repo can be used both by humans and by ClawHub/OpenClaw packaging flows.
