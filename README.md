# Rank Tracking Residential IP Guide: How Many IPs Do You Need, Do You Need City Targeting, and What Does It Cost? (Plan Comparison + Request Math)

A keyword doesn't have one ranking. It has a ranking per location, per device, per logged-in state and per hour, and the IP your request leaves from decides which version of the results page comes back. That fact alone shapes the entire purchase: you're buying clean residential exits in the markets you actually measure, in enough quantity to keep each address under its daily request ceiling.

Two numbers set the budget, and keyword count isn't one of them. Depth comes first. Since September 2025 Google returns ten results per page and no longer honors the old `num=100` parameter, so tracking a keyword's top 20 costs two requests and its top 100 costs ten. Geographic precision comes second, because city-level targeting is a paid tier nearly everywhere, and at some providers it doesn't exist at all.

For US-level tracking, a residential-IP VPS is the cheapest route I can document with verified prices. SixtyNet's **Residential-STARTER is $25 a month**: a 2-core, 2 GB machine that comes with an AT&T Mobility residential IP and 5 TB of monthly traffic. You get one static exit rather than a rotating pool, which puts a rough ceiling of a hundred keywords a day at top-20 depth on a single box.

> **The short version.** US-only tracking, a few hundred to a few thousand keywords, daily top-20 checks: start with one Residential-STARTER at $25/month and add boxes as the list grows, since each box adds another residential IP and roughly another hundred keywords of daily depth-20 capacity. Skip this if you need city-level local pack data across many metros, or if you're tracking tens of thousands of keywords.
> 👉 [See the current residential plans and the monthly price of each](https://sixtynet.net/aff.php?aff=39)

## SixtyNet's residential plans, side by side

Four plans, same port policy, same residential IP type. The only thing that changes is how much machine and traffic you get per address.

| Plan | CPU / RAM / NVMe | Monthly traffic | Price (USD, monthly) | Order |
| --- | --- | --- | --- | --- |
| Residential-STARTER | 2 cores / 2 GB / 40 GB | 5 TB | **$25.00** | [Order Residential-STARTER](https://sixtynet.net/aff.php?aff=39) |
| Residential-MICRO | 4 cores / 4 GB / 80 GB | 10 TB | **$45.00** | [Order Residential-MICRO](https://sixtynet.net/aff.php?aff=39) |
| Residential-MEDIUM | 8 cores / 8 GB / 160 GB | 20 TB | **$85.00** | [Order Residential-MEDIUM](https://sixtynet.net/aff.php?aff=39) |
| Residential-LARGE | 16 cores / 16 GB / 320 GB | 40 TB | **$165.00** | [Order Residential-LARGE](https://sixtynet.net/aff.php?aff=39) |

All four include a 10G premium network link and 12,500 to 25,000 IOPS of NVMe storage, which is far more disk throughput than a SERP crawler will ever touch. Two details matter more than the specs:

- **Ports 80 and 443 are closed on every residential plan**, by the provider's own risk-control policy. For rank tracking this is irrelevant. Your crawler makes outbound HTTPS requests to a search engine and never needs to accept inbound traffic on 80 or 443. If you also want to host a public site, that's a different product line entirely.
- **The prices above are monthly "starting from" figures.** Quarterly, semi-annual and annual billing all carry discounts on this site, and the annual cycle is the largest. Check the renewal price for the cycle you pick at checkout rather than assuming the monthly rate carries over.

## The other SixtyNet lines, and why they're the wrong buy here

The residential box is not the cheapest thing SixtyNet sells, and that's the part worth understanding before you click anything.

| Line | Specs | Verified price | For rank tracking? |
| --- | --- | --- | --- |
| Mobile VPS (Mobile-STARTER, Mobile-MICRO) | dynamic carrier IP, 2–4 cores | shown at checkout, lower than the residential line | Yes, for mobile-device SERP checks |
| LAX-STARTER | 2 cores / 2 GB / 40 GB / 5 TB, datacenter IP, DDoS protection | $200/yr (list $240) | No |
| LAX-MICRO | 4 / 4 GB / 80 GB / 10 TB | $400/yr (list $480) | No |
| LAX-MEDIUM | 8 / 8 GB / 160 GB / 20 TB | $800/yr (list $960) | No |
| LAX-LARGE | 8 cores / 16 GB / 320 GB / 40 TB | $1,600/yr (list $1,920) | No |

The datacenter plans work out cheaper per year than the residential Starter ($200 against $300), and a datacenter IP is exactly what search engines throttle first. Paying more for the residential IP is the entire point of the purchase.

The Mobile VPS line is the genuinely interesting second option. Mobile and desktop are different result pages, sometimes with different orderings, and a carrier IP is the honest way to see the phone version of a SERP. If you track both, run them on separate boxes rather than switching user agents on one.

SixtyNet also lists China-optimized residential variants and larger RAID 10 storage configurations; those are priced by configuration at checkout. One note carried openly on the official page: refunds on the China-optimized residential products are issued as account balance only.

## Same keyword, different answer: pin four variables first

Rankings move with location, personalization, device and time, and an unprofessional measurement confuses a change in any of those with a change in rank. Fixing all four is what makes a number comparable between checks.

**Log out and use a clean cookie jar.** A logged-in session carries search history and preferences that nudge ordering. Accurate measurement approximates a neutral searcher, not a specific person's tailored view. **Fix one user agent and keep it.** Pick desktop or mobile, then present the same string every time. **Sample on a schedule and read the trend.** Results shift through the day as engines re-rank and test changes, so a single reading is a snapshot and a series is the signal.

IP reputation belongs in the same list. An address that's shared, flagged, or has been hammering an engine draws distorted or challenged results, which corrupts the data rather than merely failing the request. A clean residential IP presenting as an ordinary home connection is what lets you record what a normal searcher in that place would see, and a static residential box holds that vantage point constant by construction.

There's a practical side effect worth knowing: a static IP is naturally a sticky session. If a check walks through three or four result pages in one sequence, all of them come from the same address, which is what you want for a paginated SERP. Rotating networks need a session parameter to imitate this.

## The number that decides your bill is crawl depth

Ten results per page, no `num=100`, so depth is pure arithmetic: top 20 is two requests per keyword, top 100 is ten. A team tracking 2,000 keywords daily to position 20 issues 4,000 requests a day; the same list at depth 100 issues 20,000. Most teams land on daily top-20 checks plus a weekly deep crawl of a small subset, which keeps the request count near the low end while still catching movement below the fold.

What you won't find in any public source is a reliable conversion from "one SERP request" to megabytes. Page weight varies with ads, local packs, knowledge panels and whether you fetch the rendered DOM or the raw HTML. Measure it yourself: push a hundred keywords through your actual stack with your actual parser and record the bytes. That number, multiplied by monthly requests, is your bandwidth figure, and it's the only one worth planning against.

On a plan with 5 TB of included traffic, bandwidth is unlikely to be your binding constraint. Requests per IP per day is.

## How many residential IPs does one keyword list need?

Plan on keeping each IP to the low hundreds of requests a day, spread across the day, and adding addresses as the keyword list grows. Using 200 requests a day as a working ceiling:

| Depth | Requests per keyword | Keywords one IP covers per day |
| --- | --- | --- |
| Top 20 | 2 | ~100 |
| Top 50 | 5 | ~40 |
| Top 100 | 10 | ~20 |

That maps directly onto the plan table. One Residential-STARTER handles roughly a hundred keywords at daily depth-20. Three boxes at the MICRO tier take you to about 300 keywords a day on three separate addresses for $135 a month, and a MEDIUM/LARGE pair covers around 500. Confirm with support that separate orders receive distinct residential IPs before you build a rollout around that assumption.

The rest is scheduling discipline, and it's cheap to get right:

- Randomize the gap between searches instead of firing at fixed intervals.
- Keep cookies per IP so each address maintains its own consistent state.
- When an IP meets a CAPTCHA, rest it for the rest of the day. Don't retry through it.
- Use separate addresses for desktop and mobile checks rather than alternating user agents on one IP.
- Never dump 5,000 keywords from one box in an hour. That's how a clean IP stops being clean.

👉 [Compare the per-month cost of one box against four](https://sixtynet.net/aff.php?aff=39)

## Country, state, or city?

A static residential IP gives you one vantage point. Whatever location that address resolves to is the version of the SERP you'll record, so if you need results for the UK, Germany and Brazil, you need exits in all three, and a single US box won't do it.

City-level targeting is where the tiers split, and it's usually a paid upgrade:

| Provider | Model | Verified entry price | Geographic granularity |
| --- | --- | --- | --- |
| Shifter | rotating residential, per GB | from $0.75/GB | 195+ countries |
| ResiFactory | rotating residential, prepaid per GB, no subscription | Essential $1.50/GB | 150 countries, 51 US state targets; US city only on Premium and Mobile |
| ZentisLabs | rotating residential, non-expiring GB | $4.79/GB at 1 GB, down to $2.39/GB at 1 TB | 195+ countries; state and city on Light and Basic |
| Leastslow | static residential IPs, sold per IP | pool pricing for 25 or 100 IPs | a single US ISP location (Ashburn, Virginia) |
| Helodata | rotating residential, success-based billing | pay per successfully collected SERP page | 195 countries, city and ZIP |

Read that table as a map of what each shape can do, not as a price ranking. Those per-GB figures come from different tiers of different products, and putting them in one column doesn't make them a market price.

The decision is simple from here. National-level tracking for one market: a static residential box is enough, and SixtyNet provisions from a single Los Angeles facility, so confirm where the assigned carrier IP appears to be located if a specific metro matters to you. City-level local pack, "near me" and map results across multiple metros: you need city-targeted exits, which means a rotating pool with city parameters, and SixtyNet isn't that product.

## How you're billed, and where a $25 flat fee wins

Three billing models show up in this market. Prepaid per gigabyte with no expiry (ZentisLabs, ResiFactory) means you buy a block, spend it whenever, and top up. Success-based billing (Helodata) charges per successfully collected SERP page. Flat monthly with traffic included is what SixtyNet does, and it behaves differently because the cost doesn't move when your request count moves.

That makes the comparison purely a threshold question. Divide the flat fee by the per-GB rate you'd otherwise pay:

- $25 ÷ $4.79/GB ≈ **5.2 GB** of monthly traffic
- $25 ÷ $1.50/GB ≈ **16.7 GB**
- $25 ÷ $0.75/GB ≈ **33 GB**

Below about 5 GB a month, a prepaid per-GB pool is cheaper than the flat fee and there's no argument. Above roughly 17 GB, the $25 box undercuts ResiFactory's entry rate. Above 33 GB it beats even the cheapest from-$0.75 rate listed above. Since nobody publishes a SERP-to-GB conversion, you have to measure your own burn before you can place yourself on that scale.

There's a second variable the arithmetic hides: $25 buys one address, not ten thousand. That's fine when your volume is low enough that a single clean IP can carry it, which is exactly the situation where a large rotating pool is more infrastructure than the job needs. It stops being fine the moment your keyword list outgrows one IP's daily ceiling.

## When you don't need a residential IP at all

Three cases where the right answer costs nothing or costs less:

**You only care about your own site.** Google Search Console already reports your average positions for free. If that's the whole question, no proxy solves anything you can't already see.

**You need a few hundred to a few thousand US keywords daily.** A handful of static residential IPs plus a scheduler is the lean setup, and SixtyNet is one way to buy those IPs at $25 each. Leastslow sells the same shape on a per-IP basis from a Virginia ISP, which is worth pricing if a fixed US East location suits you better than a Los Angeles one.

**You need tens of thousands of keywords.** At that size, a managed SERP API or a large rotating network is the practical answer. Running that volume through a small pool of static addresses will just get the addresses burned.

Build or buy is a real fork and both sides work. Building gives you control over exactly which variables you pin and how you parse; buying a parsed SERP API trades that control for less to operate. Either way the discipline is identical: measure public search results, respect each engine's terms of service and robots directives, and query politely enough that you don't degrade the service you depend on.

## Before you order: five things to confirm

- **The refund window is short.** Third-party reviews of the residential line report a 3-day money-back period, well under the 30 days most hosts offer. Assume you have one weekend to prove the IP works for your pipeline.
- **Stock moves.** The residential order page lists availability per plan and can show none available. Check before you plan a rollout around a specific box count.
- **Payment methods may be limited.** Reviews report that card payments were suspended for fraud-prevention reasons; check what the checkout page currently accepts before you commit.
- **Ports 80 and 443 are closed.** Fine for outbound scraping, fatal for hosting anything public.
- **Where does the IP land?** Ask support which market the assigned AT&T Mobility address resolves to. A residential IP is only useful for rank tracking if it sits in the market you're measuring.

## The rule I'd use

Track one country at national level, a few hundred to a few thousand keywords, daily top-20: one Residential-STARTER at $25/month, and add a box each time your list outgrows the last one. Need mobile SERPs as well: put the phone checks on the Mobile VPS line instead of spoofing a user agent. Need city-level local packs, or tens of thousands of keywords: SixtyNet is the wrong tool, and a city-capable rotating pool or a SERP API is where your money should go.

👉 [Check the residential plan prices and current availability before you decide](https://sixtynet.net/aff.php?aff=39)
