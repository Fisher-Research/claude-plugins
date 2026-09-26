# cold-email

Find leads, write a personalized cold email sequence for each one, and upload them to Instantly with one command:

```text
/cold-email:run 25 US accounting firms with 10-50 people. I sell AI automation for client onboarding. Campaign: Accounting Q4
```

## What it does

1. Researches companies that fit your description with Firecrawl.
2. Finds a decision-maker at each company with free Apollo searches.
3. Gets verified work emails from Apollo.
4. Writes a subject, an initial email, and two follow-ups for each lead.
5. Removes risky leads, such as mismatched names or duplicate emails.
6. Uploads the leads to your Instantly campaign.

If you don't name a campaign, the plugin creates a new one in Instantly. You can review every lead and email there. Nothing is sent until you connect your sending accounts and launch the campaign yourself.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Apollo](https://www.apollo.io): a plan with credits for email enrichment (about 1 credit per lead)
- [Firecrawl](https://www.firecrawl.dev): an API key (about 2 credits per lead)
- [Instantly](https://instantly.ai): a plan with API access and connected sending accounts

## Setup

1. Install the plugin (see the [repository README](../../README.md)).
2. Enter your Firecrawl and Instantly API keys when prompted during install. Create the Instantly key under Settings > Integrations > API with these scopes:
   - `campaigns:create`
   - `campaigns:read`
   - `leads:create`
   - `leads:read`
   - `leads:update`

   Copy the key right away; Instantly only shows it once. Keys are stored in your system's secure credential store. To change them later, run `/plugin configure cold-email@fisher-research`.
3. Start Claude Code, run `/mcp`, and sign in to Apollo.
