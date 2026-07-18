# Supabase Setup Guide — Phase 1

Follow these steps once to wire up the backend. Takes ~10 minutes.

---

## 1. Create a Supabase Project

1. Go to **https://supabase.com** and sign in (free account)
2. Click **New project**
3. Choose a name (e.g. `retirement-planner`), set a strong DB password, pick the closest region
4. Wait ~2 minutes for the project to provision

---

## 2. Create the Database Table

In your Supabase project, go to **SQL Editor** and run:

```sql
-- Application plans table
CREATE TABLE plans (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id     UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  name        TEXT NOT NULL DEFAULT 'My Retirement Plan',
  data        JSONB NOT NULL,
  created_at  TIMESTAMPTZ DEFAULT now(),
  updated_at  TIMESTAMPTZ DEFAULT now()
);

-- Row-Level Security: each user sees only their own plans
ALTER TABLE plans ENABLE ROW LEVEL SECURITY;

CREATE POLICY "users own their plans"
  ON plans FOR ALL
  USING  (auth.uid() = user_id)
  WITH CHECK (auth.uid() = user_id);
```

---

## 3. Get Your API Keys

In your Supabase project:

1. Go to **Project Settings → API**
2. Copy:
   - **Project URL** → looks like `https://xxxxxxxxxxxx.supabase.co`
   - **anon / public key** → long JWT string starting with `eyJ...`

---

## 4. Add Keys to index.html

Open `index.html` and find these two lines near the bottom of the `<script>` block:

```js
const SUPABASE_URL  = 'YOUR_SUPABASE_URL';
const SUPABASE_ANON = 'YOUR_SUPABASE_ANON_KEY';
```

Replace the placeholder strings with your actual values:

```js
const SUPABASE_URL  = 'https://xxxxxxxxxxxx.supabase.co';
const SUPABASE_ANON = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';
```

> **Safe to commit?** Yes — the `anon` key is designed to be public.
> It only allows operations permitted by Row-Level Security policies.
> Never commit the `service_role` key.

---

## 5. Enable Email Auth (already on by default)

In Supabase: **Authentication → Providers → Email** — ensure it is enabled.

Optional: turn off "Confirm email" during development so you can sign in immediately
after registering (Authentication → Settings → uncheck "Enable email confirmations").

---

## 6. Test Locally

Open `index.html` directly in your browser (or via `npx serve .`).

- The login screen appears
- Register a new account → confirm email if required → sign in
- The planner loads, plan is auto-saved to Supabase on every change
- Open a second browser / incognito → same account → same plan loads

---

## 7. Deploy (Phase 4 preview)

Push to GitHub → connect to **Vercel** (vercel.com) or **Netlify**:

1. Import your GitHub repo
2. No build command needed — it's a static file
3. Set publish directory to `.` (root)
4. Deploy → you get a `https://your-app.vercel.app` URL instantly

Add a custom domain in the Vercel dashboard when ready.
