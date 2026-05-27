# Phase 1 Deep Dive: Trusted Discovery + Coordination

This document is the build bible for Phase 1. Read it before every planning conversation with your engineers.

---

## The Problem You're Solving (In Parents' Own Words)

From customer interviews, here is the language parents use:
- *"I just ask people I know"*
- *"The Facebook group is overwhelming — I don't know who to trust"*
- *"Yelp reviews for kids' stuff are useless — they're from 2018 and there's no context"*
- *"I want to know what Sarah does with her kids — her kids are just like mine"*
- *"I spend hours every fall trying to figure out activities. It shouldn't be this hard."*

**The insight:** The information exists in parents' social networks. It's just trapped there — in iMessages, in conversations at school pickup, in group chats where the good stuff gets buried. Joyful's job is to surface and organize that trusted knowledge.

---

## User Journey: The Magic Moment

Here is the experience you are designing toward. This is your north star for Phase 1.

**The scenario:** It's September. Parent opens Joyful for the first time.

1. **Onboarding** (3 minutes): Enters kids' names, ages, interests. Connects phone contacts. Finds 12 parents they know already on Joyful.

2. **First discovery moment**: Feed shows: *"3 parents you know (including Jamie from soccer) recommend Brooklyn Robot Foundry for kids ages 6–10 who love building. $180/semester. Saturday mornings available."*

3. **The click**: Parent taps. Sees Jamie's note: *"Our son Leo (7) loved this. The instructors are amazing and patient."* Sees two other familiar names endorsing it.

4. **The share**: Parent texts their spouse: *"Jamie loves this place for Leo — can we check it out for Emma?"*

5. **The RSVP**: Parent sees at the bottom: *"2 families from your network are going to the open house this Saturday. Want to join them?"*

**This is the magic moment.** This is why people will tell their friends. Design every screen toward this.

---

## Core User Flows

### Flow 1: Onboarding
```
Welcome screen → 
Enter parent name + location → 
Add kids (name, age, interests) → 
Connect your network (phone contacts or school search) → 
See who's already on Joyful → 
First discovery feed
```

**Key design principles:**
- Each screen should feel like less than 30 seconds of effort
- Show the value as early as possible — if they have 3+ network connections, show them a personalized feed *before* they finish onboarding
- The "connect contacts" step is critical — make the value exchange explicit: *"We'll show you what parents you know are recommending. We never contact anyone without your permission."

### Flow 2: Discovery
```
Feed (curated for kids + network) → 
Activity card (name, age range, endorsements, location, price) → 
Activity detail (full description, all endorsements, photos, map) → 
Save / Share / RSVP
```

**Feed ranking logic (for your engineers):**
1. Activities endorsed by your trust network (highest weight)
2. Activities matching your kids' age + interests
3. Activities with high overall quality score
4. New activities added recently in your area
5. Activities your network is RSVPing to this week

### Flow 3: Adding a Recommendation
```
Search for activity (or add new one) → 
Rate: Would recommend? (Yes/No) → 
Optional note (1–2 sentences) → 
Optional: tag which kid and age → 
Share with network
```

**Keep rating frictionless.** The biggest enemy of your data flywheel is asking too much. A thumbs up and one optional sentence is enough. You can ask for more detail later.

### Flow 4: Coordination
```
On any activity: "Who else is going?" → 
See network RSVPs → 
Mark yourself as going → 
Optional: suggest a date → 
Notify others in network
```

---

## The Trust Graph: Technical Concepts Explained Simply

The "trust graph" is just a map of who trusts whom. Think of it like a web:
- Each parent is a dot
- Each connection between parents is a line
- You can only see recommendations that travel through YOUR lines

Why this matters technically:
- You need to store relationships between users ("User A trusts User B")
- When showing recommendations, you filter: *only show if at least one of User A's trusted connections has rated this*
- Strength of trust: a direct connection is stronger than a friend-of-a-friend

For Phase 1, keep it simple: **binary trust** (connected or not connected). Don't build weighted trust scores yet — that's Phase 5 territory.

**How users build their trust network:**
1. **Contact import**: Upload phone contacts → system finds matches → "You know these people" → one-tap connect
2. **School search**: Enter school name → see parent list (name + profile picture only) → connect with parents you recognize
3. **Direct invite**: Send a link via iMessage/WhatsApp
4. **Mutual connection**: "You both know [name] — would you like to connect?"

---

## Content Strategy: Building the Activity Catalog

You need activities in the catalog *before* you can deliver discovery value. This is the classic cold start problem. Here's how to solve it.

### Phase 1 Content Approach: Curated + AI-Enriched

**Step 1: Choose 1–2 launch cities**
Don't spread thin. Pick cities where you have personal connections and can do high-touch community building. Ideal: a mid-to-large city with strong parent community culture (Austin, Denver, Seattle, Brooklyn, Chicago neighborhoods).

**Step 2: Build a seed catalog (before launch)**
Hire a part-time content researcher ($20–25/hr, 20 hrs/week) to:
- Identify the top 300–500 kids' activity providers in your launch city
- For each: name, address, website, age range, price range, category
- This takes 4–6 weeks for a thorough job
- Total cost: ~$3,000–4,000

**Step 3: AI enrichment**
Use Claude (or similar AI) to:
- Write compelling activity descriptions from website copy
- Categorize and tag each activity
- Identify age ranges and interest matches
- Generate "why parents love this" summaries

**Step 4: Community-generated content**
Once you have early users, their ratings and notes become your best content. A parent's note — *"Great for kids who are too energetic for traditional classes — very unstructured and creative"* — is more valuable than any marketing copy.

### Content Categories (Priority Order)
1. **Classes + lessons**: Music, art, coding, language, cooking, STEM
2. **Sports + movement**: Soccer, gymnastics, swim, martial arts, dance
3. **Camps**: Day camps, specialty camps, holiday camps
4. **Experiences**: Museums, farms, escape rooms, nature activities
5. **Free + outdoor**: Parks, hiking trails, community events
6. **Tutoring + enrichment**: Academic support, test prep

---

## The AI Layer: What It Does (In Plain English)

The AI in Phase 1 does four things:

### 1. Personalized Ranking
Given what you know about a family (kids' ages, interests, location, trust network), sort the activity catalog to show the most relevant things first. This is recommendation system logic — not magic, just math with a lot of data.

### 2. Natural Language Search
When a parent types *"Something creative for a rainy Saturday with my 5-year-old"*, the AI understands what they mean and returns relevant results — even if none of the activity descriptions use those exact words.

### 3. Weekly Digest Generation
The AI writes a personalized weekly email/notification: *"Here's what's happening in your Joyful community this week..."* Personalized, not generic.

### 4. Recommendation Synthesis
When multiple network members have rated the same activity, the AI synthesizes their notes into a summary: *"Parents say the instructors are patient with beginners, class sizes are small, and it's worth the price — especially for ages 6–9."*

**What AI does NOT do in Phase 1:**
- It does not make decisions for parents
- It does not have long-form conversations (that's Phase 6)
- It does not have opinions about your parenting choices
- It does not track children's development

---

## Metrics That Matter in Phase 1

### The One Metric That Rules Them All
**Weekly Active Families (WAF)**: The number of families who open the app and take at least one action (view a feed item, add a rating, share an activity, RSVP) in a given week.

This is your heartbeat. If WAF is growing, you're doing something right. If it's flat or falling, everything else is noise.

### Supporting Metrics

| Metric | Why it matters | Red flag |
|---|---|---|
| Trust connections / family | Measures network density — key to value | < 3 connections after 2 weeks |
| Ratings submitted / WAF | Measures content flywheel health | < 0.5 ratings/active user/month |
| Discovery → RSVP rate | Measures if discovery is converting | < 5% |
| Week 1 → Week 4 retention | Measures if habit is forming | < 35% |
| Invites sent / family | Measures viral growth | < 1 invite/family/month |
| NPS | Overall satisfaction | < 40 |

### What NPS > 50 Tells You
An NPS above 50 means parents are enthusiastically recommending you to other parents. This is the signal that you've found product-market fit for Phase 1 and it's time to invest in growth. Don't scale before you hit this number — you'll just be scaling churn.

---

## Week-by-Week Build Schedule (8-Week MVP)

### Weeks 1–2: Data + Auth Foundation
- User accounts (login with Google/Apple)
- Family profiles (parent + kids)
- Activity database schema
- Seed catalog import (first 200 activities)

### Weeks 3–4: Trust Network
- Contact import and matching
- School search and matching
- Connection requests and acceptance
- Basic user directory (for your network)

### Weeks 5–6: Discovery Feed
- Activity cards and detail pages
- Basic recommendation feed (by age + location)
- Trust-network endorsement display
- Save / bookmark functionality

### Weeks 7–8: Ratings + Coordination
- Rating flow (thumbs up/down + note)
- "Who else is going?" RSVP feature
- Activity sharing
- Basic notifications (new endorsement from network, RSVP from network)

### Week 9: Polish + Waitlist Launch
- Bug fixes and performance
- Onboarding refinement
- Invite flow
- Soft launch to waitlist

---

## What You Should Be Doing Every Week During Phase 1

**As the founder / product leader (that's you):**
- Talk to 5–10 active users per week. Not surveys — actual conversations.
- Review your metrics dashboard every Monday morning. Write down what changed and your hypothesis for why.
- Be in the product daily. Use it yourself. Feel the friction.
- Run weekly syncs with your engineer: what shipped, what's blocked, what's next.
- Stay close to your champion parents. They are your product advisory board.

**The questions to always be asking:**
- Are people coming back? (Retention)
- Are people telling friends? (Virality)
- What are people complaining about most? (Priorities)
- What feature are they most excited for next? (Roadmap)
- Is the AI making discovery better or just adding complexity? (AI value)
