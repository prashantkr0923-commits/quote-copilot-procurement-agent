# Product brief

## The buyer

A procurement buyer at a manufacturing plant runs an RFQ for a category the plant buys every year. The demo uses corrugated packaging: 30 items (boxes, partition sets, pads and trays), roughly 960 tonnes a year, and seven vendors. The buyer must recommend an award they can defend to finance and to their manager.

## What makes the job hard

- **Format chaos.** Every vendor replies differently, and a few reply in ways no template survives: a photo, a scanned PDF, a sentence.
- **Unit and basis mismatch.** A price per kg and a price per box can't be compared until the box's weight is worked out from its specification. Some prices include tax at an outdated rate, some exclude freight, and one is in dollars per thousand.
- **Incomplete and ambiguous quotes.** "38 for the 3-ply, rest same as last year" has more than one reasonable reading.
- **Hidden risk.** The best-formatted quote can carry the most risk in its terms: lapsed validity, an escalation clause, a one-time plate charge. The cheapest headline price can be on lighter board than specified.
- **Trust.** A buyer won't act on a number they can't trace back to the vendor's own words.

## Who it is for

- **Primary:** the buyer running the RFQ, who needs one comparison and a defensible recommendation.
- **Secondary:** the buyer's manager or finance reviewer, who needs to see why a vendor won.
- **Tertiary (preview):** vendors, who are asked only about the points that were unclear in their quote.

## Scope

**In:**
- Drafting an RFQ from a chat, with an Excel template for vendors.
- Reading every vendor reply, whatever the format.
- One comparison with traceable numbers and status labels.
- A review queue for anything uncertain.
- Supplier questionnaire qualification, including certificates checked against the bid due date.
- Split-award and whole-basket scenarios.
- An analyst chat, with an Excel award summary.
- A vendor-side preview.

**Deliberately out:**
- **A real email server.** The inbox is a folder of real email files with their attachments, so the reading loop is genuine.
- **Feeding a drafted RFQ into the comparison.** The comparison runs on the RFQ that was actually issued; wiring a new RFQ through extraction and checks is a separate project.
- **Price comparison for other categories.** Drafting works for any category (an IT hardware RFQ was tested). Price comparison is built for corrugated packaging, as one "category pack" with its own formulas.

## What a buyer sees

| Page | What it does |
|---|---|
| Draft RFQ | Chat to draft an RFQ; export the vendor template |
| Inbox | Every vendor email and attachment as received; upload a new quote to run the real pipeline on it |
| Comparison | One grid of landed prices per piece, with a status on every cell and the recommended award marked. Click any number to see where it came from |
| Review queue | Uncertain items, starting with those that could change the award. The buyer confirms, corrects or drafts a question to the vendor; every decision is recorded next to the original value |
| Analyst | Questions in plain English; answers with tables, charts, the SQL used and an Excel export |
| Assumptions | Exchange rate, freight per lane, board allowances and size tolerance. Changing one recalculates everything for that session only |
| Vendor view (preview) | What a vendor would see: our reading of their quote and the questions only they can answer |

## What a better version would solve

Most of the uncertainty in the review queue exists because vendors write free text. A vendor-side flow could ask each vendor to confirm the system's reading, choose between two readings, or split a flat discount by item, before the deadline. The vendor view is a first step toward that.
