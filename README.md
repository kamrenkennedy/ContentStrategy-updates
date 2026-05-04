# Content Strategy — Updates

Auto-update feed for [Content Strategy](https://kamstudios.com), a content planning + AI-assisted social media manager in the Aligned product suite.

The application source lives in a private repository. This public repository hosts only the [Sparkle](https://sparkle-project.org) update feed (`appcast.xml`) and the released `.zip` artifacts (as GitHub Releases).

## What's here

- **`appcast.xml`** — the feed Sparkle reads on the user's Mac on each update check. Updated each release.
- **Releases tab** — released `.zip` artifacts (one per version), referenced by `appcast.xml`'s `<enclosure>` URLs.

## Connect Claude Code to your library (v1.0.4+)

Once Content Strategy v1.0.4 is installed at `/Applications/ContentStrategy.app`, you can connect Claude Code (or Claude Desktop) directly to your library through MCP. Seven tools — `list_brands`, `list_posts`, `read_creative_profile`, `create_post`, `attach_media`, `update_post`, `delete_post` — let Claude read and write your content via stdio.

Add to your `~/.claude/settings.local.json` (or per-project `.mcp.json`):

```json
{
  "mcpServers": {
    "content-strategy": {
      "command": "/Applications/ContentStrategy.app/Contents/Resources/ContentStrategyMCP.app/Contents/MacOS/ContentStrategyMCP"
    }
  }
}
```

Reload Claude Code. The seven tools surface as MCP tools.

The MCP server shares the same iCloud + CloudKit private database as the app, so writes from Claude appear in the running app within ~30 seconds via CloudKit sync. Cross-Mac sync also works through your iCloud account — the MCP server can be invoked from any Mac signed into the same Apple ID.

## Release flow (for the maintainer)

1. Archive a notarized `.app` build of Content Strategy
2. Zip it → run Sparkle's `sign_update` against the zip to get an EdDSA signature
3. Create a new GitHub Release here; upload the zip as the release asset
4. Update `appcast.xml` with a new `<item>` (title, version, signature, asset URL, length)
5. Commit + push `appcast.xml`
6. Sparkle on user Macs picks up the change on the next scheduled check

## Privacy / scope

This repository is public so the appcast feed and release artifacts are reachable by users' Sparkle update checks. It contains only:

- One XML feed file
- Published release `.zip` artifacts

It does NOT contain the application source, planning artifacts, design files, or any internal materials.
