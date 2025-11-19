# 1in10killah Technical Architecture

> **Complete System Design & Implementation Guide**

**Document Version:** 1.0
**Last Updated:** November 19, 2025
**Status:** Approved for Implementation

---

## Table of Contents

1. [System Overview](#system-overview)
2. [Chrome Extension Architecture](#chrome-extension-architecture)
3. [Backend API Architecture](#backend-api-architecture)
4. [Database Schema](#database-schema)
5. [External API Integrations](#external-api-integrations)
6. [Data Flow Diagrams](#data-flow-diagrams)
7. [Security & Privacy](#security--privacy)
8. [Performance & Scalability](#performance--scalability)
9. [Deployment & Infrastructure](#deployment--infrastructure)
10. [Code Examples](#code-examples)

---

## 1. System Overview

### 1.1 High-Level Architecture

```
┌──────────────────────────────────────────────────────────┐
│                   USER ENVIRONMENT                        │
│                                                          │
│  ┌──────────────────┐         ┌─────────────────────┐  │
│  │  Chrome Browser  │         │  Mobile App         │  │
│  │  ┌────────────┐  │         │  (React Native)     │  │
│  │  │ Extension  │  │         │  [Phase 3]          │  │
│  │  │ (Manifest  │  │         └─────────────────────┘  │
│  │  │  V3)       │  │                │                  │
│  │  └──────┬─────┘  │                │                  │
│  └─────────┼────────┘                │                  │
│            │                         │                  │
└────────────┼─────────────────────────┼──────────────────┘
             │                         │
             │    HTTPS/WSS            │
             │                         │
┌────────────▼─────────────────────────▼──────────────────┐
│               CLOUDFLARE CDN                            │
│  (DDoS Protection, Edge Caching, SSL Termination)        │
└────────────┬───────────────────────────────────────────┘
             │
┌────────────▼─────────────────────────────────────────────┐
│              BACKEND API (Vercel)                        │
│                                                          │
│  ┌─────────────────┐  ┌──────────────┐ ┌──────────────┐ │
│  │  Express.js     │  │  BullMQ      │ │  Supabase    │ │
│  │  REST API       │  │  Job Queue   │ │  Auth        │ │
│  └────────┬────────┘  └──────┬───────┘ └──────┬───────┘ │
│           │                  │                │          │
└───────────┼──────────────────┼────────────────┼──────────┘
            │                  │                │
┌───────────▼──────────────────▼────────────────▼──────────┐
│                    DATA LAYER                            │
│                                                          │
│  ┌─────────────┐  ┌──────────┐  ┌────────────────────┐  │
│  │ PostgreSQL  │  │  Redis   │  │  Chrome Storage    │  │
│  │ (Vercel)    │  │  (Cache) │  │  (Local/Sync)      │  │
│  └─────────────┘  └──────────┘  └────────────────────┘  │
└──────────────────────────────────────────────────────────┘
            │
┌───────────▼──────────────────────────────────────────────┐
│              EXTERNAL APIS                               │
│                                                          │
│  ┌──────────────┐ ┌───────────┐ ┌───────────────────┐  │
│  │  YouTube     │ │  AI APIs  │ │  Keyword APIs     │  │
│  │  Data API v3 │ │  (OpenAI, │ │  (DataForSEO)     │  │
│  │              │ │  Claude,  │ │                   │  │
│  │              │ │  Gemini)  │ │                   │  │
│  └──────────────┘ └───────────┘ └───────────────────┘  │
└──────────────────────────────────────────────────────────┘
```

### 1.2 Technology Stack

**Frontend (Chrome Extension):**
- React 18.2+ (UI framework)
- TypeScript 5.0+ (type safety)
- Vite 5.0+ (build tool)
- Tailwind CSS 3.4+ (styling)
- Zustand 4.5+ (state management)
- Shadcn UI + Radix UI (components)

**Backend:**
- Node.js 20 LTS (runtime)
- Express.js 4.18+ (web framework)
- Prisma 5.8+ (ORM)
- BullMQ 5.1+ (job queue)
- Zod 3.22+ (schema validation)

**Database & Caching:**
- PostgreSQL 16 (primary database)
- Redis 7.2+ (caching, session storage, job queue)
- IndexedDB (client-side large data storage)

**AI/ML:**
- OpenAI GPT-4 Turbo (script analysis, insights)
- Anthropic Claude 3.5 Sonnet (brief generation, pattern analysis)
- Google Gemini 2.5 Flash (cost-efficient processing)
- Chrome Built-in AI / Gemini Nano (client-side, privacy-first)
- TensorFlow.js 4.15+ (performance predictor model)

**Infrastructure:**
- Vercel (backend hosting, serverless functions)
- Cloudflare (CDN, DDoS protection, edge caching)
- Supabase (authentication, realtime subscriptions)
- Stripe (payment processing)
- Sentry (error tracking)
- PostHog (product analytics)

---

## 2. Chrome Extension Architecture

### 2.1 Extension Structure

```
1in10killah-extension/
├── manifest.json                 # Manifest V3 configuration
├── src/
│   ├── background/
│   │   └── service-worker.ts     # Background service worker
│   ├── content/
│   │   ├── youtube.tsx           # YouTube content script
│   │   ├── 1of10.tsx             # 1of10.com content script
│   │   └── components/
│   │       ├── Overlay.tsx       # Metadata overlay UI
│   │       └── Badge.tsx         # Outlier badge component
│   ├── sidepanel/
│   │   ├── App.tsx               # Side panel main app
│   │   ├── pages/
│   │   │   ├── Bookmarks.tsx
│   │   │   ├── Analyzer.tsx
│   │   │   ├── BriefGenerator.tsx
│   │   │   └── Settings.tsx
│   │   └── components/
│   │       ├── PatternReport.tsx
│   │       ├── VideoCard.tsx
│   │       └── ExportModal.tsx
│   ├── popup/
│   │   └── Popup.tsx             # Extension popup (settings)
│   ├── lib/
│   │   ├── api-client.ts         # Backend API client
│   │   ├── youtube-scraper.ts    # YouTube DOM scraper
│   │   ├── storage.ts            # Chrome storage wrapper
│   │   └── ai-client.ts          # AI API client (multi-provider)
│   ├── types/
│   │   ├── index.d.ts
│   │   └── youtube.d.ts
│   └── utils/
│       ├── message-passing.ts    # Chrome message API helpers
│       └── dom-helpers.ts
├── public/
│   ├── icons/
│   │   ├── icon-16.png
│   │   ├── icon-48.png
│   │   └── icon-128.png
│   └── sidepanel.html
├── vite.config.ts
├── tsconfig.json
└── package.json
```

### 2.2 Manifest V3 Configuration

**manifest.json:**

```json
{
  "manifest_version": 3,
  "name": "1in10killah",
  "version": "1.0.0",
  "description": "AI-powered YouTube creator research tool. Find winning video ideas, analyze patterns, generate briefs.",

  "permissions": [
    "storage",
    "tabs",
    "sidePanel",
    "notifications",
    "contextMenus",
    "webNavigation"
  ],

  "host_permissions": [
    "https://www.youtube.com/*",
    "https://1of10.com/*",
    "https://api.1in10killah.com/*"
  ],

  "background": {
    "service_worker": "background/service-worker.js",
    "type": "module"
  },

  "content_scripts": [
    {
      "matches": ["https://www.youtube.com/*"],
      "js": ["content/youtube.js"],
      "css": ["content/youtube.css"],
      "run_at": "document_idle"
    },
    {
      "matches": ["https://1of10.com/*"],
      "js": ["content/1of10.js"],
      "css": ["content/1of10.css"],
      "run_at": "document_idle"
    }
  ],

  "side_panel": {
    "default_path": "sidepanel.html"
  },

  "action": {
    "default_popup": "popup.html",
    "default_icon": {
      "16": "icons/icon-16.png",
      "48": "icons/icon-48.png",
      "128": "icons/icon-128.png"
    }
  },

  "icons": {
    "16": "icons/icon-16.png",
    "48": "icons/icon-48.png",
    "128": "icons/icon-128.png"
  },

  "web_accessible_resources": [
    {
      "resources": ["assets/*"],
      "matches": ["https://www.youtube.com/*", "https://1of10.com/*"]
    }
  ]
}
```

### 2.3 Component Communication

**Message Passing Architecture:**

```typescript
// src/utils/message-passing.ts

// Message types
type MessageType =
  | 'ANALYZE_PATTERNS'
  | 'GENERATE_BRIEF'
  | 'FETCH_VIDEO_METADATA'
  | 'EXPORT_DATA'
  | 'UPDATE_BOOKMARK';

interface Message<T = any> {
  type: MessageType;
  payload: T;
}

// Content Script → Service Worker
export const sendToBackground = <T = any>(
  message: Message
): Promise<T> => {
  return chrome.runtime.sendMessage(message);
};

// Side Panel → Service Worker
export const sendFromSidePanel = <T = any>(
  message: Message
): Promise<T> => {
  return chrome.runtime.sendMessage(message);
};

// Service Worker → Content Script
export const sendToContentScript = <T = any>(
  tabId: number,
  message: Message
): Promise<T> => {
  return chrome.tabs.sendMessage(tabId, message);
};

// Long-lived connection (for real-time updates)
export const createPort = (name: string) => {
  return chrome.runtime.connect({ name });
};
```

### 2.4 Storage Strategy

**Multi-Layer Storage:**

```typescript
// src/lib/storage.ts

// Layer 1: chrome.storage.sync (user preferences, synced across devices)
export const syncStorage = {
  async get<T>(key: string): Promise<T | null> {
    const result = await chrome.storage.sync.get(key);
    return result[key] || null;
  },

  async set(key: string, value: any): Promise<void> {
    await chrome.storage.sync.set({ [key]: value });
  },

  // 4KB per item limit, 100KB total
  // Use for: user tier, preferences, settings
};

// Layer 2: chrome.storage.local (5MB limit, fast access)
export const localStorage = {
  async get<T>(key: string): Promise<T | null> {
    const result = await chrome.storage.local.get(key);
    return result[key] || null;
  },

  async set(key: string, value: any): Promise<void> {
    await chrome.storage.local.set({ [key]: value });
  },

  // Use for: video cache, bookmarks, recent searches
};

// Layer 3: IndexedDB (unlimited storage, complex queries)
import { openDB, DBSchema } from 'idb';

interface VideoDB extends DBSchema {
  videos: {
    key: string; // video ID
    value: {
      id: string;
      title: string;
      thumbnail: Blob; // Store as binary
      transcript: string;
      metadata: VideoMetadata;
      cachedAt: number;
    };
    indexes: { 'by-cached': number };
  };
  analyses: {
    key: string; // analysis ID
    value: PatternAnalysis;
  };
}

const db = await openDB<VideoDB>('1in10killah-db', 1, {
  upgrade(db) {
    const videoStore = db.createObjectStore('videos', { keyPath: 'id' });
    videoStore.createIndex('by-cached', 'cachedAt');

    db.createObjectStore('analyses', { keyPath: 'id' });
  },
});

// Use for: thumbnails (binary), large transcripts, analysis results
```

---

## 3. Backend API Architecture

### 3.1 API Structure

```
backend/
├── src/
│   ├── index.ts                  # Express app entry point
│   ├── routes/
│   │   ├── auth.ts               # Authentication routes
│   │   ├── videos.ts             # Video metadata endpoints
│   │   ├── analyze.ts            # Pattern analysis endpoints
│   │   ├── briefs.ts             # Video brief generation
│   │   ├── export.ts             # Data export endpoints
│   │   └── webhooks.ts           # Stripe webhooks
│   ├── services/
│   │   ├── youtube.service.ts    # YouTube API wrapper
│   │   ├── ai.service.ts         # AI provider abstraction
│   │   ├── keyword.service.ts    # Keyword research
│   │   └── analytics.service.ts  # User analytics
│   ├── jobs/
│   │   ├── analyze-patterns.job.ts
│   │   ├── generate-brief.job.ts
│   │   └── export-data.job.ts
│   ├── middleware/
│   │   ├── auth.ts               # JWT validation
│   │   ├── rate-limit.ts         # Rate limiting
│   │   └── error-handler.ts      # Global error handling
│   ├── lib/
│   │   ├── prisma.ts             # Prisma client
│   │   ├── redis.ts              # Redis client
│   │   └── queue.ts              # BullMQ queue
│   └── types/
│       └── index.d.ts
├── prisma/
│   ├── schema.prisma
│   └── migrations/
├── tests/
│   ├── unit/
│   └── integration/
├── .env.example
└── package.json
```

### 3.2 Key API Endpoints

**REST API Specification:**

```typescript
// GET /api/v1/videos/:videoId
// Fetch video metadata (cached if available)
interface GetVideoResponse {
  id: string;
  title: string;
  channelName: string;
  views: number;
  likes: number;
  comments: number;
  engagementRate: number;
  duration: number;
  publishDate: string;
  tags: string[];
  keywordData?: {
    searchVolume: number;
    seoDifficulty: number;
    trend: 'rising' | 'stable' | 'declining';
  };
}

// POST /api/v1/analyze/patterns
// Analyze patterns across multiple videos
interface AnalyzePatternsRequest {
  videoIds: string[]; // 2-50 videos
  userId: string;
}

interface AnalyzePatternsResponse {
  analysisId: string;
  patterns: {
    titles: TitlePattern[];
    thumbnails: ThumbnailPattern[];
    hooks: HookPattern[];
    metadata: MetadataInsight[];
  };
  recommendations: string[];
  createdAt: string;
}

// POST /api/v1/briefs/generate
// Generate video brief from outlier
interface GenerateBriefRequest {
  videoId: string;
  userId: string;
  format?: 'markdown' | 'notion' | 'google-docs';
}

interface GenerateBriefResponse {
  briefId: string;
  content: string; // Markdown or HTML
  sections: {
    concept: string;
    hook: { script: string; visual: string };
    body: BodySection[];
    cta: string;
    seo: { keywords: string[]; tags: string[] };
    thumbnailIdeas: string[];
  };
}

// POST /api/v1/export
// Export data to various formats
interface ExportRequest {
  videoIds: string[];
  format: 'csv' | 'excel' | 'pdf';
  fields: string[];
  sort?: { field: string; order: 'asc' | 'desc' };
}

interface ExportResponse {
  downloadUrl: string; // Pre-signed URL, expires in 1 hour
  expiresAt: string;
}
```

### 3.3 Service Worker (Background Script)

```typescript
// src/background/service-worker.ts

import { analyzePatterns, generateBrief } from './api-client';

// Listen for messages from content scripts and side panel
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  handleMessage(message, sender, sendResponse);
  return true; // Keep channel open for async response
});

async function handleMessage(
  message: Message,
  sender: chrome.runtime.MessageSender,
  sendResponse: (response: any) => void
) {
  try {
    switch (message.type) {
      case 'ANALYZE_PATTERNS': {
        const { videoIds } = message.payload;
        const result = await analyzePatterns(videoIds);
        sendResponse({ success: true, data: result });
        break;
      }

      case 'GENERATE_BRIEF': {
        const { videoId } = message.payload;
        const result = await generateBrief(videoId);
        sendResponse({ success: true, data: result });
        break;
      }

      case 'FETCH_VIDEO_METADATA': {
        const { videoId } = message.payload;

        // Check cache first
        const cached = await getCachedVideo(videoId);
        if (cached && !isStale(cached)) {
          sendResponse({ success: true, data: cached, cached: true });
          return;
        }

        // Fetch from API
        const metadata = await fetchVideoMetadata(videoId);
        await cacheVideo(videoId, metadata);
        sendResponse({ success: true, data: metadata, cached: false });
        break;
      }

      default:
        sendResponse({ success: false, error: 'Unknown message type' });
    }
  } catch (error) {
    console.error('Service worker error:', error);
    sendResponse({ success: false, error: error.message });
  }
}

// Context menu integration
chrome.runtime.onInstalled.addListener(() => {
  chrome.contextMenus.create({
    id: 'analyze-video',
    title: 'Analyze with 1in10killah',
    contexts: ['link'],
    documentUrlPatterns: ['https://www.youtube.com/*', 'https://1of10.com/*'],
  });
});

chrome.contextMenus.onClicked.addListener(async (info, tab) => {
  if (info.menuItemId === 'analyze-video' && info.linkUrl) {
    const videoId = extractVideoId(info.linkUrl);
    if (videoId) {
      // Open side panel and trigger analysis
      await chrome.sidePanel.open({ tabId: tab.id });
      // Send message to side panel to analyze this video
      chrome.runtime.sendMessage({
        type: 'ANALYZE_SINGLE_VIDEO',
        payload: { videoId },
      });
    }
  }
});
```

---

## 4. Database Schema

### 4.1 Prisma Schema

```prisma
// prisma/schema.prisma

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id            String   @id @default(uuid())
  email         String   @unique
  tier          Tier     @default(FREE)
  stripeCustomerId String? @unique

  createdAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt

  bookmarks     Bookmark[]
  analyses      Analysis[]
  apiUsage      ApiUsage[]

  @@index([email])
}

enum Tier {
  FREE
  CREATOR
  PRO
  AGENCY
}

model Video {
  id            String   @id // YouTube video ID
  title         String
  channelName   String
  channelId     String
  views         BigInt
  likes         Int?
  comments      Int?
  duration      Int      // seconds
  publishDate   DateTime
  thumbnailUrl  String
  transcript    String?  @db.Text
  tags          String[]

  // Computed fields
  engagementRate Float?

  // Keyword data (nullable if not yet fetched)
  searchVolume   Int?
  seoDifficulty  Int?
  trend          String?

  fetchedAt     DateTime @default(now())
  updatedAt     DateTime @updatedAt

  bookmarks     Bookmark[]
  analysisVideos AnalysisVideo[]

  @@index([channelId])
  @@index([fetchedAt])
}

model Bookmark {
  id          String   @id @default(uuid())
  userId      String
  videoId     String
  customTags  String[]
  notes       String?  @db.Text

  createdAt   DateTime @default(now())

  user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  video       Video    @relation(fields: [videoId], references: [id], onDelete: Cascade)

  @@unique([userId, videoId])
  @@index([userId])
}

model Analysis {
  id          String   @id @default(uuid())
  userId      String
  type        AnalysisType

  // Pattern analysis results (JSONB for flexibility)
  patterns    Json

  createdAt   DateTime @default(now())

  user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  videos      AnalysisVideo[]

  @@index([userId, createdAt])
}

enum AnalysisType {
  PATTERN
  SCRIPT
  PERFORMANCE
}

model AnalysisVideo {
  analysisId  String
  videoId     String

  analysis    Analysis @relation(fields: [analysisId], references: [id], onDelete: Cascade)
  video       Video    @relation(fields: [videoId], references: [id], onDelete: Cascade)

  @@id([analysisId, videoId])
}

model ApiUsage {
  id          String   @id @default(uuid())
  userId      String
  endpoint    String   // 'analyze_patterns', 'generate_brief', etc.
  provider    String?  // 'openai', 'claude', 'youtube', etc.
  cost        Decimal  @db.Decimal(10, 4) // in USD
  tokensUsed  Int?

  createdAt   DateTime @default(now())

  user        User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@index([userId, createdAt])
  @@index([endpoint, createdAt])
}

model KeywordCache {
  keyword       String   @id
  searchVolume  Int
  seoDifficulty Int
  trend         String
  relatedKeywords String[]

  cachedAt      DateTime @default(now())
  expiresAt     DateTime

  @@index([expiresAt])
}
```

---

## 5. External API Integrations

### 5.1 YouTube Data API v3

**Quota Management:**

```typescript
// src/services/youtube.service.ts

import { google } from 'googleapis';
import { redisClient } from '../lib/redis';

const youtube = google.youtube('v3');
const API_KEY = process.env.YOUTUBE_API_KEY;
const DAILY_QUOTA = 10000; // units/day

class YouTubeService {
  private quotaUsed = 0;

  async getVideoMetadata(videoId: string) {
    // Check cache first (7-day TTL)
    const cacheKey = `yt:video:${videoId}`;
    const cached = await redisClient.get(cacheKey);
    if (cached) {
      return JSON.parse(cached);
    }

    // Check quota
    await this.checkQuota(1); // videos.list costs 1 unit

    // Fetch from YouTube API
    const response = await youtube.videos.list({
      key: API_KEY,
      id: [videoId],
      part: ['snippet', 'statistics', 'contentDetails'],
    });

    const video = response.data.items?.[0];
    if (!video) throw new Error('Video not found');

    const metadata = {
      id: videoId,
      title: video.snippet.title,
      channelName: video.snippet.channelTitle,
      views: parseInt(video.statistics.viewCount || '0'),
      likes: parseInt(video.statistics.likeCount || '0'),
      comments: parseInt(video.statistics.commentCount || '0'),
      duration: this.parseDuration(video.contentDetails.duration),
      publishDate: video.snippet.publishedAt,
      thumbnailUrl: video.snippet.thumbnails.high.url,
      tags: video.snippet.tags || [],
    };

    // Cache for 7 days
    await redisClient.setex(cacheKey, 7 * 24 * 60 * 60, JSON.stringify(metadata));

    // Track quota usage
    this.quotaUsed += 1;
    await this.recordQuotaUsage('videos.list', 1);

    return metadata;
  }

  async getTranscript(videoId: string) {
    // Check cache (30-day TTL)
    const cacheKey = `yt:transcript:${videoId}`;
    const cached = await redisClient.get(cacheKey);
    if (cached) return cached;

    // Check quota (captions.list costs 50 units!)
    await this.checkQuota(50);

    const response = await youtube.captions.list({
      key: API_KEY,
      videoId,
      part: ['snippet'],
    });

    // Download caption track (simplified - real implementation needs OAuth)
    const trackId = response.data.items?.[0]?.id;
    if (!trackId) throw new Error('No captions available');

    // ... download and parse SRT file ...

    // Cache for 30 days (transcripts rarely change)
    await redisClient.setex(cacheKey, 30 * 24 * 60 * 60, transcript);

    this.quotaUsed += 50;
    await this.recordQuotaUsage('captions.list', 50);

    return transcript;
  }

  private async checkQuota(units: number) {
    const today = new Date().toISOString().split('T')[0]; // YYYY-MM-DD
    const quotaKey = `quota:${today}`;

    const used = await redisClient.get(quotaKey);
    const currentUsage = used ? parseInt(used) : 0;

    if (currentUsage + units > DAILY_QUOTA) {
      throw new Error('Daily YouTube API quota exceeded. Try again tomorrow.');
    }
  }

  private async recordQuotaUsage(endpoint: string, units: number) {
    const today = new Date().toISOString().split('T')[0];
    const quotaKey = `quota:${today}`;

    await redisClient.incrby(quotaKey, units);
    await redisClient.expireat(quotaKey, this.getTomorrowMidnightPST());

    // Also record in database for analytics
    await prisma.apiUsage.create({
      data: {
        userId: 'system',
        endpoint,
        provider: 'youtube',
        cost: 0, // YouTube API is free
        tokensUsed: units,
      },
    });
  }

  private getTomorrowMidnightPST(): number {
    const now = new Date();
    const tomorrow = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1);
    const pst = new Date(tomorrow.toLocaleString('en-US', { timeZone: 'America/Los_Angeles' }));
    return Math.floor(pst.getTime() / 1000);
  }

  private parseDuration(isoDuration: string): number {
    // Parse ISO 8601 duration (PT8M30S → 510 seconds)
    const match = isoDuration.match(/PT(?:(\d+)H)?(?:(\d+)M)?(?:(\d+)S)?/);
    if (!match) return 0;

    const hours = parseInt(match[1] || '0');
    const minutes = parseInt(match[2] || '0');
    const seconds = parseInt(match[3] || '0');

    return hours * 3600 + minutes * 60 + seconds;
  }
}

export const youtubeService = new YouTubeService();
```

### 5.2 AI Provider Abstraction

```typescript
// src/services/ai.service.ts

interface AIProvider {
  name: string;
  generate(prompt: string, options?: any): Promise<string>;
  estimateCost(prompt: string): number;
}

class OpenAIProvider implements AIProvider {
  name = 'openai';

  async generate(prompt: string, options = {}) {
    const response = await openai.chat.completions.create({
      model: 'gpt-4-turbo',
      messages: [{ role: 'user', content: prompt }],
      temperature: 0.7,
      max_tokens: 2000,
      ...options,
    });

    return response.choices[0].message.content;
  }

  estimateCost(prompt: string): number {
    const tokens = prompt.length / 4; // Rough estimate
    return (tokens / 1000) * 0.01; // $0.01 per 1K tokens (GPT-4 Turbo)
  }
}

class ClaudeProvider implements AIProvider {
  name = 'claude';

  async generate(prompt: string, options = {}) {
    const response = await anthropic.messages.create({
      model: 'claude-3-5-sonnet-20241022',
      max_tokens: 4000,
      messages: [{ role: 'user', content: prompt }],
      ...options,
    });

    return response.content[0].text;
  }

  estimateCost(prompt: string): number {
    const tokens = prompt.length / 4;
    return (tokens / 1000) * 0.003; // $0.003 per 1K tokens (Claude 3.5 Sonnet)
  }
}

class AIService {
  private providers: Map<string, AIProvider> = new Map();

  constructor() {
    this.providers.set('openai', new OpenAIProvider());
    this.providers.set('claude', new ClaudeProvider());
    this.providers.set('gemini', new GeminiProvider());
  }

  async generate(
    task: 'analyze' | 'brief' | 'script',
    prompt: string,
    options?: { provider?: string }
  ): Promise<string> {
    // Route to optimal provider based on task
    const providerName = options?.provider || this.selectProvider(task);
    const provider = this.providers.get(providerName);

    if (!provider) throw new Error(`Provider ${providerName} not found`);

    // Generate
    const result = await provider.generate(prompt);

    // Track cost
    const cost = provider.estimateCost(prompt);
    await this.recordCost(provider.name, cost);

    return result;
  }

  private selectProvider(task: string): string {
    // Task-specific routing for cost optimization
    switch (task) {
      case 'analyze':
        return 'claude'; // Best for pattern analysis
      case 'brief':
        return 'claude'; // Best for long-form structured output
      case 'script':
        return 'openai'; // GPT-4 Turbo is faster for short analysis
      default:
        return 'gemini'; // Cheapest fallback
    }
  }

  private async recordCost(provider: string, cost: number) {
    await prisma.apiUsage.create({
      data: {
        userId: 'system',
        endpoint: 'ai_generation',
        provider,
        cost,
      },
    });
  }
}

export const aiService = new AIService();
```

---

## 6. Data Flow Diagrams

### 6.1 Smart Outlier Analyzer Flow

```
┌─────────────────────────────────────────────────────────┐
│ 1. USER TRIGGERS ANALYSIS                               │
│    (Clicks "Analyze Patterns" with 10 bookmarked videos)│
└────────────────┬────────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 2. CONTENT SCRIPT sends message to SERVICE WORKER      │
│    Message: { type: 'ANALYZE_PATTERNS',                │
│               payload: { videoIds: [...] } }            │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 3. SERVICE WORKER sends request to BACKEND API         │
│    POST /api/v1/analyze/patterns                       │
│    Body: { videoIds: [...], userId: '...' }            │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 4. BACKEND creates JOB in BullMQ queue                 │
│    Job: { type: 'analyze-patterns', data: {...} }      │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 5. JOB WORKER processes videos (parallel)              │
│    For each video:                                     │
│    a) Check cache (Redis)                              │
│    b) If miss → Fetch from YouTube API                 │
│    c) Cache result (7-day TTL)                         │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 6. WORKER sends all video data to AI API (Claude)      │
│    Prompt: "Analyze these 10 videos for patterns..."   │
│    Returns: { titles: [...], thumbnails: [...], ... }  │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 7. WORKER saves analysis to DATABASE                   │
│    Table: analyses                                     │
│    { id, userId, patterns (JSONB), createdAt }         │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 8. BACKEND returns analysis ID to SERVICE WORKER       │
│    Response: { analysisId: '...', patterns: {...} }    │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 9. SERVICE WORKER sends result to SIDE PANEL           │
│    Message: { type: 'ANALYSIS_COMPLETE', data: {...} } │
└────────────────┬───────────────────────────────────────┘
                 │
                 ▼
┌────────────────────────────────────────────────────────┐
│ 10. SIDE PANEL renders pattern report                  │
│     UI updates with: title patterns, thumbnail          │
│     patterns, hook analysis, recommendations            │
└─────────────────────────────────────────────────────────┘
```

---

## 7. Security & Privacy

### 7.1 Authentication Flow

```typescript
// Using Supabase Auth + JWT

// 1. User signs up
const { user, error } = await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'securepassword',
});

// 2. Backend validates JWT on each request
app.use(async (req, res, next) => {
  const token = req.headers.authorization?.replace('Bearer ', '');

  if (!token) {
    return res.status(401).json({ error: 'Unauthorized' });
  }

  try {
    const { data: { user }, error } = await supabase.auth.getUser(token);

    if (error || !user) {
      return res.status(401).json({ error: 'Invalid token' });
    }

    req.user = user;
    next();
  } catch (error) {
    return res.status(401).json({ error: 'Auth error' });
  }
});
```

### 7.2 Data Privacy

**Principles:**
1. **Minimal Data Collection** - Only collect what's necessary for features
2. **User-Controlled Data** - Users can export/delete all their data
3. **Encryption at Rest** - PostgreSQL with encryption enabled
4. **Encryption in Transit** - HTTPS only, TLS 1.3+
5. **No Selling Data** - Never sell user data to third parties

**GDPR Compliance:**
- Right to access: `/api/v1/users/me/data` (export all data)
- Right to delete: `/api/v1/users/me` DELETE (hard delete)
- Data portability: Export in JSON/CSV formats
- Privacy policy: Clear explanation of data usage

---

## 8. Performance & Scalability

### 8.1 Caching Strategy

**Multi-Layer Caching:**

```
┌─────────────────────────────────────────────┐
│ Layer 1: Browser Memory (In-Memory Cache)   │
│ TTL: 5 minutes                              │
│ Use: Recently viewed videos, UI state       │
└────────────────┬────────────────────────────┘
                 │ Miss
                 ▼
┌─────────────────────────────────────────────┐
│ Layer 2: chrome.storage.local               │
│ TTL: 7 days                                 │
│ Use: Video metadata, bookmarks              │
└────────────────┬────────────────────────────┘
                 │ Miss
                 ▼
┌─────────────────────────────────────────────┐
│ Layer 3: Redis (Backend)                    │
│ TTL: 7-30 days                              │
│ Use: API responses, transcripts, patterns   │
└────────────────┬────────────────────────────┘
                 │ Miss
                 ▼
┌─────────────────────────────────────────────┐
│ Layer 4: PostgreSQL (Database)              │
│ TTL: Indefinite                             │
│ Use: User data, analyses, historical records│
└─────────────────────────────────────────────┘
```

### 8.2 Load Testing Targets

**Performance Benchmarks:**
- API response time (p95): <500ms
- Side panel load time: <300ms
- Extension background script CPU: <5% (idle)
- Memory usage: <50MB (extension + side panel)
- Database queries (p95): <100ms
- Redis cache hit rate: >85%

**Scale Targets (Year 1):**
- Support 10,000 concurrent users
- Handle 1M API requests/day
- Store 10M video metadata records
- Process 100K AI analyses/month

---

## 9. Deployment & Infrastructure

### 9.1 CI/CD Pipeline

```yaml
# .github/workflows/deploy.yml

name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 20
      - run: npm ci
      - run: npm run test
      - run: npm run lint

  build-extension:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm run build:extension
      - uses: actions/upload-artifact@v3
        with:
          name: extension-build
          path: dist/

  deploy-backend:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm ci
      - run: npm run build:backend
      - uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
          vercel-args: '--prod'

  submit-chrome-store:
    needs: build-extension
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v3
        with:
          name: extension-build
      - run: |
          # Upload to Chrome Web Store (manual for now)
          echo "Extension built successfully. Manual Chrome Web Store submission required."
```

---

## 10. Code Examples

### 10.1 YouTube Content Script

```typescript
// src/content/youtube.tsx

import { createRoot } from 'react-dom/client';
import { MetadataBadge } from './components/Badge';

// Detect YouTube SPA navigation
let currentUrl = location.href;
new MutationObserver(() => {
  if (location.href !== currentUrl) {
    currentUrl = location.href;
    if (isVideoPage()) {
      injectMetadata();
    }
  }
}).observe(document, { subtree: true, childList: true });

// Also listen to YouTube's custom events
window.addEventListener('yt-navigate-finish', () => {
  if (isVideoPage()) {
    injectMetadata();
  }
});

function isVideoPage(): boolean {
  return location.pathname === '/watch' && location.search.includes('v=');
}

async function injectMetadata() {
  const videoId = new URLSearchParams(location.search).get('v');
  if (!videoId) return;

  // Wait for video info element to load
  const infoElement = await waitForElement('#info');

  // Create badge container
  const badgeContainer = document.createElement('div');
  badgeContainer.id = '1in10killah-badge';
  infoElement.appendChild(badgeContainer);

  // Fetch metadata
  const metadata = await chrome.runtime.sendMessage({
    type: 'FETCH_VIDEO_METADATA',
    payload: { videoId },
  });

  // Render badge
  const root = createRoot(badgeContainer);
  root.render(<MetadataBadge metadata={metadata.data} />);
}

function waitForElement(selector: string, timeout = 5000): Promise<Element> {
  return new Promise((resolve, reject) => {
    const element = document.querySelector(selector);
    if (element) return resolve(element);

    const observer = new MutationObserver(() => {
      const element = document.querySelector(selector);
      if (element) {
        observer.disconnect();
        resolve(element);
      }
    });

    observer.observe(document.body, { childList: true, subtree: true });

    setTimeout(() => {
      observer.disconnect();
      reject(new Error(`Element ${selector} not found within ${timeout}ms`));
    }, timeout);
  });
}
```

---

**END OF ARCHITECTURE DOCUMENT**

**Next Steps:**
1. Review architecture with team
2. Set up development environment
3. Begin implementation following this blueprint

**Status:** ✅ **ARCHITECTURE APPROVED FOR IMPLEMENTATION**
