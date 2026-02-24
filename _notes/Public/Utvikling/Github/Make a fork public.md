Short answer: you cannot directly make a fork public while its upstream (parent) is private. You have three practical options:

1) Make the upstream repository public first
- If you (or the upstream repo owner) make the parent repository public, your fork will then be allowed to be public and you can change its visibility in Settings → Danger Zone → Change repository visibility → Make public.
- If you control the parent repo, this is the simplest route.

2) Ask GitHub Support to detach your fork from the private parent
- GitHub Support can “detach” a fork from its parent network. Once detached you can change visibility to public.
- Open a ticket here: https://support.github.com/contact and request that your fork (give full repo name/URL) be detached from its private parent so you can set visibility to public.
- Note: Support may ask why; they’ll need the repo name and details. This preserves issues/PRs? No — detaching preserves the git history but does not magically copy upstream issues/PRs from the private repo.

3) Create a new public repository and push your repository contents into it (recommended, fastest if you just want the code)
- This creates an independent public repo with your full git history, branches and tags. It does NOT preserve issues, PRs, watchers or stars from the fork network.
- Two common ways:

A — Mirror-push (preserves all refs: branches, tags, notes)
1. Create a new public repo on GitHub (via UI or gh CLI), e.g. https://github.com/kadalsaune/bildatabase-med-innlogging-losingsforslag (choose a name).
2. On your machine:
   - Clone mirror:
     git clone --mirror https://github.com/<your-account-or-fork-owner>/bildatabase-med-innlogging-losingsforslag.git
     cd bildatabase-med-innlogging-losingsforslag.git
   - Set the new repo as the push target:
     git remote set-url --push origin https://github.com/kadalsaune/bildatabase-med-innlogging-losingsforslag.git
   - Push everything:
     git push --mirror
   - If repo uses Git LFS, also:
     git lfs fetch --all
     git lfs push --all https://github.com/kadalsaune/bildatabase-med-innlogging-losingsforslag.git

B — Regular clone and push (simpler, if you don't need refs like reflogs or notes)
1. Create new public repo on GitHub.
2. On your machine:
   git clone https://github.com/<your-account-or-fork-owner>/bildatabase-med-innlogging-losingsforslag.git
   cd bildatabase-med-innlogging-losingsforslag
   git remote remove origin
   git remote add origin https://github.com/kadalsaune/bildatabase-med-innlogging-losingsforslag.git
   git push -u origin --all
   git push origin --tags
   If using LFS: git lfs fetch --all && git lfs push --all origin

What will and won’t be preserved
- Preserved: full commit history, branches, tags (if you push them), files, Git LFS objects (if you push LFS).
- Not preserved by a bare push: issues, pull requests, PR comments, watchers, stars, CI/Actions runs, project boards, release binaries (release metadata can be recreated but not transferred automatically).
- If you need issues/PRs migrated, you must export them (via API scripts or third-party tools) and recreate or import them in the new repo.

Which option to choose
- If you can ask the original owner to make the upstream public, do that (option 1).
- If you want the simplest direct control and only need the repo code/history, create a new public repo and mirror-push (option 3).
- If you need to keep the fork relationship and are blocked only by the fork-parent being private, contact GitHub Support to detach (option 2).

If you want, I can:
- walk you through any of the commands step-by-step in your environment, or
- draft the exact message to send to GitHub Support to request a fork detachment, or
- if you want me to create the new public repo and push for you, tell me which owner/org and whether you want me to use the same name — I’ll need permission and/or repository details to proceed.

Which path do you want to take?

