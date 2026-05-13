# Git Sync handoff

GitBook's API does not let you set up Git Sync — the GitHub/GitLab app installation, repo selection, branch selection, project directory, and initial sync direction are all UI-only. This file is the template for the user-facing instructions you generate so the user can finish wiring it up themselves.

The goal: hand the user a numbered, copy-paste-ready set of steps. One block per space. No prose paragraphs they'd have to read carefully — they should be able to skim it.

## Pre-handoff checklist

Before generating the handoff, make sure all of this is true:

- The local repo is committed and pushed to a remote (GitHub or GitLab).
- You know each space's project directory in the repo (e.g. `guides`, `api-reference`).
- You know which branch the user wants to sync from (default: `main`).
- The site exists in GitBook (you have its dashboard URL).
- For each space, you know whether it already exists (and you have its URL) or whether the user will create it during this step.

If any of those is false, finish that prep work first. Don't ask the user to context-switch into the GitBook UI before everything is ready.

## The handoff template

Fill in the bracketed values and present this to the user:

---

> ## Setting up Git Sync — one short step in the GitBook UI
>
> Everything else is done. To finish, you need to wire up two-way sync between each space and the corresponding folder in your repo. This is the one part that GitBook's API doesn't expose, so it has to happen in the UI. It takes about 30 seconds per space.
>
> **Before you start:** if you haven't already, install the GitBook app on your GitHub/GitLab account. The first space you wire up will prompt you to do this.
>
> ---
>
> ### Space 1: `[Space Title]`
>
> 1. Open the space dashboard: **[https://app.gitbook.com/o/<orgId>/s/<spaceId>](https://app.gitbook.com/...)**
> 2. Click **Set up Git Sync** in the top-right.
> 3. Choose **GitHub** (or GitLab — pick whichever matches your repo).
> 4. Authorize GitBook if prompted, then select repository: **`[owner/repo]`**
> 5. Branch: **`main`**
> 6. Click **Show advanced options** and set **Project directory** to: **`[guides]`**
> 7. Initial sync direction: **GitHub → GitBook** (since the repo is the source of truth).
> 8. Click **Initialize** and wait for the import to finish.
>
> ### Space 2: `[Space Title]`
>
> 1. Open the space dashboard: **[https://app.gitbook.com/o/<orgId>/s/<spaceId>](https://app.gitbook.com/...)**
> 2. Click **Set up Git Sync** in the top-right.
> 3. Choose **GitHub**.
> 4. Repository: **`[owner/repo]`**
> 5. Branch: **`main`**
> 6. **Project directory**: **`[api-reference]`**
> 7. Initial sync direction: **GitHub → GitBook**.
> 8. Click **Initialize**.
>
> *(repeat for each remaining space)*
>
> ---
>
> Once you've done all of them, let me know and I'll verify each space's sync state and apply the branding settings.

---

## Verifying afterwards

After the user confirms they're done, verify each space programmatically:

```bash
for space_id in $SPACE_IDS; do
  echo "=== $space_id ==="
  curl -s -H "Authorization: Bearer $GITBOOK_TOKEN" \
    https://api.gitbook.com/v1/spaces/$space_id/git/info
done
```

For each space, expect a 200 with `{repoName, installationProvider, integration, url, updatedAt}`. A 404 means sync isn't set up — point the user back to the relevant step.

Common issues:

- **"Repository not found"** in the UI — the GitBook app doesn't have access. The user needs to go to GitHub Settings → Applications → GitBook → Configure and grant access to the right repo.
- **Initial sync direction wrong** — if the user picks "GitBook → GitHub" by mistake on a space whose content lives in the repo, GitBook will overwrite the repo with the empty space. They can't undo this except by `git revert`. Be very explicit in the instructions about direction.
- **Project directory missing or wrong** — the space will sync the wrong content (or the whole repo). They can edit this in space settings → Git after the fact.

## When the user wants GitLab instead of GitHub

The flow is identical except the user needs to generate a GitLab personal access token first with `api`, `read_repository`, `write_repository` scopes, and they'll be asked to paste it in the GitBook UI. Mention this in the handoff if the repo is on GitLab.

## When there is no remote (local-only)

Git Sync requires a hosted remote — GitBook reaches the repo over the public Git provider APIs, not via direct file access. If the user explicitly chose local-only, they'll need to either push to a hosted remote later (GitBook supports private repos) or skip Git Sync and use the API content path. Tell them this clearly rather than implying Git Sync is possible without a remote.
