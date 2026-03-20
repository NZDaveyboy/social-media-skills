# Social Media Skills

AI agent skills for social media content strategy, creation, and analysis across text-first platforms.

## Skill Catalog

### Foundation

| Skill                                                | Description                                                                                                 |
| ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| [social-media-context](skills/social-media-context/) | Captures platform context, audience details, content pillars, and tone preferences used by all other skills |

### Strategy

| Skill                                          | Description                                                                             |
| ---------------------------------------------- | --------------------------------------------------------------------------------------- |
| [content-strategy](skills/content-strategy/)   | Defines content pillars, audience targeting, and positioning for consistent brand voice |
| [content-calendar](skills/content-calendar/)   | Plans publishing cadence, themes, and scheduling across platforms                       |
| [platform-strategy](skills/platform-strategy/) | Tailors content approach per platform based on audience and format strengths            |

### Creation

| Skill                                            | Description                                                                      |
| ------------------------------------------------ | -------------------------------------------------------------------------------- |
| [post-writer](skills/post-writer/)               | Writes single standalone posts optimized for each platform's format and audience |
| [thread-writer](skills/thread-writer/)           | Writes multi-post threads with a clear narrative arc and strong opening hook     |
| [carousel-writer](skills/carousel-writer/)       | Writes slide-by-slide carousel scripts for LinkedIn and similar visual formats   |
| [content-repurposer](skills/content-repurposer/) | Transforms existing content into new formats and adapts it across platforms      |
| [hook-writer](skills/hook-writer/)               | Crafts high-performing opening lines to maximize engagement and stop-the-scroll  |

### Analysis

| Skill                                                        | Description                                                             |
| ------------------------------------------------------------ | ----------------------------------------------------------------------- |
| [performance-analyzer](skills/performance-analyzer/)         | Interprets post and account metrics to surface actionable insights      |
| [audience-growth-tracker](skills/audience-growth-tracker/)   | Tracks follower trends and identifies the content driving growth        |
| [content-pattern-analyzer](skills/content-pattern-analyzer/) | Identifies which content types, topics, and formats perform best        |
| [optimization-advisor](skills/optimization-advisor/)         | Recommends specific improvements based on performance data and patterns |

## Installation

### Claude Code plugin (recommended)

```bash
claude plugin add blacktwist/social-media-skills
```

### Git submodule

```bash
git submodule add https://github.com/blacktwist/social-media-skills .claude/skills/social-media-skills
```

### Git clone

```bash
git clone https://github.com/blacktwist/social-media-skills .claude/skills/social-media-skills
```

## Supported Platforms

- **LinkedIn** — long-form posts, carousels, newsletters
- **Twitter/X** — posts, threads, spaces
- **Threads** — posts, threads (Meta)
- **Bluesky** — posts, threads, starter packs

## Tool Integrations

### BlackTwist (primary)

[BlackTwist](https://blacktwist.app/mcp) is the recommended MCP integration for this skill set. When the BlackTwist MCP server is connected to your Claude environment, skills use it directly for:

- Publishing and scheduling posts
- Fetching analytics and engagement data
- Managing drafts and queued content
- Tracking follower growth

When BlackTwist is not available, skills fall back to advisory mode — generating content and instructions for manual posting.

See [tools/REGISTRY.md](tools/REGISTRY.md) for the full tool reference.

## License

MIT — see [LICENSE](LICENSE) for details.
