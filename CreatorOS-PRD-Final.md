# CreatorOS — Final Product Requirements Document (PRD)
**Version:** 1.0 FINAL  
**Status:** Ready for Design & Engineering  
**Last Consolidated:** June 2026  
**Classification:** Founder + Team Internal

---

## DOCUMENT PURPOSE

This PRD consolidates three vision documents, two architecture specifications, six UI builds, and all feature analyses produced across the CreatorOS design sprint into a single authoritative source of truth. Duplicates removed. Contradictions resolved. All feature decisions final and justified.

**This document is the handoff artifact for:**
- Product designers (Figma specs, component inventory)
- Frontend engineers (Next.js implementation)
- Backend engineers (API + DB + queue systems)
- AI engineers (prompt strategy + model routing)
- Founders (investor narrative + roadmap)

---

## PART 1 — PRODUCT DEFINITION

### 1.1 Product Name & Tagline
**Product:** CreatorOS  
**Tagline:** *"Paste an idea. Get a YouTube video."*  
**Category:** AI Creator Operating System  
**Position:** The Canva + CapCut + ChatGPT + VidIQ for YouTube creators — unified.

### 1.2 The Single Mission Statement
Help anyone create a high-quality, publishable YouTube video in under 15 minutes — with zero editing skill, zero equipment, and zero team.

### 1.3 The 14-Year-Old Test (Non-Negotiable UX Constraint)
*"If a 14-year-old beginner opens CreatorOS for the first time, can they create a professional YouTube video without any tutorials?"*

Every feature decision, UX flow, and copy choice must pass this test. If it adds friction for a beginner, it either moves to Advanced Mode or is cut.

### 1.4 Core Promise (Resolved — Final Version)
Previous documents had slight variations. This is canonical:

> **"Paste an idea or a YouTube link. Get a script, scenes, voiceover, edited video, thumbnail, and SEO package — in under 15 minutes. Completely original. Ready to upload."**

### 1.5 Target Audience (Priority Order)
1. **Complete beginners** — never made a YouTube video, don't know where to start
2. **Faceless channel creators** — want income without showing their face
3. **Hindi/Hinglish creators** — massively underserved by existing English-first tools
4. **Shorts creators** — optimizing for the algorithm's fastest growth path
5. **Cartoon/animated creators** — AI-generated character-driven content
6. **Educational creators** — facts, documentaries, explainers
7. **Agencies/power users** — managing multiple channels

---

## PART 2 — FEATURE INVENTORY (FINAL, DEDUPLICATED)

### 2.1 Feature Priority Matrix

| Feature | MVP | Phase 2 | Phase 3 | Enterprise | Decision Rationale |
|---|---|---|---|---|---|
| Beginner Magic Mode | ✅ | — | — | — | Highest conversion driver; chains all modules |
| AI Script Studio | ✅ | — | — | — | Core value; all 12 styles from day 1 |
| Hook Generator | ✅ | — | — | — | Low complexity, high retention impact |
| Scene Creator AI | ✅ | — | — | — | Bridges script→visual gap for beginners |
| Prompt Generator | ✅ | — | — | — | Low effort, high value for external AI tools |
| Voice Studio (EN) | ✅ | — | — | — | ElevenLabs integration |
| Voice Studio (HI/Hinglish) | ✅ | — | — | — | Azure Neural; core differentiator |
| YouTube SEO Studio | ✅ | — | — | — | Full package from day 1 |
| Thumbnail AI (template) | ✅ | — | — | — | Canvas-based templates; no image gen required |
| Shorts Creator Mode | ✅ | — | — | — | Reuses pipeline with format constraints |
| Auto Editor AI (preset) | ✅ | — | — | — | FFmpeg preset-based; no AI decisions needed in MVP |
| Basic Content Planner | ✅ | — | — | — | Calendar + static ideas; trend API in Phase 2 |
| Viral Blueprint AI | — | ✅ | — | — | YouTube API quota complexity; Phase 2 |
| A/B Thumbnail Variants | — | ✅ | — | — | Requires image generation layer |
| Character Studio (basic) | — | ✅ | — | — | Prompt-seed approach first |
| Character Studio (advanced) | — | — | ✅ | — | IPAdapter consistency; GPU-intensive |
| Content Planner + Trends | — | ✅ | — | — | Google Trends API integration |
| Direct YouTube Upload | — | ✅ | — | — | OAuth scope management |
| Brand Voice Memory | — | ✅ | — | — | Requires 3+ video history to activate |
| 4K Export Pipeline | — | — | ✅ | — | Studio plan only |
| Team Collaboration | — | ✅ | — | — | Studio plan, 3 seats |
| API Access | — | — | ✅ | — | Beta access for Studio plan |
| White-Label Exports | — | — | ✅ | — | Agency demand |
| Custom Voice Cloning | — | — | — | ✅ | Enterprise only |
| Bulk Video Generation | — | — | — | ✅ | Enterprise only |
| Agency Dashboard | — | — | — | ✅ | Multi-account management |
| Custom LLM Fine-tuning | — | — | — | ✅ | Per-channel model personalization |

### 2.2 Features REMOVED From Scope (With Reasons)
The following appeared in early drafts and are formally excluded:

| Removed Feature | Reason |
|---|---|
| Real-time collaboration editing | Too complex for MVP; team collab is view/comment only |
| YouTube Analytics Dashboard | Requires YouTube channel auth; Phase 3 at earliest |
| In-app video trimming | Replaced by Auto Editor AI; manual trimming contradicts zero-skill promise |
| Stock footage library | Licensing complexity + cost; use AI images instead |
| Text-to-video direct generation | Phase 3 when Runway/Kling APIs mature enough for reliable quality |
| Community/social features | Not core to creation pipeline; distraction in MVP |
| Browser extension | Engineering overhead; lower priority than pipeline completion |

---

## PART 3 — MODULE SPECIFICATIONS (FINAL)

### Module 1: Beginner Magic Mode
**Purpose:** Remove all decision paralysis for new creators. Chain all modules automatically.  
**Inputs:** 5 questions maximum (topic, style, language, format, optional inspiration URL)  
**Outputs:** Complete video project with all steps pre-generated  
**User Flow:** Landing CTA → 5 questions (2 min) → AI runs full pipeline → Review + Export  
**Technical:** Orchestration service chains: analyze → script → scenes → prompts → voice → thumbnail → SEO → render queue  
**UX Rules:**
- Never more than 5 questions
- Real-time streaming status (never blank loading)
- Autosave after every step completes
- Resume from any step if session interrupted
- Mobile-responsive form

**Error Handling:**
- Inspiration URL invalid → Skip analysis, proceed with topic only
- Voice generation fails → Retry once, then offer alternative voice
- Render queue full → Notify via email, show queue position

---

### Module 2: AI Script Studio
**Purpose:** Generate structured, retention-optimized scripts for 12 video types  
**Inputs:** topic, video_type, language, tone, target_length_seconds, niche, hook_type  
**Outputs:** JSON `{hook, intro, body[], emotional_beats[], cta, outro, retention_tips[], engagement_score, word_count, estimated_duration}`

**12 Supported Video Types (Final List):**
1. Faceless / Facts
2. Horror Story
3. Motivational
4. Educational / Explainer
5. Documentary Style
6. Cartoon Story
7. Comparison / Versus
8. AI Avatar Presenter
9. Shorts / Reels
10. Kids Content
11. True Crime
12. Finance / Wealth

**AI Model:** Claude Sonnet (Anthropic) — best narrative structure quality  
**Validation Rules:**
- Hook must be ≤ 35 words
- CTA must be present (auto-insert if missing)
- Estimated duration must be within 15% of target
- Retry once on validation failure, then surface to user

**Quality Gates:**
- Engagement score < 60 → Automatically suggest regeneration
- For educational/facts content → Add disclaimer: "Verify factual claims before publishing"
- Brand voice applied after 3+ videos created in same niche

---

### Module 3: Hook Generator
**Purpose:** Generate high-retention first 3-second openers  
**Inputs:** topic, video_type, count (default 7)  
**Outputs:** 7 hook types × 3 variants = 21 hooks per session

**7 Hook Types (Final — Resolved from conflicting earlier lists):**
1. Curiosity Gap ("What if I told you...")
2. Shocking Fact (specific statistic opener)
3. Story Hook (mid-scene drop)
4. Question Hook (direct viewer address)
5. Controversial Statement
6. Problem-Solution Promise
7. Trend/Timely Hook

**Rating System:** User can rate hooks (👍/👎) to improve future outputs  
**AI Model:** GPT-4o-mini (cost-efficient for structured generation)

---

### Module 4: Scene Creator AI
**Purpose:** Convert script into shot-by-shot visual production plan  
**Inputs:** script_id, video_type, scene_count (default: auto-calculated from script duration)  
**Outputs per scene:** `{number, duration_sec, visual_desc, camera_angle, motion, mood, background, transition, sfx_idea, ai_image_prompt, ai_video_prompt}`

**Scene Constraints:**
- Short videos (≤ 60s): 4–8 scenes, 8–15s each
- Medium videos (3–8 min): 10–20 scenes, 15–30s each
- Long videos (8–20 min): 20–40 scenes, 20–45s each

**UX:** Drag-to-reorder scenes. Each scene card expandable. Inline edit of any field.

---

### Module 5: Prompt Generator
**Purpose:** Generate AI-tool-ready image/video prompts per scene  
**Inputs:** scene_id, style_preset, target_tool  
**Output per prompt:** `{image_prompt, video_prompt, negative_prompt, style_tags, quality_modifiers}`

**6 Style Presets (Final):**
1. Cinematic Realistic
2. 3D Pixar-Style
3. Anime / Manga
4. Horror / Dark
5. Documentary / Photorealistic
6. Cartoon Flat

**Tool Presets:** Midjourney v7, Runway Gen-3, Kling 1.6, Flux.1-dev, DALL-E 3  
**Each preset adjusts:** syntax, aspect ratio flags, quality tags, model-specific tokens

---

### Module 6: Voice Studio
**Purpose:** Convert script to production-quality voiceover  
**Inputs:** script_id, voice_id, language, emotion, speed, emotion_intensity, pause_timing  
**Outputs:** `{audio_url, duration_sec, segments[{text, start_ms, end_ms}]}`

**Voice Options (Final — Resolved conflict between 4 and 6 voice types):**

| Voice | Language | Provider | Character |
|---|---|---|---|
| Marcus | English | ElevenLabs | Deep, cinematic, authoritative |
| Aria | English | ElevenLabs | Clear, warm, engaging |
| James | English | ElevenLabs | Young, energetic narrator |
| Rohan | Hindi | Azure Neural | hi-IN-MadhurNeural — warm, natural |
| Priya | Hindi | Azure Neural | hi-IN-SwaraNeural — clear, professional |
| Arjun | Hinglish | Azure Neural | Code-switching, youthful |

**SSML Controls:** Speed (0.75x–1.5x), pause timing (tight/normal/dramatic), emotion intensity (0–100)  
**Segment-level regeneration:** User can re-generate any individual sentence  
**Preview before commit:** All voices pre-playable with sample text

---

### Module 7: Auto Editor AI
**Purpose:** Assemble all assets into export-ready video automatically  
**Inputs:** project_id, resolution, include_captions (bool), music_mood  
**Output:** Render job → MP4 file URL

**Render Pipeline (Final Sequence):**
```
1. Asset validation (all scene images/clips + voice audio exist)
2. Per-scene: Ken Burns zoom (scale 1.0→1.08 over duration)
3. Caption SRT generation from voice segments
4. Background music selection (mood-matched from licensed library)
5. Audio mix: voice (-16 LUFS) + music (-24 LUFS, duck to -35 during voice)
6. FFmpeg assembly: concat scenes + burn captions + overlay audio
7. Transitions between scenes (type from scene.transition_type)
8. Color grade: contrast +5%, saturation +3%
9. Watermark (free plan) or clean (paid)
10. H.264 encode → MP4 → R2 upload → signed URL
```

**Render Time Targets:**
- Shorts (≤ 60s): < 90 seconds
- Medium (3–8 min): < 5 minutes
- Long (8–20 min): < 15 minutes
- Priority queue (Studio plan): 40% faster

**FFmpeg Stack:** fluent-ffmpeg wrapper, worker pool 3–10 instances, BullMQ jobs

---

### Module 8: Thumbnail AI
**MVP:** Template-based canvas composition (no image generation)  
**Phase 2:** AI-generated thumbnail with face integration

**MVP Inputs:** project_id, text_top, text_main, color_scheme, layout_style  
**MVP Outputs:** `{image_url, ctr_score, layout, variant}` — A/B variants

**5 Layout Templates (MVP):**
1. Text Center — Dark Background (best for faceless)
2. Text Left — Visual Right (facts/educational)
3. Full Bleed — Text Overlay (horror/cinematic)
4. Split Screen — Two Panels (comparison)
5. Number Dominant — Large numeral focus (listicle)

**CTR Score:** Heuristic 1–100 based on: contrast ratio, text length, number presence, niche benchmarks. Always labeled as "Estimated CTR Score."

---

### Module 9: YouTube SEO Studio
**Purpose:** Generate complete SEO package for YouTube upload  
**Inputs:** project_id, target_keyword (optional)  
**Outputs:** `{seo_title, ctr_title, description, hashtags[], tags[], keywords[], seo_score, checklist[], chapters[]}`

**SEO Score Breakdown (100 points):**
- Title includes primary keyword: 20pts
- Description ≥ 300 chars: 15pts
- Description has chapters: 10pts
- Tags 10+: 15pts
- Hashtags 3–8: 10pts
- First 100 chars of description have keyword: 15pts
- CTA in description: 10pts
- Keyword in first tag: 5pts

**Upload Checklist:** 12 items covering title, description, thumbnail, tags, chapters, end screen, cards, category, captions.

---

### Module 10: Viral Blueprint AI (Phase 2)
**Purpose:** Analyze viral YouTube videos and generate transformed original direction  
**Legal Rule:** NEVER store or reproduce verbatim transcript content. All outputs are patterns + transformations, never content.

**Analysis Pipeline:**
1. Extract video ID from URL
2. YouTube Data API v3: metadata (title, description, view count, duration, tags)
3. youtube-transcript-api: auto-captions (if available)
4. Claude Sonnet analysis: extract 10 pattern signals
5. Generate transformation brief: different topic, same psychological framework
6. Return analysis object + confidence score

**10 Pattern Signals:**
hook_type, pacing_grade, emotional_arc, story_structure, cta_style, scene_rhythm, caption_style, thumbnail_formula, retention_peak_timing, audience_appeal_mechanism

**Confidence Score:** 1–100 indicating how different generated content is from source (must be ≥ 85 to display without warning)

**Fallback:** Private/deleted videos → Title/description-only analysis with lower confidence score

---

### Module 11: Shorts Creator Mode
**Purpose:** Optimized pipeline for 15–60s vertical video  
**Format:** 9:16 aspect ratio (1080×1920)  
**Lengths:** 15s / 30s / 45s / 60s

**Differences from Long-Form Pipeline:**
- Script: Hook in first 2 seconds (not 3), no intro, direct value delivery
- Scenes: 3–6 scenes maximum, 8–12s each
- Voice: Speed default 1.1x, no dramatic pauses
- Edit: Hard cuts preferred over dissolves, captions always on, no end card
- Loop ending: Final frame designed to connect back to first frame
- Export: 1080×1920, MP4, < 60s for Shorts algorithm

**Repurpose Flow:** Long video → select segment → auto-crop to 9:16 → add Shorts captions → export (Phase 2)

---

### Module 12: Character Studio
**MVP (available in Studio plan):** Prompt-seed consistency approach  
**Phase 2:** IPAdapter-style visual consistency  
**Phase 3:** Custom LoRA training per character

**Character Schema:**
```
name, age_range, visual_style, skin_tone, hair_style, hair_color,
outfit_style, outfit_color, facial_features, personality,
base_prompt, negative_prompt, style_seed, expression_library{}
```

**Expression Library (8 expressions):** Default, Happy, Shocked, Thinking, Sad, Angry, Excited, Laughing

**Consistency Seed:** A hash string combining all character attributes, used as reference prompt suffix in all scene image generation.

**Wardrobe Memory:** Characters remember their outfit across scenes unless explicitly changed.

---

### Module 13: Content Planner
**MVP:** Monthly calendar + AI idea generation (static niche-based)  
**Phase 2:** Google Trends integration + series arc planning

**Calendar Features:** Add/edit/delete video slots. Status: idea/draft/scheduled/published. Link to project.

**AI Idea Engine:** 
- Inputs: niche, channel_history (past titles)
- Outputs: 10 ideas/request with heat score (🔥 Trending / ⚡ Rising / 📊 Steady)
- Refresh: Weekly trend update via YouTube trending API

**Series Builder:** Define a series name + episode structure → AI generates N episode titles and briefs

---

## PART 4 — FINAL TECHNICAL STACK (RESOLVED)

### Contradiction Resolution
Earlier documents listed both Hono.js and Express as backend frameworks. **Final decision: Hono.js** — Edge-compatible, TypeScript-native, faster cold starts on Railway.

Earlier documents mentioned both Drizzle ORM and Prisma. **Final decision: Drizzle ORM** — Lighter, better TypeScript inference, no shadow database requirement.

### Definitive Stack

**Frontend**
```
Framework:      Next.js 14 (App Router, RSC)
Language:       TypeScript 5.x
Styling:        Tailwind CSS 3.x
Components:     shadcn/ui + Radix UI primitives
State:          Zustand (client) + TanStack Query v5 (server)
Animation:      Framer Motion 11
Drag/Drop:      @dnd-kit/core
Rich Text:      Tiptap 2.x (script editor)
Video Player:   Plyr.js
Audio Viz:      WaveSurfer.js
Charts:         Recharts
Deployment:     Vercel (Edge Network)
```

**Backend**
```
Runtime:        Node.js 20 LTS + TypeScript
Framework:      Hono.js (edge-compatible API router)
ORM:            Drizzle ORM
Database:       PostgreSQL via Supabase
Cache/Queue:    Upstash Redis + BullMQ
Auth:           NextAuth.js v5 + Supabase Auth
Payments:       Stripe (subscriptions + webhooks)
Email:          Resend
File Storage:   Cloudflare R2 (S3-compatible)
Video Render:   FFmpeg via fluent-ffmpeg, Railway worker pool
Real-time:      WebSocket (render progress, autosave events)
Monitoring:     Sentry (errors) + PostHog (analytics)
CI/CD:          GitHub Actions → Vercel + Railway
```

**AI Services**
```
Script/SEO/Hook/Analysis:  Anthropic Claude Sonnet 4
Scene/Prompt:              OpenAI GPT-4o-mini (cost tier)
Voice EN:                  ElevenLabs Multilingual v2
Voice HI/Hinglish:         Azure Cognitive Services TTS (hi-IN)
Images (Phase 2):          Replicate API (Flux.1-dev)
Video Analysis:            YouTube Data API v3
Transcripts:               youtube-transcript-api (npm)
Keywords (Phase 2):        Google Trends API via RapidAPI
Vector DB (Phase 2):       Pinecone (character embeddings)
```

**Infrastructure**
```
Frontend hosting:    Vercel Pro
Backend API:         Railway (autoscaling)
FFmpeg workers:      Railway (3–10 instances, auto-scale)
Database:            Supabase (Postgres + Auth + Realtime)
Cache + Queues:      Upstash Redis (serverless)
File Storage:        Cloudflare R2
CDN:                 Cloudflare
Secrets:             Vercel Environment Variables
```

---

## PART 5 — DATABASE SCHEMA (FINAL CANONICAL)

*Supersedes all previous schema versions. All table and column name conflicts resolved.*

### Schema Decisions (Resolved Contradictions)
- `users.plan` ENUM: `['free','creator','studio','enterprise']` (not 'pro' — internal consistency)
- `projects.status` ENUM: `['draft','generating','ready','exported','archived']`
- `exports.resolution` ENUM: `['720p','1080p','4k']` (lowercase — matches FFmpeg convention)
- Character table: in main schema (not separate schema) — simplifies joins
- Voice outputs: segments stored as JSONB on `voice_outputs` table (not separate table)

**All 13 tables:** users, projects, project_versions, scripts, scenes, voice_outputs, thumbnails, seo_outputs, exports, characters, content_plans, subscriptions, analytics_events

*(Full DDL in `creatorOS-blueprint.md` — referenced, not repeated here)*

---

## PART 6 — API SURFACE (FINAL CANONICAL)

### Base URL
`https://api.creatoros.ai/v1`

### Authentication
All endpoints require `Authorization: Bearer {jwt}` except `/auth/*`

### Endpoint Groups (Final — Deduplicated)
```
/auth          → register, login, logout, me, refresh, reset-password
/projects      → CRUD, autosave, versions, restore, duplicate
/generate      → analyze, script, hooks, scenes, prompts, voice, thumbnail, seo, magic
/render        → POST (queue), GET :jobId (status), DELETE (cancel)
/export        → POST (initiate), GET :id (download URL)
/subscription  → GET, checkout, portal, webhook
/credits       → GET balance, consume (internal)
/planner       → CRUD calendar events, GET ideas, GET trends
/characters    → CRUD characters, lock, get-seed
/analytics     → track event (internal)
```

### WebSocket Events (Real-time)
```
render:progress  → {jobId, pct, step, eta_seconds}
render:complete  → {jobId, file_url, duration}
render:error     → {jobId, message, retry_available}
autosave:saved   → {project_id, version, saved_at}
```

---

## PART 7 — PRICING (FINAL — Resolved All Contradictions)

### Final Plan Names
*Earlier versions used "Pro/Studio/Enterprise" and "Creator/Studio/Enterprise" inconsistently. Final decision:*

| Internal ID | Display Name | Monthly | Annual (÷12) |
|---|---|---|---|
| `free` | Starter | $0 | $0 |
| `creator` | Creator Pro | $19 | $13 |
| `studio` | Studio | $49 | $34 |
| `enterprise` | Enterprise | Custom ($299+) | Custom |

### Plan Limits (Final — All Contradictions Resolved)

| Limit | Starter | Creator Pro | Studio |
|---|---|---|---|
| Projects/month | 3 | Unlimited | Unlimited |
| Max export length | 1 minute | 20 minutes | Unlimited |
| Export resolution | 720p | 1080p | 4K |
| Watermark | Yes | No | No |
| Voice Studio | No | EN + HI + Hinglish | EN + HI + Hinglish |
| Auto Editor AI | No | Yes | Yes |
| Viral Blueprint AI | No | Yes | Yes |
| Thumbnail AI | No | Yes (A/B) | Yes (A/B/C) |
| Script styles | 3 | 12 | 12 + Custom |
| Scene Creator | 5 scenes | Unlimited | Unlimited |
| Character Studio | No | No | Yes |
| Content Planner | Basic | Standard | + Trend alerts |
| Team seats | 1 | 1 | 3 |
| Render priority | Low | Standard | Priority |
| Export file storage | 30 days | 1 year | 1 year |
| API access | No | No | Beta |
| White-label | No | No | Yes |
| Support | Community | Email | Priority + Call |

### Additional Revenue (Resolved — Credit Top-Up Prices)
- $5 for 25 render credits (casual users)
- $10 for 60 render credits (better value)
- Lifetime deal: $199 (capped 1,000 users, launch only)
- Affiliate: 30% recurring for 12 months

---

## PART 8 — UX SYSTEM (FINAL)

### Design Tokens (Canonical)
```css
/* Background Layers */
--bg-void:    #03030A;   /* page background */
--bg-surface: #080812;   /* primary surface */
--bg-raised:  #0D0D1A;   /* elevated panels */
--bg-card:    #111120;   /* card background */
--bg-hover:   #1A1A35;   /* hover state */

/* Accent Colors */
--accent-violet: #8B5CF6;  /* primary brand */
--accent-teal:   #06B6D4;  /* secondary accent */
--accent-orange: #F97316;  /* CTA / conversion */
--accent-green:  #10B981;  /* success / confirmation */
--accent-rose:   #F43F5E;  /* error / hot / viral */
--accent-amber:  #F59E0B;  /* warning / scheduled */

/* Text */
--text-primary: #EEEEFF;
--text-muted:   rgba(238,238,255,0.50);
--text-faint:   rgba(238,238,255,0.20);
--text-ghost:   rgba(238,238,255,0.08);

/* Borders */
--border-subtle:  rgba(238,238,255,0.07);
--border-visible: rgba(139,92,246,0.15);
--border-accent:  rgba(139,92,246,0.30);

/* Typography */
--font-display: 'Syne', sans-serif;       /* headlines, logos */
--font-body:    'Inter', sans-serif;      /* all body text */
--font-mono:    'JetBrains Mono', mono;   /* labels, data, code */

/* Border Radius */
--radius-sm: 6px;
--radius-md: 10px;
--radius-lg: 16px;
--radius-xl: 24px;

/* Shadows / Glows */
--glow-violet: 0 0 40px rgba(139,92,246,0.25);
--glow-teal:   0 0 30px rgba(6,182,212,0.20);
--glow-orange: 0 0 32px rgba(249,115,22,0.30);
```

### Typography Scale
```
Display XL:  Syne 800, clamp(48px,7vw,92px), -3px tracking
Display LG:  Syne 800, clamp(36px,5vw,64px), -2px tracking
Display MD:  Syne 700, clamp(24px,3vw,40px), -1px tracking
Display SM:  Syne 700, 20px, -0.5px tracking
Body LG:     Inter 400, 18px, 1.75 line-height
Body MD:     Inter 400, 15px, 1.70 line-height
Body SM:     Inter 400, 13px, 1.60 line-height
Label:       JetBrains Mono 500, 11px, 0.10em letter-spacing, UPPERCASE
```

### Component Library (Required for MVP)

**Buttons:** Primary (orange CTA), Violet (standard action), Ghost (secondary), Teal (tool action), Danger (destructive)  
**Cards:** Panel card, Bento card, Highlight card, Workflow card  
**Forms:** Input, Select, Textarea, Chip toggle, Range slider  
**Feedback:** Toast notification, Progress bar, Loading shimmer, Empty state  
**Navigation:** Topbar, Sidebar, Pipeline header, Breadcrumb  
**Data:** Score ring, Analysis bar, Waveform, Calendar grid  
**Modals:** Upgrade wall, Confirmation dialog, Export options  

### Microcopy Standards (Final)
| Context | Copy | Reason |
|---|---|---|
| Script generating | "Writing your hook — the most important 3 seconds." | Specific, not generic |
| Voice generating | "Turning your script into a voice…" | Simple, clear |
| Render queued | "Your video is being assembled. We'll notify you." | Sets expectation |
| Export ready | "Ready to download. Link valid for 30 days." | Actionable, time-bound |
| Free limit hit | "This video is 2:14. Upgrade to export videos over 1 minute." | Specific, not pushy |
| Empty dashboard | "Your studio is empty. Start your first video — 5 questions." | Invitation, not sad |
| Autosaved | "Saved · just now" (ambient, never intrusive) | Confirms safety |
| Error: private URL | "This video is private. Try a different public YouTube link." | Tells the fix |
| Factual content warning | "This script makes factual claims. Verify before publishing." | Responsible |

---

## PART 9 — USER FLOWS (CANONICAL)

### Flow 1: Magic Mode (Primary Acquisition Flow)
```
Landing page CTA
    ↓
Magic Mode form (5 questions, ~2 min)
    ↓
[IF inspiration URL provided] → Viral Blueprint analysis (~45s)
    ↓
Script generation (streaming, ~60s)
    ↓
Scene plan generation (~30s)
    ↓
Voice generation (async, ~90s)
    ↓
Thumbnail generation (~20s)
    ↓
SEO package generation (~15s)
    ↓
Auto Editor render queued (3–15 min async)
    ↓
User reviews: script / scenes / voice / thumbnail / SEO
    ↓
Export download → YouTube upload → DONE
```

### Flow 2: Power User (Step-by-Step)
```
Dashboard → New Project
    ↓
Optional: Viral Blueprint analysis
    ↓
Script Studio → Generate / Edit / Approve
    ↓
Scene Creator → Generate / Reorder / Edit
    ↓
Prompt Generator → Copy for external AI tools
    ↓
Voice Studio → Select voice / Generate / Preview / Approve
    ↓
Auto Editor → Select preset → Queue render
    ↓
Thumbnail AI → Generate / A-B compare / Select
    ↓
SEO Studio → Review / Edit / Copy to YouTube
    ↓
Export → Download
```

### Flow 3: Upgrade Flow
```
[Trigger: export length > 1 min OR watermark removal OR advanced feature click]
    ↓
Upgrade wall → Shows locked feature blurred
    ↓
"Upgrade to Creator Pro for $19/mo — unlock this in 30 seconds"
    ↓
Stripe checkout (pre-filled email)
    ↓
Success → Feature unlocked → Return to interrupted action
```

### Flow 4: Onboarding (New User, Post-Registration)
```
Register (email or Google)
    ↓
6-screen setup: Welcome → Name/Channel → Niche → Style + Language → Goal + Plan → Ready
    ↓
Studio configured → "Your studio is ready"
    ↓
CTA: "Make my first video now →" → Magic Mode
```

---

## PART 10 — SPRINT ROADMAP (FINAL — 8 WEEKS MVP)

### Week 1–2: Foundation
- [ ] Next.js 14 project, Supabase config, TypeScript setup
- [ ] Database schema deployment (all 13 tables)
- [ ] Auth: email + Google OAuth (NextAuth.js v5)
- [ ] Project CRUD + 30-second autosave
- [ ] Dashboard shell + pipeline header + sidebar
- [ ] Topbar with plan badge + user avatar
- [ ] Onboarding flow (6 screens)

### Week 3: Core AI Modules
- [ ] Script Studio API (Anthropic Claude integration)
- [ ] Script Studio UI (all 12 types, retry, engagement score)
- [ ] Hook Generator API + UI (7 types, 21 hooks)
- [ ] Scene Creator API + UI (drag-to-reorder, inline edit)
- [ ] Prompt Generator API + UI (6 presets, tool presets)

### Week 4: Media Modules
- [ ] Voice Studio API (ElevenLabs EN + Azure HI)
- [ ] Voice Studio UI (selector, preview, segment player, settings)
- [ ] Thumbnail AI API (5 canvas templates)
- [ ] Thumbnail AI UI (A/B compare, CTR score, live edit)
- [ ] SEO Studio API + UI (full package, checklist, tags)

### Week 5: Pipeline Orchestration
- [ ] Magic Mode orchestration service (chain all modules)
- [ ] Pipeline step validation (N unlocks N+1)
- [ ] BullMQ + Upstash Redis job queue
- [ ] FFmpeg render pipeline (full spec from Module 7)
- [ ] WebSocket server (render progress, autosave events)

### Week 6: Export + Payments
- [ ] Cloudflare R2 upload + signed URL delivery
- [ ] Export page UI (render progress, options, download)
- [ ] Stripe integration (3 tiers, webhooks)
- [ ] Plan limits enforcement (duration, resolution, watermark)
- [ ] Upgrade modal + Stripe checkout redirect
- [ ] Credit system backend

### Week 7: Shorts + Content + Polish
- [ ] Shorts Creator Mode (format switching, 9:16 export)
- [ ] Content Planner (calendar UI + idea generation)
- [ ] Project page (full pipeline single view)
- [ ] Auto Editor timeline UI (visual scene arrangement)
- [ ] Mobile responsive pass (all pages)
- [ ] Empty states + error states + skeleton loaders

### Week 8: QA + Launch
- [ ] End-to-end pipeline test (Magic Mode → Export)
- [ ] Load test render queue (10 concurrent jobs)
- [ ] Security audit (rate limits, JWT, CSRF, input sanitization)
- [ ] PostHog analytics instrumentation (20 key events)
- [ ] Performance: Lighthouse score ≥ 85 on all pages
- [ ] Beta launch: 200 waitlist users

---

## PART 11 — ANALYTICS EVENTS (MVP INSTRUMENTATION)

### 20 Required Events for Launch

| Event | Properties | Purpose |
|---|---|---|
| `page_viewed` | page, referrer | Funnel analysis |
| `signup_started` | method (email/google) | Auth conversion |
| `signup_completed` | plan, niche | User acquisition |
| `onboarding_completed` | plan_selected, niche, language | Setup quality |
| `magic_mode_started` | style, language, format | Feature adoption |
| `magic_mode_completed` | duration_ms | Pipeline success rate |
| `script_generated` | video_type, language, engagement_score | Quality tracking |
| `voice_generated` | voice_id, language, duration_sec | Voice adoption |
| `render_queued` | resolution, video_length | Render volume |
| `render_completed` | render_time_ms, resolution | Performance |
| `export_downloaded` | plan, resolution, watermarked | Core success event |
| `upgrade_wall_shown` | trigger_feature, current_plan | Conversion trigger |
| `upgrade_clicked` | from_plan, to_plan, trigger | Revenue intent |
| `subscription_created` | plan, billing_interval, amount | Revenue |
| `subscription_canceled` | plan, reason, days_active | Churn |
| `viral_blueprint_used` | video_id_hash (not URL), confidence_score | Feature usage |
| `thumbnail_generated` | variant_count, selected_variant | Adoption |
| `seo_package_generated` | seo_score | Quality |
| `referral_shared` | channel | Viral loop |
| `project_created` | video_type, language, via_magic_mode | Growth |

---

## PART 12 — RISK REGISTER (FINAL — CONSOLIDATED)

| Risk | Severity | Mitigation | Owner |
|---|---|---|---|
| YouTube API quota exhaustion | HIGH | Cache popular analyses 24h; pool quota across users; paid API tier at scale | Backend |
| Copyright claim on AI output | HIGH | Transformation layer (≥85 confidence); legal disclaimer; no verbatim text in output | Legal + AI |
| Render bottleneck at scale | HIGH | BullMQ priority tiers; async UX (never block); auto-scale workers | Infra |
| LLM cost overrun | HIGH | Claude for quality tasks only; GPT-4o-mini for structure tasks; prompt caching; credit gates | AI + Finance |
| Hindi TTS quality complaints | MEDIUM | Azure Neural (best available); per-sentence preview; regeneration UI | Product |
| Character inconsistency (Phase 2) | HIGH | Phase 2 timeline committed; MVP uses prompt-only; set user expectations clearly | Product |
| Free plan GPU abuse | HIGH | Strict queue priority; watermark enforcement; render credit limits | Infra |
| Competitor feature copying | MEDIUM | Channel memory moat; Hindi market; retention science depth not easily replicated | Strategy |
| Stripe chargeback fraud | LOW | Fraud detection; disable exports after chargeback; email verification required | Finance |
| Data loss (no autosave) | HIGH | 30-second autosave to DB; version history (20 versions); resume from any step | Backend |

---

## PART 13 — PAGES & ROUTES (COMPLETE SITE MAP)

### Public Pages
```
/                    → Landing page (vision3-platform.html)
/pricing             → Pricing page with plan comparison
/features            → Feature deep-dive (long-form)
/blog                → Content marketing
/changelog           → Product updates
/privacy             → Privacy policy
/terms               → Terms of service
```

### Auth Pages
```
/auth/login          → Sign in (email + Google)
/auth/register       → Sign up
/auth/onboarding     → 6-screen setup flow
/auth/reset          → Password reset
```

### App Pages (Authenticated)
```
/dashboard           → Project list + quick actions + stats
/projects/new        → New project (or redirect to Magic Mode)
/projects/[id]       → Single project workspace (all pipeline steps)
/projects/[id]/script     → Script Studio
/projects/[id]/scenes     → Scene Creator
/projects/[id]/voice      → Voice Studio
/projects/[id]/editor     → Auto Editor timeline
/projects/[id]/thumbnail  → Thumbnail AI
/projects/[id]/seo        → SEO Studio
/projects/[id]/export     → Export page
/magic               → Beginner Magic Mode
/shorts              → Shorts Creator dedicated mode
/characters          → Character Studio
/planner             → Content Planner (calendar + ideas)
/settings            → Account settings
/settings/billing    → Subscription + usage
/settings/team       → Team members (Studio plan)
```

### Admin Pages (Internal)
```
/admin               → Founder analytics dashboard
/admin/users         → User management
/admin/render-queue  → Queue monitoring
/admin/revenue       → MRR/ARR tracking
```

---

## PART 14 — WHAT MAKES CREATOROS WIN (FINAL ANSWER)

### Why It Beats Every Existing Tool
Every competitor solves one piece. CreatorOS is the only platform where:
1. Every step's output becomes the next step's input — automatically
2. The AI gets smarter about *your channel specifically* over time
3. A 14-year-old with no skills can have a real YouTube channel by tonight
4. Hindi and Hinglish are first-class citizens, not afterthoughts

### What Makes It Unforgettable
Three moments define the product experience:
1. **The First Video Moment** — downloading a complete video 9 minutes after signing up, having never made a video before
2. **The "It Knows Me" Moment** — script #5 sounds like *you*, not a generic AI
3. **The Channel Growth Moment** — first 1,000 subscribers attributed to CreatorOS workflow

### What Makes Creators Pay
- Free plan is genuinely useful (full pipeline, 1-min export) — removes risk
- The moment they want to keep the video (>1 min or watermark removal) → natural upgrade
- $19/mo is one brand deal, one sponsored post, one affiliate sale — trivially justified by results
- Channel memory increases switching cost with every video — compounding retention

### How It Becomes Category-Defining
1. Name and own the category: "AI Creator Operating System"
2. Hindi market: 500M+ users, zero world-class tools — instant #1 in that market
3. Retention science layer: scripts and edits that actually perform, not just look good
4. Platform play: Phase 3 opens API → third-party tools integrate *into* CreatorOS
5. Data flywheel: 250K+ videos → proprietary retention data → better outputs → more users

---

*CreatorOS Final PRD v1.0 — Ready for Design & Engineering Handoff*  
*"From idea to impact. For every creator. In every language."*  
*Next review: After MVP Week 4 midpoint checkpoint*
