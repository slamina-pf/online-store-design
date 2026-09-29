# store-online-design

UI mockups for the `store-online` project — one step upstream of
`projects-story-book` (the component library) and `online-store-api` (the
backend). This is where new screens get designed and reviewed *before* the
components they need get built into the library.

## What's here

`views/index.html` is a single, click-through mockup covering every view
that corresponds to a **real, currently-implemented** endpoint in
`online-store-api`:

- Products — List, Create/Edit, Detail (Info/Options/Variants/Images)
- Collections — List, Detail

It is also published as a Claude Artifact for easy sharing/review:
https://claude.ai/artifact/QVRfCTRiCrg98gKyhyzaDo

Cart, Checkout, Orders, and Customer/Login views are intentionally **not**
included yet — those endpoints don't exist in `online-store-api` yet either
(DB models only, per its README roadmap). They'll get their own mockup once
the corresponding endpoints ship.

## Design principle: the mockup leads, the library follows

Wherever a view needs a component that already exists in
`projects-story-book` (Button, Alert, Badge, Breadcrumb, Dropdown,
ButtonClose), this mockup reuses that exact visual treatment (colors,
spacing, states) so it stays consistent with the real, shipped components.

But the mockup is **not limited** to what the library already has. Where a
view needs something new, it gets designed here anyway, in the same visual
language, and flagged below as a candidate for the library. The design
should drive what gets built next, not the other way around.

**New components identified in this pass (not yet in `projects-story-book`):**
- Data table (sortable list rows)
- Form inputs (text, textarea, select)
- Pagination controls
- Tabs
- Image thumbnail/gallery grid

## Viewing it

Open `views/index.html` directly in a browser — it's a static file, no
server or build step needed. Or open the published Artifact link above.

## Versioning

This folder is its own git repository, versioned independently of
`online-store-api` and `projects-story-book`, using
[Semantic Versioning](https://semver.org/) via git tags:

- **Patch** (`0.1.x`) — visual tweaks, copy changes, bug fixes to the mockup.
- **Minor** (`0.x.0`) — a new view added (e.g. once Cart/Checkout endpoints
  exist), or a meaningfully restructured existing view.
- **Major** (`x.0.0`) — a full visual/IA redesign of the whole mockup set.

`package.json` has no dependencies and is never published to a registry —
it exists only so `npm version patch|minor|major` can be used as the
bump-and-tag command, the same release mechanic `projects-story-book` uses:

```sh
npm version patch   # or minor / major
git push --follow-tags   # once a remote is added
```

Every version bump should also get a corresponding entry in
[`CHANGELOG.md`](./CHANGELOG.md).
