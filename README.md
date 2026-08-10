# VMG

Portfolio and contact page for VMG's construction business. 

## Goals

- Make the experience an easy one for any person to be able to surf the site and contact the owner whether it be through the sites contact area or through SMS or a call. 
- Make it possible so that the owner is notified of a new contact within seconds of getting the request. 
- Make an admin page so that the owner has access to all requests and can post anything they want as well. Possibly a schedule?
- Send an estimate with professional courtesy.
- Add accessibility for all. 

## Tech Stack (May be subject)

| Concern | Choice | Why |
| --- | --- | --- |
| Framework | Next.js (App Router) + TypeScript | Static public pages for speed/SEO, dynamic admin behind auth, one codebase. Server Actions remove the need for a separate API layer. |
| Styling | Tailwind | Fast, consistent, no CSS architecture decisions. |
| UI primitives | Radix UI or React Aria Components | Keyboard nav and focus management are hard to hand-roll correctly. |
| Hosting | Vercel | Push to GitHub → deploy. HTTPS + CDN automatic. |
| Database | Supabase (Postgres) | Relational data with a real schema. |
| Auth | Supabase Auth — magic link, single user | No password to forget, leak, or build a reset flow for. |
| File storage | Supabase Storage + `next/image` | Job photos come off phones at 4MB+; needs resizing and modern formats. |
| Email | Resend + React Email | Lead notifications and estimate delivery. Needs a real domain with SPF/DKIM/DMARC or estimates land in spam. |
| SMS | Twilio | New-lead alerts — in contracting, the first responder usually wins the job. |
| Spam protection | Cloudflare Turnstile | Invisible in most cases; no visual puzzle to fail. |
| Rate limiting | Upstash Redis | On the contact form endpoint. |
| Validation | Zod | Shared between client and server. |
| Error monitoring | Sentry | Nobody is watching this site daily. |
| Analytics | Vercel Analytics or Plausible | Which pages actually drive contacts. |
| PDF export | `@react-pdf/renderer` | Downloadable estimates for customers who want a copy. |
| Image compression | `browser-image-compression` | Shrink customer photo uploads client-side before they hit the network. |

Supabase is chosen over assembling Neon + Auth.js + a separate storage provider because
this is a solo-maintained project. Every extra vendor is another dashboard and another set
of keys to debug later.
