# EBOND lab run — screenshot placeholders

This repo holds the screenshots from one pass through the lab. The boxes below are placeholders. Replace each file with the real capture, same filename, after you finish that step.

Lab: https://eltonaguiar.github.io/EBOND_ServiceNowSalesforce/

Code: https://github.com/eltonaguiar/EBOND_ServiceNowSalesforce

Do not commit passwords, tokens, consumer secrets, or session cookies. Cover them before you save the image.

This README is the page for now. A GitHub Pages site can be added later from these same files; do not turn that on until the placeholders have been replaced.

## Lab 0 — Free instances

**Why.** Nothing else in the lab can be proven until both free accounts exist and you know the host each API will call. A wrong Salesforce host (Lightning instead of My Domain) fails every later call and looks like an auth bug.

| File | What to capture |
|------|-----------------|
| `screenshots/00-pdi-url.png` | Captured. Instance `dev296154`, Australia, Online, user `admin`. Password masked. |
| `screenshots/00-salesforce-mydomain.png` | Captured. Developer Edition welcome on the Lightning host. API host is `orgfarm-e1f47f3d5e-dev-ed.develop.my.salesforce.com`. |

![PDI instance dev296154, password masked](screenshots/00-pdi-url.png)

![Salesforce Developer Edition welcome](screenshots/00-salesforce-mydomain.png)

## Lab 1 — Table API

**Why.** This is the smallest proof that ServiceNow accepts an outside create. A 201 and a matching Incident mean the instance, the user, and the table are good before Salesforce is involved. If this fails, do not debug Flow or Apex yet.

| File | What to capture |
|------|-----------------|
| `screenshots/01-explorer-201.png` | REST API Explorer, POST incident, status 201, INC number visible. |
| `screenshots/01-incident-list.png` | Incident list with that same number. |

![Explorer 201 placeholder](screenshots/01-explorer-201.png)

![Incident list placeholder](screenshots/01-incident-list.png)

## Lab 2 — Salesforce to ServiceNow

**Why.** This is the first real direction of the integration: a Case save creates one Incident and stores the Case Id on it. The screenshots prove the credential is named, the correlation field is filled, and a second save would update instead of duplicating.

| File | What to capture |
|------|-----------------|
| `screenshots/02-case-fields.png` | Case fields `Snow_Sys_Id__c`, `Snow_Number__c`, `Snow_Sync_Source__c`. |
| `screenshots/02-named-credential.png` | Named Credential `EBOND_ServiceNow`. No secret in the frame. |
| `screenshots/02-case-and-incident.png` | The Case, and the Incident whose `u_ebond_sf_case_id` matches the Case Id. |

![Case fields placeholder](screenshots/02-case-fields.png)

![Named Credential placeholder](screenshots/02-named-credential.png)

![Case and Incident placeholder](screenshots/02-case-and-incident.png)

## Lab 3 — ServiceNow to Salesforce

**Why.** One direction is not a bond. This proves ServiceNow can call back and update the same Case, matched by `Snow_Sys_Id__c`, instead of creating a second Case. The 200 and the single Case update are the proof.

| File | What to capture |
|------|-----------------|
| `screenshots/03-external-client-app.png` | External Client App. Consumer secret covered. |
| `screenshots/03-rest-message-200.png` | REST Message `patch_case` test, HTTP 200. |
| `screenshots/03-case-after-update.png` | Case after the Incident change. One update, not a stream. |

![External Client App placeholder](screenshots/03-external-client-app.png)

![REST Message 200 placeholder](screenshots/03-rest-message-200.png)

![Case after update placeholder](screenshots/03-case-after-update.png)

## Lab 4 — Ownership and loops

**Why.** Bidirectional sync fails in production when both sides copy every field. This lab is where you show which system owns the title and which owns state, and that one save does not bounce forever.

| File | What to capture |
|------|-----------------|
| `screenshots/04-ownership.png` | A note or form that shows Salesforce owns the title and ServiceNow owns state. |

![Ownership placeholder](screenshots/04-ownership.png)

## Lab 5 — Troubleshooting

**Why.** A clean run does not need a shot. If something failed, the before-and-after is the evidence that the failure was diagnosed (asleep instance, wrong host, missing principal access, callout before the save committed) and not papered over.

| File | What to capture |
|------|-----------------|
| `screenshots/05-troubleshooting.png` | Optional. One failure you actually hit, and the screen after the fix. Leave the placeholder if the run was clean. |

![Troubleshooting placeholder](screenshots/05-troubleshooting.png)

## Also useful

Not required. Take these if the screen is already open.

![My Domain API host](screenshots/00-my-domain.png)

| Suggested file | Why |
|----------------|-----|
| `screenshots/00-my-domain.png` | Captured. Current My Domain URL `orgfarm-e1f47f3d5e-dev-ed.develop.my.salesforce.com`. |
| `screenshots/02-principal-access.png` | Permission set granting External Credential Principal Access. This is the usual Lab 2 miss. |
| `screenshots/02-incident-fields.png` | Incident columns `u_ebond_sf_case_id` and `u_sync_source`. |
| `screenshots/04-syslog-one-write.png` | `syslog.list` filtered to EBOND, one write, not a loop. |

## Replace a placeholder

1. Take the screenshot.
2. Cover any secret.
3. Save over the file in `screenshots/` with the same name.
4. Commit only that image. Do not commit `.env`, pem files, or browser profiles.
