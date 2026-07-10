# Study Resources Rollout Plan (INTERNAL - do not upload)

> This file is for planning only. It is excluded from the public repo via `.gitignore`. Do not publish it.

All 96 cheatsheets are generated locally, but we **upload them in batches over time**, not all on one day.

## Why phased
- **SEO:** a steady stream of new pages signals an active, maintained resource. Google favors consistent
  freshness over a one-time dump; 96 pages appearing in one commit can look low-effort or scraped.
- **Credibility:** a repo with regular commits reads as maintained, not dump-and-abandon.
- **Shareable moments:** each new cheatsheet is a fresh reason to help in a relevant thread (later, in comments).
- **Quality control:** you review each batch (accuracy, no client data, no braindumps) instead of rushing 96 at once.

## Cadence
- **2-3 cheatsheets per week**, on different days (e.g., Mon / Wed / Fri), each as its own small commit.
- Full rollout takes roughly **8-12 weeks**.
- Regenerate anytime: `node scripts/generate-study-resources.cjs` (add `--force` to refresh all).
- Upload only the current batch's folders each time (see mechanic below).

## Phase order (fundamentals first - beginner audience = free-plan sweet spot)

| Phase | Timing | Publish |
|---|---|---|
| 1 | Week 1 | ai901, az900, + Azure roadmap (`certifications/roadmaps/azure.md`) |
| 2 | Week 2 | dp900, sc900, aws-clf, gcp-cdl (remaining fundamentals) |
| 3 | Weeks 3-4 | az104, az305, az500, aws-saa (popular associates/expert) |
| 4 | Weeks 5-8 | rest of Microsoft + AWS + Google Cloud associate/pro exams |
| 5 | Weeks 9-12 | Security, Cisco, Cloud Native / Kubernetes, Linux, Citrix, Nutanix, VMware |
| 6 | Ongoing | checklists, then kubernetes manifests + IaC (smaller, more advanced audience) |

## Upload mechanic (per batch)
```powershell
# In the cloned study-resources repo (NOT the app repo):
# copy only this batch's folders in, then:
git add certifications/microsoft/az900 certifications/roadmaps
git commit -m "Add AZ-900 cheatsheet + Azure roadmap"
git push
```
Keep commits small and descriptive ("Add AZ-900 cheatsheet"), one batch at a time.

## Reddit tie-in
- Do NOT share links on Reddit until the u/certgrid account is warmed up (see `../marketing/reddit/Reddit-Setup.md`).
- Once warmed up, mention a relevant cheatsheet **in comments** when someone asks - one at a time, disclosed.

## Do NOT
- Do not push all 96 in a single commit or on the same day.
- Do not share the same link across multiple subreddits in a short window.
- Do not upload this ROLLOUT.md or any file with client data / real exam questions.
