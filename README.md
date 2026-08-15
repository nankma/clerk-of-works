# Clerk of Works

A knowledge tool for homeowners working with a contractor on their own house — so you can ask an informed question, not just nod along.

## Why this exists

Passing city inspection doesn't mean nothing needs to be redone — it just means an inspector happened to catch (or miss) what's visible at the time they show up. Most of a house's construction quality gets sealed behind drywall, siding, and roofing long before anyone from the city sees it. And a contractor, however experienced, is not infallible and doesn't always know everything either — trades specialize, codes get amended, and "the way we've always done it" isn't always the way the current code or current best practice actually requires.

The goal here isn't to replace an inspector, and it isn't to make a compliance ruling. It's to make sure the *owner* — the person paying for the work and living in the result — has enough grounded, cited knowledge to have a real conversation with their contractor before something is closed up and expensive to fix.

**Historically, this role has a name.** A *Clerk of Works* is an owner's representative on a construction project — independent of the contractor — whose job is to observe the work and flag anything that doesn't match spec or code, on the owner's behalf. This project is a (much smaller, software) attempt at that same function.

## What it does today

Retrieval-augmented Q&A over the Washington State Residential Code (2021 WSRC, based on the 2021 IRC + WA amendments) for single-family house construction:

- Chunked by section number (not character count), with exceptions kept attached to their parent rule — splitting an exception from its rule is the single most dangerous failure mode for a tool like this, since it can make the system state the opposite of what the code actually says.
- Hybrid retrieval (BM25 + dense) so it handles both exact section lookups ("R602.10") and natural-language questions ("how far apart do outlets need to be").
- Every answer cites a section number and a verifiable source link — **machine locates, human confirms**. The system is not the final word; the code text and, where it matters, an actual inspector are.

## Code text and licensing — what this repo does and doesn't contain

**This repository ships tools, not code text.** The IRC (International Residential Code) is copyrighted, published, and sold by the International Code Council (ICC). This repo does not include, and will not include, any ICC-authored code text, PDFs, or extracted excerpts of it.

What it does provide:
- A script that downloads Washington's free, publicly published amendment PDFs directly from `sbcc.wa.gov`.
- A parser that chunks whatever PDF you point it at (by section number, exceptions kept attached to their parent rule) into structured Markdown.

If you want to run this against the base 2021 IRC, you need to buy it yourself from the [ICC Shop](https://shop.iccsafe.org/) — this project doesn't, and isn't intended to, substitute for that purchase. Downloaded PDFs and any text extracted from them stay local (`data/` is gitignored) and are never committed to this repo.

None of this is a legal opinion — whether model-code text incorporated into law is copyrightable at all is genuinely unsettled and varies by court (see *Veeck v. Southern Building Code Congress International*), and ICC actively enforces its copyright regardless. The above is a practical "tools only, bring your own source" boundary, not a guarantee.

## Why it's not code-only

Code is a floor, not a description of good construction. It defines the legal minimum, not the modern, durable, or sensible way to build something — and "technically passed inspection" and "actually done well" are frequently different things. So alongside code text, this project is also gathering construction SOP / best-practice knowledge (from builder and inspector forums, building-science sources, etc.) — the kind of judgment an experienced tradesperson has and a first-time homeowner usually doesn't. The aim is for a homeowner to be able to ask not just "does this meet code" but "is this actually how it should be done."

## Where this is headed

Longer-term, more ambitious directions under consideration — not built yet:

- **A portable camera device** that can watch ongoing work and flag something worth asking about, live, while it's still open and inexpensive to fix.
- **Meeting/conversation analysis** — feed in a recording of a discussion or walkthrough with a contractor and check whether what was proposed or described lines up with code and known best practice.

## Scope limit — read this before trusting an answer

This tool answers **"what does the code/best-practice literature say"** — it does not, and is not intended to, issue a compliance verdict on your specific house. Actual compliance determination requires a licensed inspector, permit records, and often direct inspection of concealed work that no retrieval system can see. Treat every answer as a starting point for a conversation, not a final ruling.
