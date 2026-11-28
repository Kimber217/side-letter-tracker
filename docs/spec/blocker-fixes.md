# Spec: blocker fixes from the IR review

Source: [Side Letter Tracker: IR review](https://claude.ai/artifact/MfFkMWFnxK5Ep7u6aZqD9J), blockers B1 to B6. Decisions settled with Kimber on 25 and 28 Nov 2026. Terms follow `GLOSSARY.md`.

## Scope

Blockers B1 to B6 only. Major and minor findings and the design review wait for a later pass.

## Decisions

1. **Grant basis on every term (B1).** Values: commitment size, closing date, LP status, anchor package, none. A term can have several. It replaces the old "LP-status based" yes/no field: "yes" becomes the LP status grant basis.
2. **Carve-outs by category or grant basis (B1).** Each LP's MFN clause settings hold carve-outs by category (existing) and by grant basis (new). A term whose grant bases include a carved-out basis is not eligible for that electing LP.
3. **Carve-outs drafted at review (B1).** Extraction reads the letter's MFN clause and proposes carve-outs. The reviewer confirms them before Finish review; on finish they are written to the LP record. They stay editable on the LP.
4. **Backfill (B1).** The model proposes a grant basis for each existing approved term. Each proposal waits for a person to approve it. Until then, MFN results for that term are "Needs a decision".
5. **Conditions (B2).** Any term with a condition is "Needs a decision" for every electing LP, with the condition text shown. No automatic "eligible" for conditional terms.
6. **Letter vs LP record (B3).** Extraction reads commitment, legal name, letter date and closing from the letter. Review shows each mismatch with the LP record; Finish review is blocked until each is fixed on the record or overridden with a note.
7. **Brannock County (B3).** The record is corrected to the letter's $40,000,000.
8. **Generating worksheets while letters are in review (B4).** Generate names the letters still in review and offers two choices: wait, or generate anyway. When generating anyway, an LP whose own letter is in review gets no worksheet and is listed as "waiting for letter review". Draft terms never appear in any worksheet.
9. **Archive, not delete (B5).** LPs, letters and draft election worksheets can be archived and restored. Archived records drop out of totals, alerts, worksheets and search. Signed-off or sent worksheets cannot be archived. Every archive and restore goes in the audit log.
10. **Search on obligations (B6).** Questions about reports, notices or deadlines filter on "ongoing obligation = yes" instead of category. When the keyword cross-check finds approved terms, they join the results instead of the page showing 0.
11. **Internal label.** The MFN screen is the **election worksheet**, marked "Internal: do not send to the LP". An LP-facing election package export waits for the export work (M6).
12. **Release.** Build on a test copy of the artifact first; republish the live tracker only after Kimber has clicked through.

## Out of scope for this pass

Fee schedules, the obligations calendar, export, multi-vehicle letters, dated closings, structured conditions, the LP-facing election package, and the design review.
