# Lofi for Claude

[Lofi](https://studiolofi.com) is a wireframe canvas for builders. This plugin
connects Claude to your Lofi account so you can design low-fidelity flows in a
conversation, save them as private boards, keep working on them in Lofi, and
send a whole board back to Claude for review.

The plugin pairs a remote MCP connector with one skill. It contains no Lofi
application source.

- `.claude-plugin/plugin.json`: the plugin manifest.
- `.mcp.json`: the remote connector, `https://app.studiolofi.com/api/mcp/claude`.
- `skills/lofi-design/SKILL.md`: the design workflow Claude follows.

## What Claude can do with it

- **Design new boards.** Describe a product or a task. Claude works out the
  flow logic, drafts every screen with Lofi's component catalog and guidance,
  checks the structure with Lofi, and saves the result as a private board in
  your account. Claude-authored designs use no Lofi generation credits.
- **Change or extend a board.** Add screens, rework a flow, or add an
  alternative beside the original on the same board, with version checks so
  nothing is overwritten.
- **Open your boards.** List projects, open a board, and read its screens.
- **Review a board.** Send to Claude delivers the board's structure and a
  preview into the conversation for feedback.
- **Use Lofi's own model when you ask for it.** Lofi-model generation and
  variations spend Lofi credits at the rate shown in Lofi; Claude never
  switches to it on its own.

## Getting started

1. Install the plugin from the Claude directory, or add the connector URL
   above as a custom connector in Claude.
2. Sign in with your Lofi account when Claude asks. Signing in lets the
   connection read the projects you own, create private boards, and save the
   changes you request. Disconnect at any time from Claude's connector settings.
3. Ask Claude to wireframe something.

A free Lofi account is enough to start. Plans, limits and credits are
described at https://studiolofi.com.

## Privacy and terms

Use of the connector is governed by Lofi's
[privacy policy](https://studiolofi.com/privacy) and
[terms of service](https://studiolofi.com/terms). Optional analytics is off by
default and can be allowed during sign-in or in Lofi's privacy settings.

## Support

hello@studiolofi.com

## License

The files in this repository are released under the MIT License (see
`LICENSE`). The license covers this plugin bundle only; the Lofi application
and service are not open source and remain subject to Lofi's terms.
