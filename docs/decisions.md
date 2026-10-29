# Decisions

The decisions that most change what the buyer sees, with the reasons.

## D1. Corrugated packaging as the demo category

**Options:** IT hardware; maintenance spares; freight lanes; corrugated packaging (chosen).

**Why:** its hardest ambiguity, per kg against per box, can be settled by calculation from the box specification, so the system can show its working. It is bought every year, so "same as last year" and split awards come up naturally. In IT hardware the unit problem disappears, and the main question ("is this model equivalent?") is a judgement that can't be proven.

## D2. A fabricated dataset with planted problems and an answer key

**Why:** because the right answer for every cell is known, accuracy can be measured instead of claimed. Casually generated vendor files come out too clean, and the demo would only show the happy path. The dataset includes:
- outdated tax baked into prices;
- lighter board sold as "equivalent";
- outside dimensions;
- charges and lapsed validity hidden in a Terms tab;
- a revised quote.

## D3. Real photos of a hand-marked rate card

**Why:** a simulated photo is clean in unrealistic ways. A printed rate card, with a price struck out and a new one handwritten, was put in a plastic sleeve and photographed at an angle, six times. The true prices are the same in every photo, so accuracy can be reported per photo. One planned problem, glare hiding a digit, was dropped because it never happened in the real photos.

## D4. The AI reads; code calculates

**Why:** models can make arithmetic slips and can't show a checkable calculation. The model copies what the document says with a pointer to where; Python does every conversion with a visible formula. This is what lets a buyer trust a large award decision.

## D5. The answer key is isolated from the app

**Why:** if the app could see the answer key, accuracy numbers would mean nothing. The app reads only the inbox and the buyer's own data. The scoring script runs separately.

## D6. A missing price is Missing, never zero

**Why:** a zero makes an incomplete basket look cheap. A vendor with missing lines shows "27 of 30 lines" instead of a total.

## D7. Conditional discounts are never applied to line prices

**Why:** a discount that applies only if one vendor wins everything disappears in a split award. Applied to line prices, it would make a split look cheaper than it really is. It is shown as its own whole-basket scenario, labelled "only if awarded everything".

## D8. A price with more than one reading: price every believable reading, default to the costlier one

**Why:** the buyer should never see a saving that depends on guessing in the vendor's favour. If the vendor confirms the cheaper reading, the price only improves.

**How:**
- Readings no vendor in the market would charge are set aside, using the other vendors' prices for the same line as the reference.
- When two believable readings remain, the cell says "needs vendor confirmation", and the other reading is shown with its price.

**Considered:** picking the most natural reading by hand. Rejected, because "natural" is a judgement the buyer can't check, and the model and I disagreed on it.

## D9. A reading is ambiguous only when it changes the price

**Why:** the model raises many possible readings. Only those that give a different price on some line need the buyer's attention; the rest would bury the review queue.

## D10. Questionnaire: the model reads the wording, code decides

**Why:** whether an answer passes a numeric rule, or whether a certificate was valid on the due date, should never depend on the model's arithmetic.

**Borderline answers:** an answer such as "Yes, full lab incl. strength testing" flipped between pass and unclear across prompt versions. I chose not to keep tuning the prompt to hit the expected answer, because that would be fitting the prompt to the answer key. An unclear answer to a mandatory question makes the vendor Conditional, the reason is shown, and the buyer confirms with one click.

## D11. Every number explains itself, and every decision is recorded

**Why:** trust. Clicking any price shows the vendor's words, the source and each calculation step. When the buyer confirms, corrects or overrides something, it is recorded with a note and time, and the original value is kept beside it.

## D12. The analyst answers only through tools, and code checks its numbers

**Why:** "the AI reads, code calculates" has to hold in a chat too. The model must compute differences in SQL or a scenario tool, and code checks every number in its answer against the tool results. Unscripted testing found two reasoning errors (see [evaluation.md](evaluation.md)). Both were fixed in the tools and code, not only in the prompt.

## D13. Hosted with a password, fresh state for every reviewer

**Why:** a public app would let anyone spend the API budget. A password gate runs before any page, and the app refuses to open if the password is missing. Each viewer's decisions live in their own browser session.

## D14. A drafting assistant kept small, but working for any category

**Why:** drafting matters less than reading and comparing, so it got a strict time box. It still had to work for more than boxes: a drafting tool that only knew box sizes would make an IT hardware RFQ look broken. Drafting is generic; price comparison stays a "category pack" for corrugated packaging.

**Rule:** nothing about the buyer's business is invented. Sizes, quantities and dates not given are left blank and asked for.

## D15. A vendor view, as a preview

**Why:** the biggest source of uncertainty is free-text vendor replies. Asking each vendor to confirm the system's reading is cheaper than the buyer chasing every point.

**Integrity rules:**
- the buyer's decision wins over the vendor's;
- a price change after the deadline needs the buyer's acceptance;
- a vendor can't override hard evidence, such as an expired certificate.
