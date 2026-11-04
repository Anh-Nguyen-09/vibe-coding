# Project: Maze Capture the Flag

> - **Files:** maze_capture_the_flag.html
> - **Dates:** 2026-10-25 → 2026-11-04
> - **Defaults:** Claude · Sonnet 5.5
> - **Status:** prototype
> - **Use:** Built as a candidate for a ChatGPT multiplayer game challenge (due 2026-10-31); not used in any event yet
> - **Reusability:** artifact medium · prompt pattern medium
> - **Tags:** single-file-html, game, canvas, brainstorm
> - **Takeaway:** One long, very specific design prompt (rules, controls, scoring) produced a playable single-file game; the earlier rounds of trying other game types were what made the prompt specific.
> - **Story value:** anecdote
> - **Surprises:** The assistant found a real fairness bug (the bot had rules the player's side lacked) by running 30 automated bot-vs-bot matches. Earlier versions (territory capture, dice duel) were scrapped because they felt "clunky and hard to play".

Note: between Prompt 1 and Prompt 2 there were a few short follow-up messages (answers to the questions above and feedback on the first zone-based playable version) that are not included here.

Background: this is a single-player preview of a two-team capture-the-flag game. I play BLUE against a RED bot. The 12 pixel-art zodiac characters were made earlier for my Astraeum Tower dungeon game. The full online multiplayer version was meant to be built in ChatGPT, so this prototype was for working out the rules.

# Prompt 1 (first idea: Castlelands-style capture the flag):

> - **Tool:** Claude · Sonnet 5.5 · 2026-10-25
> - **Session:** continued · attached: none
> - **Verified:** human-tested
> - **Human edits:** none (the prompt and output were originally written in Vietnamese; translated to English for this repo; Verified raised to human-tested after I played it myself 2026-11-04)

Earlier in this chat I had tried a dice-duel idea and wanted something different. This is where the capture-the-flag game started.

I have a thought like this: similar to the game Castlelands, an RTS. For now just 2 sides, each with the same number of units and the same skill set from the 12 characters, differing only in color (blue or red), on one map area with all kinds of terrain. Each side takes turns choosing the terrain area it wants and stations its units there. Each side secretly chooses where to plant its flag. The rules are to split into a defense team, a scouting team and an attack team that support each other to capture the opponent's flag and protect your own. The game lasts about 10 minutes. During that time, whichever side captures a flag first gets 10 points, and every minute a side keeps its flag safe adds 2 more points. A side that loses its flag has to go and win it back if it wants points, because while the flag is lost it gets none. There will be a countdown at the top center of the screen. If time runs out and neither side has a flag, it is decided by the number of kills on the other side (each character has only 1 life and a health bar; characters automatically attack or defend depending on the position the player assigned; the two sides fight each other according to their roles; players have to work out how to make skills complement each other or fit their position).

## Output 1:

This direction is completely different from the previous two versions, and I think it's much better. Fog, a hidden flag and split roles create real situations for the player to think about, rather than just comparing scores. Here is how I understand it, plus a few points you need to settle.

## Rules as I understand them
- **Symmetric sides:** the same 12 characters with the same skills, differing only in blue/red. Nobody is stronger; you win by how you arrange things.
- **Setup:** flip a coin, the two sides take turns choosing terrain areas to station in, then secretly choose where to plant the flag inside their own area.
- **A 10-minute match** with a countdown clock at the top center.
- **Scoring:**
  - Every minute your flag stays safe: **+2**.
  - Capturing the enemy flag first: **+10**.
  - If your flag is captured, the +2 stops until you get it back.
  - If time runs out and both sides have lost their flags, kills decide it.
- **Each character has only 1 life** and fights automatically according to the order you give. You don't control individual hits; you assign roles and positions, then change orders as the situation changes.

## Giving orders
There are 4 roles, and you can assign any character to any of them:
- **Defense:** stand guard at a point.
- **Scout:** patrol between points, avoid fights, and lift the fog to find the enemy flag.
- **Attack:** advance to a chosen point, fight everything on the way, and grab the flag if it's seen.
- **Support:** follow a teammate, healing and buffing.

A role is an order, not locked to a character. You could send Taurus to attack, but its skill would be wasted. That is the "calculation" part you wanted.

## Terrain (one effect each, so a new player understands at a glance)
- **Forest:** hides units; enemies only see them up close.
- **Mountain:** good for defense, long sight.
- **River / swamp:** slows movement.
- **Grassland:** fast to cross but easy to spot.

## The 12 characters (suggested best-fit roles)
| Best role | Sign | Skill |
|---|---|---|
| Defense | Taurus | Taunt + stone armor |
| | Cancer | Reflects 30% damage |
| | Capricorn | Thorn trap roots enemies |
| Scout | Gemini | Clone, runs fast |
| | Sagittarius | Long sight, long-range shots |
| | Aquarius | Lightning bolt reveals enemy positions |
| Attack | Aries | Charge + burn |
| | Leo | Roar: adjacent allies get +ATK |
| | Scorpio | Poisoned throwing knives |
| Support | Virgo | Healing |
| | Libra | Swaps places, rescues the flag carrier |
| | Pisces | Wave pushes enemies back + speeds up allies |

The skills combine well, for example Capricorn roots and then Sagittarius shoots, or Libra pulls a flag carrier out of danger.

## Risks, stated plainly
This is the hardest direction of all the ones I've offered. 24 characters moving freely, finding their own paths, with per-side fog, are very easy to desync, and you only have 6 days. I suggest the first version **splits the map into about 12 connected zones** (a 4x3 grid), where characters move from zone to zone, taking time depending on terrain. Fights happen inside a zone and are calculated every second. It is still real time with a 10-minute clock, but without pathfinding the server sends very little data. Fog is also simpler: you see any zone where you have units, and the rest is hidden.

## What I need you to decide
1. **Flag:** once a flag is captured, does the captor have to carry it back to base to get +10, or does touching it count right away? If the two sides keep stealing it back and forth, is the +10 given only once (to whoever captured first) or every time? By default I'd say carry it back to base, with +10 only for the first capture.
2. **Movement:** linked zones (my recommendation) or free movement on the map?
3. **Orders:** give orders to groups of 3 characters with the same role (faster on a phone) or per character? I lean toward groups of 3, which can be split when needed.
4. **Preview:** because of the fog, two players can't share one screen. I'd build a version you play against a red bot so you can see how a match runs. Is that okay?

Reply to these 4 questions (or just say "use your defaults") and I'll start building.

# Prompt 2 (redesign as a real-time dungeon maze):

> - **Tool:** Claude · Sonnet 5.5 · 2026-10-26
> - **Session:** continued · attached: none
> - **Verified:** human-tested
> - **Human edits:** none (the prompt and output were originally written in Vietnamese; translated to English for this repo; Verified raised to human-tested after I played it myself 2026-11-04)

Cut the time down to 5 minutes, keep only the Attack and Defend commands, and make the map like the one in Astraeum, where you move around a layout with obstacles (you can't walk through walls). Make it a dungeon-style maze with lots of nooks and corners, but still divided into rooms that can be chosen as a base. Rooms that aren't chosen have no special effect and are just normal rooms, and every room gets a random item or chest each time. At the start of the match you can choose one fixed character to be the leader. You can steer the leader through the maze to find items (they can heal, or boost attack/defense depending on the type) and lead 6 teammates who follow along to attack together. The other 5 characters stay behind to guard the flag, and you also choose a leader for the defense team that you can switch to when needed. Both sides explore and grab chests/items while searching for the room holding the opponent's flag so they can steal it. Scoring stays the same. Add an Interact button so a leader can steal the flag or take it back. While carrying the flag home you can still fight to win it back. The controls are: move in 4 directions, switch leader (to watch and direct either the defense or the attack team), interact to pick up the flag, retreat (when you want the team to steady its formation), and attack (when facing the enemy team). Leaders who aren't being steered still automatically follow their team's role, and when you press Attack they fight automatically like the other characters. Characters do one basic attack and then use an elemental skill (3s cooldown).

## Output 2:

**How to play**
- **Maze:** 31x13 tiles with real walls, generated randomly every match. There are 11 rooms, mirrored left and right to keep it fair. Paths are blocked, with nooks and loops.
- **Pick the Attack leader:** leads 6 teammates following in a line. You steer them with ▲◀▶▼ (or WASD / arrow keys).
- **Pick the Defense leader:** guards the flag with 4 others and fights on their own when enemies arrive. Press "Switch leader" (Q) to take control of this one, and the other leader goes back to running on their own.
- **Pick a room as your base:** your flag and the flag-guarding squad stay there; rooms you don't pick are just normal rooms. The bot's base is chosen far from yours.
- **Chests and items:** every room has 1 item (healing, attack boost or defense boost for the whole squad of whoever picks it up). There are also chests that open to one of the three at random.
- **Fog:** you can see the whole maze layout, but you only see enemies, flags and items within sight range.
- **Buttons:**
  - **Interact (E):** pick up the enemy flag, or take back your own flag.
  - **Retreat (R):** the squad stops fighting and returns to formation, running faster for 4 seconds.
  - **Attack (F):** when on, the leader you're steering also fights automatically. By default the leader does not attack until you press it.
- **Carrying the flag home:** the leader holding the flag has to return to their own base room to score. Fights still happen on the way, and if the carrier is taken down the flag drops on the ground.
- **Score and time:** unchanged (+10 per capture, every 30 seconds +2 if your flag is safe and +1 if you hold the enemy flag), 5-minute match.
- **Combat:** a basic attack, then an elemental skill on a 3-second cooldown. The skill effect is shown on the leader; other characters only get small effects to keep the screen readable.

**What I saw when running simulations**
- Two equally strong bot teams usually meet and nearly wipe each other out, or draw 20-20 because each side still has 5 flag guards left. A real player can slip past them, so it's hard to predict.
- I raised HP by 1.7x so a match doesn't end within 40 seconds, and made the red bot attack with its defense squad once its attackers run out.
- All the numbers (HP, damage, items, sight range, speed) are placeholders.

**Not verified:** the real fonts (the sandbox couldn't load them), sound, and tapping on a phone. The direction buttons support touch but haven't been tried on a real device.

Play a few matches and tell me what feels worst (speed, bot difficulty, sight range or the controls) and I'll keep adjusting. When you're happy with it, I'll write the brief for ChatGPT to build the online version, with about 5 days left before the Oct 31 deadline.

(Note: this output is the middle and end of the original final message; its opening paragraph could not be retrieved.)

# Prompt 3 (translate the game into English):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** human-tested
> - **Human edits:** none (Verified raised to human-tested after I played it myself 2026-11-04)

convert to english

## Output 3:

I've translated the whole game into English and sent it again as `astraeum-maze-flag.html`. That covers the menus, the rules screen, in-game messages, skill descriptions, room names and the result screens. The zodiac characters now use their English names (Aries, Taurus and so on), and the title is now "Maze Capture the Flag".

I checked that it loads and runs without errors, and I looked at the lineup screen after shortening two long lines that overlapped the Continue button. I did not play a full match, so some of the longer in-game messages may still look crowded.

This is a separate copy; the original Vietnamese artifact is unchanged.
