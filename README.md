# Books

Direct ebook sales page, linking out to Gumroad for checkout, meant to sit alongside [britleyhoffconsulting.com](https://britleyhoffconsulting.com) as a lower-fee alternative to selling only through Apple Books.

Live at [books.britleyhoffconsulting.com](https://books.britleyhoffconsulting.com). `index.html` renders a card grid from `data/books.js`. To add a new title, drop a `books/<slug>.yaml` + cover image into place and it gets folded into `data/books.js` and `assets/books/`. Every title carries a `category` (one of Mainframe Training, Mainframe Security, AI & Infrastructure, Industrial (ICS/OT), Bundles) and an `added` date. The page uses them for the filter pills and a New badge on anything added in the last 7 days, and a search box matches titles first, then summaries. The grid order in `data/books.js` is curated, not sorted. See [ROADMAP.md](ROADMAP.md) for the why and what's next.
