# optimal-links

A self-hosted link-in-bio page for [@beoptimal.ca](https://www.instagram.com/beoptimal.ca/) — the Linktree replacement.

**Live:** https://optimal-research-team.github.io/optimal-links/

One static HTML file on GitHub Pages: no build step, no subscription, no Linktree branding. Built on the
[Optimal design system](https://github.com/Optimal-Research-Team/optimal-design-system) ("Forest night" tokens,
Castoro + Public Sans, the `<optimal-logo>` Into Range animation, a v1.3 fluorescence micrograph).

## What's on it

| Section | Links |
| --- | --- |
| Hero | Book an intro (book.beoptimal.ca), Call, Directions, Email |
| Care | Menopause & perimenopause · Longevity Membership · IV iron founding waitlist |
| Testing | VO₂ max · InBody 580 · Creator 600 · Hyperbaric oxygen |
| Read | Menopause Protocol · Longevity Protocol · The Journal |
| Visit | Address, hours (today highlighted in clinic time), phone, email, a vCard download |

Facts come from the design system's "Current clinic facts" (Oct 2026) and the live beoptimal.ca nav.

## Analytics (what Linktree charges for)

beoptimal.ca already runs GA4, the Meta pixel and Clarity, so the page doesn't track anything itself. Instead,
every beoptimal.ca link is UTM-tagged on load:

```
utm_source=instagram  utm_medium=social  utm_campaign=link_in_bio  utm_content=<row id>
```

In GA4: **Reports → Acquisition → Traffic acquisition**, filter session campaign = `link_in_bio`, and add
`Session manual ad content` as a secondary dimension to see which row people tapped.

Use the same page for other profiles by adding `?s=`: `…/optimal-links/?s=facebook` tags clicks as
`utm_source=facebook`.

## Editing

Open `index.html`. Each link is one `<a class="row">` (or `<a class="cell">` in the Testing grid): title in `<b>`,
subtitle in `<span>`, a `data-id` for analytics. Commit to `main` and Pages redeploys in about a minute.

## Custom domain (recommended)

To make the bio read `links.beoptimal.ca` instead of the github.io address:

1. At the beoptimal.ca DNS provider, add `CNAME  links  optimal-research-team.github.io`.
2. Then run:
   ```bash
   echo links.beoptimal.ca > CNAME && git add CNAME && git commit -m "Custom domain" && git push
   gh api -X PUT repos/Optimal-Research-Team/optimal-links/pages -f cname=links.beoptimal.ca -F https_enforced=true
   ```
   Don't add the `CNAME` file before the DNS record exists, or the github.io URL will redirect to a domain that
   doesn't resolve yet.

## Local preview

```bash
python3 -m http.server 3093
```
