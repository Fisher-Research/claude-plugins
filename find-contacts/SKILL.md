---
name: find-contacts
description: >
  Use this skill to source contacts for a specified ideal customer profile using the Apollo MCP server.
  Only search using Apollo endpoints that do not consume any credits.
---

## Your workspace
Create a new folder in the workspace directory which will serve as your workspace for this session. The name should be the date in YYYY-MM-DD format followed by a brief description of the ideal customer profile I asked for.

For example, 2026-09-12_seattle-saas-companies

I want the only file in this workspace folder to be an Excel file with the same name, for example 2026-09-12_seattle-saas-companies.xlsx

In the workspace, you are free to write scripts or add any other kinds of files you need. Just keep all files that aren't the final Excel file in subdirectories like scripts/ or cache/. Those aren't hard required names, you can add as many subdirectories as you reasonably need.

So the directory would look something like this:

workspace/
  2026-09-12_seattle-saas-companies/
    scripts/
    cache/
    # other directories...
    2026-09-12_seattle-saas-companies.xlsx

## Your deliverable
The deliverable I want from this session is an Excel file with the information you can get from free Apollo searches, which includes basic company info and an obfuscated lead name.

Focus on finding the companies first. I'm a one-man shop, so I'm looking for smaller companies to contract for. The companies should:
- Have less than 50 people (Apollo free search returns bucket ranges for company size, e.g. 1-10, 11-20)
- Not be in an industry with a lot of red tape or deals with a lot of sensitive information, e.g. defense, healthcare
- Apollo sometimes returns companies that are basically just Shopify stores, I'm not interested in those. 
- Companies without an established dev team (you should be able to search Apollo for engineering sounding titles). If they already have engineers on staff, then there's no need for me as a software contractor.
- You can't get the company's specific tech stack without enriching, but I believe you can do free searches to look for things like AWS, Python, Typescript (my specialties). 

Only after you've found a company should you find an obfuscated lead for it. Since these are smaller companies, focus on:
- CEOs, Founders, C-suite execs (decision makers)
- Make sure each contact has the `has_email` as true from Apollo, otherwise I can't enrich it.

The final Excel sheet should have these columns:
- company
- website (can be opened by clicking on it in Excel)
- employees_bucket (range of company size, e.g. 1-10)
- contact_name (obfuscated since you'll be using the free people search)
- contact_title
- rationale (2-3 short sentences explaining why you added this company to the list)
- apollo_org_id (so we can later enrich the company)
- contact_apollo_id (so we can later enrich the contact)

## Rules for sourcing
- Use the Apollo MCP server but only use the endpoints that do not consume credits (do not enrich company data or contact emails/phone).

## Rules for writing the Excel file
- Verify each website URL you put in the Excel file. Sometimes Apollo has stale data where the website is either inactive or parked, so do not include the contact if the website is bad. In the website column, make sure the hyperlink is clickable.
- Make sure that no columns or rows remain frozen when you're done writing the file. I should be able to open it in Excel and shouldn't have to unfreeze anything.

## Your goal
/goal Create an Excel file as I've described with the total number of contacts I requested.

