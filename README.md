# Skillence Review

Student review frontend for Skillence Academy.

Fields: name, email, review, comment, and optional JPG/PNG/WebP/PDF upload (5 MB limit). The website requests geolocation permission before revealing the form. Browsers can always deny permission.

## Backend setup

The frontend is deployed as a static website, but submissions are disabled until you configure `config.js` with a Supabase URL, a publishable/anon key, and a **private** Storage bucket named by `storageBucket`. Do not use service-role/secret keys in browser code.

The `skillence_reviews` table must have columns `student_name`, `email`, `review`, `comment`, `attachment_path`, `latitude`, `longitude`, `consent_given` with suitable types, and RLS permitting only validated public INSERT operations. Storage must be configured to allow uploads without exposing private files. In production, enforce validation, rate limits, and restricted uploads server-side (for example via an authenticated, rate-limited Edge Function), with authorized-only read access. Never make student emails, locations, or files publicly readable.

The form does not upload or save anything until the backend is configured. This site can access only files a visitor explicitly chooses.
