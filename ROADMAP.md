# Joyful — Phased Product & Business Roadmap

This is the master roadmap. It's opinionated. It will change. That's fine — the discipline is in revisiting it monthly and being honest about what you've learned.

---

## Phase 0: Foundation
**Duration:** Weeks 1–8 | **Goal:** Know your customer deeply before writing a line of code

### What you're doing
This phase is about **learning, not building**. The single biggest mistake early founders make is building before they truly understand the problem. You have a hypothesis — go test it.

### Customer Discovery (Weeks 1–4)
**Target: 50 parent interviews**

Who to talk to:
- Parents with kids ages 4–14 (your core demographic)
- Mix of: dual-income households, single parents, parents in suburbs vs. urban areas
- Find them: your own network, school parent groups, Facebook parenting groups, nextdoor.com

Key questions to ask:
1. *Walk me through the last time you tried to find a new activity for your kid.* (Listen for the friction.)
2. *Where did you end up finding it? Who did you ask?* (Listen for trust signals.)
3. *How much time per week do you spend on "kid logistics"?* (Quantify the pain.)
4. *Tell me about a time a recommendation from another parent turned out to be amazing.* (Understand the delight.)
5. *What tools do you use today to manage your family's schedule and activities?* (Know the competition.)
6. *If you could wave a magic wand and fix one thing about parenting logistics, what would it be?*

What you're listening for:
- The words they use (steal their language for your copy)
- Moments of visible frustration or delight
- Workarounds they've invented (signs of real pain)
- Who they trust and why

### Validation Goals (Weeks 3–6)
- **Problem validation**: Can you get 80%+ of parents to say "yes, this is a real problem" when you describe it back to them?
- **Solution validation**: When you describe the MVP, do they say "where do I sign up?" or do they look politely confused?
- **Trust graph validation**: Do parents light up when you say "recommendations from parents you actually know"? (You're betting yes.)
- **Willingness to pay**: Ask directly — "If this existed and worked well, what would you pay for it?" Then stop talking.

### Business Foundation (Weeks 1–8, parallel)
- [ ] **Incorporate** — Delaware C-Corp if you plan to raise VC; LLC if you're bootstrapping. Use Stripe Atlas or Clerky (takes 1 week, ~$500).
- [ ] **Trademark search** — Search "Joyful" (or your chosen name) at USPTO.gov. Hire a trademark attorney for the filing (~$1,500).
- [ ] **Domain + social handles** — Lock them in now. Variations of your brand name across .com, Instagram, TikTok, X.
- [ ] **Waitlist landing page** — A single page describing the vision and capturing emails. Use Framer or Webflow, no engineers needed. Goal: 500 emails before you launch.
- [ ] **Bank account** — Mercury Bank (free, startup-friendly, good APIs for later).
- [ ] **CAP table** — Even if it's just you, set this up in Carta from day one.

### Team Decisions (Weeks 4–8)
The most important decision in Phase 0 is **how you'll build**. You have three options:

**Option A: Find a Technical Co-Founder**
- Best outcome if you find the right person
- Hardest to execute — takes 2–4 months to find/vet someone good
- Look in: your network, YC co-founder matching, Lunchclub, developer communities

**Option B: Hire a Small Agency / Studio**
- Faster to start (2–4 weeks)
- More expensive ($15K–$40K for Phase 1 MVP)
- Risk: agencies optimize for delivery, not learning
- Good choice if you want to validate quickly before hiring

**Option C: Hire 1 Full-Stack Engineer**
- The pragmatic middle path
- $140K–$180K/year in a major city (or $80–120/hr contract)
- Gives you dedicated capacity + someone who's bought in
- Requires you to be a good product partner

**Recommended:** Start Option B to build your waitlist-gathering proof of concept while you pursue Option A or C in parallel.

### Phase 0 Exit Criteria
- [ ] 50 parent interviews completed, insights documented
- [ ] Problem + solution validated with > 70% of interviewees
- [ ] Company incorporated
- [ ] 500 waitlist emails captured
- [ ] Build path decided (co-founder / agency / engineer)
- [ ] $50K–$150K in initial capital (personal savings, friends & family, or pre-seed)

---

## Phase 1: Trusted Discovery + Coordination MVP
**Duration:** Months 2–5 | **Goal:** 500 active families, NPS > 50

### The Core Bet
Parents don't trust Yelp reviews from strangers. They trust Sarah from soccer, who has a kid the same age and similar values. **Joyful's moat is the social trust graph.** Recommendations filtered through people you actually know are 10x more valuable than crowd-sourced reviews.

The AI layer amplifies this: it knows your kids, it knows your network, and it surfaces the right recommendation at the right moment.

### What to Build (in priority order)

**1. Family Profile (Week 1–2 of build)**
- Parent name, location (zip code), phone/email
- Kids: name, age, interests (select from curated list + free text)
- Quick onboarding: < 3 minutes to complete

**2. Trust Network (Week 2–4 of build)**
- Import phone contacts to find other Joyful families
- Connect by school (enter school name → see other parents)
- Manual invite: share a link to invite specific parents
- "Trust" is explicit: you choose who's in your network, not everyone at a school

**3. Activity Discovery Feed (Week 3–6 of build)**
- AI-curated feed based on: kids' ages + interests + location + what trusted network recommends
- Activity cards: name, age range, location, price, trusted endorsements ("3 parents you know recommend this")
- Categories: classes, camps, experiences, free/outdoor, enrichment, sports
- Filters: age, distance, price, available spots, endorsed by network

**4. Simple Rating System (Week 4–5 of build)**
- After an activity: "Would you recommend this to another family?" → Thumbs up / thumbs down
- Optional: short note ("great for ages 6-8 who love building things")
- This is your data flywheel. Guard it carefully — quality over quantity.

**5. Coordination Layer (Week 5–8 of build)**
- "Who else is going?" — see network activity RSVPs
- Share an activity with a specific parent
- Group formation: "Starting a weekly gymnastics carpool — anyone interested?"
- Group messaging (keep it simple: threaded comments on an activity)

**6. AI Discovery Assistant (Week 6–8 of build)**
- Natural language search: "Find me a pottery class for my 7-year-old on Saturday mornings"
- Proactive suggestions: "Based on Emma's love of animals, you might like..."
- Weekly digest: "Here's what's happening in your network this week"

### What NOT to Build in Phase 1
- ❌ Full calendar integration (Phase 2)
- ❌ In-app booking / payments (Phase 2)
- ❌ Carpool matching (Phase 3)
- ❌ Developmental tracking (Phase 4)
- ❌ Native mobile app (optimize the mobile web experience first)
- ❌ Anything requiring more than 1–2 engineers to build

### Activity Data Strategy
You need a catalog of activities to power discovery. Three approaches:

1. **Scrape + clean public sources**: Google Places, Yelp, local parenting blogs. Use AI to categorize and enrich. This gets you breadth fast.
2. **Manual curation in key launch cities**: Have someone (a contractor, or you) manually build out 200–500 quality activities per launch city. This gets you quality.
3. **User-submitted**: Let parents add activities they love. Lower quality at first, but scales.

**Recommended**: Start with manual curation in 1–2 cities, layer in scraped data with AI quality filtering, enable user submissions for long tail.

### Launch Strategy
**Don't launch to everyone. Launch deep into 3 communities.**

- Choose 3 schools or neighborhoods in the same city
- Find a "champion parent" at each — someone well-connected who genuinely loves the product
- Offer them: free premium access, early input on product direction, recognition as founding community member
- Goal: 150–200 active families per community before expanding
- Why this works: network effects require density. A discovery app with 5 parents in your network is useless. One with 50 is magic.

### Phase 1 KPIs
| Metric | Target at 90 days | Target at 5 months |
|---|---|---|
| Registered families | 200 | 500 |
| Weekly Active Families | 100 | 300 |
| Activities in catalog | 500 | 2,000 |
| Network connections/family | 3+ | 8+ |
| Ratings submitted | 500 | 3,000 |
| NPS | > 40 | > 50 |
| Retention (W4) | > 40% | > 50% |

### Phase 1 Exit Criteria
- [ ] 500 active families with real weekly engagement
- [ ] NPS > 50 (this is the signal the core loop is working)
- [ ] Average of 8+ trusted network connections per family
- [ ] Evidence of the "social flywheel": new families joining because friends invited them
- [ ] Identified the top 3 features users are begging for (these inform Phase 2)

---

## Phase 2: Scheduling + Booking
**Duration:** Months 5–9 | **Goal:** $10K MRR, 2,000 families

### Why This Comes Next
You've proven parents trust your discovery. Now they're saying: *"Great, I found the activity — can you help me actually get us there?"* Scheduling is where discovery converts to habit. Booking is where you start generating revenue.

### What to Build

**Scheduling:**
- Sync with Google Calendar and Apple Calendar (read + write)
- Add activities directly to family calendar from the app
- Conflict detection: "Emma already has swim practice that time"
- Family calendar view: all kids, all caregivers, at a glance
- Smart reminders: "Piano tomorrow at 4pm — here's what to pack"
- Recurring activity management

**Booking:**
- Partner with 20–30 activity providers in your launch city
- In-app booking: see availability, reserve spots, pay
- Commission model: you take 10–15% of each booking
- Provider portal: simple dashboard for activity providers to manage availability
- Booking confirmation + reminders
- Waitlist management

**Introduction of Paid Plans:**
- Phase 1 is free to drive adoption
- Phase 2 is when you introduce premium: $12/month or $99/year
- Premium features: calendar sync, booking, unlimited AI searches
- Free tier: discovery + coordination (keep the network growing)

### Phase 2 KPIs
| Metric | Target |
|---|---|
| Active families | 2,000 |
| MRR | $10,000 |
| Booking providers | 30+ |
| Bookings/month | 500+ |
| Calendar connections | 60% of premium users |

---

## Phase 3: Carpools
**Duration:** Months 9–14 | **Goal:** 10,000 families, carpooling as a retention driver

### Why This Is Hard and Why It Matters
Carpooling sounds simple. It isn't. It requires trust (I'm putting my kid in your car), coordination (schedules, routes, cancellations), and consistency (recurring commitments). But when it works, it creates deep lock-in — families who carpool together don't churn.

### What to Build

**Carpool Matching:**
- "Find carpool matches" for a specific activity/school
- Matching algorithm: proximity, schedule overlap, trust network overlap (prioritize people you know)
- Proposed carpool with terms: who drives which days, pickup/dropoff locations
- In-app acceptance and agreement

**Carpool Management:**
- Recurring schedule management
- Day-of coordination: running late notifications, substitute driver requests
- Route optimization (integrate with Google Maps)
- Group messaging for carpool group

**Safety Layer:**
- Driver verification (driver's license + insurance on file)
- Emergency contact management
- "Kid arrived safely" notification

**Why trust network matters here**: Carpool matching from within your trusted network dramatically reduces the "stranger danger" friction. This is your moat against standalone carpool apps.

---

## Phase 4: Developmental Insights
**Duration:** Months 12–18 | **Goal:** 25,000 families, 3+ insights/family/month

### The Shift: From Logistics to Development
This is where Joyful starts becoming something deeper than a logistics tool. You're now helping parents be more *intentional* about their kids' development.

### What to Build

**Age-Appropriate Recommendations:**
- Activity recommendations layered with developmental context: *"At 7, kids thrive with activities that build mastery — here's why pottery is great right now"*
- Draws on established developmental frameworks (Montessori, positive psychology, pediatric guidelines)
- Curated by child development experts (hire an advisory board)

**Insight Cards:**
- Weekly "developmental moments" delivered to parents
- Short, actionable, specific to your child's age and interests
- Example: *"Mia is at a great age for responsibility. Here's a simple way to start this week."*

**Growth Awareness (NOT Tracking):**
- Soft signals from parent inputs: what activities they've done, what their kids are loving
- No surveillance, no grades, no anxious comparison
- Framing: "wonder portfolio" not "achievement tracker"

**Expert Content Network:**
- Partnership with pediatricians, child therapists, educators
- Vetted, non-preachy, culturally sensitive content
- This becomes a content moat over time

---

## Phase 5: Family Graph
**Duration:** Months 16–22 | **Goal:** Network density > 5 connections/family

### The Full Relationship Map
- Extended family coordination (share activities with grandparents, invite to events)
- Teacher and coach connections (with appropriate privacy controls)
- Friendship visibility: which kids are friends with which kids (useful for activity and carpool matching)
- Life stage transitions: new school year setup wizard, new baby mode, summer planning mode

### Why This Creates the Moat
A family graph with real relationship data is extraordinarily hard to replicate. When Joyful knows that Emma's best friend is Zoe, that Zoe's mom is in your trust network, that both families use the same soccer coach, and that they live 3 blocks apart — the quality of recommendations and coordination that becomes possible is years ahead of any newcomer.

---

## Phase 6: AI Concierge
**Duration:** Months 20–28 | **Goal:** $1M ARR, 50,000 families

### The Full Vision Realized
This is the agent parents actually wanted all along: a knowledgeable, proactive family COO that handles the coordination layer of parenting entirely.

### What to Build

**Proactive Planning:**
- *"Summer break is 6 weeks away. Based on what your kids loved last year, here are 3 camp options I'd suggest. Want me to check availability and hold spots?"*
- *"Jake's been doing soccer for 2 years. Several parents in your network have moved to this club team — want me to find out more?"*

**Conversational Interface:**
- Voice and text
- Multi-turn: *"Find a piano teacher" → "Something on Tuesday afternoons" → "Near our new house on Elm Street" → "Under $100/hour"*
- The agent remembers context across sessions

**Full Coordination Execution:**
- Book it, schedule it, coordinate the carpool, add it to the calendar, set the reminders — all from one conversation
- Integrations with Venmo/Zelle for splitting costs
- Automated check-ins: *"How was the first piano lesson?"* → feeds back into recommendations

**Household Intelligence:**
- Budget awareness for family activities
- Seasonal planning (school year, summer, holiday breaks)
- Sibling coordination: *"You have 3 kids in different activities — here's how to restructure so Saturdays aren't chaos"*

---

## What Success Looks Like

### 12-Month Vision
- 10,000 active families across 3 cities
- $25K MRR
- Seed round of $2–3M raised
- Team of 5–8 people
- NPS consistently > 60

### 24-Month Vision
- 75,000 active families, 8–10 cities
- $500K MRR
- Series A of $8–12M raised
- Team of 20–30
- Marketplace GMV > $5M/year

### 36-Month Vision
- 500,000 active families
- National product with local depth
- $5M+ MRR
- The default "family operating system" for US parents

---

*Review this roadmap monthly. Mark what's done, what changed, and why.*
