# 111 Timer

DATETIME of last agent review: 16 Aug 2026 15:51 (Europe/London)

`111 Timer` is a task-reminder addon for WoW Forever and World of Warcraft 3.3.5a that counts active play instead of ordinary clock time.

## Stack

- WoW Forever (`Interface: 16001`) and Wrath 3.3.5a (`Interface: 30300`)
- Modern backdrop templates and player movement detection on Forever
- Lua 5.1-compatible addon code
- Node.js with `npx` and Fengari for the development test harness

## Quick Start

Install this repository as a folder named `111timer` inside:

```text
World of Warcraft/Interface/AddOns/111timer
```

Restart World of Warcraft after first installation. For updates to an already discovered addon, run `/reload`. Left-click the countdown to choose a new duration immediately, without waiting for expiry. Drag it to move; right-click or use `/111timer` to open settings.

## Use

- The countdown is displayed at 70% scale.
- Loading screens and frame stalls longer than one second do not consume play time.
- The countdown runs only while the character is moving or in combat and pauses as soon as both stop.
- White text means the timer is running, grey means it is idle, and orange means a reminder is due.
- Drag the countdown or reminder to reposition it.
- Choose one of the three reminder durations when the **Check tasks** window appears.
- Configure the three durations, login default, countdown visibility, and window positions in settings.

Settings and window positions are account-wide through `OneElevenTimerDB`. Timer progress is session-only: login, character changes, and `/reload` start a fresh default timer. Reminders due during combat appear when combat ends.

## Development

Run the behavioural harness from the repository root:

```sh
npx --yes --package=fengari-node-cli fengari tests/test.lua
```

Also run the Forever simulation with native Lua:

```sh
lua -e 'unpack=table.unpack or unpack; arg={[1]="forever"}; dofile("tests/test.lua")'
```

The harness simulates the WoW API and verifies login reset, immediate idle pausing, movement, combat queuing, reminder buttons, and settings persistence.

## Licence

MIT; see `LICENSE`.

## Agent Docs

- Runtime map: `ops/manifest.yaml`
- Testing map: `ops/TESTING.md`
- Agent-skill routing: `docs/agents/domain.md`
- Security review: `ops/SECURITY_REVIEW.md`

## Forever installation

On this Mac the live copy is `/Applications/World of Warcraft/_forever_/Interface/AddOns/111timer`. Deploy `111timer.lua` and `111timer_Forever.toc` from this repository there, renaming the latter to `111timer.toc`. The ordinary `111timer.toc` stays on interface 30300 for the original Wrath client. Settings are separate in each client; no other client configuration needs copying.

Compatibility was checked against the installed 1.60.1.70790 client metadata and Blizzard UI source on the Gethe `forever` branch. The modern simulation requires `BackdropTemplate` and rejects `GetUnitSpeed` use, whose results can be secret; Forever uses `IsPlayerMoving` instead. In-game rendering still needs acceptance in the actual client.
