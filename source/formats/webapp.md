# Web app playbook

The kit builds apps, not just pages: a calculator, a booking or intake form, an interactive
simulator, a small internal tool, a dashboard over a data file. Same brand, same rules, same
publish loop as the site — read `source/brand/voice.md`, `design.md` and `tokens.css` first, like
for any output.

## Page or app?

Before creating an app, check the ladder:

- **It mostly displays content** (even interactive touches: a gallery filter, an accordion) → it's
  a **page or collection** on the site, per `source/formats/website.md`. Don't create an app.
- **It's a tool someone uses** (inputs → computation or flow → result: a simulator, a configurator,
  a multi-step form, a game) → it's an **app**, per this playbook.
- **It belongs to a different project or brand** → it's a **new repo**, not an app here (the
  `new-project` skill makes that call).

## Shape

One app = one self-contained folder at `apps/<slug>/` (see `apps/README.md`). Defaults, in order
of preference:

1. **A single static folder** — `index.html` + inline or co-located CSS/JS, no build step, no
   framework. Right for most tools; a single file someone could download and open still works.
2. **A small Astro app** (its own `package.json` inside `apps/<slug>/`) only when the app
   genuinely needs components, routing, or a build — don't reach for this by default.

Either way: colors, fonts, and spacing come from `source/brand/tokens.css` (copy the current
values into a token block at the top of the app's CSS, like the deck template does, so the app
stays self-contained); the voice guide applies to every label and message.

## Data and logic

- **Client-side by default.** Computation in the browser, data as a co-located JSON/CSV (or drawn
  from `source/content/collections/` when it's the same data the site uses — one source, two
  views).
- **No secrets, ever.** An API key in a static app is public. Anything needing a real backend,
  accounts, payments, or a database is a "needs a human decision" item, same ladder as the site's
  forms: propose the simplest option (a mailto, a Stripe link, a hosted form) and let the owner
  decide.
- The model that has served well: heavy simulation in a spreadsheet or data file in `source/`,
  the app as an interactive **view** of it — change the assumptions at the source, the app
  follows.

## Publishing

Two options, simplest first:

- **Under the site** — for an app that belongs to the same domain: build/copy it into
  `site/public/apps/<slug>/` so it ships with the site at `yourdomain.com/apps/<slug>/`. Zero
  extra hosting setup.
- **Its own Cloudflare Pages project** — for an app that wants its own URL or its own domain:
  a second Pages project **on the same repo**, with **Root directory: `apps/<slug>`** and
  production branch `main` (same gotchas as the site: the branch must exist, the root directory
  is the easy-to-miss field — `docs/deploy-cloudflare.md` and `docs/troubleshooting.md` apply).

## Quality bar

Same as the site: check it at ~390px and desktop, click everything, console clean, real alt text.
Plus, for a tool: try wrong and empty inputs — a calculator that NaNs on a blank field isn't done.

Record every app in `source/brief.md` under derivatives (what it is, where it lives, its URL).
