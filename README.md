TLL Loot System

Dynamic Loot for Living Scenarios

[!IMPORTANT]

🚧 BETA / WORK IN PROGRESS

TLL Loot System is currently a BETA version and is actively being developed.

Systems still being expanded

🛠️ Tools

📦 Misc

🍖 Food / Drinks — coverage and balance

🔑 Key spawning and key-required containers are now functional.

Classification, balance, prefab coverage, and progression behavior may still change during development.

Scenario makers should thoroughly test scenarios before relying on beta systems for critical progression.

Overview

TLL Loot System is a configurable dynamic loot framework for Arma Reforger, created for scenario makers who want to transform ordinary world props into searchable loot containers.

Instead of manually creating fixed inventories for every locker, cabinet, crate, desk, refrigerator, or other searchable object, TLL Loot System generates loot dynamically from a shared global loot catalog.

The system supports:

Dynamic loot generation

Automatic vanilla loot discovery

Compatible modded-content discovery

Loot Classes

Tier 1–5 progression

Configurable container loot pools

Configurable spawn chances

Configurable item counts

Loot respawning

Physical Tier 1–5 keys

Locked loot containers

Multiplayer-aware unlocking

Manual catalog overrides

Existing world-prop overrides

The goal is to give scenario makers control over where loot appears, what can appear, how valuable locations are, and how players progress through the world.

The Last Light — Same Ground. New Stories.

Current Development Status

TLL Loot System is currently in BETA.

The core systems are functional and being actively tested.

Currently Functional

Dynamic loot generation

Global loot catalog

Automatic vanilla item discovery

Compatible modded-content discovery

Runtime catalog merging

Manual catalog overrides

Loot Class filtering

Loot Tier filtering

Configurable container spawn chance

Configurable minimum/maximum item count

Configurable loot respawn time

Searchable world containers

Physical Tier 1–5 keys

Key-required containers

Equipped-key detection

Key consumption

Replicated container unlock state

Multiplayer container access

Existing-world-prop prefab overrides

Key spawning and distribution

Key-required vanilla and modded containers

Food and drink spawning in vanilla refrigerators and kitchen furniture

Searchable / lootable vegetable crops

Custom / Forced Loot

[!CAUTION]

🔴 Tier 5 Key Containers

Tier 5 key-required containers are NOT present in the vanilla map/world-prop setup.

Scenario makers who want Tier 5 key-required loot locations must place and configure the modded TLL container included with the addon.

Configure that container with the desired Tier 5 loot pool and Tier 5 key requirement.

Still Work In Progress

Key progression balancing

Tool classification/balance

Misc classification/balance

Food / Drink coverage and balance

Additional searchable world props

Further multiplayer testing

Overall balance

How the Loot System Works

TLL Loot System uses a global runtime loot catalog.

Instead of every container having its own enormous list of weapons and equipment, containers request items from this shared catalog.

When a player searches a TLL loot container, the system can:

Check whether the container requires a key.

Verify that the correct physical key is equipped if the container is locked.

Start a new loot cycle when appropriate.

Apply the container's configured spawn chance.

Load/build the global runtime loot catalog.

Filter items using the container's enabled Loot Classes.

Filter those items again using the container's enabled Loot Tiers.

Select eligible items.

Spawn those items into the container.

Open the container inventory for the player.

This allows hundreds of different containers to use the same underlying loot system while still having completely different loot configurations.

Automatic Loot Discovery

TLL Loot System automatically discovers compatible inventory items and adds them to the runtime loot pool.

This includes supported:

Vanilla weapons

Modded weapons

Magazines

Ammunition

Vests

Rigs

Backpacks

Helmets

Clothing

Attachments

Medical items

Throwables

Tools

Other supported inventory items

This means scenario makers generally do not need to manually register every compatible weapon from every installed weapon addon.

Compatible third-party arsenal content can automatically enter the global loot pool.

Manual Catalog Overrides

Automatic discovery does not prevent manual configuration.

Items can also be manually entered into the TLL Loot Catalog.

When the same prefab exists as both:

an automatically discovered item, and

a manually configured catalog item,

the manual catalog entry takes priority.

This allows special equipment to receive deliberate:

Loot Class

Loot Tier

Weight

Classification

without disabling automatic discovery for everything else.

Loot Classes

Containers can individually enable or disable Loot Classes.

Current classes include:

Loot Class

Purpose

Assault Rifle

Standard rifles and assault rifles

Sniper Rifle

Sniper and precision weapons

Machine Gun

Machine guns

SMG

Submachine guns

Handgun

Pistols and handguns

Ammunition

Magazines and ammunition

Vest / Rig

Vests and load-bearing equipment

Backpack

Backpacks

Helmet

Helmets and supported headgear

Clothing

Clothing

Medical

Medical supplies

Key Item

TLL keys and key-related items

Misc

Miscellaneous inventory items

Attachment

Weapon attachments

Throwable

Grenades, flares, and supported throwables

Tool

Tools and utility equipment

Food / Drink

Food and drink items

[!WARNING]
KEY ITEM, TOOL, MISC, and FOOD / DRINK are still under active development during the beta.

Their final classification, spawning rules, and balance may change.

Loot Tiers

TLL Loot System supports five loot tiers:

Tier

General Purpose

Tier 1

Common / basic equipment

Tier 2

Improved equipment

Tier 3

Advanced / military progression

Tier 4

High-value equipment

Tier 5

Endgame / extremely valuable equipment

A container can permit one tier or multiple tiers.

For example:

Allowed Loot Tiers

Tier 1 ✓
Tier 2 ✓
Tier 3 ✗
Tier 4 ✗
Tier 5 ✗

That container can select eligible Tier 1 and Tier 2 items.

Loot Tier vs Key Tier

These are two completely separate systems.

Loot Tier

Controls:

What can spawn inside the container?

Key Tier

Controls:

What physical key is required to open the container?

For example:

Allowed Loot Tier:
Tier 4

Is Key Required:
Yes

Required Key Tier:
Tier 3

This means:

The container contains Tier 4 loot, but requires a Tier 3 key to access it.

The two values do not need to match.

Physical Tiered Keys

TLL Loot System includes physical Tier 1–5 keys.

Keys are actual inventory items rather than invisible player variables.

Tier

Theme

Color

Tier 1

Civilian / Maintenance

Rusty Brown / Iron #5C4033

Tier 2

First Responder / Medical

Emergency Blue #1A5276

Tier 3

Military Logistics

Olive Drab Green #3B5249

Tier 4

Biohazard / Containment

Hazmat Yellow #D4AC0D

Tier 5

Strategic Command

Crimson / Red #922B21

Tier 1 — Civilian / Maintenance

Rusty Brown / Iron

Basic keys intended for locations such as:

Residential buildings

Garages

Workshops

Tool sheds

Civilian storage

Tier 2 — First Responder / Medical

Emergency Blue

Intended for locations such as:

Medical facilities

Ambulance storage

Police areas

First responder locations

Medical supply rooms

Tier 3 — Military Logistics

Olive Drab Green

Intended for locations such as:

Military checkpoints

Supply areas

Military storage

Logistics facilities

Ammunition storage

Tier 4 — Biohazard / Containment

Hazmat Yellow

Intended for locations such as:

Containment facilities

Quarantine areas

Laboratories

Chemical storage

High-security medical areas

Tier 5 — Strategic Command

Crimson / Red

Intended as the highest progression tier for locations such as:

Strategic bunkers

Armories

Command facilities

Underground installations

Extraction communication areas

Endgame locations

How Key Unlocking Works

Keys must physically be used by the player.

Simply having the correct key somewhere inside the player's inventory is not enough.

For a locked container:

The player obtains the required key.

The player equips the key in their hands.

The container detects the equipped key.

The interaction changes to:

Unlock

The player activates the interaction.

Exactly one matching key is consumed.

The physical container becomes unlocked.

Loot generation/search proceeds normally.

The unlocked state is replicated to other players.

If the player does not have the correct key equipped, the interaction displays the requirement.

Example:

Tier 3 Key Required

Stacked Keys

Keys support stacking.

If a player has:

Tier 3 Key x3

and uses one to unlock a container, the result is:

Tier 3 Key x2

Only one matching key is consumed.

Multiplayer Unlocking

Container unlocking is tied to the physical container rather than individual players.

If Player A unlocks a Tier 3 container:

Player A
    ↓
Uses Tier 3 Key
    ↓
Container Unlocks
    ↓
One Key Consumed

Player B can then access that same unlocked container without spending another key.

The unlock state is replicated for multiplayer.

This describes the container's replicated runtime/session state. Long-term persistence across server restarts depends on the scenario/persistence environment and should not be assumed unless separately configured and tested.

Normal Containers

Keys are completely optional.

If:

Is Key Required = OFF

the container behaves as a normal TLL searchable loot container.

The value selected under:

Required Key Tier

is ignored.

Normal containers display:

Search

Loot Respawning

TLL containers support configurable loot respawn timing.

When the configured respawn period has elapsed and a new loot cycle begins, the system can clear the previous generated contents and generate a new selection.

This allows searchable locations to become useful again during longer-running scenarios.

Scenario makers should choose respawn values appropriate for:

Scenario length

Server population

Loot scarcity

Progression speed

Location importance

Scenario Maker Configuration Guide

TLL Loot System is designed so that scenario makers can customize containers primarily through Component Properties.

You should normally not need to edit the core TLL scripts just to rebalance a container.

Most container configuration is performed through:

TLL_LootContainerComponent

Basic Container Settings

The primary settings are:

Setting

Description

Spawn Chance Percent

Chance from 0–100% that the container generates loot

Loot Respawn Time Seconds

Time before another loot cycle can begin

Min Items

Minimum normal loot items generated

Max Items

Maximum normal loot items generated

Allow Duplicate Items

Determines whether the same loot entry can be selected multiple times

Allowed Loot Classes

Determines which categories can spawn

Allowed Loot Tiers

Determines which tiers can spawn

Is Key Required

Enables/disables physical locking

Required Key Tier

Selects the physical key required to unlock the container

Example — Civilian Container

A small civilian dresser could use:

Spawn Chance Percent:
65

Loot Respawn Time Seconds:
600

Min Items:
1

Max Items:
3

Allow Duplicate Items:
OFF

Allowed Classes

Clothing ✓
Backpack ✓
Misc ✓

Allowed Tiers

Tier 1 ✓

This creates a low-value civilian loot source.

Example — Military Weapons Locker

A military locker could use:

Spawn Chance Percent:
100

Loot Respawn Time Seconds:
1800

Min Items:
4

Max Items:
8

Allow Duplicate Items:
OFF

Allowed Classes

Assault Rifle ✓
Machine Gun ✓
Handgun ✓
Ammunition ✓
Attachment ✓
Vest Rig ✓
Helmet ✓

Allowed Tiers

Tier 2 ✓
Tier 3 ✓

This produces a much more valuable military loot pool.

Example — Medical Storage

A medical container could eventually use:

Medical ✓
Misc ✓

with:

Tier 1 ✓
Tier 2 ✓

This allows scenario makers to create locations specifically focused on medical supplies.

Medical configuration should still be tested against the actual installed arsenal and scenario dependencies.

Example — High Security Locked Container

A high-value container could be configured as:

Spawn Chance Percent:
100

Min Items:
5

Max Items:
10

Allowed Classes

Assault Rifle ✓
Sniper Rifle ✓
Machine Gun ✓
Ammunition ✓
Vest Rig ✓
Helmet ✓
Attachment ✓

Allowed Tiers

Tier 4 ✓

Lock

Is Key Required:
ON

Required Key Tier:
Tier 3

The result is:

Tier 4 military loot protected by a Tier 3 physical key.

How Loot Class and Tier Filtering Work Together

Class and Tier filters are both applied.

For example:

Allowed Loot Classes:
Assault Rifle ✓
Ammunition ✓

Allowed Loot Tiers:
Tier 3 ✓

does not mean every Tier 3 item can spawn.

It means:

Select items that are Assault Rifles OR Ammunition and are also eligible for Tier 3.

This makes it possible to create highly specialized loot sources.

Designing Different Container Types

Different props can represent different loot economies.

For example:

Civilian House

Clothing
Backpacks
Misc
Food / Drink

Tier 1

Police Station

Handguns
Ammunition
Medical
Vest / Rig

Tier 1
Tier 2

Military Supply Area

Assault Rifles
Machine Guns
Ammunition
Attachments
Vest / Rig
Helmet

Tier 2
Tier 3

High Security Armory

Assault Rifles
Sniper Rifles
Machine Guns
Ammunition
Attachments

Tier 4
Tier 5

Key Required

These are examples only.

Scenario makers are free to create their own progression.

TLL Container Components

A typical TLL-enabled searchable world prop uses the following component structure:

SCR_UniversalInventoryStorageComponent
TLL_LootContainerComponent
InventoryStorageManagerComponent
ActionsManagerComponent
RplComponent

The Actions Manager contains the TLL search interaction:

TLL_SearchContainerAction

The exact component inheritance can vary depending on the original Arma Reforger prefab.

Important — Prefab Inheritance

[!WARNING]

⚠️ Check Inheritance Before Adding Components

Do not blindly add the complete TLL component stack to every child prefab.

Arma Reforger / Enfusion uses prefab inheritance.

A child prefab can inherit components and configuration from a parent prefab.

Because of this, always check whether the required components are already inherited.

For example, if a base cargo container receives the TLL components, several color variants may already inherit that functionality.

Duplicating components unnecessarily can cause prefab or replication problems.

Food, Drinks & Vegetable Crops

[!NOTE]

🍖 Food & Drink Spawning

Food and drink spawning is now functional and integrated into the TLL loot system.

Vanilla Kitchen Loot

Configured food and drink items can spawn in supported vanilla:

Refrigerators

Small refrigerators

Kitchen furniture

Searchable Vegetable Crops

Existing vegetable crops found around house backyards can now be made searchable / lootable through TLL.

The crop uses its configured Forced Loot Pool to provide the corresponding vegetable.

[!TIP]
This allows existing crops already placed around the map to function as natural food sources without manually replacing every crop instance.

Existing World Props

TLL Loot System can use prefab overrides to add loot functionality to existing Arma Reforger world objects.

This allows already-placed terrain objects to become searchable without manually replacing every instance.

Current/ongoing coverage includes objects such as:

Metal cabinets

Desks

Long desks

Short desks

Dressers

Nightstands

Wardrobes

Refrigerators

Small refrigerators

Kitchen furniture

Vegetable crops

Stoves

Washing machines

Chests

Bookshelves

Medical cabinets

Medical bins

Medical furniture

Wooden crates

Industrial storage

Cargo containers

Other suitable world props

Prefab coverage continues to expand during development.

Recommended Scenario Maker Workflow

When creating custom loot behavior:

Step 1 — Choose the Container

Select the world prop or TLL-enabled prefab you want to customize.

Step 2 — Check Components

Confirm that the prefab already contains or inherits the required TLL components.

Step 3 — Configure Spawn Behavior

Set:

Spawn Chance Percent
Loot Respawn Time Seconds
Min Items
Max Items
Allow Duplicate Items

Step 4 — Select Loot Classes

Choose what categories are allowed.

For example:

Assault Rifle
Ammunition
Attachment

Step 5 — Select Loot Tiers

Choose which progression tiers can appear.

For example:

Tier 2
Tier 3

Step 6 — Configure Locking

Decide whether the container requires a physical key.

Is Key Required

If enabled, select:

Required Key Tier

Step 7 — Test In Game

Always test:

Interaction position

Search prompt

Loot generation

Item count

Loot classes

Loot tiers

Inventory opening

Key requirement

Unlock behavior

Multiplayer behavior

before applying the same configuration to large numbers of prefabs.

[!IMPORTANT]

Do Not Edit Core Scripts for Normal Balancing

Scenario makers should normally configure loot using TLL_LootContainerComponent.

Editing the core TLL scripts should only be necessary when extending the actual functionality of the loot system, not when changing ordinary container balance.

Automatic Vanilla & Modded Compatibility

One of the primary goals of TLL Loot System is to avoid giant hand-maintained weapon lists.

Compatible installed content can be discovered and classified automatically.

This allows the system to work with a wide range of:

Vanilla weapons

Modded weapons

Modded equipment

Modded ammunition

Modded attachments

without requiring every scenario maker to manually add every prefab.

However, third-party addons can use unusual component or prefab structures.

Therefore:

Compatibility with every third-party addon cannot be guaranteed.

Important dependencies should always be tested.

Key Distribution

Physical key spawning and unlocking are now functional.

Keys can spawn through configured loot containers, allowing scenario makers to build progression between normal loot areas and key-required locations.

[!NOTE]
Key progression and overall distribution balance are still subject to change during beta development.

For example:

Tier 1 Loot Locations
        ↓
Tier 1 / Tier 2 Keys
        ↓
Tier 2 Progression
        ↓
Tier 3 Keys
        ↓
Military Logistics
        ↓
Tier 4 Keys
        ↓
High Security / Containment
        ↓
Tier 5 Keys
        ↓
Strategic / Endgame Locations

The exact distribution system is still subject to change during beta development.

Custom / Forced Loot System

Scenario makers can add specific custom prefabs to individual containers using the Forced / Custom Loot configuration.

These items are evaluated separately from the normal Class/Tier loot filtering.

The configuration can resemble:

Forced / Custom Loot

[0]
Prefab:
Custom_Camo_Rifle_A.et

Spawn Chance:
100%


[1]
Prefab:
Custom_Camo_Rifle_B.et

Spawn Chance:
35%


[2]
Prefab:
Unique_Sword.et

Spawn Chance:
10%


Minimum Forced Items:
1

This system is intended for:

Custom weapons

Unique weapons

Camo weapon variants

Quest items

Scenario-specific items

Rare equipment

Special rewards

Easter eggs

Progression objects

Forced Loot Will Ignore Normal Class/Tier Restrictions

For example, imagine a container configured for:

Allowed Loot:
Tier 4 Military Equipment

but the scenario maker wants a custom sword to have a chance to appear.

The custom sword could be added to:

Forced / Custom Loot

with:

Prefab:
Unique_Sword.et

Spawn Chance:
25%

The sword would be evaluated separately from the normal Tier 4 loot pool.

Minimum Forced Items

The planned system will also support a minimum guaranteed number of custom items.

Example:

Custom Items:

Camo Rifle A — 30%
Camo Rifle B — 30%
Camo Rifle C — 30%

Minimum Forced Items:
1

If none of the three passes its natural percentage roll, the system can select enough eligible custom entries to satisfy the configured minimum.

If all three naturally pass their roll, all three can spawn.

This allows scenario makers to create locations where:

At least one special reward is guaranteed, but which reward appears can still vary.

[!NOTE]
Custom / Forced Loot is functional, but its balance and use across additional world props may continue to evolve during beta.

Example Scenario Progression

TLL Loot System does not force one progression model.

A scenario maker could build something like:

CIVILIAN AREAS
      │
      ▼
Basic Supplies
Tier 1 Equipment
Early Keys
      │
      ▼
FIRST RESPONDER LOCATIONS
      │
      ▼
Medical Supplies
Handguns
Tier 2 Equipment
      │
      ▼
MILITARY LOGISTICS
      │
      ▼
Rifles
Armor
Tier 3 Equipment
      │
      ▼
CONTAINMENT / HIGH SECURITY
      │
      ▼
Rare Equipment
Tier 4 Loot
      │
      ▼
STRATEGIC COMMAND
      │
      ▼
Tier 5 / Endgame Rewards

Or completely ignore that structure and build something different.

The system is intended to provide the tools, not dictate the scenario.

Beta Notes

Please remember:

TLL Loot System is currently BETA.

Key spawning and key-required containers are functional.

Key progression/balance is still WIP.

Tools are WIP.

Misc is WIP.

Food / Drinks are functional, but coverage and balance are still WIP.

Custom / Forced Loot is functional.

Tier 5 key-required locations require scenario-maker placement/configuration of the included modded TLL container.

Automatic discovery depends on compatible prefab/component structures.

Some third-party addons may require manual catalog overrides.

Existing prefab overrides may need to be retested after Arma Reforger updates.

Loot classifications may change.

Tier assignments may change.

Balance may change.

If your scenario depends heavily on TLL Loot System, test it against the exact version of the mod you intend to use.

Design Philosophy

TLL Loot System is being built around one principle:

Give scenario makers the systems and let them decide how to use them.

The framework provides:

Dynamic Loot

Configurable Classes

Configurable Tiers

Physical Keys

Locked Locations

Searchable Worlds

Automatic Mod Support

Scenario-Maker Control

You decide:

Where loot appears

How much loot appears

How rare loot is

Which classes appear

Which tiers appear

How quickly loot respawns

Which locations require keys

Which keys unlock them

How players progress

What constitutes endgame loot

Support & Community

Need setup instructions, support, or want to follow TLL development?

Join The Last Light community on Discord:

https://discord.gg/CGpqaKcCq3

Built for scenario makers, by scenario makers.
