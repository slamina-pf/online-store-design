# Changelog

All notable changes to these design mockups are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/);
versions follow [Semantic Versioning](https://semver.org/).

## [0.3.0] - 2026-09-29

### Added
- Collections Create/Edit view (`POST`/`PATCH /collections`): title, slug,
  description form, matching the Products Create/Edit pattern. "Add
  collection" and "Edit collection" previously did nothing
  (`data-action="noop"`) — both now navigate here and Save actually adds
  the collection and returns to the list with a confirmation toast.
- "Save product" is now wired up too (it was equally dead before) — adds
  the product and returns to the Products list with a toast, for
  consistency with the newly-fixed collection flow.

### Changed
- Layout is now full-width: `.content` no longer caps at `1040px`, so the
  sidebar and every table/card stretch to fill the page. `html`/`body`
  get an explicit `height: 100%` so the sidebar's full-height styling
  actually resolves against the viewport instead of a collapsed parent.
- Create/Edit forms (Products, Collections) are capped at a readable
  `640px` via a new `.form-card` wrapper, since a form's inputs — unlike
  tables — don't benefit from stretching edge-to-edge on a wide screen.

## [0.2.0] - 2026-09-29

### Added
- Product Detail's Options, Variants, and Images tabs are now fully
  editable in place: "+ Add" reveals an inline form row, each row gets
  Edit/Delete actions, and Save/Cancel commit or discard changes — matching
  the real `POST`/`PATCH`/`DELETE` sub-resource endpoints under
  `/products/{id}/options`, `/variants`, and `/images`.
- Images can be uploaded for real via a file picker (`FileReader` +
  `data:` URLs, since external image hotlinking isn't reachable under the
  Artifact's CSP), with an editable alt-text caption and a remove button
  per image.
- Products List and Collections List now share a real pagination control:
  rows-per-page (10/25/50), numbered pages, first/prev/next/last, and a
  jump-to-page input. The Products dataset was expanded from 6 to 22 items
  across 4 vendors so paging is genuinely functional, not just decorative.

### Fixed
- Dropdown/row-action menus (`.menu-panel`) showed browser-default bullet
  points and indentation outside the menu card — missing `list-style`/
  `margin` reset on the underlying `<ul>`.
- Opening a row's action menu on the last row of a table added an
  unwanted vertical scrollbar and grew the table — caused by a CSS
  overflow quirk (`.table-scroll` set only `overflow-x: auto`, which
  forces the other axis to compute as `auto` too). Menus are now
  `position: fixed` and positioned in JS from the trigger's own bounding
  box, so they can no longer be clipped by, or expand, a scrolling
  ancestor, and they flip upward automatically when there isn't room
  below.

## [0.1.0] - 2026-09-29

### Added
- Initial mockup covering the two resources with real endpoints in
  `online-store-api` today: **Products** and **Collections**.
- Views: Products List, Products Create/Edit, Products Detail
  (Info/Options/Variants/Images tabs), Collections List, Collections Detail.
- Reuses the `projects-story-book` visual language: Button, Alert, Badge,
  Breadcrumb, Dropdown, ButtonClose (same colors/treatment, hand-compiled to
  plain CSS since the artifact can't import the private npm package).
- New UI patterns not yet in `projects-story-book`, designed here first:
  data table, form inputs, pagination, tabs, image thumbnail gallery. These
  are candidates for the component library's next additions.
- Published as a Claude Artifact: https://claude.ai/artifact/QVRfCTRiCrg98gKyhyzaDo
