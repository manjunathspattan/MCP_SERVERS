# ExpenseTrackerMCPServer

MCP server for local expense tracking using `fastmcp` + SQLite.

## Project Files
- `main.py`: MCP tools (`add_expense`, `list_expenses`, `summarize`), categories resource, DB init.
- `categories.json`: category & subcategory definitions.
- `pyproject.toml`: metadata.
- `README.md`: this file.

## Requirements
- Python 3.14+
- `fastmcp` package

## Install
```powershell
python -m venv .venv
.venv\Scripts\activate
pip install fastmcp
```

## Run
```powershell
python main.py
```

## MCP tools and endpoints
- `add_expense(date, amount, category, subcategory="", note="")`
  - Adds expense row, returns `{'status': 'ok', 'id': <new id>}`.
- `list_expenses(start_date, end_date)`
  - Returns expense entries between dates (inclusive).
- `summarize(start_date, end_date, category=None)`
  - Returns total amount grouped by category.

## MCP resource
- `expense://categories` returns live `categories.json` content as JSON.

## Database
- `expenses.db` created automatically on first run.
- Schema:
  - `id INTEGER PRIMARY KEY AUTOINCREMENT`
  - `date TEXT NOT NULL`
  - `amount REAL NOT NULL`
  - `category TEXT NOT NULL`
  - `subcategory TEXT DEFAULT ''`
  - `note TEXT DEFAULT ''`

## Data
`categories.json` includes a full category/subcategory taxonomy (food, transport, housing, utilities, health, etc.).

## Notes
- `categories.json` is re-read on each request, so you can update categories dynamically without restarting the server.
- Date fields are text; use ISO format (`YYYY-MM-DD`) for consistent sorting.

