# Roadmap

## Why this exists

Books currently sell only through Apple Books. At the $1.99–$2.99 price points used for these titles, Apple's 30% cut plus the low sticker price barely clears anything, and with more books planned, that math needed to change.

The fix isn't chasing a lower percentage fee, it's two things: picking a platform that doesn't also tack on a flat per-transaction fee (which is what actually kills margin on a cheap ebook), and moving toward bundle/catalog offers over time, since Apple doesn't support that well but a direct-sales page can.

Rough numbers on a $1.99 book:
- Apple Books (30% flat): keep **$1.39**
- LemonSqueezy (5% + $0.50): keep **$1.39** — the flat fee erases the lower percentage
- Stripe direct (2.9% + $0.30): keep **$1.63**
- Gumroad (flat 10%, no separate fixed fee): keep **$1.79**

**Gumroad** won out over LemonSqueezy and a self-built Stripe checkout for three reasons:
- Best net take at these price points (see above)
- LemonSqueezy is mid-migration into Stripe Managed Payments (as of their Jan 2026 update), with storefront/download-delivery features specifically flagged as possibly not surviving the move, that's exactly the feature this needs
- A self-built Stripe checkout would save a few more points of fee but means owning file-delivery security and VAT/sales-tax compliance directly; not worth the engineering time at this volume

Direct sales also get buyer emails, which Apple denies entirely. Useful later for telling past buyers about new releases, something that compounds as the catalog grows past today's 8 titles.

## Decisions locked in

- Standalone page (not just a section on the main consulting site), since the current site would get long as titles grow; lives as `index.html` at the repo root so it's what loads at `books.britleyhoffconsulting.com` directly
- Launch with individual book listings only, no bundle offer yet, that gets added later once a bundle product exists in Gumroad
- Cover art is supplied manually (from existing Apple Books listings or new art), no placeholder-image system
- Future books get added via a simple per-book intake file (`books/<slug>.yaml` + cover image) that gets reviewed and folded into the published page, rather than hand-editing markup for every new title
- This lives in its own repo (`books`), not inside `wren-creator.github.io`, connected via subdomain (see Next actions). Note: `wren-creator/books` on GitHub was already taken by an older private repo of manuscript drafts/cover art, that got renamed to `wren-creator/book-manuscripts` to free up the name for this repo

## Next actions

- [x] Create Gumroad account
- [x] Verify a payout method (bank or PayPal)
- [x] Post first book(s) as Gumroad products — *LLMOps Infrastructure for the Generative Era*, *The Prompt Playbook*, *A Beginner's Introduction to Terraform*, all live on Gumroad
- [x] Build `index.html` + `data/books.js` + `.book-grid`/`.book-card` styling — three books live, intake files in `books/`, covers pulled from the Gumroad listings into `assets/books/`
- [x] Decide how this repo connects to britleyhoffconsulting.com — **subdomain**: `books.britleyhoffconsulting.com`
- [x] Enable GitHub Pages on `wren-creator/books` (source: `main`, root)
- [x] Add a DNS `CNAME` record at GoDaddy: `books` → `wren-creator.github.io` — live
- [x] Wire a link from `wren-creator.github.io`'s homepage Publications section over to this page

## Learning Series (Mainframe 101 follow-ons)

*Mainframe 101* ($6.99, live on Gumroad) is book 1 of a planned 5-book learning series built on the WebTerm/3270 mock LPAR fleet. Shape decided 2026-08-10, after weighing how much real mock content exists per platform against how much new build work a standalone book would demand:

- **Book 2 — IBM i (AS/400) & RPG IV**: richest existing mock content already (WRK* commands, PDM source navigation, a real RPG interpreter already running two programs), least new build work needed. Live on Gumroad.
- **Book 3 — z/OS Fundamentals**: framed as "operator/app developer" (ISPF, JCL, SDSF) rather than the security-tooling angle *WebTerm/3270: The Nuts and Bolts Guide* already owns, so the two titles don't cannibalize each other. Live on Gumroad.
- **Book 4 — Specialized Engines: z/VM & z/TPF**: combined rather than split into two books, six sessions instead of the usual seven, sized to what the mock fleet actually supported. Content task list settled and closed in `web3270`'s `Bridge_server/ROADMAP.md` first (added the MAXVAL REXX exec to close the one real gap), then written, six sessions plus capstone, every command traced against `mock-zvm.js`/`mock-tpf.js` source. Live on Gumroad.
- **Book 5 — Advanced/Capstone**: cross-platform orchestration and integration. Scoped 2026-08-20 as a four-hop "Data Integrity Night" token chain, z/OS produces a Batch Control Number, IBM i validates it and issues a Resource Clearance Code, z/VM's REXX interpreter checks that and computes a System Authorization Value, z/TPF's `ZBOOK` requires both prior values to finalize a booking. No shared datastore between mocks, each hop just validates a fixed value from the last; the client's existing multi-session tabs are the actual mechanic, so a student genuinely has to do all four platforms in order, not skip to the end. Built and verified live against the real mocks (task list closed in `web3270`'s `Bridge_server/ROADMAP.md`), six sessions written, cover art, packaged. Live on Gumroad.

**Learning series complete as of 2026-08-20** — all five books (101-105) shipped and live on Gumroad.

## 200 Series (Operational Judgment)

Full plan: `/Users/britleywrenhoff/.claude/plans/let-s-plan-out-what-lively-tarjan.md`. Task list logged in `web3270`'s `Bridge_server/ROADMAP.md` ("Operational Judgment — Mainframe 200 series prep"). Shift decided 2026-08-21: operational judgment over rote commands, troubleshooting/incident-response scenarios on the same four platforms, plus a first, deliberately light touch of security-adjacent content, heavier security depth reserved for a future 400 series.

Two constraints shaped the whole series before any book got scoped: *WebTerm/3270: The Nuts and Bolts Guide* already owns nearly all the obvious security-tooling content (deep z/OS RACF recon, CICS/DB2, the z/VM minidisk exposure, the entire IBM i 7-tool security suite), so none of that is reusable without cannibalizing an already-published book. And nothing in the mock fleet models an ambiguous/multi-cause failure today, every outcome anywhere is a single fixed, deterministic response, that's the one real new-build lift every book in this series needs.

- **Book 1 — Orientation** (*Mainframe 201*): one small Differential-Diagnosis vignette per platform, teaches the Triage → Isolate → Remediate loop the rest of the series exercises. Built and verified live against the real mocks (task list closed in `web3270`'s `Bridge_server/ROADMAP.md`), six sessions written (~6,400 words), amber cover art, packaged. Live on Gumroad.
- **Book 2 — IBM i** (*Mainframe 202*): three real operational-judgment scenarios (a held report, a job log, an MSGW job), light touch reframed as operational auditing/forensics rather than security tooling to avoid overlapping Nuts and Bolts' claimed territory. Built and verified live against the real mocks, seven sessions written (~5,800 words), amber cover art, packaged. Live on Gumroad.
- **Book 3 — z/OS** (*Mainframe 203*): a payroll job's "DATA SET NOT FOUND" message that reads like data loss but isn't, plus the already-built, book-unclaimed Dataset Recon Scanner (required new LISTCAT LEVEL(prefix) mock support, genuinely missing before this book) as the light security touch, "everyday hygiene," not RACF auditing. Built and verified live against the real mocks, six sessions written (~5,200 words), amber cover art, packaged. Live on Gumroad.
- **Book 4 — z/VM & z/TPF** (*Mainframe 204*): a z/VM device-conflict scenario that looks like a Book 201 repeat and isn't, plus z/TPF's already-built, book-unclaimed security tools panel (ECB Enumerator, Entry Point Prober, Pool Monitor, Privilege Scanner) reframed as Resource Containment & System Stability, lightest new-build lift of the series (zero new z/TPF mock code). Built and verified live against the real mocks, seven sessions written (~4,800 words), amber cover art, packaged. Live on Gumroad.
- **Book 5 — Capstone**: cross-platform incident correlating symptoms across all four mocks, mirrors the 100 series' capstone role but for diagnosis instead of a scripted chain.

**Length and voice**: each book targets at least 24 pages, longer than the leaner 100-series books; where more length is needed, real historical context (why a platform or failure mode exists the way it does) fills it out, in Britley's storyteller voice, not padding for padding's sake. **Cover art**: same structural template as the 100 series, a different accent color scheme so the two series read as related but visually distinct.

Working in Auto mode on this series per the user's direction (2026-08-21).

## Later / not yet scoped

- Gumroad API integration for automation (sales webhooks, emailing past buyers about new releases), not needed for launch, only becomes relevant once there's an actual buyer list to act on

Full implementation detail lives in the working plan from the session this was scaffolded in: `/Users/britleywrenhoff/.claude/plans/let-s-talk-through-and-parallel-cocke.md`.
