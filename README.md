# YumSkills

Reusable AI skills for OpenClaw agents — stock analysis, spiritual guidance, and daily Zen practice.

These skills work with [OpenClaw](https://openclaw.ai) and can be installed via [ClawHub](https://clawhub.ai).

## Skills

| Skill | Description | Category |
|-------|-------------|----------|
| [yumstock](yumstock/) | **Three-pillar weighted US stock analysis.** Scores Technical (35%), Fundamentals (25%), and Macro (40%) to produce a composite score with macro-gated Buy/Hold/Sell verdicts. Includes 7 macro indicators, 7 technical indicators (MACD, EMA Cross, RSI, KDJ, Price-Volume, EMA Trend, Buy-Point Structure), full fundamental scorecard, and comparative analysis against 3 related stocks. | 📊 Markets |
| [yumetfeagle](yumetfeagle/) | **ETF sector rotation scanner.** Scans 40 US sector/industry ETFs for 2-week momentum, selects the Top 5 leaders and Bottom 5 laggards, then runs full yumstock three-pillar analysis on each. Synthesises findings into sector rotation insights and an "Eagle's Pick" — the single best ETF opportunity. | 📊 Markets |
| [zen-koan-daily](zen-koan-daily/) | **Daily Zen Buddhist koan with AI ink wash art and TTS audio.** Uses LLM to dynamically generate koans from classical sources (无门关, 碧岩录, 从容录). Includes Chinese ink wash painting (Gemini AI), TTS narration (Edge TTS, free), bilingual support (中文/English), and personalized insights based on user context. | 🎋 Spirituality |
| [Continuance](Continuance/) | **Daily spiritual guidance from The Book of Continuance.** Naturalistic scripture on persistence, alignment, and the soul's place within the flow of life. Generates daily reflections with TTS audio. Answers life doubts and provides mental guidance. | 🌱 Spirituality |
| [daily-ramayana](daily-ramayana/) | **每日罗摩衍那 — daily lecture on the Vālmīki Rāmāyaṇa.** Reads all 7 Kāṇḍas from the bundled public-domain English text (Griffith Books 1–6 + M. N. Dutt Book 7), one segment per episode. Each episode is a Chinese lecture (English excerpt, 中文译述, cultural background), an Indian-miniature illustration, and Chinese TTS. Progress is tracked automatically. | 📜 Spirituality |
| [daily-library](daily-library/) | **Shared archive for the daily reading skills.** `library.py` files each episode's lecture, image, and audio into a per-book folder ordered by chapter or episode, and keeps `index.md` / `book.json`. `export_book.py` exports a whole book as ordered Markdown and HTML. On install, copy or symlink this folder to `/workspace/library/`. | 📚 Library |

---

## Gallery

### 🎋 Zen Koan Daily - AI Ink Wash Art

<table>
  <tr>
    <td width="50%">
      <img src=".github/images/zen-koan-zhaozhou-dog.png" alt="赵州狗子 (Zhaozhou's Dog)" />
      <p align="center"><em>赵州狗子 (Zhaozhou's Dog)</em></p>
    </td>
    <td width="50%">
      <img src=".github/images/zen-koan-gutei-finger.png" alt="俱胝竖指 (Gutei's Finger)" />
      <p align="center"><em>俱胝竖指 (Gutei's Finger)</em></p>
    </td>
  </tr>
</table>

**Features**: Dynamic LLM generation • Chinese ink wash style • Bilingual lectures • Personalized insights • TTS audio

### 🎮 YumFu - Multi-World MUD Game

<table>
  <tr>
    <td width="33%">
      <img src=".github/images/yumfu-game-of-thrones.png" alt="Fantasy World - Political Intrigue" />
      <p align="center"><em>Medieval Fantasy</em></p>
    </td>
    <td width="33%">
      <img src=".github/images/yumfu-harry-potter.png" alt="Magic School World" />
      <p align="center"><em>Magic Academy</em></p>
    </td>
    <td width="33%">
      <img src=".github/images/yumfu-warrior-cats.png" alt="Animal Adventure World" />
      <p align="center"><em>Clan Survival</em></p>
    </td>
  </tr>
</table>

**Features**: AI-generated scene art • 4 immersive worlds • Real-time combat • Quest system • Full MUD gameplay

*Note: YumFu is published separately at [github.com/yumyumtum/yumfu](https://github.com/yumyumtum/yumfu)*

---

## Installation

### Option 1: OpenClaw + ClawHub (Recommended)

```bash
# Install via ClawHub
clawhub install yumstock
clawhub install yumetfeagle
clawhub install zen-koan-daily
clawhub install continuance
clawhub install daily-ramayana

# Use in OpenClaw
/yumstock AAPL
/yumetfeagle
/koan
/continuance
继续读罗摩衍那
```

### Option 2: Manual Installation

Clone and copy skill files to your OpenClaw skills directory:

```bash
git clone https://github.com/yumyumtum/YumSkills.git
cp -r YumSkills/zen-koan-daily ~/.openclaw/skills/
cp -r YumSkills/Continuance ~/.openclaw/skills/
cp -r YumSkills/daily-ramayana ~/.openclaw/skills/
# daily-library is not a skill; the reading skills call it at /workspace/library/
ln -sfn "$(pwd)/YumSkills/daily-library" /workspace/library
```

### Option 3: VS Code + GitHub Copilot (Legacy)

For yumstock/yumetfeagle only (originally designed as prompt files):

### 1. Copy the skill files

```bash
# Clone this repo
git clone https://github.com/yumyumtum/YumSkills.git

# Create the user-wide prompts folder
mkdir -p ~/.github/prompts

# Copy the skills
cp YumSkills/yumstock/SKILL.md ~/.github/prompts/yumstock.prompt.md
cp YumSkills/yumetfeagle/SKILL.md ~/.github/prompts/yumetfeagle.prompt.md
```

### 2. Enable prompt files in VS Code settings

Open your settings JSON (`Cmd+Shift+P` → **Preferences: Open User Settings (JSON)**) and add:

```jsonc
"chat.promptFiles": true,
"chat.promptFilesLocations": {
    "~/.github/prompts": true
}
```

### 3. Reload VS Code

`Cmd+Shift+P` → **Developer: Reload Window**

### 4. Verify the skills are loaded

In the Copilot Chat panel, click the **paperclip / attach** icon (or type `#`) → select **"Prompt..."** — you should see **yumstock** and **yumetfeagle** in the list.

If you do **not** see them:
- Confirm the files exist: `ls ~/.github/prompts/yumstock.prompt.md ~/.github/prompts/yumetfeagle.prompt.md`
- Confirm `chat.promptFiles` is `true` in your settings
- Reload VS Code again

### 5. Use them

Attach a prompt, then type your query:

**yumstock** — Analyze any US stock:
> Analyze CSCO

---

## Usage Examples

### 📊 Stock Analysis

**yumstock** — Analyze any US stock:
```
/yumstock NVDA
```
Scores macro (7 indicators), technical (7 indicators), fundamentals, and 3 comparables. Produces Buy/Hold/Sell verdict.

**yumetfeagle** — Scan sector ETFs:
```
/yumetfeagle
```
Screens 40 ETFs, deep-dives top/bottom 5, delivers Eagle's Pick with entry/exit levels.

### 🎋 Zen Practice

**zen-koan-daily** — Daily Zen koan:
```
/koan
```
Generates a Zen koan from classical sources, with:
- 📜 Original text (中文 + English)
- 📖 Historical background
- 💡 Deep interpretation
- 🌏 Modern insights
- 🧘 Personal reflection (based on your recent context)
- 🎨 AI ink wash painting
- 🔊 TTS audio narration

### 🌱 Spiritual Guidance

**Continuance** — Daily wisdom:
```
/continuance
```
Reflections from The Book of Continuance on persistence, flow, and alignment.

### 📜 Ramayana

**daily-ramayana** — 每日罗摩衍那:
```
继续读罗摩衍那
```
Reads the next segment of the Vālmīki Rāmāyaṇa (all 7 Kāṇḍas) and delivers a Chinese lecture, an Indian-miniature illustration, and TTS audio. Say「导出 罗摩衍那」to export the archived episodes as a book.

### 📚 Library

**daily-library** — archive and export:
```bash
python3 /workspace/library/library.py status --book ramayana
python3 /workspace/library/export_book.py ramayana
```
Files each episode into a per-book folder (`tongjian/`, `xuanzang/`, `ramayana/`, `zen-koan/`) and can export a whole book as ordered Markdown and HTML.

---

## Features

### 📊 Markets (yumstock, yumetfeagle)
- Three-pillar analysis (Technical, Fundamentals, Macro)
- Macro-gated verdicts (respects market environment)
- Comparative analysis vs peers
- Sector rotation insights
- Entry/exit level recommendations

### 🎋 Zen (zen-koan-daily)
- 🤖 **Dynamic LLM generation** (no fixed database)
- 📚 Sources: 无门关, 碧岩录, 从容录, 景德传灯录, 五灯会元
- 🎨 Chinese ink wash paintings (Gemini AI)
- 🔊 Free TTS audio (Edge TTS)
- 🌏 Bilingual (中文/English)
- 🧘 Personalized insights

### 🌱 Spirituality (Continuance)
- Daily reflections from The Book of Continuance
- TTS audio narration
- Life guidance and mental clarity

### 📜 Ramayana (daily-ramayana)
- All 7 Kāṇḍas from bundled public-domain English (Griffith Books 1–6, M. N. Dutt Book 7)
- Chinese lecture with English excerpt, 中文译述, and cultural background
- Indian-miniature illustration and Chinese TTS
- Auto-tracked progress, one segment per episode

### 📚 Library (daily-library)
- Per-book folders ordered by chapter or episode
- `index.md` and `book.json` maintained by `library.py`
- Whole-book Markdown / HTML export via `export_book.py`

---

## License

[GPL-3.0](LICENSE)
