# lavalink-list — Project Documentation

> Complete 5-page engineering documentation. Part of the Alivelyyy coding-history dossier (generated 2026-10-18).

## lavalink-list

> *His copy of the community's canonical catalog of free public Lavalink nodes — the MkDocs–Material site behind `lavalink.darrennathanael.com` that A L I V E's own Lavalink hosting (and his Lavalink-Monitor project) participates in. A public fork/curated mirror of DarrenOfficial/lavalink-list: an SSL/NonSSL node directory, a REST API of machine-readable node entries, and per-node status badges — kept fully buildable locally with MkDocs.*

| Fact | Value |
|---|---|
| GitHub URL | https://github.com/Alivelyyy/lavalink-list |
| Visibility | Public |
| Created / last pushed | 2026-04-08 → 2026-04-20 |
| Primary language | HTML |
| All languages | HTML (per GitHub Linguist) — by file count the snapshot is heavier on Markdown (8 files), XML (6: sitemap, JetBrains), plus YML/TXT; real prose lives in `docs/*.md` with heavy inline-HTML blocks |
| Total files | 27 (in the shallow 50-commit snapshot; the upstream repo is far larger at ~800 PRs) |
| Total commits | 50 visible in the local shallow clone (2025-09-07 → 2026-03-23); the GitHub fork tracks upstream DarrenOfficial/lavalink-list history — none of the visible 50 commits are authored by A L I V E |
| Live site | Upstream: https://lavalink.darrennathanael.com (README also markets https://lavalink-list.darrennathanael.com) — hosted on Cloudflare Pages per the FAQ |
| Category | Community-maintained documentation site / curated directory (Lavalink node list) |

### 📄 Page 1 — Overview & Purpose

#### What the project is

`lavalink-list` is the community's central registry of **free, public Lavalink audio nodes** — the standalone Java audio servers that Discord music bots route their streams through so audio never touches the bot's shards. The upstream project (`DarrenOfficial/lavalink-list`) is a MkDocs–Material site with:

- a **"Lavalink with SSL"** page (`docs/SSL/Lavalink-SSL.md`) — `secure: true` nodes,
- a **"Lavalink without SSL"** page (`docs/NoSSL/Lavalink-NonSSL.md`) — plain-WS nodes,
- an **FAQ** (`docs/FAQ/frequently-asked-questions.md`),
- a **REST API & Badges** page (`docs/rest-api-badges.md`) documenting the machine-readable list endpoint and per-node stat badges,
- and a **PR-driven contribution model** — anyone hosting a node opens a PR to add themselves; anything offline for 7 days can be PR-removed.

A L I V E's repo is a **public GitHub fork/clone** of that catalog (created 2026-04-08, last pushed 2026-04-20, 1 star on the snapshot). All content, README, mkdocs config, GPL-3.0 license, and the visible gitlog are inherited from upstream contributors; his participation is in the *ecosystem*: he runs his own `node.vyrix.xyz` Lavalink node (monitored by his private Lavalink-Monitor repo) and consumes the exact REST API + badge conventions this list defines — `https://lavalink-list-api.ajieblogs.eu.org/<unique-id>/badge/<Players|Status|Load>` — with his own in-repo badge generator of the same shape.

#### The user-facing README, quoted

The clone's `README.md` is the upstream pitch verbatim:

```
Lavalink List

For quality control I checked on these servers per weekly basis, if the
lavalink is offline / unreachable / zero uptime it will be removed.

<Open Website »> — lavalink-list.darrennathanael.com
Create PR · Report Bug · Request Feature · Status Page
```

plus a candid FAQ entry — *"Why spring logo? Because lavalink is based off spring."* — a contributors image, and *"If you find this useful give it a star ⭐️"*.

#### Problem it solves, and intended users

- **Client-bot developers** who need to *find free nodes fast* — pick SSL vs NonSSL based on whether their client is configured for `secure: true`, then copy a 4-line `Host/Port/Password/Secure` block.
- **Hosters** who want discoverability for their free nodes (a PR template exists in the FAQ).
- **Scraper authors** — explicitly told to *not scrape* (the physical marker files `docs/NoSSL/DO NOT SCRAPE THE FILE, PLEASE USE THE API INSTEAD!` and its SSL twin) and instead consume the JSON list API; the rationale is documented: *"we have received reports of abusive activity … likely using invalid regex … please use the valid REST API instead"* (`docs/rest-api-badges.md`).
- **A L I V E himself** — as an ecosystem participant: he hosts his own node (`Vyrix-US-1` @ `node.vyrix.xyz:8002` per his monitor's `src/config.js`) and builds his own status/badge stack in the private Lavalink-Monitor, deliberately mirroring this list's conventions.

#### What makes it notable as a portfolio item

It shows engagement with **open-source community infrastructure**, not only his own private products. The snapshot's gitlog is a 100%-community artifact — 11+ distinct contributing identities (AneFaiz, Kirito/Arthur Dos Santos Sousa, IamnotJamesBG, Ajie Genrald, southctrl/AV, Tapao, Jirayu, G3V/Archie Williams, Kartik, MaliCk Saad, sakura, urfavteddybear, Bernard) — and it documents, through `docs/`, the entire lifecycle of community node hosting: launches, EOLs (`"JM Lite LAVALINK V2 (EOL)"`, `"dead lavalink"`), password hygiene changes (`"Cleanup & Update password"`), and version migrations (`"Updated youtube plugin & lavalink itself"`).

#### Notable upstream evolution visible in the gitlog

Selected newest-first lines (2025-09-07 → 2026-03-23):

```
2026-03-23 delete inactive nodes, fix missing close on code block (#808)   — Ajie Genrald
2026-03-23 Update Lavalink-NonSSL.md with VexaNode details (#807)
2026-03-17 Hosted a Free Lavalink by NexCloud Hostings (#805)              — ᴋᴀʀᴛɪᴋ
2026-03-11 Ganti IP host mas (#802)                                        — AneFaiz
2026-03-07 Cleanup & Update password (#800)                                — Ajie Genrald
2026-01-09 added new host (#782)
2025-12-03 badges + ssl lavalink (#755)
2025-10-18 add website (#746)                                              — Jirayu
2025-09-20 Updated youtube plugin & lavalink itself (#739)
2025-09-28 JM Lite LAVALINK V2 (EOL) (#741)
2025-09-08 dead lavalink (#729)
```

The `#PR`s climb #728 → #808 across the 50-commit window — evidence of a very active, PR-driven project (hundreds of entries over time) and of a strict "one entry per hoster" doc rhythm.

### 📄 Page 2 — Technology Stack & Architecture

#### Build stack (mkdocs, Python — verified against the clone's `requirements.txt`)

```
# Requirements for core
jinja2, markdown, mkdocs, mkdocs-material, pygments,
pymdown-extensions, markdown-meta-extension

# Requirements for plugins
babel, colorama, paginate, regex,
mkdocs-git-authors-plugin,
mkdocs-git-revision-date-localized-plugin,
mkdocs-minify-plugin,
pymdown-extensions
```

- Docs engine: **MkDocs + mkdocs-material** (no builder beyond that; renders `docs/` → `site/`).
- **Three git-aware plugins** are enabled in `mkdocs.yml` — `git-authors`, `git-revision-date-localized(enable_creation_date: true)`, and `minify(minify_html: true)` — so each deployed page shows per-page authorship and revision dates pulled from repository history.
- A custom theme override dir (`overrides/`) holds Jinja2 template `overrides/main.html` extending `base.html`: it injects **Microsoft Clarity** (script id `nbw4ysvvn3`) — prefaced by the maintainer's comment *"<!-- Microsoft forced me to use this or something -->"* — loads **Bunny fonts** (`fonts.bunny.net`, JetBrains Mono) plus a self-hosted font gateway (`lore.dpaste.org/g-fonts/gateway-primary-font.css`), and sets `--md-text-font: "Gotham SSm A"/"Gotham SSm B"` with `--md-code-font: 'JetBrains Mono'` (preceded by an embedded prose-western comment: *"I open my eyes and it's November, And I am in a freight elevator. …"*).

#### Site configuration (`mkdocs.yml`, essentials)

| Field | Value |
|---|---|
| `site_name` | `lavalink hosting` |
| `site_author` | `DarrenOfficial` |
| `site_url` | `https://lavalink.darrennathanael.com` |
| `site_description` | "List of free lavalink servers! If you have lavalink that you can share feel free to make a pull request! Lavalink is a standalone audio sending node based on Lavaplayer and JDA-Audio. Allows for sending audio without it ever reaching any of your shards." |
| `repo_url` / `edit_uri` | `github.com/DarrenOfficial/lavalink-list` / `.../edit/main/docs` |
| theme | `name: material`, `palette: primary: black, accent: deep orange, scheme: slate`, logo `https://ajie.is-a.dev/cdn/img/spring-logo.svg`, favicon `spring.ico` |
| nav | Home → SSL → NoSSL → FAQs → Rest API & Badges |
| features | `tabs`, `instantsite`, `content.code.annotate`, `navigation.tracking/expand/indexes/instant/sections/tabs/top`, `search.highlight`, `search.suggest`, `footnotes`, `def_list` |
| markdown_extensions | `meta`, `admonition`, `pymdownx.details/superfences/tabbed/keys`, `attr_list`, `footnotes`, `pymdownx.betterem` (smart_enable: all) |
| plugins | `search`, `tags`, `git-authors`, `git-revision-date-localized`, `minify(mkdocs-minify-plugin)` |
| extras | socials (Darren's Twitter/GitHub/Discord icons), `generator: false`, copyright "Darren Nathanael" |

#### Build/local-run commands

```bash
pip install -r requirements.txt
mkdocs serve        # dev preview at localhost:8000
mkdocs build        # static output → site/
```

#### Repository hygiene artifacts in the clone

- `.gitignore`, `.yarnrc.yml` (1-line repo marker), `.yarn/install-state.gz` — upstream experiments with Yarn tooling.
- `.idea/` directory (6 JetBrains files: `misc.xml`, `modules.xml`, `discord.xml`, `vcs.xml`, `lavalink-list.iml`, `inspectionProfiles/profiles_settings.xml`) — the maintainer works in a JetBrains IDE.
- `docs/robots.txt` + `docs/sitemap.xml` for crawler control — consistent with the anti-scraping stance of the API page.
- `LICENSE` = **GNU GPL v3** (full 674-line text), `CODE_OF_CONDUCT.md` (93 lines), `CONTRIBUTING.md` (a strict 4-bullet rule set, see Page 4).
- Marker files literally named `docs/SSL/DO NOT SCRAPE THE FILE, PLEASE USE THE API INSTEAD!` and the NoSSL twin.
- A stray `.cache` file (no extension) and `.yarn/install-state.gz` sit at the repo root — lock/artifact residue.

#### Language weighting note

GitHub Linguist reads this repo as HTML because `overrides/main.html` is Jinja2+HTML and `sitemap.xml` counts as markup; by prose volume the content layer is Markdown — `docs/index.md` carries inline `<h1>`s and `{ .md-button }` chip CTAs, the node pages use `???+ danger` admonitions and fenced connection blocks.

### 📄 Page 3 — Features & Functionality (Feature-by-Feature)

#### Site navigation & content map

| Route (from `nav`) | Content |
|---|---|
| `/` | Landing: Gotham-SSm-A display title, PR/Report/Feature/Contributors pills, `.md-button` CTAs to SSL / NoSSL / FAQs / Rest API & Badges, an "Info" explainer of the SSL split (*"SSL one needed `”secure”` to be set to true at client side, whilst the one without SSL should just works."*), a hosting guide link (`darrennathanael.com/post/how-to-lavalink/`), an EthicalAds image slot, and the commented-out TunnelBroker guide (*"Temporary removal due isnt work anymore, tunnelbroker flagged"*) |
| `SSL/Lavalink-SSL/` | Directory of `Secure: true` nodes |
| `NoSSL/Lavalink-NonSSL/` | Directory of plain-WS free nodes |
| `FAQ/` | What Lavalink is, identifier rules, dead-node policy, ads, hosting guide, Cloudflare Pages, PR template |
| `/rest-api-badges` | Scrape-ban rationale + REST API spec (SSL/NonSSL/All) + badge URL format |

Every content page shares: the `???+ danger "v4 is not backwards compatible with v3."` admonition ("You must update your bot library to support v4!"), a `<!-- PLEASE READ -->` comment block (new entries at the bottom; don't scrape; ads contact `ads@darrennathanael.com`), and an EthicalAds `<div data-ea-publisher="darrennathanaelcom" data-ea-type="image">` slot.

#### Real directory entries — what a "hosting record" looks like

Snapshot of `docs/SSL/Lavalink-SSL.md`:

| Hosted by | node | Port | Password field | Extras on record |
|---|---|---|---|---|
| Amane & AjieDev | `lavalinkv4.serenetia.com` | 443 | `"https://seretia.link/discord"` (support-server URL as secret) | Version 4.x; badges `ajieblogs.eu.org/lavalink/v4/badge/<Status\|Uptime\|Players>` |
| Jirayu | `lavalink.jirayu.net` | 443 | `"youshallnotpass"` | v4.0.8, salee-plugin (Proxy); badges `…/lavalink-jirayu-net-443/badge/<Status\|Load\|Players>` |
| AneFaiz | `lava-v4.millohost.my.id` | 443 | `"https://discord.gg/mjS5J2K3ep"` | status page link `lavalink.millohost.my.id` |
| TriniumHost | `lavalink-v4.triniumhost.com` + `lavalink-v3.…` | 443 | `"free"` | v4.x.x and v3.x.x listed side by side with own status-API badges |

Snapshot of `docs/NoSSL/Lavalink-NonSSL.md`:

| Hosted by | node | Port | Password field | Notes |
|---|---|---|---|---|
| Jirayu | `lavalink.jirayu.net` | 13592 | `"youshallnotpass"` | v4.0.8, salee-plugin |
| Amane & AjieDev | `lavalinkv4.serenetia.com` | 80 | `"https://seretia.link/discord"` | v4.x |
| Tapao (Nyxbot) | `sg1-nodelink.nyxbot.app`, `sg2-nodelink.nyxbot.app` | 3000 | `nyxbot.app/support` | Nodelink (lavalink-compatible); YouTube/Spotify/Apple Music/Deezer/Twitch sources |
| G3V | `lava.g3v.co.uk` | 9008 | `"lavalinklol"` | v4.2.1, youtube-plugin + lavasrc-plugin, quality tuning (opusEncodingQuality=10, resamplingQuality HIGH) |
| TriniumHost | `lavalink.triniumhost.com` | 4333 / 2334 | `"free"` | v4 & v3 |
| Kartik | `n3.nexcloud.in` | 2026 | `"nexcloud"` | v4.2.1, full source list |
| VexaNode | `omega.vexanode.cloud` | 2031 | `"https://discord.vexanode.cloud"` | v4.x, Miami US node |

The consistent **"password = support-server invite URL"** convention lets hosters rotate their URL as the actual secret while keeping self-serve access through Discord.

#### REST API & Badges (documented by the list, consumed by his ecosystem)

- JSON list endpoints (refreshed every 10 minutes, offline nodes pruned): `https://lavalink-list.ajieblogs.eu.org/SSL`, `.../NonSSL`, `.../All`; object shape `{"unique-id", "identifier", "host", "port", "password", "secure", "version"}` (e.g. `lavalinkv3-id-serenetia-com-80`).
- Badge endpoint: `https://lavalink-list-api.ajieblogs.eu.org/<unique-id>/badge/<type>` with `type ∈ {Players, Status, Load}`.
- His private Lavalink-Monitor re-implements this exact badge family (`badge/status|players|uptime` SVGs through `src/web/utils/BadgeGenerator.js`) so his node badge URLs sit natively next to these.

#### Community process features (FAQ + CONTRIBUTING + CoC)

- **Weekly quality control** — README states hosts are checked weekly: *"if the lavalink is offline / unreachable / zero uptime it will be removed."*
- **Dead-node policy** — *"if the server has been down for 7 days you can make a Pull Request removing the server completely."*
- **PR template** — exact block: `### Hosted by @ [Your Name Here](https://example.com)` + `Version ?.? / extra info` + a `Host/Port/Password/Secure` bash block; status badges optional; advertising separate via `ads@darrennathanael.com`.
- **Identifier rule** — *"Put it as anything, it doesn't matter as long as it's one sentence and there's no `'`."*
- **Monetization transparency** — ads at *"pricing starts at 2$ per day"*, with traffic disclosure *"This site gets 120+ average visits per day"*; site hosted on **Cloudflare Pages**.
- **Support** — Discord invite (`discord.darrennathanael.com` in socials; `discord.gg/CFbwj7YCPb` on the API page).

### 📄 Page 4 — Code Internals & Systems Design

#### What "systems design" means in a docs repo — repository-as-database

1. `docs/SSL/Lavalink-SSL.md` and `docs/NoSSL/Lavalink-NonSSL.md` are the canonical node records: one `###` section per host, new entries go at the bottom ("SUPPORT OTHER CONTRIBUTORS BY PLACING THE NEW LAVALINK AT THE VERY BOTTOM OF THE OTHERS!").
2. Each record follows a strict schema: hoster title + Discord-ref link → optional metadata (version, plugins, sources) → optional badge `<img>` URLs → one fenced `bash` connection block.
3. Consumers never parse these files: the REST API mirrors them with stable `unique-id`s derived from host-port (`lava-v4-ajieblogs-eu-org-80`), refreshed every 10 minutes. That decouples doc churn from clients — which is *why* scraping is banned in favor of the API.
4. Build-time arch: MkDocs renders Markdown via `pymdownx.superfences/tabbed/details`; `mkdocs-git-authors-plugin` computes per-page authors from git history; `git-revision-date-localized` stamps creation dates; `mkdocs-minify-plugin` shrinks HTML — *repository metadata itself becomes page columns*.
5. `overrides/main.html` (Jinja2 layer) wraps every page for fonts + Clarity analytics injection; ordering matters because `extrahead` extends the Material `base.html` block.

#### Anti-scraping design

- Physical blocker files at `docs/{SSL,NoSSL}/DO NOT SCRAPE THE FILE, PLEASE USE THE API INSTEAD!`.
- `robots.txt`/`sitemap.xml` tuned for the intended crawler persona (search engines only).
- API-first messaging with the abusive-traffic explanation quoted on the API page.
- Badges stay same-origin and cache-friendly, with colored fallback states (`Error / Invalid node` label `#DA644D`; offline-as-`N/A`) — the JSON annex wraps `schemaVersion 1` payload style.

#### Upstream contribution rules

`CONTRIBUTING.md` in its entirety:

```
- Write in camelCase, not snake_case.
- Make sure your lavalink is accessible via public. you can test this by doing `dig @1.1.1.1 example.com`
- Do not push to master/main without testing your changes first, make a branch if you have to.
```

- `dig @1.1.1.1 example.com` is a real public-DNS accessibility test against Cloudflare's resolver.
- camelCase keeps doc keys and API `unique-id` fields predictable.
- Branch-before-push keeps the git-authors page stats clean.
- Plus a 93-line `CODE_OF_CONDUCT.md` and the GPL-3.0 `LICENSE` — a full community-governance kit inherited intact.

#### How the author actually used it (snapshot analysis)

- He kept the repo cloned shallow (depth 50), latest-state as of 2026-03/04 — a local copy a node-runner would keep for Ctrl+F lookups (passwords live in plain doc text) and for style-matching his own status page.
- His own node is absent from this snapshot's docs (no `vyrix.xyz` entries in `SSL/NonSSL` files) — he participates from the consumer side: his node's public GitHub-described homepage field still points at `https://lavalink.darrennathanael.com/`, and his monitor/badge stack clones the list's URL/lookup idioms (`/badge/<Type>`) exactly.
- The 12-day fork window (2026-04-08 → 2026-04-20) overlaps his `Lavalink-Monitor` SEO/branding commit era (`Update branding and theme to Vyrix…`, `Improve website SEO…`) — one coherent Lavalink-infrastructure work-stream across a public and a private repo.

#### How to build it (concrete)

```bash
git clone https://github.com/Alivelyyy/lavalink-list && cd lavalink-list
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
mkdocs serve    # local render: Home, SSL, NoSSL, FAQ, API & badges
mkdocs build    # → static site/ (upstream deploys this to Cloudflare Pages)
```

### 📄 Page 5 — Development Timeline, Skills & Resume Highlights

#### Timeline narrative (a "timeline of a fork")

- **2025-09-07 → 2026-03-23 — community record visible in the snapshot:** 50 merged upstream PRs (#728 → #808) showing the full lifecycle of community nodes: new hosts (`"added lavalink (#799)"`, `"Hosted a Free Lavalink by NexCloud Hostings (#805)"`), credential rotation (`"Cleanup & Update password (#800)"`, `"Update Lavalink host and secure settings (#772)"`), deaths (`"dead lavalink (#729)"`, `"JM Lite LAVALINK V2 (EOL) (#741)"`), infrastructure (`"add website (#746)"`, `"badges + ssl lavalink (#755)"`, `"Updated youtube plugin & lavalink itself (#739)"`).
- **2026-04-08 — fork creation.** A L I V E creates `Alivelyyy/lavalink-list` (public, ~1 star).
- **2026-04-08 → 2026-04-20 — his activity window:** 12 days of syncing/publishing while he simultaneously ships his `Lavalink-Monitor` branding/SEO era and runs his Vyrix hosting identity.
- **2026-04-20 — last push.** Lavalink work then continues in private repos (Lavalink-Monitor receives commits through 2026-05-26).

#### Attribution honesty (a dossier must-have)

- **None of the 50 visible commits are his** — all authors are upstream community members (AneFaiz ×10, Kirito/KiritoGamesPlays ×7, IamnotJamesBG ×5, Ajie Genrald ×4, AV/southctrl ×4, Jirayu ×2, Tapao ×2, plus G3V, Bernie, Kartik, MaliCk Saad, sakura, urfavteddybear, Jirayu, Charles Giann Marcelo); every email is `@users.noreply.github.com` or a personal domain, none `aliveisalive8354@gmail.com`.
- The accurate resume framing: **"maintains a public fork of and participates in the lavalink.darrennathanael.com node ecosystem"** — supported by his own hosting node, his monitor/badge implementation parity, and homepage metadata — rather than claiming upstream authorship of entries.

#### Skills demonstrated

- **Open-source literacy** — adopting, tracking, and building against a live community project; sourcing exact deps from `requirements.txt`; understanding MkDocs-material's plugin chain (git-authors / git-revision-date-localized / minify); keeping a fork buildable locally.
- **Docs-as-data thinking** — recognizing the real "system" as git-versioned host records with stable `unique-id`s and a REST mirror; consuming an API instead of scraping by explicit ecosystem convention.
- **Protocol knowledge** — `secure: true` (wss) vs plain-WS clients, v3→v4 breaking-change awareness, plugin ecosystems (youtube-plugin, lavasrc, salee-proxy, Nodelink) and the "password-as-invite-URL" secret-rotation pattern.
- **CDN-hosted docs sites** — Cloudflare Pages deployment awareness + EthicalAds monetization model of the upstream project.
- **Docs hygiene** — branch-before-push, camelCase content rules, DNS accessibility verification (`dig @1.1.1.1`), LICENSE/CoC/CONTRIBUTING completeness.

#### Resume-ready bullet points

- Maintains a public GitHub fork of **DarrenOfficial/lavalink-list**, the community-curated directory of free public Lavalink audio nodes (MkDocs–Material, GPL-3.0, ~800 community PRs upstream), kept locally buildable with `mkdocs serve`/`mkdocs build`.
- Studied and mirrored the project's **REST API + status badge conventions** (`/All|SSL|NonSSL` JSON list refreshed every 10 minutes; `<unique-id>/badge/<Players|Status|Load>` endpoints) — and re-implemented an equivalent badge generator for his own private node-monitoring service.
- Operates a Lavalink node of his own (`node.vyrix.xyz`, identifier `Vyrix-US-1`) within the same discovery/health-check ecosystem this list standardizes: weekly liveness checks, API snapshots, and a 7-day dead-node removal policy.
- Comprehensively cataloged the ecosystem opts-in patterns — SSL vs NonSSL (`ws`/`wss` + `secure`) matrix, v3/v4 compatibility warnings, plugin/sourcing disclosure (YouTube/Spotify/Apple Music/Deezer/Twitch), and the "password = support-server URL" self-serve secret strategy — from upstream content.
- Practices community fork hygiene: branch discipline, camelCase doc rules, DNS accessibility checks (`dig @1.1.1.1 example.com`), and GPL-3.0 + Contributor Covenant reuse intact from upstream.

#### Limitations, honest scope, and maturity

- **Scope:** a (shallow, 50-commit) mirror of a 27-file docs repo — no code authored by him in the visible snapshot. It evidences *ecosystem participation, API consumption, and upkeep of a related private service*, not original development.
- **Maintenance window:** short (12 days of pushes in 2026-04); the fork went dormant after as his Lavalink work moved into private repos.
- **Consistency realities:** the fork carries upstream's origin everywhere (`mkdocs.yml` `repo_url`/`edit_uri` → DarrenOfficial, README links, GPL-3.0 license), so presenting it as his own product would be false; presenting it as a curated mirror + ecosystem participation is accurate.
- **Snapshot quirks:** Jetbrains `.idea/` files and Yarn install state sit in-tree; the `.cache` artifact and single-commit marker (`docs/…` edits) show a working-directory, not a release artifact.
- **Maturity:** snapshot-level; its dossier value is *context* — it explains the design targets of his Lavalink-Monitor badge API (`/api/v1/badge/status|players|uptime`), the "live stats" DNA of his node dashboard with an in-repo shields-style SVG generator, and why his hosting model (free node, support-URL password) matches community best practice.
