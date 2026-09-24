---
name: run
description: Find new cold-email leads for a described audience, get their verified emails, write a personalized email sequence for each, and upload them to an Instantly campaign, end to end. Use when the user asks to find leads, run cold outreach, or fill an Instantly campaign for a target audience.
argument-hint: "[count] <who to target, what you sell, Instantly campaign>"
---

# Run

Run the whole cold-email pipeline from one description, for example:

```text
/cold-email:run 25 US accounting firms with 10-50 people. I sell AI automation for client onboarding. Campaign: Accounting Q4
```

## 1. Brief

Build the brief from the arguments and what you already know about the user's business:

- `audience`: who to target (industry, size, location, anything else the user gave)
- `count`: number of leads to upload (default 20)
- `offer`: what the user sells and why it helps this audience
- `sender`: the name to sign the emails with
- `campaign`: an existing Instantly campaign name, or blank to create a new draft campaign

If `audience`, `offer`, or `sender` is missing, ask for all the missing ones in a single question. After that, run unattended to the end.

Before researching, confirm that Firecrawl, Apollo, and Instantly all respond, so no credits are spent if one is down. If a service needs a login, is out of credits, or keeps failing, stop and report the specific problem.

## 2. Research

Credit limit: at most 2x `count` in Firecrawl credits. If you hit it, continue with the leads found so far.

1. Research candidate companies with Firecrawl. Specific queries beat broad category searches. Find public evidence that each company fits the audience; never qualify a company from Apollo's industry label alone.
2. Open each website and confirm it loads, belongs to the company, and supports the fit. Skip parked or stale sites.
3. Find each company with free Apollo organization search, then use free Apollo people search to choose a decision-maker for the `offer`. At small companies that is usually the owner, founder, or CEO.
4. Keep a contact only if Apollo shows `has_email: true`, and skip anyone already in the Instantly workspace.
5. For each lead, note 2-3 sentences on why the company fits. The emails build on this.

Research a bit past `count`, since some leads drop out in the next steps.

## 3. Enrich

This step spends Apollo credits: at most 5x the number of contacts. Standard enrichment costs 1 credit per matched person.

1. Call `apollo_users_api_profile` with `include_waterfall_capability=true`. Use waterfall email enrichment if it is enabled, otherwise standard enrichment.
2. Call `apollo_people_bulk_match` in batches of up to 10, passing each person's Apollo `id`. For waterfall, set `run_waterfall_email=true` and poll `apollo_webhook_result_show` until results are ready. Never request phone numbers or personal emails.
3. Keep only work emails Apollo marks as `verified`, plus the returned first name, last name, and title. Drop everyone else. Bad addresses hurt deliverability.
4. Never enrich the same person twice.

## 4. Write

For each lead, write a subject and three emails:

- Subject: short, specific, and not salesy.
- Initial email: one sentence showing you know the company, the `offer` framed as a benefit to a company like theirs, and a low-pressure question.
- Follow-up 1: shorter, adds one new reason to reply, and names the company.
- Follow-up 2: a brief last check-in asking whether someone else is the right person.

Greet with the first name, sign with the `sender`, and write plainly, like one person writing to another. Never claim anything about the company that the research doesn't support. Use `<br>` for line breaks.

## 5. QA

Drop any lead with a real or likely problem. When in doubt, drop it:

- a mangled name, or one that conflicts with the email address
- an email or website domain that doesn't match the company
- a duplicate email address
- similarly named companies mixed up
- an email that names the wrong company, makes an unsupported claim, or contains a placeholder like `{Company}`

## 6. Upload

- If the brief names a campaign, find it in Instantly. Stop and report if it doesn't exist.
- Otherwise, create a campaign named after the audience and date, with three steps a few days apart:
  1. Subject `{{email_subject}}`, body `{{email_body}}`
  2. Blank subject (a reply in the same thread), body `{{email_body_2}}`
  3. Blank subject, body `{{email_body_3}}`
- Add each lead with `email`, `first_name`, `last_name`, `company_name`, `website`, and `job_title`. Add the subject and emails as the custom variables `email_subject`, `email_body`, `email_body_2`, and `email_body_3`.
- Set `skip_if_in_workspace: true`, `skip_if_in_campaign: true`, and `verify_leads_on_import: false` on every lead.
- Never activate or change a campaign's settings, send emails, or delete leads.

Upload at most `count` leads.

## 7. Report

Reply with:

- the campaign name
- leads uploaded against `count`, with the reason for any shortfall
- leads dropped at each step
- Firecrawl and Apollo credits used

If you created a new campaign, remind the user to connect sending accounts, review the emails in Instantly, and launch it.
