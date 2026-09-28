# AGENTS.md — layer-charly-immich

Standalone candy repo for the `charly-immich` concept candy — it ships no
install content and owns the `immich` family of `skill:` entities whose names
have no namesake candy. The entities live in `charly.yml` at the repo root;
`candy/plugin-marketplace` regenerates the standalone opencharly/marketplace
corpus from them.

Canonical files:

- `charly.yml` — the `charly-immich:` concept candy entity plus two `skill:`
  entities: `immich-layer-skill` (`name: immich-layer`) and
  `immich-ml-layer-skill` (`name: immich-ml-layer`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-immich:immich-layer` — the owning skill for the Immich server candy
  (port 2283, PostgreSQL/Redis, the pnpm build, the db-init service). Load
  before editing the `immich-layer-skill:` entity.
- `/charly-immich:immich-ml-layer` — the Immich machine-learning backend candy
  (port 3003, model caches). Load before editing the `immich-ml-layer-skill:`
  entity.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro package arms, service
  declarations). Load before editing any entity field or plan step.

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate.
- The candy is documentation-only: its `plan:` is a `true` no-op plus a `true`
  `check:` that the skill entities are present and generated into the
  marketplace. There is no live bed.

## Modify this repo

- The `skill:` entities are the projected usage source. Edit them here, never
  the generated `SKILL.md` in the marketplace corpus; a corpus regeneration
  (`charly marketplace generate`) projects them.
- Two `immich`-family skills (`immich`, `immich-ml`) are owned by sibling repos
  (`pod-immich`, `pod-immich-ml`) — edit those in their own repos, not here.
- When the Immich candy's behaviour changes (version, port, volumes, build
  steps), update the matching `skill:` entity in the same change so the corpus
  does not drift.
- Keep the concept candy's `plan:` no-op; it exists only to carry the entities.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
