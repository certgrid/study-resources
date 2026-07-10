# Lab 12 - App Service Plan and Deployment Slots

App Service questions are mostly about tiers: which tier unlocks slots, autoscale, and backups. This lab creates a Standard-tier app just long enough to use a slot swap, then scales the plan down.

## Time Needed

35-40 minutes.

## What You Will Learn

- The relationship between an App Service plan and its apps
- Which features each tier unlocks
- How deployment slots and swaps work
- Scale up vs scale out on a real plan

## AZ-104 Concepts Covered

| Concept            | Where you see it in the lab                 |
| ------------------ | ------------------------------------------- |
| App Service plan   | You create one and read the tier matrix     |
| Web app            | You deploy sample content                   |
| Deployment slots   | You create a staging slot (Standard tier)   |
| Slot swap          | You swap staging and production             |
| Scaling            | You find scale up vs scale out blades       |
| Custom domains/TLS | You locate the blades and read requirements |

## Cost Warning

A Standard (S1) plan costs real money per hour (roughly the price of a mid-size VM). This lab uses S1 only for the slot exercise, then you IMMEDIATELY scale down or delete. Do not leave an S1 plan running overnight. The plan bills even with zero apps on it.

## Steps

### 1. Create the plan and app

1. Search **App Services > Create > Web App**.
2. Resource group `rg-az104-labs`, name `app-az104-<unique>` (must be globally unique), runtime: any (e.g. .NET or Node), OS: default for the runtime.
3. Pricing plan: create new plan `plan-az104-lab`, tier **Standard S1** (needed for slots). Note what the picker shows for Free/Basic vs Standard vs Premium: slots, autoscale, backups appear at Standard.
4. Create and wait for deployment.
5. Browse the default URL `https://app-az104-<unique>.azurewebsites.net`: the placeholder page confirms it runs.

### 2. Put identifiable content in production

1. Open the app, go to **Development Tools > Advanced Tools (Kudu) > Go**, or use the App Service Editor if available.
2. Edit the default page (e.g. `hostingstart.html` in `site/wwwroot`) so it says `PRODUCTION V1`. Verify in the browser.

### 3. Create a staging slot

1. On the app, open **Deployment > Deployment slots**.
2. Add slot `staging`, clone settings from production. Note: this option exists because the plan is Standard; Basic would refuse.
3. Open the staging slot (it is a full app with its own URL `...-staging.azurewebsites.net`) and edit ITS page to say `STAGING V2`.

### 4. Swap

1. Back on **Deployment slots**, select **Swap**: source staging, target production.
2. Read the swap screen: settings marked as slot-specific (sticky) stay behind; the rest move with the code.
3. Complete the swap and refresh the production URL: it now shows `STAGING V2` content: zero-downtime deploy. Swapping back is the instant rollback story.

### 5. Scaling and the other exam blades

1. **Settings > Scale up (App Service plan)**: this changes tier (vertical). See the feature/tier matrix again.
2. **Scale out (App Service plan)**: rule-based autoscale lives here (Standard+); note it looks exactly like the scale set autoscale UI.
3. Locate, read, do not configure: **Custom domains** (needs CNAME/TXT validation), **Certificates** (free managed certificate), **Backups** (Standard+), **Networking** (VNet integration = outbound, private endpoint = inbound).

## Clean Up

Slots and content are included in the plan price, but the S1 PLAN is the cost. Do one of these NOW:

- If continuing to other labs today and tomorrow: scale the plan DOWN to Free F1 or Basic B1 (Scale up blade) - the staging slot must be deleted first for Free/Basic.
- If done with App Service: delete the web app AND `plan-az104-lab` (deleting only the app leaves the plan billing).

## Success Criteria

You are done when you can explain:

- Why the plan bills even with no apps, and what deleting only the app leaves behind
- Which tier first offers slots and autoscale, and slot counts for Standard/Premium
- What happens to app settings during a swap (sticky vs swapped)
- Scale up vs scale out in App Service terms
- VNet integration vs private endpoint direction (outbound vs inbound)
