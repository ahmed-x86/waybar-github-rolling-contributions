<div align="center">
  <h1>🟪🟪⬛🟪⬛</h1>
</div>

# GitHub Rolling Contributions Widget for Waybar

> 💡 **Note:** This is a modified fork of [ad1822/weekly-github-waybar-module](https://github.com/ad1822/weekly-github-waybar-module). It has been rewritten to display a **rolling 7-day window** and features a custom **purple color scheme**.

A terminal or bar integration script that fetches your **GitHub contribution activity for the last 7 rolling days** using the GitHub GraphQL API and renders a **custom purple colored heatmap** with detailed tooltips.

Designed for seamless integration with status bars like **Waybar**, **Polybar**, or any custom desktop widget.

-----

## Features

  - Pulls real-time contribution data from GitHub's GraphQL API.
  - Displays a **rolling 7-day contribution heatmap** (Always shows the past 7 days, avoiding empty trackers at the start of the week).
  - Uses a **color-coded square** (■) system with a custom purple gradient.
  - Provides a **detailed tooltip** with:
      - Date-wise contribution breakdown.
      - Total contributions over the tracked 7 days.

-----

## Color Levels (Purple Theme)

| Contributions | Color Hex  | Meaning            |
|---------------|------------|--------------------|
| 0             | `#161b22`  | No contributions   |
| 1–3           | `#3d2258`  | Low activity       |
| 4–6           | `#6a3896`  | Moderate activity  |
| 7–9           | `#974ddb`  | High activity      |
| 10+           | `#c463ff`  | Very high activity |

-----

## Setup

### 1\. Clone the Repository

```bash
git clone https://github.com/ahmed-x86/waybar-github-rolling-contributions.git
cd waybar-github-rolling-contributions
```

-----

### 2\. GitHub Authentication

To make this module work, you need to provide:

  * Your **GitHub username**

  * A **Fine-Grained Personal Access Token (PAT)**

      * Scope: `Repository access → All repositories`
      * Minimum required permissions for reading contribution data

➡ **Generate your token here:**
[https://github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new)

-----

### 3\. Create `.env` File

Inside the project directory, create a `.env` file with the following content:

```env
GITHUB_USERNAME=your_github_username
GITHUB_PAT=ghp_yourGeneratedTokenHere
```

-----



### 4\. Waybar Integration

Add the following block to your Waybar `config.jsonc` (Make sure to update the path to where you placed the script):

```jsonc
"custom/gh_heatmap": {
  "exec": "sleep 1 & ~/.config/waybar/scripts/weekly_commits",
  "return-type": "json",
  "interval": 2400,
  "tooltip": true,
  "on-click": "xdg-open https://github.com/ahmed-x86",
  "on-click-right": "~/.config/waybar/scripts/weekly_commits"
}
```

  - On `click` of that module, your GitHub profile opens in the browser.
  - On `right-click` of that module, you refresh the module to fetch the latest commit data.

Then add styling in your `style.css`:

```css
#custom-gh_heatmap {
  color: #c463ff;
  background: rgba(30, 30, 46, 0.89); /* Fits perfectly with dark/Catppuccin backgrounds */
  border-radius: 6px;
  margin-right: 2px;
  padding: 0px 8px;
}
```

> Ensure the script is executable:
>
> ```bash
> chmod +x ~/.config/waybar/scripts/weekly_commits
> ```

-----

If you like it, consider giving it a ⭐ — it helps\!