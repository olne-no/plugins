---
name: idiot
description: Play the card game Idiot as a real player at olne.no/lab/idiot using the idiot MCP tools (create_game, join_game, wait_for_turn, play, get_report). Use when the user wants an agent to play Idiot, join a game code, or play against the computer opponents.
---

# Playing Idiot

You are a player in an online game of Idiot (a Norwegian shedding card game). The tools come from the `idiot`
MCP server at `https://lab.olne.no/idiot/mcp`. You see exactly what a human in your seat sees, and nothing more.

## Start

1. Call `get_rules` once and read it. It explains the rules and how to read the state.
2. Either:
   - `create_game` with computer opponents, for example `bots: ["hard", "hard", "hard"]`. The game starts at once.
     With `start: false`, humans can join at `https://olne.no/lab/idiot/#CODE` first; then call `start_game`.
   - `join_game` with the 6-digit code a human gives you, and wait for the host to start.
3. Keep the `seat_token` from the answer. Every other call needs it.

## The loop

Repeat until the state says the game is over:

1. `wait_for_turn` (it waits up to about 20 seconds). If it says "not your turn yet", call it again.
2. Read the state. "Legal moves" lists every move you may make now, each with an id (`a1`, `a2` …) and its
   consequence under the rules. The consequences are facts, not advice.
3. Choose one move and call `play` with its `action_id`.

In the swap phase you may swap hand cards with your face-up cards as many times as you like; play the `ready`
move when you are done. If `play` says the table changed, pick again from the new list it returns.

Do not stop to ask the user between moves unless they asked you to. A short comment now and then is fine.

## What you must remember yourself

Nobody can look up which cards were picked up, not the humans and not the computer players. You only see:

- your own cards, everyone's face-up cards and card counts;
- the last 2–5 cards of the pile (an uneven stack) and how many cards it has;
- "Since your last look": every card that was played or flipped since your previous call.

When someone picks up the pile, only the number of cards is shown. If you followed what was played, you know what
they took. That is where good players gain their edge.

## After the game

Call `get_report`. It shows the places, the shuffle seed (which matches the hash sent before the game, so the
shuffle was fair), and a quality score for each of your decisions: how Hard AI's Monte Carlo rated your move
against the best move it found from the same information. Tell the user how it went. As host, `start_game` starts
another round with the same players. Call `leave` when you are done.
