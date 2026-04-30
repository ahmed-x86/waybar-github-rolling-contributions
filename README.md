<div align="center">
  <h1>🟪🟪⬛🟪⬛</h1>
</div>

# GitHub Rolling Contributions Widget for Waybar

> 💡 **Note:** This is a modified fork of [ad1822/weekly-github-waybar-module](https://github.com/ad1822/weekly-github-waybar-module). It has been rewritten to display a **rolling 7-day window** and features **dynamic color palette generation**.

A terminal or bar integration script that fetches your **GitHub contribution activity for the last 7 rolling days** using the GitHub GraphQL API and renders a **custom colored heatmap** with detailed tooltips.

Designed for seamless integration with status bars like **Waybar**, **Polybar**, or any custom desktop widget.

-----

## Features

  - Pulls real-time contribution data from GitHub's GraphQL API.
  - Displays a **rolling 7-day contribution heatmap** (Always shows the past 7 days, avoiding empty trackers at the start of the week).
  - Uses a **color-coded square** (■) system with **dynamic gradient generation** based on your preferred base color.
  - Supports custom colors via CLI arguments in **HEX** or **RGB** formats.
  - Provides a **detailed tooltip** with:
      - Date-wise contribution breakdown.
      - Total contributions over the tracked 7 days.
      - Currently active base color.

-----

## Color Levels (Default Purple Theme)

By default, the script uses a purple theme. However, you can pass any custom base color (representing the highest activity level `10+`), and the script will automatically calculate and generate the lower-level gradients based on that color.

| Contributions | Default Hex | Meaning            |
|---------------|-------------|--------------------|
| 0             | ![#161b22](https://placehold.co/15x15/161b22/161b22.png) `#161b22`  | No contributions   |
| 1–3           | ![#3d2258](https://placehold.co/15x15/3d2258/3d2258.png) `#3d2258`  | Low activity       |
| 4–6           | ![#6a3896](https://placehold.co/15x15/6a3896/6a3896.png) `#6a3896`  | Moderate activity  |
| 7–9           | ![#974ddb](https://placehold.co/15x15/974ddb/974ddb.png) `#974ddb`  | High activity      |
| 10+           | ![#c463ff](https://placehold.co/15x15/c463ff/c463ff.png) `#c463ff`  | Very high activity |

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

[➡ **Generate your token here:**](https://github.com/settings/personal-access-tokens/new)

-----

### 3\. Create `.env` File

Inside the project directory, create a `.env` file with the following content:

```env
GITHUB_USERNAME=your_github_username
GITHUB_PAT=ghp_yourGeneratedTokenHere
```

-----

### 4\. Waybar Integration & Custom Colors

Ensure the script is executable:

```bash
chmod +x ~/.config/waybar/scripts/weekly_commits
```

Add the following block to your Waybar `config.jsonc`. You can customize the heatmap color by passing the `-c` or `--color` argument in the `exec` command. If no color is passed, it defaults to purple.

**Example 1: Default (Purple)**
```jsonc
"custom/gh_heatmap": {
  "exec": "sleep 1 & ~/.config/waybar/scripts/weekly_commits",
  "return-type": "json",
  "interval": 2400,
  "tooltip": true,
  "on-click": "xdg-open [https://github.com/ahmed-x86](https://github.com/ahmed-x86)",
  "on-click-right": "~/.config/waybar/scripts/weekly_commits"
}
```

**Example 2: Custom Color using HEX (e.g., Green)**
```jsonc
"custom/gh_heatmap": {
  "exec": "sleep 1 & ~/.config/waybar/scripts/weekly_commits --color '#00ff00'",
  "return-type": "json",
  "interval": 2400,
  "tooltip": true,
  "on-click": "xdg-open [https://github.com/ahmed-x86](https://github.com/ahmed-x86)",
  "on-click-right": "~/.config/waybar/scripts/weekly_commits"
}
```

**Example 3: Custom Color using RGB (e.g., Orange)**
```jsonc
"custom/gh_heatmap": {
  "exec": "sleep 1 & ~/.config/waybar/scripts/weekly_commits --color '255,165,0'",
  "return-type": "json",
  "interval": 2400,
  "tooltip": true,
  "on-click": "xdg-open [https://github.com/ahmed-x86](https://github.com/ahmed-x86)",
  "on-click-right": "~/.config/waybar/scripts/weekly_commits"
}
```

Then add styling in your `style.css` (Update the `color` property if you used a custom base color):

```css
#custom-gh_heatmap {
  color: #c463ff; /* Change this to match your custom base color if used */
  background: rgba(30, 30, 46, 0.89); /* Fits perfectly with dark/Catppuccin backgrounds */
  border-radius: 6px;
  margin-right: 2px;
  padding: 0px 8px;
}
```

-----

If you like it, consider giving it a ⭐ — it helps\!