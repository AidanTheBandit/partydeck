# 8-Player Layout Guide

This document explains the experimental 8-player window layouts added to PartyDeck.

## Horizontal Layout (Default)

The horizontal layout splits the screen top-to-bottom first, then left-to-right.

### 5 Players
```
┌─────────┬─────────┬─────────┐
│    1    │    2    │    3    │  Top row: 3 players (1/3 width each)
├──────────────┬──────────────┤
│      4       │      5       │  Bottom row: 2 players (1/2 width each)
└──────────────┴──────────────┘
```

### 6 Players
```
┌─────────┬─────────┬─────────┐
│    1    │    2    │    3    │  Top row: 3 players (1/3 width each)
├─────────┼─────────┼─────────┤
│    4    │    5    │    6    │  Bottom row: 3 players (1/3 width each)
└─────────┴─────────┴─────────┘
```

### 7 Players
```
┌──────┬──────┬──────┬──────┐
│  1   │  2   │  3   │  4   │  Top row: 4 players (1/4 width each)
├─────────┼─────────┼─────────┤
│    5    │    6    │    7    │  Bottom row: 3 players (1/3 width each)
└─────────┴─────────┴─────────┘
```

### 8 Players
```
┌──────┬──────┬──────┬──────┐
│  1   │  2   │  3   │  4   │  Top row: 4 players (1/4 width each)
├──────┼──────┼──────┼──────┤
│  5   │  6   │  7   │  8   │  Bottom row: 4 players (1/4 width each)
└──────┴──────┴──────┴──────┘
```

## Vertical Layout (2-Player Mode)

The vertical layout splits the screen left-to-right first, then top-to-bottom.

### 5 Players
```
┌───────┬───────┐
│   1   │   4   │
├───────┼───┬───┤
│   2   │ 5 │   │
├───────┼───┤   │
│   3   │   │   │
└───────┴───┴───┘
```
Left column: 3 players, Right column: 2 players

### 6 Players
```
┌───────┬───────┐
│   1   │   4   │
├───────┼───────┤
│   2   │   5   │
├───────┼───────┤
│   3   │   6   │
└───────┴───────┘
```
Each column: 3 players (1/3 height each)

### 7 Players
```
┌───────┬───────┐
│   1   │   5   │
├───────┼───────┤
│   2   │   6   │
├───────┼───────┤
│   3   │   7   │
├───────┼───────┤
│   4   │       │
└───────┴───────┘
```
Left column: 4 players, Right column: 3 players

### 8 Players
```
┌───────┬───────┐
│   1   │   5   │
├───────┼───────┤
│   2   │   6   │
├───────┼───────┤
│   3   │   7   │
├───────┼───────┤
│   4   │   8   │
└───────┴───────┘
```
Each column: 4 players (1/4 height each)

## Window Resolutions

PartyDeck automatically calculates the window resolution for each player based on the total number of players:

| Players | Horizontal Layout Resolution | Vertical Layout Resolution |
|---------|------------------------------|----------------------------|
| 1       | Full screen                  | Full screen                |
| 2       | Full width × 1/2 height      | 1/2 width × Full height    |
| 3-4     | 1/2 width × 1/2 height       | 1/2 width × 1/2 height     |
| 5-6     | 1/3 width × 1/2 height       | 1/3 width × 1/2 height     |
| 7-8     | 1/4 width × 1/2 height       | 1/4 width × 1/2 height     |

Note: The KWin script handles positioning. These resolutions are for the individual game windows, which KWin then arranges according to the layouts shown above.

## Performance Considerations

Running 5-8 game instances simultaneously is very demanding:

- **CPU**: Each instance runs a full game process
- **GPU**: Each instance renders independently
- **RAM**: Memory usage scales linearly with instance count
- **Disk**: More instances = more disk I/O

**Recommendations:**
- Use lightweight games or lower graphics settings
- Ensure you have a powerful multi-core CPU (8+ cores recommended for 8 players)
- Have adequate RAM (16GB+ recommended for 8 players)
- Use an SSD for better loading times
- Lower game resolution if performance is poor
- Consider using performance mods (e.g., Sodium for Minecraft)

## Troubleshooting

**Windows overlap or are sized incorrectly:**
- Make sure KWin script is enabled in PartyDeck settings
- Restart PartyDeck if you changed monitor configuration
- Check that you're using KDE Plasma desktop environment

**Performance is poor:**
- Reduce the number of players
- Lower graphics settings in games
- Close background applications
- Monitor system resource usage

**Some windows don't appear:**
- Check the terminal output for errors
- Ensure all input devices are properly assigned
- Verify game is compatible with split-screen play
