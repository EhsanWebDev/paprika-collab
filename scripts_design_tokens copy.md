# Scripts — Design Tokens (quick reference)

Brief token cheat-sheet for the Scripts pages (`src/features/scripts/`). All
values are Tailwind utilities consuming the shared CSS-variable design tokens —
**no hardcoded hex** in component files.

## Color tokens

Values are CSS variables in [`src/styles/globals.css`](../../src/styles/globals.css),
stored as HSL component triples (`H S% L%`). Hex is the resolved approximation.

| Role                | Token classes               | Light HSL / hex           | Dark HSL / hex            |
| ---------------------| -----------------------------| ---------------------------| ---------------------------|
| Primary text        | `text-foreground`           | `240 5% 10%` · `#18181b`  | `220 8% 92%` · `#e8eaed`  |
| Secondary text      | `text-muted-foreground`     | `240 4% 44%` · `#6b6b75`  | `240 4% 65%` · `#a3a3ad`  |
| Faint dividers/sep  | `text-muted-foreground/50`  | ↑ at 50% alpha            | ↑ at 50% alpha            |
| Surface / canvas    | `bg-background`             | `0 0% 100%` · `#ffffff`   | `30 3% 11%` · `#1d1c1a`   |
| Row hover           | `hover:bg-muted/40`         | `30 5% 96%` · `#f6f5f4`   | `30 3% 8%` · `#151413`    |
| Borders             | `border-border`, `border-b` | `30 6% 91%` · `#e9e8e7`   | `220 11% 22%` · `#323742` |
| Primary (paprika)   | `bg-primary`                | `17 88% 40%` · `#c2410c`  | `17 88% 52%` · `#ed6726`  |
| Error / destructive | `text-destructive`          | `0 84% 60%` · `#ef4444`   | `0 75% 60%` · `#e74c4c`   |
| Success (fg)        | `text-success`              | `142 72% 29%` · `#157f3c` | `96 27% 69%` · `#a7c794`  |
| Warning (fg)        | `text-warning`              | `28 92% 37%` · `#b55908`  | `38 92% 65%` · `#f6b94f`  |
| Info (fg)           | `text-info`                 | `224 76% 48%` · `#1d4fd7` | `213 32% 69%` · `#9fb3cb` |

Semantic surface/border companions (used by runtime badges):

| Token                   | Light HSL / hex            | Dark HSL / hex            |
| -------------------------| ----------------------------| ---------------------------|
| `bg-success-bg`         | `138 76% 97%` · `#eefbf2`  | `105 19% 12%` · `#19251a` |
| `border-success-border` | `142 50% 85%` · `#c5ecd3`  | `105 20% 27%` · `#37522e` |
| `bg-warning-bg`         | `48 100% 96%` · `#fffaeb`  | `38 50% 12%` · `#2e2310`  |
| `border-warning-border` | `38 92% 80%` · `#fad79a`   | `38 50% 22%` · `#54401d`  |
| `bg-info-bg`            | `214 100% 97%` · `#ebf3ff` | `213 21% 13%` · `#1a2029` |
| `border-info-border`    | `214 70% 88%` · `#c5dbf5`  | `213 26% 29%` · `#37485d` |

### Test-status colors (`STATUS_META`)

| Status     | Color                   | Icon          |
| ---------- | ----------------------- | ------------- |
| `success`  | `text-success`          | CheckCircle2  |
| `failed`   | `text-destructive`      | XCircle       |
| `warning`  | `text-warning`          | AlertTriangle |
| `untested` | `text-muted-foreground` | CircleDashed  |

### Runtime badges (`RUNTIME_BADGE_CLASSES`)

`Badge variant="outline"` + per-runtime classes. Python/JS/TS use the semantic
tokens above; Bash/PowerShell use raw Tailwind palette steps (hex shown):

- **Python / TypeScript** — `border-info-border bg-info-bg text-info`
- **JavaScript** — `border-warning-border bg-warning-bg text-warning`
- **Bash** — slate: `bg-slate-50 #f8fafc` · `border-slate-200 #e2e8f0` ·
  `text-slate-700 #334155` (dark: `bg-slate-900 #0f172a` ·
  `border-slate-800 #1e293b` · `text-slate-300 #cbd5e1`)
- **PowerShell** — indigo: `bg-indigo-50 #eef2ff` · `border-indigo-200 #c7d2fe` ·
  `text-indigo-700 #4338ca` (dark: `bg-indigo-950 #1e1b4b` ·
  `border-indigo-900 #312e81` · `text-indigo-300 #a5b4fc`)

## Typography

| Use                 | Classes                                            |
| ---------------------| ----------------------------------------------------|
| Detail page H1      | `text-[18px] font-semibold leading-tight`          |
| Breadcrumb          | `text-[12px] leading-none text-muted-foreground`   |
| Body / cell text    | `text-sm`                                          |
| Cell name           | `text-sm font-medium`                              |
| Secondary cell text | `text-xs text-muted-foreground`                    |
| Column headers      | `text-[11px] font-medium uppercase tracking-wide`  |
| Micro labels        | `text-2xs` (durations, dropdown section labels)    |
| Metadata strip      | `text-[11.5px] text-muted-foreground`              |
| Code / version      | `font-mono text-xs` (+ `tabular-nums` for numbers) |

## Spacing & layout

| Token            | Value                                             |
| ---------------- | ------------------------------------------------- |
| Page section gap | `space-y-5`                                        |
| Toolbar gap      | `gap-3` (wraps)                                    |
| Row padding      | `px-4 py-3` (header row `py-2.5`)                  |
| Grid column gap  | `gap-3` (12px) — used in min-width calc            |
| Action btn gap   | `gap-2`                                            |
| Sticky header    | `sticky top-0 z-10 -mx-6 px-6 pt-4 pb-3` (bleeds to `Content` `p-6`) |

## Components / sizing

- **Buttons:** header actions `size="sm"` + `h-8 text-sm font-medium`; toolbar
  triggers `h-9`; row icon buttons `size="icon" h-8 w-8`.
- **Search input:** `Input` with leading `Search` icon, `pl-9`,
  `min-w-[220px] flex-1 sm:max-w-sm`.
- **Table:** CSS-grid rows (`grid` + dynamic `gridTemplateColumns`), not `<table>`;
  horizontal scroll via `overflow-x-auto` + computed `minWidth`. Trailing
  `48px` actions column.
- **Icons:** `@/lib/icons` (lucide). Inline icons `h-4 w-4`; small/menu icons
  `h-3.5 w-3.5`; micro `h-3 w-3`.
- **Empty/menu/dropdown/pagination:** shared shadcn primitives from
  `@/components/ui/` (`EmptyState`, `DropdownMenu`, `Badge`, `TablePagination`).

## Conventions

- Every interactive element carries a `data-testid`.
- Destructive menu items: `text-destructive focus:text-destructive`.
- Numeric values use `tabular-nums`; durations via `formatDuration`, dates via
  `formatDate` (utils).
