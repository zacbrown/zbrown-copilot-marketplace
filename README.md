# zbrown-copilot-marketplace

A GitHub Copilot CLI plugin marketplace for custom skills and curated plugins.
The catalog lives in [`.github/plugin/marketplace.json`](.github/plugin/marketplace.json).

## Getting started

With [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli) installed and authenticated:

```sh
copilot plugin marketplace add zacbrown/zbrown-copilot-marketplace
copilot plugin marketplace browse zbrown-copilot-marketplace
copilot plugin install advanced-security@zbrown-copilot-marketplace
copilot plugin install workiq@zbrown-copilot-marketplace
copilot plugin list
```

Install only the plugins you need. For a local checkout, register the repository
directory instead: `copilot plugin marketplace add /absolute/path/to/zbrown-copilot-marketplace`.

## Example entries

These entries reference real, externally maintained plugins rather than placeholder packages:

| Plugin | Purpose | Upstream documentation |
| --- | --- | --- |
| `advanced-security` | GitHub Advanced Security workflows, including dependency and secret scanning | [github/copilot-advanced-security-plugin](https://github.com/github/copilot-advanced-security-plugin) |
| `workiq` | Microsoft 365 workflows for email, meetings, documents, and Teams | [microsoft/work-iq](https://github.com/microsoft/work-iq) |

Review each upstream project's prerequisites, authentication, permissions, and
license before installing. These plugins may access sensitive data or perform
write operations. Sources are not pinned; installs follow the upstream default
branch.

## Adding entries

Add an object to the catalog's `plugins` array with a unique `name`, a
`description`, and a `source`. The catalog name is used in `name@marketplace`
install commands.
For a GitHub-hosted plugin, use:

```json
{
  "name": "my-plugin",
  "description": "What the plugin does.",
  "source": {
    "source": "github",
    "repo": "owner/repository",
    "path": "plugins/my-plugin"
  }
}
```

Omit `path` when the plugin is at the upstream repository root. For a plugin
hosted in this repository, use `"source": "./plugins/my-plugin"` and include
the plugin directory and its `plugin.json` manifest. Relative sources resolve
from the repository root, not from the catalog directory.

See GitHub's [marketplace guide](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-marketplace)
and [plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference)
for supported fields and plugin components. Refresh the catalog after changes:

```sh
copilot plugin marketplace update zbrown-copilot-marketplace
```

## License

This marketplace is [MIT licensed](LICENSE). Referenced plugins retain their
own licenses.
