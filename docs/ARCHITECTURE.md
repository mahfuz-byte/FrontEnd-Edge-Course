# Architecture

## Overview
TaskBoard is a small React (Vite) application that implements a Kanban-style task manager.

### Core goals
- Keep the app simple and fully client-side.
- Persist user session/theme/tasks in `localStorage`.
- Use React Context + `useReducer` to centralize task state updates.

## Runtime flow
1. `src/main.jsx` renders `<App />`.
2. `src/App.jsx` wraps routes with providers:
   - `AuthProvider`
   - `ThemeProvider`
   - `BoardProvider`
3. Routing:
   - `/login` → `LoginPage`
   - `/board` → `BoardPage` (protected by `PrivateRoute`)

## State model
### Auth
- Source: `src/context/AuthContext.jsx`
- Storage key: `taskboard_user`
- Notes: This is **mock authentication** for demo use.

### Theme
- Source: `src/context/ThemeContext.jsx`
- Storage key: `taskboard_theme`
- Implementation: toggles the `dark` class on `document.documentElement`.

### Board / Tasks
- Sources:
  - `src/context/BoardContext.jsx`
  - `src/reducers/boardReducer.js`
- Storage key: `taskboard_tasks`

#### Task shape
A task is a plain object:
- `id`: number (created using `Date.now()`)
- `title`: string
- `description`: string
- `priority`: `'low' | 'medium' | 'high'`
- `status`: `'todo' | 'in_progress' | 'done'`
- `createdAt`: string (localized date)

#### Actions
The reducer supports:
- `ADD_TASK`
- `UPDATE_TASK`
- `DELETE_TASK`
- `MOVE_TASK`
- `SET_TASKS`

## Persistence
The app uses `src/hooks/useLocalStorage.js` as the abstraction for reading/writing JSON values.

### Important note
If you extend task fields, ensure:
- The reducer updates remain immutable.
- Local storage saves/loads remain backward-compatible (provide defaults for missing fields).

## UI composition
- `BoardPage` splits tasks into columns by `status`.
- `Column` renders a list of `TaskCard`.
- `Modal` is used for creating/editing tasks.

## Suggested future improvements
- Replace mock auth with a real backend.
- Add drag-and-drop via a DnD library.
- Add tests (unit tests for reducer; integration tests for pages).
