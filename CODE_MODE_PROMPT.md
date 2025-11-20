# Code Mode Prompt for 1in10killah Development

> **Copy-paste this prompt into Claude Code Mode to start building**

---

## 🚨 **CRITICAL: Previous Implementation Failures**

I've tried building this 20+ times and hit the same bugs. **DO NOT repeat these mistakes:**

### **Bug 1: Video ID Extraction (YouTube Home)**
**SYMPTOM:** Console showed same video ID no matter which bookmark button I clicked
**CAUSE:** Used global `querySelector` instead of scoped to specific video element
**FIX REQUIRED:**
```javascript
// ❌ WRONG - always gets first video
const link = document.querySelector('a#video-title-link');

// ✅ CORRECT - scoped to specific video element
const link = videoElement.querySelector('a#video-title-link');
const videoId = extractVideoIdFromURL(link.href);
```

### **Bug 2: Bookmark Storage Overwrite**
**SYMPTOM:** First bookmark disappeared when adding second one
**CAUSE:** Overwrote storage instead of read-modify-write pattern
**FIX REQUIRED:**
```javascript
// ❌ WRONG - overwrites all bookmarks
await chrome.storage.local.set({ bookmarks: [videoId] });

// ✅ CORRECT - read, append, write
const result = await chrome.storage.local.get('bookmarks');
const bookmarks = result.bookmarks || [];
if (!bookmarks.includes(videoId)) {
  bookmarks.push(videoId);
  await chrome.storage.local.set({ bookmarks });
}
```

### **Bug 3: YouTube SPA Navigation**
**SYMPTOM:** Bookmark buttons disappeared on scroll or navigation
**CAUSE:** Didn't handle YouTube's dynamic DOM (SPA)
**FIX REQUIRED:** Implement MutationObserver to re-inject buttons on DOM changes

---

**MANDATE:** Verify these three patterns are implemented correctly in the codebase before proceeding with other features.

---

## 🎯 **CONTEXT**

I'm building **1in10killah**, an AI-powered Chrome extension for YouTube creators. I have:

1. **Complete product spec** at: https://github.com/creativeprofit22/1in10killah-spec
2. **Existing Chrome extension framework** at: [YOUR_EXTENSION_REPO_URL]

**Read the spec first**, then implement features incrementally following the roadmap.

---

## 📋 **YOUR MISSION**

Build **Phase 1 MVP features** (Months 1-3) based on the comprehensive spec:

### **P0 Features to Implement:**

1. **Smart Outlier Analyzer** (Week 2-4)
   - Auto-extract patterns across 10+ bookmarked videos
   - AI analysis using your chosen provider (Claude, GPT-4, Gemini, etc.)
   - Pattern report: titles, thumbnails, hooks, metadata insights

2. **Enhanced Metadata Viewer** (Week 5-6)
   - Inject metadata badges into 1of10.com video cards
   - Display: engagement rate, duration, tags, niche benchmarks
   - Chrome storage caching (7-day TTL)

3. **Keyword Validator** (Week 7)
   - Extract keywords from video titles
   - Show search volume + SEO difficulty + trend
   - Inject under video title on 1of10.com

4. **Data Exporter Pro** (Week 8)
   - Export to CSV, Excel, Notion, Google Sheets
   - Custom field selection, sorting, filtering
   - Client-side file generation (no server storage)

5. **Chrome Extension Infrastructure** (Week 1-2)
   - Manifest V3 compliant
   - Service worker (background script)
   - Content scripts (YouTube + 1of10.com)
   - Side panel dashboard (React + TypeScript)
   - Storage strategy (chrome.storage + IndexedDB)

---

## 🏗️ **TECHNICAL REQUIREMENTS**

### **Tech Stack (from spec):**
- **Frontend:** React 18, TypeScript, Vite, Tailwind CSS, Zustand
- **Backend:** Node.js, Express, Prisma, BullMQ, PostgreSQL, Redis
- **AI:** Your choice - Claude 3.5 Sonnet, GPT-4 Turbo, Gemini, or local models (see provider options below)
- **APIs:** YouTube Data API v3 (required), your choice for keywords/SEO (see alternatives below)
- **Infrastructure:** Vercel (backend), Cloudflare (CDN), Supabase (auth)

### **API Provider Options:**

**AI Providers (Pattern Analysis):**
The architecture supports any AI provider via abstraction layer. Choose based on your needs:

| Provider | Model | Cost (per 1M tokens) | Strengths | Setup |
|----------|-------|---------------------|-----------|-------|
| **Anthropic Claude** | 3.5 Sonnet | $3 input / $15 output | Best reasoning, context window (200K), function calling | anthropic.com/console |
| **OpenAI** | GPT-4 Turbo | $10 input / $30 output | Excellent analysis, JSON mode, wide adoption | platform.openai.com |
| **Google Gemini** | 1.5 Pro | $1.25 input / $5 output | Cheapest, good performance, 1M context | ai.google.dev |
| **Local (Ollama)** | Llama 3 / Mistral | Free | Zero cost, privacy, offline | ollama.ai |

**Keyword/SEO Providers:**
Optional - you can launch without this feature and add later:

| Provider | Cost | Data Quality | Setup |
|----------|------|--------------|-------|
| **DataForSEO** | $0.004/keyword | High accuracy, YouTube-specific data | dataforseo.com |
| **SEMrush API** | $0.01/keyword | Industry standard, broad coverage | semrush.com/api |
| **Ahrefs API** | Custom pricing | Best backlink data, keyword difficulty | ahrefs.com/api |
| **YouTube Autocomplete** | Free | Basic suggestions, no volume data | Built into YouTube API |

**Recommendation:** Start with free tier of chosen AI provider + YouTube Autocomplete, upgrade to paid keyword API once you validate user demand.

### **Existing Framework:**
- Review my existing extension code at: [YOUR_EXTENSION_REPO_URL]
- **DO NOT rebuild what already exists**
- Integrate new features into existing structure
- Follow existing code patterns and conventions

### **Architecture (from ARCHITECTURE.md):**
```
Extension Structure:
- manifest.json (Manifest V3)
- src/background/service-worker.ts
- src/content/youtube.tsx (YouTube injection)
- src/content/1of10.tsx (1of10.com injection)
- src/sidepanel/App.tsx (main dashboard)
- src/lib/api-client.ts (backend calls)
- src/lib/storage.ts (chrome.storage wrapper)
```

---

## 📖 **SPECIFICATION REFERENCE**

**Read these documents from the spec repo before coding:**

1. **README.md** - Project overview, differentiators, business model
2. **SPEC.md** - Detailed feature specs, competitive analysis, personas
3. **ARCHITECTURE.md** - Technical blueprint, code examples, API design
4. **USER_FLOWS.md** - Step-by-step user journeys (critical for UX)
5. **ROADMAP.md** - Development timeline, week-by-week breakdown

**Key sections to reference:**
- `SPEC.md` → Section 4: Feature Specifications (P0 features)
- `ARCHITECTURE.md` → Section 2: Chrome Extension Architecture
- `USER_FLOWS.md` → Flow 1-3 (most important flows for MVP)
- `ROADMAP.md` → Month 1-3 (MVP development plan)

---

## 🎯 **DEVELOPMENT PRIORITIES**

### **Week 1-2: Foundation** (START HERE)
**Goal:** Set up infrastructure, integrate with existing framework

**Tasks:**
1. Review my existing extension code
2. Set up backend (if not already exists):
   - Express.js API server
   - PostgreSQL + Prisma ORM
   - Redis for caching
   - BullMQ for job queue
3. Create database schema (see `ARCHITECTURE.md` Section 4)
4. Set up YouTube Data API integration
5. Implement chrome.storage wrapper (see `ARCHITECTURE.md` Section 2.4)

**Questions to ask me:**
- What exists in my current extension framework?
- Do I have a backend already, or do we need to build it?
- Do I have YouTube API credentials set up?
- What's my preferred project structure?

---

### **Week 2-4: Feature 1 - Smart Outlier Analyzer**
**Goal:** Auto-extract patterns across bookmarked videos

**Implementation Steps:**
1. **Backend: Pattern Analysis Endpoint**
   ```typescript
   POST /api/v1/analyze/patterns
   Body: { videoIds: string[], userId: string }
   Response: { analysisId: string, patterns: {...} }
   ```

2. **Service Worker: Message Handling**
   - Listen for `ANALYZE_PATTERNS` message from side panel
   - Send request to backend
   - Return results to side panel

3. **Side Panel: Pattern Report UI**
   - "Analyze Patterns" button (triggers when 5+ videos bookmarked)
   - Progress indicator (shows analysis progress)
   - Tabbed pattern report:
     - Tab 1: Title Patterns (word cloud, formulas)
     - Tab 2: Thumbnail Styles (visual grid)
     - Tab 3: Hook Analysis (opening lines, time to hook)
     - Tab 4: Metadata Insights (length, engagement)

4. **AI Integration:**
   - Use your chosen AI provider (see provider comparison below)
   - Implement via provider abstraction layer (see ARCHITECTURE.md Section 5.2)
   - Prompt engineering (see prompt template in SPEC.md)
   - Cost tracking for chosen provider

**Reference:**
- `USER_FLOWS.md` → Flow 2: Creator Analyzes Competitor Video Patterns
- `SPEC.md` → Section 4.2: Feature 1 - Smart Outlier Analyzer
- `ARCHITECTURE.md` → Section 5.2: AI Provider Abstraction

**Success Criteria:**
- Analyze 20 videos in <60 seconds
- Pattern accuracy >80% (validate with test cases)
- Display insights in clean, scannable format

---

### **Week 5-6: Feature 2 - Enhanced Metadata Viewer**
**Goal:** Inject metadata badges into 1of10.com video cards

**Implementation Steps:**
1. **Content Script: 1of10.com Injection**
   - Detect 1of10.com page load
   - Find video cards (DOM selector: `.video-card` or inspect actual selectors)
   - Inject metadata badges (top-right corner overlay)

2. **Backend: Video Metadata Endpoint**
   ```typescript
   GET /api/v1/videos/:videoId
   Response: { engagementRate, duration, tags, keywordData }
   ```

3. **Caching Strategy:**
   - Check chrome.storage.local first (7-day TTL)
   - If miss → Fetch from backend (which checks Redis → YouTube API)
   - Cache result locally

4. **Badge UI Component:**
   ```tsx
   <Badge>
     🔥 TOP 5%
     Engagement: 8.2%
     Duration: 10:34
   </Badge>
   ```

**Reference:**
- `USER_FLOWS.md` → Flow 1: Creator Finds Video Idea (Step 2)
- `SPEC.md` → Section 4.2: Feature 2 - Enhanced Metadata Viewer
- `ARCHITECTURE.md` → Section 2.4: Storage Strategy

**Success Criteria:**
- Inject metadata in <100ms per card
- Cache hit rate >70%
- Zero visual jank (smooth injection)

---

### **Week 7: Feature 3 - Keyword Validator**
**Goal:** Show search volume + SEO difficulty under video titles

**Implementation Steps:**
1. **Keyword Extraction:**
   - Parse video title for main keyword
   - Use YouTube autocomplete API for suggestions

2. **Backend: Keyword Data Endpoint**
   ```typescript
   GET /api/v1/keywords?q=start+a+podcast
   Response: { searchVolume, seoDifficulty, trend, related }
   ```

3. **Keyword API Integration:**
   - Choose your keyword provider (DataForSEO, SEMrush, Ahrefs, etc.)
   - Set up API key for chosen provider
   - Implement keyword lookup service
   - Cache results (30-day TTL)

4. **UI Injection:**
   ```html
   🔍 Search: 12K/mo | SEO: 45 (Medium) | Trend: ↗️ Rising
   ```

**Reference:**
- `SPEC.md` → Section 4.2: Feature 3 - Keyword Validator
- `ARCHITECTURE.md` → Section 5.1: External API Integrations

**Success Criteria:**
- Keyword lookup <2 seconds
- Accuracy >85% (validate against actual search results)

---

### **Week 8: Feature 4 - Data Exporter Pro**
**Goal:** Export bookmarked videos to CSV/Excel/Notion/Sheets

**Implementation Steps:**
1. **Export UI Modal:**
   - Format selection (CSV, Excel, Notion, Sheets)
   - Field checkboxes (title, views, engagement, etc.)
   - Sort/filter options

2. **Client-Side Export:**
   - Use PapaParse for CSV
   - Use ExcelJS for .xlsx
   - No server storage (privacy-first)

3. **API Integrations:**
   - Notion API (create database, insert rows)
   - Google Sheets API (OAuth flow, write to sheet)

**Reference:**
- `SPEC.md` → Section 4.2: Feature 4 - Data Exporter Pro
- `USER_FLOWS.md` → Flow 6: Agency Exports Research for Client Report

**Success Criteria:**
- Export 100 videos in <5 seconds
- Notion/Sheets success rate >95%

---

## 🚨 **IMPORTANT GUIDELINES**

### **DO:**
✅ **Read the spec docs FIRST** before writing any code
✅ **Follow user flows** from USER_FLOWS.md for UX decisions
✅ **Use code examples** from ARCHITECTURE.md as reference
✅ **Integrate with my existing framework** (don't rebuild what exists)
✅ **Ask clarifying questions** if spec is unclear
✅ **Ask about API provider preferences** (don't assume specific providers)
✅ **Implement provider abstraction layer** (easy to swap AI/keyword APIs)
✅ **Implement incrementally** (one feature at a time, test before moving on)
✅ **Track costs** (AI API calls, YouTube quota usage)
✅ **Cache aggressively** (reduce API calls by 80%+)

### **DON'T:**
❌ **Don't rebuild existing infrastructure** (ask what I have first)
❌ **Don't assume specific API providers** (ask user preference first)
❌ **Don't deviate from spec** without discussing trade-offs
❌ **Don't skip error handling** (spec has detailed error scenarios)
❌ **Don't ignore performance targets** (spec has specific benchmarks)
❌ **Don't hardcode API keys** (use environment variables)
❌ **Don't skip caching** (quota limits are strict)

---

## 📊 **SUCCESS METRICS (from SPEC.md)**

Track these metrics during development:

### **Performance:**
- Smart Analyzer: <60 seconds for 20 videos
- Metadata injection: <100ms per card
- API response time (p95): <500ms
- Extension load time: <200ms
- Memory usage: <50MB

### **Accuracy:**
- Pattern analysis: >80% accuracy
- Keyword validation: >85% accuracy
- Performance predictor: ±30% of actual views

### **User Experience:**
- First-time user completion rate: >70%
- 7-day retention: >50%
- NPS score: >40 (MVP), >50 (Phase 2)

---

## 🔗 **INTEGRATION POINTS**

### **My Existing Extension Repo:**
**URL:** [YOUR_EXTENSION_REPO_URL]

**What I need you to do:**
1. Clone my existing repo
2. Review current structure and features
3. Identify integration points for new features
4. Implement features incrementally (don't break existing functionality)

### **Spec Repo:**
**URL:** https://github.com/creativeprofit22/1in10killah-spec

**What to reference:**
- README.md → High-level overview
- SPEC.md → Detailed feature requirements
- ARCHITECTURE.md → Technical implementation
- USER_FLOWS.md → UX patterns
- ROADMAP.md → Development timeline

---

## 🎬 **GETTING STARTED**

### **Step 1: Discovery (5 minutes)**
Ask me these questions:
1. What's the URL of your existing extension repo?
2. What features have you already built?
3. Do you have a backend set up? (Node.js, database, etc.)
4. Which AI provider do you want to use? (Claude, OpenAI, Gemini, local models?)
5. Which keyword API do you want to use? (DataForSEO, SEMrush, Ahrefs, or none initially?)
6. Do you have API keys ready, or should we set up later?
7. What's your preferred database? (PostgreSQL, MySQL, MongoDB?)

### **Step 2: Review Existing Code (15 minutes)**
1. Clone my extension repo
2. Read through existing code structure
3. Identify what's already built
4. Map out integration points for new features

### **Step 3: Plan Integration (10 minutes)**
1. Create integration plan:
   - What to reuse from existing code
   - What to build new
   - What to refactor
2. Share plan with me for approval

### **Step 4: Implement Incrementally (Ongoing)**
1. Build one feature at a time (follow roadmap order)
2. Test thoroughly before moving to next feature
3. Share progress updates and demos
4. Iterate based on feedback

---

## 💡 **HELPFUL CONTEXT**

### **Target Users (from SPEC.md):**
- **Alex** (Faceless creator) - Needs scalable research, saves 9+ hours/week
- **Sarah** (Personal brand) - Needs editing efficiency, prevents burnout
- **Marcus** (Agency) - Needs team features, white-label reports

### **Competitive Landscape:**
We're crushing:
- **1of10** ($49-99/mo) - Automate their manual workflow
- **VidIQ** ($7.50-499/mo) - Pre-production vs post-production
- **TubeBuddy** ($2.25-49.50/mo) - Add AI (they have none)
- **NexLev** ($510-799 lifetime) - Reliability + FREE tier
- **VidNinjas** (free) - Intelligence vs basic filtering

### **Value Proposition:**
Save creators **15-20 hours/week** on research, increase hit rate **3x**, prevent flop videos with pre-production validation.

---

## 🚀 **LET'S BUILD**

**My current status:**
- I have an existing Chrome extension framework
- I'm ready to implement MVP features from the spec
- I'll provide my extension repo URL and answer your discovery questions

**What I need from you:**
1. Ask discovery questions (above)
2. Review my existing code
3. Create integration plan
4. Build features incrementally following roadmap
5. Reference spec docs for all implementation details

**Let's start with discovery questions!**

---

## 📧 **QUESTIONS?**

If anything in the spec is unclear:
1. Check SPEC.md Section 4 (detailed feature requirements)
2. Check ARCHITECTURE.md Section 10 (code examples)
3. Check USER_FLOWS.md (step-by-step UX)
4. Ask me directly if still unclear

**Spec Repo:** https://github.com/creativeprofit22/1in10killah-spec

---

**Ready to code? Let's crush it! 🔥**
