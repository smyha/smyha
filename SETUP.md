# Setup — GitHub profile repo (`smyha/smyha`)

Neofetch-style SVG card (auto-updated stats) + markdown sections. Based on [Andrew6rant/Andrew6rant](https://github.com/Andrew6rant/Andrew6rant).

## Fix `401 Bad credentials` in Actions

The workflow needs a valid **Personal Access Token** stored as repo secret `ACCESS_TOKEN`.

### Option A — Classic PAT (simplest)

1. Go to [github.com/settings/tokens](https://github.com/settings/tokens) → **Generate new token (classic)**
2. Note: `smyha-profile-stats`
3. Expiration: 90 days or No expiration (your choice)
4. Scopes — enable:
   - `read:user`
   - `public_repo` (add `repo` if you want private-repo LOC counted)
5. Generate and **copy the token** (`ghp_...`)
6. Repo **smyha/smyha** → **Settings → Secrets and variables → Actions → New repository secret**
   - Name: `ACCESS_TOKEN` → paste token
   - Name: `USER_NAME` → `smyha`
7. Re-run the failed workflow: **Actions → README build → Re-run jobs**

### Option B — Fine-grained PAT

1. [github.com/settings/personal-access-tokens](https://github.com/settings/personal-access-tokens) → **Generate new token**
2. Resource owner: **smyha**
3. Repository access: **All repositories**
4. **Account permissions** (read-only):
   - Followers
5. **Repository permissions** (read-only):
   - Contents
   - Metadata
   - Commit statuses
6. Generate token (`github_pat_...`) and save as secret `ACCESS_TOKEN`
7. Secret `USER_NAME` = `smyha`

> `today.py` detects fine-grained tokens (`github_pat_`) and uses `Bearer` auth automatically.

### Checklist

| Secret | Value | Required |
|--------|-------|----------|
| `ACCESS_TOKEN` | `ghp_...` or `github_pat_...` | Yes |
| `USER_NAME` | `smyha` | Yes |

If the token expired or was revoked, create a new one and **update** the secret (no code change needed).

## Publish

1. Repo **`https://github.com/smyha/smyha`** must stay **public** (profile README only renders from public repos).
2. Push this folder to `main`.
3. Configure secrets above.
4. Workflow runs on push and daily at 04:00 UTC → updates `dark_mode.svg` / `light_mode.svg`.

## Files

| File | Role |
|------|------|
| `README.md` | Profile page (SVG + sections) |
| `dark_mode.svg` / `light_mode.svg` | Neofetch card — edit static fields here |
| `today.py` | Fetches GitHub stats via GraphQL |
| `.github/workflows/build.yaml` | Auto-update workflow |
| `cache/requirements.txt` | Python deps for Actions |

## Customize static text

Edit both SVG files (OS, Host, Languages, Contact, Focus…). Dynamic fields (`age_data`, `commit_data`, `repo_data`, etc.) are overwritten by `today.py`.

## Portfolio (separate repo)

The website lives in **`smyha/smyha.github.io`**.

| Plan | Portfolio repo | Published site |
|------|----------------|----------------|
| **GitHub Free** | Must be **public** | `https://smyha.github.io` |
| **GitHub Pro** | Can be **private** | Still public at same URL |
