
# Supabase Project Export

This project includes a complete, GitHub-safe replication of a Supabase project, including both **SQL schema** and **non-SQL configuration**.

## Contents

### 1. `Supabase Full Schema And Config.sql`
A comprehensive SQL dump containing:
- Tables, types, indexes, and constraints
- Functions and triggers
- RLS policies and permissions
- Sequences and their ownership
- Storage buckets and access policies
- Installed PostgreSQL extensions

### 2. `Supabase Project NonSQL Config.json`
JSON configuration covering:
- Auth providers, JWT config, and templates
- Realtime settings (broadcast, presence, changes)
- File Storage rules
- Edge Function metadata
- Webhooks and API rate limits
- Project metadata (name, region, created_at)

## Usage

### 🛠 Restore SQL Schema (3 Methods)

#### Method 1: Supabase SQL Editor (Web UI)
1. Open your Supabase project.
2. Go to the **SQL Editor**.
3. Paste the contents of `Supabase Full Schema And Config.sql`.
4. Run the script.

#### Method 2: Supabase CLI
```bash
supabase db reset --file Supabase\ Full\ Schema\ And\ Config.sql
```

#### Method 3: psql (PostgreSQL CLI)
```bash
psql -h db.<project-ref>.supabase.co -U postgres -d postgres -f "Supabase Full Schema And Config.sql"
```
> Replace `<project-ref>` with your actual project reference.

### 🔐 Apply Non-SQL Config (3 Approaches)

#### Method 1: Supabase Dashboard
Manually copy settings from the JSON file into the UI:
- Auth > Settings
- Auth > Email Templates
- Storage > Settings
- Edge Functions > Deploy

#### Method 2: Supabase Admin API (Advanced)
Use REST calls to set config programmatically. Example (requires service_role token):
```bash
curl -X PATCH https://<project>.supabase.co/auth/settings   -H "Authorization: Bearer <service_role>"   -H "Content-Type: application/json"   -d @Supabase\ Project\ NonSQL\ Config.json
```

#### Method 3: Supabase CLI (partial)
Some features like edge function deployment or project settings can be managed:
```bash
supabase functions deploy hello-world
```

## Limitations
- File contents inside storage buckets are **not exported**.
- Edge Function source code must be deployed via CLI or Git.
- Auth settings like branding and magic link templates require dashboard configuration.

## Recommended Tools
- [Supabase CLI](https://supabase.com/docs/guides/cli)
- [pg_dump + pg_restore](https://www.postgresql.org/docs/current/app-pgdump.html)
- `supabase functions deploy`
- [Supabase Admin API Docs](https://supabase.com/docs/reference/api)

---
**Last updated:** {{timestamp}}

Maintained by the Supabase Project Export Kit ✨
