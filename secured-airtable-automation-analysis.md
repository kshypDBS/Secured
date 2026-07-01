# Airtable Automation Analysis

## Scope

This document is based on **direct inspection of the Airtable `Automations` tab** for:

- `Secured Commesse` (`app8B65UB03x6TsbS`)
- `Secured CPQ` (`app0KpNcZBMSC4ATa`)

Inspection date: **July 1, 2026**

Unlike the previous inferred draft, this version is grounded in the actual automation list and workflow canvas visible in Airtable.

## Important reading note

The Airtable UI exposes different levels of detail depending on the automation:

- For some automations, the workflow canvas clearly shows the trigger, conditions, and named actions.
- For some script-based automations, Airtable only exposes `Run a script` / `Custom script from code editor` in the visible canvas, not the internal script logic itself.
- For a subset of items, the automation list clearly confirmed the automation name, status, trigger type, and action family, but the full step-by-step branch text was not fully expanded in the visible panel during this capture.

Because of that, this document distinguishes between:

- `Fully captured from canvas`
- `Partially captured from canvas`

That distinction is about **UI visibility during inspection**, not about whether the automation exists.

---

## Secured Commesse

Total automations found: **27**

### Commesse automation inventory

| Automation | Status | Trigger | Actions / flow | Capture quality |
| --- | --- | --- | --- | --- |
| `AT-REFC Eliminare il nome referente s'è stata cambiata la org` | ON | `When a record is updated` on `Committente` | If `Committente Name` is empty and `responsabile_committente Name` is not empty, `Update record` to clear `referente committente`. | Fully captured from canvas |
| `AT-CPLU - Carica Prezzo da listino update` | ON | `When a record is updated` on `Costi and Quantità` | If supplier/manpower/subcontract/material/other cost fields are empty and `da_prev` condition is met, `Update record`. Otherwise branch is empty. | Fully captured from canvas |
| `AT-CPLC - Carica Prezzo da listino Create` | ON | `When a record is created` in `dettagli_costi` | If supplier/manpower/subcontract/material/other cost fields are empty and `da_prev` condition is met, `Update record`. Otherwise branch is empty. | Fully captured from canvas |
| `AT-VDC markup generale e costo responsabile commessa` | OFF | `When a record is created` in `vdc_commesse` | `Create record` in `vdc_comm_mark_line_items`; `Create record` in `vdc_comm_cost_line_items`; additional condition excludes several activity types such as indagini/monitoraggi/sollevamenti. | Fully captured from canvas |
| `AT-DMU Set default markup` | OFF | `When a button is clicked` | `Create record` for `Margine generale`. | Fully captured from canvas |
| `AT-TPR Tipologia commessa` | ON | `When a record is updated` | `Find records`, then `Update record`. | Fully captured from canvas |
| `AT-CDR Commessa- Gdrive Clone Folder` | OFF | `When a button is clicked` | `Run a script` from Airtable code editor. Likely Google Drive folder cloning. | Partially captured from canvas |
| `AT-RDR Commessa - cartella tipo modificata - refresh json structure` | ON | `When a button is clicked` | `Run a script`; visible note says it is used only when the Google Drive folder template has been updated. | Fully captured from canvas |
| `AT-CAS Flag inarcassa if the vdc meets the requirement` | ON | `When a record is updated` on `voce_di_computo_comm` | If the linked `Attività_principale_vdc` belongs to a long list of professional-service categories (structural, architectural, geological, DL, CSP/CSE, collaudi, consulenze, pratiche, PFTE, definitive, esecutive, etc.), then update the record to set the inarcassa-related flag; otherwise update the record differently. | Partially captured from canvas |
| `AT-CCU1 Commessa costi url insert` | ON | `When a record is created` | `Update record`. Based on the name, it writes or refreshes a commessa cost URL on insert. | Partially captured from list/canvas |
| `AT-CCU2 Commessa costi url update` | ON | `When a record is updated` | `Update record`. Based on the name, it refreshes a commessa cost URL on update. | Partially captured from list/canvas |
| `AT-CVU1 VDC commesse costi url insert` | ON | `When a record is created` | `Update record`. Based on the name, it writes or refreshes a VDC/commessa cost URL on insert. | Partially captured from list/canvas |
| `AT-CVU2 VDC commesse costi url insert copy` | ON | `When a record is updated` | `Update record`. Based on the name, it refreshes a VDC/commessa cost URL on update/copy flow. | Partially captured from list/canvas |
| `AT-CRC Create ClickUp project` | ON | `When a button is clicked` | `Run a script` from Airtable code editor. The business purpose is clearly ClickUp project creation. | Partially captured from list/canvas |
| `AT-RST Stato di rate - fatturato` | ON | `When a record is updated` | `Update record`. Based on the name, it updates payment installment status against invoicing/fatturato. | Partially captured from list/canvas |
| `AT-ARC Archiviazione commessa` | OFF | `When a button is clicked` | `Update record`, plus `2 more actions`. The name indicates project archival workflow. | Partially captured from list/canvas |
| `AT-CCV Relazione contratto da vdc a commessa` | ON | `When a record matches conditions` | `Update record`. The name indicates propagation of contract relationship from VDC to commessa. | Partially captured from list/canvas |
| `AT-CPREV Cost da prev fill in in da prev only` | ON | `When a record matches conditions` | `Find records`, then `1 more action`. The name indicates filling cost data from preventivo into `da_prev` context only. | Partially captured from list/canvas |
| `AT-NUM Automated number assignment commessa` | ON | `When a record is created` | `Run a script` from Airtable code editor to assign automatic commessa numbering. | Partially captured from list/canvas |
| `AT-NUM1 Automated number assignment commessa_manual_year_insert` | ON | `When a record is updated` on `anno_creazione_manual` | `Run a script` from Airtable code editor. Visible description says it updates automatic numbering for commesse created in prior years so they do not interfere with the current year numbering. | Fully captured from canvas |
| `AT-CNUM Automated number contract` | ON | `When a record is created` in `Contratti` | `Run a script` from Airtable code editor for automatic contract numbering. | Fully captured from canvas |
| `AT-COS Commessa status sulla base di VDC` | ON | `When a record is updated` on `Stato_vdc` | `Run a script` from Airtable code editor to derive commessa status from VDC status. | Fully captured from canvas |
| `AT-CSA Commessa status sulla base di SAL` | ON | `When a record is updated` on `Stato` | `Run a script` from Airtable code editor to derive commessa status from SAL status. | Fully captured from canvas |
| `AT-SALI Aggiornamento SAL importo` | ON | `When a record is updated` on `Importo Rata` | `Run a script` from Airtable code editor to recalculate/update SAL amount. | Fully captured from canvas |
| `AT-SALN Nuovo SAL, trigger per creare il Clickup` | ON | `When a record is created` in `comm_rate_pagamento` | `Run a script` from Airtable code editor. The name indicates new SAL creation triggers ClickUp creation. | Fully captured from canvas |
| `AT-CBR Generare brief progetto` | OFF | `When a button is clicked` | `Run a script` from Airtable code editor to generate project brief. | Fully captured from canvas |
| `Automation 1` | OFF | `At a scheduled time` | No business logic defined in visible steps; canvas only showed a scheduled trigger and an empty action area. | Fully captured from canvas |

### Commesse observations

- `Secured Commesse` automations are heavily focused on:
  - price/cost initialization
  - status derivation
  - numbering
  - project/document structure refresh
  - ClickUp/Drive integration
  - contract/payment/SAL synchronization
- Several operationally important flows are script-based, which means the UI confirms the trigger and action type, but **the core business logic is hidden inside Airtable script code**.

---

## Secured CPQ

Total automations found: **26**

### CPQ automation inventory

| Automation | Status | Trigger | Actions / flow | Capture quality |
| --- | --- | --- | --- | --- |
| `AT-CPL - Carica Prezzo da listino` | ON | `When a record is updated` on `Servizio and qty` | If `vdc_prev_costo_manod`, `vdc_prev_costo_mater`, `vdc_prev_costo_subap`, or `vdc_prev_costo_altro` is empty, `Update record`. | Fully captured from canvas |
| `AT-VDC markup generale e costo responsabile commessa` | ON | `When a record is created` in `Voci di computo preventivo` | `Create record` in `vdc_prev_mark_line_items`; `Create record` in `vdc_prev_cost_line_items`; then `Update record`. | Fully captured from canvas |
| `AT-DAI - Data approvazione-accettazione-invio per Status preventivo` | ON | `When a record is updated` on `Stato` | Branches by status value: `Da inviare` updates approval date, `Inviato` updates send date, `Accettato` updates acceptance date. | Fully captured from canvas |
| `AT-DAIO - Data e status accettazione-invio do Opportunità` | ON | `When a record is updated` | `Find records`, plus `3 more actions`. Based on the name, it syncs send/acceptance dates and status from preventivo to opportunità. | Partially captured from list/canvas |
| `AT-DMU Set default markup` | OFF | `When a button is clicked` | `Create record` for `Margine generale`. | Fully captured from canvas |
| `REVIEWED AT-RDP 4 Rate` | ON | `When a button is clicked` | Creates 4 payment rows: `Acconto 30%`, `SAL 20%`, `SAL 20%`, `Saldo 30%`. | Fully captured from canvas |
| `REVIEWED AT-3RDP - 3 Rate` | ON | Creates 3 payment-rate rows according to defined criteria | The list description explicitly says it creates `3x rate di pagamento`. The visible canvas did not fully expand in this pass. | Partially captured from list/canvas |
| `REVIEWED AT-CPO - Crea Preventivo da Opportunità` | ON | `When a button is clicked` | `Find records`, plus `2 more actions`. The name indicates quote creation from opportunity. | Partially captured from list/canvas |
| `AT-DIA - aggiornamento data mese-anno invio ed accettazione prev + campi di opportunità` | ON | Update/sync automation | The list description says it updates send/acceptance date, month-year values, and opportunity fields. | Partially captured from list/canvas |
| `REVIEWED AT-REV Revisione preventivo` | ON | `When a button is clicked` | `Run a script` from Airtable code editor for quote revision flow. | Partially captured from list/canvas |
| `AT-ARI Aggiungere le attività in ricavi` | OFF | `When a button is clicked` | `Find records`, plus `1 more action`. The name indicates adding activities into ricavi/revenue lines. | Partially captured from list/canvas |
| `AT-DPO Data invio preventivo in Opportunità` | OFF | `When a record is updated` on `Data di invio and Data accettazione` | `Find records` where `Record ID Preventivo` matches Airtable record ID; if records exist, `Update record`; otherwise no action runs. | Fully captured from canvas |
| `REVIEWED AT-REF Eliminare il nome referente s'è stata cambiata la org` | ON | `When a record is updated` on `Clienti` | If `Clienti Name` is empty, `Update record` to clear the assigned `referente`. | Fully captured from canvas |
| `REVIEWED AT-TPR Tipologia preventivo` | ON | `When a record is updated` | `Find records`, then `Update record`. | Fully captured from canvas |
| `AT-CAS Flag inarcassa if the vdc meets the requirement` | ON | `When a record is updated` | Long condition checks whether linked `Attività_principale_vdc` belongs to a professional-service category set; then `Update record`, otherwise another `Update record`. | Fully captured from canvas |
| `AT-SQD Creazione template google docs preventivo trigger` | ON | `When a button is clicked` | `Run a script` from Airtable code editor to generate a Google Docs quote template flow. | Partially captured from list/canvas |
| `Crea commessa da preventivo` | ON | `When a button is clicked` | `Run a script` from Airtable code editor to create a commessa from a preventivo. | Partially captured from list/canvas |
| `REVIEWED AT-DEP Aggiornamento Data emmissione dopo la creazione del preventivo` | OFF | `When a record is created` | `Update record` after quote creation to populate emission date. | Partially captured from list/canvas |
| `AT-CPL Relazione commessa al preventivo` | ON | `When a record matches conditions` where `preventivo_record_id` is not empty | `Update record`, then another `Update record` to maintain quote-project relationship. | Fully captured from canvas |
| `AT-PVN numero progressivo preventivo` | ON | `When a record is created` in `Preventivi` | `Run a script` from Airtable code editor for automatic quote numbering. | Fully captured from canvas |
| `AT-OPN Numero progressivo Opportunità` | ON | `When a record is created` in `Opportunità` | `Run a script` from Airtable code editor for automatic opportunity numbering. | Fully captured from canvas |
| `AT-OCD Crea RDO task in Clickup` | ON | `When a button is clicked` | `Run a script` from Airtable code editor to create a ClickUp RDO task. | Fully captured from canvas |
| `AT-OCDC Crea RDO cartella in Drive` | ON | `When a button is clicked` | `Run a script` from Airtable code editor to create a Drive folder for RDO. | Fully captured from canvas |
| `AT-PRL Cancella il link preventivo` | ON | `When a button is clicked` | `Update record` to clear the quote link. | Fully captured from canvas |
| `AT-CN Numero cliente (TEMPORANEA)` | OFF | `When a record is created` in `Clienti` | `Run a script` from Airtable code editor. Visible description says it keeps customer numbers updated temporarily and may later be removed from customer names. | Fully captured from canvas |
| `Aggiorna Clienti` | OFF | `When a webhook is received` | `Run a script` from Airtable code editor. | Fully captured from canvas |

### CPQ observations

- `Secured CPQ` automations are focused on:
  - quotation pricing and markup initialization
  - quote lifecycle dates and statuses
  - opportunity-to-quote conversion
  - quote-to-project conversion
  - installment generation
  - numbering
  - Drive / Google Docs / ClickUp integrations
- The CPQ base clearly contains the commercial workflow backbone that later feeds `Secured Commesse`.

---

## Cross-base conclusions

### 1. The two bases are operationally coupled

The direct automation names confirm that:

- `Secured CPQ` is responsible for commercial creation logic
- `Secured Commesse` is responsible for downstream execution/project logic
- there is an explicit bridge from `preventivo` to `commessa`

Key confirmations:

- `Crea commessa da preventivo`
- `AT-CPL Relazione commessa al preventivo`
- `AT-CPREV Cost da prev fill in in da prev only`
- `AT-CCV Relazione contratto da vdc a commessa`

### 2. A large share of core logic lives in scripts

This is especially true for:

- numbering
- ClickUp integration
- Drive integration
- quote revision
- project creation
- status propagation

For migration/replatforming purposes, these script-backed automations are the highest-risk items because the business rules are **not fully visible from schema alone**.

### 3. There are three major automation clusters

#### Commercial cluster (`Secured CPQ`)

- pricing from catalog / markup defaults
- quote generation and revision
- quote dates/status lifecycle
- opportunity synchronization
- payment schedule generation

#### Delivery cluster (`Secured Commesse`)

- cost initialization and VDC cost/markup propagation
- SAL/payment state updates
- status management
- archive/brief/project support flows

#### Integration cluster (both bases)

- ClickUp project/task creation
- Google Drive folder creation / refresh
- Google Docs template generation
- webhook-driven client sync

---

## Migration implications

### Highest-priority automations to preserve first

1. Numbering automations:
   - `AT-PVN numero progressivo preventivo`
   - `AT-OPN Numero progressivo Opportunità`
   - `AT-NUM Automated number assignment commessa`
   - `AT-CNUM Automated number contract`

2. Quote/project conversion automations:
   - `REVIEWED AT-CPO - Crea Preventivo da Opportunità`
   - `Crea commessa da preventivo`
   - `AT-CPL Relazione commessa al preventivo`
   - `AT-CPREV Cost da prev fill in in da prev only`

3. Commercial date/status automations:
   - `AT-DAI`
   - `AT-DAIO`
   - `AT-DIA`
   - `AT-DPO`

4. Cost/price initialization automations:
   - `AT-CPL`
   - `AT-CPLU`
   - `AT-CPLC`
   - both `AT-VDC markup generale...` variants

5. Script integrations:
   - ClickUp-related automations
   - Drive-related automations
   - Google Docs template generation

### What still needs a second-pass extraction

The following automations were directly verified as existing, but their **internal script logic or complete branch details** were not fully visible in the current UI capture:

- all `Run a script` automations, unless the visible notes already explained their purpose
- automations where the list confirmed `find records` / `update record` / multi-action patterns, but the detailed branch tree was not fully expanded in the visible panel during this pass

To fully reconstruct those, the next step would be:

1. open each script action
2. copy the script body
3. map input tables/fields and outputs
4. convert that into executable migration requirements

---

## Recommended next deliverable

The next useful document should be:

`automation-to-target-system-mapping.md`

For each automation it should contain:

- source automation name
- source base
- trigger table / field / event
- conditions
- actions
- script dependency yes/no
- external dependency (`ClickUp`, `Google Drive`, `Google Docs`, webhook, none)
- target implementation proposal
- migration priority

