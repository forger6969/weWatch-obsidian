---
project: weWatch
type: ideas
---

# 💡 weWatch — Ideas

<!-- auto-appended by obsidian-note.sh idea -->

### 💡 External video search: Rutube API + VK API + Yandex Video scraping
> Add GET /api/v1/content/search/external?q=...&platforms=rutube,vk,yandex endpoint in content service. Rutube: public REST API (no key). VK: official VK API with service token (video.search method). Yandex: HTML scraping via __INITIAL_STATE__ JSON block. Results normalized to {platform, externalId, title, thumbnailUrl, duration, directUrl}. User taps result → MediaWebViewScreen with directUrl → yt-dlp already handles Rutube/VK extraction.
> Date: 2026-05-11 15:35

### 💡 MCP plugins research for WeWatch mobile dev
> 11 ta MCP plugin analiz qilindi. P0: Expo MCP, GitHub MCP, Sequential Thinking, Fetch. P1: React Native MCP (49 tools), MongoDB, Redis, Obsidian. P2: Playwright, Figma, Memory. Emirhan tanlashi kerak.
> Date: 2026-05-18 00:26
