---
name: zen-koan-daily
description: "Daily Zen Buddhist koan (禅宗公案) lecture with Chinese ink wash illustration and TTS audio. Generates detailed lecture (origin, background, interpretation, modern insights), zen ink wash painting, and audio narration. Use when: /koan, /公案, zen/禅宗 content requests, or daily spiritual content."
homepage: https://github.com/yumyumtum/yumskills/tree/main/zen-koan-daily
metadata:
  openclaw:
    emoji: "🎋"
    requires:
      bins: ["python3", "edge-tts"]
    triggers:
      - "/koan"
      - "/公案"
      - "zen koan"
      - "禅宗公案"
      - "禅宗"
---

# Zen Koan Daily | 每日禅宗公案 🎋

**Daily Zen Buddhist koan with ink wash art and audio narration**

每日禅宗公案配水墨画和语音讲解

---

## 🎯 What This Skill Does | 功能说明

Delivers a complete Zen koan experience every day:

每天提供完整的禅宗公案体验：

1. **📜 Koan Lecture | 公案讲解**
   - Original text (classical Chinese + English)
   - Historical background
   - Deep interpretation
   - Modern-life insights

2. **🎨 Zen Ink Wash Art | 禅宗水墨画**
   - AI-generated Chinese ink wash painting
   - Minimalist aesthetic with vast empty space (留白)
   - Mood matches the koan theme

3. **🔊 Audio Narration | 语音讲解**
   - TTS audio (Edge TTS, free)
   - Chinese: Calm, contemplative voice
   - English: Narrative, meditative style

---

## 📚 书库归档（Library · 每期必做）

本 skill 产出的**所有东西（讲稿 / 水墨配图 / 语音 / 朗读稿）都要按章节顺序归档到自己的书目录**，将来可以按顺序导出成一本书（Markdown / HTML，后续可转 PDF、PPT），用户不用 AI、也不用在聊天记录里翻。

- 书目录：`/workspace/library/zen-koan/`（本书专属，别的 skill 不往这里写）
- 每期一个文件夹：`/workspace/library/zen-koan/epNNN-<slug>/`（公案不是连续的书，按交付序号排序；slug 为公案名拼音，如 `ep001-ririshihaori/`）
  - `lecture.md` 讲稿（图片/音频用**相对路径**引用，文件夹自包含）
  - `image.png（或 .jpg）` 水墨配图
  - `voice.mp3` 语音
  - `read.txt` 朗读稿
- `book.json`：按期号排序的清单（导出脚本读它）；`index.md`：目录（期号、出处、标题、日期、相对链接）。两者都由归档脚本自动维护，**不要手改**。
- 归档脚本：`/workspace/library/library.py`（导出：`/workspace/library/export_book.py zen-koan`）。脚本源文件在本仓库 `daily-library/`；安装时复制或软链接到 `/workspace/library/`，上面的命令默认走这个运行时路径。

归档命令（文件可以先生成在任意临时位置，脚本会复制进书目录、把讲稿里的图片/音频改成相对链接、更新 `book.json` 和 `index.md`）：

```bash
python3 /workspace/library/library.py add --book zen-koan --episode <N> --slug <拼音slug> --title "本期标题" \
  --date <YYYY-MM-DD，太平洋时间当天> --source "<出处，如 碧岩录 第6则>" \
  --lecture <讲稿.md> --image <水墨配图文件> --audio <语音.mp3> --read <朗读稿.txt>
```

- **分件归档、可重复执行**：文字写好就先 `add --lecture`（保底）；水墨配图、语音做好后再用**同一个 `--episode` 和 `--slug`** 各补一次 `add --image …` / `add --audio … --read …`。重复 add 同一期只会补齐/覆盖对应文件，不会重复建期。
- 查缺补漏：`python3 /workspace/library/library.py status --book zen-koan` 列出每期缺哪件（`missing`），以及 `next_episode`。
- 期号 `<N>` 以本 skill 进度为准（`references/progress.json` 的 `total_deliveries` + 1；交付后把 `total_deliveries` +1 并在 `recent_koans` 追加本期），与讲稿标题里的"第 N 期"一致。
- 归档失败**不阻塞**给用户的交付（吞错继续），但要尽量完成；不要把归档路径、脚本输出念给用户或写进讲稿正文。
- 用户说"导出 禅宗公案"时：`python3 /workspace/library/export_book.py zen-koan` → 生成 `/workspace/library/zen-koan/export/zen-koan.md` 和 `zen-koan.html`（按期序、带图和音频播放器）；加 `--embed-images` 可把图片内嵌进单个 HTML，`--from/--to` 选期号范围。

---

## 🤖 Agent Instructions | AI助手指令

### Trigger Commands | 触发命令

**User says any of:**
- `/koan` or `/公案` → Generate today's koan
- `/koan next` → Next koan in sequence
- `/koan random` → Random koan
- `/koan 1` → Specific koan by ID
- `zen koan`, `禅宗公案`, `tell me a koan` → Conversational trigger

### Workflow | 工作流程

**Dynamic Generation Mode** (动态生成模式)

This skill uses **LLM-powered dynamic generation** instead of a fixed database:
- Only 2 reference koans are stored as examples
- All other koans are generated fresh by the LLM
- Sources: 无门关, 碧岩录, 从容录, 景德传灯录, 五灯会元

**When triggered:**

**Step 1: Generate Koan Content** (LLM生成公案)

The LLM will:
1. Select an appropriate koan from classical Zen literature
2. Generate complete content:
   - Original text (classical Chinese + English)
   - Historical background
   - Deep interpretation
   - Modern-life insights
   - Visual elements for image generation

3. **Optional**: Use stored reference koans (ID 1-2) for testing
4. **Optional**: Use `web_search` to find contemporary Zen teachings

**Step 2: Format Lecture Text**
**Step 2: Format Lecture Text**

**For stored koans (testing)**:
   ```bash
   python3 ~/clawd/skills/zen-koan-daily/scripts/generate_koan.py --id 1 --lang zh
   ```

**For LLM-generated koans**:
   - LLM directly generates the full lecture in the correct format
   - Use the same structure as reference koans:
     - Title + Collection
     - Original text (📜)
     - Background (📖)
     - Interpretation (💡)
     - Modern Insight (🌏)
     - Optional: Personal Insight (🧘 **为你而讲**)
   
   Options:
   - `--lang zh` → Chinese lecture
   - `--lang en` → English lecture
   - `--personal "..."` → Add personalized insight based on recent context

**Step 3: Get Koan JSON** (for image generation)
**Step 3: Get Koan JSON** (for image generation)

**Option A - Use stored koan**:
   ```bash
   python3 ~/clawd/skills/zen-koan-daily/scripts/generate_koan.py --id 1 --format json
   ```

**Option B - LLM generates koan metadata**:
   LLM creates JSON with visual elements:
   ```json
   {
     "id": 3,
     "title_zh": "俱胝竖指",
     "visual_elements": ["finger", "mountain", "clouds"],
     "mood": "sudden, shocking, direct"
   }
   ```

**Step 4: Generate Zen Ink Wash Image**
   ```bash
   # Get the prompt command
   python3 ~/clawd/skills/zen-koan-daily/scripts/generate_image.py \
     --koan-json '{"id": 1, "visual_elements": ["dog", "bamboo"], "mood": "serene"}'
   
   # Then run the displayed uv command via exec tool
   ```

**Step 5: Generate TTS Audio**
   ```bash
   # Save lecture text to temp file
   echo "<lecture_text>" > /tmp/koan.txt
   
   ~/clawd/skills/zen-koan-daily/scripts/generate_tts.sh \
     --text-file /tmp/koan.txt \
     --lang zh \
     --output /tmp/koan-$(date +%Y%m%d).mp3   # then archive it (Step 6)
   # fallback: uvx edge-tts --voice zh-CN-XiaoxiaoNeural --rate=-10% --file /tmp/koan.txt --write-media <out.mp3>
   ```

**Step 6: Archive to the library | 归档到书库**
   - Save the full formatted lecture (the same markdown you send, with the title line `## 🎋 每日禅宗公案 · 第 N 期`) to a .md file, and the TTS text to a .txt file.
   - Archive each piece as it is ready (see 「书库归档」 above):
     ```bash
     python3 /workspace/library/library.py add --book zen-koan --episode N --slug <slug> \
       --title "<公案名>" --source "<出处>" --lecture <lecture.md>
     python3 /workspace/library/library.py add --book zen-koan --episode N --slug <slug> --image <ink.png>
     python3 /workspace/library/library.py add --book zen-koan --episode N --slug <slug> --audio <koan.mp3> --read <koan.txt>
     ```
     → `/workspace/library/zen-koan/epNNN-<slug>/{lecture.md,image.png,voice.mp3,read.txt}`
   - Update `references/progress.json` (`total_deliveries`, `last_delivery_date`, `recent_koans`).

**Step 7: Send to User**
   - Image (PNG)
   - Audio (MP3)
   - Lecture text (formatted)

---

## 📚 Koan Database | 公案数据库

**Generation Mode:** Dynamic (动态生成)

**Stored Reference Koans:** 2
- 赵州狗子 (Zhaozhou's Dog)
- 平常心是道 (Ordinary Mind is the Way)

**Additional Koans:** Generated dynamically by LLM from:
- *The Gateless Gate* (无门关) - 48 cases
- *Blue Cliff Record* (碧岩录) - 100 cases  
- *Book of Serenity* (从容录) - 100 cases
- *Transmission of the Lamp* (景德传灯录)
- *Five Lamps Meeting at the Source* (五灯会元)

**Why Dynamic Generation?**
- ✅ LLM quality is excellent (verified through testing)
- ✅ No need to store 50-100 koans manually
- ✅ Unlimited variety from classical sources
- ✅ Fresh interpretations each time
- ✅ Optional web_search for contemporary teachings

**Quality Assurance:**
- LLM trained on authentic Zen literature
- Cross-references classical sources
- Maintains consistent format
- Verified through testing (see reference koans)
1. **赵州狗子** (Zhaozhou's Dog) - The first barrier
2. **平常心是道** (Ordinary Mind is the Way) - Non-seeking

**Coming Soon:**
- 德山棒 (Deshan's Stick)
- 临济喝 (Linji's Shout)
- 庭前柏树子 (The Cypress Tree)
- 青原三境 (Three Stages)
- ...and 42+ more classical koans

**Location:** `~/clawd/skills/zen-koan-daily/references/koans.json`

---

## 🎨 Image Style | 图片风格

**Zen Ink Wash Aesthetic:**

```
Chinese zen ink wash painting (禅宗水墨画),
minimalist composition, vast empty space (留白),
subtle gradations of black ink on rice paper,
sparse brushstrokes, meditative atmosphere,
traditional Chinese calligraphy style,
serene and contemplative mood
```

**Visual Elements by Koan:**
- **Dog/Buddha-nature koans** → Dog silhouette, bamboo, moon
- **Void/Emptiness koans** → Vast sky, simple tea cup
- **Nature koans** → Misty mountain, pine tree, plum blossom

---

## 🔊 TTS Configuration | 语音配置

**Voices:**
- **Chinese (中文)**: `zh-CN-XiaoxiaoNeural`
  - Warm, calm, suitable for contemplative content
  - 温暖、平静、适合讲解内容
  
- **English**: `en-US-AriaNeural`
  - Calm, narrative, meditative style
  - 平静、叙述风格、冥想氛围

**Audio Format:**
- MP3 (compressed)
- Archived to `/workspace/library/zen-koan/epNNN-<slug>/voice.mp3`

---

## 📖 Output Example | 输出示例

**Text (Chinese):**
```
🎋 每日禅宗公案 | Daily Zen Koan

━━━━━━━━━━━━━━━━━━━━━━━━

**赵州狗子**
*无门关 第1则*

━━━━━━━━━━━━━━━━━━━━━━━━

📜 **原文**

僧问赵州：「狗子还有佛性也无？」州云：「无。」

━━━━━━━━━━━━━━━━━━━━━━━━

📖 **背景**

赵州从谂禅师（778-897）是唐代著名禅师...

━━━━━━━━━━━━━━━━━━━━━━━━

💡 **白话解读**

赵州答「无」，并非否定佛性...

━━━━━━━━━━━━━━━━━━━━━━━━

🌏 **现代启示**

现代人陷入「有用/无用」「成功/失败」的二元思维...
```

**Files Generated (library):**
- `/workspace/library/zen-koan/ep001-ririshihaori/lecture.md` (lecture, relative links to media)
- `/workspace/library/zen-koan/ep001-ririshihaori/image.jpg` (Zen ink wash image)
- `/workspace/library/zen-koan/ep001-ririshihaori/voice.mp3` (TTS audio narration)
- `/workspace/library/zen-koan/ep001-ririshihaori/read.txt` (narration script)
- `/workspace/library/zen-koan/index.md` + `book.json` (table of contents / manifest, auto-updated)

---

## 🔄 Progress Tracking | 进度追踪

**Automatic tracking:**
- `references/progress.json` tracks which koans have been delivered
- Cycles through all koans, then repeats
- Stores delivery history

**Check progress:**
```bash
cat ~/clawd/skills/zen-koan-daily/references/progress.json
```

---

## 🛠️ Installation | 安装

**Requirements:**
- Python 3.10+
- Edge TTS: `pipx install edge-tts`
- Gemini API key (for images): `export GEMINI_API_KEY="..."`

**Install:**
```bash
clawhub install zen-koan-daily
```

**Or from GitHub:**
```bash
git clone https://github.com/yumyumtum/yumskills.git
cd yumskills/zen-koan-daily
```

---

## 📅 Cron Scheduling | 定时任务

**Daily delivery at 6:00 AM:**

Create OpenClaw cron task:
```json
{
  "name": "Daily Zen Koan",
  "schedule": {
    "kind": "cron",
    "expr": "0 6 * * *",
    "tz": "America/Los_Angeles"
  },
  "sessionTarget": "isolated",
  "payload": {
    "kind": "agentTurn",
    "message": "/koan next"
  }
}
```

---

## 🏷️ Tags & Metadata | 标签与元数据

**Difficulty Levels:**
- `beginner` - Foundational koans (赵州狗子, 平常心)
- `intermediate` - Deeper practice (德山棒, 临济喝)
- `advanced` - Subtle realization (庭前柏树子, 青原三境)

**Schools:**
- `rinzai` - Sudden enlightenment tradition
- `soto` - Gradual cultivation tradition
- `both` - Universal teachings

---

## 🔗 Related Skills | 相关技能

- **Continuance** - Daily spiritual guidance
- **Nano Banana Pro** - AI image generation
- **Azure TTS** - Alternative TTS option

---

## 📜 License | 许可证

GPL-3.0-or-later

Open source, free to use and modify.

---

*"When you meet a swordsman on the road, draw your sword. Don't recite poetry to one who is not a poet."*

*"路逢剑客须呈剑，不是诗人莫献诗。"*

— Zen saying | 禅宗古语
