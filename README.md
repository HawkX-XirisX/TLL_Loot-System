The Last Light Loot System

**Dynamic Loot for Living Scenarios**

> [!IMPORTANT]
> **Work in progress.** Loot balance, prefab coverage and progression can change as development continues. Test the complete mod set on your server before using keyed containers for critical scenario progression.

## Overview

**TLL_LootSystem** is an Arma Reforger addon by **XirisX** for Project Ashfall and custom survival scenarios. Search world containers for supplies, spend tiered keys to unlock valuable loot, mine ore and crystals, and turn harvested timber into planks.

[Arma Reforger Workshop](https://reforger.armaplatform.com/workshop/6A4F61ED4143DA79-TLL_LootSystemWIP) · [Workshop changelog](https://reforger.armaplatform.com/workshop/6A4F61ED4143DA79-TLL_LootSystemWIP/changelog) · [Project Ashfall Discord](https://discord.gg/GH6vQzQ7en)

The mod generates loot from a shared catalog when players search supported world props. Scenario authors can decide which classes and tiers appear in each container, how often it can refresh, and which extra rewards or keys it can drop.

- [Install on a client, server or scenario](#install)
- [Search containers and use keys](#search-containers-and-use-keys)
- [Food and drinks](#food-and-drinks)
- [Mining, woodcutting and crafting](#mining-woodcutting-and-crafting)
- [Configure a scenario](#configure-a-scenario)
- [Compatibility and verification](#compatibility-and-verification)

## Install

- **Players:** Enable **TLL_LootSystem WIP** from the Workshop and join or launch a scenario that uses it.
- **Server owners:** Add the Workshop mod to the existing `game.mods` array in your server config. Keep the scenario and companion addons in that array as well. [Bohemia Interactive server config reference](https://community.bistudio.com/wiki/Arma_Reforger%3AServer_Config)
- **Scenario authors:** Open `addon.gproj` in Enfusion Workbench to browse the source project. Add **TLL_LootSystem** as a dependency in your scenario project and use a game mode derived from `SCR_BaseGameMode` for automatic catalog registration. [Bohemia Interactive Workbench project setup](https://community.bistudio.com/wiki/Arma_Reforger%3AMod_Project_Setup)

```json
{
  "modId": "6A4F61ED4143DA79",
  "name": "TLL_LootSystem WIP"
}
```

The project ID is `TLLLootSystem`. The sole declared project dependency is the base Arma Reforger project (`58D0FB3206B6F859`).

## Search containers and use keys

Use **Search** on supported cupboards, wardrobes, dressers, shelves, lockers, safes, crates and cardboard boxes. The addon overrides supported native prefabs, including 38 additional furniture and storage prefabs covered by the civilian loot update. Derived variants can inherit their base prefab's loot profile. The furniture coverage reference (`Docs/CivilianFurnitureLoot_20261104.md`) lists the added prefabs and their settings.

- Loot uses five tiers and weighted selection. Pools include weapons, magazines, attachments, throwables, clothing, protective gear, backpacks, medical supplies, tools, consumables, keys and valuables.
- Keyed containers require the exact tier of TLL key equipped in your hand. Successful unlocking consumes the key and leaves the container unlocked for subsequent searches. Tier 1–5 key prefabs are in `Prefabs/Props/Keys`.
- A search generates loot on the server. During the cooldown, searches access the existing contents. The first search after cooldown clears the remaining inventory and starts a new loot cycle, so take anything you want to keep.

### Valuables and rare weapons

Loot includes copper, silver and gold coins, precious-metal bars, silver collectibles, goblets and chalices. Selected containers roll separately for precious metals. Each successful roll awards one weighted item from its metal pool. Both rolls can succeed on the same search.

| Container profile | Gold chance | Silver chance |
| --- | ---: | ---: |
| Six selected common furniture and storage profiles | 3% | 5% |
| Tier 3 keyed metal locker | — | 15% |
| Tier 4 keyed safe | 10% | — |
| Tier 5 keyed crate | 15% | — |

The **Golden AK-74** and **Golden M16A2** are Tier 5 assault rifles with gold-and-black finishes and native firing, sights, animations and reloading. The AK-74 uses native 5.45×39 mm magazines. The M16A2 uses 5.56×45 mm STANAG magazines. The AK prefab retains its legacy filename, `TLL_GoldenAK47.et`, for resource compatibility. Weapon implementation notes (`Docs/NativeGoldFinish_20261103.md`)

## Food and drinks

The catalogs contain **190 individually named consumables**, including **155 foods** and **35 drinks**. Food ranges from produce and canned goods to snacks and prepared meals. Equip food and choose **Eat** to start consumption. Equipping it alone leaves it intact.

Drinks use the native Arma Reforger 1.9 drinking interaction and animation. There are **33 single-use drinks** and **two reusable canteens** (US and Soviet). Each canteen holds **1 L**, uses **0.1 L** per successful drink and grants **25 Water** with the matching Metabolism integration. Food, Water and Energy rewards are configurable. Alcohol has no intoxication mechanic. Native drinking notes (`Docs/NativeDrinking_20261106.md`) · Food interaction notes (`Docs/FoodEquipActivation_20261106.md`)

## Mining, woodcutting and crafting

Equip the **Old Pickaxe** or **Fire Axe** in primary weapon slot 1 or 2, select it as your active weapon and use the native melee binding. Harvesting drops resources on the ground beside you. Both tools enter the loot pool as **TOOL / TIER_1**.

| Target | Action | Default reward | Recovery |
| --- | --- | --- | --- |
| Normal Rock | 5 pickaxe strikes | 1 ore. Copper 50%, iron 35%, silver 12%, gold 3%. | 10 minutes |
| Void Touched Rock | 5 pickaxe strikes | 1 Titanium Ore | 10 minutes |
| Crystal Stone Rock | 5 pickaxe strikes | 1 of 4 equally weighted crystals | 10 minutes |
| TLL Harvestable Pine | 8 axe strikes | 2 Logs | Falls, despawns and respawns after 15 minutes |
| Supported native destructible trees | 8 axe strikes | 2 Logs | Native tree lifecycle |
| Old Workbench | Carry 1 Log and choose **Refine one Log into Planks** | 4 Planks after 4 seconds | Repeat with another Log |

The Old Workbench attempts to put planks in your inventory and leaves them on the ground if insertion fails. The server validates harvesting hits and crafting inputs, and stages output before depleting a node or consuming a log.

Place the three rock-node prefabs and `TLL_OldWorkbench.et` from `Assets/Harvesting/Prefabs` in your scenario. Place `TLL_HarvestablePine.et` for a tree with a configurable respawn. Mining requires placed nodes. Native woodcutting applies to supported destructible trees under `Assets/Vegetation/Tree/`.

Edit `TLL_HarvestNodeComponent` to tune valid hits, yield, weighted outputs and respawn delay for placed nodes. A zero delay makes depletion permanent for the mission. See the harvesting setup guide (`HARVESTING_SETUP.md`) for the showcase world, tool behavior and validation details.

## Configure a scenario

### Container profiles

Start from a supported searchable prefab. For a custom prefab, use a working container as a reference for inventory storage, action placement, replication and the `TLL_SearchContainerAction`. Edit its `TLL_LootContainerComponent` in Workbench.

| Setting | What it controls |
| --- | --- |
| Spawn Chance % | Chance to run the normal loot roll |
| Minimum / Maximum Items | Target count for normal loot |
| Allowed Loot Classes / Tiers | Which entries qualify for normal loot |
| Allow Duplicate Items | Whether the same prefab can be selected repeatedly in one normal roll |
| Loot Respawn Time | Cooldown in seconds before a search refreshes the container |
| Is Key Required? / Required Key Tier | Whether unlocking requires a held key, and which tier it must match |
| Forced / Custom Loot Items | Independent chances for fixed prefabs or weighted class picks, optionally restricted to a prefab whitelist |

Forced entries bypass the normal chance, class and tier filters and item count. Use them for progression keys or bonus rewards. The additional civilian profiles generally allow Tiers 1–2 and refresh after 600 seconds. Their normal chances and item limits vary by prefab.

### Loot catalogs

| Catalog | Contents |
| --- | --- |
| Core (`Configs/TLL_LootCatalog.conf`) | Core loot entries |
| Food (`Configs/TLL_FoodCatalog.conf`) | Edible items |
| Drinks (`Configs/TLL_DrinksCatalog.conf`) | Beverages and reusable canteens |
| Valuables (`Configs/TLL_ValuablesCatalog.conf`) | Collectibles, golden rifles and the Construction Bolt |
| Harvesting tools (`Assets/Harvesting/Configs/TLL_HarvestingToolsCatalog.conf`) | Fire Axe and Old Pickaxe |

Each `TLL_LootEntry` specifies a prefab, loot class, tier and relative weight. Higher weight makes an item more likely within its eligible pool.

### Automatic loot discovery

The runtime discovers eligible vanilla items and supported modded weapons, gear and ammunition from the loaded arsenal. Discovery depends on the item's arsenal registration and classification. Use an explicit catalog entry to include a specific prefab or assign a custom tier and weight.

| Discovered loot | Default tier |
| --- | --- |
| Handguns, ammunition and other supported classes without a special rule | 1 |
| Vanilla clothing, vests and rigs, helmets and backpacks | 1 |
| Assault rifles and supported modded clothing, vests and rigs, helmets and backpacks | 2 |
| Sniper rifles | 3 |
| Machine guns | 4 |

Tier 5 rewards, such as the two golden rifles, can be assigned explicitly in a catalog. Discovery tiers describe the defaults for automatically discovered items. The container's class and tier filters still apply.

For an extension addon, create a `TLL_LootCatalog` configuration and call `TLL_LootCatalogRegistry.RegisterCatalog(resourceName)` on the server after the base game-mode initialization has registered the core catalogs. Use the GUID-qualified resource path for your catalog. Registration invalidates the merged-entry cache. Container profiles still determine which entries are eligible. Game-mode bootstrap (`Scripts/Game/TLL_LootSystemGameModeExtension.c`) · Catalog registry (`Scripts/Game/TLL_LootCatalogRegistry.c`)

### Project Ashfall integrations

| Companion addon | Integration |
| --- | --- |
| **TLL_Metabolism** | Applies consumable rewards to hunger, thirst and energy. Use a matching version for native drink completion and rewards. |
| **TLL_BuildingSystem** | Uses harvested planks and loot resources in construction and crafting. The LootSystem supplies Construction Bolt and stone assets. Building recipes and upgrades live in the companion addon. |
| **TLL_Traders** | Supplies trader inventories and prices, including food, drink and valuables listings. |
| **TLL_Persistence** | Handles long-term player inventory and survival state. Updated player inventory snapshots include canteen water, including canteens in nested gear. Building storage and garage cargo use separate serializers. Harvest depletion and respawn jobs are mission state. |

## Compatibility and verification

Local Workbench validation used **Arma Reforger 1.9.0.37**. The recorded runs covered Game and WorkbenchGame compilation, loading all 190 consumable resources, 36 harvesting regression checks, and 79 food and native-drink integration checks, including the 73 native-drink checks. The companion Persistence addon separately passed 24 local checks for player inventory save and restore. Production loot generation, remote-client inventory transfers and dedicated-server reconnect and restart behavior still require validation with the full scenario and addon set.

Compatibility report (`Docs/Compatibility_1_9_20261106.md`) · Local changelog (`CHANGELOG.md`)

## Credits and license

**XirisX** develops TLL_LootSystem for The Last Light and Project Ashfall. Thanks to **FriendlyModder** for inspiring the searchable native prefab overrides and configurable loot chances.

The Workshop release is listed under the **Arma Public License (APL)**. The Rock and Stone assets have separate **CC BY 4.0** credits for **Siesta** and **Xephira**. [Workshop license listing](https://reforger.armaplatform.com/workshop/6A4F61ED4143DA79-TLL_LootSystemWIP) · Asset attribution (`Assets/Building/Economy/ATTRIBUTION.txt`)
Built for scenario makers, by scenario makers.

For any help needed please reach out to sebastian_rus on Discord
