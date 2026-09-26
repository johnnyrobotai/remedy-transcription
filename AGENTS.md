# Repository Guidelines

## Project Structure & Module Organization

Remedy Transcription is a local-first Tauri 2 desktop app. The root `package.json` drives Tauri commands, while the React/Vite app lives under `frontend/`. Frontend source is in `frontend/src/`, with reusable UI in `components/`, IPC and domain types in `services/`, Web Worker transcription in `workers/`, shared formatting logic in `lib/` and `utils/`, and styles in `css/`. Rust application code is in `src-tauri/src/`; sidecar handling, paths, store, commands, and events are split into separate modules. Generated app icons come from `src-tauri/app-icon.svg`, public web assets are in `frontend/public/`, and setup helpers are in `scripts/`.

## Build, Test, and Development Commands

- `./scripts/fetch-sidecars.sh`: downloads required `yt-dlp`, `ffmpeg`, and `ffprobe` sidecars into `src-tauri/binaries/`.
- `npm ci` and `npm --prefix frontend ci`: install root Tauri CLI and frontend dependencies from lockfiles.
- `npm run dev`: starts the Vite frontend through `tauri dev` with hot reload.
- `npm run frontend:build`: runs `tsc` and builds the Vite frontend.
- `npm --prefix frontend run lint`: runs ESLint over frontend source.
- `cargo check --manifest-path src-tauri/Cargo.toml` and `cargo test --manifest-path src-tauri/Cargo.toml`: validate Rust code.
- `npm run build`: builds the platform installer into `src-tauri/target/release/bundle/`.

## Coding Style & Naming Conventions

Frontend code uses TypeScript, React 18, ES modules, ESLint, and Prettier. Follow `frontend/.prettierrc`: 4-space indentation, semicolons, 80-column print width, double quotes in TS, and single quotes in JSX. Name React components in PascalCase, hooks as `useSomething`, and service/lib utilities in camelCase. Rust uses edition 2021 and standard `rustfmt` conventions; keep Tauri command handlers and sidecar/store logic in their existing modules.

## Testing Guidelines

Rust tests run with `cargo test --manifest-path src-tauri/Cargo.toml`. No frontend unit-test runner is configured, so frontend changes should at minimum pass `npm run frontend:build` and `npm --prefix frontend run lint`. When adding tests, place them close to the affected code and use clear behavior names such as `formats_long_segments` or `downloads_audio_sidecar`.

## Commit & Pull Request Guidelines

Recent commits use short, imperative subject lines, for example `Add Tauri CI build checks` and `Clarify education fair use disclaimer`. Keep PRs focused, describe user-facing impact, list validation commands, and include screenshots or recordings for visible UI changes. Link related issues when available.

## Security & Configuration Tips

Do not commit downloaded sidecars, model weights, credentials, or local app data. Keep transcription local-first: avoid introducing network services unless the README and privacy expectations are updated.
