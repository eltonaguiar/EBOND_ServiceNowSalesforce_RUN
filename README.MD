# EBOND lab run — screenshots
Lab: https://eltonaguiar.github.io/EBOND_ServiceNowSalesforce/
Code: https://github.com/eltonaguiar/EBOND_ServiceNowSalesforce
Do not commit passwords, tokens, consumer secrets, or session cookies. Cover them before you save the image.
- `screenshots/from-chat/` — authentic captures from the chat, numbered in the order they were sent.
- `screenshots/redrawn-stand-ins/` — caption cards a previous pass drew to stand in for missing screenshots. Not real screens. Parked out of the narrative.
Each screenshot lists the steps that produced it and what it showcases. Mapping is by chat order.

## Lab 0 — Free instances
**Why.** Nothing else can be proven until both free accounts exist and you know the host each API will call. A wrong Salesforce host (Lightning instead of My Domain) fails every later call.
![ServiceNow PDI instance](screenshots/from-chat/000-1794866651343-prt_1e663a0b4001NpUiTNuEgGe69H.png)

Steps: open your ServiceNow PDI instance page. Showcases: the instance URL and status.
![ServiceNow PDI instance (2)](screenshots/from-chat/001-1794866651346-prt_1e663a0b5001tgOScshAZC2DAM.png)

Steps: open your ServiceNow PDI instance page. Showcases: the instance URL and status.
![Salesforce My Domain](screenshots/from-chat/002-1794867560432-prt_1e6717fdb0012ersEvBrp6cmdM.png)

Steps: Salesforce → Setup → Quick Find My Domain. Showcases: the API host, not Lightning.

## Lab 1 — Table API
**Why.** The smallest proof ServiceNow accepts an outside create. A 201 and a matching Incident mean the instance, the user, and the table are good before Salesforce is involved.
#### REST API Explorer
![Explorer open](screenshots/from-chat/003-1794869097707-prt_1e688f4bf001UpdYElRviq0rj7.png)

Steps: System Web Services → REST → REST API Explorer. Showcases: namespace now, Table API.
![Explorer request body](screenshots/from-chat/004-1794869097710-prt_1e688f4bf0029wCaE7apxdm0Kz.png)

Steps: Create a record (POST), table incident, fill body. Showcases: the request body. One of these was sent empty; that one is skip-able.
![Explorer request body (2)](screenshots/from-chat/005-1794869097711-prt_1e688f4c00017uOkLBAY4Df9Y0.png)

Steps: same screen as above. Showcases: another request-body view.
![Confirm dialog](screenshots/from-chat/006-1794869301757-prt_1e68c11e70013mP8p0wA5WPLHU.png)

Steps: after Send, the browser asks Modifying data, confirm to continue. Showcases: the confirm dialog before the write.
![After OK](screenshots/from-chat/007-1794869301760-prt_1e68c11e7002TOLN4N2qm8IWUE.png)

Steps: click OK on the confirm dialog. Showcases: the run after confirming.
![Response body](screenshots/from-chat/008-1794869301762-prt_1e68c11e7003B1TVqPvdpeodmf.png)

Steps: click OK. Showcases: the response body.
![Response body (2)](screenshots/from-chat/009-1794869301763-prt_1e68c11e70043HHYp6Ww6hoNOJ.png)

Steps: click OK. Showcases: response body with result.number and result.sys_id.
![201 Created](screenshots/from-chat/010-1794869301764-prt_1e68c11e7005Bn1ZrQpucbtdQk.png)

Steps: Send. Showcases: status 201.
![201 Created (2)](screenshots/from-chat/011-1794869301765-prt_1e68c11e8001fp2tBonIVC0hVk.png)

Steps: Send. Showcases: status 201.
![Response result](screenshots/from-chat/012-1794869301768-prt_1e68c11e8002q88L84hitY0J07.png)

Steps: after OK. Showcases: result.number and result.sys_id.
![Ticket list](screenshots/from-chat/013-1794869494374-prt_1e68f02630010BOICQ5O7oFSpv.png)

Steps: open the Incident list after the 201. Showcases: the new ticket row.
#### Second create
![INC0010003 form](screenshots/from-chat/014-1794869754173-prt_1e692f938001hyY9Jiz1a3p08B.png)

Steps: POST again, open the row in the classic form. Showcases: the form. sys_id comes from the URL.
![INC0010003 filtered list](screenshots/from-chat/015-1794869754175-prt_1e692f938002HG4IFM7frpMMN7.png)

Steps: filter the list to that number. Showcases: the filtered list.
#### curl / PowerShell / Command Prompt
![Windows curl success](screenshots/from-chat/016-1794870299716-prt_1e69b4c41001maTUydAR6OOOAS.png)

Steps: run the one-line curl in the Windows shell. Showcases: a successful create, password covered.
![Linux curl success](screenshots/from-chat/017-1794870660967-prt_1e6a0cf63001XsRrwDK5YaF4Td.png)

Steps: run the Linux curl example. Showcases: Linux success, password covered.
![Command Prompt curl](screenshots/from-chat/018-1794870707213-prt_1e6a18409001VeQYfUBKZGueP1.png)

Steps: run curl.exe -u admin in Command Prompt. Showcases: prompt-for-password success.
![PowerShell success](screenshots/from-chat/019-1794870784847-prt_1e6a2b34c001HrzI6Z18iE2sTn.png)

Steps: run Invoke-RestMethod with Read-Host in PowerShell. Showcases: PowerShell success. Password censored.

## Lab 2 — Salesforce to ServiceNow
**Why.** The first real direction: a Case save creates one Incident and stamps it with the Case Id. The screenshots prove the credential is named, the correlation field is filled, and the Flow writes the Incident id back onto the Case.
### ServiceNow fields
![Incident table config](screenshots/from-chat/020-1794871876192-prt_1e6b35a4d001UgUZxoqtaFO0my.png)

Steps: open an Incident → form menu (three lines) → Configure → Table. Showcases: Global application, extends Task.
![Incident table config (2)](screenshots/from-chat/021-1794871876197-prt_1e6b35a4e001t4PGYd8T21jm7H.png)

Steps: Configure → Table. Showcases: the table.
![Incident table config (3)](screenshots/from-chat/022-1794871876201-prt_1e6b35a4e002rIZ8L5ISL1ndkv.png)

Steps: Configure → Table. Showcases: the table.
![Custom columns added](screenshots/from-chat/023-1794871924553-prt_1e6b417450017mfeIB2UePE6PG.png)

Steps: Columns related list → New. Showcases: u_ebond_sf_case_id and u_sync_source.
### Salesforce fields
![Gear icon](screenshots/from-chat/024-1794872325333-prt_1e6ba34cb001lKDHh4zTju7OUt.png)

Steps: Salesforce gear (top right). Showcases: the gear.
![Setup menu](screenshots/from-chat/025-1794872325335-prt_1e6ba34cb002L17WNZr93sbL1w.png)

Steps: click Setup, not Setup for current app. Showcases: the Setup menu.
![Setup menu (2)](screenshots/from-chat/026-1794872325337-prt_1e6ba34cc001ic4zETcCft7HlH.png)

Steps: Gear → Setup. Showcases: Setup.
![Field details step](screenshots/from-chat/027-1794875101317-prt_1e6e4907b001H6hAvh2p3urki8.png)

Steps: Object Manager → Case → Fields & Relationships → New → Text, Step 2 of 4. Showcases: the details screen. Snow_Sys_Id__c failed because you typed __c.
![Case layouts](screenshots/from-chat/028-1794875148052-prt_1e6e54710001B5Ja5K5X7V3Yrg.png)

Steps: Step 4 of 4, add to page layouts. Showcases: all Case layouts checked.
### Cases and the new fields
![Case object fields](screenshots/from-chat/029-1794881670689-prt_1e748ce140010vgxim2wr0xykL.png)

Steps: Object Manager → Case → Fields & Relationships. Showcases: the three custom fields.
![Case object fields (2)](screenshots/from-chat/030-1794881670692-prt_1e748ce1500150aGD7t6aqcf30.png)

Steps: Fields & Relationships. Showcases: the fields.
![Case object fields (3)](screenshots/from-chat/031-1794881670694-prt_1e748ce15002V1rfBSQGBzB529.png)

Steps: Fields & Relationships. Showcases: the fields.
![Case object fields (4)](screenshots/from-chat/032-1794881670696-prt_1e748ce16001TLCFtBv3p5W2nq.png)

Steps: Fields & Relationships. Showcases: the fields.
![Cases tab](screenshots/from-chat/033-1794889325420-prt_1e7bd9b61001fThXoXu8A0nDCy.png)

Steps: App launcher → Cases. Showcases: the Cases tab.
![Cases tab (2)](screenshots/from-chat/034-1794889325422-prt_1e7bd9b62001xFaV5mjdn7i7nt.png)

Steps: App launcher → Cases. Showcases: Cases.
![Cases tab (3)](screenshots/from-chat/035-1794889325424-prt_1e7bd9b62002ML72UEqeKDknaY.png)

Steps: App launcher → Cases. Showcases: Cases.
![New fields highlighted](screenshots/from-chat/036-1794889362052-prt_1e7be2a7f001pfygP3xge4Vkyu.png)

Steps: open a Case. Showcases: the three new fields highlighted.
![Setup screen](screenshots/from-chat/037-1794889427195-prt_1e7bf28f7001ee7NqMH9LGWkdy.png)

Steps: Gear → Setup. Showcases: Setup.
### External Credential (created first)
![Named Credentials empty](screenshots/from-chat/038-1794889460242-prt_1e7bfaa0f001LnEWTlAxHCKcjD.png)

Steps: Setup → Quick Find named credentials → External Credentials tab → New. Showcases: the empty list.
![Create Principal form](screenshots/from-chat/039-1794889603915-prt_1e7c1db48001Q8wJQCKNa3NpVs.png)

Steps: save the External Credential, then Principals → New. Showcases: the create principal form.
![Label vs Name](screenshots/from-chat/040-1794889664424-prt_1e7c2c7a6001DLrmFeXANid9gx.png)

Steps: the External Credential name field. Showcases: name must have no space.
![Principal sequence](screenshots/from-chat/041-1794889749403-prt_1e7c41396001AOZcsTtqBK1VvI.png)

Steps: principal form. Showcases: sequence number.
![Identity type](screenshots/from-chat/042-1794889749404-prt_1e7c41396002Gemhs53WyG1UbT.png)

Steps: principal form. Showcases: Identity Type Named Principal.
![Principal form (3)](screenshots/from-chat/043-1794889749405-prt_1e7c41396003dUlA0WuFlXws5l.png)

Steps: principal form. Showcases: the fields.
![Manage Assignments hunt](screenshots/from-chat/044-1794889832919-prt_1e7c559d5001gJC0bSrS4OluKb.png)

Steps: look for Manage Assignments on the principal. Showcases: it is not there.
![Manage Assignments hunt (2)](screenshots/from-chat/045-1794889858858-prt_1e7c5bf24001aBG4WUlVP899Wc.png)

Steps: as above. Showcases: it is not there.
### Permission set (links the principal)
![User detail](screenshots/from-chat/046-1794890116802-prt_1e7c9aebb0012zI2Iysmb2cJ0N.png)

Steps: top-right picture → your name → User Detail. Showcases: the user to assign, System Administrator.
![User detail (2)](screenshots/from-chat/047-1794890116805-prt_1e7c9aebb002h0lTGN1CYgadnW.png)

Steps: as above. Showcases: the user.
![Permission Sets](screenshots/from-chat/048-1794890174307-prt_1e7ca8f60001tBQpW4JyirILRO.png)

Steps: Setup → Users → Permission Sets → New. Showcases: license stays --None--.
![Permission Sets (2)](screenshots/from-chat/049-1794890174308-prt_1e7ca8f60002725XHMpRI83Pfs.png)

Steps: Permission Sets. Showcases: the list.
![External Credential Principal Access](screenshots/from-chat/050-1794890237412-prt_1e7cb85df001gMsNC8q0KzdWje.png)

Steps: open the permission set → External Credential Principal Access. Showcases: the section.
![Principal access (2)](screenshots/from-chat/051-1794890237414-prt_1e7cb85df002C9MAdRden9oODt.png)

Steps: as above. Showcases: the section.
![Edit principal access](screenshots/from-chat/052-1794890325034-prt_1e7ccdc23001Qs54TUpYF4diZK.png)

Steps: Edit. Showcases: the edit screen.
![Principal enabled](screenshots/from-chat/053-1794890325035-prt_1e7ccdc23002WZaShyf0VMAdmc.png)

Steps: move EBONDServiceNow - PDI_admin to Enabled. Showcases: the principal enabled.
![Principal enabled (2)](screenshots/from-chat/054-1794890325036-prt_1e7ccdc230034qk58sNPYMc5SX.png)

Steps: as above. Showcases: enabled.
![Principal access saved](screenshots/from-chat/055-1794890341575-prt_1e7cd1cc2001avRqBiVLGhDCCV.png)

Steps: Save. Showcases: principal access saved.
![Manage Assignments](screenshots/from-chat/056-1794890458606-prt_1e7cee5e300126O55CHpuQGIzk.png)

Steps: Manage Assignments → Add Assignment. Showcases: the assignment screen.
![Add Assignment](screenshots/from-chat/057-1794890458607-prt_1e7cee5e3002djRGVAatt8eBh6.png)

Steps: Add Assignment. Showcases: choose the user.
![Assignment check user](screenshots/from-chat/058-1794890458608-prt_1e7cee5e4001iUixmb3LuZgAFL.png)

Steps: check your user, Next. Showcases: the user checked.
![Assignment done](screenshots/from-chat/059-1794890458609-prt_1e7cee5e40020UivK7PaoaDt7U.png)

Steps: Assign. Showcases: one assignment.
### Named Credential (created after)
![New Named Credential](screenshots/from-chat/060-1794890552647-prt_1e7d05544001Eizb6cRReVSy7Y.png)

Steps: Named Credentials tab → New. Showcases: the form.
![Named Credential name](screenshots/from-chat/061-1794890632010-prt_1e7d18b3e001tJWNYnw25Hy7GR.png)

Steps: fill Name. Showcases: EBOND_ServiceNow.
![Named Credential URL](screenshots/from-chat/062-1794890632012-prt_1e7d18b3f0010Q6juHelIBgWx6.png)

Steps: fill URL. Showcases: https://dev296154.service-now.com/.
![External Credential on Named](screenshots/from-chat/063-1794890632013-prt_1e7d18b3f002k9xb7FJJ10sAqi.png)

Steps: External Credential field. Showcases: EBOND ServiceNow.
![Generate Authorization Header](screenshots/from-chat/064-1794890684715-prt_1e7d25928001oMQU3IYK7X5V6n.png)

Steps: check Generate Authorization Header. Showcases: the box checked.
### Flow
![Flow vs Apex](screenshots/from-chat/065-1794890767241-prt_1e7d39b81001N1DNOncjtAaPRO.png)

Steps: the path choice. Showcases: which path, pros and cons.
![Flow choice (2)](screenshots/from-chat/066-1794890767242-prt_1e7d39b82001t1hzpih11MydpH.png)

Steps: as above. Showcases: the choice.
![Flow choice (3)](screenshots/from-chat/067-1794890980503-prt_1e7d6dc92001DJ4RlUNE62Wm14.png)

Steps: as above. Showcases: the choice.
![Async path](screenshots/from-chat/068-1794891315960-prt_1e7dbfae1001D3yYRHY58GATgs.png)

Steps: Setup → Flows → New Flow → Record-Triggered Flow → Case → A record is created. Enable Add Asynchronous Path. Showcases: the async path.
![Async path (2)](screenshots/from-chat/069-1794891315964-prt_1e7dbfae2001obhLo97Gb40Ts8.png)

Steps: enable the slider. Showcases: Add Asynchronous Path on.
![Async path (3)](screenshots/from-chat/070-1794891315966-prt_1e7dbfae2002pFGG1O26KTcoc5.png)

Steps: as above. Showcases: async path.
![Async path (4)](screenshots/from-chat/071-1794891315968-prt_1e7dbfae2003pQiDTHcokJQf8c.png)

Steps: as above. Showcases: async path.
![Async path (5)](screenshots/from-chat/072-1794891315970-prt_1e7dbfae2004l2yd3wd6FjuFPS.png)

Steps: as above. Showcases: async path.
![Create HTTP Callout link](screenshots/from-chat/073-1794891336952-prt_1e7dc4cf5001pWbdNSYuBE63kt.png)

Steps: Run Asynchronously → plus → Action → Create HTTP Callout. Showcases: the link.
![New HTTP Callout name](screenshots/from-chat/074-1794891432019-prt_1e7ddc04b001RGatpmc12UMry2.png)

Steps: Name field. Showcases: EBONDCreateIncident, no underscore.
![Named Credential on callout](screenshots/from-chat/075-1794891432020-prt_1e7ddc04b002wT2EPUvf8Ox6Q7.png)

Steps: Named Credential field. Showcases: EBOND_ServiceNow.
![Configure Invocable Action](screenshots/from-chat/076-1794891467421-prt_1e7de4a95001Zx4tTrqPSg1QSQ.png)

Steps: Label, method, path. Showcases: the configure screen.
![Method POST](screenshots/from-chat/077-1794891491548-prt_1e7dea8d8001Jm3X41OdIcXNwd.png)

Steps: method field. Showcases: POST.
![Path](screenshots/from-chat/078-1794891567794-prt_1e7dfd2ad001cE6V5U5eWC2qHE.png)

Steps: path field. Showcases: /api/now/table/incident.
![Configure (4)](screenshots/from-chat/079-1794891576654-prt_1e7dff549001RpGNdxGIhQNH3G.png)

Steps: as above. Showcases: the config.
![Action label](screenshots/from-chat/080-1794891676363-prt_1e7e17ac3001zzNA5Z4LOkW3w4.png)

Steps: the Label box. Showcases: what to fill in.
![Action body](screenshots/from-chat/081-1794891731186-prt_1e7e250ed001PU4vEmR1Ac0uYi.png)

Steps: Set Request Body. Showcases: the body field.
![Review sample request](screenshots/from-chat/082-1794891781869-prt_1e7e316e8001o9WYhoB7PiLWnZ.png)

Steps: Sample JSON Request → paste → Review. Showcases: review.
![Review succeeded](screenshots/from-chat/083-1794891818645-prt_1e7e3a68d001VBimh3sEVTV2Q3.png)

Steps: after Review. Showcases: Data Structure lists fields.
![Review (2)](screenshots/from-chat/084-1794891818646-prt_1e7e3a68d0020sfwepKZAv5HyO.png)

Steps: as above. Showcases: the review result.
![Use Example Response](screenshots/from-chat/085-1794891840239-prt_1e7e3faea0013zEoss9JCenizV.png)

Steps: Select Sample Response Method → Use Example Response. Showcases: not Connect for Schema.
![Example Response selected](screenshots/from-chat/086-1794891858374-prt_1e7e441be001it2EoMPp2GpcOL.png)

Steps: pick Use Example Response. Showcases: selected.
![number is String](screenshots/from-chat/087-1794891953289-prt_1e7e5b4810013zMszDWGm2oXBL.png)

Steps: Sample JSON Response → Review. Showcases: number shows as String. That is correct.
![Save response](screenshots/from-chat/088-1794891989529-prt_1e7e6420e001OvMI2H4Um79ADG.png)

Steps: click Save. Showcases: the response screen.
![Save (2)](screenshots/from-chat/089-1794891989530-prt_1e7e6420f001qh5S0QmKGozjiQ.png)

Steps: Save. Showcases: save.
![Action created](screenshots/from-chat/090-1794892077853-prt_1e7e79b11001HQuAUORYbrWI7L.png)

Steps: Save. Showcases: the action on Run Asynchronously.
![Action created (2)](screenshots/from-chat/091-1794892077855-prt_1e7e79b1100206NfyBWm4Cyh1x.png)

Steps: as above. Showcases: action created.
![Action created (3)](screenshots/from-chat/092-1794892077856-prt_1e7e79b11003CHg3XXK4qTNVBR.png)

Steps: as above. Showcases: action created.
![Labels fine](screenshots/from-chat/093-1794892107781-prt_1e7e80fff001BoS15ZsCV0AL1s.png)

Steps: the action label. Showcases: labels are fine.
![New Resource](screenshots/from-chat/094-1794892225661-prt_1e7e9dc7a001LEEyLVzQOFvYqU.png)

Steps: Set Request Body → Value → + New Resource. Showcases: the menu.
![Resource dialog](screenshots/from-chat/095-1794892328685-prt_1e7eb6ee5001lp63B3NrpUKNiG.png)

Steps: New Resource. Showcases: the dialog.
![Resource dialog (2)](screenshots/from-chat/096-1794892328687-prt_1e7eb6ee5002uLI4kAQXzuZv3x.png)

Steps: API Name IncidentBody. Showcases: the dialog.
![Body value IncidentBody](screenshots/from-chat/097-1794892352323-prt_1e7ebcb40001YL4SIaS4D6VOXs.png)

Steps: after Done. Showcases: the body value.
![Assignment not in panel](screenshots/from-chat/098-1794892388464-prt_1e7ec586c001SdMjSZ847uw6E0.png)

Steps: the action panel. Showcases: assignment is not inside the panel.
![Close panel](screenshots/from-chat/099-1794892433961-prt_1e7ed0a1b001JZM9vZ5XD8X7qk.png)

Steps: close the panel. Showcases: how to leave the panel.
![Assignment plus](screenshots/from-chat/100-1794892489380-prt_1e7ede2a1001ZQkg3blHW17QZ1.png)

Steps: plus above Create Incident → Assignment. Showcases: the plus.
![Choose Assignment](screenshots/from-chat/101-1794892547908-prt_1e7eec73c001kA4KnelcgBMhGD.png)

Steps: click Assignment. Showcases: how to configure.
![Pick IncidentBody field](screenshots/from-chat/102-1794892639177-prt_1e7f02bc3001adTpjualHXig6H.png)

Steps: assignment row. Showcases: pick one field, not the whole resource.
![Pick field (2)](screenshots/from-chat/103-1794892639178-prt_1e7f02bc30026Wyis3CBjss1lg.png)

Steps: as above. Showcases: one field per row.
![Assignment filled](screenshots/from-chat/104-1794892888872-prt_1e7f3fb21001yZML9dd9U87g7u.png)

Steps: six Equals rows. Showcases: ready to save.
![Save flow dialog](screenshots/from-chat/105-1794892922751-prt_1e7f47f7d001LQ1LVNm5tsi73c.png)

Steps: Save. Showcases: Label EBOND Create Incident, API Name EBOND_Create_Incident.
![Flow canvas](screenshots/from-chat/106-1794892981054-prt_1e7f5632b001c7vvuXbfPP2Gco.png)

Steps: after save. Showcases: the canvas.
![Flow canvas (2)](screenshots/from-chat/107-1794892981056-prt_1e7f5632b002AJwJxqCzrLcXbV.png)

Steps: after save. Showcases: the canvas with Set Incident Body and Create Incident.
![Flow canvas (3)](screenshots/from-chat/108-1794892981063-prt_1e7f5632b003ZYVigWLUKUp7dN.png)

Steps: after save. Showcases: the canvas.
![Flow canvas (4)](screenshots/from-chat/109-1794893066778-prt_1e7f6b214001zhE5VMDzJod0ht.png)

Steps: after save. Showcases: the canvas.
![Flow diagram](screenshots/from-chat/110-1794893263682-prt_1e7f9b33d001V3aauFWwgrNJ64.png)

Steps: the flow builder. Showcases: the full flow.
### Update Records and the proof
![Update Records element](screenshots/from-chat/111-1794893464153-prt_1e7fcc250001BOcwCnSzHOWzUC.png)

Steps: plus under Create Incident → Update Records. Showcases: the element.
![Update Records (2)](screenshots/from-chat/112-1794893464155-prt_1e7fcc250002yKcQRbjCXffRXJ.png)

Steps: as above. Showcases: the element.
![Row 1 value picker](screenshots/from-chat/113-1794893716637-prt_1e8009c92001XOJm5K3FSdl2vN.png)

Steps: ServiceNow Sys Id = Create Incident → 2XX → result → sys_id. Showcases: the picker. sys_x5f_id is sys_id.
![Row 1 (2)](screenshots/from-chat/114-1794893716638-prt_1e8009c930012eLLQxXZrYdc4v.png)

Steps: as above. Showcases: the picker.
![Row 1 (3)](screenshots/from-chat/115-1794893716639-prt_1e8009c93002rreFlqHcPpZPIc.png)

Steps: as above. Showcases: the picker.
![Row 1 (4)](screenshots/from-chat/116-1794893716639-prt_1e8009c930030FAR9vSveNpMFG.png)

Steps: as above. Showcases: the picker.
![Row 1 (5)](screenshots/from-chat/117-1794893716640-prt_1e8009c93004ZsdYibnne6AgWL.png)

Steps: as above. Showcases: the picker.
![Row 1 (6)](screenshots/from-chat/118-1794893716640-prt_1e8009c930058FVlWE2poAFIQ0.png)

Steps: as above. Showcases: the picker.
![Row 1 (7)](screenshots/from-chat/119-1794893716642-prt_1e8009c93006OjwZ7wCGulZKNW.png)

Steps: as above. Showcases: the picker.
![Right side source](screenshots/from-chat/120-1794893762928-prt_1e801516d001JUtBxn3nwMLzky.png)

Steps: the right side of the rows. Showcases: values come from Create Incident, not the triggering Case.
![Right side (2)](screenshots/from-chat/121-1794893762929-prt_1e801516d002avdDRKDSswlRqH.png)

Steps: as above. Showcases: the source.
![Row 2](screenshots/from-chat/122-1794893799812-prt_1e801e17c0016UdhUgX2Rma6yN.png)

Steps: ServiceNow Number = result → number. Showcases: z0number is number.
![Row 2 (2)](screenshots/from-chat/123-1794893799814-prt_1e801e17c002Uu4Bg7MpNVeuyC.png)

Steps: as above. Showcases: the picker.
![Sync Source row](screenshots/from-chat/124-1794893837017-prt_1e80272d5001QxXadBS2rj3ZvS.png)

Steps: Row 3, Sync Source. Showcases: type salesforce, no quotes, lowercase.
![Update Records filled](screenshots/from-chat/125-1794893907937-prt_1e80387dd001mKkEtqFNeNStzW.png)

Steps: all three rows. Showcases: ready to save and activate.
![No Done button](screenshots/from-chat/126-1794893922273-prt_1e803bfd90018RfC0ZFAofBP19.png)

Steps: the panel. Showcases: close with X, then Save.
![Flow save](screenshots/from-chat/127-1794893951805-prt_1e8043337001kkcZyLYS3ZTbW0.png)

Steps: Save. Showcases: the save.
![Flow save (2)](screenshots/from-chat/128-1794893951806-prt_1e8043338001YC1zyt5RE7d6KH.png)

Steps: Save. Showcases: the save.
![Activate](screenshots/from-chat/129-1794893976731-prt_1e8049497001hqoSpU7pP9AT74.png)

Steps: Activate. Showcases: activation.
![Activate (2)](screenshots/from-chat/130-1794893976731-prt_1e80494970026h3kpTQHX0HTc6.png)

Steps: Activate. Showcases: activation.
![Active flow](screenshots/from-chat/131-1794893976732-prt_1e8049497003q3YfZS3ZHcocEk.png)

Steps: after activate. Showcases: the active flow.
![New Case form](screenshots/from-chat/132-1794894080460-prt_1e80629c3001noCLoCuxSLCqwU.png)

Steps: App launcher → Cases → New. Showcases: the form.
![Case Origin Web](screenshots/from-chat/133-1794894080461-prt_1e80629c3002rdyoOdcvL2mbKA.png)

Steps: set Case Origin. Showcases: origin set to Web.
![New Case (3)](screenshots/from-chat/134-1794894080462-prt_1e80629c3003uPj4BpzD4i14zm.png)

Steps: new case. Showcases: the form.
![New Case (4)](screenshots/from-chat/135-1794894080463-prt_1e80629c3004Z0K0G1I6Chzsxt.png)

Steps: new case. Showcases: the form.
![New Case (5)](screenshots/from-chat/136-1794894080463-prt_1e80629c3005DF1vb1qJIjzGFt.png)

Steps: new case. Showcases: the form.
![Case created](screenshots/from-chat/137-1794894088893-prt_1e8064abb001Eidr1PzvdJ9IIM.png)

Steps: save the Case. Showcases: the created case.
![Case detail with fields](screenshots/from-chat/138-1794894171677-prt_1e8078e0d001SrYw8TXQfHjl7d.png)

Steps: open the Case after the async call. Showcases: the ServiceNow fields filled.
![Case detail (2)](screenshots/from-chat/139-1794894171679-prt_1e8078e0d002QVa41zrTNy0WJR.png)

Steps: open the Case. Showcases: the fields.
![Case detail (3)](screenshots/from-chat/140-1794894171682-prt_1e8078e0e001emaE9iR4rmspGh.png)

Steps: open the Case. Showcases: the fields.
![ServiceNow search](screenshots/from-chat/141-1794894189592-prt_1e807d411001RLzcKsZsPQmFBr.png)

Steps: ServiceNow global search for the number. Showcases: verifying the Incident.
![REST Explorer GET](screenshots/from-chat/142-1794894954339-prt_1e8137f4b001gZ5Gbs9XPNagdg.png)

Steps: REST API Explorer GET. Showcases: reading the Incident.
![GET (2)](screenshots/from-chat/143-1794894954341-prt_1e8137f4c001I8Uk2Z1q8yICNl.png)

Steps: as above. Showcases: the GET result.
![GET (3)](screenshots/from-chat/144-1794894954344-prt_1e8137f4c002Zm3te5x1Cz9ZyY.png)

Steps: as above. Showcases: the GET result.
![GET (4)](screenshots/from-chat/145-1794894954345-prt_1e8137f4c0031W8bRRtBSRy7YO.png)

Steps: as above. Showcases: the GET result.
![GET (5)](screenshots/from-chat/146-1794894954346-prt_1e8137f4d001f7gh8XvuxI7jNR.png)

Steps: as above. Showcases: the GET result.
![GET (6)](screenshots/from-chat/147-1794894954349-prt_1e8137f4d002hIt3Js33kaSe4F.png)

Steps: as above. Showcases: the GET result.
![Empty POST response](screenshots/from-chat/148-1794894954362-prt_1e8137f4d003dGGO7KPTti2l2B.png)

Steps: an empty POST. Showcases: INC0010011 / INC0010012 created. Impact and Urgency default to 3.
![Empty POST (2)](screenshots/from-chat/149-1794894954364-prt_1e8137f4e001SgEzzVMTlMzPs2.png)

Steps: as above. Showcases: the empty response.
![Empty POST (3)](screenshots/from-chat/150-1794894954365-prt_1e8137f4e002Vgv7URu3QuKXX1.png)

Steps: as above. Showcases: the response.
![Empty POST (4)](screenshots/from-chat/151-1794894954366-prt_1e8137f4e003zSdt1OBhrhmID7.png)

Steps: as above. Showcases: the response.
![REST API methods](screenshots/from-chat/152-1794895169567-prt_1e816c81b001YG4crEdkagwlUb.png)

Steps: REST API Explorer. Showcases: the method list. POST creates.
![Methods (2)](screenshots/from-chat/153-1794895169568-prt_1e816c81c001Y2qVczaWQ7YKLC.png)

Steps: as above. Showcases: the method list.
![Named Credential detail](screenshots/from-chat/154-1794895191433-prt_1e8171d80001ZavVmpV3LipfDL.png)

Steps: Setup → Named Credentials → EBOND_ServiceNow. Showcases: created after.
![Named Credential (2)](screenshots/from-chat/155-1794895191435-prt_1e8171d80002KoI77w5rqiI732.png)

Steps: as above. Showcases: the detail.
![External Credential detail](screenshots/from-chat/156-1794895232947-prt_1e817bfaf0015ARM4fB2XhJQRm.png)

Steps: Setup → External Credentials → EBONDServiceNow. Showcases: created first.
![Confirm dialog](screenshots/from-chat/157-1794895306932-prt_1e818e0b1001fHWaWbTMphv5BG.png)

Steps: Explorer Send on a write method. Showcases: Modifying data, confirm to continue.
![Confirm dialog (2)](screenshots/from-chat/158-1794895317283-prt_1e8190920001EBtcTlqut3ThaZ.png)

Steps: as above. Showcases: the dialog.
![File listing](screenshots/from-chat/159-1794895436478-prt_1e81adabb00180LodVmdUO0zhK.png)

Steps: the screenshots folder. Showcases: where the duplicate screenshots showed up.
![Folder structure](screenshots/from-chat/160-1794895662562-prt_1e81e4de1001xTbWUsKTrIfvsp.png)

Steps: the folder tree. Showcases: where the screenshots live on disk.

## Lab 3 — ServiceNow to Salesforce
<details>
<summary>Not started yet</summary>

Not done yet. This will prove ServiceNow can call back and update the same Case by Snow_Sys_Id__c, instead of creating a second Case. No screenshots yet.

</details>

## Lab 4 — Ownership and loops
<details>
<summary>Not started yet</summary>

Not done yet. This will show which system owns which field, and that one save does not bounce. No screenshots yet.

</details>

## Lab 5 — Troubleshooting
<details>
<summary>Not started yet</summary>

Not done yet. A clean run does not need a shot. No screenshots yet.

</details>

## Appendix — redrawn stand-ins (not real screens)
64 files in `screenshots/redrawn-stand-ins/`. A previous pass drew these caption cards to stand in for missing screenshots. They are not Salesforce or ServiceNow screens and must not be used as proof.

## Appendix — full from-chat index
All 161 authentic captures are in `screenshots/from-chat/`, in send order. The sections above attach them to the lab step that produced them. Anything not matched stays here.
