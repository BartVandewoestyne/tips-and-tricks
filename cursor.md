# Cursor

## Configuration files

* Global (user) config files:
  * Main IDE settings:
    * Editor settings: `~/.config/Cursor/User/settings.json`
    * Keybindings: `~/.config/Cursor/User/keybindings.json`
    * Snippets: `~/.config/Cursor/User/snippets/`
    * Extensions: `~/.config/Cursor/User/extensions/` (or similar under the Cursor app data dir)
    * App state / storage: `~/.config/Cursor/User/globalStorage/`, `~/.config/Cursor/User/workspaceStorage/`
  * Cursor-specific user config:
    * CLI config: `~/.cursor/cli-config.json`
    * User hooks: `~/.cursor/hooks.json`, `~/.cursor/hooks/*`
    * User skills: `~/.cursor/skills/`
    * User agents: `~/.cursor/agents/`
    * Slash commands: `~/.cursor/commands/*.md`
    * Built-in skills (system-managed): `~/.cursor/skills-cursor/`
    * Project metadata (transcripts, MCP cache, canvases): `~/.cursor/projects/<workspace>/`
    * MCP server metadata: `~/.cursor/mcps/`
* Project (workspace) config (usually checked into git):
  * Workspace settings: `.vscode/settings.json`
  * Cursor rules: `.cursor/rules/*.mdc`
  * Project skills: `.cursor/skills/`
  * Project hooks: `.cursor/hooks.json`, `.cursor/hooks/*`
  * Project agents: `.cursor/agents/`
  * Project slash commands: `.cursor/commands/*.md`
  * CLI overrides: `.cursor/cli.json` (merged over `~/.cursor/cli-config.json`)