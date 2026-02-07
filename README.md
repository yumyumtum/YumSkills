# YumSkills

Reusable AI prompt skills (structured system prompts) for stock & market analysis.

These `.md` skill files work with any AI tool that supports prompt/instruction files — GitHub Copilot, Claude, ChatGPT custom instructions, Cursor, Windsurf, and others.

## Skills

| Skill | Description |
|-------|-------------|
| [yumstock](yumstock/) | Macro-weighted US stock analysis. Scores 7 macro indicators (Fear & Greed, Fed liquidity, NFCI, BDI, ISM, LEI, yield curve) to gate Buy/Hold/Sell verdicts, then runs full fundamentals + 3 related stocks. |

---

## Setup: VS Code + GitHub Copilot

### 1. Copy the skill file

```bash
# Clone this repo
git clone https://github.com/yumyumtum/YumSkills.git

# Create the user-wide prompts folder
mkdir -p ~/.github/prompts

# Copy the skill
cp YumSkills/yumstock/SKILL.md ~/.github/prompts/yumstock.prompt.md
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

### 4. Verify the skill is loaded

In the Copilot Chat panel, click the **paperclip / attach** icon (or type `#`) → select **"Prompt..."** — you should see **yumstock** in the list. If it appears, the skill is active and ready to use.

If you do **not** see it:
- Confirm the file exists: `ls ~/.github/prompts/yumstock.prompt.md`
- Confirm `chat.promptFiles` is `true` in your settings
- Reload VS Code again

### 5. Use it

Attach the prompt, then type your query:

> Analyze NVDA

The skill will first score the macro environment, then produce a full fundamental report with gated Buy/Hold/Sell verdicts for NVDA and 3 related stocks.

---

## License

[GPL-3.0](LICENSE)
