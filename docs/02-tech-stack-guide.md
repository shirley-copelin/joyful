# Technology Guide for Non-Technical Founders

You don't need to become an engineer to make smart technology decisions. You need to understand the *shape* of the problem well enough to hire well, ask good questions, and avoid common traps.

This guide covers:
1. How to think about your tech stack
2. What the AI layer actually does
3. The recommended stack for Joyful
4. Build vs. buy decisions
5. How to evaluate engineers

---

## How to Think About Your Technology (The Right Mental Model)

Think of your application in three layers:

```
┌─────────────────────────────────────────┐
│  EXPERIENCE LAYER                       │
│  What users see and touch               │
│  → Mobile app, web app, notifications   │
├─────────────────────────────────────────┤
│  INTELLIGENCE LAYER                     │
│  What makes your product smart          │
│  → AI recommendations, personalization  │
│  → Search, ranking, insights            │
├─────────────────────────────────────────┤
│  DATA LAYER                             │
│  What you know and store                │
│  → User profiles, activities, ratings   │
│  → Trust graph, calendars, bookings     │
└─────────────────────────────────────────┘
```

Most of your early product decisions are about the **Experience Layer** (what to build and in what order) and the **Intelligence Layer** (which AI capabilities to use). The Data Layer is largely solved by existing tools.

---

## The AI Layer Explained Simply

### What "AI" Actually Means for Joyful

When people say "AI app" they often mean different things. Here's what it specifically means for Joyful:

**1. Large Language Models (LLMs) — e.g., Claude, GPT-4**
Think of these as incredibly well-read assistants that can:
- Understand what someone means when they write naturally (*"fun thing for a rainy day with my anxious 9-year-old"*)
- Generate personalized text (weekly digests, activity summaries, insight cards)
- Answer questions conversationally
- Synthesize multiple reviews into a summary

You access these via an API (a connection to an external service). You pay per use (roughly $0.003–$0.015 per 1,000 words processed).

**Recommended: Anthropic Claude** — industry-leading reasoning and safety, excellent for family-focused content.

**2. Recommendation Systems**
Algorithms that learn what each user likes and surface relevant content. Think Spotify's Discover Weekly or Netflix recommendations. In Phase 1, you can approximate this with simple rules (age filter + interest filter + network endorsement weight). By Phase 3, you'll want to invest in proper ML-based recommendations.

**3. Vector Search**
A way to search by *meaning* rather than exact words. When a parent searches "outdoor adventure for curious kids", vector search finds activities that match the meaning, even if no activity description uses those exact words. Powered by tools like Pinecone or built into Supabase.

**4. Structured Data + Rules**
Not everything needs to be "AI." Many smart features are just good data structure and clear rules:
- "Show activities within 10 miles" = a distance filter
- "Endorsed by your network" = a join on your trust graph data
- "Conflict detected" = a calendar overlap check

Don't over-AI things that can be solved simply. Save the AI for where it creates genuine value: personalization, natural language, and synthesis.

---

## Recommended Tech Stack for Joyful

This is a pragmatic stack chosen for: speed of development, ability to scale, and ability to be built by 1–2 engineers.

### Frontend (What Users See)
**React Native with Expo**
- One codebase that works on iOS, Android, and web
- Huge community, tons of tutorials, easy to hire for
- Expo makes builds and deployments dramatically simpler
- Alternative: if you decide to start web-only, use **Next.js** (faster to ship, easier to iterate)

*Non-technical translation: This is the "skin" of your app — the screens, buttons, and flows that users interact with.*

### Backend + Database (Where Data Lives)
**Supabase**
- Database (PostgreSQL — industry standard, extremely reliable)
- Authentication (login with Google, Apple, email — all handled for you)
- Real-time (so you can show "3 parents are going!" update live)
- File storage (for photos)
- Cost: free up to 500MB, then ~$25/month. Scales to millions of users.

*Non-technical translation: This is the "warehouse" where all your data is stored and organized. Supabase is essentially a full backend in a box — it saves months of infrastructure work.*

### AI / Intelligence
**Anthropic Claude API** (for LLM capabilities)
- Natural language search and understanding
- Content generation (summaries, digests, insight cards)
- Conversational features (Phase 6)
- Cost: pay-per-use. At 10,000 active families, estimate $500–$2,000/month depending on feature depth.

**Supabase pgvector** (for semantic search)
- Built into Supabase, no extra service needed
- Enables "search by meaning" for activity discovery

### Notifications
**Expo Notifications** (push notifications, free)
**Resend** (email, $20/month for up to 100K emails)

### Hosting
**Vercel** (for web/API layer)
- Free tier is generous
- Deploying a new version takes seconds

### Maps + Location
**Google Maps API**
- Activity location display, distance calculations
- Cost: ~$0 at early stage, pay-as-you-go at scale

### Analytics (Know What's Working)
**PostHog**
- Open source, privacy-friendly
- Track user flows, funnel analysis, feature flags
- Free up to 1M events/month

### Total Monthly Infrastructure Cost at Phase 1 Scale
| Service | Cost |
|---|---|
| Supabase | $25/month |
| Vercel | $20/month |
| Claude API (10K users) | $500–$1,500/month |
| Resend | $20/month |
| PostHog | $0 |
| Google Maps | ~$50/month |
| **Total** | **~$600–$1,600/month** |

This is extremely lean. You're not paying for servers, database administrators, or infrastructure engineers.

---

## Build vs. Buy Decision Matrix

Never build what you can buy. Your engineering time is your scarcest resource. Spend it only on the things that are unique to Joyful.

| Capability | Build or Buy? | Tool |
|---|---|---|
| User authentication (login) | **Buy** | Supabase Auth |
| Database | **Buy** | Supabase (PostgreSQL) |
| Push notifications | **Buy** | Expo Notifications |
| Email | **Buy** | Resend |
| Maps + directions | **Buy** | Google Maps |
| Calendar sync | **Buy** | Nylas or Cronofy (Phase 2) |
| Payments | **Buy** | Stripe |
| LLM / AI reasoning | **Buy** | Anthropic Claude API |
| AI search | **Buy** | Supabase pgvector |
| Analytics | **Buy** | PostHog |
| Trust graph logic | **Build** | Core to your product |
| Recommendation ranking | **Build** | Core to your product |
| Activity catalog + curation | **Build** | Core to your product |
| Network discovery UI | **Build** | Core to your product |
| Family profile + kid data model | **Build** | Core to your product |

---

## Data Privacy and Safety: Non-Negotiable from Day One

You are building a product that involves children's information. This is not a detail — it is central to your brand and your legal obligations.

### Legal Requirements
- **COPPA (Children's Online Privacy Protection Act)**: If you collect data from or about children under 13, you have specific legal obligations. Get a privacy attorney to review your policies before launch.
- **FERPA**: Relevant if you integrate with schools.
- **State privacy laws**: California (CPRA), Virginia (VCDPA), and others have strict requirements.

### Best Practices That Become Brand Advantages
- **No child data profiles**: Joyful profiles are *parent* profiles that reference children. Parents control what's stored. Children are never addressable users.
- **Network data is yours**: Users can export or delete all their data at any time.
- **Minimal data collection**: Collect only what you need for the feature to work. Resist the temptation to collect "in case we need it later."
- **No selling data**: Ever. State this clearly in your marketing.
- **Trust network is always private**: Your connections are never visible to non-connected users.

**The brand message**: *"Joyful knows about your family so it can serve your family — not to sell to advertisers."* This is a real differentiator against most consumer apps.

---

## How to Evaluate Engineers (Without Being Technical)

When you interview engineers, you can't test their code. But you can test their thinking.

### Questions to Ask Every Engineering Candidate

**On problem-solving:**
- *"Describe a time you had to make a technical decision with incomplete information. What did you do?"*
- *"Tell me about something you built that you're most proud of — not just technically, but in terms of user impact."*

**On your specific stack:**
- *"Have you worked with Supabase or similar backend-as-a-service tools? What do you think of that approach vs. building your own backend?"*
- *"How would you approach building a trust-graph recommendation system? What would you need to know first?"*

**On AI:**
- *"Have you worked with LLM APIs before (Claude, GPT, etc.)? What's the most interesting thing you've built with them?"*
- *"What's your philosophy on when to use AI vs. simpler algorithmic approaches?"*

**Green flags:**
- Asks clarifying questions before answering
- Gives examples from real projects
- Can explain technical concepts simply
- Has shipped something real that users used
- Is honest about what they don't know

**Red flags:**
- Only talks in jargon
- Claims expertise in everything
- Dismisses simple solutions in favor of complex ones
- Has never shipped a consumer product to real users
- Can't explain the tradeoffs of their technical choices

### The Most Important Trait
For a Stage 0/1 startup, you need engineers who can **move fast and make good decisions with uncertainty**. A senior engineer who has only worked at large companies with perfect specs and clear processes is often worse for an early startup than a mid-level engineer who has shipped 3 consumer apps from scratch.

---

## What You Should Own as the Non-Technical Founder

You don't need to code. But you should be able to:

1. **Write precise product specs**: Before your engineer builds anything, write a clear description of what the feature does, what success looks like, and what the edge cases are. Good specs save weeks of rework.

2. **Understand your data model conceptually**: Know what the core "objects" in your product are (Family, Kid, Activity, Rating, Connection, RSVP) and how they relate to each other. Draw this on a whiteboard with your engineer on Day 1.

3. **Use your metrics tools**: Learn PostHog well enough to check your own dashboards without asking an engineer.

4. **Make scope decisions quickly**: Every week, your engineer will have questions about edge cases and scope. The faster you can make clear decisions, the more they can build. Indecision is expensive.

5. **Distinguish between "broken" and "not how I imagined it"**: Bugs are urgent. UI that doesn't match your mental image is a prioritization decision, not an emergency.
