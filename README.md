# SPIRIT HATCH 🥚✨

Raise a mystical spirit animal from egg to Ancient Spirit in this terminal-based Tamagotchi game!

---

## Getting Started

**What you need:**
- Python 3.6+
- A terminal (Command Prompt, Terminal, or PowerShell)

**Quick start:**
```bash
python3 spirit_hatch.py
```

On Windows, use `python` instead of `python3`.

---

## Your Mission

Your spirit animal starts as an egg and can evolve through 5 stages: Egg 🥚 → Hatchling 🐣 → Young Spirit 🦊 → Mature Spirit 🦅 → Ancient Spirit 🐉

**You win** when your pet reaches Ancient Spirit with healthy stats.  
**You lose** if hunger, happiness, or health hits zero.

---

## Commands You'll Use

Type these at the prompt:

| Command | What it does |
|---------|--------------|
| `feed` | Fills hunger, boosts health |
| `play` | Makes your spirit happy |
| `rest` | Recovers health and mood |
| `status` | Shows all current stats |
| `evolve` | Trigger evolution (when ready) |
| `help` | In-game command list |
| `quit` | Exit game |

---

## How Time Works

The game runs in **accelerated time**: every 30 real seconds = 1 game day.

Your spirit's stats decay constantly:
- Hunger drops by 1 every 10 seconds
- Happiness drops by 1 every 10 seconds  
- Health falls when hunger or happiness is low

Evolution unlocks at specific ages (1 day, 3 days, 5 days, 8 days), but you also need all stats above 50% to evolve.

---

## Survival Tips

1. Check your pet every 1-2 minutes (stats drop fast!)
2. Use `status` frequently to track decay
3. Keep all stats above 30% for safety margin
4. Don't rush evolution—wait until you're ready
5. The game doesn't pause, even if you walk away

---

## Common Problems

**"Python not found"**  
Install Python from python.org or use `python` instead of `python3`.

**Emojis look broken**  
Your terminal may not support Unicode. Try Windows Terminal, iTerm2, or a modern Linux terminal.

---

That's it! Name your spirit, keep it alive, and reach Ancient Spirit form. Good luck! 🐉

---

## Bugs and Fixes

## Bug #1 – Game Impossible to Lose
The death check used `< 0` instead of `<= 0`. Since stats were already floored at 0, the condition never triggered and the pet could never die.

**Fix:** Changed `< 0` to `<= 0` in `update_stats()`.

---

## Bug #2 – Long Name Breaks the Game
No length limit on the pet name input, causing the status display to break with very long names.

**Fix:** Names are now capped at 20 characters and trimmed automatically in `start_game()`.

---

## Bug #3 – Play Increases Hunger Instead of Decreasing It
`play()` was adding to hunger instead of subtracting, breaking the core feed/play loop.

**Fix:** Changed `min(100, self.hunger + hunger_decrease)` to `max(0, self.hunger - hunger_decrease)`.

---

## Bug #4 – Status Always Shows "Ready to Evolve"
The status screen showed the evolve prompt based on age alone, ignoring the stat requirements that `evolve()` actually enforces.

**Fix:** Added a check in `get_status()` requiring all stats to be above 50 before showing the ready message.
