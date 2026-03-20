# Social Media Skills — Design Spec

## Overview

A skill set for social media creators and managers working across text-first platforms (LinkedIn, Twitter/X, Threads, Bluesky). Helps users define content strategy, write platform-tailored content in their own voice, analyze performance, and extract actionable suggestions.

Structured as a Claude Code plugin following the same conventions as [marketingskills](https://github.com/coreyhaines31/marketingskills): skills in `skills/<name>/SKILL.md`, cross-referenced, with a foundational context skill all others depend on.

## Target Users

- Solo creators and personal brands building their own audience
- Social media managers and marketers managing brands or clients

## Supported Platforms

- LinkedIn
- Twitter/X
- Threads
- Bluesky

## Architecture

Four layers, 14 skills total. Each skill is a single `SKILL.md` file with YAML frontmatter, under 500 lines.

### Foundation Layer

#### `social-media-context`

The base skill all others reference. The user defines their social media identity once; all creation and analysis skills read from it.

Stores to `.agents/social-media-context.md`:

- **Identity**: Creator vs. brand, role, industry
- **Target audience**: Who they are, pain points, what they care about
- **Voice & tone**: Descriptive adjectives, example phrases, things to avoid
- **Content pillars**: 3-5 topics the user owns
- **Platform config**: Which platforms, goals per platform, posting frequency
- **Example posts**: Real posts for style matching

### Strategy Layer

#### `content-strategy`

Builds a content framework around the user's pillars, audience, and goals. Outputs:

- Topic clusters mapped to content pillars
- Content mix ratios (educational / storytelling / promotional / engagement)
- Platform-specific content approaches
- Differentiation angles — what makes this voice unique in the space

References: `social-media-context`, `platform-strategy`

#### `content-calendar`

Turns strategy into a concrete posting schedule. Outputs:

- Weekly or monthly calendar with topics, formats, and target platforms
- Posting frequency per platform
- Content variety distribution (no pillar gets neglected)
- Key dates and events relevant to the user's niche

References: `content-strategy`, `social-media-context`

#### `platform-strategy`

Platform-specific tactical guidance:

- Algorithm nuances and what each platform rewards
- Optimal post lengths, formatting, and conventions per platform
- Cross-posting dos and don'ts
- Tone adaptation guidance (same voice, different register)
- Platform-specific features to leverage (LinkedIn polls, Twitter spaces, etc.)

References: `social-media-context`

### Creation Layer

#### `post-writer`

Writes single posts for any supported platform. Capabilities:

- Takes a topic, idea, or rough draft and produces platform-ready copy
- Respects the user's voice profile from `social-media-context`
- Optimizes for platform conventions (length, formatting, hashtags, CTAs)
- Can generate multiple variants for testing
- Supports different content types: educational, storytelling, promotional, engagement

References: `social-media-context`, `platform-strategy`, `hook-writer`

#### `thread-writer`

Writes multi-part threads for Twitter/X and similar formats:

- Hook writing for the opening post
- Narrative arc and pacing across posts
- Each post stands alone but builds on the previous
- Strong closers with CTAs
- Thread length optimization

References: `social-media-context`, `hook-writer`, `platform-strategy`

#### `carousel-writer`

Writes slide-by-slide content for LinkedIn carousels and similar visual-text formats:

- Slide structure and count recommendations
- Text density per slide (brief, scannable)
- Visual flow — each slide drives to the next
- Cover slide hook and final slide CTA
- Outputs slide-by-slide text content (not visual design)

References: `social-media-context`, `hook-writer`

#### `content-repurposer`

Transforms one piece of content into multiple formats and platforms:

- Blog post → thread → LinkedIn post → carousel
- Newsletter → tweet storm → Threads post
- Podcast notes → social snippets
- Maintains voice consistency while adapting to each platform
- Suggests which derivative formats have the highest leverage

References: `social-media-context`, `platform-strategy`, `post-writer`, `thread-writer`, `carousel-writer`

#### `hook-writer`

Specialized skill for opening lines that stop the scroll:

- Pattern library of proven hook formats: contrarian, question, story opener, statistic, list preview, bold claim, empathy
- Generates multiple hook options per topic
- Platform-aware — hooks that work on LinkedIn differ from Twitter/X
- Can be used standalone or invoked by other creation skills

References: `social-media-context`, `platform-strategy`

### Analysis Layer

#### `performance-analyzer`

Analyzes engagement metrics across posts:

- Metrics: likes, replies, reposts, impressions, saves, clicks
- Identifies top and bottom performers with reasoning
- Spots trends over time (improving, declining, plateauing)
- Generates actionable suggestions based on findings
- Uses BlackTwist analytics API when available; works from user-provided data otherwise

References: `social-media-context`, `content-pattern-analyzer`

#### `audience-growth-tracker`

Tracks follower growth and audience development:

- Growth trends over time per platform
- Correlates growth spikes with specific content
- Identifies what drives follows vs. engagement-without-follows
- Surfaces audience composition shifts
- Uses BlackTwist follower data when available

References: `social-media-context`, `performance-analyzer`

#### `content-pattern-analyzer`

Finds patterns in what works:

- Analyzes by: topic, format, posting time, length, tone, hook type
- Cross-platform comparison (same content, different platforms)
- Outputs a "do more / do less" report with specific evidence
- Identifies underexplored content gaps

References: `social-media-context`, `performance-analyzer`

#### `optimization-advisor`

Synthesizes insights into concrete next steps:

- Pulls from performance, audience, and pattern analysis
- Suggests strategy adjustments with rationale
- Recommends content experiments to run
- Proposes formats and topics to try or retire
- Prioritizes recommendations by expected impact

References: `performance-analyzer`, `audience-growth-tracker`, `content-pattern-analyzer`, `social-media-context`

## Tool Integration

### BlackTwist

When the BlackTwist MCP server is connected:

- **Creation skills** can schedule and publish posts directly
- **Analysis skills** can pull live metrics, follower data, and post analytics
- **Strategy skills** can access posting history for informed planning

When not connected, all skills operate in advisory mode — generating content and analysis from user-provided information.

### Available BlackTwist capabilities

- `create_post`, `edit_post`, `delete_thread` — content management
- `list_posts`, `list_drafts` — content inventory
- `get_post_analytics`, `get_live_metrics`, `get_metric_timeseries` — performance data
- `get_follower_growth` — audience tracking
- `get_consistency`, `get_daily_recap` — habit tracking
- `list_time_slots`, `reschedule_thread` — scheduling
- `get_recommendations` — platform suggestions

## Repo Structure

```
social-media-skills/
├── CLAUDE.md                          # Agent guidelines and repo overview
├── AGENTS.md                          # Agent Skills spec and validation
├── README.md                          # Human-readable documentation
├── LICENSE                            # MIT license
├── .gitignore
├── .claude-plugin/
│   └── marketplace.json               # Claude plugin marketplace config
├── skills/
│   ├── social-media-context/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── content-strategy/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── content-calendar/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── platform-strategy/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── post-writer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── thread-writer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── carousel-writer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── content-repurposer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── hook-writer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── performance-analyzer/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── audience-growth-tracker/
│   │   ├── SKILL.md
│   │   └── evals/
│   ├── content-pattern-analyzer/
│   │   ├── SKILL.md
│   │   └── evals/
│   └── optimization-advisor/
│       ├── SKILL.md
│       └── evals/
├── tools/
│   └── REGISTRY.md                    # Tool integrations (BlackTwist, etc.)
└── validate-skills.sh                 # Skill validation script
```

## Conventions

- **Skill file format**: YAML frontmatter with `name`, `description`, `metadata.version`, followed by markdown content
- **Naming**: kebab-case, 1-64 characters, lowercase/numbers/hyphens only
- **Max length**: 500 lines per SKILL.md
- **Style**: Active voice, clarity over cleverness, bold for key terms
- **Cross-references**: Skills reference related skills by name at the end of their content
- **Foundation dependency**: All creation and analysis skills check for `.agents/social-media-context.md` and prompt the user to run `social-media-context` if it doesn't exist
- **Tool fallback**: Every skill that uses BlackTwist has an advisory-only path for when the MCP is not connected
- **Version**: All skills start at 1.0.0
