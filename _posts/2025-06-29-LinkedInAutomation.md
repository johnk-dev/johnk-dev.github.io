---
title: "Automated LinkedIn Job Scraping with Apify and Zapier"
date: 2025-06-26
author: John K.
categories: [Automation, Job Search]
tags: [LinkedIn, Apify, Zapier, scraping, automation]
---

After recently re-entering the job market, I quickly realized how challenging it is to search for industry-specific keywords on LinkedIn. LinkedIn’s search functionality is intentionally limited: results are pulled only from three indexed fields—job title, company, and a general keywords field (which itself is just a combination of title, skills, location, and seniority). This means you can’t reliably search within the full job description, forcing users like me to spend hours each week manually scrolling through hundreds or even thousands of postings in search of relevant opportunities.

While LinkedIn’s built-in filters offer some help, they fall short when you need to pinpoint jobs based on specific terms buried in descriptions or requirements. Frustrated by this limitation, I started looking for a better solution.

I knew web scraping tools could help, but I wasn’t sure where to begin. With a bit of guidance from ChatGPT, I was able to set up an automated workflow using Apify and Zapier to streamline the process. In this post, I’ll share exactly how I did it—so you can, too.

## Why Automate LinkedIn Job Search?

Automating your LinkedIn job search can save hours of manual effort, help you discover hidden opportunities, and allow you to filter jobs based on *your* criteria—not just what LinkedIn’s interface allows. By scraping job data and organizing it in a spreadsheet, you can:

- Search for any keyword in any field (not just job titles)
- Bulk filter and analyze postings
- Get notified of new matches automatically
- Focus your energy on the most relevant opportunities

## What is Apify?

**Apify** is a cloud-based platform for web automation and scraping. It lets you build, schedule, and run web scrapers (called “actors”) without needing to manage your own infrastructure. Apify provides ready-made actors for popular sites—including LinkedIn—and supports custom scripts for advanced use cases. You can extract job listings, company data, and more, then export results to formats like JSON, CSV, or directly to Google Sheets or other apps[6].

## What is Zapier?

**Zapier** is an automation tool that connects your favorite apps and services without any coding. By creating “Zaps,” you can automate workflows such as sending scraped job data from Apify directly into Google Sheets, Slack, or your email. Zapier acts as the glue between Apify and your daily tools, enabling seamless, real-time updates to your job search database.

## My Automated Pipeline

Here’s a high-level overview of the workflow I set up:

1. **Define Search Criteria:**  
   Set up Apify’s LinkedIn Jobs Scraper to search for your desired keywords, locations, and job types.
   Apify use what they call an "Actor" to build the scraping workflow. An Actor is essentially a serverless cloud program—think of it as a micro-service or cloud app you write once and then run on Apify’s infrastructure. There are many different pre-made Actors, I ended up using "AI Linkedin Job Matcher" - https://console.apify.com/actors/0tYWyTvxt367lXwWG/input which fit my requirements and was cheap enough ($5.00/1000 jobs = $0.0005 per job result, my keyword was specific enough to get around ~100 results per week which was within budget for Apify's monthly free credit of $5.00.
   ![alt text](/assets/img/screenshots/20250629/linkedin_scraper.png)

2. **Run the Scraper:**  
   Schedule Apify to run daily, weekly or monthly, collecting new job postings that match your criteria. I chose weekly which was a good frequency for my case.

3. **Save Data to Google Drive to be used by Zapier:**  
   Use Apify’s integrations or webhooks to send or share the scraped job data to Zapier. I ended up using the Google Drive integration, loading all job results to a Google sheet as a CSV. Zapier itself also has a Apify Zap which allows you to get results directly within Zapier's interface without the need to deal with Google Drive but I ran into a Zapier’s Apify integration limitation which flattens arrays into strings, which breaks structured data. The only option available then were Webhooks which is a Zapier premium feature or passing the data as a JSON string and parsing it in the Zapier Code step. I chose the latter of the two. 
   ![alt text](/assets/img/screenshots/20250629/zapier.png)

4. **Use Zapier to Transform the CSV and Automate Delivery:**  
   I started with a Google Drive Zap on Zapier that monitors a directory for new files, then a Zap to read in the new file as text, passing that to a Javascript code runner which takes and parses the incoming CSV text then builds a HTML table along with the header. The final table is then sent to my email using the Gmail's Send Email Event.
   ![alt text](/assets/img/screenshots/20250629/final_email.png)

The result? No more manual scrolling. I now have a living, searchable database of jobs tailored to my needs, updated and sent as an weekly email automatically.

## Final Thoughts

If you’re frustrated with LinkedIn’s limited job search, automation is a game-changer. Tools like Apify and Zapier make it accessible—even if you’re not a developer. With just a bit of setup, you can take control of your job hunt, save time, and never miss a relevant opportunity again.

---

*Have you tried automating your job search? Let me know your experiences or questions in the comments!*