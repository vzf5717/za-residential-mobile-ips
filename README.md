# South Africa proxies: picking real ZA residential and mobile IPs for Takealot, Google.co.za and ad verification

Most "South Africa proxy" listings are lying to you in a small, specific way. You buy a ZA exit, run a quick check, and the IP resolves to Amsterdam or Frankfurt. Or the pool does have ZA addresses, but there are only a few thousand of them, and half are already burned by other buyers scraping the same Takealot listings you want.

South Africa is a small proxy market. The country has roughly 600 ASNs and a few million consumer IPs in total, which is why some providers quietly route "ZA" traffic through neighbouring regions or lean on a thin pool of recycled addresses. If your project depends on seeing the country the way a local sees it — pricing in rand, Google.co.za rankings, ads served to a Johannesburg audience — a thin pool shows up fast as CAPTCHAs, wrong prices and inconsistent SERPs.

So the useful question isn't "which provider says it has South Africa." It's which one has enough ZA residential and mobile supply to survive a real workload, and how much per gigabyte that costs you. This piece works through the ZA-specific details that actually change results, and uses DataImpulse as the concrete example because its ZA residential and mobile traffic sits at the cheap end of the market.

## What people actually need when they search for South Africa proxies

The phrase covers at least four different jobs, and they don't want the same IP type.

**E-commerce and price intelligence.** Takealot is the big one, with Amazon.co.za and Makro worth watching too. Prices, stock status, delivery estimates and promo badges often only render correctly for a local IP. Product pages are also the heaviest thing you'll scrape here, since you're loading images, scripts and review blocks.

**SERP and local rank tracking.** Google.co.za results shift by city, and Google is aggressive about flagging datacenter ranges. If you're tracking a client's rankings in Cape Town, a country-level average tells you very little.

**Ad verification.** Checking that a campaign shows up in ZA, with the right creative and the right landing page, requires an exit that looks like a real South African connection.

**Platform and app access.** Ticket sites, regional streaming platforms, and mobile-first apps that treat cellular IPs differently from home broadband.

Residential IPs cover most of that. Mobile IPs on Vodacom, MTN or Telkom SA networks are the fallback when a target is tuned to distrust anything that isn't a phone. Datacenter ranges are cheapest and fastest, but in this market they get spotted quickly, so treat them as suitable only for soft targets.

## The ZA network details that decide whether your scrape works

A few local facts are worth knowing before you configure anything.

South African consumer traffic runs through a handful of major providers: Vodacom, MTN South Africa, Telkom SA, Cell C and Rain, with fixed-line fibre from Afrihost, Vox Telecom, Herotel, Metrofibre and others. Carrier and ASN matter if you're building a mobile profile on a specific network.

Currency is the rand, the timezone is UTC+2 (SAST, which lines up with Johannesburg), and the local search engine is google.co.za. Two languages dominate: English and Afrikaans.

City targeting is where most buyers overpay or under-specify. Johannesburg, Cape Town, Durban, Pretoria and Gqeberha are the cities that matter for pricing and rank checks. Country-level targeting is usually enough for ad verification and for stock checks where you just need to see the ZA storefront. It is not enough for genuine local rank tracking.

Also worth knowing: proxy supply in any single ZA city is fluid for every provider in the industry. Devices connect and disconnect constantly, so a city that looks strong this week can thin out next week. Build your job so a country-level exit is an acceptable fallback.

## Setting up South Africa targeting in DataImpulse

DataImpulse keeps ZA residential traffic inside its main pool of 90M+ ethically sourced IPs across 195 countries, with country targeting included at no extra cost. South African mobile IPs are available at $2/GB, which is unusual at this price point — most providers push mobile traffic at $5/GB and up.

Setting the exit country is done in the proxy username, not in a dashboard toggle:

> `YOUR_LOGIN__cr.za:YOUR_PASSWORD@gw.dataimpulse.com:823`

For multi-step flows like a Takealot listing sweep that needs the same IP across several requests, append a session ID:

> `YOUR_LOGIN__cr.za:YOUR_PASSWORD@gw.dataimpulse.com:823` with `;sessid.xxxx`

Connection details, since these trip people up:

- **Rotating sessions:** HTTP/HTTPS on port 823, SOCKS5 on port 824. New IP per request.
- **Sticky sessions:** ports 10000–20000. You can request 1 to 120 minutes; DataImpulse's team says the average session holds around 30 minutes, with 30 minutes as the default when you don't specify. Because the IPs come from real devices, a sticky session ends early if the real user goes offline. Plan for that rather than assuming a clean 120 minutes.
- **Protocols:** HTTP, HTTPS and SOCKS5, which covers Scrapy, Playwright, Puppeteer, Selenium, curl and most antidetect browsers.

One verification step is worth the ten seconds. Before you scale anything, hit an IP lookup through the proxy:


curl -x "http://USER:PASS@gw.dataimpulse.com:823" http://ip-api.com/json


If the response doesn't say South Africa, fix that before debugging your parser.

City, ZIP and ASN targeting exist, but they're a paid add-on on top of country targeting. If Cape Town specifically is a hard requirement for your rank tracking, price that in rather than assuming it comes free with the $1/GB rate. One independent review notes advanced targeting on the standard residential plan is billed at double the per-GB rate — that's a second-hand figure, so confirm it with support before you build a budget around city-level checks at volume.

👉 [Start with ZA country targeting on the $5 intro plan](https://bit.ly/dataimPulse)

## Every current DataImpulse plan, side by side

Four products, each with its own volume ladder. All of them are pay-as-you-go with no subscription, and purchased traffic doesn't expire.

| Proxy type and plan | Traffic included | Effective rate | Price | Billing | Get it |
| --- | --- | --- | --- | --- | --- |
| Residential — Intro | 5 GB | $1/GB | $5 | Pay-as-you-go, GB never expire | [Buy the $5 residential intro](https://bit.ly/dataimPulse) |
| Residential — Basic | 50 GB | $1/GB | $50 | Pay-as-you-go | [Buy 50 GB residential](https://bit.ly/dataimPulse) |
| Residential — Advanced | 1 TB | $0.80/GB | $800 | Pay-as-you-go, ~20% volume discount | [Buy 1 TB residential](https://bit.ly/dataimPulse) |
| Residential — Custom+ | 5 TB+ | Custom | From $4,000 | Pay-as-you-go, dedicated account manager | [Request a residential custom plan](https://bit.ly/dataimPulse) |
| Datacenter — Intro | 10 GB | $0.50/GB | $5 | Pay-as-you-go | [Buy the $5 datacenter intro](https://bit.ly/dataimPulse) |
| Datacenter — Basic | 100 GB | $0.50/GB | $50 | Pay-as-you-go | [Buy 100 GB datacenter](https://bit.ly/dataimPulse) |
| Datacenter — Advanced | 1 TB | $0.45/GB | $450 | Pay-as-you-go | [Buy 1 TB datacenter](https://bit.ly/dataimPulse) |
| Datacenter — Custom | 5 TB+ | Custom | From $2,250 | Pay-as-you-go | [Request a datacenter custom plan](https://bit.ly/dataimPulse) |
| Mobile — Intro | 2.5 GB | $2/GB | $5 | Pay-as-you-go | [Buy the $5 mobile intro](https://bit.ly/dataimPulse) |
| Mobile — Basic | 25 GB | $2/GB | $50 | Pay-as-you-go | [Buy 25 GB mobile](https://bit.ly/dataimPulse) |
| Mobile — Advanced | 1 TB | $1.60/GB | $1,600 | Pay-as-you-go | [Buy 1 TB mobile](https://bit.ly/dataimPulse) |
| Mobile — Custom | 5 TB+ | Custom | From $8,000 | Pay-as-you-go | [Request a mobile custom plan](https://bit.ly/dataimPulse) |
| Premium Residential — Intro | 1 GB | $5/GB | $5 | Pay-as-you-go | [Buy the $5 premium residential intro](https://bit.ly/dataimPulse) |
| Premium Residential — Basic | 10 GB | $5/GB | $50 | Pay-as-you-go | [Buy 10 GB premium residential](https://bit.ly/dataimPulse) |
| Premium Residential — Custom | 5 TB+ | Custom | From $20,000 | Pay-as-you-go, all targeting included | [Request a premium residential plan](https://bit.ly/dataimPulse) |

A few notes on reading that table.

The residential ladder is unusually flat. Between roughly 5 GB and 850 GB you pay the same $1/GB, and the only real discount step is at 1 TB, where the rate drops to $0.80/GB. Buying the Basic 50 GB plan doesn't save you anything per gigabyte over topping up the intro; it just means fewer top-ups. If your ZA workload is seasonal, there's no penalty for staying small.

Premium Residential is a different pool, not a bigger version of the same thing, and it's priced at five times standard residential. It bundles the finer targeting options and adds a dedicated account manager. For most South African price-tracking and SERP jobs, standard residential on a ZA exit is the sensible starting point, and premium only earns its rate when your targets reject the standard pool.

Mobile traffic costs double residential, and for most ZA tasks that premium isn't justified. Takealot, Google.co.za and standard ad checks read residential IPs fine. Reach for mobile when the target specifically treats cellular connections differently, or when you're working with app data.

Those rate levels are the published 2026 figures. Entry prices and volume steps move, so check the live pricing page before you commit budget. The $5 entry applies to your first purchase; one review reports later top-ups carry a $50 minimum, which is worth confirming if you plan to test in small increments.

## What 5 GB of South African traffic actually buys you

Bandwidth estimates float around the internet, and most of them are wrong for your specific job. Don't guess — measure.

DataImpulse's dashboard breaks usage down by site, request count and traffic consumed in one-minute intervals. Run a few hundred requests against your real ZA targets, look at the bytes per successful request, then multiply by your expected monthly volume. A plain HTML SERP response and a fully rendered marketplace product page with images, scripts and reviews are orders of magnitude apart, so a blanket estimate is worthless.

The practical framing: $5 buys 5 GB of ZA residential traffic. If your per-request average lands around 200 KB, that's on the order of 25,000 requests. If you're loading heavy marketplace pages at a couple of megabytes each, the same $5 covers roughly a tenth of that. The dashboard tells you which world you're in within a few minutes of testing.

This is also the argument for pay-as-you-go over a monthly plan. Rank tracking spikes during audits and reporting weeks and sits quiet in between. If unused gigabytes vanish at the end of the billing cycle, you're paying for capacity you never used. Non-expiring traffic makes the uneven schedule cost-neutral.

👉 [Test ZA residential traffic with a $5 intro plan](https://bit.ly/dataimPulse)

## Where DataImpulse fits for South Africa, and where it doesn't

**It fits well when** you need cheap rotating ZA residential or mobile IPs, you're integrating proxies into your own stack, and your workload is uneven. HTTP/HTTPS and SOCKS5 both work, country targeting is free, and the published success rate is 99.51%. DataImpulse also advertises a 4.8/5 rating on G2 and runs human 24/7 support over live chat, with documented codeless setup guides for common frameworks.

**It doesn't fit when** you need a dedicated static IP that stays with one account for months. DataImpulse's public lineup is built around rotating residential, premium residential, mobile and datacenter networks. There's no standalone static ISP product, and for multi-account work on marketplaces or ad platforms, a stable residential-looking IP per profile is often what the job actually requires. One review makes this point directly: for multi-accounting, ISP proxies are usually the better tool.

Three other practical limits:

- **No free trial.** Access starts at a $5 minimum purchase. The intro plans do carry a 7-day money-back guarantee on card payments, provided you've used less than 80% of the traffic. Crypto purchases on intro plans are non-refundable.
- **No enterprise SLA at the $1/GB price point.** If you need contractual uptime guarantees and account management, that's the 1 TB+ tiers or a different provider with a contract.
- **Datacenter ranges get flagged.** DataImpulse is fairly open that its datacenter IPs are faster and cheaper but easier to detect. Fine for Bing, technical audits and high-volume checks where occasional blocks don't matter. Not the tool for Google.co.za rank tracking.

## What ZA-capable proxies cost elsewhere

For context, 2026 market ranges sit around $1–8/GB for residential, $2–15/GB for mobile (4G/5G), $0.50–3/GB for datacenter, and roughly $1.50–5 per IP per month for ISP/static residential.

Within those ranges, the pay-as-you-go budget tier clusters near $1–3/GB and the enterprise naming rights go for $6–8/GB and up. Rates published in DataImpulse's own provider comparison put Decodo near $4/GB for residential, SOAX around $3.60/GB, IPRoyal from about $7.35/GB, and Oxylabs or Bright Data around $8/GB standard. Those are a vendor's numbers and worth spot-checking, but the shape of the market holds: you're paying three to eight times more for enterprise tooling you may not need if you're running your own scrapers.

One tip before you buy anywhere: check the provider's public location list. Several providers publish IP counts per country, which lets you confirm ZA supply exists before you pay rather than discovering it's thin after. Availability also shifts, so re-check if a ZA job suddenly starts failing.

## South Africa proxy questions worth answering

**Do I need mobile proxies for South Africa?**
Usually not. Residential ZA IPs handle Takealot, Amazon.co.za, Google.co.za and standard ad verification. Mobile earns its double price tag when a target reacts differently to cellular connections or when you're working with app-side data.

**Can I target Cape Town or Johannesburg specifically?**
Yes, but city and ZIP targeting is a paid add-on on top of the included country targeting, and it adds to your effective cost per gigabyte. For national price monitoring, country-level ZA is enough. For genuine local rank tracking, city targeting is the whole point.

**Does purchased traffic expire?**
No. Across all four products and all plan tiers, unused gigabytes stay in your account. That's the main reason a pay-as-you-go model suits seasonal ZA work better than a monthly plan.

**Is there a free trial?**
No. You start at $5. Card payments on intro plans have a 7-day refund window if you've used under 80% of the traffic.

**How long can a sticky ZA session last?**
You can request up to 120 minutes, with 30 minutes as the default. Because the IPs belong to real devices, sessions can end early when the user disconnects. Design your scraper to re-authenticate rather than assuming a fixed session length.

**Is using South Africa proxies legal?**
Routing traffic through a proxy isn't illegal in itself. What matters is what you do with it: collect only public, non-personal data, respect site terms and rate limits, and stay inside POPIA requirements if personal information is involved. Same rules as any other market.

If you want to see how ZA residential and mobile exits behave against your own targets before committing real budget, the $5 entry point is the cheapest way to find out — and the gigabytes don't disappear if the test takes a few weeks.

👉 [Check current DataImpulse plans and start a South Africa test](https://bit.ly/dataimPulse)
