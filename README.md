# Portfolio — Mohamed Matroud

Personal portfolio for a Senior .NET Developer, built as a single self-contained HTML page.

**Live:** <https://mohamedmatroud.github.io>

---

## What it is

One `index.html` file. No build step, no framework, no package manager, no dependencies — all CSS,
JavaScript and the favicon are inlined. It renders identically from `file://`, offline, and from
GitHub Pages.

**The page makes zero network requests on load.** The only fetch that ever happens is the CV PDF,
and only when a visitor clicks Download.

## Notable bits

**Bilingual, English and Arabic.** A single dictionary drives the Arabic; English lives in the
markup and is snapshotted at load, so the two can't drift apart. Arabic switches the whole document
to RTL — layout mirroring is handled with CSS logical properties (`padding-inline-start`,
`border-inline-start`, `inset-inline-start`) rather than `[dir]` overrides, so it falls out of the
cascade almost for free. Arabic also zeroes `letter-spacing`, which otherwise breaks the cursive
joining between letters.

**Dark by default, with a light theme.** Colour values are declared once as `--d-*` / `--l-*` pairs
and mapped by a single block, so a colour is only ever written in one place. Every
foreground/surface pair in both themes clears WCAG AA at 4.5:1.

**Fourteen projects, paginated six per page**, grouped so the most recent work leads.

**A CSS-only 3D hero graphic** — a rotating isometric stack representing Clean Architecture layers,
leaning toward the cursor. Four nested transforms, no library.

**Progressive enhancement throughout.** Without JavaScript the page is fully readable: all content
visible, all fourteen projects rendered, the pager hidden rather than leaving cards trapped behind a
control that can't work. Animations are decoration and never gate visibility — each has a fallback
that restores the finished state if its animation never runs.

**Accessibility.** Skip link, semantic landmarks, `aria-current` on pagination, live-region
announcements on page change, keyboard-reachable controls, and full `prefers-reduced-motion`
support that stops all motion while keeping everything visible.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire site |
| `Mohamed_Matroud_CV.pdf` | Served by the Download CV button |
| `.nojekyll` | Skips Jekyll processing on GitHub Pages |

## Running it locally

Open `index.html` in a browser. That's all — there is nothing to install or compile.

The clipboard button on the contact section falls back to `execCommand` when opened over `file://`,
since the async Clipboard API is restricted to secure contexts.

To serve it over HTTP instead:

```bash
npx serve .
```

## Deploying

The repository is named `<username>.github.io`, so GitHub Pages publishes it from the default
branch automatically. No workflow file and no Pages configuration are required.
