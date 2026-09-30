## IMQRScan QR Code Tracking: One Code, No Way to Compare Placements

A lightweight reference implementation for generating and tracking QR codes tied to individual campaign placements. Built to demonstrate real [QR Code Marketing Examples](https://imqrscan.com/qr-code-marketing) at the placement level, this project solves one core problem: a single shared code, reused across every placement, makes location-level performance impossible to measure once the material has already been printed and distributed.

### The problem this solves

Most QR code setups follow the same pattern. One code gets generated then reused across a flyer, a counter card, a poster, sometimes several store locations running an identical promotion. At the design stage, this feels efficient. One code, one file, nothing extra to manage or track separately.

The trade-off only becomes visible after the campaign has run its course. A shared code can report exactly one thing: a total scan count. It cannot say which specific piece of material produced those scans. If a flyer, a counter card and a poster all funnel through the same code, there is no way afterward to determine which placement actually worked, whether a specific store location's foot traffic came from the code at all or whether an entire batch of printed material is simply being ignored by the people walking past it.

This becomes a hard limitation the moment a campaign spans more than one variable more than one store, more than one version of an offer, more than one placement type. Five locations running the same promotion through one shared code cannot be compared against each other once the campaign is over. The scan count exists as a single, flat number. The breakdown that would make that number actionable was never built into the setup in the first place.

Once material is in circulation, the placements are fixed. Flyers are already distributed. Posters are already mounted. Packaging has already shipped. If everything ran through a single code from day one, there is no way to retroactively split the resulting data by location, store, or campaign version. That information was never generated, and a single scan total cannot be reverse-engineered into a location-by-location breakdown after the fact.

### What this project demonstrates

The core idea is generating a distinct, trackable path per placement rather than pointing everything at a single shared destination. Each path routes through a server-side redirect, which logs the hit, timestamp, referrer and a placement identifier, before forwarding the visitor to the actual destination URL. The logging happens before the redirect completes, so no scan goes unrecorded, and no third-party analytics dashboard is required to reconstruct what happened afterward.

This matters more than it sounds. A server-side log, even a simple one, already contains everything needed to answer the question a shared code can never answer: which specific placement produced which specific result. No dashboard, no subscription, no third-party service standing between the scan and the data.

### Use cases this pattern supports

* **Retail displays** - separate paths for a window display versus a checkout counter, compared afterward to see which placement actually drove more scans within the same store
* **Restaurant table cards** - one path for a digital menu, a separate path added later specifically for review requests, so each can be measured independently instead of blending into one number
* **Event check-in** - a distinct path per session room, doubling as both an entry mechanism and a way to measure attendance against session length afterward
* **Packaging inserts** - a path whose scan timestamp reveals when customers actually engage after delivery, rather than assuming a fixed window based on guesswork
* **Multi-location campaigns** - the same promotion distributed across several stores, each through its own location-specific path, so underperforming placements can be identified by data instead of assumption

### What the data actually shows once it's split apart

A single shared code, over a month, produces one number: total scans. Split by placement, that same volume of traffic tells a completely different story. Usually one or two placements account for most of the activity, and the rest produce almost nothing. That pattern is invisible in a combined total. It only becomes visible once each placement has its own path and its own log.

This is where the real value sits. Not in generating a code which takes seconds regardless of approach but in being able to say afterward, with actual data, which specific piece of printed material earned its place in the next campaign and which one is quietly wasting print budget every time it gets reordered.

### Why this matters before the print run, not after

This setup decision has to happen before material goes to print, not after. Once a code is already circulating on physical material, its structure cannot be changed without reprinting. Deciding on a per-placement path at generation time is the only point where this is inexpensive to fix. Retrofitting it afterward means the data that would have answered the question was simply never collected in the first place, and no amount of analysis after the fact can recover it.

The fix costs almost nothing at the design stage. A short, distinct path per placement, and a log recording what came through it. What it prevents is a campaign ending with nothing more to show for it than a single number nobody can act on.

