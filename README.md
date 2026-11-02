# racknerd unmetered: How RackNerd's Unmetered Dedicated Servers Actually Work, What All 8 Plans Cost, and Which One Makes Sense for Your Workload

"racknerd unmetered" usually means one of two things when someone searches it: either they've heard RackNerd sells "true unmetered" dedicated servers and want to know if the claim holds up, or they're staring at a $599/month price tag and wondering which plan they actually need. Both get answered here.

Short version: RackNerd's unmetered line is real unmetered — a fully dedicated 10Gbps, 20Gbps, or 40Gbps port with no traffic cap, no fair-use policy, and no peak-hour throttling. The 10Gbps tier runs from $599 to $1,999 per month across six configurations, and there's a long-running promo code that knocks 15% off for the life of the server. Whether any of this is worth it depends almost entirely on how much you actually transfer, and we'll do that math below.

> **Quick pick:** For most bandwidth-heavy workloads (IPTV relay, file mirrors, VPN gateways), the $599/mo entry plan with a 10Gbps dedicated port is the sensible starting point — the CPU is older, but bandwidth-bound tasks don't care. 👉 [Check the current price of the $599 Limited Time Special plan](https://my.racknerd.com/aff.php?aff=11397&pid=746)

## What "unmetered" actually means here — and what it doesn't

At RackNerd, unmetered means you pay for port speed, not for bytes. The 10Gbps, 20Gbps, and 40Gbps plans all run on unshared dedicated ports, and the company explicitly states there are no restrictions on usage. That matters because "1Gbps unmetered" from a lot of budget hosts turns out to be a shared port with a fair-use clause — the kind that quietly drops you to 200Mbps on a Friday night. RackNerd's positioning is the opposite: sustained full line rate, 24/7, on a port nobody else touches.

Two details back this up. First, the unmetered servers ride on a multi-provider BGP network blend rather than a single upstream line, and every plan includes Noction IRP intelligent routing, which picks the best upstream path per destination in real time. Second, the bandwidth policy is stated on the official announcement pages, not buried in a ToS footnote.

One thing to watch for, though: RackNerd also sells a separate line of 10Gbps *specials* starting at $219/month that come with a **100TB monthly transfer cap** (hosted in Utah, on a premium network blend). Those are capped plans — they look similar on a spec sheet but are a different product. If your traffic is predictable and stays well under 100TB, a capped special can be the cheaper route. If your traffic is sustained, spiky, or hard to predict, that's exactly what the unmetered line is for. Comparing the two on port speed alone is meaningless.

## The full unmetered lineup, priced

All plans below are monthly billing, include 5 usable IPv4 addresses, root access, IPMI/KVM, remote reboot, custom ISO support (Linux, Windows, FreeBSD), and DDoS protection. The 10Gbps plans deploy in **Los Angeles, New Jersey, London, or Montreal**.

| Plan | CPU | RAM / Storage | Port | Price/mo | Order |
| --- | --- | --- | --- | --- | --- |
| Limited Time Special | Xeon E3-1230 V3 (4C/8T) | 32GB DDR3 / 1TB SSD | 10Gbps | $599 | [ Order the $599 plan](https://my.racknerd.com/aff.php?aff=11397&pid=746) |
| E-2136 | Xeon E-2136 (6C/12T) | 32GB DDR4 / 1TB NVMe | 10Gbps | $799 | [ Order the E-2136 plan](https://my.racknerd.com/aff.php?aff=11397&pid=747) |
| Dual E5-2630 V4 | 2× E5-2630 V4 (20C/40T) | 64GB DDR4 / 1TB NVMe | 10Gbps | $950 | [ Order the Dual E5-2630 V4](https://my.racknerd.com/aff.php?aff=11397&pid=748) |
| Dual E5-2695 V4 | 2× E5-2695 V4 (36C/72T) | 128GB DDR4 / 2×1TB NVMe | 10Gbps | $1,399 | [ Order the Dual E5-2695 V4](https://my.racknerd.com/aff.php?aff=11397&pid=749) |
| EPYC 7642 | EPYC 7642 (48C/96T) | 128GB DDR4 / 2×1TB NVMe | 10Gbps | $1,699 | [ Order the EPYC 7642](https://my.racknerd.com/aff.php?aff=11397&pid=750) |
| EPYC 7702P | EPYC 7702P (64C/128T) | 128GB DDR4 / 2×1TB NVMe | 10Gbps | $1,999 | [ Order the EPYC 7702P](https://my.racknerd.com/aff.php?aff=11397&pid=751) |
| 20Gbps Unmetered | E3-1230 V3 | 16GB / 1TB SSD | 20Gbps | $1,499 | [ Order the 20Gbps plan](https://my.racknerd.com/aff.php?aff=11397&pid=752) |
| 40Gbps Unmetered | E3-1230 V3 | 16GB / 1TB SSD | 40Gbps | $2,799 | [ Order the 40Gbps plan](https://my.racknerd.com/aff.php?aff=11397&pid=758) |

The EPYC 7642 has a published PassMark score of 60,115 on the official page — useful for comparing multi-core muscle across the lineup, though a synthetic score won't tell you how a specific application behaves on it.

## Which plan fits which workload

Do the bandwidth math before picking a tier, because it kills most of the indecision. A 10Gbps port at theoretical line speed moves roughly 1.25GB per second, and real-world throughput lands somewhat below that once protocol overhead, storage, and routing get involved. On the demand side: 5,000 concurrent viewers at 2.5Mbps each is about 12.5Gbps of aggregate traffic — which is exactly why streaming relays end up on this hardware tier.

Some concrete rules of thumb:

- **$599 Limited Time Special.** The E3-1230 V3 is the oldest CPU in the lineup, but for bandwidth-bound work — file distribution, proxies, network services — it still saturates a 10Gbps port without breaking a sweat, and DDR3 vs DDR4 barely registers when the network is the bottleneck. Officially tagged as a limited-time special, so if the spec fits, it's the one to grab. Just know its limits: don't plan heavy virtualization or anything needing modern instruction sets on it.
- **$799 E-2136.** The cheapest plan with NVMe storage. That jump from SATA SSD to NVMe matters for random I/O, local caching, database activity, and high-concurrency file operations. Still 32GB of RAM, so it won't host a large virtualization fleet.
- **$950 Dual E5-2630 V4.** Twenty cores and forty threads make sense for build systems, content processing, application workers, and moderate virtualization. Note for anyone running per-core licensed software: check how your license counts sockets and cores before ordering a dual-CPU box.
- **$1,399 Dual E5-2695 V4.** With 128GB of RAM and two NVMe drives, this is the tier for larger VM groups, containers, and caching layers. One caveat worth flagging: the listed specs don't state a RAID level, so if storage redundancy matters to you, sort out your backup approach before (or right after) deployment.
- **EPYC 7642 / 7702P ($1,699 / $1,999).** These exist for CPU-heavy throughput — AI/ML data pipelines, big per-core software workloads. If you don't have a specific reason to need 48–64 cores, the savings from staying lower in the lineup are substantial.
- **20Gbps / 40Gbps ($1,499 / $2,799).** Same E3-1230 V3 as the $599 plan, just faster ports. These make sense only when you've genuinely saturated a 10Gbps port or need headroom for aggregate traffic well past 12–13Gbps. Paying 2.5× the entry price for double the port when your CPU-bound workload won't fill it is money spent on nothing.

One honest counterpoint: if your monthly transfer on a stable 1Gbps line stays under roughly 50TB, a 10Gbps plan is mostly buying you redundancy and headroom, not capacity you're using. RackNerd's own 1Gbps unmetered line starts at $59/month, and that's where a lot of "I need unmetered" searches should actually land.

## What it really costs with the 15% lifetime promo

RackNerd runs a recurring promo code — **15OFFDEDI** — that takes 15% off all dedicated servers, and it applies every billing cycle for as long as you keep the server. It's published on RackNerd's own promotions pages, and it was still being advertised on the company's official blog as recently as October 2026, so it's an official standing offer rather than a flash discount.

The math on the entry plan: $599 becomes about $509 per month, which is roughly $1,080 saved per year. On the $1,999 EPYC 7702P, the code trims about $300 per month. Enter it in the promo field at checkout and confirm the recurring price shows the discount before you pay — that confirmation step is what makes the "for life" part real.

The unmetered plans are part of the dedicated server catalog, so the code applies to them. Payment covers PayPal, credit cards, Alipay, and some cryptocurrencies.

## Ordering, delivery, and the things worth checking first

Deployment is officially within 72 hours, and in most cases same-day. Every server ships with IPMI/KVM access, so you can reinstall the OS yourself whenever you want — RackNerd's own FAQ puts it plainly: you're in full control at all times. Custom configurations are possible too; if none of the stock specs fit, sales will quote a modified build.

Three things to do before clicking buy, all cheap to do and all worth it:

1. **Grab the test IP for your target datacenter** from the order form and run latency checks from where your users actually are. LA to London is a different product than LA to LA.
2. **Email sales if you have a hard deadline** or want the setup and cancellation terms in writing — the official page itself invites this for time-sensitive projects.
3. **Confirm DDoS protection coverage for your chosen location.** Plans are listed with DDoS protection, but coverage specifics vary by datacenter, and a quick pre-sales question settles it.

## FAQ

**Is the bandwidth really unlimited?**
For the unmetered plans covered here, yes — dedicated port, no transfer cap, no usage restrictions, per the company's own product pages and announcements. The separately-priced $219/month specials are the exception, and those carry a 100TB cap.

**Can I reinstall the OS later?**
Yes, self-service, through the included IPMI/KVM access. Custom ISOs for Linux, Windows, and FreeBSD are supported on all plans in this lineup.

**10Gbps or 20Gbps — how do I know?**
Add up your real aggregate demand. Under ~10Gbps sustained, the 10Gbps plans cover it; the 20Gbps tier exists for workloads that have already saturated 10Gbps or need aggregate capacity in the 12–20Gbps range (that 5,000-viewer × 2.5Mbps example lands right at the boundary). Skip the 40Gbps tier unless you're in the second category with room to grow.

## If you're still deciding

The decision tree is short. Sustained or unpredictable traffic that would swamp a 1Gbps line: the **$599 Limited Time Special** is the entry point, and the 15% promo takes it to roughly $509/month. Traffic with heavy random I/O or a database component: step up to the **E-2136 at $799** for the NVMe storage. Big virtualization or caching workloads: the **Dual E5-2695 V4 at $1,399**. Only reach for the 20Gbps or 40Gbps tiers when you've measured saturation on a 10Gbps port.

And before ordering, run the test IP from your primary user base — it takes two minutes and it's the cheapest way to avoid regretting a datacenter choice. When you're ready, 👉 [head to RackNerd's unmetered plans and pick the tier that matches your workload](https://my.racknerd.com/aff.php?aff=11397&pid=746), with the promo code applied at checkout.
