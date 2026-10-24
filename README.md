> 🚀 **Run Directly on Apify Cloud (100% No Cookie / No Login Required):**
> 👉 **[Launch Weibo & BlackCat Intelligence Scraper on Apify Store](https://apify.com/axon-studio/weibo-scraper)**
# Weibo Scraper — Chinese Social Intelligence & BlackCat API (100% No Cookie / No Login)

Extract Chinese public opinion, real-time trending topics, creator timelines, comment threads, and consumer complaints from **Sina Weibo (新浪微博)** and **BlackCat (新浪黑猫投诉)** — China's dominant microblogging and public-opinion platform with **580M+ monthly active users**.

Built for **AI/LLM training corpora, Chinese consumer equity research (alt-data), global brand monitoring agencies, KOL due diligence, and automated RAG workflows** (n8n, Make, Dify, LangGraph, Claude MCP). **No API key, no VPN, and no Weibo login or cookies required.** Users on the **Apify Free plan can extract up to 1,111 Weibo items per month for free**.

---

## Why Choose This Weibo Scraper (Features)

| Weibo Scraper Capability | Built-In Advantage |
| :--- | :--- |
| **Managed Cloud Session Pool (No Cookie Needed)** | Runs all 9 modes—including **`user_posts` (creator timelines)** and **BlackCat keyword search**—completely cookie-free via our built-in managed session pool and PC/Mobile dual-engine fallback. |
| **Deep Weibo Search (>1,000 Posts/Run)** | Bypasses Weibo's 30-post anonymous page limit using **5 content streams** + **80+ unbiased Chinese grammatical particles** (`的`, `了`, `在`, `是`...) without distorting sentiment polarity. |
| **Auto EN ↔ ZH Brand Localization** | Searching an English brand on Weibo (e.g., `Tesla`, `Nike`, `Luckin`) automatically translates and searches both the Chinese (`特斯拉`, `耐克`, `瑞幸咖啡`) and English terms simultaneously. |
| **Author Followers Included Free** | Every Weibo `search` and `user_posts` row includes `authorFollowers`, `authorVerified`, and `authorVerifiedReason` at no extra cost. |
| **Full Text Expansion (`>140` chars)** | Automatically expands truncated Weibo long posts (`...全文`) via dual PC & Mobile extend endpoints. |
| **Chinese & English Sentiment Analysis** | Zero-RAM sentiment lexicon with **Chinese negation reversal** (`"不满意"` → negative, `"不错"` → positive) and degree weighting. |
| **Weibo IP Province Geolocation (`regionEn`)** | Automatically maps Chinese IP location labels (`发布于 广东`) into standardized English names (`Guangdong`, `Shanghai`, `Beijing`). |
| **256 MB RAM Real-Time Streaming** | Streams records to your Dataset in real-time batches of 10 rows on just **256 MB RAM**—preserving every scraped batch if a run stops early. |

---

## How to Scrape Weibo in 3 Easy Steps

1. **Select a Weibo `mode`** — Choose from 9 modes (`search`, `realtime_search`, `user_posts`, `hot_timeline`, `hot_search`, `user_profile`, `post_details`, `post_comments`, or `complaints`).
2. **Enter your target** — Type a brand or topic in **English or Chinese** (e.g., `Tesla`, `Luckin`, `Apple`, `瑞幸咖啡`, `人工智能`) or paste Weibo User UIDs / Post URLs.
3. **Click "Start"** — Download your Weibo data in **JSON, CSV, Excel, or Parquet**, or connect via API, Webhooks, n8n, Make, or Claude MCP.

---

## Weibo Scraper Use Cases

| Buyer Profile | Weibo & BlackCat Use Case |
| :--- | :--- |
| **AI / LLM Training Data Teams** | Real-time Simplified Chinese Weibo microblog text and comment threads for SFT, RLHF, and current-events RAG grounding |
| **Hedge Funds & Equity Research** | Track Weibo brand mention velocity, BlackCat complaint spikes, and hot-search momentum on Chinese consumer stocks (BYD, POP MART, Anta, Luckin, Yum China, NIO, Xiaomi) |
| **Brand Monitoring & PR Agencies** | Real-time tracking of Western brand mentions on Weibo, campaign reception, and crisis detection |
| **KOL & Influencer Marketing** | Evaluate Weibo KOLs by follower count, verification badge (`黄V` / `蓝V`), timeline engagement, and audience province distribution |
| **Academic NLP & Policy Analysts** | Chinese microblog corpus with labeled sentiment and regional conversation distribution (`regionEn`) |

---

## Weibo Scraper Input & 9 Modes Configuration

All parameters are documented in the **Input** tab. Below is the summary of all 9 Weibo and BlackCat modes:

| Mode | What It Extracts from Weibo / BlackCat | Input Needed | Cookies Needed? |
| :--- | :--- | :--- | :--- |
| **`search`** | Deep Weibo keyword search across 5 streams (comprehensive, realtime, hot, video, image) | `searchQuery` | **No** |
| **`realtime_search`** | Strictly chronological latest Weibo posts matching your keyword | `searchQuery` | **No** |
| **`user_posts`** | Full historical Weibo post timeline of specific creators, brands, or KOLs | `userIds` | **No (Built-in Pool)** |
| **`hot_timeline`** | Viral high-engagement posts currently pushed on Weibo's discovery feeds | *None (Click Start)* | **No** |
| **`hot_search`** | Real-time Top 50 Weibo Trending Board (`微博热搜榜`) with heat scores & badges (`新`/`热`/`沸`/`爆`) | *None (Click Start)* | **No** |
| **`user_profile`** | Weibo creator metrics: followers, following, total posts, verification, bio, location | `userIds` | **No** |
| **`post_details`** | Single Weibo post tracker: latest likes, reposts, comments, and full text | `postIds` | **No** |
| **`post_comments`** | Weibo comment thread extraction with commenter IP province mapping (`regionEn`) | `postIds` or `searchQuery` | **No** |
| **`complaints`** | **BlackCat (`新浪黑猫投诉`)** consumer disputes: company, title, appeal (`退款/赔偿`), status | `searchQuery` *(optional)* | **No** |

### Cascade Add-ons: Scrape Replies & Author Profiles in One Run
When running `search`, `realtime_search`, `user_posts`, `hot_timeline`, or `post_details`, enable these optional toggles:
* **`scrapeComments: true`**: Automatically extracts up to `maxCommentsPerPost` comments under each Weibo post (posts with 0 comments are skipped automatically; each comment is billed as 1 row). Pairing `hot_timeline` (`maxResults: 10`) with `scrapeComments: true` (`maxCommentsPerPost: 20`) yields ~190 rows in one pass.
* **`includeAuthorProfiles: true`**: Emits a dedicated `user_profile` row (`authorDescription`, `authorFollowing`, `statusesCount`, `location`) for each unique Weibo post author at zero extra network latency (billed as 1 row per unique author).

### JSON Input Examples

#### 1. Weibo Keyword & Brand Search with Date Window (`search`)
```json
{
  "mode": "search",
  "searchQuery": "Tesla",
  "autoLocalize": true,
  "searchAliases": ["Model Y", "Cybertruck"],
  "dateStart": "2026-09-01",
  "dateEnd": "2026-10-24",
  "maxResults": 200,
  "fullText": true,
  "sentimentAnalysis": true,
  "adFilter": true
}
```

#### 2. Weibo Creator Timeline Posts — No Cookie Required (`user_posts`)
```json
{
  "mode": "user_posts",
  "userIds": ["1749127163", "https://weibo.com/u/1642634100"],
  "maxResults": 100,
  "fullText": true,
  "sentimentAnalysis": true
}
```

#### 3. Weibo Comments & Province Rollup (`post_comments`) & BlackCat (`complaints`)
```json
{
  "mode": "post_comments",
  "postIds": ["5356654347420790"],
  "maxResults": 200,
  "sentimentAnalysis": true
}
```

---

## Automated Daily Weibo Monitoring (Schedules & Delta Mode)

Turn this Weibo Scraper into a **24/7 automated Chinese brand and public-opinion feed** in 2 minutes:
1. Run the Actor once with your target `searchQuery`, `user_posts`, or `complaints` input.
2. In **Apify Console → Schedules → Create new schedule**, select **`axon-studio/weibo-scraper`** and set your cron schedule (e.g., hourly `0 * * * *` or daily `0 8 * * *`).
3. Enable **`deltaMode: true`** in the input. The Actor stores up to 10,000 scraped IDs in your Key-Value Store (`DELTA_SEEN_IDS`) and automatically skips previously delivered items on future runs—so you only pay for brand-new Weibo mentions.

```json
{
  "mode": "search",
  "searchQuery": "Nike",
  "autoLocalize": true,
  "deltaMode": true,
  "maxResults": 100,
  "sentimentAnalysis": true
}
```

---

## Scrape Weibo with Python, JavaScript, REST API & MCP

### 1. Python (`apify-client`)
```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_API_TOKEN")
run = client.actor("axon-studio/weibo-scraper").call(run_input={
    "mode": "search",
    "searchQuery": "Luckin",
    "autoLocalize": True,
    "maxResults": 100,
    "fullText": True,
    "sentimentAnalysis": True,
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item.get("postId"), item.get("authorName"), item.get("sentiment"), item.get("text", "")[:60])
```

### 2. JavaScript / TypeScript (`apify-client`)
```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_API_TOKEN' });
const run = await client.actor('axon-studio/weibo-scraper').call({
    mode: 'search',
    searchQuery: 'Tesla',
    maxResults: 100,
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(`Extracted ${items.length} Weibo records:`, items[0]);
```

### 3. Synchronous REST API (cURL / n8n / Make / Dify / Claude MCP)
* **n8n / Make / Zapier**: Use the official Apify integration to run `axon-studio/weibo-scraper` and pipe results into OpenAI, Claude, DeepSeek, or Google Sheets.
* **Claude Desktop / Cursor (MCP)**: Click **"Copy setup prompt"** at the top right of this page to use this Weibo Scraper inside your AI agent.

```bash
curl -X POST "https://api.apify.com/v2/acts/axon-studio~weibo-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"mode":"search","searchQuery":"Tesla","maxResults":50,"sentimentAnalysis":true}'
```

---

## Weibo Scraper Output Examples

### 1. Weibo Post Row (`search`, `realtime_search`, `user_posts`, `hot_timeline`, `post_details`)
```json
{
  "postId": "5356654347420790",
  "mblogid": "RnLPYv8ua",
  "mode": "search",
  "searchQuery": "特斯拉",
  "text": "今天深度试驾了特斯拉焕新版 Model Y，智能辅助驾驶体验非常丝滑，能耗控制也很满意！",
  "sentiment": "positive",
  "sentimentScore": 0.8,
  "createdAt": "Thu Oct 22 03:03:01 +0800 2026",
  "createdAtIso": "2026-10-22T03:03:01+08:00",
  "authorId": "7758432697",
  "authorName": "科技观察员",
  "authorAvatar": "https://tvax1.sinaimg.cn/crop.0.0.1080.1080.180/...",
  "authorVerified": true,
  "authorVerifiedReason": "科技领域优质创作者",
  "authorFollowers": "8.9万",
  "attitudesCount": 128,
  "commentsCount": 34,
  "repostsCount": 12,
  "regionName": "广东",
  "regionEn": "Guangdong",
  "images": ["https://wx1.sinaimg.cn/large/008s..."],
  "isPromoted": false,
  "isRepost": false,
  "postUrl": "https://weibo.com/7758432697/RnLPYv8ua",
  "scrapedAt": "2026-10-22 03:20:34 UTC"
}
```

### 2. Weibo Comment Row (`post_comments`) & Creator Profile Row (`user_profile`)
```json
{
  "mode": "post_comments",
  "postId": "5356654347420790",
  "commentId": "5356658192014412",
  "text": "确实很稳，周末也准备去门店试驾一下！",
  "sentiment": "positive",
  "sentimentScore": 0.67,
  "createdAtIso": "2026-10-22T03:15:10+08:00",
  "authorId": "6108685154",
  "authorName": "数码玩家Leo",
  "authorVerified": false,
  "regionName": "上海",
  "regionEn": "Shanghai",
  "likesCount": 19,
  "scrapedAt": "2026-10-22 03:20:36 UTC"
}
```

### 3. BlackCat Consumer Complaint Row (`complaints` / 黑猫投诉)
```json
{
  "mode": "complaints",
  "sn": "17402361718",
  "company": "某咖啡品牌",
  "title": "小程序优惠券无法核销且客服拒绝退差价",
  "appeal": "退款,改善服务",
  "text": "本人于今日在门店下单时小程序卡顿导致优惠券未生效，联系客服处理敷衍...",
  "summary": "本人于今日在门店下单时小程序卡顿导致优惠券未生效，联系客服处理敷衍...",
  "sentiment": "negative",
  "sentimentScore": -0.78,
  "statusEn": "in_progress",
  "scrapedAt": "2026-10-22 03:20:40 UTC"
}
```

---

## Weibo Scraper Pricing & Free Plan Credits

**$4.50 per 1,000 results (`$0.0045` per item) + `$0.02` per Actor start (Pay-Per-Event)**

* **Free Plan Credits**: Every Apify account includes **$5.00 in free monthly credits**, covering up to **1,111 Weibo posts, comments, profiles, or BlackCat complaints every month for free**.
* **Volume Discounts**: Automatic lower unit prices for Apify **Bronze / Starter**, **Silver / Scale**, and **Gold / Business** plan subscribers.
* **No Extra Server Compute Fees**: Memory and CPU usage are included in the Pay-Per-Event rate.
* **Typical Run Costs**: 50 Weibo Hot Search topics = **`$0.245`** · 100 Brand Search posts = **`$0.47`** · 100 Creator Timeline posts (`user_posts`) = **`$0.47`** · 10,000 Weibo posts for AI training = **`$45.02`**.

---

## Weibo Scraper FAQ

### Is there an official Weibo API for international developers?
Sina Weibo's commercial API requires a Chinese business license (`营业执照`), enterprise review, and high annual fees. This Weibo Scraper provides a plug-and-play alternative requiring no Chinese entity, no VPN, and no Weibo account.

### Do I need to provide Weibo cookies for `user_posts` or search?
**No.** All 9 modes—including `user_posts` (creator timelines), `search`, `post_comments`, and `complaints`—use our built-in managed session pool and anonymous visitor rotation automatically.

### Legal & GDPR / PIPL Compliance
This Actor extracts publicly available information from Sina Weibo and BlackCat public endpoints and does not access private or locked accounts. Public creator names, UIDs, bios, and IP province labels may constitute personal data under **GDPR** or **PIPL**; ensure you have a lawful basis for processing public social data. *Not affiliated with Sina Corporation or Weibo.*
