# Pokémon Showdown — DigiPen Client Resources

Custom sprites and icons served from this repository. All image files must be PNG (`.png`). Audio and FX are currently unimplemented.

---

## Pokémon sprites & icons

| Asset | Size | File naming |
|-------|------|-------------|
| Sprites | 96×96 px | Species ID; use a hyphen between name and forme (e.g. `gardevoir-mega.png, sandslash-alola.png`) |
| Icons | 40×30 px | Same as sprites |

**Server (`pokemon-showdown`):** In `data/mods/gen9digipen/pokedex.ts`, set both flags on the species entry:

- `digipenSprite: true`
- `digipenIcon: true`

---

## Item icons

| Asset | Size | File naming |
|-------|------|-------------|
| Icons | 24×24 px | Same as the item ID (e.g. `choiceband` → `sprites/itemicons/choiceband.png`) |

**Server:** In `data/mods/gen9digipen/items.ts`, set `isNonstandard: "DigiPen"` on the item.

---

## Trainer sprites (avatars)

Trainer sprites are **80×80 px**.

### Public avatars (everyone — avatar picker)

Use for sprites that should appear in the avatar popup for all users.

1. **Add the image**  
   `sprites/trainers/<spritename>.png`

2. **Register in the client** — `pokemon-showdown-client/play.pokemonshowdown.com/src/battle-dex-data.ts`  
   In the DigiPen section of `BattleAvatarNumbers`, add the next free index:

    ```ts
    296: '$spritename',
    ```

   The `$` prefix tells the client to load from `sprites/trainers/` in this repo.

3. **Extend the avatar picker loop** - `pokemon-showdown-client/play.pokemonshowdown.com/js/client-topbar.js`
    Increment the `for` loop end in `AvatarsPopup`.

4. **Register on the server** — `pokemon-showdown/server/chat-commands/avatars.tsx`  
   Add the sprite name **without** `$` to `OFFICIAL_AVATARS_DIGIPEN`:

    ```ts
    const OFFICIAL_AVATARS_DIGIPEN = new Set([
    	'spritename',
    ]);
    ```

Users can select the avatar in the picker or use `/avatar spritename` in a Pokemon Showdown chat.

---

### Private avatars (per-user)

Use for personal sprites that only specific Showdown accounts may use.

1. **Add the image**  
   `sprites/trainers-custom/<spritename>.png`

2. **Whitelist your showdown username to use the avatar in the server** — `pokemon-showdown/config/avatars.json`:

    ```json
    {
    	"yourshowdownusername": {
    		"allowed": ["#spritename"]
    	}
    }
    ```

   Or if you have admin privileges, use `/groupavatar yourshowdownusername, #spritename` in a Showdown chat.

3. **Set in-game**  
   Use `/avatar #spritename` in a Showdown chat.

---
