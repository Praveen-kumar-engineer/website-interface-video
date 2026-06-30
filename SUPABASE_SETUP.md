# SkillBridge — Supabase Setup

1. Open `assets/js/supabase.js`
2. Replace `PASTE_YOUR_PUBLISHABLE_ANON_KEY_HERE` with your project's **anon / public** key
   (Supabase Dashboard → Project Settings → API → Project API keys → `anon` `public`).
3. Required tables (RLS **disabled** as requested):

```sql
create table students (
  id bigserial primary key,
  full_name text, email text unique, phone text,
  college text, department text,
  created_at timestamptz default now()
);

create table companies (
  id bigserial primary key,
  company_name text, email text unique, password text,
  industry text, website text,
  created_at timestamptz default now()
);

create table internships (
  id bigserial primary key,
  title text, company text, location text,
  duration text, stipend text, description text,
  created_at timestamptz default now()
);

create table applications (
  id bigserial primary key,
  student_email text, internship_id bigint references internships(id),
  status text default 'Pending',
  created_at timestamptz default now()
);
```

4. Deploy: drag the `skillbridge/` folder onto Netlify — no build step.
