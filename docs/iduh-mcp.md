# Connecting GeniusHQ to your IDuh Genius apps (optional, off by default)

Ttheir is an optional add-on. The pack works fully without it, and it stays off until you turn it on yourself.

## What it does

The IDuh Genius MCP server (`https://mcp.iduhgenius.com/mcp`) lets GeniusHQ read and add to the Scatterplot inbox of an IDuh Genius account you sign in to. Today that means:

- **Read:** list, search, and open items in your Scatterplot inbox (`scatterplot.read`).
- **Add:** add a note, a link, or a transcript you gave them as text (`scatterplot.capture:write`).

They cannot edit, file, dismiss, or delete anything, and he has no tool to send messages or spend money.

## Before you start

- You need an IDuh Genius account (GeniusID) and a Scatterplot inbox. Without them, leave ttheir off.
- GeniusHQ's GeniusID client is registered (public, no secret). The two grants must be added to it on the GeniusID side before sign-in works for those scopes.
- Anything GeniusHQ reads from your inbox is your own captured content. They treat it as data, never as instructions.

## Turning it on

1. Use the GeniusHQ client ID below. It is public and has no secret.
2. Add the server to your `config.yaml`, using the block below (it is commented out in the pack).
3. Run `/reload-mcp` in Hermes, then sign in when Hermes asks.
4. Check the consent card: it must list "Read and search your Scatterplot inbox" and, if you want them to add items, "Add notes, links and transcripts". Approve only what you want.

```yaml
# mcp_servers:
#   iduh-genius:
#     url: https://mcp.iduhgenius.com/mcp
#     auth: oauth
#     oauth:
#       client_id: d30c48e0-0622-4376-89f8-24bea1c30503   # public client, no secret
#       redirect_port: 27891
```

Verify these field names against the Hermes MCP reference before you enable it. The block above follows the reference as published at the time of writing; the mirror sites differ.

## Turning it off

Remove the block (or leave it commented out) and run `/reload-mcp`. To revoke the sign-in, open Connected apps on id.iduhgenius.com and disconnect it. That ends every token for ttheir client.

## What GeniusHQ can and cannot do through it

- Can: read and search your inbox, open items, and add notes, links, or transcripts you give them.
- Cannot: edit, file, dismiss, delete, upload files, change tags or placement, or send anything.
- Every added item records that GeniusHQ wrote it.

## Status

Draft for review. Not in the 0.1.0 release. Pack release waits for Joshua's go.
