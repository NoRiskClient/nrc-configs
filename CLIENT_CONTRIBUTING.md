# Contributing to NoRisk Modpacks

This guide explains how to set up your own development branch and pack for contributing to NoRisk Client.

## Quick Start

### 1. Create Your Branch (nrc-core)

Fork/branch from the main development branch:
```
https://github.com/NoRiskClient/nrc-core/tree/dev/mojang-mappings
```

**Important:** Your branch name becomes part of the JAR filename!

Example:
- Branch: `dev/mojang-mappings`
- JAR: `nrc-core-1.0.151-dev-mojang-mappings+fabric.1.21.11`

### 2. Create Your Pack (nrc-configs)

1. Go to [nrc-configs/packs](https://github.com/NoRiskClient/nrc-configs/tree/main/packs)
2. Copy `norisk-bughunter.json` as a template
3. Rename it to your pack name (e.g., `my-feature-pack.json`)
4. Create a Pull Request

### 3. Configure Your Mod Version

In your new pack JSON, find the mod you're working on and update its version:

```json
{
  "id": "nrc-core",
  "displayName": "nrc-core",
  "source": {
    "type": "maven",
    "repositoryRef": "noriskproduction",
    "groupId": "gg.norisk",
    "artifactId": "nrc-core"
  },
  "compatibility": {
    "1.21.11": {
      "fabric": {
        "identifier": "1.0.151-YOUR-BRANCH-NAME+fabric.1.21.11",
        "filename": null,
        "source": null
      }
    }
  }
}
```

**Note:** You only need to do this once! After the initial setup, auto-update will handle new versions.

### 4. Wait for Approval

Your PR needs approval from a NoRisk maintainer (one-time setup).

### 5. Test in Launcher

1. Open NoRisk Launcher
2. Create a new profile
3. Click "Show all versions" checkbox
4. Select your pack from the dropdown
5. Launch and test!

## Development Workflow

Once your pack is set up, the workflow becomes:

```
Code changes → Version bump → Push → CI builds → Discord approval → Auto-deployed
```

1. Make your code changes in nrc-core
2. Bump version in `gradle.properties`
3. Push to your branch
4. Woodpecker CI builds all versions automatically
5. Approve in Discord when prompted
6. Your pack auto-updates with the new version!

## Pack Structure

```json
{
  "displayName": "My Pack Name",
  "description": "Description of your pack",
  "inheritsFrom": null,
  "mods": [...],
  "isExperimental": true,
  "autoUpdate": true
}
```

| Field | Description |
|-------|-------------|
| `displayName` | Shown in launcher dropdown |
| `description` | Pack description |
| `inheritsFrom` | Inherit mods from another pack (e.g., `["norisk-prod"]`) |
| `excludeMods` | Mods to exclude from inherited pack |
| `isExperimental` | Mark as experimental (shows warning) |
| `autoUpdate` | Enable auto-update for maven mods |

## Version Format

NoRisk uses semantic versioning with branch info:

```
1.0.151-dev-mojang-mappings+fabric.1.21.11
│ │ │   │                   │      │
│ │ │   │                   │      └── Minecraft version
│ │ │   │                   └── Loader (fabric/forge)
│ │ │   └── Branch/prerelease identifier
│ │ └── Patch
│ └── Minor
└── Major
```

## Questions?

- Discord: [NoRisk Discord](https://discord.gg/norisk)
- Issues: [nrc-configs Issues](https://github.com/NoRiskClient/nrc-configs/issues)
