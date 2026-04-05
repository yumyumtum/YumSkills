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

---

## Installation

### Option 1: OpenClaw + ClawHub (Recommended)

```bash
# Install via ClawHub
clawhub install yumstock
clawhub install yumetfeagle
clawhub install zen-koan-daily
clawhub install continuance

# Use in OpenClaw
/yumstock AAPL
/yumetfeagle
/koan
/continuance
```

### Option 2: Manual Installation

Clone and copy skill files to your OpenClaw skills directory:

```bash
git clone https://github.com/yumyumtum/YumSkills.git
cp -r YumSkills/zen-koan-daily ~/.openclaw/skills/
cp -r YumSkills/Continuance ~/.openclaw/skills/
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

---

## License

[GPL-3.0](LICENSE)
