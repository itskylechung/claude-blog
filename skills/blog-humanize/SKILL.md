---
name: blog-humanize
description: >
  Remove signs of AI-generated writing from blog posts. Detects and fixes
  24 AI writing patterns based on Wikipedia's "Signs of AI writing" guide:
  inflated symbolism, promotional language, superficial -ing analyses, vague
  attributions, em dash overuse, rule of three, AI vocabulary words, negative
  parallelisms, sycophantic tone, and excessive conjunctive phrases. Adds
  genuine voice and personality. Works with any blog format (MDX, markdown,
  HTML). Use when user says "humanize", "de-AI", "make it sound human",
  "remove AI patterns", "natural writing", "too AI", "sounds like AI",
  "AI detection", "humanize blog".
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Blog Humanizer -- Remove AI Writing Patterns

Identifies and removes signs of AI-generated text from blog posts. Based on
Wikipedia's "Signs of AI writing" guide, maintained by WikiProject AI Cleanup.

## Workflow

### Phase 1: Scan

1. **Read the blog post** -- detect format (MDX, markdown, HTML)
2. **Run AI pattern detection** across all 24 categories below
3. **Count instances** of each pattern type found
4. **Present a scan report**:
   - Total AI patterns found
   - Breakdown by category with line numbers
   - Severity: low (< 5 patterns), medium (5-15), high (> 15)

Wait for user approval before rewriting.

### Phase 2: Draft rewrite

Apply fixes for every detected pattern. Preserve the post's core meaning,
structure, and any sourced statistics. The goal is natural writing, not
sterile writing -- add voice, vary rhythm, have opinions where appropriate.

### Phase 3: Anti-AI audit

After drafting, answer: "What makes this still obviously AI generated?"
List remaining tells as brief bullets.

### Phase 4: Final revision

Fix the remaining tells identified in Phase 3. Present the final version.

### Phase 5: Summary

```
## Humanizer complete: [Title]

### Patterns fixed
- [N] total AI patterns removed
- [breakdown by top categories]

### Voice check
- Sentence length variance: [before SD] -> [after SD]
- Personality signals added: [list]

### Remaining notes
- [any patterns that couldn't be fixed without changing meaning]
```

---

## The 24 AI writing patterns

### Content patterns

**1. Inflated significance and legacy**

Words to watch: stands/serves as, is a testament/reminder, vital/significant/
crucial/pivotal/key role/moment, underscores/highlights importance, reflects
broader, symbolizing ongoing/enduring/lasting, setting the stage, marking/
shaping, represents/marks a shift, key turning point, evolving landscape,
focal point, indelible mark, deeply rooted.

Fix: State what happened and why, without editorializing its importance.

**2. Inflated notability and media coverage**

Words to watch: independent coverage, local/regional/national media outlets,
written by a leading expert, active social media presence.

Fix: Cite one specific source with a specific claim instead of listing names.

**3. Superficial -ing analyses**

Words to watch: highlighting/underscoring/emphasizing..., ensuring...,
reflecting/symbolizing..., contributing to..., cultivating/fostering...,
encompassing..., showcasing...

Fix: Remove the -ing phrase. If the information matters, make it its own
sentence with a specific claim.

**4. Promotional language**

Words to watch: boasts a, vibrant, rich (figurative), profound, enhancing its,
showcasing, exemplifies, commitment to, natural beauty, nestled, in the heart
of, groundbreaking (figurative), renowned, breathtaking, must-visit, stunning.

Fix: Replace with plain description. Add a specific detail instead.

**5. Vague attributions and weasel words**

Words to watch: Industry reports, Observers have cited, Experts argue, Some
critics argue, several sources/publications.

Fix: Name the specific source, person, or study. If you can't, cut the claim.

**6. Formulaic "challenges and future prospects" sections**

Words to watch: Despite its... faces several challenges..., Despite these
challenges, Challenges and Legacy, Future Outlook.

Fix: State specific problems with dates and details. Cut vague optimism.

### Language and grammar patterns

**7. Overused AI vocabulary**

High-frequency words: Additionally, align with, crucial, delve, emphasizing,
enduring, enhance, fostering, garner, highlight (verb), interplay, intricate/
intricacies, key (adjective), landscape (abstract), pivotal, showcase,
tapestry (abstract), testament, underscore (verb), valuable, vibrant.

Fix: Use plain alternatives. "Additionally" -> "Also" or restructure.
"Crucial" -> cut it or say why it matters. "Landscape" -> name the specific
domain.

**8. Copula avoidance (avoiding "is"/"are")**

Words to watch: serves as/stands as/marks/represents [a], boasts/features/
offers [a].

Fix: Use "is", "are", "has". Simple is better.

**9. Negative parallelisms**

Patterns: "Not only...but...", "It's not just about..., it's...", "It's not
merely a..., it's a..."

Fix: Say what the thing IS. Cut the theatrical contrast.

**10. Rule of three overuse**

Pattern: forcing ideas into groups of three for false comprehensiveness.

Fix: Use the actual number of items. Two is fine. Four is fine.

**11. Elegant variation (synonym cycling)**

Pattern: protagonist/main character/central figure/hero all in one paragraph.

Fix: Pick one term and stick with it. Repetition is fine.

**12. False ranges**

Pattern: "from X to Y" where X and Y aren't on a meaningful scale.

Fix: List items plainly without forcing them into a range.

### Style patterns

**13. Em dash overuse**

Fix: Replace most em dashes with commas, periods, or parentheses.

**14. Overuse of boldface**

Fix: Remove mechanical bolding. Bold only when genuinely drawing attention
to something the reader might miss.

**15. Inline-header vertical lists**

Pattern: bullet points starting with "**Header:** description..."

Fix: Convert to prose paragraphs when the list has < 5 items. For longer
lists, keep the structure but drop the bold headers.

**16. Title case in headings**

Fix: Use sentence case. Capitalize only the first word and proper nouns.

**17. Emojis**

Fix: Remove all emojis from headings and bullet points.

**18. Curly quotation marks**

Fix: Replace curly quotes with straight quotes for code/technical content.
Curly quotes are acceptable in prose-heavy editorial content.

### Communication patterns

**19. Collaborative artifacts**

Words to watch: I hope this helps, Of course!, Certainly!, You're absolutely
right!, Would you like..., let me know, here is a...

Fix: Delete entirely. Start with the content.

**20. Knowledge-cutoff disclaimers**

Words to watch: as of [date], Up to my last training update, While specific
details are limited/scarce..., based on available information...

Fix: State what you know with a source. If unknown, say so plainly.

**21. Sycophantic/servile tone**

Fix: Cut the flattery. Respond to the substance.

### Filler and hedging

**22. Filler phrases**

Common patterns:
- "In order to" -> "To"
- "Due to the fact that" -> "Because"
- "At this point in time" -> "Now"
- "In the event that" -> "If"
- "Has the ability to" -> "Can"
- "It is important to note that" -> cut it

**23. Excessive hedging**

Fix: Reduce qualifiers. One hedge per claim is enough. Zero is usually better.

**24. Generic positive conclusions**

Words to watch: the future looks bright, exciting times lie ahead, journey
toward excellence, step in the right direction.

Fix: End with a specific fact, recommendation, or next step. Or just stop.

---

## Voice injection

Removing AI patterns is half the job. The other half is making sure the result
doesn't read like a sanitized press release.

Signs of soulless writing (even when technically clean):
- Every sentence is the same length
- No opinions, just neutral reporting
- No acknowledgment of uncertainty
- No first-person perspective when appropriate
- No humor, no edge, no personality

How to add voice:
- **Have opinions.** React to facts, don't just report them
- **Vary rhythm.** Short sentences. Then longer ones that take their time
- **Acknowledge complexity.** "This is impressive but also unsettling"
- **Use "I" when it fits.** First person isn't unprofessional
- **Be specific about feelings.** Not "concerning" but "unsettling"
- **Let some mess in.** Perfect structure feels algorithmic
