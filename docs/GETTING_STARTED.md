# Getting Started

This checklist takes a fresh repository from template to first successful build.

## 1. Install Tools

Install Bun 1.3 or newer:

```sh
bun --version
```

Then install dependencies:

```sh
bun install
```

## 2. Rename the Sample Package

Update `datasworn.config.yaml`:

- `repository.url`: your repository URL.
- `packages[0].id`: the Datasworn package ID. This becomes the first path
  element in IDs such as `oracle_rollable:my_package/signals/encounter`.
- `packages[0].source`: the matching source directory.
- `packages[0].packageName`: your npm package name.
- `packages[0].description`: your package description.
- `packages[0].license`: your content license.

Rename `source_data/my_package` to match the new package ID, and update `_id`,
`title`, `url`, `date`, `authors`, and `license` in the YAML files.

Keep package IDs lowercase with underscores, such as `starforged_oracles`.
Use npm package names with hyphens, such as `@your-npm-scope/starforged-oracles`.

## 3. Choose Dependencies

This template demonstrates a Starforged expansion:

```yaml
dependencies:
  - starforged
publishDependencies:
  - id: starforged
    packageName: "@datasworn-community/starforged"
    schemaLine: "0.2"
```

Keep `@datasworn-community/starforged` in `devDependencies` when your source
references Starforged IDs. For Ironsworn Classic content, use
`@datasworn-community/ironsworn-classic` instead and update the dependency ID to
`classic`.

If your package is a standalone ruleset, change `type` to `ruleset`, remove
`ruleset: starforged` from source YAML, and remove the dependency declarations.

## 4. Build and Validate

```sh
bun run build
bun run validate
```

Commit the regenerated `generated-datasworn/` files with your source changes.
Those files are the raw JSON surface for users who browse or download content
directly from GitHub.

The build fails if:

- source YAML is invalid;
- referenced Datasworn IDs cannot be resolved;
- package versions do not match the configured schema line;
- required package metadata, such as `repository`, is missing.

## 5. Prepare to Publish

When the package is ready:

1. Remove `private: true` from the package entry in `datasworn.config.yaml`.
2. Confirm `packageName` is the package you own.
3. Confirm `repository.url` points at this repository.
4. Confirm your license and provenance docs are accurate.
5. Read [Publishing](PUBLISHING.md).
