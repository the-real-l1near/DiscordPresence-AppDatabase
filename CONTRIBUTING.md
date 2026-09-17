# Contributing

DiscordPresence-AppDatabase is curated for reliable application identification.

The guiding rule is simple: accuracy is more important than coverage. If the evidence is not strong enough, leave the application unsupported until it can be verified.

## Before adding an application

Confirm all of the following:

- the product is within the current database scope;
- the product's primary category and subcategory are supported;
- the executable identity is verified rather than guessed;
- the proposed match rule does not obviously collide with another application;
- a suitable presence asset is available when adding a new record.

Read these policies first:

- [CATEGORY_POLICY.md](CATEGORY_POLICY.md)
- [MATCHING_POLICY.md](MATCHING_POLICY.md)
- [ASSET_GUIDELINES.md](ASSET_GUIDELINES.md)

## Source record location

Create one source file per application:

```text
apps/<category>/<id>.json
```

Examples:

```text
apps/development/visual-studio-code.json
apps/creative/blender.json
```

The filename must match the record's `id`.

## Record format

```json
{
  "id": "example-app",
  "name": "Example App",
  "category": "development",
  "subcategory": "code-editor",
  "match": [
    {
      "processName": "ExampleApp",
      "productName": "Example App",
      "originalFilename": "ExampleApp.exe"
    }
  ],
  "presence": {
    "largeImage": "https://raw.githubusercontent.com/the-real-l1near/DiscordPresence-AppDatabase/main/assets/example-app.png"
  }
}
```

Only include optional metadata that has actually been verified.

## Evidence expectations

Prefer primary or directly inspectable evidence, such as:

- official vendor documentation;
- official source repositories;
- official support documentation;
- installer or package manifests from the vendor;
- executable VersionInfo inspected from a legitimate installation;
- other first-party material that clearly establishes the executable identity.

Community reports can be useful for discovery, but should not be the only basis for ambiguous executable metadata.

Do not infer `productName` or `originalFilename` from the product name, process name, or branding.

## Matching rules

`match` is an array of alternative rules.

- Rules are ORed.
- Fields within a rule are ANDed.
- `processName` is required.
- `processName` must not include `.exe`.
- `productName` and `originalFilename` are optional identity constraints from Windows executable VersionInfo.

If a generic process name can collide with unrelated software, strengthen the rule with verified metadata or do not add it yet.

See [MATCHING_POLICY.md](MATCHING_POLICY.md) for details.

## Categories

Use only categories and subcategories permitted by the schema.

Do not invent a new subcategory in an application record. Taxonomy changes should be discussed and applied deliberately to the schema and policy together.

See [CATEGORY_POLICY.md](CATEGORY_POLICY.md).

## Assets

New applications should have:

```text
assets/<id>.png
```

The asset ID must match the application record ID.

See [ASSET_GUIDELINES.md](ASSET_GUIDELINES.md) for image requirements and presentation guidance.

## Database generation and versioning

`database.json` is generated output. Source records under `apps/` are the maintainable authoring source.

For a published content change:

- update the relevant source record(s);
- update artwork if needed;
- regenerate `database.json`;
- increment `databaseVersion` once for the complete change set.

Do not increment `schemaVersion` for ordinary app additions or corrections. It is reserved for structural or semantic database format changes that clients must understand.

Asset-only published changes also require a `databaseVersion` increment so consumers and maintainers have a deterministic content revision.

## Validation checklist

Before publishing a change, verify that:

- every changed source record conforms to `schema/app.schema.json`;
- IDs are unique;
- source filenames match IDs;
- categories and subcategories are valid;
- every match rule has a non-empty `processName`;
- optional metadata is supported by evidence;
- required assets exist and are valid PNG files;
- `presence.largeImage` points to the correct HTTPS asset URL;
- generated `database.json` reflects the source records;
- `databaseVersion` advanced exactly once for the published change set.

## Corrections

Corrections are welcome. A smaller accurate rule is preferable to a broader uncertain rule.

If an existing record is discovered to produce false positives, prioritize fixing or temporarily narrowing that record rather than preserving compatibility with the incorrect match.
