# ◎ Middlez

**Find the fairest place to meet.** Middlez helps a group pick a meeting spot in Singapore based on *travel time*, not geographic distance — so no one gets stuck with the longest trip.

🔗 **Live:** https://adamtoh97.github.io/middlez/v5/

v6 is wip (pending categorisation)

Designed by **Adam Toh**.

---

## What it does

- Add **2–10 participants**, each with a name, a postal code or address, and a transport mode (driving, public transport, walking, cycling).
- Geocodes every origin live, finds the **fairest meeting zone**, and shows the real travel time (and PT fare) for each person.
- Recommends nearby places — **shopping malls, restaurants, cafés, and activities** — ranked by fairness, popularity, and centrality, with category toggles.
- Visualises everything on an interactive map: origins coloured by trip length, routes, the meeting zone, and 10/20-minute travel rings.
- Produces a **shareable link** that encodes the whole session in the URL — no account, no database.

---

## How the fairness engine works

Picking the spot is a two-stage process so it's both accurate and fast:

1. **Shortlist (estimate):** a coarse grid over the group's area is scored with a quick distance-based model to nominate a handful of geographically diverse candidate spots.
2. **Score (live):** each finalist is measured with **real travel times** — OSRM for driving, OneMap for public transport — and ranked by a balanced fairness score (low total time + low longest trip + small gap between people).
3. **Refine (adaptive):** if the best spot is still lopsided, a short local search probes around it with live times to tighten toward the true balance point. Already-balanced results skip this step, and a per-search cache avoids repeat lookups.

This matters because Singapore's PT network is uneven — a purely distance-based optimiser would happily suggest a spot that's a quick drive for one person but a punishing multi-transfer trip for another. Scoring finalists on live times avoids that.

**Version History**
v2: lean version: 6 candidates, 4-direction refinement, max 2 rounds. Quickest, but the lightest search

v3: 8 candidates, 8-direction refinement, runs every time. Best at finding the fairest spot, but slowest — and it has no cache and no skip-when-balanced shortcut

v4: 7 candidates, 8-direction refinement, but with the two free speed wins: a per-search cache and skip refinement when the result is already balanced

v5: refine shopping mall to ignore departmental stores

v6 (wip): changes to categories (dine-in for both restaurants/fast food/cafes, filter out takeaways)
change activities category definition to entertainment and rank parks last

**Roadmap**
ST
1. Improve Fairness Score optimisation to understand rankings instantly
2. Better Loading Experience
3. Share Link + Voting
4. Saved Groups

LT
1. Outing planner (Purpose-Based Recommendations)
2. AI Venue Concierge
3. Date Planner (matchmaking?)
4. Holiday Planner
5. Carpool Optimizer
6. Weather-Aware Meeting Planner
7. Live Weekend Activity Finder
