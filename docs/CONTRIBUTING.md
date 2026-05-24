# Contributing

## Scope
This repository is a course-style project. Contributions are welcome as:
- bug fixes
- UI improvements
- accessibility improvements
- refactors that reduce complexity
- documentation updates

## Development
### Requirements
- Node.js 16+
- npm

### Setup
1. Install dependencies: `npm install`
2. Start dev server: `npm run dev`
3. Build: `npm run build`

## Code style
- Prefer small, focused components.
- Keep state changes inside contexts/reducers.
- Do not mutate reducer state.
- Use Tailwind utility classes rather than custom CSS when possible.

## Commits
- Use clear messages: `feat: ...`, `fix: ...`, `docs: ...`, `refactor: ...`.

## Pull requests
- Describe the problem and solution.
- Include screenshots for UI changes.
- Ensure `npm run build` succeeds.
