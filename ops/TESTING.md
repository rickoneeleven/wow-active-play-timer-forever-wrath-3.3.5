# Testing

DATETIME of last agent review: 16 Aug 2026 15:51 (Europe/London)

## Purpose

The Lua behavioural harness simulates the World of Warcraft API and exercises the addon's public event and UI behavior.

## Fast Path

- `npx --yes --package=fengari-node-cli fengari tests/test.lua` - run the complete addon behavioural suite from the repository root
- `lua -e 'unpack=table.unpack or unpack; dofile("tests/test.lua")'` - run locally when Lua is installed

- `lua -e 'unpack=table.unpack or unpack; arg={[1]="forever"}; dofile("tests/test.lua")'` - Forever API simulation, modern backdrops, public movement query, loading and stall exclusions
- `luac -p 111timer.lua` - syntax check

## Area Overrides

- `111timer.lua` -> `npx --yes --package=fengari-node-cli fengari tests/test.lua` - verify timer state, activity detection, combat behavior, UI controls, and saved settings
- `111timer.toc` -> inspect the file in a WoW Forever or World of Warcraft 3.3.5a addon installation - verify client metadata and load order; no automated client integration exists

## Key Test Locations

- `tests/test.lua` - WoW API simulation and behavioural assertions

## Known Gaps

- The harness does not render frames or execute inside the World of Warcraft client.

## Agent Testing Protocol

**MANDATORY:** Run relevant tests after every new feature or behavior change; fix failures immediately.
