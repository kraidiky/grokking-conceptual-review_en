# Grokking: a conceptual literature review

A conceptual literature review of grokking — the delayed generalization of
neural networks — in the form of a card wiki. The primary carrier of the
knowledge is the cards: concept cards (90) and paper cards
(172, of which 103 are full cards and 69 are
publishable excerpts), plus external works carrying relevant observations
(46).

This is the English edition of the review. The working language of the
review is Russian; the cards here are the English twins of the Russian
ones, stored in the repository beside them so that a correction has a
place to live and every build ships the identical text. The papers' own
text is not reproduced in the English edition: it is already in English
and is stored, as the authors published it, in the `original/` folder of
each paper, which is where every anchor in the cards points.

The review is the work of an author who uses language models. Errors and
inaccuracies are certainly present in it, and everyone is invited to look
for them: every find helps improve the code that produces this review.
Findings can be reported through the repository's issues.

## Where to start

- [concepts/index.md](concepts/index.md) — the global concept index.
- [papers/index.md](papers/index.md) — the index of the paper corpus: where each
  work stands in the corpus, with citation counts.
- [externals/README.md](externals/README.md) — the register of external works.
- [papers/README.md](papers/README.md) — the card convention: folder layout,
  anchor scheme, linking rules.

## How the cards are built

A paper card is a header with metadata, the editorial sections (what is shown,
points we could not reconcile inside the paper, common misreadings of the
paper) and a pointer to the paper's text in `original/`. A concept card
gathers the positions of every work of the corpus on a single concept, with
verbatim quotations and links into specific paragraphs of the papers.

Anchors of the form `pN-M` (page-paragraph), `fig-N` (figure), `sec-X`
(section) are the same in a card and in the conversion of the original — they
are what takes a reader from a concept card to the exact place in a paper.
Mentions of external works, which are not part of the corpus, carry the sign ↗.

## Licences and what went into the public version

The review is a fully open, non-commercial project for educational purposes.
The publication of each paper follows its arXiv licence; the licence record
lies in the paper's folder (`<folder-name>.license.txt`):

- Papers under Creative Commons (BY, BY-SA, BY-NC-SA) are included whole: the
  stored original, the illustrations, and a full card. The Russian edition
  additionally carries the full translation, which is a derivative work with
  attribution; for BY-SA papers derivative materials inherit the licence of the
  original.
- Papers under CC BY-NC-ND permit verbatim non-commercial distribution but not
  derivatives: the stored original and the illustrations are included, and in
  place of a full translation an excerpt card is published — the editorial
  sections and the quoted fragments (the right of quotation).
- Papers under the arXiv non-exclusive licence permit neither republication nor
  derivatives: for them only the excerpt card is published; the full text is
  reachable through the arXiv link in the card's header.

Copyright in the papers belongs to their authors; the link to the arXiv version
and the list of authors are in the header of every card.

The editorial materials of the review — the concept cards, the editorial
sections of the paper cards and the translations — are distributed under the
[CC BY-SA 4.0](LICENSE) licence: use and rework them freely, with attribution
and under the same licence. Translations of papers are derivative works: the
authorship of the original is given in the card's header, and translations of
BY-SA papers inherit the licence of the original even without that caveat.
Short quoted fragments of papers in the excerpt cards remain the right of their
authors and are given under the right of quotation.

A snapshot of the working corpus as of 2026-09-06.
