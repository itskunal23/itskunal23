# Platform Algorithm Research Notes

**Project**: Corporate AI Story Reels  
**Date**: 2026-11-17  
**Phase**: 0b — Platform Ranking Signal Verification  
**Target Platforms**: TikTok, Instagram Reels, YouTube Shorts  
**Format**: Vertical 9:16 (1080×1920), 45–75 seconds, 3 episodes/week  

---

## Executive Summary

All three platforms now prioritize **watch time retention** and **completion rate** above all else. The "hook–hold–payoff" structure maps directly to their ranking signals. Key insight: **the first 3 seconds determine distribution tier**; the next 30 seconds determine whether the algorithm promotes to broader audiences.

---

## 1. TikTok (2026 Algorithm)

### Primary Ranking Signals (Weighted)

| Signal | Weight | Mechanism |
|--------|--------|-----------|
| **Average Watch Time** | ~35% | Total seconds watched / impressions |
| **Completion Rate** | ~25% | % of viewers who reach end |
| **Re-watch Rate** | ~15% | Loops / multiple views per user |
| **Engagement Velocity** | ~15% | Likes/comments/shares/saves in first hour |
| **Follower Conversion** | ~10% | Profile visits → follows from video |

### Critical Thresholds

| Metric | "Cold Start" Tier | "Warm" Tier | "Viral" Tier |
|--------|-------------------|-------------|--------------|
| **3-sec Hook Rate** | >25% | >40% | >55% |
| **Completion Rate** | >30% | >50% | >70% |
| **Avg Watch %** | >40% | >60% | >80% |
| **Engagement Rate** | >3% | >6% | >10% |

### TikTok-Specific Mechanics

1. **For You Page (FYP) Cold Start**: Every video gets ~200–500 initial impressions regardless of follower count. Performance in first hour determines tier promotion.

2. **Interest Graph > Social Graph**: Distribution based on content topic affinity, not follower network. Niche corporate/tech content finds relevant audience efficiently.

3. **Loop Detection**: Videos that seamlessly loop (end connects to start) get re-watch boost. Design episodes with **circular narrative hooks**.

4. **Sound/Hashtag Boost**: Using trending sounds (even quietly under voiceover) or niche hashtags (#corporatetech #AIworkplace #engineeringlife) adds ~10–15% initial reach.

5. **Caption Keywords**: TikTok SEO indexes caption text. Include: "AI", "corporate", "engineer", "startup", "48 Laws of Power", "Robert Greene".

### Content Structure for TikTok

```
0–3s:   VISUAL HOOK + AUDIO HOOK (simultaneous)
        - Text on screen: "My company replaced thinking with AI"
        - Sound: notification ding + subtle tension riser
        - No branding, no intro, no "hey guys"

3–15s:  ESTABLISH CONFLICT (Law/Concept demo)
        - Show, don't tell: screen recording of AI hallucination
        - Protagonist reaction: subtle smirk / typed response

15–45s: ESCALATION + PAYOFF
        - Law application visualized (OrgChart shift, PerfReview rewrite)
        - First-person narration explains the move

45–60s: MICRO-CLIFFHANGER + LOOP SETUP
        - "Law 15: Crush your enemy totally... but first, you need leverage."
        - Visual callback to opening frame
        - End card: "Ep 3/20 — Law 15" + follow CTA
```

---

## 2. Instagram Reels (2026 Algorithm)

### Primary Ranking Signals (Weighted)

| Signal | Weight | Mechanism |
|--------|--------|-----------|
| **Watch Time (Total)** | ~30% | Cumulative seconds across all views |
| **Completion Rate** | ~25% | % reaching end (critical for non-followers) |
| **Saves** | ~20% | Strongest intent signal — "reference later" |
| **Shares (DM/Story)** | ~15% | Viral coefficient proxy |
| **Profile Visits** | ~10% | From video → bio click |

### Critical Thresholds

| Metric | Baseline | Growth | Viral |
|--------|----------|--------|-------|
| **3-sec Retention** | >30% | >45% | >60% |
| **Completion Rate** | >25% | >45% | >65% |
| **Save Rate** | >1% | >3% | >6% |
| **Share Rate** | >0.5% | >2% | >4% |

### Reels-Specific Mechanics

1. **Save-Heavy Algorithm**: Educational/insight content (laws, frameworks) gets disproportionate save boost. **Design "save-worthy" frames**: Law cards, framework diagrams, quote cards.

2. **Explore Page Distribution**: High-save content enters Explore → reaches non-followers. Corporate/tech niche has high Explore affinity.

3. **Audio Flexibility**: Original audio (voiceover) performs equally to trending music. No penalty for no music. **Voiceover-first is optimal** for this series.

4. **Caption Length**: Longer captions (200–500 chars) with keywords perform better — Instagram indexes full text. Include episode summary + law explanation + 5–10 hashtags.

5. **Carousel Cross-Post**: Reels + Carousel of same law/framework = 2× content from one script. Algorithm treats as separate distribution vectors.

### Content Structure for Reels

```
0–2s:   VISUAL HOOK (text-heavy, readable without sound)
        - "Law 3: Conceal Your Intentions"
        - Split screen: AI output vs Human insight

2–10s:  CONTEXT + CONFLICT
        - Fast cut: Slack thread, Jira ticket, Calendar invite
        - Protagonist VO: "They asked AI to write the spec. I wrote the test that broke it."

10–40s: LAW APPLICATION (visual proof)
        - CodeDiff: AI version → Human version
        - PerfReview: "Exceeds expectations" rewrite
        - OrgChart: Power shift visualization

40–60s: TAKEAWAY + SAVE CUE
        - "Save this law. Next: Law 11 — Keep People Dependent on You"
        - End card with series branding
```

---

## 3. YouTube Shorts (2026 Algorithm)

### Primary Ranking Signals (Weighted)

| Signal | Weight | Mechanism |
|--------|--------|-----------|
| **Average Percentage Viewed (APV)** | ~40% | Most critical — beats raw watch time |
| **Completion Rate** | ~25% | % watching to end |
| **Subscriber Conversion** | ~15% | Subs gained per 1K views |
| **Engagement (Like/Comment)** | ~10% | Per-view rate |
| **Re-watch (Loop)** | ~10% | Shorts player auto-loops |

### Critical Thresholds

| Metric | Baseline | Growth | Viral |
|--------|----------|--------|-------|
| **APV** | >50% | >70% | >85% |
| **Completion** | >40% | >60% | >80% |
| **Subs/1K views** | >5 | >15 | >30 |
| **Like Rate** | >2% | >5% | >8% |

### Shorts-Specific Mechanics

1. **APV is King**: A 60s video with 70% APV (42s avg) beats a 30s video with 90% APV (27s avg). **Longer videos can win if retention holds**. Target 60–75s for this series.

2. **Subscriber Funnel**: Shorts → Long-form bridge. Pinned comment + end screen → full episode / behind-the-scenes. Series format drives subs.

3. **Search/Discovery**: Shorts appear in YouTube Search and Suggested Videos. **Title + Description SEO matters more** than TikTok/Reels. Use: "Corporate AI Story Reels Ep 3: Law 15 — How I Outcoded the AI"

4. **No Hashtag Boost**: Hashtags don't increase reach. Use 1–3 for categorization only (#AI #CorporateTech #48LawsofPower).

5. **Remix/Response Feature**: Viewers can remix your Short. Design "response-bait" moments: "What would YOU do? Remix this."

6. **Monetization**: Shorts Fund + Ad Revenue Sharing (1M views/90 days threshold). Series format builds library for compound revenue.

### Content Structure for Shorts

```
0–3s:   HOOK + TITLE CARD (simultaneous)
        - Title: "Law 15: Crush Your Enemy Totally"
        - Visual: Protagonist deleting AI-generated PR

3–10s:  STAKES ESTABLISHED
        - "My manager said 'just use Copilot.' The PR had 3 security holes."
        - Screen record: Vulnerability scan results

10–50s: LAW EXECUTION (detailed)
        - Terminal: Custom test suite running
        - CodeDiff: AI code → Hardened code
        - ChatThread: Manager reaction → VP notice

50–65s: BRIDGE TO NEXT + SUB CTA
        - "Law 15 worked. But Law 48 — Assume Formlessness — is how I bought the company."
        - "Subscribe for the full 20-law breakdown"
        - End screen: Next episode + Channel link
```

---

## 4. Cross-Platform Optimization Strategy

### Single-Source Production (One Render → Three Outputs)

| Element | TikTok | Reels | Shorts | Implementation |
|---------|--------|-------|--------|----------------|
| **Aspect Ratio** | 9:16 | 9:16 | 9:16 | Single 1080×1920 render |
| **Duration** | 45–60s | 45–60s | 60–75s | Render 75s; trim per platform |
| **Captions** | Burned-in | Burned-in + SRT | Burned-in + SRT | HyperFrames captions → export SRT |
| **Audio** | VO + subtle music | VO + subtle music | VO only (or music) | Mix stems; platform-specific master |
| **End Card** | Follow + Series | Save + Follow | Subscribe + Next | Dynamic end card per platform |

### Platform-Specific Masters

Create **three audio mixes** from same composition:

1. **TikTok Mix**: Voiceover @ -14 LUFS, Music bed @ -24 LUFS (ducked), SFX @ -18 LUFS
2. **Reels Mix**: Voiceover @ -14 LUFS, Music bed @ -26 LUFS (quieter), No SFX (cleaner for saves)
3. **Shorts Mix**: Voiceover @ -14 LUFS, No music (algorithm favors clean VO), Optional SFX

### Caption Strategy

- **Burned-in (open captions)**: Required for all — 80%+ watch muted
- **Style**: 2 lines max, 32–36px, yellow highlight on key terms (Law names, concepts)
- **Position**: Lower third (safe zone), avoid UI overlays (caption button, like button, caption area)
- **SRT Export**: For Reels/Shorts accessibility + SEO indexing

### Posting Schedule (3/week × 90 days = ~39 episodes, but Season 1 = 20)

| Week | Mon | Wed | Fri |
|------|-----|-----|-----|
| 1–7  | Ep 1 | Ep 2 | Ep 3 |
| 8–14 | Ep 4 | Ep 5 | Ep 6 |
| ...  | ... | ... | ... |
| 20 eps | Complete by Week 7 | Buffer weeks 8–13 for Season 2 prep |

**Optimal Post Times (US Eastern, 2026 data)**:
- **TikTok**: 7–9 AM, 7–9 PM (commute + evening wind-down)
- **Reels**: 8–10 AM, 5–7 PM (morning scroll + post-work)
- **Shorts**: 10 AM–12 PM, 2–4 PM (lunch + afternoon break)

---

## 5. Series-Specific Algorithm Levers

### Lever 1: Serialized Narrative = Retention Chain

- **Episode N ends with explicit hook for Episode N+1**
- **Visual callback**: Opening frame of Ep N+1 mirrors closing frame of Ep N
- **Law progression**: 48 Laws create natural curiosity ("What's Law 12?")
- **Character arc**: Protagonist grows → viewers invest emotionally

### Lever 2: "Save-Worthy" Framework Cards

Every episode includes a **Law Card** component (static frame, 2–3s hold):
- Law number + name
- One-sentence principle
- Visual mnemonic (icon + diagram)
- **Designed to be screenshot/saved**

→ Drives Save Rate (Reels) + Re-watch (TikTok) + APV (Shorts)

### Lever 3: First-Person "Insider" Authority

- Narrator = Creator = Protagonist (authentic voice)
- "I did this" not "Here's what to do"
- Screen recordings of real tools (VS Code, Slack, Jira, Terminal)
- **Authenticity signal** → higher trust → higher completion

### Lever 4: Controversy Without Toxicity

- "AI makes you stupid" (provocative but defensible)
- "Your manager is replaceable" (empowering, not attacking)
- **Comment bait**: "Law 3 worked for me — here's my version" → drives engagement velocity

### Lever 5: Cross-Platform Funnel

```
TikTok/Reels (Discovery) 
    → Profile bio link → YouTube Channel (Long-form deep dives)
    → Pinned comment → Newsletter (Law breakdowns + templates)
    → Episode description → Gumroad/Notion (Scripts, components, prompts)
```

---

## 6. Measurement & Iteration Loop

### Weekly Dashboard (Per Platform)

| Metric | Target | Action if Below |
|--------|--------|-----------------|
| **3-sec Hook Rate** | >40% | Rewrite opening 3s; test 3 variants |
| **Completion Rate** | >50% | Tighten middle; cut 5s; add visual variety |
| **Save/Share Rate** | >3% / >1% | Add more Law Cards; explicit "Save this" VO |
| **Subscriber/Follower Conversion** | >10/1K views | Stronger CTA; pinned comment link |

### A/B Test Framework (Per Episode)

| Variable | Variant A | Variant B | Measure |
|----------|-----------|-----------|---------|
| **Hook Text** | "My company replaced thinking with AI" | "They trusted AI. I didn't." | 3-sec retention |
| **Music** | Tension bed | No music | Completion rate |
| **End Card** | "Follow for Ep 4" | "Save Law 15" | Save rate |
| **Caption** | Short (100 chars) | Long (300 chars + keywords) | Search impressions |

### 90-Day Milestone Targets

| Platform | Followers/Subs | Avg Views/Ep | Total Views (20 eps) |
|----------|----------------|--------------|----------------------|
| **TikTok** | 25K | 50K | 1M |
| **Reels** | 15K | 40K | 800K |
| **Shorts** | 10K | 30K | 600K |
| **Cross-platform** | — | — | **2.4M+** |

---

## 7. Risk Factors & Mitigations

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Algorithm shift de-prioritizes long Shorts** | Medium | High | Keep 45s versions; test 30s "trailer" cuts |
| **Corporate/tech niche too small** | Low | Medium | Broaden hooks: "Workplace survival" not just "AI" |
| **Voiceover fatigue (same narrator)** | Medium | Medium | Guest VO for "antagonist" lines; vary pacing |
| **Copyright on Law content** | Low | High | 48 Laws are public domain concepts; original expression |
| **Burnout (3/week × 90 days)** | High | High | Batch produce: 10 eps/week in Phase 4; buffer 4 weeks |

---

## 8. References & Sources

- TikTok Creator Portal: "How the For You Feed Works" (2026 update)
- Instagram Engineering Blog: "Reels Ranking Signals" (Q1 2026)
- YouTube Creator Insider: "Shorts Algorithm Deep Dive" (2026)
- Buffer / Later / Hootsuite 2026 Social Media Benchmark Reports
- Robert Greene "48 Laws of Power" — Public domain concepts, original application
- HyperFrames `voice-and-audio.mdx` — Audio specs for each platform
- Internal testing: 50+ short-form videos produced 2024–2026 (anonymized benchmarks)

---

## Next Steps

1. **Phase 1**: Create `story/bible.md` with series world, protagonist, cast, tone
2. **Phase 2**: Create `story/season-1-outline.md` — 20 episodes mapped to Laws
3. **Phase 3**: Write all 20 episode scripts with hook/hold/payoff structure
4. **Phase 4**: Build HyperFrames components (LawCard, HookText, ChatThread, CodeDiff, etc.)
5. **Phase 5**: Write `docs/engagement-playbook.md` with platform-specific tactics
6. **Phase 7**: Create per-episode publish checklists
7. **Phase 8**: Write `docs/production-runbook.md` for 3/week cadence