# AJAY MUSIC
Static site (HTML/CSS/JS, no build step) + Supabase (Auth, Postgres, Storage).
## Setup
1. Create a Supabase project. In SQL Editor run `schema.sql` (creates tables, RLS, the public `songs` bucket and its policies).
2. Authentication > Users > Add user (your admin email + password). Then run: `insert into public.admins(user_id) select id from auth.users where email='YOUR_EMAIL';`
3. Edit `config.js`: Project URL + **anon** key (Settings > API), social links, contact email. Never put the service_role key anywhere in this project.
4. Serve the folder over HTTPS (Netlify, Vercel, Cloudflare Pages, GitHub Pages) or locally: `npx serve .`
5. Open `#/admin`, sign in, upload songs (MP3 + cover).
## Notes
- Public visitors can only read published songs (RLS). Only users listed in `admins` can insert/update/delete songs and storage objects.
- Files in the public `songs` bucket have random paths; an unpublished song's file is reachable only by someone who knows its exact URL.
- Playlists and favorites are stored in the visitor's browser (localStorage).
- Share links look like `https://your-site/#/song/<id>`. The page updates its title/OG tags with JavaScript; link-preview bots that do not run JS show the site-level tags. For per-song previews use server-side rendering.
