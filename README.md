# charly-immich

The `charly-immich` family — the Immich photo-management image skills.

The `charly-immich` candy is a **concept candy**: it ships no install content
and owns the `immich` family of `skill:` entities whose names have no namesake
candy. It currently carries two entities:

- `immich-layer` — the Immich server candy (self-hosted photo management on
  port 2283, with PostgreSQL, Redis, and FFmpeg).
- `immich-ml-layer` — the Immich machine-learning backend candy (face
  recognition and CLIP search on port 3003).

Two further `immich`-family skills are owned by sibling repos: `immich` in
`opencharly/pod-immich` and `immich-ml` in `opencharly/pod-immich-ml`.
`candy/plugin-marketplace` regenerates the standalone
[opencharly/marketplace](https://github.com/opencharly/marketplace) corpus from
these entities, so the skills are authored here and projected there.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `charly-immich` (concept candy) |
| Install content | none — a `true` no-op `plan:` |
| Owns | 2 `skill:` entities: `immich-layer`, `immich-ml-layer` |
| Projected to | `marketplace/immich/skills/` |
| Service / port | none |

## How to use it

This repo is consumed as a **skill source**, not as an image layer. Edit the
`skill:` entities in `charly.yml`; the marketplace regeneration projects them
into `/charly-immich:*` pages. To reference the repo directly, compose it in a
box. A box is a `candy:` node that carries the box's `base:` image and a nested
`candy:` list of layer refs (the nested `candy:` is the composition list; the
outer `candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    base: fedora          # the box's base image
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-charly-immich:v2026.243.2103'
```

The Immich service itself is deployed through the `immich` box, which composes
the `immich` candy from `opencharly/pod-immich`; the `immich-layer` skill here
documents that candy's behaviour.

## Layout

- `charly.yml` — the `charly-immich:` concept candy entity plus two `skill:`
  entities (`immich-layer`, `immich-ml-layer`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-immich:immich-layer`
- ML backend: `/charly-immich:immich-ml-layer`
- Authoring reference: `/charly-image:layer`
- Immich box: `/charly-immich:immich` (in `opencharly/pod-immich`)
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
