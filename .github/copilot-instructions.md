# Project Guidelines

## Build And Test
- Prerequisite: Node.js 22+.
- Install dependencies: `npm install`.
- Start dev server: `npm run dev`.
- Lint: `npm run lint`.
- Build: `npm run build`.
- Test: `npm run test`.
- For code changes, run `npm run lint; npm run build; npm run test` before finalizing.

## Architecture
- Entry point is `src/main.tsx`; it mounts `App` and loads global styles.
- `src/App.tsx` is a thin state-driven screen switch between `StartScreen` and `GameScreen` plus `BingoModal`.
- `src/hooks/useBingoGame.ts` owns game state, actions, win detection orchestration, and localStorage persistence.
- `src/components/*` are UI components that consume props and callbacks.
- `src/utils/bingoLogic.ts` contains pure domain logic (board generation, toggling, bingo checks).
- `src/data/questions.ts` stores the question bank.
- Behavior contracts live in `src/utils/bingoLogic.test.ts` with setup in `src/test/setup.ts`.

## Conventions
- Keep game rules in `src/utils/bingoLogic.ts` as pure functions; keep orchestration and side effects in `useBingoGame`.
- Use shared domain types from `src/types/index.ts` instead of duplicating inline object shapes.
- Prefer small presentational components and pass behavior down via props.
- Preserve localStorage compatibility checks in `useBingoGame` (`STORAGE_VERSION` and payload validation) when changing persisted shape.

## Environment Notes
- Tailwind v4 is configured via `@tailwindcss/vite` and `@import 'tailwindcss'` in `src/index.css`.
- The production base path in `vite.config.ts` depends on `VITE_REPO_NAME`; this affects GitHub Pages deploy paths.
