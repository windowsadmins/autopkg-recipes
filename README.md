# Cimian AutoPkg Recipes

These are [AutoPkg](https://github.com/autopkg/autopkg) recipes that download the
latest Windows installers for popular software and import them into a
[Cimian](https://github.com/windowsadmins/cimian) repo.

Recipes use the YAML-native `.cimian.recipe.yaml` format and the
`CimianInfoCreator` / `CimianImporter` processors from the
[Cimian fork of AutoPkg](https://github.com/rodchristiansen/autopkg/tree/add-cimian-support).

## Installation

```pwsh
autopkg repo-add https://github.com/windowsadmins/autopkg-recipes.git
```

## Layout

One directory per app. Recipes are named after the app and architecture:

```
Slack/
  Slack-x64.cimian.recipe.yaml      # x86_64 MSIX
  Slack-arm64.cimian.recipe.yaml    # ARM64 MSIX
Chrome/
  Chrome.cimian.recipe.yaml         # universal MSI (x64 + arm64)
```

* Universal packages (one installer for both architectures) have no arch suffix.
* Architecture-specific recipes are explicitly suffixed `-x64` or `-arm64`.

## Catalogs

All recipes import to the `Development` and `Testing` catalogs by default.
Promotion to `Production` is handled by your Cimian repo's promoter.

## Contributing

Issues and pull requests are welcome. New recipes should:

1. Live in their own app directory.
2. Set `Identifier: com.github.autopkg.cimian.<Name>[-arch]`.
3. Provide a `cimian_info_*` set in `CimianInfoCreator` (name, category,
   developer, description, icon name).
4. Use `CimianImporter` with an explicit `cimian_subdirectory` and
   `supported_architectures`.
5. Default to `catalogs: [Development, Testing]` and
   `unattended_install: true`.

## License

Apache License 2.0 — see [LICENSE](LICENSE).
