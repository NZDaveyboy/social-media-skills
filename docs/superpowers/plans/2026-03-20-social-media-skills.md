# Social Media Skills Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 14-skill Claude Code plugin for social media content strategy, creation, and analysis across text-first platforms (LinkedIn, Twitter/X, Threads, Bluesky).

**Architecture:** Skills organized in `skills/<name>/SKILL.md` with YAML frontmatter. A foundational `social-media-context` skill stores user identity, voice, and goals in `.agents/social-media-context.md`. Strategy, creation, and analysis skills reference it. BlackTwist MCP integration when available, advisory fallback otherwise.

**Tech Stack:** Markdown skills with YAML frontmatter, Bash validation script, JSON plugin manifest.

**Spec:** `docs/superpowers/specs/2026-03-20-social-media-skills-design.md`

---

## File Map

### Root files
- Create: `CLAUDE.md` — Agent guidelines, repo overview, skill categories, conventions
- Create: `AGENTS.md` — Agent Skills spec, validation requirements, git workflow
- Create: `README.md` — Human-readable docs, installation, skill catalog
- Create: `LICENSE` — MIT license
- Create: `.gitignore` — Standard ignores (.env, .DS_Store, node_modules, etc.)
- Create: `.claude-plugin/marketplace.json` — Plugin manifest with all 14 skills
- Create: `validate-skills.sh` — Skill validation script
- Create: `tools/REGISTRY.md` — Tool integrations (BlackTwist, scheduling tools)

### Foundation layer
- Create: `skills/social-media-context/SKILL.md`
- Create: `skills/social-media-context/evals/.gitkeep`

### Strategy layer
- Create: `skills/content-strategy/SKILL.md`
- Create: `skills/content-strategy/evals/.gitkeep`
- Create: `skills/content-calendar/SKILL.md`
- Create: `skills/content-calendar/evals/.gitkeep`
- Create: `skills/platform-strategy/SKILL.md`
- Create: `skills/platform-strategy/evals/.gitkeep`

### Creation layer
- Create: `skills/post-writer/SKILL.md`
- Create: `skills/post-writer/evals/.gitkeep`
- Create: `skills/thread-writer/SKILL.md`
- Create: `skills/thread-writer/evals/.gitkeep`
- Create: `skills/carousel-writer/SKILL.md`
- Create: `skills/carousel-writer/evals/.gitkeep`
- Create: `skills/content-repurposer/SKILL.md`
- Create: `skills/content-repurposer/evals/.gitkeep`
- Create: `skills/hook-writer/SKILL.md`
- Create: `skills/hook-writer/evals/.gitkeep`

### Analysis layer
- Create: `skills/performance-analyzer/SKILL.md`
- Create: `skills/performance-analyzer/evals/.gitkeep`
- Create: `skills/audience-growth-tracker/SKILL.md`
- Create: `skills/audience-growth-tracker/evals/.gitkeep`
- Create: `skills/content-pattern-analyzer/SKILL.md`
- Create: `skills/content-pattern-analyzer/evals/.gitkeep`
- Create: `skills/optimization-advisor/SKILL.md`
- Create: `skills/optimization-advisor/evals/.gitkeep`

---

### Task 1: Repo Scaffolding

**Files:**
- Create: `CLAUDE.md`
- Create: `AGENTS.md`
- Create: `README.md`
- Create: `LICENSE`
- Create: `.gitignore`
- Create: `.claude-plugin/marketplace.json`
- Create: `validate-skills.sh`
- Create: `tools/REGISTRY.md`

- [ ] **Step 1: Create `.gitignore`**

```
node_modules/
.env
.env.*
!.env.example
.DS_Store
*.swp
.idea/
.vscode/
```

- [ ] **Step 2: Create `LICENSE`**

MIT license, copyright 2026.

- [ ] **Step 3: Create `CLAUDE.md`**

Agent guidelines document. Must cover:
- Repository overview: "Social media skills for AI agents — 14 skills across strategy, creation, and analysis for text-first platforms"
- Skill organization by layer (foundation, strategy, creation, analysis) with skill names
- Key conventions: YAML frontmatter (name, description, metadata.version), kebab-case naming, max 500 lines per SKILL.md
- Foundation dependency: all skills check for `.agents/social-media-context.md` first
- BlackTwist integration: use when available, advisory fallback when not
- Cross-references: skills should reference related skills
- Writing style: active voice, clarity over cleverness, bold for key terms

Follow the structure and tone of the reference repo's CLAUDE.md.

- [ ] **Step 4: Create `AGENTS.md`**

Agent Skills specification. Must cover:
- Repository structure overview
- Skill requirements: YAML frontmatter with `name` (1-64 chars, kebab-case), `description` (1-1024 chars), `metadata.version`
- Naming conventions: lowercase, alphanumeric, hyphens only
- File size: under 500 lines per SKILL.md
- Git workflow: conventional commits

Follow the reference repo's AGENTS.md structure.

- [ ] **Step 5: Create `README.md`**

Human-readable documentation:
- Title: "Social Media Skills"
- One-line description
- Skill catalog organized by layer with descriptions
- Installation instructions (claude plugin add, git submodule, git clone)
- Supported platforms list
- Tool integrations section (BlackTwist)
- License

- [ ] **Step 6: Create `.claude-plugin/marketplace.json`**

```json
{
  "name": "social-media-skills",
  "owner": "threads-power-tool",
  "version": "1.0.0",
  "description": "Social media skills for AI agents — content strategy, creation, and analysis for LinkedIn, Twitter/X, Threads, and Bluesky",
  "skills": [
    "social-media-context",
    "content-strategy",
    "content-calendar",
    "platform-strategy",
    "post-writer",
    "thread-writer",
    "carousel-writer",
    "content-repurposer",
    "hook-writer",
    "performance-analyzer",
    "audience-growth-tracker",
    "content-pattern-analyzer",
    "optimization-advisor"
  ],
  "strict": false
}
```

Note: `strict: false` means the plugin allows flexible skill invocation — skills can be triggered even when the match is approximate, rather than requiring exact name matches.

- [ ] **Step 7: Create `validate-skills.sh`**

Bash script that validates all skills in `skills/` against conventions:
- Check YAML frontmatter exists with `name` and `description`
- Validate name is kebab-case, 1-64 chars
- Validate description is 1-1024 chars
- Check file is under 500 lines
- Color-coded output (✓ pass, ⚠️ warning, ❌ fail)

Use the reference repo's `validate-skills.sh` as the template.

- [ ] **Step 8: Create `tools/REGISTRY.md`**

Tool integrations registry focused on social media:
- **BlackTwist** (primary): MCP server for posting, scheduling, analytics. List all available tools: create_post, edit_post, edit_thread, get_thread, delete_thread, list_posts, list_drafts, get_post_analytics, get_live_metrics, get_metric_timeseries, get_follower_growth, get_consistency, get_daily_recap, list_time_slots, reschedule_thread, get_recommendations, get_thread_follow_up, set_thread_follow_up, get_user_settings, list_teams, get_subscription, list_providers
- **Buffer / Hootsuite / Later** — third-party scheduling tools (reference only)
- **Platform native analytics** — where to find data manually when no API is connected

- [ ] **Step 9: Commit**

```bash
git add .gitignore LICENSE CLAUDE.md AGENTS.md README.md .claude-plugin/marketplace.json validate-skills.sh tools/REGISTRY.md
git commit -m "feat: add repo scaffolding — root files, plugin manifest, validation script, tools registry"
```

---

### Task 2: Foundation — `social-media-context`

**Files:**
- Create: `skills/social-media-context/SKILL.md`
- Create: `skills/social-media-context/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/social-media-context/evals
touch skills/social-media-context/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/social-media-context/SKILL.md`**

This is the foundational skill. All other skills reference it. Follow the `product-marketing-context` pattern from the reference repo.

**Frontmatter:**
```yaml
---
name: social-media-context
description: "When the user wants to set up or update their social media profile, voice, audience, content pillars, or platform preferences. Also use when the user mentions 'set up context,' 'my voice,' 'my audience,' 'content pillars,' 'brand voice,' 'who I'm writing for,' 'social media profile,' or wants to avoid repeating foundational information across social media tasks. Use this at the start of any new project before using other social media skills — it creates .agents/social-media-context.md that all other skills reference."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Purpose**: Establish a persistent context file (`.agents/social-media-context.md`) that prevents repeating foundational info across tasks
2. **Two setup paths**:
   - **Quick setup**: User provides key info directly, agent drafts the context file
   - **Conversational walkthrough**: Agent asks questions one at a time to build the profile
3. **Core sections to capture** (8 sections — 6 from spec + 2 additions marked with *):
   - **Identity**: Creator vs. brand, name, role, industry/niche
   - **Target audience**: Who they are, demographics, pain points, what they care about, where they hang out online
   - **Voice & tone**: 3-5 adjectives describing their voice, example phrases they'd use, phrases/tones to avoid, formality level
   - **Content pillars**: 3-5 topics they own, with a one-line description of their angle on each
   - **Platform config**: Which platforms (LinkedIn, Twitter/X, Threads, Bluesky), goals per platform, current posting frequency, target frequency
   - ***Content formats** (addition): Which formats they use (posts, threads, carousels, etc.), preferred formats per platform — needed by creation skills to know what to produce
   - **Example posts**: 3-5 real posts that represent their best work, for style matching
   - ***Anti-patterns** (addition): Topics to avoid, tones that don't fit, types of content they won't create — needed by creation skills to respect boundaries
4. **Output format**: Save to `.agents/social-media-context.md` with clear section headers
5. **Update flow**: When the file already exists, read it and ask what to update rather than starting from scratch

**Related skills**: content-strategy, platform-strategy, post-writer

Max 500 lines.

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `social-media-context` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/social-media-context/
git commit -m "feat: add social-media-context foundational skill"
```

---

### Task 3: Strategy Layer — `content-strategy`

> **Note:** This skill references `platform-strategy` (Task 4), but cross-references between skills are soft dependencies — they just name related skills the user can invoke separately. No skill imports or calls another. Tasks 3-5 can be built in any order.

**Files:**
- Create: `skills/content-strategy/SKILL.md`
- Create: `skills/content-strategy/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/content-strategy/evals
touch skills/content-strategy/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/content-strategy/SKILL.md`**

**Frontmatter:**
```yaml
---
name: content-strategy
description: "When the user wants to plan a social media content strategy, decide what to post, or figure out topic clusters and content mix. Also use when the user mentions 'content strategy,' 'what should I post,' 'content ideas,' 'topic clusters,' 'content pillars,' 'content planning,' 'content mix,' 'I don't know what to post,' or 'social media strategy.' Use this to define the what and why of posting. For writing actual posts, see post-writer. For scheduling, see content-calendar. For platform-specific tactics, see platform-strategy."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` if it exists. If not, prompt user to run `social-media-context` first.
2. **Discovery questions** (only ask what's not already in context):
   - Business goals for social media
   - Current content performance (what works, what doesn't)
   - Competitors or creators they admire
   - Time/resource constraints
3. **Content pillar development**:
   - Map 3-5 pillars from user's context
   - For each pillar: unique angle, subtopics, content types that fit
   - Pillar balance ratios (e.g., 30% educational, 25% storytelling, etc.)
4. **Topic cluster framework**:
   - Cluster topics around each pillar
   - Identify cornerstone topics vs. supporting topics
   - Map topics to content formats
5. **Content mix ratios**:
   - Educational / Storytelling / Promotional / Engagement / Personal
   - Platform-specific adjustments
6. **Differentiation analysis**:
   - What makes this voice unique
   - Content gaps in the user's niche
   - Underserved topics or angles
7. **Output**: A structured content strategy document the user can reference

**Related skills**: social-media-context, platform-strategy, content-calendar

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

- [ ] **Step 4: Commit**

```bash
git add skills/content-strategy/
git commit -m "feat: add content-strategy skill"
```

---

### Task 4: Strategy Layer — `platform-strategy`

**Files:**
- Create: `skills/platform-strategy/SKILL.md`
- Create: `skills/platform-strategy/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/platform-strategy/evals
touch skills/platform-strategy/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/platform-strategy/SKILL.md`**

**Frontmatter:**
```yaml
---
name: platform-strategy
description: "When the user wants platform-specific tactical guidance for LinkedIn, Twitter/X, Threads, or Bluesky. Also use when the user mentions 'LinkedIn strategy,' 'Twitter strategy,' 'Threads strategy,' 'Bluesky strategy,' 'algorithm,' 'what works on LinkedIn,' 'cross-posting,' 'platform differences,' 'adapt my content,' or 'which platform should I focus on.' For overall content strategy, see content-strategy. For writing posts, see post-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` first
2. **Platform-by-platform tactical guide**:
   - **LinkedIn**: Algorithm signals, optimal post length (1200-1500 chars for feed posts), formatting (line breaks, no links in body), best content types (carousels, personal stories, industry takes), posting times, hashtag strategy (3-5 relevant), engagement patterns
   - **Twitter/X**: Algorithm signals, thread vs single tweet strategy, optimal lengths, quote tweets vs replies, hashtag usage (minimal), engagement windows, community building tactics
   - **Threads**: Platform culture (conversational, less polished), cross-posting from Twitter considerations, engagement patterns, hashtag behavior, discovery mechanics
   - **Bluesky**: Decentralized platform nuances, custom feeds, starter packs, community dynamics, content discoverability, tone (early-adopter tech-savvy audience)
3. **Cross-posting guidance**:
   - What to cross-post vs. what to make native
   - Adaptation checklist per platform (length, formatting, tone, CTAs)
   - Common cross-posting mistakes
4. **Platform selection framework**:
   - How to choose which platforms to focus on based on goals and audience
   - When to add a new platform vs. double down
5. **Tone adaptation**: Same voice, different register per platform

**Related skills**: social-media-context, content-strategy, post-writer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `platform-strategy` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/platform-strategy/
git commit -m "feat: add platform-strategy skill"
```

---

### Task 5: Strategy Layer — `content-calendar`

**Files:**
- Create: `skills/content-calendar/SKILL.md`
- Create: `skills/content-calendar/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/content-calendar/evals
touch skills/content-calendar/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/content-calendar/SKILL.md`**

**Frontmatter:**
```yaml
---
name: content-calendar
description: "When the user wants to plan a posting schedule, create a content calendar, or organize when and what to post. Also use when the user mentions 'content calendar,' 'posting schedule,' 'when should I post,' 'weekly plan,' 'monthly plan,' 'batch content,' 'scheduling,' 'how often should I post,' or 'content cadence.' For deciding what topics to cover, see content-strategy. For writing the actual posts, see post-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` and any existing content strategy
2. **Calendar inputs**:
   - Platforms and target frequency per platform (from context)
   - Content pillars and mix ratios (from content-strategy or user input)
   - Time available for content creation
   - Key dates, events, or launches relevant to niche
3. **Calendar generation**:
   - Weekly or monthly view (user's choice)
   - Each entry: day, platform, content pillar, topic/angle, format (post/thread/carousel)
   - Ensure pillar balance across the period
   - No platform gets neglected
4. **Batching strategy**:
   - How to batch-create content efficiently
   - Suggested batching sessions (e.g., "2 hours Monday: write all LinkedIn posts for the week")
   - Batch by platform vs. batch by pillar
5. **Scheduling with BlackTwist**:
   - When BlackTwist MCP is available: use `list_time_slots` to find optimal slots, schedule via `create_post`
   - When not available: output calendar in markdown table format for manual scheduling
6. **Flexibility buffer**: Leave 20-30% of slots open for timely/reactive content
7. **Review cadence**: Weekly review to adjust based on performance

**Related skills**: content-strategy, social-media-context, post-writer, platform-strategy

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `content-calendar` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/content-calendar/
git commit -m "feat: add content-calendar skill"
```

---

### Task 6: Creation Layer — `hook-writer`

**Files:**
- Create: `skills/hook-writer/SKILL.md`
- Create: `skills/hook-writer/evals/.gitkeep`

This is built before other creation skills because `post-writer`, `thread-writer`, and `carousel-writer` all reference it.

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/hook-writer/evals
touch skills/hook-writer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/hook-writer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: hook-writer
description: "When the user wants help writing opening lines, hooks, or first sentences that grab attention. Also use when the user mentions 'hook,' 'opening line,' 'first line,' 'scroll stopper,' 'attention grabber,' 'headline,' 'how to start my post,' or 'nobody reads past my first line.' Can be used standalone or invoked by other creation skills. For writing full posts, see post-writer. For threads, see thread-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` for voice and platform preferences
2. **Hook pattern library** (7-10 patterns with examples for each):
   - **Contrarian**: Challenge conventional wisdom. "Stop [common advice]. It's killing your [metric]."
   - **Question**: Provoke curiosity. "What if everything you know about [topic] is wrong?"
   - **Story opener**: Pull into a narrative. "Last Tuesday, I [unexpected event]."
   - **Statistic/Data**: Lead with a number. "[Surprising number]% of [group] do [thing]. Here's why."
   - **List preview**: Promise structured value. "[N] things I wish I knew about [topic] before [milestone]:"
   - **Bold claim**: Make a strong statement. "[Common thing] is dead. Here's what's replacing it."
   - **Empathy**: Connect with a pain point. "If you're struggling with [common pain], this is for you."
   - **Before/After**: Show transformation. "I went from [bad state] to [good state] in [time]. Here's the exact process:"
   - **Confession**: Vulnerability that builds trust. "I've been lying to you about [topic]."
3. **Platform-specific hooks**:
   - LinkedIn: Professional tone, can be longer (2-3 lines), personal stories work well
   - Twitter/X: Punchy, under 280 chars ideally in one line, curiosity-driven
   - Threads: Conversational, casual, relatable
   - Bluesky: Authentic, anti-corporate, clever
4. **Hook generation process**:
   - User provides topic or idea
   - Generate 5-7 hook variants across different patterns
   - Adapt each to the target platform
   - Mark the recommended top pick with reasoning
5. **Hook testing tips**: How to evaluate which hooks perform best

**Related skills**: social-media-context, platform-strategy, post-writer, thread-writer, carousel-writer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `hook-writer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/hook-writer/
git commit -m "feat: add hook-writer skill"
```

---

### Task 7: Creation Layer — `post-writer`

**Files:**
- Create: `skills/post-writer/SKILL.md`
- Create: `skills/post-writer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/post-writer/evals
touch skills/post-writer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/post-writer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: post-writer
description: "When the user wants to write a social media post for LinkedIn, Twitter/X, Threads, or Bluesky. Also use when the user mentions 'write a post,' 'draft a post,' 'LinkedIn post,' 'tweet,' 'Threads post,' 'Bluesky post,' 'social media post,' 'help me write,' or shares a topic and wants it turned into a post. For multi-part content, see thread-writer. For carousels, see carousel-writer. For opening lines specifically, see hook-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` for voice, pillars, platform preferences. If not found, prompt user to run `social-media-context`.
2. **Input gathering** (only ask what's not provided):
   - Topic or idea (or rough draft to refine)
   - Target platform(s)
   - Content type: educational, storytelling, promotional, engagement, personal
   - Any specific angle or CTA
3. **Post structure by platform**:
   - **LinkedIn**: Hook (1-2 lines) → Body with line breaks every 1-2 sentences → CTA. 1200-1500 chars optimal. No links in body (comment instead). 3-5 hashtags at end.
   - **Twitter/X**: Hook → Core message → CTA. Under 280 chars for single tweets. Minimal hashtags (0-2).
   - **Threads**: Conversational tone, can be longer, less structured than LinkedIn. No hashtag culture yet.
   - **Bluesky**: Concise, authentic, 300 char limit. Clever > corporate.
4. **Writing process**:
   - Generate hook options (reference hook-writer patterns)
   - Draft post body maintaining user's voice
   - Add appropriate CTA
   - Format for target platform
   - Generate 2-3 variants if requested
5. **Voice matching**: Use example posts from context to match tone, vocabulary, sentence structure
6. **Publishing with BlackTwist**: When available, offer to schedule/publish via `create_post`. When not, output the post as formatted text.
7. **Post checklist**: Quick pre-publish checklist (hook strong? voice consistent? CTA clear? platform-appropriate length?)

**Related skills**: social-media-context, hook-writer, platform-strategy, content-repurposer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `post-writer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/post-writer/
git commit -m "feat: add post-writer skill"
```

---

### Task 8: Creation Layer — `thread-writer`

**Files:**
- Create: `skills/thread-writer/SKILL.md`
- Create: `skills/thread-writer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/thread-writer/evals
touch skills/thread-writer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/thread-writer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: thread-writer
description: "When the user wants to write a multi-part thread for Twitter/X, LinkedIn, or other platforms. Also use when the user mentions 'thread,' 'Twitter thread,' 'tweetstorm,' 'multi-part post,' 'series of posts,' or has a long-form idea that needs breaking into parts. For single posts, see post-writer. For carousels, see carousel-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md`
2. **Input gathering**:
   - Topic, key points, or source material
   - Target platform
   - Thread length preference (short 3-5, medium 7-10, long 10+)
   - Goal: educate, tell a story, share a framework, document a journey
3. **Thread architecture**:
   - **Post 1 (Hook)**: Must stand alone and compel clicks. Use hook-writer patterns. Include "🧵" or "Thread:" signal if on Twitter/X.
   - **Body posts**: One idea per post. Each post should make sense on its own but build on the previous. Use transitions ("Here's the thing:", "But that's not all:", "The real insight:").
   - **Final post (Closer)**: Summarize key takeaway, strong CTA (follow, repost, bookmark, reply), optional self-plug.
4. **Thread formats**:
   - **Listicle**: "[N] things about [topic]" — one item per post
   - **Story arc**: Setup → Conflict → Resolution → Lesson
   - **Framework**: Present a step-by-step process
   - **Breakdown**: Analyze a case study or example
   - **Contrarian**: Challenge common belief with evidence
5. **Platform-specific threading**:
   - Twitter/X: 280 chars per post, number posts (1/, 2/), self-reply chain
   - LinkedIn: Longer posts in series, can link between them
   - Threads: More conversational, no strict length limit
6. **Pacing tips**: Vary post length, use short punchy posts between longer ones, end posts on curiosity hooks
7. **Publishing**: Offer BlackTwist scheduling when available

**Related skills**: social-media-context, hook-writer, platform-strategy, post-writer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `thread-writer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/thread-writer/
git commit -m "feat: add thread-writer skill"
```

---

### Task 9: Creation Layer — `carousel-writer`

**Files:**
- Create: `skills/carousel-writer/SKILL.md`
- Create: `skills/carousel-writer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/carousel-writer/evals
touch skills/carousel-writer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/carousel-writer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: carousel-writer
description: "When the user wants to write content for a LinkedIn carousel, slide deck, or swipeable multi-slide format. Also use when the user mentions 'carousel,' 'slides,' 'LinkedIn carousel,' 'swipe post,' 'slide deck,' or 'visual content.' Outputs slide-by-slide text content (not visual design). For single posts, see post-writer. For threads, see thread-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md`
2. **Input gathering**:
   - Topic or key message
   - Target slide count (recommend 7-12 for LinkedIn)
   - Goal: educate, framework, tips, story, data
3. **Carousel structure**:
   - **Slide 1 (Cover)**: Bold headline hook, subtitle with promise, clean and scannable
   - **Slide 2 (Context)**: Set the problem or frame the topic
   - **Slides 3-N (Body)**: One point per slide, minimal text (max 30 words), use bold headers + supporting text
   - **Final slide (CTA)**: Summary of key takeaway, follow/save/share CTA, optional author info
4. **Carousel formats**:
   - **Listicle**: "[N] tips/mistakes/lessons" — one per slide
   - **Framework**: Step-by-step process, numbered slides
   - **Before/After**: Contrast slides showing wrong vs. right
   - **Data storytelling**: Stat per slide with insight
   - **Mini case study**: Problem → Approach → Result → Lesson
5. **Writing guidelines**:
   - Headlines do the heavy lifting (people skim)
   - Max 30 words per slide body
   - Use formatting cues: "→" for emphasis, numbered lists, bold key phrases
   - Each slide should make the reader swipe to the next
   - End slides on mini-cliffhangers or curiosity gaps
6. **Output format**: Numbered slide-by-slide text content, clearly marked

**Related skills**: social-media-context, hook-writer, content-repurposer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `carousel-writer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/carousel-writer/
git commit -m "feat: add carousel-writer skill"
```

---

### Task 10: Creation Layer — `content-repurposer`

**Files:**
- Create: `skills/content-repurposer/SKILL.md`
- Create: `skills/content-repurposer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/content-repurposer/evals
touch skills/content-repurposer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/content-repurposer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: content-repurposer
description: "When the user wants to turn one piece of content into multiple formats or adapt content across platforms. Also use when the user mentions 'repurpose,' 'turn this into,' 'adapt this for,' 'cross-post,' 'reformat,' 'blog to social,' 'newsletter to posts,' or 'get more from this content.' For writing original posts, see post-writer. For threads, see thread-writer. For carousels, see carousel-writer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` for platforms and voice
2. **Input**:
   - Source content (blog post, newsletter, podcast notes, video transcript, existing social post)
   - Target platforms and formats
   - Or: let the skill suggest the highest-leverage derivatives
3. **Repurposing matrix**:
   - Blog post → LinkedIn post (key insight), Twitter/X thread (key takeaways), carousel (framework/tips), Threads post (casual take), multiple standalone posts (one per insight)
   - Newsletter → Thread (curated highlights), single post (best insight), carousel (if framework-heavy)
   - Podcast/video transcript → Quote posts, thread of key moments, carousel of insights
   - Existing social post → Adapt for other platforms, expand into thread, compress into shorter format
4. **Repurposing process**:
   - Extract key insights from source (3-7 per piece)
   - Rank by standalone value
   - Match insights to best format per platform
   - Draft each derivative maintaining user's voice
   - Adapt tone/length/formatting per platform conventions
5. **Leverage ranking**: Suggest which derivatives will get the most reach relative to effort
6. **Scheduling**: When BlackTwist available, spread derivatives across the week. When not, output a suggested posting schedule.
7. **Anti-patterns**: Don't just copy-paste across platforms. Each derivative should feel native.

**Related skills**: social-media-context, platform-strategy, post-writer, thread-writer, carousel-writer

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `content-repurposer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/content-repurposer/
git commit -m "feat: add content-repurposer skill"
```

---

### Task 11: Analysis Layer — `performance-analyzer`

> **Note:** `performance-analyzer` and `content-pattern-analyzer` (Task 13) cross-reference each other. This is intentional — both can operate independently. The cross-references indicate that their outputs complement each other, not that one requires the other to function. Same soft-dependency principle as the strategy layer.

**Files:**
- Create: `skills/performance-analyzer/SKILL.md`
- Create: `skills/performance-analyzer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/performance-analyzer/evals
touch skills/performance-analyzer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/performance-analyzer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: performance-analyzer
description: "When the user wants to analyze how their social media posts are performing. Also use when the user mentions 'analytics,' 'performance,' 'how did my posts do,' 'engagement,' 'impressions,' 'what's working,' 'post metrics,' 'my best posts,' or 'why isn't this post performing.' Uses BlackTwist analytics when available, works from user-provided data otherwise. For audience growth specifically, see audience-growth-tracker. For pattern detection, see content-pattern-analyzer. For actionable next steps, see optimization-advisor."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md`
2. **Data collection**:
   - **With BlackTwist**: Use `get_post_analytics`, `get_live_metrics`, `list_posts` to pull data automatically. Use `get_metric_timeseries` for trends over time.
   - **Without BlackTwist**: Ask user to provide metrics (screenshot, CSV, or manual input). Provide a template for what data to collect.
3. **Metrics framework**:
   - **Reach**: Impressions, reach, profile visits
   - **Engagement**: Likes, comments, reposts, saves, engagement rate (engagements / impressions)
   - **Conversion**: Link clicks, DMs, follows from post
4. **Analysis outputs**:
   - **Top performers**: Top 3-5 posts by engagement rate with analysis of why they worked (topic, format, hook, timing)
   - **Bottom performers**: Bottom 3-5 posts with diagnosis
   - **Trend analysis**: Engagement trending up/down/flat? Impressions growing?
   - **Actionable insights**: 3-5 specific suggestions based on the data
5. **Benchmarking**: Compare against user's own averages (not vanity benchmarks)
6. **Reporting format**: Structured summary with sections, not a wall of numbers
7. **With BlackTwist**: Also incorporate `get_daily_recap`, `get_consistency` for habit tracking insights

**Related skills**: social-media-context, content-pattern-analyzer, optimization-advisor

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `performance-analyzer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/performance-analyzer/
git commit -m "feat: add performance-analyzer skill"
```

---

### Task 12: Analysis Layer — `audience-growth-tracker`

**Files:**
- Create: `skills/audience-growth-tracker/SKILL.md`
- Create: `skills/audience-growth-tracker/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/audience-growth-tracker/evals
touch skills/audience-growth-tracker/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/audience-growth-tracker/SKILL.md`**

**Frontmatter:**
```yaml
---
name: audience-growth-tracker
description: "When the user wants to track follower growth, understand what drives new followers, or analyze audience development. Also use when the user mentions 'follower growth,' 'followers,' 'audience growth,' 'gaining followers,' 'losing followers,' 'who follows me,' or 'grow my audience.' Uses BlackTwist follower data when available. For post-level metrics, see performance-analyzer. For content patterns, see content-pattern-analyzer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md`
2. **Data collection**:
   - **With BlackTwist**: Use `get_follower_growth` for growth data, `get_metric_timeseries` for trends
   - **Without BlackTwist**: Ask user for follower counts over time (weekly snapshots), or platform analytics screenshots
3. **Growth analysis**:
   - Net growth per period (daily/weekly/monthly)
   - Growth rate (% change)
   - Growth spikes: identify specific posts or events that drove unusual follows
   - Growth stalls: periods of flat growth and what was happening content-wise
4. **Content-growth correlation**:
   - Which content types drive the most follows?
   - Engagement vs. follows: some posts get likes but not follows (entertainment), others drive follows (authority/value)
   - Viral moments vs. consistent growth
5. **Platform-specific growth dynamics**:
   - LinkedIn: connection requests vs. followers, newsletter subscribers
   - Twitter/X: follow-back culture, thread virality
   - Threads: early-platform growth dynamics
   - Bluesky: starter packs, custom feeds, community-driven growth
6. **Growth recommendations**: Specific actions to accelerate growth based on findings
7. **Milestone tracking**: Where the user is relative to their goals (from context)

**Related skills**: social-media-context, performance-analyzer, optimization-advisor

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `audience-growth-tracker` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/audience-growth-tracker/
git commit -m "feat: add audience-growth-tracker skill"
```

---

### Task 13: Analysis Layer — `content-pattern-analyzer`

**Files:**
- Create: `skills/content-pattern-analyzer/SKILL.md`
- Create: `skills/content-pattern-analyzer/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/content-pattern-analyzer/evals
touch skills/content-pattern-analyzer/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/content-pattern-analyzer/SKILL.md`**

**Frontmatter:**
```yaml
---
name: content-pattern-analyzer
description: "When the user wants to find patterns in what content works and what doesn't. Also use when the user mentions 'what's working,' 'content patterns,' 'best topics,' 'best format,' 'best time to post,' 'analyze my content,' 'do more of,' 'do less of,' or 'what should I change.' For raw metrics, see performance-analyzer. For audience-specific analysis, see audience-growth-tracker. For actionable recommendations, see optimization-advisor."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md`
2. **Data collection**:
   - **With BlackTwist**: Pull post history via `list_posts` and analytics via `get_post_analytics` for a meaningful sample (30+ posts minimum)
   - **Without BlackTwist**: Ask user to provide post history with metrics
3. **Pattern dimensions**:
   - **By topic/pillar**: Which content pillars perform best? Any that consistently underperform?
   - **By format**: Posts vs. threads vs. carousels — which format gets best engagement?
   - **By posting time**: Day of week and time of day patterns
   - **By length**: Short vs. long — is there a sweet spot?
   - **By hook type**: Which opening patterns get the most engagement?
   - **By tone**: Educational vs. personal vs. storytelling — what resonates?
   - **By platform**: Same content on different platforms — where does it perform best?
4. **Output: "Do More / Do Less" report**:
   - **Do more**: Top 3-5 patterns with evidence (e.g., "Threads about [pillar X] with story hooks get 3x average engagement")
   - **Do less**: Bottom 3-5 patterns with evidence
   - **Experiment with**: Gaps or untested combinations worth trying
5. **Cross-platform comparison**: If user posts similar content across platforms, compare performance
6. **Content gap identification**: Topics or formats the user hasn't tried that align with their audience

**Related skills**: social-media-context, performance-analyzer, optimization-advisor

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `content-pattern-analyzer` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/content-pattern-analyzer/
git commit -m "feat: add content-pattern-analyzer skill"
```

---

### Task 14: Analysis Layer — `optimization-advisor`

**Files:**
- Create: `skills/optimization-advisor/SKILL.md`
- Create: `skills/optimization-advisor/evals/.gitkeep`

- [ ] **Step 1: Create evals directory**

```bash
mkdir -p skills/optimization-advisor/evals
touch skills/optimization-advisor/evals/.gitkeep
```

- [ ] **Step 2: Write `skills/optimization-advisor/SKILL.md`**

**Frontmatter:**
```yaml
---
name: optimization-advisor
description: "When the user wants concrete recommendations on how to improve their social media performance. Also use when the user mentions 'what should I do next,' 'how do I improve,' 'optimize my social media,' 'recommendations,' 'suggestions,' 'next steps,' 'what's my biggest opportunity,' or 'help me grow.' Synthesizes insights from performance, audience, and pattern analysis into prioritized actions. For raw analytics, see performance-analyzer. For growth tracking, see audience-growth-tracker. For pattern detection, see content-pattern-analyzer."
metadata:
  version: 1.0.0
---
```

**Content must cover:**

1. **Context check**: Read `.agents/social-media-context.md` and any existing analysis
2. **Data synthesis**:
   - Pull from performance-analyzer findings (if available)
   - Pull from audience-growth-tracker findings (if available)
   - Pull from content-pattern-analyzer findings (if available)
   - If no prior analysis exists, run a quick assessment using BlackTwist data or user-provided info
3. **Recommendation framework** — prioritize by expected impact:
   - **Quick wins**: Changes that take <1 hour and likely improve results (e.g., "Start using story hooks — your data shows 2.5x engagement")
   - **Strategic shifts**: Bigger changes to content mix, platform focus, or posting cadence (e.g., "Shift 20% of educational content to storytelling — your stories outperform by 40%")
   - **Experiments to run**: Specific tests with hypothesis and success criteria (e.g., "Test posting LinkedIn carousels on Tuesday vs. Thursday for 4 weeks")
   - **Things to stop**: Content types or habits that actively hurt performance
4. **Recommendation format**:
   - Each recommendation: What to do → Why (evidence) → Expected impact → How to measure
   - Prioritized list (highest impact first)
   - Max 7-10 recommendations (focused, not overwhelming)
5. **With BlackTwist**: Also incorporate `get_recommendations` for platform-generated suggestions
6. **Action plan output**: A numbered list the user can immediately act on

**Related skills**: performance-analyzer, audience-growth-tracker, content-pattern-analyzer, social-media-context

- [ ] **Step 3: Run validation**

```bash
bash validate-skills.sh
```

Expected: `optimization-advisor` passes all checks.

- [ ] **Step 4: Commit**

```bash
git add skills/optimization-advisor/
git commit -m "feat: add optimization-advisor skill"
```

---

### Task 15: Final Validation and Root Commit

- [ ] **Step 1: Run full validation**

```bash
bash validate-skills.sh
```

Expected: All 14 skills pass (✓) on name, description, and line count.

- [ ] **Step 2: Verify repo structure**

```bash
find . -type f -not -path './.git/*' | sort
```

Expected: All files from the file map are present.

- [ ] **Step 3: Final commit if any uncommitted changes remain**

```bash
git status
# If anything is uncommitted:
git add -A
git commit -m "chore: final validation pass"
```
