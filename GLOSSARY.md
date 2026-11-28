# Side Letter Tracker

The record of what Harrow Ridge Infrastructure Fund I promised each LP in side letters, and which LPs can claim those promises through their MFN clauses.

## Language

### Letters and terms

**Term**:
One promise the fund made to one LP, taken from one or more paragraphs of that LP's side letter.
_Avoid_: Right, provision, benefit (when meaning a single recorded promise)

**Condition**:
Something that must be true for a term to apply, stated in the letter (for example, a commitment of $50M or more, or admission at the Initial Closing).
_Avoid_: Requirement, qualifier

**Grant basis**:
The reason the fund gave a term: commitment size, closing date, LP status, anchor package, or none. A term can have more than one.
_Avoid_: Reason (alone), rationale, trigger, "LP-status based" (now the LP status grant basis)

**Ongoing obligation**:
A term that requires the fund to deliver something or give notice, once or repeatedly, by a deadline. Reports, notices and data deliveries are ongoing obligations whatever their category.
_Avoid_: Deliverable, reporting term (when the category is not Reporting)

### LPs

**LP record**:
The tracker's details for one LP: legal name, commitment, vehicle, closing and MFN clause settings. The side letter is the source; the record must match it.
_Avoid_: LP profile, LP setup

**Archived**:
Set aside by a person: an archived LP, letter or election package no longer counts in totals, alerts, election packages or search, and can be restored.
_Avoid_: Deleted, removed, hidden

### MFN

**MFN clause**:
The paragraph in an LP's side letter that lets it claim terms granted to other LPs.
_Avoid_: MFN right (when meaning the clause text)

**Carve-out**:
A kind of term an LP's MFN clause does not reach, named in that clause by category or by grant basis.
_Avoid_: Exclusion (alone), exception

**Holder**:
The LP that was granted a term.
_Avoid_: Grantee, original LP

**Electing LP**:
The LP whose MFN clause is being tested against another LP's term.
_Avoid_: Elector, claimant

**Election package**:
The document sent to one LP after the final close listing the other LPs' terms it may claim through its MFN clause. It contains what that LP's MFN clause entitles it to see, and by default names no other LP.
_Avoid_: Package (alone, outside the MFN context), MFN offer, compendium

**Election worksheet**:
The fund's internal working list for one electing LP: every other LP's term, its holder, and whether it is offered, needs a decision, or is not eligible and why. Never sent to the LP.
_Avoid_: Package (for the internal list), draft package

**Needs a decision**:
The result for a term the tracker cannot settle for an electing LP, so counsel decides. Every term with a condition gets this result.
_Avoid_: Review, pending, unclear

## Relationships

- A **Term** has zero or more **Conditions** and zero or more **Grant bases**
- An **MFN clause** has zero or more **Carve-outs**
- A **Carve-out** names a category or a **Grant basis**
- Each electing LP has one **Election worksheet**; counsel signs it off, and the **Election package** sent to the LP is drawn from its offered items only
