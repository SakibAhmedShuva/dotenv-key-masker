# dotenv-key-masker

A lightweight Python utility to **mask API keys and secrets** in `.env` files and optionally strip comment lines — safe to commit, safe to share.

---

## What it does

- 🔍 Recursively finds all `.env`, `.env_local`, `.env.*` files in a given folder
- 🔒 Masks values longer than 7 characters → `FORMS_API_KEY=fsk_20babd` becomes `FORMS_API_KEY=fs...`
- ✅ Skips numeric values like `POLL_INTERVAL=15`
- ✅ Skips boolean values like `DEBUG=True` / `ENABLED=False`
- 🗑️ Optionally deletes all comment lines starting with `#`
- 👁️ Dry run mode — preview changes without touching files

---

## Example

**Before:**
```dotenv
# Database config
DB_HOST=localhost
DB_PORT=5432

FORMS_API_KEY=fsk_20babd39xyz
POLL_INTERVAL=15
DEBUG=True
SECRET_TOKEN=s3cr3tT0k3nAbc
```

**After** (`STRIP_COMMENTS=True`, `MASK_KEYS=True`):
```dotenv
DB_HOST=localhost
DB_PORT=5432
FORMS_API_KEY=fs...
POLL_INTERVAL=15
DEBUG=True
SECRET_TOKEN=s3...
```

---

## Usage

1. Clone the repo:
```bash
git clone https://github.com/SakibAhmedShuva/dotenv-key-masker.git
cd dotenv-key-masker
```

2. Open `mask_env.py` and set your config at the top:
```python
FOLDER_PATH    = "/path/to/your/project"  # folder to scan
STRIP_COMMENTS = True   # delete lines starting with #
MASK_KEYS      = True   # mask long secret values
MIN_LENGTH     = 7      # values longer than this get masked
DRY_RUN        = False  # set True to preview without saving
```

3. Run:
```bash
python mask_env.py
```

Or use it directly in **Jupyter Notebook** — just paste the script into a cell and run.

---

## Config options

| Option | Default | Description |
|---|---|---|
| `FOLDER_PATH` | `"."` | Root folder to scan recursively |
| `STRIP_COMMENTS` | `True` | Remove lines starting with `#` |
| `MASK_KEYS` | `True` | Mask values longer than `MIN_LENGTH` |
| `MIN_LENGTH` | `7` | Minimum value length to trigger masking |
| `DRY_RUN` | `False` | Preview changes without writing files |

---

## Masking logic

A value is masked only if **all** of the following are true:

- Length is greater than `MIN_LENGTH` (default 7)
- It is **not** a pure number (e.g. `15`, `3.14`)
- It is **not** a boolean (`True`, `False`, `true`, `false`)

---

## Requirements

No external dependencies. Pure Python 3.

```bash
python >= 3.6
```

---

## License

MIT License — free to use and modify.

---

## Author

**Sakib Ahmed**
[LinkedIn](https://linkedin.com/in/sakibahmedai) · [Kaggle](https://kaggle.com/skbahmed) · [GitHub](https://github.com/SakibAhmedShuva)
