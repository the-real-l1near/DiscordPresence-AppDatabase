# Asset Guidelines

Presence artwork lives under `assets/` and is referenced by application records through `presence.largeImage`.

The goal is consistent, recognizable artwork that remains readable at Discord activity-card sizes.

## Filename

Each application asset must use the application's stable ID:

```text
assets/<id>.png
```

Examples:

```text
assets/blender.png
assets/visual-studio-code.png
assets/obs-studio.png
```

The filename must stay aligned with the source application record ID.

## Format

Use PNG.

Recommended source dimensions are:

- 512 × 512
- 1024 × 1024

Use a square canvas.

Transparency is preferred when it suits the logo or artwork.

Do not add unnecessary backgrounds solely to fill the square canvas.

## Safe space

Leave enough transparent or neutral space around the visible mark so Discord does not make the artwork feel cramped or clipped.

Do not scale a logo until it touches the image edges.

The exact amount of safe space depends on the shape of the mark; visual consistency matters more than a fixed percentage.

## Artwork selection

Prefer official product artwork or a faithful presentation of the product's current recognizable icon.

Avoid:

- screenshots;
- unrelated illustrations;
- text-heavy banners;
- low-resolution upscales;
- visibly compressed images;
- watermarked images;
- assets whose branding belongs to a different product or edition.

Do not modify a logo in a way that changes its identity.

## Backgrounds

Transparent backgrounds are generally preferred for logos designed to stand on their own.

A background is acceptable when it is an intentional part of the product's official icon or necessary for legibility.

Avoid arbitrary gradients, drop shadows, borders, or decorative framing that are not part of the product identity.

## Presence URL

Repository-hosted assets should be referenced through the raw GitHub URL:

```text
https://raw.githubusercontent.com/the-real-l1near/DiscordPresence-AppDatabase/main/assets/<id>.png
```

Example:

```json
"presence": {
  "largeImage": "https://raw.githubusercontent.com/the-real-l1near/DiscordPresence-AppDatabase/main/assets/blender.png"
}
```

Use HTTPS only.

## Replacing an existing asset

An asset replacement is a published database content change even when the application JSON record itself does not change.

When replacing artwork:

1. keep the same `<id>.png` filename unless the application ID itself changes;
2. verify that the new file is a valid PNG;
3. confirm that the product identity is still correct;
4. increment `databaseVersion` once for the published change set;
5. regenerate or republish the database as required by the maintainer workflow.

## Trademarks

Application logos and trademarks remain the property of their respective owners.

Assets in this repository are used for application identification and Discord presence display. Their inclusion does not imply affiliation, sponsorship, or endorsement.
