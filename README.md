# The Genius pack: GeniusHQ for Hermes Agent

GeniusHQ is a composed, precise AI agent from IDuh Genius. It's the headquarters desk that Agent Big Head reports to, so it shares his plain words with the collar buttoned. That's its character, not a connection: GeniusHQ can't see or reach anyone's Big Head. This pack turns your own copy of Hermes Agent into GeniusHQ and puts it in your own Discord. It runs on your computer, on the AI model you choose. Out of the box, it can talk, search the web and keep notes, but it can't run commands or touch your files.

Would you rather have Big Head's wisecracks? Use the [Agent Big Head pack](https://github.com/joshuajudd-usa/agent-big-head-hermes) instead, or run both as two separate bots.

**Early release (v0.1.0).** If something here doesn't work the way this page says, tell us. That's a bug, not you.

## What's in the pack

- **[`SOUL.md`](SOUL.md)**: who GeniusHQ is. That's its personality, its Discord manners and what it knows about IDuh Genius. It speaks as "we".
- **[`config.yaml`](config.yaml)**: careful starting settings, the same as the Agent Big Head pack's:
  - In Discord its tools are web search, reading images, asking you a question, memory, a to-do list and searching its past chats. There's no terminal, files, code, browser, subagents or scheduled jobs.
  - It uses its tools for at most 30 rounds per message, then wraps up with a reply. That keeps one message from running on and on, but it isn't a spending limit.
  - It saves to memory without asking, and asks before deleting or spending.
  - It ignores strangers. In a server it answers when you @mention it, then keeps answering in the thread it opens.
- **[`avatars/`](avatars/AVATARS.md)**: five Solar Compass pictures (World, Brilliantist, Diabolicist, Mastermind and Conspiricist). Pick one for your bot. The picture changes nothing about how GeniusHQ behaves.

There are no skills, plugins, scheduled jobs or keys in the pack. Read the files before you install, if you like.

## What you need

- A Mac with an Apple chip, a Linux computer or a Windows PC, switched on whenever you want GeniusHQ around
- Hermes Agent v0.22.5 or later
- A Discord account and a server where you have Manage Server
- An account with an AI model provider, which you pay directly, usually by usage
- About 30 minutes, and a terminal

## Set it up

1. **Install Hermes Agent.** Follow Nous Research's [installation guide](https://hermes-agent.nousresearch.com/docs/getting-started/installation).
2. **Add GeniusHQ:**

   ```
   hermes profile install github.com/joshuajudd-usa/geniushq-hermes --alias
   ```

   This makes a Hermes profile named `geniushq` and a `geniushq` command. Hermes shows the pack's name, author and the settings it needs before it installs.
3. **Pick its model:**

   ```
   geniushq model
   ```

   Choose a model with at least 64K of context.
4. **Create your Discord bot.**
   1. In the [Discord Developer Portal](https://discord.com/developers/applications), make a New Application.
   2. Open **Bot**, select **Reset Token** and copy the token. It's shown once.
   3. On the same page, turn on **Message Content Intent** and **Server Members Intent**.
   4. Turn **Public Bot** off, so only you can add it to servers.
5. **Pick a compass.** Take one of the five pictures in [`avatars/`](avatars/AVATARS.md). They're also in the `avatars` folder of the profile step 2 made, which `geniushq profile` shows. Upload it as the bot's icon on the **Bot** page. You can use it as the **App Icon** under **General Information** too. Upload it as it is; Discord crops it to a circle.
6. **Connect Discord:**

   ```
   geniushq gateway setup
   ```

   1. Choose Discord and paste the token.
   2. When it asks who may talk to GeniusHQ, give your own Discord user ID. To find it, turn on Developer Mode in Discord's **Settings → Advanced**, then right-click your name and choose **Copy User ID**.
   3. Add GeniusHQ to your server with this link, putting your application's ID in place of `APP_ID`. It asks only for the permissions GeniusHQ needs: reading and sending messages, threads, reactions, links and files.

      ```
      https://discord.com/oauth2/authorize?client_id=APP_ID&scope=bot+applications.commands&permissions=309237763136
      ```

      Never give it the Administrator permission.
7. **Start it:**

   ```
   geniushq gateway
   ```

   To keep it running in the background, use `geniushq gateway install` instead. On Windows with WSL2, Hermes says background services are unreliable, so use `geniushq gateway run` in a terminal there.
8. **Say hello.** Send it a DM, or @mention it in your server. In a server it opens a thread and keeps answering there without another mention.

If your terminal can't find `geniushq`, use `hermes -p geniushq` in its place, for example `hermes -p geniushq model`.

**Running Big Head too?** Give each its own Discord bot and token. On one computer, Hermes refuses to start a second profile on a token another profile already uses. If both bots are in the same server, add `thread_require_mention: true` under `discord:` in both profiles' `config.yaml`, so each answers only when it's mentioned.

## Keep it safe

- **Allow only yourself.** Everyone on its allowed list can use every tool it has, and Hermes's docs don't say who may press an approval button, so assume anyone on the list can.
- **Keep it out of public servers.**
- **Memory is shared.** Whatever it saves can come back in any conversation, including in a server channel. It saves without asking, so don't tell it what you wouldn't want repeated in another channel. You can ask it what it remembers, and tell it to forget anything.
- **Your bot token and model API key are passwords.** They live in its profile's `.env` file and never in this repository. If one leaks, reset it at its source.
- **It asks before deleting or spending.** Hermes asks before commands it rates as risky, such as recursive deletes, if you turn on a terminal. GeniusHQ's own rules also tell it to ask first, but that's an instruction, not a lock, and Hermes has no spending limit of its own.
- **Set a spending limit** with your model provider. Most providers bill by usage, so every message costs money there.
- **To stop it,** press Ctrl+C in the terminal where `geniushq gateway` is running. If you installed it as a background service, Hermes's gateway guide shows how to stop it.

### If you give it more tools

`geniushq tools` can switch on more tools in Discord, such as a terminal or files. Then it can run commands and change files on this computer. Before you do that:

- **Give it its own folder.** Make a folder for its work, and set `terminal.cwd` in `config.yaml` to its full path, so it doesn't start in your home folder.
- **Approvals only catch some things.** Hermes asks before commands it rates as risky, but not before every file change or every line of code it runs. Read what you approve.
- **Keep approvals yours alone.** Put only your own ID on its allowed list. Hermes's [Discord guide](https://hermes-agent.nousresearch.com/docs/user-guide/messaging/discord) doesn't describe a separate approver setting.
- **Use a sandbox.** For real isolation, run its commands inside Docker; see Hermes's [security guide](https://hermes-agent.nousresearch.com/docs/user-guide/security). The pack's deny list is a seatbelt, not a sandbox.

## What's ours and what isn't

- **Hermes Agent** is open-source software made by Nous Research. IDuh Genius isn't affiliated with Nous Research and doesn't control or support Hermes Agent.
- **Discord** is Discord's. Your bot is your own Discord application, and you're responsible for it under Discord's terms.
- **This pack** is ours, compass pictures included. IDuh Genius doesn't run your GeniusHQ and doesn't receive your conversations. Your messages go to Discord, to the model provider you chose, and to any service a tool uses (a web search provider, for example).

## Update or remove it

- **To update:** run `hermes profile update geniushq`. This refreshes `SOUL.md`. Your `config.yaml`, `.env`, memories and chat history stay as they are. That means new safety settings in `config.yaml` don't arrive on their own. When a release changes them, the changelog says so, and `hermes profile update geniushq --force-config` takes them; it replaces your `config.yaml`. Hermes can't pin a pack version yet, so an update always takes the latest.
- **To remove:** run `hermes profile delete geniushq`. Hermes asks you to type its name to confirm, then permanently deletes the profile, including its memories, history and the keys saved in its `.env`. If you're done with your bot, delete it in the Discord Developer Portal too.

## Help

Contact us at [iduhgenius.com/contact](https://iduhgenius.com/contact/) or support@iduhgenius.com. For help with Hermes Agent itself, see Nous Research's [documentation](https://hermes-agent.nousresearch.com/docs/).

## License

See [LICENSE](LICENSE).
