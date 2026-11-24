HELLOFIXER PASSWORD RESET PAGE
===============================

Files
-----
index.html - hosted password reset page.

1) Create a GitHub repository
-----------------------------
- Sign in to GitHub.
- Create a NEW public repository, for example: hellofixer-password-reset
- Upload index.html to the repository root.
- Commit the file.

2) Enable GitHub Pages
----------------------
- Open repository Settings -> Pages.
- Under "Build and deployment", choose "Deploy from a branch".
- Select branch "main" and folder "/ (root)".
- Save and wait for GitHub Pages to publish the site.

Your page URL will look like:
https://YOUR-GITHUB-USERNAME.github.io/hellofixer-password-reset/

3) Configure Supabase
---------------------
- Open Supabase -> Authentication -> URL Configuration.
- Set Site URL to the published GitHub Pages URL above.
- Add that exact URL to Redirect URLs (including trailing slash).
- Save.

4) Update HelloFixer forgot-password request
--------------------------------------------
When calling Supabase resetPasswordForEmail, set redirectTo to the exact published URL:

redirect_url = "https://YOUR-GITHUB-USERNAME.github.io/hellofixer-password-reset/"
supabase.auth.reset_password_for_email(email, options={"redirect_to": redirect_url})

If your Python code uses Supabase REST directly, send redirect_to as the redirect_to query parameter to:
POST https://jouxqhwhwckzhfslyaht.supabase.co/auth/v1/recover?redirect_to=URL_ENCODED_REDIRECT_URL

Keep your existing publishable key in the apikey header.
Do NOT put a service_role/secret key in the desktop app or this page.

5) Test
-------
- Request a fresh reset email from HelloFixer.
- Open the newest email link on the same browser where the page opens.
- The page should say "Reset link verified".
- Enter and confirm a new password.
- Return to HelloFixer and sign in.

Important
---------
- The reset link is single-use and expires according to your Supabase email template/auth settings.
- If the page says no valid session, request a NEW reset email.
- GitHub Pages URL must match exactly in both Supabase Redirect URLs and HelloFixer redirect_to.
- The page uses the Supabase publishable key, which is safe for client-side use. Never use the service-role key.
- This page changes the Supabase Auth password only. It does not approve a pending technician or grant 365-day access.
- Supabase SMTP/email delivery must be configured separately for reliable email delivery.
