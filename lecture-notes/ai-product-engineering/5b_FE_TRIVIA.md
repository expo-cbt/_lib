# Frontend Developer Trivia

## Feature-based Directory Structure

## Atomic Design Pattern

**Atomic Design** — a component organization pattern (Brad Frost), structuring UI into 5 levels of increasing complexity:

- **Atoms** — smallest building blocks: `Button`, `Text`, `Input`, `Icon`
- **Molecules** — collection of atoms: `FormField` (label + input), `DataTable` 
- **Organisms** — shared UI sections: `Header`, `Nav`, `Aside`, `Footer`
- **Templates** — page layout skeletons, arranging organisms without real data
- **Pages** — templates filled with real/actual data — the final screen

#### Classic folder structure:

```sh
components/
  atoms/
    Button.tsx
    Text.tsx
  molecules/
    SearchBar.tsx
  organisms/
    TransactionListItem.tsx
    Header.tsx
  templates/
    DashboardTemplate.tsx
```

#### Adapted folder structure:

- **Templates ❌** — deprecated by Next.js and Expo file-based route layouts (i.e. layout.tsx, \_layout.tsx)
- **Pages ❌** — deprecated by Next.js and Expo file-based routing (i.e. app directory)
- **Species** — feature-based directory, organizes code by domain (components, hooks, types, utils) `products`, `customers`, `orders`
- **Widgets** — standalone, smart components with internal api calls (HoC, impure functions) `NotificationsWidget`

## SOLID Principles
