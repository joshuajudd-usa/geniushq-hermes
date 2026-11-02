# Changelog

## 0.1.0 (2026-11-09)

The first Genius pack.

- **`SOUL.md`:** GeniusHQ's persona (personality, product knowledge, Discord manners and running on your own Hermes Agent). It shares Agent Big Head's rules for safety, truth and consent, word for word. SHA-256 `01df139249291cc1adaeb3b63d7b11469a3d4a47a99d5b5aa09ac664b166bfbc`.
- **`config.yaml`:** the same settings as the Agent Big Head pack 0.1.0:
  - In Discord its tools are limited to web, vision, clarify, memory, to-do and past-chat search.
  - It uses its tools for at most 30 rounds per message, then wraps up with a reply.
  - Approvals are manual, with a deny list.
  - It saves to memory without asking and is told to ask before deleting or spending. There are no background memory reviews.
  - Strangers are ignored, it replies in servers when @mentioned (then keeps answering in the thread it opens), and it doesn't read earlier channel history.
- **`avatars/`:** five Solar Compass pictures to choose from for your bot: World of Geniuses, Brilliantist, Diabolicist, Conspiricist and Mastermind.
