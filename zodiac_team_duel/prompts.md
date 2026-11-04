# Project: Zodiac Team Duel

> - **Files:** zodiac_team_duel.html
> - **Dates:** 2026-11-04
> - **Defaults:** Claude · Sonnet 5.5
> - **Status:** prototype
> - **Use:** Built for this assignment as a playable card-battle prototype inspired by the Genshin Impact card game (elemental dice and reactions); not used in any event
> - **Reusability:** artifact medium · prompt pattern medium
> - **Tags:** single-file-html, game, card-game, turn-based
> - **Takeaway:** Describing the dice rules concretely (counts, faces, costs) got a playable game on the first pass; the later prompts fixed the screen flow and the turn and cost rules.
> - **Story value:** anecdote
> - **Surprises:** With strict "own element only" dice costs, a skill was rarely affordable from 7 random dice, so the assistant added 2 rerolls per round. An earlier automated test never played because it matched "Your turn" in the wrong letter case (the page shows it in capitals).

Note: this project started from an earlier 1-vs-1 prototype built in the same chat (not included). The three prompts below are the most recent ones that shaped the final game. The 12 pixel-art zodiac sprites come from my earlier Astraeum Tower game.

# Prompt 1 (3-vs-3 team game with element dice):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

generate me a cards fighting turn based game using the 12 zodiac sprites as card photos. each with a different element (7) and fighting in 2 teams. each teams has 3 cards. each round throw 7 dices with 8 faces of 7 element and an omni one. card can be played with the amount of same element dice as the requirement on card (ex: cancer is hydro (water) element and required 3 hydro dices to activate elemental skills, 3 hydro dices must be achieved if wanting to use cancer to attack). each card require 3-4 dices to activate elemental skill and 2 to active normal physical attack.

## Output 1:

The Zodiac Team Duel is published: a 3v3 card battle against a bot, using the 12 zodiac sprites as card art. A scripted play-through ran with no errors and no horizontal overflow at desktop width and at 390px phone width.

**How it follows your rules**
- **Teams:** you pick 3 of the 12 cards, or press Random team. The enemy gets 3 random cards you didn't pick.
- **Elements:** the 7 elements are Pyro (Aries, Leo), Hydro (Cancer, Pisces), Anemo (Gemini, Libra), Electro (Scorpio, Aquarius), Dendro (Virgo), Cryo (Sagittarius) and Geo (Taurus, Capricorn).
- **Dice:** each round both sides roll 7 dice. Each die has 8 faces: the 7 elements plus an Omni face that counts as any element.
- **Costs:** a card can only pay with dice of its own element or Omni. Normal attack costs 2 and deals 2 Physical damage. Elemental skills cost 3 or 4, shown on each card. Cancer needs 3 Hydro/Omni to use its skill.
- **Reactions:** Vaporize, Melt, Overloaded, Frozen, Swirl, Crystallize and the others are in. Taurus gains a shield from its skill and Virgo heals an ally.
- **Playing:** tap a move on one of your cards, then tap the enemy card to hit. Press End round when you're done. The round ends when both sides have ended it.

**One addition you should decide on:** I added 2 rerolls per round, before the fighting starts, where you tap dice and reroll them. With strict own-element-only costs, about 1 die in 4 matches a given card, so a 3–4 dice skill would rarely be affordable without it. If you'd rather have the pure rules with no rerolls, or a different number of rerolls, I can change it.

# Prompt 2 (separate screens, coin flip, dice screen, timer):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

I want the ui to be separate. choose cards -> flip coin to decide whose play first -> play screen (with cards on table) -> choose dice with rolling animation -> back to play screen -> take turn to play (15s choosing time)

## Output 2:

The Zodiac Team Duel now runs as separate screens, in the order you described. I tested the flow on desktop and phone width with no errors. I did not separately confirm the 15-second timeout actually ends your round, because my test run didn't reach that case.

1. **Choose cards:** pick your 3 cards or press Random team, then Start duel.
2. **Coin flip:** an animated coin shows who plays first. It lands on YOU or FOE and shows both teams underneath.
3. **Play screen:** both teams of cards sit on the table. A short "Rolling dice…" moment follows.
4. **Dice screen:** the 7 dice tumble with a rolling animation. You can tap dice and reroll them twice, then press Keep dice.
5. **Back to the table:** you take turns playing a move on a card, then tapping the enemy card to hit. Each of your turns has a 15-second timer bar, which turns red under 5 seconds. If it runs out, your round ends automatically.

The dice screen repeats at the start of every round.

# Prompt 3 (3 turns per round, new costs, attack animation, wind icon):

> - **Tool:** Claude · Sonnet 5.5 · 2026-11-04
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

i forgot to say, each round has 3 turns, and you can choose to skip if not have suitable dices to play. fix so each normal skill require 1 same elemental dice as the character and one is not (2 dices total to activate skill) and elemental skills require 2 same elemental dices and one is not (3 dices total). add animation for the attacks. fix the icon of anemo to be wind blowing instead of that swirl symbol

## Output 3:

The updated Zodiac Team Duel is published with all four changes. I ran it in a browser and saw the attack animation and new icon render, with no errors. I haven't played a full match through to the end.

- **3 turns per round:** each side gets 3 turns per round, alternating. The header shows turns left. The first player swaps every round.
- **Skip turn:** the End round button is now Skip turn. It uses up one of your 3 turns. If the 15-second timer runs out, that turn is skipped for you.
- **Costs:**
  - Normal attack is 2 dice: 1 of the card's element (Omni counts) plus any 1 other die.
  - Elemental skill is 3 dice: 2 of the card's element (Omni counts) plus any 1 other die.
  - The cost icons show the element dice plus a grey ✦ for the "any" die. I read "one is not" as any other die, so the extra die can be any element, not only a different one.
  - When paying, the game spends off-element dice first and Omni last.
- **Attack animation:** the attacker lunges, an element-coloured projectile flies to the target, and an impact ring bursts on arrival. Damage numbers and the hit shake land after the projectile. Physical attacks use ⚔️.
- **Anemo icon:** it's now 🌬️ (wind blowing) everywhere.

I made two changes you didn't ask for. All skills now deal 3 damage, since they all cost 3 dice. Cards now have 12 HP instead of 8, because 3 turns per round would otherwise end fights in about one round.
