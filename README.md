# Caveman for ChatGPT and Codex

Marketplace wrapper for the [`skills/caveman`](https://github.com/JuliusBrussee/caveman/tree/main/skills/caveman) skill from [`JuliusBrussee/caveman`](https://github.com/JuliusBrussee/caveman).

This repository contains no MCP server, external API, backend, hook, or executable. It packages one instruction-only skill using the current portable Agent Plugins manifest and the ChatGPT/Codex repo marketplace catalog.

## Repository layout

```text
caveman-chatgpt/
├── .agents/
│   └── plugins/
│       └── marketplace.json
├── plugins/
│   └── caveman/
│       ├── plugin.json
│       └── skills/
│           └── caveman/
│               └── SKILL.md
├── LICENSE
└── README.md
```

The marketplace root is the repository root. `.agents/plugins/marketplace.json` points to `./plugins/caveman`. The plugin uses `plugin.json` with Agent Plugins schema `1.0.0`; portable packages discover skills automatically from the plugin-root `skills/` directory.

## Add from Git

In **Plugins → Add marketplace → Git**, enter:

- **Repository:** `https://github.com/<user>/<repo>`
- **Git ref:** `main`
- **Sparse path:** leave empty

Do not enter `/`, `skills/caveman`, or `plugins/caveman`. Sparse path selects the marketplace root. This repository already places the supported marketplace manifest relative to the Git repository root, so no sparse checkout is needed.

CLI equivalent:

```bash
codex plugin marketplace add <user>/<repo> --ref main
```

After import, refresh the Plugins Directory, select **Caveman for ChatGPT and Codex**, then install **Caveman**. Start a new chat if an existing chat does not refresh its available skills.

## Usage

Supported triggers:

- `caveman lite`
- `caveman` (defaults to `full`)
- `caveman full`
- `caveman ultra`
- `stop caveman`
- `caveman off`
- `normal mode`

The skill compresses prose, not technical content. It preserves code, shell commands, CLI options, file paths, URLs, JSON, YAML, SQL, regex, error messages, function names, class names, API names, library names, model names, versions, numbers, units, important conditions, and task order.

## Upstream and changes

- Upstream repository: <https://github.com/JuliusBrussee/caveman>
- Upstream skill path: `skills/caveman/SKILL.md`
- Vendored upstream file blob: `ea8bf271fc89cb783a19c54d9d0b5fdaec48a482`
- Retrieved: 2026-09-13
- Upstream author and copyright: Julius Brussee
- License: MIT for the skill and this wrapper content

Core rules, `lite`/`full`/`ultra` behavior, relevant examples, safety behavior, and boundaries are retained. Wrapper-only changes are limited to:

1. OpenAI/Codex marketplace and portable plugin manifests.
2. Explicit slash-optional trigger wording for `caveman`, `caveman lite`, `caveman full`, `caveman ultra`, and `caveman off`.
3. Upstream wenyan modes removed to keep this wrapper focused on `lite`, `full`, and `ultra`.

The upstream repository also contains proxy, engine, hooks, commands, and other components. They are intentionally excluded because this package is skill-only.

## Specification basis

- [OpenAI: Package your plugin](https://developers.openai.com/plugins/build/plugins)
- [OpenAI: Build skills](https://developers.openai.com/codex/skills)

OpenAI documents `.agents/plugins/marketplace.json` as the repo marketplace catalog, `plugin.json` as the portable plugin manifest, and `skills/<skill-name>/SKILL.md` as the skill location.
