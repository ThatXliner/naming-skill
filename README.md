<p align="center">
  <a href="https://github.com/kettanaito/naming-cheatsheet">
    <img src="./naming-cheatsheet.png" alt="Naming cheatsheet" />
  </a>
</p>

# Naming cheatsheet skill

An [agent skill](https://agentskills.io) that teaches coding agents how to name variables and functions. It packages [kettanaito/naming-cheatsheet](https://github.com/kettanaito/naming-cheatsheet) for Claude Code and other agents that read `SKILL.md` files.

The agent loads the skill when it writes new code, picks or reviews names, or renames things in a refactor. The skill covers:

- The S-I-D rule: names must be short, intuitive, and descriptive
- The A/HC/LC pattern for function names: `prefix? + action + high context + low context?`
- What the standard verbs mean: `get`, `set`, `reset`, `remove`, `delete`, `compose`, `handle`
- Boolean and state prefixes: `is`, `has`, `should`, `min`/`max`, `prev`/`next`
- Contractions, context duplication, and singular vs. plural names

## Installation

### Claude Code (plugin)

In Claude Code, run:

```
/plugin install naming-cheatsheet --marketplace ThatXliner/naming-skill
```

On Claude Code versions before 2.1.275, add the marketplace first and then install the plugin:

```
/plugin marketplace add ThatXliner/naming-skill
/plugin install naming-cheatsheet@naming-skill
```

### Any agent (skills CLI)

Install with the [`skills`](https://github.com/vercel-labs/skills) CLI. It supports Claude Code, Codex, Cursor, and other agents:

```sh
npx skills add ThatXliner/naming-skill
```

### Manual

Copy the skill folder into your agent's skills directory. For Claude Code:

```sh
git clone https://github.com/ThatXliner/naming-skill.git
mkdir -p ~/.claude/skills
cp -r naming-skill/skills/naming-cheatsheet ~/.claude/skills/
```

To install it for one project only, copy it to `.claude/skills/` in that project instead.

## Usage

You do not need to call the skill. The agent loads it when a task involves naming. To use it on purpose, ask for it by name, for example:

```
Use the naming-cheatsheet skill to review the names in src/cart.ts
```

In Claude Code, you can also run the skill as a slash command: `/naming-cheatsheet:naming-cheatsheet` if you installed the plugin, or `/naming-cheatsheet` if you copied the folder by hand.

## Repository layout

```
.claude-plugin/
  plugin.json          Claude Code plugin manifest
  marketplace.json     Lets this repo act as a plugin marketplace
skills/naming-cheatsheet/
  SKILL.md             The rules the agent reads
  references/
    cheatsheet.md      The full cheatsheet with all examples
```

To read the cheatsheet itself, see [`skills/naming-cheatsheet/references/cheatsheet.md`](skills/naming-cheatsheet/references/cheatsheet.md).

## Credits

The content comes from [naming-cheatsheet](https://github.com/kettanaito/naming-cheatsheet) by [Artem Zakharchenko](https://github.com/kettanaito). MIT licensed. See [LICENSE.md](LICENSE.md).
