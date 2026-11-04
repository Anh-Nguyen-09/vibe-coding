# Project: Maze Capture the Flag

> - **Files:** maze_capture_the_flag.html
> - **Dates:** 2026-10-25 → 2026-11-04
> - **Defaults:** Claude · Sonnet 5.5
> - **Status:** prototype
> - **Use:** Built as a candidate for a ChatGPT multiplayer game challenge (due 2026-10-31); not used in any event yet
> - **Reusability:** artifact medium · prompt pattern medium
> - **Tags:** single-file-html, game, canvas, source-material
> - **Takeaway:** One long, very specific design prompt (rules, controls, scoring) produced a playable single-file game; the earlier rounds of trying other game types were what made the prompt specific.
> - **Story value:** anecdote
> - **Surprises:** The assistant found a real fairness bug (the bot had rules the player's side lacked) by running 30 automated bot-vs-bot matches. Earlier versions (territory capture, dice duel) were scrapped because they felt "clunky and hard to play".

Background: this is a single-player preview of a two-team capture-the-flag game. I play BLUE against a RED bot. The 12 pixel-art zodiac characters were made earlier for my Astraeum Tower dungeon game. The full online multiplayer version was meant to be built in ChatGPT, so this prototype was for working out the rules.

# Prompt 1 (maze capture-the-flag redesign):

> - **Tool:** Claude · Sonnet 5.5 · 2026-10-26
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none (the prompt and output were originally written in Vietnamese; translated to English for this repo)

Cut the time down to 5 minutes, keep only the Attack and Defend commands, and make the map like the one in Astraeum, where you move around a layout with obstacles (you can't walk through walls). Make it a dungeon-style maze with lots of nooks and corners, but still divided into rooms that can be chosen as a base. Rooms that aren't chosen have no special effect and are just normal rooms, and every room gets a random item or chest each time. At the start of the match you can choose one fixed character to be the leader. You can steer the leader through the maze to find items (they can heal, or boost attack/defense depending on the type) and lead 6 teammates who follow along to attack together. The other 5 characters stay behind to guard the flag, and you also choose a leader for the defense team that you can switch to when needed. Both sides explore and grab chests/items while searching for the room holding the opponent's flag so they can steal it. Scoring stays the same. Add an Interact button so a leader can steal the flag or take it back. While carrying the flag home you can still fight to win it back. The controls are: move in 4 directions, switch leader (to watch and direct either the defense or the attack team), interact to pick up the flag, retreat (when you want the team to steady its formation), and attack (when facing the enemy team). Leaders who aren't being steered still automatically follow their team's role, and when you press Attack they fight automatically like the other characters. Characters do one basic attack and then use an elemental skill (3s cooldown).

## Output 1:

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

# Prompt 2 (translate the game into English):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

convert to english

## Output 2:

I've translated the whole game into English and sent it again as `astraeum-maze-flag.html`. That covers the menus, the rules screen, in-game messages, skill descriptions, room names and the result screens. The zodiac characters now use their English names (Aries, Taurus and so on), and the title is now "Maze Capture the Flag".

I checked that it loads and runs without errors, and I looked at the lineup screen after shortening two long lines that overlapped the Continue button. I did not play a full match, so some of the longer in-game messages may still look crowded.

This is a separate copy; the original Vietnamese artifact is unchanged.
