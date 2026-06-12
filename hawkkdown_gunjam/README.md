# Hawkk Gun Jam

An immersion weapon wear script that adds a chance for weapons to jam during firing, requiring manual clearing QTEs.

## Dependencies
- `es_extended`
- `ox_lib`

## Features
- Calculates weapon jam chances per bullet shot, scaling with weapon class
- Jams disable shooting immediately, forcing the player to run or cover
- Clearing weapon jams requires completing a skillcheck minigame
- Includes realistic inspect and unjam animations
- Styled dark card notifications warning the shooter

## Commands
- **/unjam**: Manually triggers the QTE sequence to clear your weapon jam

## Configuration Sample
```lua
Config.JamChance = {
    enabled = true,
    baseChance = 0.3,
    perShotIncrease = 0.05
}
```

## Installation
1. Ensure all dependencies listed above are started in your `server.cfg`.
2. Copy this folder into your resources directory under `[Hawkk]`.
3. Add `ensure hawkkdown_gunjam` to your `server.cfg`.
