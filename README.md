# web scraping: What It Is, Three Ways to Do It, and the Real Cost of Doing It at Scale

Web scraping is the automated extraction of data from websites: a program fetches a page, pulls out the specific fields you care about — prices, product names, reviews, listings — and saves them as structured data you can actually use, whether that's a spreadsheet, a CSV, a database, or a JSON feed. If you've ever copied a hundred product prices into Excel by hand, a scraper does that job in seconds and repeats it every day without you.

Most people searching for this term eventually hit the same wall. Writing a basic scraper is easy. Getting it to run reliably at scale — against sites that rotate layouts, require JavaScript rendering, and block anything that looks like a bot — is where projects stall. This guide covers how scraping actually works, the three ways to do it, and, for when you outgrow DIY scripts, what a managed service like ScraperAPI costs once you account for the details that don't show up on the pricing headline.

> **Quick take:** if you're scraping protected sites on a schedule, a managed API saves more in maintenance than it costs. ScraperAPI starts at **$49/month for 100,000 credits**, with a 5,000-credit free trial that needs no credit card. Most small projects fit the entry tier; check the current tiers here: [👉 see ScraperAPI's current plans and trial](https://www.scraperapi.com/?fp_ref=coupons)

## What web scraping actually involves

A scraper loops through four steps: fetch, parse, extract, store. First it sends an HTTP request for a URL, exactly like your browser does. Then it parses the returned HTML into a tree it can query. Next it locates the target values using CSS selectors or XPath, and cleans them up — stripping whitespace, converting `"$1,299.00"` into a number, normalizing dates. Finally it writes the structured result somewhere useful: CSV, JSON, a SQL database, or straight into another system via an API.

Two related terms cause constant confusion:

- **Web crawling** is about discovery at scale — a bot follows links from page to page to find and index URLs (that's what Google does). Crawling finds pages; scraping extracts data from them. Real projects usually do a bit of both.
- **Screen scraping** is the older technique of capturing data from what's displayed on a screen. For most web use cases today, it's been replaced by parsing the HTML directly.

One common misconception worth killing early: pointing a scraper at a domain does not download the entire site. A scraper only extracts the fields you specified from the pages you pointed it at. Most projects touch a tiny fraction of the target site.

## The three ways to scrape, and which one fits your project

There are roughly three ways to run a scraper, and they map to very different team shapes and budgets.

**Write your own code.** Python dominates here. `requests` plus BeautifulSoup handles simple static pages; Scrapy is a full framework built for large multi-page crawls; Playwright or Selenium drives a real browser when content only appears after JavaScript runs. Node.js, Go, PHP, and Java all have mature toolchains too, so pick whatever your team already knows. This route gives you the most control and the lowest per-request cost — you're only paying for infrastructure. The tradeoff is maintenance: once a target site starts blocking you, the job becomes managing proxies, browser fingerprints, and retry logic, and that work reliably outgrows the scraper itself.

**Use a no-code tool.** Tools like Octoparse let you load a page, click the elements you want, and export the result to a spreadsheet — no programming. This is genuinely the fastest path for small one-off jobs on cooperative sites. The ceiling is real, though: heavy anti-bot defenses, awkward interactions, and layouts that change weekly are where click-based builders struggle.

**Use a managed scraping API.** You send a URL, the service handles proxies, browser rendering, CAPTCHA handling, and anti-bot bypass, and returns the page data or clean HTML. Per request it costs more than running your own script, but you stop maintaining any of the blocking infrastructure. For ongoing collection from protected sites, this is where the reliability lives.

The honest rule of thumb from people who do this for a living: the hard part is rarely the parsing. It's getting reliable access to the content at scale without being blocked — which is why so much of the tooling ecosystem is about proxies and anti-bot handling rather than extraction.

## When a managed API stops being optional

A DIY script is the right call for a learning project, a one-off job on a static site, or anything you control end to end. The calculus flips when at least two of these are true:

1. Your target sites use Cloudflare, DataDome, PerimeterX, or similar protection.
2. Content renders with JavaScript, so plain HTTP requests return an empty shell.
3. You need scheduled, recurring collection — daily price checks, weekly review pulls.
4. The dataset is large enough that manual unblocking would eat more engineer-hours than the API bill.

ScraperAPI sits in this third category. You make one API request with your key and a target URL, and it returns the page — with proxy rotation, CAPTCHA solving, and (if you ask for it) headless browser rendering handled upstream. In 2026, its credit system also covers SERP and e-commerce APIs for Amazon, Google, and Walmart targets, following the Traject Data acquisition folded into the platform in late April 2026.

## ScraperAPI plans and prices: the full current lineup

ScraperAPI uses a credit-based system where one successful page request costs a base number of credits, with surcharges for harder requests. The publicly listed tiers, as of mid-2026, look like this:

| Plan | Credits / capacity | Price | Billing | Get it |
| --- | --- | --- | --- | --- |
| Free trial | 5,000 credits, 7 days (then 1,000/month free) | $0 | One-time | [ Start the free trial](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | 100,000 credits | $49/month | Monthly | [ Get Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | Higher credit pool; full geotargeting unlocked | $299/month ($269.10/month billed annually) | Monthly or annual | [ Get Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling | Larger pool; Pay-As-You-Go becomes available | $475/month | Monthly | [ Get Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Pro | 10.5M credits, 300 concurrent threads | Check live pricing | Monthly | [ Get Pro](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | 21.5M credits, 500 concurrent threads | $1,975/month | Monthly | [ Get Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | Custom | Custom quote | Custom | [ Request a quote](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

One caveat on the entry tiers: ScraperAPI's pricing page uses a slider for the lower tiers, so the exact credit/price combinations there can shift. The $49 for 100,000 credits figure has been consistently reported across multiple independent reviews in 2026, but confirm the current number on the pricing page before committing.

New users have also had access to a **START10** promo code, worth 10% off the first month on any subscription plan — it's the code with the most consistent recent activation reports across coupon aggregators. Apply it at checkout.

## The credit math nobody shows you upfront

Here's the detail most reviews skip, and it changes which plan you should pick: the base credit cost is only the floor.

Every "hard" feature adds a surcharge per request:

- **JavaScript rendering** (headless Chrome): +10 credits
- **`premium=true`** (residential proxy tier): +10 credits
- **`screenshot=true`**: +10 credits
- **`ultra_premium=true`**: +30 credits (paid plans only)
- **Anti-bot bypass** (Cloudflare, DataDome, PerimeterX): +10 credits each

So a simple static page might cost 1 credit, but a JavaScript-rendered page on a Cloudflare-protected site with residential proxies can cost 20 to 30+. That 100,000-credit Hobby allowance is 100,000 easy pages — or somewhere around 3,000 to 5,000 hard ones. Before choosing a tier, estimate your request mix honestly: count how many of your target URLs actually need rendering and premium proxies, multiply, then pick the plan against that number, not against your raw page count.

Two more limits that only surface in the details:

- **Geotargeting is US/EU only on lower tiers.** Country-level targeting outside the US and EU requires Business ($299/month) or higher; the full list spans about 70 countries.
- **Pay-As-You-Go only exists on Scaling ($475/month) and above.** On lower tiers, when you burn through your credits, requests stop until the next billing cycle. If your volume spikes unpredictably mid-month, that cutoff is a real operational problem.

For most solo developers and small teams doing price monitoring or lead generation, Hobby covers the trial of the concept, and Business is where serious recurring work lands — mainly because of the geotargeting unlock and the headroom for credit multipliers. You can compare the exact credit pools on the current pricing page: [👉 check the Business tier's current credit allocation](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## Is web scraping legal?

Scraping publicly available data is generally legal in the US and EU, but it's nuanced, and the nuances matter. The stable principles:

- **Public vs. private:** data viewable without logging in has a far stronger legal position than anything behind a login or paywall. Bypassing authentication is where trouble starts.
- **Personal data:** GDPR and CCPA apply to personal data regardless of whether it's public. Names, emails, and phone numbers collected from directories need a defensible basis.
- **Public visibility ≠ permission:** a page being publicly visible doesn't automatically grant the right to copy, republish, or commercially use its data.

And one practical rule that beats all of the above: if an official API or licensed source exists for the data you need, use it. Scraping is for when there's no API, the API is rate-limited beyond your needs, or the data only exists on public pages.

## Frequently asked questions

**Do I need to know how to code to scrape a website?**
No. No-code tools handle small, structured sites through a click-based interface. You'll need code (or a managed API) once targets get defensive or jobs get large.

**How much does web scraping cost?**
A DIY Python scraper costs only server time. Managed APIs run from $49/month at the entry tier to custom enterprise pricing, with per-request surcharges for rendering and anti-bypass features.

**How many requests do I need for a real project?**
Estimate pages × frequency. Monitoring 2,000 product pages daily means roughly 60,000 requests a month before multipliers — right at the edge of the Hobby tier, which is exactly why calculating your credit mix first matters.

**Can a scraper handle sites that require JavaScript?**
Yes, two ways: find the site's underlying JSON API and call that directly (fastest and most reliable when available), or render the page in a headless browser. Managed APIs like ScraperAPI handle rendering for you at +10 credits per request.

## Choosing before you commit

If your targets are static, public, and few — write the Python script, spend nothing, done. If you need click-and-collect extraction on friendly sites a handful of times, a no-code tool will be faster than anything else. But if you're building recurring collection against sites that actively fight bots, start with the free trial and let real request costs tell you which tier fits: [👉 sign up for the 5,000-credit free trial](https://www.scraperapi.com/?fp_ref=coupons)

Before you pay for anything, do two things. First, tally how many of your requests will need JavaScript rendering or premium proxies — that number, not your raw page count, determines the right tier. Second, if you're targeting countries outside the US and EU, confirm your volume justifies Business-level pricing, because geotargeting below that tier is limited to US and EU locations. Then use **START10** at checkout to take 10% off your first month while it's still active.
