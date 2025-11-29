# Bowling League Manager

A Jekyll-based static site for managing a bowling league with weekly scores and player statistics.

## Features

- **Weekly Scoreboard**: Each week has its own page with players sorted by their total score (sum of 3 games)
- **Player Profiles**: Individual pages for each player showing their average and complete game history
- **Home Dashboard**:
  - Top 3 players from the most recent week
  - Top 5 players by overall average
  - Links to all weeks and players

## Getting Started

### Prerequisites

- Ruby (2.5 or higher)
- Bundler

### Installation

1. Install dependencies:
```bash
bundle install
```

2. Run the Jekyll server:
```bash
bundle exec jekyll serve
```

3. Open your browser to `http://localhost:4000`

## Adding Data

### Adding a New Player

Create a new file in `_players/` directory:

```bash
_players/player-name.md
```

Content:
```yaml
---
name: Player Name
---
```

The filename should be a slugified version of the player's name (lowercase, hyphens instead of spaces).

### Adding a New Week

Create a new file in `_weeks/` directory:

```bash
_weeks/week-X.md
```

Content:
```yaml
---
title: Week X
date: YYYY-MM-DD
scores:
  - player: Player Name
    game1: 150
    game2: 165
    game3: 172
  - player: Another Player
    game1: 145
    game2: 158
    game3: 162
---
```

**Important**: The `player` field must exactly match the `name` field in the player's file.

## Site Structure

```
├── _config.yml           # Jekyll configuration
├── _layouts/             # Page templates
│   ├── default.html      # Base layout with styling
│   ├── player.html       # Player profile template
│   └── week.html         # Weekly scores template
├── _players/             # Player data files
├── _weeks/               # Weekly score data files
├── index.html            # Home page
├── Gemfile               # Ruby dependencies
└── README.md             # This file
```

## How It Works

### Data Organization

- **Players**: Stored in `_players/` as individual markdown files with frontmatter
- **Weeks**: Stored in `_weeks/` as markdown files with scores in frontmatter
- **Collections**: Jekyll processes these as collections, generating individual pages

### Calculations

- **Weekly Totals**: Sum of game1 + game2 + game3 for each player
- **Player Averages**: Total pins across all games divided by total number of games played
- **Rankings**: Sorted using Liquid templating filters

### URL Structure

- Home: `/`
- Player pages: `/players/player-name/`
- Week pages: `/weeks/week-X/`

## Customization

### Styling

Edit the `<style>` section in `_layouts/default.html` to customize colors, fonts, and layout.

### Site Title and Description

Edit `_config.yml`:
```yaml
title: Your League Name
description: Your league description
```

## Sample Data

The repository includes sample data for demonstration:
- 6 players
- 3 weeks of scores

You can delete these and add your own data, or modify them to match your league.

## Tips

1. **Date Format**: Use YYYY-MM-DD format for week dates to ensure proper sorting
2. **Player Names**: Keep player names consistent across all week files
3. **Scores**: Enter scores as integers without any formatting
4. **Regeneration**: The site automatically rebuilds when you save files (when running `jekyll serve`)

## Troubleshooting

**Players not showing up?**
- Check that the player file exists in `_players/`
- Verify the `name` field matches exactly in both player and week files

**Averages not calculating?**
- Ensure all scores are valid integers
- Check that the player has scores recorded in at least one week

**Site not updating?**
- Stop and restart `bundle exec jekyll serve`
- Clear the `_site/` directory and rebuild

## License

Free to use and modify for your bowling league!
