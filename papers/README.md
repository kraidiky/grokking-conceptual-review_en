# Paper cards

`papers/<arxiv-id>.<full-title-in-kebab-case>/` — one folder per paper.

This file is the convention for the paper cards of this repository: layout, anchor scheme, language and translation policy. The general, project-independent requirements for wiki pages (the portability of anchors across Obsidian, GitHub and VS Code) are in `b0.standards/standards-wiki-maintenance.txt`, rules 1, 6, 9, 10. The procedure for creating a card is the `import-paper-card` skill; its scripts live there too, in `.claude/skills/import-paper-card/scripts/`, rather than in `papers/`, so as not to clutter Obsidian.

The list of all the works of the corpus is in [`index.md`](index.md): twice over, by citation count and by chronology, with links to the cards that have been created. Works with cards carry the first author and the year in their entry ("Power et al. 2022 — …"), so that a work can be recognized by name and not only by identifier. Each work has two citation counts: "total" — its own citationCount from Semantic Scholar, taken from [`citations-2201.02177.txt`](citations-2201.02177.txt) (a single source, decision D1-A of task-008; an additional section of the table covers works not listed as citing Power), and "within the corpus" — how many works of the corpus cite it, computed from the stored `original/` files, from [`citations-in-corpus.txt`](citations-in-corpus.txt) (computed by `count_incorpus.py`, task-012).

## What the folder contains

| Path | What it is |
|---|---|
| `<the same name>.card.md` | the paper's card: the full text in translation, cross-references, a machine-readable block of facts |
| `original/` | the primary source as downloaded, and its direct conversion into Markdown with no changes to the content |
| `images/` | the paper's illustrations at their original resolution |
| `<the same name>.claims.txt` | the working analysis: the paper's claims, numbered and annotated. The `.txt` extension rather than `.md` is deliberate — otherwise the file clutters Obsidian's graph and search on a par with the substantive pages |
| `<the same name>.license.txt` | the arXiv licence record: the licence URL verbatim, the class, the dates of the record and of the retrieval (the `fetch_license.py` script, a mandatory part of ingestion) |

The card's service section — "Paper text" — is set as a first-level heading and set off by a horizontal rule. Otherwise it stands level with the sections of the paper itself ("Abstract", "1 Introduction", …) and gets lost in the outline; a first-level heading makes it a root node and the paper's sections nested ones.

The warnings about misciting are laid out on two sides and bear different names. On the side of the **citing** work that made the error there is a section "Common misreadings and overstatements": one entry per miscited work under the anchor `mc-<arxiv-id, with the dot replaced by a hyphen>`, with the verbatim wordings, a translation and an analysis. On the side of the **cited** work that is being misreported there is a section "Common misreadings and overstatements of this paper": one entry per pattern — what exactly gets distorted, the class, links to the authors' paragraphs carrying the qualification that goes missing, and "details" links to the entries of the citing works. Both sections stand last among the editorial ones, immediately before the paper's text; if a card has both, "Common misreadings and overstatements" comes first, then "Common misreadings and overstatements of this paper". The sections are built only from observed wordings; over-extending citations are distinguished by the fate of the thesis — later checked and confirmed (the confirming work is named) or explicitly refuted (the refuting work is named).

The primary source is taken in HTML where it is available; a PDF only when no HTML version exists. For papers published before the end of 2023 there is no native `arxiv.org/html/`, and the working source is the ar5iv rendering (LaTeXML) — which also supplies the authors' LaTeX for the formulas through the `alttext` attributes, so that the formulas in the card are reversible into their original notation.

In the working corpus a card is written in Russian and the English original always lies alongside, in `original/`, serving for checking; in this edition the card itself is English. The bibliography, the titles of works and personal names are carried over verbatim in either case.

## The "Concepts covered" section

Every paper card contains such a section: one paragraph per concept of the corpus that the work touches. It is written **from the side of the paper, not from the side of the concept card**: not "the card takes such-and-such a setup from here" but "the work makes such-and-such a setup standard". The subject of the description is what the work gave the concept, and in what status:

- it **introduces** the concept or gives it a name;
- it **gives the first observation**, which others later made sense of;
- it **sets a setting or an instrument** inherited by subsequent works;
- it **merely mentions** something adjacent — then that is said outright, and on the concept card the work stands under "Passing mentions".

It is just as important to write **what the work does not have**: which readings, terms and mechanisms appeared later and therefore must not be attributed to its authors. Without that caveat a paper card starts to read as an exposition of the present-day understanding rather than of what the authors wrote.

The links inside a paragraph lead to the place in the text where the claim stands: to the anchor of a paragraph, a figure caption or a section.

## How to link into a paper card

The anchors are token headings; Obsidian `^id` anchors and HTML `<a id>` anchors are forbidden as the stored form, and linking to an ordinary section heading is not allowed (the standard, rules 1, 6, 9). Below are the token forms adopted in this repository.

| Anchor | What it addresses | Example link |
|---|---|---|
| `pN-M` | paragraph M, beginning on page N | `[Power, p. 9, para. 2](…card.md#p9-2)` |
| `fig-N` | the caption of figure N | `[Power, fig. 1](…card.md#fig-1)` |
| `sec-…` | a section of the paper (`sec-3-3`, `sec-a1-1`) | `[Power, §3.3](…card.md#sec-3-3)` |

Paragraph numbering is positional: N is the page on which the paragraph **begins**, M is its ordinal among the paragraphs beginning on that page. Adding a new anchor later therefore does not renumber the existing ones.

A paragraph is any block of text, including the author block in the header: in a paper where the authors are listed before the abstract, the abstract is `p1-2`, not `p1-1`. Not paragraphs: headings, figure captions, images, tables, display formulas and standalone `**[p. N]**` marks.

The numbers are **computed, not written from memory**: `python3 .claude/skills/import-paper-card/scripts/anchor_number.py <arxiv-id> <paper.pdf>` prints the number for every paragraph, taking the page from the PDF. In the earliest cards they were written from memory — and drifted away from the text: in one paper the paragraphs from page 3 carried `p1-15` and `p1-16`, in another the text from page 4 was listed as `p6-3`. The discrepancies were corrected by `renumber_anchors.py`, which renames an anchor at once in the card, in `original/` and in every concept card that links to it.

Anchors are created only where something links to them (the standard, rule 10). Hence a corollary for paper cards: **there is no separate anchor for the start of a page** — if a page needs to be linked to, an anchor is created for its first paragraph (`pN-1`). If a link to a section of the paper is needed, a `sec-<number>` is created; deleting the link instead of creating the anchor is not allowed.

Page breaks are marked **without anchors**, by a visible `**[p. N]**` mark — in the middle of a paragraph it stands exactly at the boundary, so as not to break the text, and on a figure caption it indicates the page on which the figure is laid out. The pagination is recovered from the PDF: in the HTML version there are no pages, and figures float in LaTeX, so a caption printed at the top of a page may belong to text on the neighbouring one.

The same anchors are duplicated in the English file in `original/` — so that an English quotation and its translation address one and the same place in the two versions of the text.

## A link from a concept card

Two links to one and the same point in the two language versions: **the verbatim English quotation leads into the English original, its Russian translation into the paper card.** The title of the work is not made into a link.

```
[`"weight decay is particularly effective at improving generalization on the tasks we study"`](https://arxiv.org/abs/2201.02177).

```

The quotation stays verbatim English. **The purpose of the quotation is to make the difference between the author's claim in the paper's text and the card's generalized claim visible at a glance.** Verbatimness is understood at the level of words: the same words of the author in the same order, hedges included. A byte-for-byte match with the stored `original/` is not required — the original and the published PDF serialize one and the same text differently (ligatures, markdown emphasis, LaTeX against Unicode in formulas, small caps, the style of bibliographic references), and a quotation faithful to either serialization is verbatim; the formatting of citations inside a phrase ("(Power et al., 2022)" against "[41]") likewise counts as verbatim. The possibility of finding the quotation by full-text search in `original/` is not promised. Verbatimness is checked by `quote_check.py` from the scripts of the `import-paper-card` skill. The locator of a quotation is **an anchor in `original/`, not a line number**: a quotation refers by the form [`"…"`](…/original/….md#pN-M) to a paragraph of the stored original; this applies both to the entries of the concept cards and to the entries of the global concept index. The txt extractions of the repository the wiki was split out of (neuroinformatica2026) are not stored here and are not the carrier of the quotations. Line numbers `(line N)` remain only for works that have no cards yet [decision of task-004, 2026-08-07: for the three PDF-only works 2411.05353, 2507.11645, 2510.25966 the existing locators are kept until cards appear]; locally such a number is not checkable by anything — the search anchor is the verbatim quotation itself, and new entries for cardless works are made with a bare quotation and no locator. When a card appears, the import pipeline (`relink.py <id> --apply`) converts the entries into the link form, finding the paragraph by the text of the quotation; the line number is not used in that conversion and is discarded. The translation in a concept card must coincide with the corresponding fragment of the translation in the paper card — otherwise one and the same phrase sounds two different ways in the wiki; only case endings may differ, because the quotation stands in the nominative while the running text inflects it. When a quotation is added, the translation is taken from the paper card rather than composed anew; if the paper card does not exist yet, a bare verbatim quotation with no locator is placed, and the translation is agreed later, when the card appears.

## Translation policy

A card must differ from one's own picture of the subject exactly as much as the text of the primary source differs from it. In practice this means four prohibitions.

**Hedging is carried over word for word.** `we believe`, `we conjectured`, `seems to be predictive`, `might be distinct` — each is rendered by an equally cautious Russian phrase, never by a flatly assertive one. The authors' caution is part of the content: it is what distinguishes an observation from an established fact.

**Terminology that came into use after the paper is not imported.** If authors writing in 2022 say "suddenly begins to grow", the translation does not acquire a "phase transition"; if they have no "progress measures", "circuits" or "delayed generalization", neither does the card. This is checked by grep — but **the list of forbidden terms is built from the date of the paper, not once for the whole corpus**. For Power et al. 2022 a "circuit" and a "progress measure" would be a sign of contamination; in Nanda et al. 2023 those same words stand in the original as `circuits` and `progress measures`, and their absence from the translation would be an error. Every hit is checked against the authors' actual phrase.

**Claims later contested or refuted are preserved as written.** A card records what the authors thought at the time of publication, not what it turned out to be. A divergence from the present understanding is material for a concept card, not a reason to amend the translation.

**The authors' caveats and rough edges are not improved.** A typo or a missing preposition is translated by sense, silently — without correcting the content and without any marks.

Carried over verbatim: the bibliography, the titles of works, personal names, and the terms the corpus keeps in Latin script (`weight decay`, `residual dropout`, `decoder-only`, `t-SNE`). The choice of terms is agreed with the existing concept cards, so that one term does not sound two ways in the wiki.

## Excerpt cards

For some papers the licence does not permit publishing a full translation
(arXiv non-exclusive, CC BY-NC-ND), and for arXiv non-exclusive not even a
copy of the original. Such papers are represented by excerpt cards: a header
with a status line, the editorial sections and the quoted fragments of the
translation (the right of quotation). The full text is in the `original/`
folder of the paper (CC BY-NC-ND) or through the arXiv link in the header.
More in the review's root README.

## External works (externals/)

Papers that carry observations relevant to the corpus but are not themselves about grokking do not enter the corpus. For them there are three levels of treatment:

1. **The corpus** (`papers/`) — a full card, an analysis of the claims, participation in the indexes and counters. Only papers about the corpus's subject.
2. **An external work** (`externals/<arxiv-id>.<title-in-kebab-case>/`) — a stored `original/` (the snapshot fixes the version and the serialization: the quotations remain locally checkable and do not rot along with external links) plus an **excerpt card**: a header (authors, title, arXiv id and version, the source of the serialization, who in the corpus cites it), a status line "an external work; the abstract, the introduction and the quoted paragraphs are translated", then the translated abstract, the **introduction down to the first substantive section** (so that a reader understands at a glance what the paper is about) and only the quoted paragraphs — new paragraphs are translated lazily, as citations appear. A work demoted from the corpus keeps its full card as an over-complete excerpt — only a status line is added. In a bulk move by triage (task-021, decision D2-b) the mandatory minimum of an excerpt is a header and a translated abstract; **the introduction is translated lazily**, at the first quotation from the work or the first substantive appeal to it, and the status line says honestly what has already been translated.
3. **A bare external link with no local copy is forbidden**: such a citation is uncheckable from the moment it is made, invisible to quote_check, rots along with the address and drops out of future audits.

Every paper folder — both in `papers/` and in `externals/` — carries its own licence file `<folder>.license.txt` (written by the `fetch_license.py` script; the arXiv licence URL verbatim, the class, the dates of the record, the date of retrieval) — a mandatory part of any ingestion (task-020).

The register of external works is `externals/README.md`, one line per paper. External works take no part in the corpus's indexes (`papers/index.md`, both lists); they do not enter the `papers_linked` counter of the concept cards — only the works of `papers/` are counted.

**Marking in the text of the cards.** The entries of external works in concept cards live in a separate group "### External works" (with its own group number; the entries open with the words "External work (excerpt):" or "External work (demoted from the corpus):"). Every mention of an external work in running text carries the sign **↗** (U+2197, text presentation — this is not an emoji) immediately after the reference: `\[[5.1](#ref-5-1)\]↗` — the same sign Wikipedia uses to mark external links.

**Promotion (external → corpus):** git mv the folder into `papers/`, build the card up to a full one, remove the status line, move the entries from the "External works" groups into the substantive groups, relink the paths for the corpus, include it in both lists of the index and in the citation table, rerun `count_incorpus.py --write`, run `relink.py --check` over every affected paper and `quote_check.py` down to zero violations.

**Demotion (corpus → external):** the mirror procedure: git mv into `externals/`, a status line in the card, correction of its outgoing relative links (`../<folder>/…` → `../../papers/<folder>/…`), removal from both lists of the index, a `=ext` verdict in the citation table (the global number remains — the table stores the external numbers of every work), moving the entries that link to it into the "External works" groups with the ↗ sign, rerunning the counters, a line in the register.
