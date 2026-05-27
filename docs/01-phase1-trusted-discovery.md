# Phase 1 Deep Dive: Trusted Discovery + Coordination

This document is the build bible for Phase 1. Read it before every build session.

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

This is the experience you are designing toward. Every build decision should move you closer to this.

**The scenario:** It's September. Parent opens Joyful for the first time.

1. **Onboarding** (3 minutes): Enters kids' names, ages, interests. Shares a link to invite parents they know. Finds 12 parents already on Joyful.

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
Invite friends (copy link or share via messages) →
First discovery feed
```

**Key design principles:**
- Each screen should feel like less than 30 seconds of effort
- Show the value as early as possible — if they have 3+ network connections, show a personalized feed *before* they finish onboarding
- The "invite friends" step is critical — make the value exchange explicit: *"We'll show you what parents you know are recommending. We never contact anyone without your permission."*

### Flow 2: Discovery
```
Feed (curated for kids + network) →
Activity card (name, age range, endorsements, location, price) →
Activity detail (full description, all endorsements, photos, map) →
Save / Share / RSVP
```

**Feed ranking logic:**
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

**Keep rating frictionless.** A thumbs up and one optional sentence is enough. You can ask for more detail later.

### Flow 4: Coordination
```
On any activity: "Who else is going?" →
See network RSVPs →
Mark yourself as going →
Optional: suggest a date →
Notify others in network
```

---

## The Trust Graph Explained Simply

The "trust graph" is just a map of who trusts whom:
- Each parent is a dot
- Each connection between parents is a line
- You can only see recommendations that travel through YOUR lines

**For Phase 1, keep it simple: binary trust** (connected or not connected). Don't build weighted trust scores yet.

**How users build their network:**
1. **Direct invite link**: Share a personal link via iMessage/WhatsApp — most reliable
2. **School search**: Enter school name → see parent list → connect with parents you recognize
3. **Mutual connection**: "You both know [name] — would you like to connect?"

---

## Content Strategy: Building the Activity Catalog

You need activities in the catalog before discovery can deliver value. See `docs/06-building-with-claude-code.md` for the exact process to build this yourself.

**Target before first school launch:** 200 quality activities in your launch area.

### Content Categories (Priority Order)
1. **Classes + lessons**: Music, art, coding, language, cooking, STEM
2. **Sports + movement**: Soccer, gymnastics, swim, martial arts, dance
3. **Camps**: Day camps, specialty camps, holiday camps
4. **Experiences**: Museums, farms, escape rooms, nature activities
5. **Free + outdoor**: Parks, hiking trails, community events

---

## The AI Layer: What It Does

### 1. Personalized Ranking
Given what you know about a family (kids' ages, interests, location, trust network), sort the activity catalog to show the most relevant things first.

### 2. Natural Language Search
When a parent types *"Something creative for a rainy Saturday with my 5-year-old"*, the AI understands what they mean and returns relevant results — even if no activity description uses those exact words.

### 3. Weekly Digest
A personalized weekly notification: *"Here's what's happening in your Joyful community this week..."* Personalized, not generic.

### 4. Recommendation Synthesis
When multiple network members have rated the same activity, the AI synthesizes their notes: *"Parents say the instructors are patient with beginners, class sizes are small, and it's worth the price — especially for ages 6–9."*

---

## Metrics That Matter

### The One Metric That Rules Them All
**Weekly Active Families (WAF)**: Families who open the app and take at least one action (view a feed item, add a rating, share an activity, RSVP) in a given week.

### Supporting Metrics

| Metric | Why it matters | Red flag |
|---|---|---|
| Trust connections / family | Measures network density | < 3 connections after 2 weeks |
| Ratings submitted / WAF | Measures content flywheel | < 0.5 ratings/user/month |
| Discovery → RSVP rate | Measures if discovery converts | < 5% |
| Week 1 → Week 4 retention | Measures if habit is forming | < 35% |
| Invites sent / family | Measures viral growth | < 1 invite/family/month |
| NPS | Overall satisfaction | < 40 |

### What NPS > 50 Tells You
This is the signal that you've found product-market fit for Phase 1 and it's time to expand to more schools. Don't expand before you hit this number — you'll just be scaling churn.

---

## Launch Strategy: The Anchor School Approach

**Don't launch to everyone. Launch deep into 3 communities.**

- Choose 3 schools or neighborhoods in the same city
- Find a "champion parent" at each — someone well-connected who genuinely loves the product
- Offer them: free premium access, early input on product direction, recognition as founding community member
- Goal: 150–200 active families per community before expanding

**Why:** Network effects require density. A discovery app with 5 parents in your network is useless. One with 50 is magic.

---

## What You Should Do Every Week During Phase 1

- Talk to 3–5 active users. Not surveys — actual conversations.
- Review PostHog metrics every Monday. Write down what changed and your hypothesis why.
- Use the product yourself daily. Feel the friction.
- Check: are people coming back without you prompting them? That's your north star signal.
