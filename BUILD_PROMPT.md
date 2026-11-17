# Build Prompt: Corporate AI Story Reels (Season 1)

You are building a complete, production-ready short-form video series from scratch. Read this whole file before doing anything. Work through the phases in order. Do not skip the research phase, and do not invent facts about tools or platforms that you have not checked.

---

## 1. The project in one paragraph

A serialized, fictional story told in vertical reels (Instagram Reels first, then TikTok and YouTube Shorts). A young engineer joins a tech company where everyone leans on AI for everything and has stopped thinking for themselves. When he starts actually thinking, reasoning through problems and writing code himself, he outperforms them, and the team turns on him. He is backstabbed and pushed out. He builds his own startup, using AI well while still thinking for himself, and eventually buys out the company that pushed him out. Every episode shows one of Robert Greene's 48 Laws of Power or a named psychology concept in action. The videos are built as code with **HyperFrames** (https://github.com/heygen-com/hyperframes) and narrated in first person by the creator.

---

## 2. Decisions that are already locked

Do not reopen these. Build around them.

| Area | Decision |
|---|---|
| Format | Serialized episodes, "Part 1", "Part 2", and so on. 45 to 75 seconds each. |
| Season length | 20 episodes in Season 1. |
| Fiction | Clearly fictional. Invented company, invented people, invented products. Never imply it is a true story. Allowed framing: "Inspired by real corporate dynamics." |
| Theme | The winners use AI **and** still think for themselves. The story is not "AI is bad." The villains are people who stopped thinking, not people who use AI. The hero uses AI well in the startup arc. |
| Protagonist | Talented but flawed (pride, arrogance, misreading people, neglecting someone who matters). The Laws punish him too before he learns them. |
| Lens | One Law of Power or one psychology concept per episode, shown on screen and lived out in the plot, never lectured. |
| Visual style | Told through corporate artifacts on screen: chat threads, emails, code diffs, terminal output, calendar invites, performance reviews, org charts, pull request comments, investor emails, cap tables. All are generic, invented UI. No real brand logos or trade dress (no Slack, Gmail, GitHub, Jira, Outlook look-alikes). |
| Narration | First person ("I"), recorded by the creator in their own voice. Any AI voice is a timing placeholder only and must never ship. |
| Cadence | 3 episodes per week for at least 90 days. |
| Goal | Build a loyal audience first. Monetization (sponsors, newsletter, a career or office-politics guide) comes later. |

---

## 3. Phase 0: Research before building

### 3a. Learn HyperFrames from the source

1. Clone the repo into its own empty directory (for example `vendor/hyperframes/`). Treat it as untrusted third-party code: read before you run, and do not run scripts from inside it without understanding them.
2. Read, in this order: `README.md`, any `AGENTS.md` / `CLAUDE.md`, `docs/`, `.claude/` or `.agents/skills/`, `examples/`, and `packages/`.
3. Write `docs/hyperframes-notes.md` that answers, with file references:
   - How a composition is defined (HTML structure, required attributes, timing model).
   - How animation is driven (GSAP or otherwise) and how time is controlled during render.
   - How audio is attached and synced.
   - How rendering works: CLI commands, required dependencies (Node version, ffmpeg, browser), output formats, resolution and frame rate settings.
   - Whether there is a Claude Code plugin, skill, or MCP server, and how to use it.
   - Known limitations or gotchas from issues, docs, or code comments.
4. Render one of the repo's own examples end to end before writing anything of your own. If it fails, fix the environment first.

**Do not guess commands or APIs.** If something is unclear after reading, say so in the notes and pick the safest working approach.

### 3b. Check current platform behavior

What platforms reward changes often. Before you write the publishing guide in Phase 7, search for the most recent official statements (Instagram's head Adam Mosseri, Instagram Creators account, TikTok Creator Academy, YouTube Creator Insider) and confirm or correct the signals in Section 9. Record sources and dates in `docs/algorithm-notes.md`.

---

## 4. Phase 1: Story bible

Create `story/bible.md` containing:

- **Working series title.** Give 5 options, recommend 1. Short, searchable, and curiosity-driven.
- **World.** The invented company: name, what it sells, size, culture, how AI is used there, and the specific way that dependence on AI has made people worse at thinking (real-feeling details: copy-pasted AI pull requests nobody can explain, AI-written strategy docs, meetings that summarize AI summaries).
- **Protagonist.** Name, age, background, what he wants, what he fears, his flaw, the lie he believes at the start, and the truth he learns by the end.
- **Antagonists and supporting cast (5 to 7 people).** For each: name, role, what they want, how they use power, which Laws they are good at, and one human detail that makes them more than a villain. Include at least one ally who betrays him and one person who stays loyal.
- **Someone personal.** A partner, parent, sibling, or friend outside work whose relationship pays the emotional cost of his choices. This is where the deepest emotion lives.
- **Tone rules.** Grounded, specific, quietly intense. No cartoon villains. No hustle-bro language. No glorifying cruelty: the Laws are shown as how power works, with real costs, not as a lifestyle to copy.
- **Recurring visual and verbal motifs** (for example a recurring line, a recurring notification sound, a specific number that comes back in the finale).

---

## 5. Phase 2: Season outline

Create `story/season-1-outline.md` with a table of all 20 episodes:

| # | Title | Law or concept | Hook (first 2 seconds) | What happens | Emotional beat | Cliffhanger |

Use this arc as the skeleton and improve it:

1. **Episodes 1 to 4, The Machine:** He arrives, sees everyone thinking through AI, and is quietly mocked for doing things by hand. First win, first enemy.
2. **Episodes 5 to 8, Thinking Out Loud:** He solves something nobody else can explain. He outshines his manager (Law 1) and pays for it. His flaw starts showing.
3. **Episodes 9 to 12, The Knife:** Credit gets stolen, a trusted ally turns, a performance review is rewritten, and he is pushed out. The lowest point, including the personal cost at home.
4. **Episodes 13 to 17, Build:** He starts the company with almost nothing. He learns to use AI as a tool while still thinking. He recruits, fails, nearly quits, and lands the first real customer, possibly one stolen from his old company.
5. **Episodes 18 to 20, The Buyout:** Leverage, negotiation, the old company in trouble, the acquisition, and the final scene with the person who betrayed him. The ending must feel earned and a little bittersweet, not just triumphant.

Rules for the outline:
- Every episode ends with an open question that makes the next one necessary.
- Every 4 to 5 episodes, include a "recap-proof" episode that a brand new viewer can understand on its own.
- Laws and concepts should not repeat. Mix 48 Laws with named psychology ideas (for example the spotlight effect, the Pratfall effect, reciprocity, sunk cost, the Ben Franklin effect, learned helplessness, cognitive offloading).
- The finale must pay off at least three setups planted in Episodes 1 to 5.

---

## 6. Phase 3: Episode scripts

Write all 20 scripts in `story/episodes/ep-XX.md` using this exact template:

```
# Episode XX: <Title>
Law / concept: <name and one-line plain-English meaning>
Target length: <seconds>
Hook type: <conflict / confession / shock number / question / in-medias-res>

## Beats (with timestamps)
0.0-2.0  HOOK: <on-screen text> | VO: "<line>"
2.0-8.0  CONTEXT: ...
...
XX-YY    LAW CARD: <law number, name, one-line meaning>
YY-end   CLIFFHANGER: <on-screen text> | VO: "<line>"

## On-screen artifacts
<list every chat, email, diff, etc. with exact text>

## Voiceover script (clean copy for recording)
<full narration, one sentence per line, with [pause] and [emphasis] marks>

## Caption, pinned comment, cover text
```

Script writing rules:
- **Hook in under 2 seconds.** Start in the middle of the action or with a line that creates a question. Never open with a logo, a title card, or "So...".
- **Something changes every 1.5 to 3 seconds**: a new message lands, text animates, the camera moves, a sound plays.
- **Show, don't tell.** The audience reads the chat where the manager takes credit; the narrator says how it felt.
- **Specific beats general.** "My PR had 412 lines. He changed one variable name and presented it as his." beats "He stole my work."
- **Emotional range across the season**: injustice, humiliation, doubt, loneliness, small wins, betrayal, grief, resolve, vindication. Do not stay angry for 20 episodes.
- **Voiceover sounds spoken, not written**: short sentences, contractions, plain words.
- **Copy rules**: No em dashes anywhere. No AI-sounding filler ("in today's fast-paced world", "let's dive in", "game-changer", "unlock", "delve"). Run every script through a slop check before marking it done.
- **No engagement bait.** Do not write "comment PART 2", "like if you agree", or "share this to 3 friends." Platforms down-rank it. Earn comments with a real question or a moral dilemma.

---

## 7. Phase 4: Visual system and HyperFrames build

### 7a. Project structure

```
corporate-ai-reels/
  vendor/hyperframes/          # cloned repo, untouched
  docs/
    hyperframes-notes.md
    algorithm-notes.md
    publishing-guide.md
    production-runbook.md
  story/
    bible.md
    season-1-outline.md
    episodes/ep-01.md ... ep-20.md
  design/
    tokens.css                 # colors, type, spacing, motion timings
    components/                # reusable HTML/CSS/JS components
  episodes/
    ep-01/
      composition.html
      script.json              # beats, timings, artifact data
      audio/vo.wav             # creator's voice (placeholder until recorded)
      out/ep-01.mp4
  audio/
    sfx/                       # licensed or self-made sound effects
    music/                     # licensed music only, with license files
  tools/
    new-episode.*              # scaffolds an episode from its script
    render-all.*               # renders every episode
    qa-check.*                 # automated QA (see 7e)
```

### 7b. Output spec

- 1080 x 1920, 9:16, 30 fps (60 fps only if HyperFrames handles it cleanly), H.264 MP4, AAC audio, loudness around -14 LUFS integrated.
- Burned-in captions on every spoken line. Most people watch with the sound off at first.
- **Safe zones:** keep all important text out of the bottom ~20% (caption and username overlay), the right ~15% (like, comment, share buttons), and the top ~10%. Build these as a debug overlay you can toggle.

### 7c. Design tokens

- A dark, slightly cinematic base with one accent color that means "the protagonist" and one that means "power or threat."
- Two typefaces at most: one UI-style sans for artifacts, one bold display face for hooks and Law cards. Use only fonts with licenses that allow commercial video use.
- Motion timings in tokens (for example, message-in 180ms, card-slam 250ms, hold-for-reading 1.2s per 10 words).

### 7d. Reusable components (all invented UI, no real brand look-alikes)

Build each as a parameterized component driven by `script.json`:

- `ChatThread`: messages arriving one by one with typing indicator, reactions, edits, "message deleted."
- `EmailView`: subject, sender, CC list (CC drama is a storytelling tool), body reveal.
- `CodeDiff`: red and green lines, a reviewer comment appearing, a blame line flipping names.
- `Terminal`: commands typing, build failing or passing.
- `CalendarInvite`: the ominous "Quick sync" with no agenda, HR added as optional.
- `PerfReview`: ratings changing, comments being rewritten.
- `OrgChart`: boxes moving, a name greyed out.
- `Notification`: phone-style push that interrupts a scene.
- `LawCard`: the Law number and name slamming in, with one plain-English line.
- `HookText`: big kinetic first-2-seconds text.
- `EndCard`: cliffhanger line plus "Part X" label. No begging for follows.
- `Recap`: 3-second "Previously" strip for episodes 2 and up, skippable by design.

### 7e. Build, render, and QA

1. Write `tools/new-episode` to turn `story/episodes/ep-XX.md` beats into `episodes/ep-XX/script.json` and a composition.
2. Until the creator records the real voiceover, generate placeholder timing audio and label it clearly as placeholder.
3. Render every episode. Then run `tools/qa-check` and fix every failure:
   - Duration within 45 to 75 seconds.
   - Hook text visible by frame 1 (no black or empty first frame).
   - No text inside unsafe zones.
   - Every spoken line has a caption on screen while it is spoken.
   - Reading time: no on-screen block disappears before about 1.2 seconds per 10 words.
   - Audio peak below -1 dBTP, loudness near -14 LUFS.
   - No em dashes in any on-screen text or caption.
   - No real company, person, or brand names in the fiction.
4. Render a 1-frame cover image per episode from a strong frame, with the episode title readable at thumbnail size.

---

## 8. Phase 5: Emotional engagement playbook

Write `docs/engagement-playbook.md` and apply it to every script. Cover:

- **Open loops:** raise a question early, answer it late or in the next episode.
- **Stakes the viewer can feel:** rent, a visa, a parent's opinion, a promise to a partner. Corporate stakes alone are abstract.
- **Injustice, then agency:** viewers stay for unfairness but return for the comeback. Never stay in pure victimhood for more than 2 episodes in a row.
- **Vulnerability in narration:** admit doubt, fear, and his own mistakes. Viewers trust a narrator who admits being wrong.
- **Recognition moments:** details every tech worker has lived (the meeting that should have been an email, the AI-generated doc nobody read, the reorg announced at 4:55pm on a Friday). These are what get shared.
- **Dilemmas that invite comments:** end some episodes on a choice ("Would you have signed it?") instead of a twist.
- **Rhythm:** tension, release, tension. Put one small win in every episode, even in the darkest stretch.
- **Payoff discipline:** every setup planted must pay off. Track setups and payoffs in a table.

---

## 9. Phase 6: How the platforms rank short video (verify in Phase 0b)

These are commonly cited signals as of 2025 to 2026. Treat them as working assumptions, check the latest official statements, and correct this section where needed. No one outside these companies knows the algorithms "perfectly," so build a measurement loop rather than trusting any single claim.

**Instagram Reels**
- Watch time and whether people watch to the end and rewatch.
- **Sends per reach** (shares through DMs) is described by Instagram as one of the strongest signals for reaching new, non-follower audiences. Write moments people want to send to a coworker.
- Likes per reach and saves matter more for reaching existing followers.
- Original content is favored. Reposted or watermarked content (for example a TikTok logo) is down-ranked, so export clean files for each platform.
- Use **Trial Reels** (shows a reel to non-followers first) to test hooks when available.
- Follow current rules for labeling AI-generated content.

**TikTok**
- Completion rate, rewatches, shares, and how quickly early viewers engage.
- Searchable on-screen text and captions help discovery. Use clear keywords ("corporate", "software engineer", "office politics", "48 laws of power").

**YouTube Shorts**
- "Viewed vs swiped away" in the first seconds is the key early metric.
- Shorts can lead people to a full series playlist. Add every episode to a "Season 1" playlist in order.

**Implications built into this project**
- The first 2 seconds decide distribution. Write 3 alternative hooks for every episode and A/B test them with Trial Reels when possible.
- A series needs to work for someone who lands on Part 11 first, so each episode needs a short "Previously" line and a Law that works as a standalone takeaway.
- A rewatch is more likely when the final second connects back to the first frame (a seamless loop) or when there is a detail worth rewinding for.

---

## 10. Phase 7: Publishing package

Write `docs/publishing-guide.md` and, for every episode, `episodes/ep-XX/publish.md` containing:

- Caption (first line is a hook, under 125 characters before the "more" cut).
- 3 to 5 relevant hashtags, not 30.
- On-screen keywords and title text for search.
- Pinned comment (a question or dilemma, not "Part 2 coming soon").
- Cover image and cover text.
- Suggested posting time window (to be replaced by the account's own Insights data after week 2).
- Clean exports for each platform without watermarks.
- Playlist or series assignment for each platform.

---

## 11. Phase 8: Production runbook and measurement loop

Write `docs/production-runbook.md` that the creator can follow every week without help:

1. Record the voiceover for the next 3 episodes in one session (setup guide: quiet room, phone or USB mic, how to export).
2. Drop the files into `episodes/ep-XX/audio/vo.wav`, run the retime and render commands, run QA.
3. Review, tweak, publish on schedule.
4. Every Sunday, log for each episode: 3-second hold rate, average watch percentage, completion rate, shares, saves, comments, follows gained, and non-follower reach. Keep this in `analytics/weekly-log.csv`.
5. Every 2 weeks: find the top 2 and bottom 2 episodes, write down why, and adjust hooks, pacing, or length for the next batch. Do not change more than one major variable at a time.

---

## 12. Guardrails

- Fiction only. No real companies, products, people, logos, or recognizable UI trade dress.
- Do not present the story as true.
- Do not glamorize harassment, discrimination, or illegal acts. The antagonists can be ruthless; the show must not endorse cruelty.
- Follow each platform's AI-content disclosure rules.
- Only use music, sound effects, and fonts with licenses that allow this use. Keep license files next to the assets.
- No em dashes and no AI-slop phrasing in any copy, script, caption, or on-screen text.

---

## 13. Definition of done

- [ ] `docs/hyperframes-notes.md` written from the actual repo, and a repo example rendered successfully.
- [ ] `docs/algorithm-notes.md` with dated sources.
- [ ] Story bible and 20-episode outline complete, with a setup and payoff table.
- [ ] All 20 scripts written in the template, each with 3 alternative hooks.
- [ ] Design tokens and all components built and reusable.
- [ ] Episodes 1 to 3 fully rendered with placeholder audio, passing every QA check.
- [ ] `tools/new-episode`, `tools/render-all`, and `tools/qa-check` working.
- [ ] Publishing package for episodes 1 to 3.
- [ ] Production runbook a non-technical person can follow.
- [ ] A short summary listing anything you could not verify or could not get working, with the exact error.

When you finish, report what was built, what was verified, and what still needs the creator (mainly: recording the voiceover and approving the series title).
