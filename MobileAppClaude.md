# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ChessLoops is a React Native/Expo mobile chess training app implementing the Woodpecker Method. Users solve sets of 50 puzzles repeatedly until mastery (96% accuracy in under 5 minutes), then unlock progressively harder sets.

## Commands

```bash
# Install dependencies
npm install

# Start development server
npx expo start

# Run on iOS simulator
npx expo start --ios

# Build for production
npx eas build --platform ios
```

## Architecture

### Context Providers (wrap app in this order)

- `AuthProvider` - Supabase authentication, user session
- `ProgressProvider` - User progress tracking, set unlock logic
- `SettingsProvider` - Board theme preferences

### Navigation Structure

- **Stack Navigator** (root): Auth | Main | PuzzleSolve | Results
- **Tab Navigator** (Main): Progress | Statistics | Settings

### Key Data Flow

1. Puzzles defined in `src/data/puzzles.ts` as typed arrays
2. Puzzle set configs in `src/constants/puzzleSets.ts` (order determines unlock sequence)
3. `ProgressContext` manages unlock state - a set unlocks when the previous set is passed
4. Pass requirements: 48/50 correct AND under 300 seconds

### Puzzle Data Format

Puzzles use Lichess format:

- `fen`: Board position
- `moves`: UCI format array (e.g., `["e2e4", "e7e5"]`) - first move is opponent's, then alternating
- `rating`: Difficulty (600-800 = Rook-ie, 800-1000 = Little, 1000-1200 = Mega)
- `themes`: Tags like "endgame", "fork", "mateIn2"

### Supabase Schema

Tables: `profiles`, `user_progress`, `set_progress`, `set_attempts`

- Row Level Security enforced - users access only their own data
- `handle_new_user()` trigger creates profile on signup

## Adding New Puzzle Sets

Puzzle data comes from Lichess CSV files stored locally. Do NOT attempt to fetch puzzles from the Lichess API or scrape web sources — always ask the user for the CSV file path if puzzle data is needed.

### Puzzle Source Files

Source CSV files are in `LiChessPuzzles/csv set/` (gitignored, ~1GB total):

- `lichess_db_puzzle_1.csv` through `lichess_db_puzzle_11.csv`
- ~500,000 puzzles per file, split from the original Lichess database

### Search Strategy

When building puzzle sets, search the CSV files sequentially:

1. Start with `lichess_db_puzzle_1.csv`
2. If the request can't be fulfilled completely or accurately (not enough puzzles matching criteria), continue to `lichess_db_puzzle_2.csv`
3. Continue through subsequent files until the request is satisfied

### Steps

1. Extract puzzles using `LiChessPuzzles/extract_puzzles.py`:

   ```bash
   python extract_puzzles.py --csv-path "csv set/lichess_db_puzzle_1.csv" --rating-min 800 --rating-max 1000 --theme endgame --count 50 --shuffle
   ```

2. Add puzzle array to `src/data/puzzles.ts`

3. Add set config to `src/constants/puzzleSets.ts` with appropriate `order` value

4. Update UI slices in `ProgressScreen.tsx` and `StatisticsScreen.tsx` if adding free sets

## Naming Conventions

- **Set IDs**: `{level}-{phase}-{number}` (e.g., `little-endgame-1`)
- **Array names**: `{level}{Phase}Puzzles{number}` (e.g., `littleEndgamePuzzles1`)
- **Levels**: Rook-ie (600-800), Little (800-1000), Mega (1000-1200), Hyper (1200-1400), Grand (1400+)
- **Phases**: endgame, midgame, opening
