# 1MBEconomy

Economy balancing workspace for the 1MoreBlock Minecraft server.

This repository is focused on the relationship between CMI `worth.yml` values
used by `/sell` and `/worth`, and ShopGUI+ buy shop configuration used by
`/buy`.

## Current Goal

Build a clean, complete, and balanced CMI `worth.yml` as the source of truth.
After that is stable, ShopGUI+ buy prices should be reviewed against it, with
the default rule:

```text
/buy price = /sell worth * 100
```

For example, if a stick has a CMI worth value of `1`, the ShopGUI+ buy price
should be `100`, unless there is a documented exception.

The tracked economy data lives in `data/`. Keep it current with the local test
server configs, but do not change worth values just because a script reports a
difference. Price changes should be proposed first, reviewed, and then applied
after approval.

## Balancing Rules

Pricing should account for how items enter the economy, including:

- Direct gathering, mob drops, loot, farming, and villager or other gameplay sources.
- Crafting relationships between ingredients and outputs.
- Smelting, blasting, smoking, and campfire conversion paths.
- Stonecutter recipes.
- Waxing, unwaxing, oxidation, scraping, stripping, dyeing, and similar item transformations.
- Edge cases that can create infinite loops, arbitrage, or duplication-like value gain.
- Whether the item can be automatically farmed or obtained very easily.
- Human expectations about value hierarchy, such as iron feeling more valuable
  than copper, and diamond feeling more valuable than iron and copper.

The first pass should cover all in-game items except a small documented
blacklist of items that should not be sold or bought.

Current unofficial blacklist:

- Lingering potions.
- Potions.
- Splash potions.
- Tipped arrows.
- Ominous bottles.
- Creative-only blocks, including test block and test instance block.

## Repository Layout

Current structure:

- `data/CMI/Worth.yml` - tracked CMI worth values mirrored from the test server.
- `data/ShopGUIPlus/shops/` - tracked ShopGUI+ buy shop files mirrored from the test server.
- `docs/` - analysis notes, pricing rationale, and exception lists.
- `servers/` - local test server runtime. This folder is ignored by git.

When live or test-server config files need to be reviewed, copy the relevant
files into `data/` instead of committing a full server directory.

Current local source paths:

- CMI worth file: `servers/Paper-26.1.2/plugins/CMI/Saves/Worth.yml`
- ShopGUI+ buy shop files: `servers/Paper-26.1.2/plugins/ShopGUIPlus/shops/*.yml`

## CMI Worth Commands

Handy to know:

```text
cmi setworth (itemname) -s:(sellPrice)
cmi setworth stick -s:0.55
```

Useful review commands:

- `cmi worth (all/blocks/hand/material)`
- `cmi worthlist -missing` - shows items missing from the worth list.
- `cmi generateworth` - console-only command that estimates missing values from recipe ingredient values.

CMI's `generateworth` command uses the `AutoGenerate.PriceIncrease` setting
from CMI `config.yml`:

```yml
Worth:
  AutoGenerate:
    # Value in percentages in how much more we should add to end product while auto calculating items price based on its ingredient worth
    # For example one stick is worth 0.1 and diamond 44 then end result as diamond_hoe will be worth 88.2 and with extra 2% this will be changed to 89.96
    # Value can be negative
    PriceIncrease: 0
```

CMI creates the `KEY` values in `Worth.yml` automatically. Do not add extra
custom keys to `Worth.yml`; they are expected to be filtered out. Use the Paper
API material list as a validation resource instead.

## Review Policy

Reports should explain what is different, why it may matter, and what the
suggested value would change. Include recipe paths, raw material value,
farmability or ease of access, inflation risk, human value expectations, and
the resulting `/buy` price impact.

Price edits should be opt-in: suggest the changes first, then apply them after
approval.

## WorthHelper

WorthHelper is implemented in the `1MB-CMIAPI-LIB` project as a separate
server-management feature plugin. This repo uses WorthHelper reports to review
economy values; it does not own the plugin source.

Local economy test server jars currently expected in
`servers/Paper-26.1.2/plugins/`:

- `1MB-CMIAPI-LIB-v1.0.0-216-j25-26.1.2.jar`
- `1MB-CMIAPI-WorthDrift-v1.0.0-216-j25-26.1.2.jar`
- `1MB-CMIAPI-WorthHelper-v1.0.0-216-j25-26.1.2.jar`

WorthHelper commands:

- `/worthhelper status`
- `/worthhelper scan [page]`
- `/worthhelper missing [page]`
- `/worthhelper recipes <material> [page]`
- `/worthhelper export`
- `/worthhelper reload`

WorthHelper is read-only by default. It may output suggested
`cmi setworth item -s:value` commands as text, but economy changes still need
human review and approval before being applied.

Useful Paper resources:

- [Paper recipe docs](https://docs.papermc.io/paper/dev/recipes/)
- [Paper 26.1.2 Material enum](https://jd.papermc.io/paper/26.1.2/org/bukkit/Material.html)
- [Paper 26.1.2 Server recipe methods](https://jd.papermc.io/paper/26.1.2/org/bukkit/Server.html#getRecipesFor(org.bukkit.inventory.ItemStack))
- [Paper 26.1.2 inventory recipe classes](https://jd.papermc.io/paper/26.1.2/org/bukkit/inventory/package-summary.html)

## Workflow

1. Keep `data/CMI/Worth.yml` and `data/ShopGUIPlus/shops/` synced from the local test server.
2. Define the item blacklist and document why each item is excluded.
3. Build or import a complete item list for the target server version, starting with `26.1.2`.
4. Normalize `worth.yml` so every allowed item has an intentional value.
5. Analyze crafting and conversion paths for balance issues.
6. Review ShopGUI+ `/buy` files against the final worth values.
7. Document all exceptions to the `worth * 100` buy-price rule.

Keep this README current as the project structure and pricing rules evolve.
