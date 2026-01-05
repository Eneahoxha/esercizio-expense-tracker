# AppSpese - Expense Tracker

Quick SPA using React + Vite that integrates with a local PocketBase backend.

Setup

1. Install dependencies:

```bash
npm install
```

2. Start the dev server:

```bash
npm run dev
```

3. Start PocketBase locally (from your PocketBase binary folder):

```bash
./pocketbase serve
```

PocketBase collection `spese` (create manually)

- Create a collection named `spese` with fields:
  - `descrizione` (text)
  - `importo` (number)
  - `data` (date)
- Set permissions for `list`, `view`, `create`, and `delete` to `anyone` so the frontend can access without auth during development.
- Insert 2 sample records manually via the PocketBase admin UI to verify the frontend fetch.

Important implementation notes

- The frontend uses `useEffect(..., [])` so the initial fetch runs once at mount.
- PocketBase list responses include records under the `items` key; the app reads `data.items` in the fetch response.
- Network operations are performed in `src/App.jsx` (parent). The `FormSpesa` component only collects data and calls `onAdd` prop.

Files added

- `src/App.jsx` - main component with fetch/create/update/delete logic
- `src/FormSpesa.jsx` - controlled form for adding expenses
- `src/ItemSpesa.jsx` - each expense item (edit & delete)
- `src/GraficoSpese.jsx` - bar chart using `react-chartjs-2` and `chart.js`

PocketBase endpoints used

- GET  /api/collections/spese/records?perPage=50
- POST /api/collections/spese/records
- PATCH /api/collections/spese/records/{id}
- DELETE /api/collections/spese/records/{id}

If you want, I can also add example PocketBase migration JSON or create sample records via the HTTP API.
