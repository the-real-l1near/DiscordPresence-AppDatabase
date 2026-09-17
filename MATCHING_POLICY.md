# Matching Policy

This document defines how DiscordPresence application records identify running desktop applications.

Matching is intentionally conservative. False positives are worse than leaving an application unknown.

## Match semantics

Each application record contains a `match` array.

Rules in the array are ORed together. Fields inside one rule are ANDed together.

Example:

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

The application matches when either complete rule matches.

A rule that contains `processName`, `productName`, and `originalFilename` requires all three values to match.

## `processName`

`processName` is required for every match rule.

Use the Windows process name without the `.exe` extension.

Examples:

```text
Code
blender
obs64
UnrealEditor
```

Do not put paths, command-line arguments, window titles, or `.exe` extensions in this field.

Process-name matching is case-insensitive in DiscordPresence.

## `productName`

`productName` is optional.

It represents the Windows executable VersionInfo `ProductName` value.

Use it when it materially strengthens identity and the value has been verified from reliable evidence.

Example:

```json
{
  "processName": "Code",
  "productName": "Visual Studio Code"
}
```

Do not derive this value from the marketing name of the product. The executable's actual VersionInfo is authoritative for this field.

## `originalFilename`

`originalFilename` is optional.

It represents the Windows executable VersionInfo `OriginalFilename` value.

Example:

```json
{
  "processName": "GitHubDesktop",
  "productName": "GitHub Desktop",
  "originalFilename": "electron.exe"
}
```

This field is especially useful when a branded process is built on a shared runtime or when another metadata constraint helps distinguish an executable reliably.

Do not assume that `originalFilename` is the same as the current executable filename.

## When to use metadata constraints

A process-only rule is acceptable when the process name is sufficiently distinctive and well verified.

Add `productName` or `originalFilename` when:

- the process name is generic;
- multiple unrelated applications may use the same process name;
- the application uses a shared runtime;
- the extra metadata has been verified and materially reduces false positives.

Do not add optional metadata merely because fields exist in the schema.

An incorrect metadata constraint can create false negatives, so every constraint must be evidence-backed.

## Multiple executables

Use multiple match rules when one product legitimately has multiple supported executable identities.

For example, different release channels or platform variants may use different process names.

Do not combine separate applications into one record simply because they share branding or a vendor.

Each rule should independently identify the same logical product represented by the record ID.

## Generic executable names

Names such as `Editor`, `App`, `Launcher`, `main`, or similarly generic processes are not strong enough on their own.

For these cases, require verified metadata constraints or leave the application unsupported until a reliable rule is available.

Unknown is better than incorrect.

## Window titles are not identity metadata

Do not use window titles as database identity rules.

Window titles are dynamic, localized, document-dependent, and frequently changed by applications. They are suitable for runtime context such as project or document detection, not for stable app identity in this database.

## Evidence

Preferred sources include:

- executable VersionInfo from a legitimate installation;
- official vendor repositories;
- official package or installer metadata;
- official documentation that explicitly names the executable;
- first-party support material.

If a source only confirms the product name but not the executable metadata, it does not justify filling `productName` or `originalFilename` by inference.

## Collision handling

Before publishing a new rule, compare it against existing records.

If two different application records can satisfy the same complete rule, the ambiguity must be resolved before publishing.

Do not rely on record order to resolve collisions.

## Runtime behavior

DiscordPresence treats metadata constraints as required when they are present in a rule.

If required executable metadata cannot be read or does not match, that rule does not match.

This fail-closed behavior is intentional and supports the database goal of preferring unknown applications over false positives.

## Changing an existing rule

Treat match-rule changes as behavior changes, not cosmetic edits.

Before broadening a rule, verify that the broader identity remains unique.

When fixing a false positive, prefer narrowing or correcting the rule even if that temporarily reduces coverage.
