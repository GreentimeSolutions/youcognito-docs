# Maintaining these docs

A note for whoever maintains the Youcognito docs.

## The one rule

**Whenever a change goes live, update the docs in the same sitting:**

1. Add an entry to the [Changelog](project/changelog.md) under the date it went live (US Central time). Write what a user notices, not what the code does. Skip internal refactors.
2. Update the feature page(s) it touches, under `features/`, `token/` or `builders/` in this repo. On the published site those last two show up as `the-token/` and `for-builders/`.
3. Update [What's live right now](getting-started/whats-live.md), and remove any 🟡 **Coming soon (rolling out)** hints on pages for things that are now live. Change the changelog's 🟡 entries to ✅.
4. If you changed a number (amounts, limits, thresholds, song length), search the docs for the old number and update every match.
5. If something was removed, delete or rewrite its page and remove it from `SUMMARY.md`.

## Where facts come from

Check against the app repo before writing:

| Fact | Source of truth |
| --- | --- |
| Faucet amounts, streak bonus, limits | `src/lib/youcog/faucet.server.ts` |
| Listen boost numbers, song title and length | `src/constants/listen.ts` |
| Tiles, links, game, Short, project wallets | `src/constants/media.ts`, `src/constants/site.ts` |
| Deep Mission threshold | `src/lib/youcog/holder.server.ts` |
| What's live | `git log origin/main` in the app repo, plus a quick look at youcognito.vercel.app |
| Changelog | `git log origin/main` (and any release branch being deployed) |

Handy command for the changelog, in Central time:

```bash
TZ=America/Chicago git log origin/main --date=format-local:'%Y-%m-%d' --format='%ad %s'
```

## Never put in the docs

* Private keys, API keys, passwords, salts, database URLs or any environment variable **values**
* Private email addresses or personal details. The only public contact is **ghost.youcog@gmail.com**
* Price talk, dollar figures for YOUCOG, price predictions or promises of value, profit or yield
* Staking or holdings-based earning teasers, or details of how nito would be earned, before a lawyer review
* A ticker for nito. nito has no ticker and is not a token. nito and the nito DAO stay marked **proposed, not live** until they really launch
* Earn, reward or pays wording for gifts. Faucet, boost and survey gifts are giveaways while supplies last

## Style

* Users first, builders second. Plain English, short sentences, skimmable headings and tables.
* Say "coming soon" for anything not live yet.
* Times in US Central with the zone named; faucet days are UTC.
* One page per feature. Every page must be listed once in `SUMMARY.md`.

## Publishing

The docs are plain Markdown for GitBook Git Sync (`.gitbook.yaml`, `README.md`, `SUMMARY.md`). Images go in `.gitbook/assets/`.

**One-time setup (needs a human with the accounts):**

1. Create a GitHub repo for the docs (for example `youcognito-docs`) and push this folder to its `main` branch.
2. Sign up at [app.gitbook.com/join](https://app.gitbook.com/join) (the Free plan is enough: one user, GitHub Sync included, published at a `gitbook.io` address).
3. Create a site, choose **Sync with Git** (or open **Git Sync** in the site sidebar), pick **GitHub**, and install the **GitBook GitHub app** on the account or org that owns the docs repo, giving it access to that repo.
4. Pick the repo and `main` branch, set the initial sync direction to **GitHub → GitBook**, leave the project directory empty, and click **Sync**.
5. Check the preview, then click **Publish**.

**After that:** every push to `main` updates GitBook. Edits made in GitBook are committed back to GitHub when a change request is merged. Don't edit `README.md` in the GitBook editor; change it in the repo.

The GitBook **Import** panel also takes Markdown or a ZIP, but only 20 pages and 20 files per import and it doesn't stay in sync, so Git Sync is the better fit for this docs set. A custom docs domain needs a paid GitBook plan.
