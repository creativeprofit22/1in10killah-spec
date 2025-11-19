# 1in10killah User Flows

> **Step-by-Step User Journeys for Key Features**

**Document Version:** 1.0
**Last Updated:** November 19, 2025

---

## Table of Contents

1. [User Flow 1: Creator Finds Video Idea and Researches It](#user-flow-1-creator-finds-video-idea-and-researches-it)
2. [User Flow 2: Creator Analyzes Competitor Video Patterns](#user-flow-2-creator-analyzes-competitor-video-patterns)
3. [User Flow 3: Creator Generates Production-Ready Video Brief](#user-flow-3-creator-generates-production-ready-video-brief)
4. [User Flow 4: Creator Validates Script Before Filming](#user-flow-4-creator-validates-script-before-filming)
5. [User Flow 5: Creator Predicts Video Performance Before Publishing](#user-flow-5-creator-predicts-video-performance-before-publishing)
6. [User Flow 6: Agency Exports Research for Client Report](#user-flow-6-agency-exports-research-for-client-report)
7. [User Flow 7: Creator Discovers Cross-Platform Content Opportunities](#user-flow-7-creator-discovers-cross-platform-content-opportunities)

---

## User Flow 1: Creator Finds Video Idea and Researches It

**Persona:** Alex (Faceless Channel Creator)
**Goal:** Find a proven video idea in the productivity niche and validate it has search demand
**Time to Complete:** 5-10 minutes (vs 2-3 hours manual)

### Step-by-Step Flow

#### 1. Discovery Phase (1of10.com)

**Location:** 1of10.com
**User Action:** Alex searches for "productivity" outliers

```
┌─────────────────────────────────────────────┐
│ 1of10.com - Outlier Search                 │
├─────────────────────────────────────────────┤
│ [Search: productivity]  [Search]            │
│                                             │
│ Filters:                                    │
│ Views: [100K+]                              │
│ Upload Date: [Last 30 days]                │
│ Outlier Score: [10x+]                       │
│                                             │
│ Results: 47 outlier videos                  │
└─────────────────────────────────────────────┘
```

**System Response:**
- 1of10 displays 47 outlier videos
- 1in10killah extension detects page load
- Content script injects metadata badges on each video card

---

#### 2. Enhanced Metadata Display

**Location:** 1of10.com video cards
**User Action:** Alex hovers over the first outlier video

**What Alex Sees:**

```
┌──────────────────────────────────────────────────────┐
│ "The 2-Minute Rule That Changed My Life"            │
│ Channel: Productivity Pro (45K subs)                 │
│ Views: 1.2M | Outlier Score: 27x                    │
│                                          ┌─────────┐ │
│ [Thumbnail Image]                        │ 🔥 TOP 3%│ │
│                                          │ Eng: 9.2%│ │
│                                          │ Dur: 8:24│ │
│                                          └─────────┘ │
│                                                      │
│ 🔍 Search: 18K/mo | SEO: 32 (Easy) | Trend: ↗️ +22% │
└──────────────────────────────────────────────────────┘
```

**1in10killah Enhancements Displayed:**
- ✅ **Engagement Rate:** 9.2% (Top 3% for productivity niche)
- ✅ **Duration:** 8:24 (optimal length for topic)
- ✅ **Search Volume:** 18K/month (healthy demand)
- ✅ **SEO Difficulty:** 32/100 (Easy - low competition)
- ✅ **Trend:** Rising +22% (growing interest)

**User Insight:** *"This topic has strong search demand, low competition, and is trending up. Good opportunity."*

---

#### 3. Validation Decision

**User Action:** Alex clicks on the video card to open side panel

**What Happens:**
1. 1in10killah side panel opens (slides in from right)
2. Extension fetches full video metadata from YouTube API
3. Displays detailed analysis

**Side Panel View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah                        [✕]     │
├─────────────────────────────────────────────┤
│ "The 2-Minute Rule That Changed My Life"   │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ QUICK STATS                             │ │
│ │ Views: 1.2M | Likes: 87K | Comments: 2.1K│ │
│ │ Engagement: 9.2% (Top 3%)               │ │
│ │ Published: 12 days ago                  │ │
│ │ Velocity: 100K views/day (viral!)       │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ KEYWORD VALIDATION                      │ │
│ │ Primary: "2 minute rule"                │ │
│ │ Search Volume: 18K/month                │ │
│ │ SEO Difficulty: 32/100 (Easy)           │ │
│ │ Trend: ↗️ Rising (+22% this quarter)    │ │
│ │ Related: "atomic habits", "productivity"│ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ NICHE BENCHMARK                         │ │
│ │ This video is performing in the         │ │
│ │ TOP 3% of productivity videos           │ │
│ │ for channels with 40-50K subscribers    │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [ Bookmark ] [ Analyze Patterns ] [ Brief ]│
└─────────────────────────────────────────────┘
```

---

#### 4. Bookmark for Later Analysis

**User Action:** Alex clicks "Bookmark" button

**System Response:**
1. Video saved to Alex's bookmark collection in chrome.storage.local
2. Toast notification: "Saved to bookmarks (1 of 20)"
3. Button changes to "✓ Bookmarked"

**User Action:** Alex repeats this for 9 more videos (total: 10 bookmarked outliers)

---

#### 5. Batch Pattern Analysis (Next Flow)

**User Outcome:**
- ✅ Found 10 validated outlier videos in 10 minutes (vs 2-3 hours manual)
- ✅ All videos have proven search demand (18K-50K searches/month)
- ✅ All videos have low SEO difficulty (<40/100)
- ✅ All videos are trending up (rising interest)
- ✅ Ready to proceed to pattern analysis

**Time Saved:** 2-3 hours → 10 minutes = **2.5 hours saved**

---

## User Flow 2: Creator Analyzes Competitor Video Patterns

**Persona:** Alex (Faceless Channel Creator)
**Goal:** Identify common patterns across 10 bookmarked outliers to replicate success
**Time to Complete:** 2-3 minutes (vs 5-10 hours manual)

### Step-by-Step Flow

#### 1. Open Bookmarks

**Location:** 1in10killah side panel
**User Action:** Alex clicks "Bookmarks" tab in side panel

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah                        [✕]     │
├─────────────────────────────────────────────┤
│ [ Search ] [ Bookmarks ] [ Analyze ]       │
│            ^^^^^^^^^^^                      │
├─────────────────────────────────────────────┤
│ BOOKMARKED VIDEOS (10)                      │
│                                             │
│ [✓] The 2-Minute Rule... (1.2M views)      │
│ [✓] How I Wake Up at 5 AM... (890K views)  │
│ [✓] Productivity Hacks... (650K views)     │
│ [✓] Time Blocking Guide... (540K views)    │
│ ... (6 more videos)                        │
│                                             │
│ [ Select All ] [ Analyze Patterns (10) ]   │
└─────────────────────────────────────────────┘
```

---

#### 2. Trigger Pattern Analysis

**User Action:** Alex clicks "Analyze Patterns (10)" button

**System Response:**
1. Button shows loading spinner: "Analyzing..."
2. Backend service worker fetches metadata for all 10 videos
3. For each video:
   - Scrape title, thumbnail, tags from YouTube
   - Fetch transcript via YouTube API (50 units × 10 = 500 units)
   - Extract hook (first 30 seconds of transcript)
   - Analyze thumbnail (color palette, text overlay, visual style)
4. Send all data to Claude 3.5 Sonnet API with pattern extraction prompt
5. Process response (30-60 seconds)

**Progress Indicator:**

```
┌─────────────────────────────────────────────┐
│ Analyzing Patterns...                       │
├─────────────────────────────────────────────┤
│ ████████████████░░░░░░░░░░░░  60%          │
│                                             │
│ Processing: Video 6 of 10                   │
│ Extracting hooks and thumbnails...          │
│                                             │
│ Estimated time: 25 seconds                  │
└─────────────────────────────────────────────┘
```

---

#### 3. Pattern Report Display

**System Response:** After 45 seconds, analysis completes

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Pattern Analysis Report       │
├─────────────────────────────────────────────┤
│ [ Titles ] [ Thumbnails ] [ Hooks ] [ Meta ]│
│   ^^^^^^^                                   │
├─────────────────────────────────────────────┤
│ TITLE PATTERNS (10 videos analyzed)         │
│                                             │
│ ✅ 90% use CURIOSITY GAP                   │
│    Examples: "The Secret...", "You Won't   │
│    Believe...", "What Nobody Tells You..."  │
│                                             │
│ ✅ 80% include NUMBERS                     │
│    Examples: "2-Minute Rule", "5 AM",      │
│    "7 Productivity Hacks"                   │
│                                             │
│ ✅ 70% use "HOW TO" or "GUIDE" format      │
│    Examples: "How I Wake Up...", "Guide to"│
│                                             │
│ ✅ Average title length: 52 characters     │
│    (Range: 42-65 chars)                    │
│                                             │
│ 💡 RECOMMENDATION:                          │
│ Use this formula:                           │
│ "[Number] + [Curiosity Gap] + [Benefit]"   │
│ Example: "The 5 Secrets to Waking Up at 5 AM│
│ (Without Coffee)"                           │
└─────────────────────────────────────────────┘
```

---

#### 4. Explore Thumbnail Patterns

**User Action:** Alex clicks "Thumbnails" tab

**View:**

```
┌─────────────────────────────────────────────┐
│ THUMBNAIL PATTERNS                          │
├─────────────────────────────────────────────┤
│ ✅ 100% use TEXT OVERLAY                   │
│    Average: 3-5 words, BOLD font           │
│                                             │
│ ✅ 80% use BRIGHT COLORS                   │
│    Dominant colors:                         │
│    🟥 Red (40%) | 🟧 Orange (25%) | 🟦 Blue (15%)│
│                                             │
│ ✅ 60% feature PERSON in frame             │
│    (Even faceless channels use stock photos)│
│                                             │
│ ✅ 90% have HIGH CONTRAST                  │
│    (Light text on dark background or vice versa)│
│                                             │
│ 💡 RECOMMENDATION:                          │
│ Create thumbnail with:                      │
│ - Red or orange background                  │
│ - 3-4 word text overlay (white, bold)      │
│ - Stock photo of person (if appropriate)   │
│ - High contrast for mobile visibility       │
└─────────────────────────────────────────────┘
```

---

#### 5. Explore Hook Patterns

**User Action:** Alex clicks "Hooks" tab

**View:**

```
┌─────────────────────────────────────────────┐
│ HOOK PATTERNS (First 30 seconds)            │
├─────────────────────────────────────────────┤
│ ✅ 80% start with a PROBLEM or PAIN POINT  │
│    Examples:                                │
│    • "Are you struggling to wake up early?"│
│    • "Most people waste 3 hours every day" │
│    • "You're making these productivity     │
│       mistakes..."                          │
│                                             │
│ ✅ 70% use PATTERN INTERRUPT               │
│    Examples:                                │
│    • Unexpected sound effect                │
│    • Bold claim: "This changed everything" │
│    • Question: "What if I told you..."     │
│                                             │
│ ✅ Average time to hook: 8 seconds         │
│    (Range: 5-12 seconds)                   │
│                                             │
│ ✅ 90% preview the SOLUTION early          │
│    Example: "In this video, I'll show you  │
│    the 2-minute rule that solves this"     │
│                                             │
│ 💡 RECOMMENDATION:                          │
│ Your hook should:                           │
│ 1. State problem (0:00-0:05)               │
│ 2. Tease solution (0:06-0:10)              │
│ 3. Promise value (0:11-0:30)               │
└─────────────────────────────────────────────┘
```

---

#### 6. Export Pattern Report

**User Action:** Alex clicks "Export Report" button (bottom of side panel)

**System Response:** Modal opens

```
┌─────────────────────────────────────────────┐
│ Export Pattern Analysis                     │
├─────────────────────────────────────────────┤
│ Format: [ PDF ▼ ]                          │
│         (Options: PDF, Notion, Google Docs) │
│                                             │
│ Include:                                    │
│ [✓] Title patterns                          │
│ [✓] Thumbnail patterns                      │
│ [✓] Hook patterns                           │
│ [✓] Metadata insights                       │
│ [✓] Recommendations                         │
│                                             │
│ [ Cancel ]          [ Export Pattern Report]│
└─────────────────────────────────────────────┘
```

**User Action:** Alex clicks "Export Pattern Report"

**System Response:**
1. Generate PDF with all pattern data + visualizations
2. Auto-download: `1in10killah_pattern_analysis_2026-01-15.pdf`
3. Toast notification: "Report exported successfully!"

---

#### 7. User Outcome

**What Alex Achieved:**
- ✅ Analyzed 10 competitor videos in 3 minutes (vs 5-10 hours manual)
- ✅ Identified title formula: "[Number] + [Curiosity Gap] + [Benefit]"
- ✅ Learned thumbnail best practices: Red/orange bg, 3-4 word text, high contrast
- ✅ Extracted hook structure: Problem (0-5s) → Solution tease (6-10s) → Promise (11-30s)
- ✅ Exported report for reference when creating next video

**Time Saved:** 5-10 hours → 3 minutes = **9+ hours saved**

**Next Step:** Alex uses these patterns to create a video brief (Flow 3)

---

## User Flow 3: Creator Generates Production-Ready Video Brief

**Persona:** Alex (Faceless Channel Creator)
**Goal:** Generate a production-ready video brief to send to scriptwriter
**Time to Complete:** 1-2 minutes (vs 30-60 minutes manual)

### Step-by-Step Flow

#### 1. Select Outlier to Replicate

**Location:** 1in10killah side panel → Bookmarks
**User Action:** Alex selects "The 2-Minute Rule That Changed My Life" (1.2M views)

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Bookmarks                     │
├─────────────────────────────────────────────┤
│ ● "The 2-Minute Rule..." (1.2M views)      │
│   Productivity Pro • 12 days ago            │
│   Engagement: 9.2% | Duration: 8:24         │
│   Search: 18K/mo | SEO: 32 (Easy)           │
│                                             │
│   [ Watch ] [ Analyze ] [ Generate Brief ] │
└─────────────────────────────────────────────┘
```

---

#### 2. Trigger Brief Generation

**User Action:** Alex clicks "Generate Brief" button

**System Response:**
1. Button shows loading: "Generating brief..."
2. Backend fetches:
   - Full video transcript (YouTube API)
   - Video metadata (title, description, tags)
   - Thumbnail image
   - Pattern analysis from previous analysis
3. Sends to Claude 3.5 Sonnet with brief generation prompt:

```
Prompt Template:
"Create a production-ready video brief based on this outlier video.

Video: 'The 2-Minute Rule That Changed My Life'
Transcript: [full transcript]
Metadata: [title, tags, description]
Thumbnail: [image analysis]
Patterns identified: [title formula, hook structure, thumbnail style]

Generate a brief with:
1. Concept (1-2 sentences - what's the video about?)
2. Hook (0:00-0:30) - opening script + visual suggestions
3. Body (3-5 main points with timestamps, B-roll keywords)
4. CTA (final 30 seconds)
5. SEO metadata (title variations, tags, keywords)
6. Thumbnail ideas (2-3 concepts based on patterns)

Format in Markdown for easy export."
```

4. Process response (30-60 seconds)

---

#### 3. Brief Preview

**System Response:** Brief generated, displayed in side panel

```
┌─────────────────────────────────────────────┐
│ Video Brief: "The 2-Minute Rule"            │
├─────────────────────────────────────────────┤
│ [Scroll to view full brief]                 │
│                                             │
│ ## CONCEPT                                  │
│ Explain the 2-minute rule from "Atomic     │
│ Habits" and show viewers how to implement  │
│ it to overcome procrastination.            │
│                                             │
│ ---                                         │
│                                             │
│ ## HOOK (0:00-0:30)                        │
│ **Script:**                                 │
│ "Do you waste hours procrastinating on     │
│ simple tasks? What if I told you there's a │
│ 2-minute rule that makes starting anything │
│ effortless? By the end of this video,      │
│ you'll never struggle with procrastination │
│ again."                                     │
│                                             │
│ **Visual:** Stock footage of person        │
│ staring at laptop, looking overwhelmed     │
│                                             │
│ ---                                         │
│                                             │
│ ## BODY                                     │
│                                             │
│ ### Point 1: What is the 2-Minute Rule?   │
│ (0:30-2:00)                                │
│ - Definition: If a task takes less than 2  │
│   minutes, do it immediately               │
│ - Origin: James Clear's "Atomic Habits"    │
│ - Visual: Text overlay "2-Minute Rule"     │
│           + book cover B-roll              │
│                                             │
│ [... continues with 4 more sections ...]   │
│                                             │
│ [ Export to Notion ] [ Export to Docs ]    │
│ [ Copy Markdown ] [ Edit Brief ]           │
└─────────────────────────────────────────────┘
```

---

#### 4. Export Brief to Notion

**User Action:** Alex clicks "Export to Notion"

**System Response:**
1. Modal opens for Notion authentication (first time only)
2. User grants access to Notion workspace
3. System creates new page in "Video Briefs" database:

**Notion Page Created:**

```
Title: [Video Brief] The 2-Minute Rule (2026-01-15)

Properties:
- Status: Draft
- Niche: Productivity
- Estimated Views: 15K-45K (from Performance Predictor)
- SEO Difficulty: 32 (Easy)
- Priority: High

Content:
[Full brief pasted as Markdown with proper formatting]
```

**System Response:** Toast notification

```
┌───────────────────────────────────┐
│ ✓ Brief exported to Notion!       │
│   View: [Open in Notion]          │
└───────────────────────────────────┘
```

---

#### 5. Share with Scriptwriter

**User Action:** Alex opens Notion page, shares with scriptwriter

**Notion Workflow:**
1. Alex assigns page to scriptwriter (teammate in Notion workspace)
2. Adds comment: "@Sarah can you write a script based on this brief? Need it by Friday."
3. Sarah receives notification, starts writing

---

#### 6. User Outcome

**What Alex Achieved:**
- ✅ Generated production-ready brief in 2 minutes (vs 30-60 minutes manual)
- ✅ Brief includes: concept, hook script, body structure, visual suggestions, SEO metadata, thumbnail ideas
- ✅ Exported to Notion for easy collaboration with scriptwriter
- ✅ Scriptwriter has clear direction (vs vague "research productivity topics")

**Time Saved:** 30-60 minutes → 2 minutes = **45+ minutes saved**

**Next Step:** Scriptwriter writes script, Alex validates it with Script Analyzer (Flow 4)

---

## User Flow 4: Creator Validates Script Before Filming

**Persona:** Sarah (Personal Brand Creator)
**Goal:** Ensure her script will keep viewers engaged before filming
**Time to Complete:** 2-3 minutes (vs no validation currently)

### Step-by-Step Flow

#### 1. Open Script Analyzer

**Location:** 1in10killah side panel → Tools
**User Action:** Sarah clicks "Script Analyzer" tab

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Script Analyzer               │
├─────────────────────────────────────────────┤
│ Paste your script below (500-5000 words):   │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ [Sarah pastes her 1,200-word script]   │ │
│ │                                         │ │
│ │ "Have you ever felt like you're stuck  │ │
│ │ in a productivity rut? Like no matter  │ │
│ │ how many planners you buy or apps you  │ │
│ │ download, you still can't get anything │ │
│ │ done?                                   │ │
│ │                                         │ │
│ │ I've been there. And I'm about to      │ │
│ │ share the one simple rule that         │ │
│ │ completely changed my life..."          │ │
│ │                                         │ │
│ │ [... rest of 1,200-word script ...]    │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [ Cancel ]              [ Analyze Script ] │
└─────────────────────────────────────────────┘
```

---

#### 2. Trigger Analysis

**User Action:** Sarah clicks "Analyze Script"

**System Response:**
1. Button shows loading: "Analyzing..."
2. Script sent to GPT-4 Turbo with analysis prompt:

```
Prompt:
"Analyze this YouTube script for viewer retention potential.

Script: [Sarah's 1,200-word script]

Provide:
1. Hook Strength (0-100): How well does the first 30 seconds grab attention?
2. Retention Prediction (%): Estimated average view duration
3. Sentiment: Positive, neutral, negative, or mixed?
4. Pacing: Words per minute (assume 150 WPM speaking rate)
5. Story Structure: Does it have clear beginning, middle, end?
6. Recommendations: 3-5 actionable improvements

Be honest and specific."
```

3. Process response (10-20 seconds)

---

#### 3. Analysis Results

**System Response:** Results displayed

```
┌─────────────────────────────────────────────┐
│ Script Analysis Results                     │
├─────────────────────────────────────────────┤
│ 📊 OVERALL SCORE: 78/100 (Good)            │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ HOOK STRENGTH: 85/100 (Excellent)       │ │
│ │ ████████████████████░░░░░░░░░           │ │
│ │                                         │ │
│ │ ✅ Strong opening question (relatable)  │ │
│ │ ✅ Personal connection ("I've been     │ │
│ │    there")                              │ │
│ │ ✅ Promise of value ("one simple rule")│ │
│ │                                         │ │
│ │ Great hook! Viewers will stay for this.│ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ RETENTION PREDICTION: 68%               │ │
│ │ ████████████████░░░░░░░░░░░░           │ │
│ │                                         │ │
│ │ Above average for 8-minute video        │ │
│ │ (niche avg: 55%)                        │ │
│ │                                         │ │
│ │ Viewers will likely watch ~5:30 of 8:00│ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ SENTIMENT: Positive & Encouraging       │ │
│ │ Tone: Conversational, authentic         │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ PACING: 155 words/minute                │ │
│ │ ✅ Optimal range (140-160 WPM)          │ │
│ │                                         │ │
│ │ Script length: 1,200 words = ~7:45 video│ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [View Recommendations ▼]                   │
└─────────────────────────────────────────────┘
```

---

#### 4. View Recommendations

**User Action:** Sarah clicks "View Recommendations ▼"

**View Expands:**

```
┌─────────────────────────────────────────────┐
│ 🎯 RECOMMENDATIONS                          │
├─────────────────────────────────────────────┤
│ 1. ✅ KEEP: Strong hook (0:00-0:30)        │
│    Your opening is excellent. Don't change │
│    it.                                      │
│                                             │
│ 2. ⚠️ IMPROVE: Add pause at 4:30 mark     │
│    Your script goes 90 seconds without a   │
│    break around the 4:30 mark. Add a pause │
│    or B-roll moment to let viewers breathe.│
│                                             │
│ 3. ⚠️ IMPROVE: Move CTA earlier            │
│    Your call-to-action is at 7:30, but     │
│    68% of viewers drop off by 5:30. Move   │
│    the CTA to the 5:00 mark.               │
│                                             │
│ 4. ✅ KEEP: Conversational tone            │
│    Your authentic, personal style is what  │
│    makes this work. Don't lose that.       │
│                                             │
│ 5. ⚠️ CONSIDER: Add visual cue at 2:15    │
│    Suggest adding text overlay or graphic  │
│    at 2:15 when you introduce the "2-minute│
│    rule" concept. Will boost retention.    │
└─────────────────────────────────────────────┘
```

---

#### 5. Revise Script Based on Feedback

**User Action:** Sarah makes edits:
1. Adds pause at 4:30 mark
2. Moves CTA from 7:30 → 5:00
3. Adds note for editor: "Text overlay at 2:15: '2-Minute Rule'"

**User Action:** Sarah re-analyzes updated script

**New Results:**

```
┌─────────────────────────────────────────────┐
│ 📊 OVERALL SCORE: 86/100 (Excellent!)      │
│                                             │
│ Hook Strength: 85/100 (no change)          │
│ Retention Prediction: 74% ⬆️ (+6%)        │
│ Sentiment: Positive & Encouraging           │
│ Pacing: 153 WPM ✅                         │
│                                             │
│ ✅ Great improvements! This script is      │
│    ready to film.                           │
└─────────────────────────────────────────────┘
```

---

#### 6. User Outcome

**What Sarah Achieved:**
- ✅ Validated script will perform well (74% predicted retention vs 55% niche avg)
- ✅ Improved retention by 6% with simple edits (move CTA, add pause)
- ✅ Confidence to film (vs anxiety about whether script will work)
- ✅ Specific notes for editor (text overlay at 2:15)

**Value Created:** Prevented potential flop video, increased retention by 6% = ~2K more views per video (at 30K avg views)

**Next Step:** Sarah films video with confidence, then validates performance prediction before publishing (Flow 5)

---

## User Flow 5: Creator Predicts Video Performance Before Publishing

**Persona:** Sarah (Personal Brand Creator)
**Goal:** Predict how many views her video will get before publishing to decide if she should adjust title/thumbnail
**Time to Complete:** 1-2 minutes

### Step-by-Step Flow

#### 1. Open Performance Predictor

**Location:** 1in10killah side panel → Tools → Performance Predictor
**User Action:** Sarah clicks "Performance Predictor" tab

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Performance Predictor         │
├─────────────────────────────────────────────┤
│ Predict views for your next video:          │
│                                             │
│ Title:                                      │
│ ┌─────────────────────────────────────────┐ │
│ │ The 2-Minute Rule That Actually Works   │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Thumbnail:                                  │
│ [ Upload Image ] or [ URL ]                │
│ ┌─────────────────────────────────────────┐ │
│ │ [Thumbnail preview shown here]          │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Niche: [ Productivity ▼ ]                 │
│                                             │
│ Channel Size: [ 120,000 ] subscribers      │
│                                             │
│ Video Length: [ 8:30 ]                     │
│                                             │
│ [ Predict Performance ]                    │
└─────────────────────────────────────────────┘
```

---

#### 2. Input Video Details

**User Actions:**
1. Sarah pastes title: "The 2-Minute Rule That Actually Works"
2. Uploads thumbnail image (red background, text overlay: "2-MIN RULE")
3. Selects niche: "Productivity"
4. Enters channel size: 120,000 subscribers
5. Enters video length: 8:30

---

#### 3. Trigger Prediction

**User Action:** Sarah clicks "Predict Performance"

**System Response:**
1. Button shows loading: "Analyzing..."
2. ML model processes inputs:
   - Title sentiment analysis (NLP)
   - Thumbnail feature extraction (ResNet embedding)
   - Niche benchmark lookup (from database)
   - Channel authority calculation (subscriber count, avg views)
3. Model predicts views, CTR, retention (XGBoost trained on 100K videos)
4. Display results with confidence intervals (2-3 seconds)

---

#### 4. Prediction Results

**System Response:**

```
┌─────────────────────────────────────────────┐
│ Performance Prediction                      │
├─────────────────────────────────────────────┤
│ 📊 PREDICTED VIEWS (7 days)                │
│                                             │
│    25,000 - 45,000 views                   │
│    ████████████████░░░░░░░░                │
│    (80% confidence interval)                │
│                                             │
│    Most likely: ~35,000 views               │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ PREDICTED CTR: 9-13%                    │ │
│ │ Your thumbnail is strong (red bg,       │ │
│ │ clear text). Expected CTR is above      │ │
│ │ average for productivity niche (8%).    │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ PREDICTED RETENTION: 65-75%             │ │
│ │ Based on your script analysis (74%      │ │
│ │ predicted) and niche benchmarks.        │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ NICHE BENCHMARK                         │ │
│ │ This video is predicted to perform in   │ │
│ │ the TOP 20% of productivity videos      │ │
│ │ for channels with 100-150K subscribers  │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ⚠️ DISCLAIMER: This is an ESTIMATE based  │
│    on historical data. Actual results may  │
│    vary ±30%. Use as a guide, not guarantee│
└─────────────────────────────────────────────┘
```

---

#### 5. Decision Point

**Sarah's Thought Process:**
- "35K views is above my channel average (30K)"
- "CTR is predicted to be strong (9-13%)"
- "This looks good, I'll publish as-is"

**Alternative Scenario:** If prediction was low (e.g., 10K-20K views), Sarah could:
1. Try different title (e.g., add number: "5 Ways the 2-Minute Rule Works")
2. Upload different thumbnail (test brighter colors)
3. Re-run prediction to see if changes improve outlook

---

#### 6. Publish with Confidence

**User Action:** Sarah publishes video to YouTube

**Follow-Up (7 days later):**
- **Actual Results:** 38,000 views, 11% CTR, 72% retention
- **Prediction Accuracy:** Views within 9% (predicted 35K, actual 38K) ✅
- **User Feedback:** "1in10killah predictions were spot-on! I trusted the data and it worked."

---

#### 7. User Outcome

**What Sarah Achieved:**
- ✅ Confidence to publish (vs anxiety about whether video will perform)
- ✅ Avoided wasting time on low-potential video (could pivot if prediction was bad)
- ✅ Validated title/thumbnail choices (predicted CTR confirmed good thumbnail)
- ✅ Benchmark for future videos (now knows what "top 20%" looks like for her channel)

**Behavioral Change:** Sarah now uses Performance Predictor for EVERY video before publishing

**Next Step:** Sarah tracks actual performance vs prediction to improve future predictions

---

## User Flow 6: Agency Exports Research for Client Report

**Persona:** Marcus (Agency Owner)
**Goal:** Export research for 3 clients into a white-label report for monthly check-in
**Time to Complete:** 5-10 minutes (vs 2-3 hours manual)

### Step-by-Step Flow

#### 1. Select Client Videos

**Location:** 1in10killah side panel → Bookmarks → Filter by client
**User Action:** Marcus filters bookmarks by client tag

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Bookmarks                     │
├─────────────────────────────────────────────┤
│ Filter by: [ Client: TechReview ▼ ]       │
│                                             │
│ VIDEOS FOR CLIENT: TechReview (15)          │
│                                             │
│ [✓] "Best Laptops 2026" (450K views)       │
│ [✓] "M3 MacBook Review" (320K views)       │
│ [✓] "Budget Gaming PC" (280K views)        │
│ ... (12 more videos)                       │
│                                             │
│ [ Select All (15) ] [ Export ]             │
└─────────────────────────────────────────────┘
```

---

#### 2. Bulk Export

**User Action:** Marcus clicks "Select All (15)" then "Export"

**Modal Opens:**

```
┌─────────────────────────────────────────────┐
│ Export Client Research                      │
├─────────────────────────────────────────────┤
│ Format: [ White-Label PDF ▼ ]              │
│         (Options: CSV, Excel, PDF,          │
│          White-Label PDF)                   │
│                                             │
│ Include:                                    │
│ [✓] Video titles & URLs                     │
│ [✓] Engagement metrics                      │
│ [✓] Keyword data (search volume, SEO)      │
│ [✓] Pattern analysis summary                │
│ [✓] Recommendations for next videos         │
│ [ ] 1in10killah branding (white-label)     │
│                                             │
│ Client Name: [ TechReview ]                │
│ Report Date: [ January 2026 ]             │
│                                             │
│ [ Cancel ]               [ Generate Report ]│
└─────────────────────────────────────────────┘
```

---

#### 3. White-Label Report Generated

**User Action:** Marcus unchecks "1in10killah branding" and clicks "Generate Report"

**System Response:**
1. Generate PDF with client branding (agency logo, client name)
2. Include all selected data + charts (engagement trends, keyword opportunities)
3. Add AI-generated executive summary
4. Auto-download: `TechReview_Monthly_Report_Jan2026.pdf`

**Report Contents:**

```
┌─────────────────────────────────────────────┐
│ [Agency Logo]                               │
│ MONTHLY VIDEO RESEARCH REPORT               │
│ Client: TechReview                          │
│ Period: January 2026                        │
├─────────────────────────────────────────────┤
│ EXECUTIVE SUMMARY                           │
│ This month, we analyzed 15 outlier videos   │
│ in the tech review niche. Key findings:     │
│ - Laptop reviews are trending (+35%)       │
│ - Budget gaming content has low SEO (25)   │
│ - Avg engagement: 8.5% (above niche avg)   │
│                                             │
│ RECOMMENDED NEXT VIDEOS:                    │
│ 1. "Best Budget Laptops Under $500" (18K   │
│    monthly searches, SEO: 28)               │
│ 2. "M3 vs M4 MacBook: Full Comparison"     │
│    (12K searches, SEO: 35)                  │
│ 3. "Gaming PC Build Guide 2026" (25K       │
│    searches, SEO: 42)                       │
│                                             │
│ [Detailed data tables, charts...]          │
│                                             │
│ [Agency Contact Info]                       │
│ Prepared by: Marcus & Team                  │
└─────────────────────────────────────────────┘
```

---

#### 4. Repeat for Other Clients

**User Action:** Marcus repeats export for 2 more clients (5 min each)

**Results:**
- TechReview report (15 videos) - 5 minutes
- FitnessGuru report (12 videos) - 4 minutes
- CookingChannel report (20 videos) - 6 minutes

**Total Time:** 15 minutes (vs 2-3 hours manual)

---

#### 5. User Outcome

**What Marcus Achieved:**
- ✅ Generated 3 white-label client reports in 15 minutes (vs 2-3 hours manual)
- ✅ Reports include data + AI-generated recommendations
- ✅ Professional branding (agency logo, no 1in10killah branding)
- ✅ Impressed clients with depth of research and insights

**Time Saved:** 2-3 hours → 15 minutes = **2+ hours saved per month**

**Business Impact:** Marcus can now handle 30 clients (vs 15) without hiring more staff

---

## User Flow 7: Creator Discovers Cross-Platform Content Opportunities

**Persona:** Sarah (Personal Brand Creator)
**Goal:** Find her winning YouTube video idea that could also work on TikTok and Instagram Reels
**Time to Complete:** 3-5 minutes (requires Phase 3 multi-platform features)

### Step-by-Step Flow

#### 1. Analyze YouTube Video

**Location:** 1in10killah side panel → Cross-Platform Analyzer
**User Action:** Sarah inputs her planned YouTube video

**View:**

```
┌─────────────────────────────────────────────┐
│ 1in10killah - Cross-Platform Analyzer       │
├─────────────────────────────────────────────┤
│ YouTube Video:                              │
│ Title: "The 2-Minute Rule That Actually     │
│ Works"                                      │
│ Length: 8:30                                │
│ Niche: Productivity                         │
│                                             │
│ [ Analyze Cross-Platform Potential ]       │
└─────────────────────────────────────────────┘
```

---

#### 2. AI Repurposing Recommendations

**System Response:**

```
┌─────────────────────────────────────────────┐
│ Cross-Platform Opportunities                │
├─────────────────────────────────────────────┤
│ ✅ HIGH POTENTIAL: TikTok                  │
│    This topic is TRENDING on TikTok         │
│    (#2minuterule has 12M views)            │
│                                             │
│    Recommended format:                      │
│    - 60-second version (hook + key takeaway)│
│    - Trending sound: "Productive vibes"    │
│    - Hashtags: #productivity #atomichabits │
│                                             │
│    Predicted TikTok views: 50K-150K        │
│                                             │
│ ✅ HIGH POTENTIAL: Instagram Reels         │
│    Similar topic performed well on Reels:   │
│    "Productivity rules" avg 80K views       │
│                                             │
│    Recommended format:                      │
│    - 30-45 second version (visual-heavy)   │
│    - Use text overlays (no voiceover)      │
│    - Trending audio: "Motivation mix"      │
│                                             │
│    Predicted Reels views: 30K-80K          │
│                                             │
│ [ Generate TikTok Script ] [ Generate Reels]│
└─────────────────────────────────────────────┘
```

---

#### 3. Generate TikTok Script

**User Action:** Sarah clicks "Generate TikTok Script"

**System Response:**

```
┌─────────────────────────────────────────────┐
│ TikTok Script (60 seconds)                  │
├─────────────────────────────────────────────┤
│ HOOK (0:00-0:03):                          │
│ "This 2-minute rule changed my life"       │
│ [Visual: Quick cut, energetic]             │
│                                             │
│ PROBLEM (0:04-0:15):                       │
│ "Ever procrastinate on tiny tasks? Making  │
│ the bed, sending that email, washing one   │
│ dish? They pile up and overwhelm you."     │
│ [Visual: Show cluttered desk, pile of tasks]│
│                                             │
│ SOLUTION (0:16-0:45):                      │
│ "The 2-minute rule: If it takes less than  │
│ 2 minutes, do it NOW. No exceptions."      │
│ [Visual: Timer, quick tasks being done]    │
│                                             │
│ CTA (0:46-0:60):                           │
│ "Try it today. You'll be shocked how much  │
│ you get done. Follow for more!"            │
│ [Visual: Before/after clean desk]          │
│                                             │
│ Trending Sound: "Productive vibes"         │
│ Hashtags: #productivity #2minuterule       │
│ #atomichabits #productivityhacks           │
│                                             │
│ [ Copy Script ] [ Add to Content Calendar ] │
└─────────────────────────────────────────────┘
```

---

#### 4. Add to Cross-Platform Content Calendar

**User Action:** Sarah clicks "Add to Content Calendar"

**System Response:** Calendar view opens

```
┌─────────────────────────────────────────────┐
│ Content Calendar - January 2026             │
├─────────────────────────────────────────────┤
│ Mon 15  │ Tue 16  │ Wed 17  │ Thu 18  │ Fri 19│
│         │         │         │         │       │
│ YouTube │         │ TikTok  │         │ Reels │
│ 8:30 AM │         │ 6:00 PM │         │ 5:00 PM│
│ "2-Min  │         │ "2-Min  │         │ "2-Min│
│ Rule"   │         │ Rule"   │         │ Rule" │
│ (8:30)  │         │ (0:60)  │         │ (0:45)│
│         │         │         │         │       │
│ Predicted views:                            │
│ YT: 35K | TikTok: 100K | Reels: 50K        │
│ Total: 185K cross-platform views            │
└─────────────────────────────────────────────┘
```

---

#### 5. User Outcome

**What Sarah Achieved:**
- ✅ Identified cross-platform opportunity (1 YouTube video → 3 pieces of content)
- ✅ Generated TikTok and Reels scripts automatically (saved 30-60 minutes each)
- ✅ Scheduled content across platforms (optimal posting times)
- ✅ Predicted total reach: 185K views (vs 35K YouTube-only)

**Time Saved:** 60-90 minutes (researching TikTok trends + writing scripts)

**Reach Amplified:** 5.3x (185K cross-platform vs 35K YouTube-only)

**Next Step:** Sarah films ONCE (YouTube version), then edits down for TikTok (60s) and Reels (45s)

---

## Summary: Total Time Savings

| User Flow | Manual Time | With 1in10killah | Time Saved |
|-----------|-------------|------------------|------------|
| 1. Find & research video idea | 2-3 hours | 10 minutes | **2.5 hours** |
| 2. Analyze competitor patterns | 5-10 hours | 3 minutes | **9 hours** |
| 3. Generate video brief | 30-60 min | 2 minutes | **45 min** |
| 4. Validate script | N/A (no validation) | 3 minutes | **Prevents flops** |
| 5. Predict performance | N/A (guesswork) | 2 minutes | **Reduces anxiety** |
| 6. Export client report | 2-3 hours | 5 minutes | **2.5 hours** |
| 7. Cross-platform repurposing | 60-90 min | 5 minutes | **75 min** |
| **TOTAL** | **12-20 hours** | **30 minutes** | **15-20 hours/week** |

---

**END OF USER FLOWS DOCUMENT**

**Next Steps:**
1. Validate flows with beta users
2. Use flows to guide UI/UX design
3. Build features following these exact workflows
4. Measure actual time savings post-launch

**Questions?** Open a GitHub issue or contact the product team.

**Status:** ✅ **USER FLOWS APPROVED FOR DESIGN & DEVELOPMENT**
