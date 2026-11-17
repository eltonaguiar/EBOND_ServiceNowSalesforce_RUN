# EBOND lab run — screenshots

This repo holds the screenshots from one pass through the lab.

Lab: https://eltonaguiar.github.io/EBOND_ServiceNowSalesforce/

Code: https://github.com/eltonaguiar/EBOND_ServiceNowSalesforce

Do not commit passwords, tokens, consumer secrets, or session cookies. Cover them before you save the image.

Two kinds of image live here:

- `screenshots/from-chat/` — the authentic captures you sent in the chat, numbered in the order they were sent. These are the real screenshots.
- `screenshots/redrawn-stand-ins/` — caption cards a previous pass drew to stand in for missing screenshots. They are not real Salesforce or ServiceNow screens. They are parked here, out of the narrative, so nobody mistakes them for proof.

Each real screenshot below lists the steps that produced it and what it showcases. The mapping is by chat order, not by looking at the pixels.

## Lab 0 — Free instances

**Why.** Nothing else in the lab can be proven until both free accounts exist and you know the host each API will call. A wrong Salesforce host (Lightning instead of My Domain) fails every later call and looks like an auth bug.

### Real captures

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 000 | `from-chat/000-…EgGe69H.png` | Open your ServiceNow PDI instance page. | The instance URL and status. |
| 001 | `from-chat/001-…AZC2DAM.png` | Open your ServiceNow PDI instance page. | The instance URL and status. |
| 002 | `from-chat/002-…Brp6cmdM.png` | Salesforce → Setup → Quick Find `My Domain`. | The Salesforce My Domain API host, not the Lightning host. |

## Lab 1 — Table API

**Why.** The smallest proof that ServiceNow accepts an outside create. A 201 and a matching Incident mean the instance, the user, and the table are good before Salesforce is involved. If this fails, do not debug Flow or Apex yet.

### Real captures — REST API Explorer

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 003 | `from-chat/003-…Rviq0rj7.png` | Filter navigator → System Web Services → REST → REST API Explorer. | The explorer open, namespace `now`, Table API. |
| 004 | `from-chat/004-…apxdm0Kz.png` | Pick Create a record (POST), table `incident`, fill the request body. | The request body. One of these was sent empty; that is the skip-able one. |
| 005 | `from-chat/005-…LBAY4Df9Y0.png` | Same screen as 004. | The other request-body view. |
| 006–012 | `from-chat/006-…011-…`, `012-…Y0J07.png` | Click Send, then OK on the "Modifying data, confirm to continue" dialog. | The send result, the confirm dialog, and the response body with `result.number` and `result.sys_id`. |

### Real captures — the ticket

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 013 | `from-chat/013-…O7oFSpv.png` | Open the Incident list after the 201. | The new ticket row. |

### Real captures — a second create

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 014 | `from-chat/014-…a3p08B.png` | POST again, open the row in the classic form. | `INC0010003` form. |
| 015 | `from-chat/015-…rMMN7.png` | Filter the list to that number. | `INC0010003` filtered list. The `sys_id` comes from the URL, not the list. |

### Real captures — curl / PowerShell / Command Prompt

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 016 | `from-chat/016-…OOOAS.png` | Run the one-line curl in the Windows shell. | A successful create, password covered. |
| 017 | `from-chat/017-…YaF4Td.png` | Run the Linux curl example. | Linux success, password covered. |
| 018 | `from-chat/018-…P1.png` | Run `curl.exe -u admin` in Command Prompt. | Prompt-for-password success. |
| 019 | `from-chat/019-…iE2sTn.png` | Run `Invoke-RestMethod` with `Read-Host` in PowerShell. | PowerShell success. Password persists on screen; censored. |

## Lab 2 — Salesforce to ServiceNow

**Why.** The first real direction of the integration: a Case save creates one Incident and stamps it with the Case Id. The screenshots prove the credential is named, the correlation field is filled, and the Flow writes the Incident id back onto the Case.

### ServiceNow fields

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 020–022 | `from-chat/020-…022-…ndkv.png` | Open an Incident, then the form menu (three lines) → Configure → Table. | The Incident table config; Global application, extends Task. |
| 023 | `from-chat/023-…ePE6PG.png` | On the Columns related list, add the two custom columns. | `u_ebond_sf_case_id` and `u_sync_source` added. |

### Salesforce fields

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 024–026 | `from-chat/024-…026-…Cft7HlH.png` | Salesforce gear (top right) → Setup, not Setup for current app. | The gear and the Setup menu. |
| 027 | `from-chat/027-…v2p3urki8.png` | Object Manager → Case → Fields & Relationships → New → Text. Step 2 of 4. | The field details screen, where Extra Details lives. `Snow_Sys_Id__c` failed because you typed `__c`. |
| 028 | `from-chat/028-…7V3Yrg.png` | Step 4 of 4, add to page layouts. | The Case layouts, all checked. |

### Salesforce Cases and the new fields

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 029–032 | `from-chat/029-…032-…2nq.png` | Object Manager → Case → Fields & Relationships. | The three custom fields on the Case object. |
| 033–035 | `from-chat/033-…035-…knaY.png` | App launcher → Cases. | The Cases tab. |
| 036 | `from-chat/036-…Vkyu.png` | Open a Case. | The three new fields, highlighted. |
| 037 | `from-chat/037-…GWkdy.png` | Gear → Setup. | The Setup screen. |

### External Credential (created first)

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 038 | `from-chat/038-…HCKcjD.png` | Setup → Quick Find `named credentials` → Named Credentials → External Credentials tab → New. | The empty Named Credentials list. |
| 039 | `from-chat/039-…3NpVs.png` | Save the External Credential, then Principals → New. | The Create Principal form. |
| 040 | `from-chat/040-…d9gx.png` | External Credential Name field. | Label vs Name. The name must have no space. |
| 041–043 | `from-chat/041-…043-…lXws5l.png` | Principal form: sequence and identity type. | Sequence Number 1, Identity Type Named Principal. |
| 044–045 | `from-chat/044-…045-…99Wc.png` | Look for Manage Assignments on the principal. | There is no Manage Assignments button there. |

### Permission set (links the principal)

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 046–047 | `from-chat/046-…047-…adnW.png` | Top-right picture → your name → User Detail. | The user to assign, profile System Administrator. |
| 048–049 | `from-chat/048-…049-…83Pfs.png` | Setup → Users → Permission Sets → New. | License left `--None--`. |
| 050–051 | `from-chat/050-…051-…oODt.png` | Open the permission set → External Credential Principal Access. | The principal access section. |
| 052–054 | `from-chat/052-…054-…YMc5SX.png` | Edit → move `EBONDServiceNow - PDI_admin` to Enabled. | The principal enabled. |
| 055 | `from-chat/055-…GhDCCV.png` | After enabling. | Principal access saved. |
| 056–059 | `from-chat/056-…059-…aDt7U.png` | Manage Assignments → Add Assignment → check your user → Next → Assign. | One assignment to the System Administrator user. |

### Named Credential (created after)

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 060 | `from-chat/060-…VSy7Y.png` | Named Credentials tab → New. | The New Named Credential form. |
| 061–064 | `from-chat/061-…064-…5V6n.png` | Fill Name, URL, External Credential, Generate Authorization Header. | Name `EBOND_ServiceNow`, URL `https://dev296154.service-now.com/`, External Credential `EBOND ServiceNow`. |

### Flow

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 065–067 | `from-chat/065-…067-…Wm14.png` | The Flow vs Apex choice. | Which path, and the pros and cons. |
| 068–072 | `from-chat/068-…072-…uFPS.png` | Setup → Flows → New Flow → Record-Triggered Flow → Case → A record is created. Enable Add Asynchronous Path. | The async path, where the HTTP call goes. |
| 073 | `from-chat/073-…63kt.png` | Run Asynchronously → plus → Action → Create HTTP Callout. | The Create HTTP Callout link. |
| 074–075 | `from-chat/074-…075-…X6Q7.png` | New HTTP Callout: Name, Named Credential. | Name `EBONDCreateIncident`, no underscore. |
| 076–079 | `from-chat/076-…079-…QNH3G.png` | Configure Invocable Action: Label, method POST, path `/api/now/table/incident`. | The POST method and incident path. |
| 080–081 | `from-chat/080-…081-…0uYi.png` | The action panel: Label and Set Request Body. | What to fill in. |
| 082 | `from-chat/082-…LWnZ.png` | Sample JSON Request → paste → Review. | Review succeeded. |
| 083–086 | `from-chat/083-…086-…pcOL.png` | Select Sample Response Method → Use Example Response. | Not Connect for Schema. |
| 087 | `from-chat/087-…oXBL.png` | Sample JSON Response → Review. | `number` shows as String. That is correct; `INC0010002` is text. |
| 088–092 | `from-chat/088-…092-…TNVBR.png` | Save. The action lands on Run Asynchronously. | The action created. |
| 093 | `from-chat/093-…AL1s.png` | The action Label. | Labels are fine. |
| 094 | `from-chat/094-…vYqU.png` | Set Request Body → Value → + New Resource. | New Resource for the request body. |
| 095–096 | `from-chat/095-…096-…yZv3x.png` | New Resource: API Name `IncidentBody`. | The resource dialog. |
| 097 | `from-chat/097-…D6VOXs.png` | After Done, the body value is `IncidentBody`. | The body value. |
| 098–099 | `from-chat/098-…099-…X7qk.png` | Assignment. Close the action panel first. | The assignment is not inside the action panel. |
| 100–101 | `from-chat/100-…101-…BMhGD.png` | Plus above Create Incident → Assignment. | How to configure the assignment. |
| 102–103 | `from-chat/102-…103-…jss1lg.png` | Assignment: pick an IncidentBody field, not the whole resource. | Selecting one field per row. |
| 104 | `from-chat/104-…U87g7u.png` | Six Equals rows filled. | The assignment ready to save. |
| 105 | `from-chat/105-…si73c.png` | Save the flow. | The Save dialog: Label `EBOND Create Incident`, API Name `EBOND_Create_Incident`. |
| 106–110 | `from-chat/106-…110-…NJ64.png` | The flow canvas after save. | The flow canvas with Set Incident Body and Create Incident. |

### Update Records and the proof

| # | File | Steps to take it | What it showcases |
|---|------|------------------|-------------------|
| 111–112 | `from-chat/111-…112-…RXJ.png` | Plus under Create Incident → Update Records. | The Update Records element. |
| 113–119 | `from-chat/113-…119-…ZKNW.png` | Row 1: ServiceNow Sys Id = Create Incident → 2XX → result → sys_id. | The value picker. `sys_x5f_id` is `sys_id`. |
| 120–121 | `from-chat/120-…121-…RqH.png` | The right side of the rows. | Values come from Create Incident, not the triggering Case. |
| 122–123 | `from-chat/122-…123-…VeuyC.png` | Row 2: ServiceNow Number = result → number. | `z0number` is `number`. |
| 124 | `from-chat/124-…3ZvS.png` | Row 3: Sync Source. | Type `salesforce`, no quotes, lowercase. |
| 125 | `from-chat/125-…zW0.png` | The filled Update Records panel. | Ready to save and activate. |
| 126 | `from-chat/126-…ofBP19.png` | The panel with no Done button. | Close with X, then Save. |
| 127–131 | `from-chat/127-…131-…cocEk.png` | Save and Activate. | The active flow. |
| 132–136 | `from-chat/132-…136-…jzGFt.png` | App launcher → Cases → New. | The New Case form. Case Origin set to Web. |
| 137 | `from-chat/137-…dJ9IIM.png` | Save the Case. | Case created. |
| 138–140 | `from-chat/138-…140-…rmspGh.png` | Open the Case after the async call. | The ServiceNow fields filled on the Case. |
| 141 | `from-chat/141-…mFBr.png` | ServiceNow global search for that number. | Verifying the Incident in ServiceNow. |
| 142–151 | `from-chat/142-…151-…hmID7.png` | REST API Explorer GET, and the empty POST response. | `INC0010011` / `INC0010012` created by an empty POST. Impact and Urgency default to `3`. |
| 152–153 | `from-chat/152-…153-…KLC.png` | REST API Explorer method list. | The method list. POST creates a record. |
| 154–155 | `from-chat/154-…155-…I732.png` | Setup → Named Credentials → `EBOND_ServiceNow`. | The Named Credential detail, created after. |
| 156 | `from-chat/156-…JQRm.png` | Setup → External Credentials → `EBONDServiceNow`. | The External Credential detail, created first. |
| 157–158 | `from-chat/157-…158-…aZ.png` | Explorer Send on a write method. | The confirm dialog: Modifying data, confirm to continue. |
| 159 | `from-chat/159-…0zhK.png` | The file listing. | Where the duplicate screenshots showed up. |
| 160 | `from-chat/160-…vsp.png` | The folder structure. | Where the screenshots live on disk. |

## Lab 3 — ServiceNow to Salesforce

<details>
<summary>Not started yet</summary>

**Why.** One direction is not a bond. This will prove ServiceNow can call back and update the same Case, matched by `Snow_Sys_Id__c`, instead of creating a second Case.

No screenshots yet. Do this lab, then drop the captures here.

</details>

## Lab 4 — Ownership and loops

<details>
<summary>Not started yet</summary>

**Why.** Bidirectional sync fails when both sides copy every field. This will show which system owns the title and which owns state, and that one save does not bounce forever.

No screenshots yet.

</details>

## Lab 5 — Troubleshooting

<details>
<summary>Not started yet</summary>

**Why.** A clean run does not need a shot. If something failed, the before-and-after is the evidence it was diagnosed, not papered over.

No screenshots yet.

</details>

## Appendix — redrawn stand-ins (not real screens)

64 files in `screenshots/redrawn-stand-ins/`. A previous pass drew these caption cards to stand in for missing screenshots. They are not Salesforce or ServiceNow screens and must not be used as proof. They stay here out of the way.

## Appendix — full from-chat index

All 161 authentic captures are in `screenshots/from-chat/`, in the order they were sent. The tables above attach them to the lab step that produced them. Anything not matched above stays here for a later pass.

## Replace a placeholder

1. Take the screenshot.
2. Cover any secret.
3. Save over the file in `screenshots/` with the same name.
4. Commit only that image. Do not commit `.env`, pem files, or browser profiles.
