# pgvector

## 1. Install pgvector on your system

**Ubuntu/Debian:**
```bash
sudo apt install postgresql-<version>-pgvector
# e.g. postgresql-16-pgvector
```

**macOS (Homebrew):**
```bash
brew install pgvector
```

**From source (any Linux):**
```bash
git clone https://github.com/pgvector/pgvector.git
cd pgvector
make
make install  # may need sudo
```

**Docker** — if your Postgres is running in Docker, the base `postgres` image doesn't include pgvector. Switch to the official pgvector image instead:
```dockerfile
# Replace your current image with:
image: pgvector/pgvector:pg16   # match your PG major version
```

---

## 2. Enable the extension in your database

Once the system library is installed, connect to the `flowers` database and run:
```sql
CREATE EXTENSION IF NOT EXISTS vector;
```

Or do it in one shot from the shell:
```bash
psql -d flowers -c "CREATE EXTENSION IF NOT EXISTS vector;"
```

---

## 3. Re-run the restore

```bash
pg_restore -d flowers flowers.dump
```

---

## Quick checklist

| Check | Command |
|---|---|
| What PG version are you on? | `psql --version` |
| Is pgvector installed? | `psql -c "SELECT * FROM pg_available_extensions WHERE name = 'vector';"` |
| Is the extension active? | `psql -d flowers -c "\dx vector"` |

The `pg_available_extensions` query will tell you if the library is visible to Postgres — if `vector` doesn't appear there at all, the system-level install (step 1) hasn't taken effect yet, and you may need to restart Postgres after installing.
