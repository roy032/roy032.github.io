# Jayanta Roy: portfolio

**Live on AWS Amplify:** https://main.d21y6lk1nky3c1.amplifyapp.com
Also served from this repo by GitHub Pages: https://roy032.github.io

My portfolio as one hand-written HTML file: no framework, no build step, no tracking. It's my entry for the [AWS Student Builder Challenge: Build Your Tech Superpower](https://builder.aws.com/build/hackathons/3bff5627-ef21-3bfc-acfc-fce21d39a4f6/aws-student-builder-challenge-build-your-tech-superpower).

## The creative feature: a terminal that measures you back

Every project I build follows one rule: measure it before you trust it, and report the result with its uncertainty. The terminal at the top of the page applies that rule to you.

| Command | What it does |
|---|---|
| `measure` | Times the gaps between your keystrokes and reports your typing speed with a **95% bootstrap confidence interval** (1,000 resamples) and the sample size. Below 15 samples it refuses to answer. |
| `reflex` | Five-round reaction-time test that works by tapping, so phones get a real number too. Reports the mean with a bootstrap interval, and tells you plainly that n = 5 makes it wide. |
| `superpower` | Unlock animation, then the superpower itself. |
| `ls`, `cat <project>`, `open <project>` | Explore the projects from the shell; `open` scrolls to the card and highlights it. |
| `about`, `projects`, `skills`, `contact` | Jump to a section. |
| `help`, `stats`, `whoami`, `hire`, `history`, `clear` | The usual, plus `hire` copies my email. Two more commands are hidden. |

It works like a terminal: Tab completes, ↑/↓ walk the history, and `/` focuses it from anywhere on the page. On phones there are tap-to-run chips under it. A counter tracks how many of the 19 commands you've discovered (stored only in your browser), and output is announced to screen readers through a live region.

## Sections

**About me**, **Selected work** (six featured projects with measured results), **More projects** (filterable grid), **Approach**, **Skills**, **Recent activity** (live from the GitHub API) and **Contact**.

## How it's deployed

```
git push ──► GitHub (this repo, main)
                │  Amplify GitHub App, read-only, this repository only
                ▼
         AWS Amplify Hosting ── no build step: index.html served as-is
                │  HTTPS, global CDN
                ▼
   https://main.d21y6lk1nky3c1.amplifyapp.com
```

- **AWS Amplify Hosting** redeploys automatically on every push to `main`, in about a minute. There's no build command; the build output directory is the repository root.
- **AWS CLI v2** signed in with `aws login`, which uses browser sign-in and temporary credentials, so no access keys exist.
- The same commit is also served by GitHub Pages, which stays the long-term address.

## Run it locally

```bash
python -m http.server 8000
```

Then open http://localhost:8000. There's nothing to install.
