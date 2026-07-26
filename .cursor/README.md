# Cursor configuration

These rules define coding and agent guidance for Extended-UniVRM. UniVRM's existing code,
package layout, public API compatibility, and serialization requirements take precedence
over generic style guidance.

## Canonical shared kit (VRMXT Unity)

This repo is the **canonical source** for shared Unity Cursor rules/skills used by sibling
VRMXT Unity projects (Warudo Plugin, UniVRMXT, VRMXT Unity Player).

| Path | Role |
|------|------|
| `.cursor/shared-manifest.json` | Shared rule/skill names + consumer sibling paths |
| `scripts/sync-vrmxt-cursor-shared.ps1` | Copy (or hard-link) shared files into consumers |

```powershell
# From Extended-UniVRM root — dry-run (default)
./scripts/sync-vrmxt-cursor-shared.ps1

# Apply copies into all listed consumers
./scripts/sync-vrmxt-cursor-shared.ps1 -Apply

# Same-volume hard links (local multi-repo only; clones still need copies)
./scripts/sync-vrmxt-cursor-shared.ps1 -Apply -HardLink
```

After editing a shared rule or `validate-unity-meta`, re-run with `-Apply` and commit the
updated copies in each consumer repo (hard links do not survive separate clones).

### Shared (synced)

- `unity-csharp-style.mdc`
- `unity-assets-and-meta.mdc`
- `unity-runtime-safety.mdc`
- `generated-and-submodules.mdc`
- `handoff-and-git.mdc`
- `unity-tests.mdc`
- `unity-ui-toolkit.mdc`
- skill `validate-unity-meta`

### Local only (never synced)

- `unity-csharp-language.mdc` — Unity **pin** (`2022.3` here)
- `univrm-repository.mdc` — host layout / fork packages
- `fork-upstream-safety.mdc` — upstream UniVRM safety

## Project assumptions

- Unity version: `2022.3.62f2`
- Authored packages: `Packages/UniGLTF`, `Packages/VRM`, and `Packages/VRM10`
- Main namespace families: `UniGLTF`, `VRM`, `UniVRM10`, `MToon`, and `VrmLib`
- Tests are package-local NUnit EditMode assemblies.
- C# and documentation use LF line endings.
- Recursive git submodules are part of the repository.

## Deliberately not copied

- Unrelated game namespaces, assemblies, issue links, and folder assumptions
- Game-specific UI architecture, story, backlog, scene, and sandbox policies
- CSharpier/Prettier and editor-agent workflows not installed in this repository
- Repository-wide naming normalization that could break serialized data or public APIs
- GridDungeon UITK / backlog / story Cursor kits
