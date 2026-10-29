# Evaluation

## How accuracy was measured

The test set was built with a known right answer for every cell:
- 7 vendors, 30 line items, and 8 emails (one vendor sent a revision);
- 38 planted problems: unit mismatches, outdated tax, lighter board, outside dimensions, hidden charges, lapsed validity, a revised quote and an expired certificate.

A separate scoring script compares the app's results with the answer key. The app itself can never read the answer key, so the comparison is fair.

## Results

| Measure | Result |
|---|---|
| Lines mapped to the right RFQ item | 210 of 210 |
| Raw values copied correctly | 197 of 197 checked |
| Landed price within 1% of the answer key | 207 of 207 quoted lines |
| Lines not quoted, marked Missing | 3 of 3; no cell shown as zero |
| Planted problems with a review item | 36 of 38 |
| Scenario totals (best single vendor, whole basket with its conditional discount, strict split) | match the answer key |

**Consistency, on a second extraction run with the same inputs:**
- the raw price was identical on 212 of 212 lines;
- no landed price differed by more than 0.5%;
- both runs scored 207 of 207 within 1%.

What did vary between runs was the number of review flags. One run raised an extra tax reading for one vendor.

## Honest caveats

- **These are best-case numbers.** The pricing rules were fixed against this same data, so the numbers show the rules work on these eight emails, not that they generalise.
- **The problem-detection score is generous.** A problem counts as caught if any signal appears on the affected cells, even one raised for another reason.
- **The real tests are unseen inputs.** The live demo accepts a new quote (email, PDF, Excel, Word or photo) and runs the real pipeline on it. In a live test, a one-page revision was read in about 9 seconds and changed one line to "Revised" in that session.

## Failures found in unscripted testing

Testing with questions that hadn't been rehearsed found real reasoning errors in the analyst. Each was fixed in the tools and code, not only in the prompt:

1. **"What if one more vendor were allowed in?"** The model used a pool that admitted every conditional vendor at once, instead of the one named. The split tool now takes the named vendor explicitly, and code refuses the wrong pool when a question names a vendor.
2. **"How does this compare with last year?"** Last year's prices were ex-works and this year's are delivered. The model compared them directly and reported a 3% increase. Last year's prices now carry an estimated landed figure, labelled as an estimate. Like for like, the result is a 0.6% decrease.
3. **A saving worked out by the model itself** was slightly wrong. Savings now come only from the scenario tools, and the number check understands lakh and crore.

## Drafting reliability

The drafting assistant first failed on the hosted app: answers came back garbled or cut off. The cause was a nested object in the tool schema. After the schema was flattened and made strict, 5 of 5 runs of the same example were usable on the first attempt.
