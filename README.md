# cgpt-clip

A Clippy-inspired animated companion for Codex, created with hatch-pet and imagegen.

![Clippy reference](source/references/canonical-base.png)

**Status:** work in progress. The character reference and build tools are available; animation generation and validation are ongoing. There is no installable pet package yet.

## What's here

- `source/references/`: canonical character image and animation layout guides.
- `source/prompts/`: exact image-generation prompts for the character, animation strips, and gaze directions.
- `source/pet_request.json`: character and atlas specification.
- `tools/`: deterministic Python tools from the hatch-pet workflow for extraction, assembly, previews, and validation.

The target is a Codex v2 atlas: 1536 × 2288 pixels, 8 × 11 cells, nine animation states and sixteen gaze directions. Each cell is 192 × 208 pixels.

## Working with the tools

Requires Python 3.10+ and Pillow:

```sh
python3 -m venv .venv
. .venv/bin/activate
pip install -r requirements.txt
python tools/prepare_pet_run.py --help
python tools/validate_atlas.py --help
```

Image generation is a separate step using the included prompts and reference images. These tools do not call an image API or generate missing artwork. Every animation strip needs its own generated, visually reviewed source before assembly. Look rows must preserve the clockwise direction sequence and pass independent visual review.

To validate a completed atlas:

```sh
python tools/validate_atlas.py path/to/spritesheet.webp --chroma-key '#FF00FF' --require-v2 --json-out validation.json
```

The finished package will contain `pet.json` with `spriteVersionNumber: 2` and `spritesheet.webp`, together with visual previews and QA reports.

## Credits

Character concept: Clippy, Microsoft's paperclip assistant. This is an unofficial fan project. Artwork generated with OpenAI imagegen; build and QA utilities supplied by the hatch-pet skill.
