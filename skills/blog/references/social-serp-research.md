# Social & SERP Research — ByCrawl MCP + Playwright Patterns

Reference for bycrawl API call patterns and Playwright scraping approaches used
by the blog-write skill. Keeps implementation details out of SKILL.md.

---

## 1. ByCrawl MCP Tool Patterns

### Social Keyword Discovery (Phase 1.3 + Phase 2)

- Search across platforms for the target keyword (~8 calls):
  - `reddit_search_posts` — sort: `new`, then `top`
  - `x_search_posts` — product: `Latest`, then `Top`
  - `tiktok_search_videos`
  - `youtube_search_videos`
  - `threads_search_posts`
- Extract from results:
  - **Emerging terms** — present in Latest/new but absent from Top
  - **Long-tail variations** — multi-word phrases in titles and comments
  - **Question-format keywords** — "how to…", "why does…", "best way to…"
  - **Volume signal** — engagement counts as rough demand proxy

### Content Gap Analysis (Phase 2)

- Pull top-performing content (~8 calls):
  - `youtube_search_videos`, `tiktok_search_videos`
  - `reddit_search_posts`, `x_search_posts`
- Pull transcripts from top 3-5 YouTube videos:
  - `youtube_get_video_transcription`
- Extract:
  - **Saturated topics** — covered repeatedly across platforms
  - **Content gaps** — questions asked but not answered well
  - **Unique angles** — underrepresented perspectives worth owning

### Comment Mining for FAQs (Phase 2 + Phase 5l)

- Pull comments (~6-10 calls):
  - `youtube_get_video_comments` — top 3 videos
  - `tiktok_get_video_comments` — top 3 videos
- Extract:
  - Recurring questions → FAQ items
  - Pain points → H2 topic candidates
  - Exact user phrases → natural-language body copy

### Audience Language Mining (Phase 5)

- Transcripts for tone and vocabulary:
  - `tiktok_get_video_subtitles` — top 3 videos
  - `youtube_get_video_transcription` — top 3 videos
- Emotional triggers (~10 calls):
  - `x_search_posts` with query: `"love OR hate OR wish OR need" {keyword}`
  - `reddit_search_posts` with query: `"frustrated OR amazing OR changed my life" {keyword}`
- Apply mined language to article:
  - Proven hooks → intro paragraph
  - Pain-point phrases → body sections
  - Real discussions → inline examples and anecdotes
  - Platform tone → overall voice matching

### Competitor Social Audit (Phase 2)

- Queries (~6-9 calls):
  - `x_search_posts` — `"{competitor} {topic}"`
  - `youtube_search_videos` — `"{competitor} {topic}"`
  - `reddit_search_posts` — `"{competitor} {topic}"`
- Extract:
  - Competitor messaging and positioning
  - Audience sentiment (positive, negative, mixed)
  - Gaps competitors leave unaddressed

### Post-Write Keyword Validation (Phase 6)

- Quick freshness check (~4 calls):
  - `reddit_search_posts` (sort: `new`)
  - `x_search_posts` (product: `Latest`)
  - `tiktok_search_videos`
  - `threads_search_posts`
- Interpret:
  - High recent volume → topic is alive, proceed
  - Low or declining volume → consider pivoting or adding a trending angle

---

## 2. Playwright SERP & Trends Scraping

### Google Trends Data (Phase 2)

- URL pattern: `https://trends.google.com/trends/explore?q={keyword}&date=today+12-m`
- Use Playwright to scrape:
  - Interest-over-time chart data
  - Related queries (top + rising)
- Fallback: `WebSearch` for `"[keyword] google trends 2026"`

### SERP Feature Analysis (Phase 2.5)

- URL: `https://www.google.com/search?q={keyword}`
- Extract:
  - **People Also Ask** questions (up to 8)
  - Top 10 organic titles and meta descriptions
  - Related searches at page bottom
- Detect presence of:
  - AI Overview
  - Featured Snippet
  - PAA box
  - Knowledge Panel
- Fallback: `WebSearch` for PAA questions and competitor titles

### People Also Ask → H2 + FAQ (Phase 3)

- PAA questions become:
  - H2 heading candidates (reworded for natural flow)
  - FAQ schema items (verbatim question, concise answer)

### Competitor Title Pattern Analysis (Phase 5a)

- From SERP organic titles, analyze:
  - Number usage (e.g., "7 Ways…", "Top 10…")
  - Question format prevalence
  - Year inclusion (e.g., "…in 2026")
  - Power words (ultimate, proven, essential)
  - Character length distribution

---

## 3. Social Proof Embedding Patterns

Inline social proof reinforces E-E-A-T signals without replacing tier 1-3 sources.

| Platform | Attribution Template |
|----------|---------------------|
| Reddit   | "A discussion in r/{subreddit} with {upvotes} upvotes…" |
| X        | "As @{handle} noted in a post with {likes} likes…" |
| YouTube  | "In a video with {views} views, {channel} demonstrated…" |
| TikTok   | "A TikTok by @{creator} with {views} views showed…" |

**Rules:**
- Always attribute with platform name + engagement metric
- Social proof reinforces — never replaces — tier 1-3 sources
- Target 2-3 social proof citations per article
- Prefer high-engagement posts (top 10% of results)

---

## 4. Estimated API Usage Per Article

| Phase     | ByCrawl Calls | Playwright Ops | Notes                        |
|-----------|---------------|----------------|------------------------------|
| Phase 1.3 | ~8            | 0              | Keyword discovery            |
| Phase 2   | ~20-30        | 1 (Trends)     | Gap analysis + transcripts   |
| Phase 2.5 | 0             | 1 (SERP)       | Feature detection            |
| Phase 5   | ~10           | 0 (reuse)      | Language mining              |
| Phase 6   | ~4            | 0              | Validation                   |
| **Total** | **~42-52**    | **~2**         |                              |

---

## 5. Error Handling

- **Empty results:** Skip the platform, log it, continue with remaining platforms.
- **Missing API key:** Fall through to standard `WebSearch`-based research.
- **Rate limit hit:** Reduce request count by half, retry once, then skip.
- **Playwright unavailable:** Fall back to `WebSearch` queries for SERP data.
- **Partial data is acceptable:** Always deliver whatever results are available
  rather than failing the entire research phase.
