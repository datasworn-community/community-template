# Datasworn Community Content Template

Use this repository as a starting point for a Datasworn content package. It
builds YAML source data into publishable npm package artifacts with
`@datasworn-community/build-tools`.

This template intentionally starts with one private sample package:
`source_data/my_package`. Rename it before publishing.

## Raw JSON

Generated raw Datasworn JSON is committed in `generated-datasworn/` for users
who want to download or browse files directly from GitHub.

Use `generated-datasworn/manifest.json` to see the current generated file,
package name, schema line, license, and dependency metadata for each content
package.

## Quick Start

```sh
bun install
bun run build
bun run validate
```

Generated artifacts are written to:

- `generated-datasworn/my_package.json`
- `datasworn/my_package/my_package.json`
- `dist/packages/my_package/`

The `dist/packages/my_package` directory is the npm package artifact generated
by build-tools. Do not edit generated files by hand; edit `source_data/` and
`datasworn.config.yaml`, then rebuild.

## First Changes

1. Rename `my_package` in `datasworn.config.yaml` and `source_data/my_package`.
2. Change `packageName` to the npm package you plan to publish.
3. Change `repository.url` to your GitHub repository URL.
4. Update title, author, URL, date, and license in your source YAML.
5. Keep `private: true` until you are ready to publish.
6. Run `bun run build` and `bun run validate`.

See [Getting Started](docs/GETTING_STARTED.md) for the full checklist.

## Documentation

- Datasworn core and build-tools:
  <https://github.com/datasworn-community/datasworn>
- Official content examples:
  <https://github.com/datasworn-community/official-content>
- Shared content workflows:
  <https://github.com/datasworn-community/.github>
- Published npm packages:
  <https://www.npmjs.com/org/datasworn-community>

Project-specific notes in this template:

- [Getting Started](docs/GETTING_STARTED.md)
- [Content Authoring](docs/CONTENT_AUTHORING.md)
- [Publishing](docs/PUBLISHING.md)
- [Provenance](PROVENANCE.md)

## Repository Layout

```text
source_data/           Datasworn source YAML you edit
datasworn.config.yaml  Build and package metadata
generated-datasworn/   Generated raw JSON committed for GitHub users
datasworn/             Generated built JSON, ignored by git
dist/packages/         Generated npm package artifacts, ignored by git
.github/workflows/    Build and release workflow callers
```

## How Publishing Works

The shared release workflows compare generated package artifacts against the
latest published version on the same Datasworn schema line. Changed packages are
published; unchanged packages are skipped.

Experimental canaries are enabled by applying the `release_experimental` label
to a pull request. Removing the label stops future publishes. The per-PR
dist-tags remain after the PR closes as convenience aliases; use the exact
canary version from the PR comment for reproducible installs.

Before publishing, read [Publishing](docs/PUBLISHING.md).
