# Quote Copilot: AI Procurement Agent

Quote Copilot reads messy vendor quotations, turns them into one comparison a buyer can trust, and answers award questions in plain English.

**[Live demo](https://appapppy-cl7jquf8iannuwn4kvf32r.streamlit.app/)**: password protected. The password is shared on request.

---

## The problem

When a buyer sends out a request for quotation (RFQ), the replies come back in every format a vendor can think of:
- an Excel sheet in the vendor's own layout;
- a letterhead PDF, or a scanned one with no text in it;
- a Word letter with a discount buried in a paragraph;
- a one-line email ("rest same as last year");
- a phone photo of a printed rate card with a price crossed out and a new one written in by hand;
- a revised quote that replaces an earlier one.

Prices arrive per piece, per 100, per 1,000, per kg or per strip, in rupees or dollars, with or without tax and freight. Before anyone can compare them, someone rebuilds everything in a spreadsheet by hand. That is slow, and the mistakes in it are invisible.

## What it does

Three AI loops, all live calls to a language model:

1. **Drafting.** The buyer describes what they need in a chat. Quote Copilot drafts a structured RFQ (line items, a supplier questionnaire and commercial terms) and exports the Excel template that goes to vendors. It asks for missing essentials instead of inventing them.
2. **Reading and normalising.** It reads every vendor reply, whatever the format, and builds one comparison:
   - the same lines, in the same unit, on the same basis (excluding tax, delivered to the plant);
   - questionnaire answers and attached certificates next to the prices;
   - anything uncertain sent to a review queue instead of silently into the table.
3. **Analyst.** The buyer asks questions such as "split it, cheapest per line, only vendors who cleared the questionnaire". The answer comes with tables, charts and an Excel award summary, and every number in it is checked by code.

There is also a **vendor view (preview)**. It shows each vendor how their quote was read and asks only about the uncertain points. One vendor confirming one answer changes the recommended split award on screen.

## The rule underneath: the AI reads, code calculates

The language model extracts what each document *says*: the numbers and units copied word for word, with a pointer to where they came from. Every conversion, tax adjustment, freight estimate, total and split award is done in plain Python.

Because of this, every number on screen can explain itself. Click a price to see:
- the vendor's own words;
- the source, as a cropped PDF page, a highlighted spreadsheet cell or an upright photo;
- each calculation step and every assumption;
- a status: Extracted, Converted, Inferred, Missing, Low confidence, Spec deviation, and so on.

A missing price is shown as **Missing**, never zero. A discount that applies only if one vendor wins everything is shown as a separate scenario, never applied to line prices.

## Results

Measured against an answer key the app never reads, on a test set of 7 vendors, 30 line items and 8 quote emails with 38 planted problems:

| Measure | Result |
|---|---|
| Line items matched to the RFQ | 210 of 210 |
| Landed prices within 1% of the answer key | 207 of 207 quoted lines |
| Lines a vendor didn't quote, marked Missing | 3 of 3 (none shown as zero) |
| Planted problems raised for review | 36 of 38 |
| Second run, same inputs | the same raw price on 212 of 212 lines; no landed price more than 0.5% different |

**The caveat:** the rules were tuned on this same data, so these numbers show the method works on these quotes, not that it generalises. The real tests are unseen quotes and unscripted questions. The live demo lets a reviewer upload a new quote and run extraction on it. Details are in [docs/evaluation.md](docs/evaluation.md).

## What's in this repository

| File | What it holds |
|---|---|
| [docs/product-brief.md](docs/product-brief.md) | The buyer, the problem, scope, and what was deliberately left out |
| [docs/architecture.md](docs/architecture.md) | How a quote travels from email to comparison, and the analyst's tools |
| [docs/decisions.md](docs/decisions.md) | The main product decisions and why |
| [docs/evaluation.md](docs/evaluation.md) | How accuracy was measured, the results, and the failures found in unscripted testing |

The source code is in a private repository and is available on request.

## Built with

- Python, with Streamlit for the interface, hosted on Streamlit Community Cloud
- The Claude API, with tool use and strict JSON schemas, for extraction, qualification, drafting and the analyst
- DuckDB for the analyst's read-only queries
- Claude Code as the build environment

## About the data

The buyer, the vendors, the people, the documents and the certificates are all fictional. The dataset was built for this project, including real phone photos of a printed, hand-marked rate card.
