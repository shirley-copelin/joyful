# Building Joyful as a Solopreneur with Claude Code

This is your actual build guide. Not theoretical — step by step, in order, with the exact prompts and decisions you'll encounter.

The premise: You have strong product sense, Claude Code writes the code, and you manage and direct like an experienced PM working with a very fast engineer.

---

## What Claude Code Is (and Isn't)

**What it does well:**
- Writes complete, working code from a clear description
- Debugs errors when you paste them in
- Explains what code does in plain English
- Refactors and improves code you show it
- Suggests the right third-party tool for a given problem
- Catches security issues and data modeling mistakes

**What it needs from you:**
- Clear, specific descriptions of what you want to build
- Context about what already exists in the codebase
- Decisions when there are tradeoffs (it'll ask, or you'll need to redirect)
- Testing: you need to actually click through the app and confirm it works

**The mental model:** You are the product manager and QA. Claude Code is a very capable engineer who needs clear specs and honest feedback. Vague prompts produce vague code. Specific prompts produce production-ready code.

---

## Your Stack (Chosen for Solo Buildability)

Every choice here optimizes for: *can one non-engineer manage and ship this?*

| Layer | Tool | Why |
|---|---|---|
| Frontend | **Next.js** (web app) | One language (JavaScript), huge community, Claude Code knows it deeply |
| Backend + DB | **Supabase** | Database + auth + file storage in one dashboard. You can see your data visually. |
| AI | **Anthropic Claude API** | Best reasoning, great for family-safe content, pay per use |
| Hosting | **Vercel** | Deploy by pushing code. Free tier is generous. Takes 2 minutes. |
| Email | **Resend** | Dead simple email API. Free up to 3,000 emails/month. |
| Payments (Phase 2) | **Stripe** | Industry standard. Claude Code can wire it up in a day. |
| Analytics | **PostHog** | See what users do. Free up to 1M events/month. |
| Maps | **Google Maps API** | Activity locations and distance. Free at your scale. |

**What you will NOT need to manage:**
- Servers (Vercel + Supabase handle all of that)
- Databases (Supabase gives you a visual interface)
- Deployment pipelines (push code → it's live)

---

## Before You Write a Line of Code: 3 Setup Steps

### Step 1: Install Your Tools (1 hour)

1. **Install Node.js**: Go to nodejs.org, download the LTS version, install it.
2. **Install VS Code**: code.visualstudio.com — this is your code editor.
3. **Install Claude Code**: Follow the instructions at claude.ai/code. This is the CLI tool that lets you use Claude directly in your code editor.
4. **Create a GitHub account** (if you don't have one): github.com — this is where your code lives.
5. **Install Git**: git-scm.com/downloads

That's it. You're set up.

### Step 2: Create Your Accounts (30 minutes)
- **Supabase**: supabase.com — create a free account, create a new project called "joyful"
- **Vercel**: vercel.com — create a free account, connect your GitHub
- **Anthropic**: console.anthropic.com — create account, get an API key (you'll need a credit card; start with $20 of credits)
- **Resend**: resend.com — create a free account
- **PostHog**: posthog.com — create a free account

### Step 3: Initialize Your Project (30 minutes with Claude Code)

Open your terminal (on Mac: search "Terminal" in Spotlight) and type:

```bash
npx create-next-app@latest joyful-app
```

Then open Claude Code in that folder and say:

> "I'm building a Next.js app called Joyful — an AI-powered activity discovery platform for parents. I've already run create-next-app. I'm using Supabase for my database and auth, Anthropic Claude API for AI features, and Vercel for hosting. Can you help me set up the project structure and install the core dependencies I'll need?"

Claude Code will scaffold everything. Review what it creates, ask it to explain anything confusing.

---

## The Build Order (Exactly)

Build in this sequence. Do not skip ahead. Each piece depends on the previous.

### Week 1: Data Foundation
**Goal: Your database exists and you can store a family profile**

What to build:
1. Supabase database tables (families, kids, activities, ratings, connections)
2. Authentication (login with Google — parents expect this)
3. Basic family profile page (name, location, add kids)

**How to prompt Claude Code for Step 1:**
> "I need to design the Supabase database schema for Joyful. Here are the core objects:
> - **families**: parent name, email, location (city, zip), created_at
> - **kids**: name, birth_date, interests (array of tags), family_id
> - **activities**: name, description, age_min, age_max, category, address, city, zip, price_min, price_max, website, created_at
> - **ratings**: activity_id, family_id, recommended (boolean), note (text), kid_age_at_rating, created_at
> - **connections**: family_id_a, family_id_b, status (pending/accepted), created_at
> - **rsvps**: activity_id, family_id, event_date, created_at
> Can you write the SQL to create these tables in Supabase with appropriate indexes and row-level security policies so users can only see their own data?"

**What to look for:** Claude Code will write the SQL. Copy it into your Supabase dashboard (SQL editor tab) and run it. If there are errors, paste them back to Claude Code.

### Week 2: Trust Network
**Goal: A parent can invite another parent and they become "connected"**

What to build:
1. Send an invite link (generates a unique URL)
2. When someone clicks the link, they see your profile and can accept
3. Accepted connections show in a "My Network" list
4. Basic search: find other families by school name

**How to prompt Claude Code:**
> "I need to build an invite system. When a parent clicks 'Invite a Parent', the app should:
> 1. Generate a unique invite link (e.g., joyful.app/invite/[unique-code])
> 2. Let them share it via copy-to-clipboard or via a share sheet on mobile
> 3. When the invited parent clicks the link and logs in (or signs up), they should see the inviting parent's profile with a 'Connect' button
> 4. When they click Connect, create a connection record in Supabase with status 'accepted'
> 5. Both parents should now see each other in their 'My Network' list
> My Supabase tables are already set up. Here's the connections table schema: [paste your schema]"

### Week 3: Activity Catalog + Discovery Feed
**Goal: Parents can browse activities. Activities endorsed by their network show prominently.**

What to build:
1. Activity card component (shows name, age range, price, # endorsements from your network)
2. Discovery feed: activities sorted by network endorsements + age match
3. Activity detail page
4. Filters: age, category, distance, endorsed by network

**Key prompt for the feed ranking logic:**
> "I need to build an activity discovery feed. Here's how to rank activities for a given family:
> 1. First: activities that at least one of their connections has rated 'recommended' (show endorsement count)
> 2. Second: activities that match the age range of any of their kids
> 3. Third: activities in their city/zip
> 4. Deprioritize: activities with no endorsements and no age match
> The feed should also show, on each card, the names of connections who endorsed it (e.g., 'Jamie and 2 others you know recommend this').
> Please write the Supabase query (using their JavaScript client) to fetch a ranked feed for a given family_id."

### Week 4: Rating Flow
**Goal: After using an activity, a parent can rate it and add a note**

What to build:
1. "Add a recommendation" button on any activity
2. Simple form: thumbs up/down + optional note (2-3 sentences max) + which kid + kid's age
3. Confirmation + share to network option
4. Activity cards update in real-time to show new endorsements

### Week 5: Coordination (Who Else Is Going?)
**Goal: Parents can RSVP to an activity and see network RSVPs**

What to build:
1. On each activity: "Mark as Going" button (with optional date)
2. "X families from your network are going" display
3. Tapping shows which families, with a message button
4. Simple in-app notification when a connected family RSVPs to something you've saved

### Week 6: AI Discovery (Natural Language Search)
**Goal: A parent can describe what they want and get relevant results**

What to build:
1. Search bar at the top of discovery feed
2. Natural language queries: "creative Saturday class for my 7-year-old"
3. AI processes the query, extracts filters, returns ranked results
4. "Why this?" explanation: brief AI-generated note on why each result matched

**How to prompt Claude Code for the AI integration:**
> "I need to integrate the Anthropic Claude API for natural language activity search. When a parent types a search query like 'creative class for my anxious 8-year-old on weekends', I want to:
> 1. Send the query to Claude with context about this parent's kids (ages, interests) and their location
> 2. Ask Claude to extract structured filters: age_range, category, price_preference, schedule, any special notes
> 3. Use those filters to query the Supabase activities table
> 4. Return results with a short AI-generated explanation of why each result matches
> Please write the API route handler in Next.js and the Supabase query. My Anthropic API key is in .env.local as ANTHROPIC_API_KEY."

### Week 7: Polish + Onboarding
**Goal: A new user can go from signup to first meaningful discovery in under 3 minutes**

What to build:
1. Onboarding flow: welcome → add kids → find your network → first discovery
2. Empty state design (what a new user sees with no network yet)
3. Mobile responsiveness (test on your phone constantly)
4. Loading states and error handling

### Week 8: Soft Launch Prep
**Goal: It's good enough to share with your first 20 families**

What to build:
1. Seed your activity catalog (use Claude Code to help scrape and format local activities)
2. Set up PostHog tracking on key events (signup, invite sent, activity rated, RSVP)
3. Set up Resend for transactional email (invite notifications, weekly digest)
4. Bug fixes from your own testing
5. Deploy to Vercel with a real domain

---

## How to Write Good Prompts for Claude Code

This is the skill that will determine how fast you move.

### The Anatomy of a Good Prompt

```
[What I'm building]: A specific feature or component
[Context]: What already exists that's relevant
[Exact behavior]: Step-by-step what should happen
[Data]: The relevant database schema or data shapes
[Constraints]: What NOT to do, or things to be careful about
[Output format]: "Write a Next.js API route" or "Write a React component"
```

### Examples: Vague vs. Specific

**Too vague:**
> "Build me the discovery feed"

**Specific and effective:**
> "Build a React component called ActivityFeed that:
> 1. Fetches activities from Supabase ordered by: (a) number of connections who endorsed it, then (b) age match with the logged-in user's kids
> 2. Renders ActivityCard components in a vertical scroll list
> 3. Shows a loading skeleton while fetching
> 4. Shows an empty state with copy 'Connect with more parents to see their recommendations' if the user has < 3 network connections
> 5. Has a filter bar at the top with: All, Classes, Sports, Experiences, Free
> The logged-in user's family data (including their kids and connections) is available from a useFamily() hook that I've already written. Here's its return shape: [paste it]"

### When You're Stuck

If something isn't working:
1. **Paste the error message** exactly as it appears into Claude Code
2. **Add context**: "This error happens when I click the Connect button"
3. **Share the relevant file**: "Here's the component where it's happening: [paste code]"

Claude Code will diagnose and fix it. Don't try to guess what's wrong yourself — just describe the symptom precisely.

---

## The Solopreneur Operating Rhythm

Without a team, your biggest risk is losing momentum or going in circles. This rhythm prevents that.

### Daily (30 minutes)
- Morning: What's the one thing I'm building today? Write it down specifically.
- Evening: Did it work? If not, what exactly is broken?

### Weekly (1 hour)
- Monday: Review your PostHog metrics. What did users actually do last week?
- Wednesday: Talk to 2-3 users from your test community. What are they confused by? What do they love?
- Friday: What shipped this week? What's the plan for next week?

### The Rule: Ship Something Every Week
Every Friday, something new should be live that wasn't live the previous Friday. It can be small — a new filter, a better empty state, a new activity in the catalog. Momentum is a force multiplier.

---

## Activity Catalog Without a Team

You need activities in the catalog before discovery works. Here's how to do it alone.

### The Claude Code + Google Sheets Approach

1. **Create a Google Sheet** with columns: name, description, address, city, zip, age_min, age_max, category, price_min, price_max, website
2. **Research manually** for 2-3 hours: Google "kids classes [your city]", look at local parenting blogs, check Yelp
3. **Paste raw data into Claude Code** and say: *"Here's a list of activity providers I found. Can you help me format this into my database schema and write an age-appropriate description for each? Here are 20 to start: [paste]"*
4. **Import the CSV** into Supabase using their table editor
5. Repeat until you have 200+ activities in your launch area

Target: 200 activities for City 1 before inviting your first school.

---

## When to Know It's Working

Before expanding to a second school, you need to see:

- [ ] Users are coming back without you texting them
- [ ] At least 5 families have rated an activity unprompted
- [ ] At least 3 families have invited someone from within the app
- [ ] When you talk to users, they say something like "I already told my friend about this"
- [ ] NPS is above 40 (ask: "How likely are you to recommend Joyful to another parent? 0-10")

If you're not seeing these signals after 6-8 weeks with your first community, don't expand — go deeper. Talk to more users. Fix the thing that's creating friction.

---

## Costs as a Solopreneur

This is what you'll actually pay per month at Phase 1 scale:

| Item | Monthly Cost |
|---|---|
| Supabase (free tier covers you until ~500 users) | $0 → $25 |
| Vercel (free tier generous) | $0 → $20 |
| Anthropic Claude API (light usage, 500 families) | $50-150 |
| Resend (email) | $0 (free tier) |
| PostHog | $0 (free tier) |
| Domain name | $15/year |
| Google Maps API | $0-10 |
| **Total at 500 families** | **~$75-200/month** |

You can run a real product with 500 active families for under $200/month. That's the magic of the current tooling.
