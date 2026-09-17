# DiscordPresence App Database

Curated application identity database used by [DiscordPresence](https://github.com/the-real-l1near/DiscordPresence).

The database maps desktop applications to stable IDs, categories, executable matching rules, and Discord presence artwork.

Accuracy is more important than coverage. An unknown application is preferable to a false positive.

## Repository layout

```text
apps/
  development/
  creative/
assets/
schema/
CATEGORY_POLICY.md
MATCHING_POLICY.md
ASSET_GUIDELINES.md
CONTRIBUTING.md
database.json
```

- `apps/` contains the source application records. Each application has one JSON file named after its stable `id`.
- `assets/` contains the corresponding presence artwork as `<id>.png`.
- `schema/` contains the JSON Schemas for individual app records and the generated database.
- `database.json` is the generated database consumed by DiscordPresence. Do not treat it as the authoring source.

## Application record

Example:

```json
{
  "id": "visual-studio-code",
  "name": "Visual Studio Code",
  "category": "development",
  "subcategory": "code-editor",
  "match": [
    {
      "processName": "Code",
      "productName": "Visual Studio Code"
    }
  ],
  "presence": {
    "largeImage": "https://raw.githubusercontent.com/the-real-l1near/DiscordPresence-AppDatabase/main/assets/visual-studio-code.png"
  }
}
```

### `id`

Stable lowercase kebab-case identifier. It is also used for the source filename and artwork filename.

Changing an existing ID should be treated as a breaking data migration rather than a cosmetic rename.

### `name`

Human-readable product name shown by DiscordPresence.

### `category` and `subcategory`

The current primary categories are:

- `development`
- `creative`

See [CATEGORY_POLICY.md](CATEGORY_POLICY.md) for the supported subcategories and classification rules.

### `match`

An array of alternative matching rules.

Rules are ORed together. Constraints inside one rule are ANDed together.

For example:

```json
"match": [
  {
    "processName": "ExampleApp",
    "productName": "Example App"
  },
  {
    "processName": "ExampleAppBeta",
    "productName": "Example App"
  }
]
```

Either rule may identify the app, but every field present inside the selected rule must match.

`processName` is required and must not include `.exe`.

`productName` and `originalFilename` are optional Windows executable VersionInfo fields and should only be added when verified.

See [MATCHING_POLICY.md](MATCHING_POLICY.md) before adding or changing identity rules.

### `presence.largeImage`

HTTPS URL used as the Discord activity large image.

For repository-hosted artwork, use the raw GitHub URL for `assets/<id>.png`.

See [ASSET_GUIDELINES.md](ASSET_GUIDELINES.md).

## Versions

`database.json` contains two independent versions:

- `schemaVersion` changes when the structure or interpretation of the database changes in a way that clients must understand.
- `databaseVersion` is a monotonically increasing content revision and changes when published database content changes.

Adding an app, changing a match rule, changing presence metadata, or replacing a published asset should advance `databaseVersion`.

A normal content update does not require changing `schemaVersion`.

## Generated database

`database.json` is built from the curated source records under `apps/` and is the file fetched by DiscordPresence at runtime.

Source records are the maintainable source of truth. Keep generated output synchronized with them.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) before proposing application records or artwork changes.

The short version is:

1. Verify the application identity from reliable evidence.
2. Choose the category using the category policy.
3. Add or update the source record under `apps/<category>/`.
4. Add a matching `<id>.png` asset when required.
5. Validate the record against the schema.
6. Regenerate `database.json` and advance `databaseVersion` once for the published change set.

Do not guess executable metadata to increase coverage.

## License and trademarks

Application names, product names, logos, and trademarks belong to their respective owners. Their presence in this repository is for application identification and Discord presence display and does not imply affiliation or endorsement.
