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

## Balancing Rules

Pricing should account for how items enter the economy, including:

- Direct gathering, mob drops, loot, farming, and villager or other gameplay sources.
- Crafting relationships between ingredients and outputs.
- Smelting, blasting, smoking, and campfire conversion paths.
- Stonecutter recipes.
- Waxing, unwaxing, oxidation, scraping, stripping, dyeing, and similar item transformations.
- Edge cases that can create infinite loops, arbitrage, or duplication-like value gain.

The first pass should cover all in-game items except a small documented
blacklist of items that should not be sold or bought.

## Repository Layout

Planned structure:

- `worth/` - curated CMI `worth.yml` files and worth-related notes.
- `shops/` - curated ShopGUI+ buy shop configuration files.
- `reference/` - imported live-server configs used for comparison.
- `docs/` - analysis notes, pricing rationale, and exception lists.
- `servers/` - local test server runtime. This folder is ignored by git.

When live or test-server config files need to be reviewed, copy the relevant
files into `reference/`, `worth/`, or `shops/` instead of committing a full
server directory.

## Workflow

1. Import the current live-server CMI `worth.yml` into a reference location.
2. Define the item blacklist and document why each item is excluded.
3. Build or import a complete item list for the target server version, starting with `26.1.2`.
4. Normalize `worth.yml` so every allowed item has an intentional value.
5. Analyze crafting and conversion paths for balance issues.
6. Review ShopGUI+ `/buy` files against the final worth values.
7. Document all exceptions to the `worth * 100` buy-price rule.

Keep this README current as the project structure and pricing rules evolve.
