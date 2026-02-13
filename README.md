# YumSkills

Reusable AI prompt skills (structured system prompts) for stock & market analysis.

These `.md` skill files work with any AI tool that supports prompt/instruction files — GitHub Copilot, Claude, ChatGPT custom instructions, Cursor, Windsurf, and others.

## Skills

| Skill | Description |
|-------|-------------|
| [yumstock](yumstock/) | **Three-pillar weighted US stock analysis.** Scores Technical (35%), Fundamentals (25%), and Macro (40%) to produce a composite score with macro-gated Buy/Hold/Sell verdicts. Includes 7 macro indicators, 7 technical indicators (MACD, EMA Cross, RSI, KDJ, Price-Volume, EMA Trend, Buy-Point Structure), full fundamental scorecard, and comparative analysis against 3 related stocks. |
| [yumetfeagle](yumetfeagle/) | **ETF sector rotation scanner.** Scans 40 US sector/industry ETFs for 2-week momentum, selects the Top 5 leaders and Bottom 5 laggards, then runs full yumstock three-pillar analysis on each. Synthesises findings into sector rotation insights and an "Eagle's Pick" — the single best ETF opportunity. |

---

## Setup: VS Code + GitHub Copilot

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

The skill scores the macro environment (7 indicators), runs technical analysis (7 indicators), performs full fundamental analysis, compares against 3 related stocks, and produces a macro-gated Buy/Hold/Sell verdict with a composite score.

**yumetfeagle** — Scan sector ETFs:
> Run ETF Eagle scan

The skill screens 40 ETFs for 2-week momentum, selects the top/bottom 5, runs three-pillar deep-dives on all 10, and delivers an Eagle's Pick with entry/exit levels.

---

## License

[GPL-3.0](LICENSE)
