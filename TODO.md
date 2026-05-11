# TODO

## Setup

- [x] Add CMI `Worth.yml` to tracked `data/` for analysis.
- [x] Add current ShopGUI+ `/buy` configuration files to tracked `data/` for later comparison.
- [x] Add notes for the local `servers/` test server focused on `26.1.2`.
- [ ] Keep `data/CMI/Worth.yml` synced with `servers/Paper-26.1.2/plugins/CMI/Saves/Worth.yml`.
- [ ] Keep `data/ShopGUIPlus/shops/` synced with `servers/Paper-26.1.2/plugins/ShopGUIPlus/shops/`.

## Worth.yml First Pass

- [ ] Build or import a complete in-game item list for the target server version.
- [ ] Define and document the item blacklist.
- [ ] Confirm the unofficial blacklist: lingering potions, potions, splash potions, tipped arrows, ominous bottles, and creative-only blocks like test block and test instance block.
- [ ] Check that every allowed item exists in the core `worth.yml`.
- [ ] Normalize item names and formatting so diffs stay readable.
- [ ] Identify missing, duplicated, obsolete, or renamed items.
- [ ] Use `cmi worthlist -missing` to compare CMI's missing-item report with our tracked analysis.
- [ ] Review whether `cmi generateworth` suggestions match our own recipe-based analysis before accepting them.

## Economy Balance

- [ ] Analyze crafting recipes and ingredient-to-output value relationships.
- [ ] Analyze smelting, blasting, smoking, and campfire conversion paths.
- [ ] Analyze stonecutter recipes.
- [ ] Analyze waxing, unwaxing, oxidation, scraping, stripping, dyeing, and similar transformations.
- [ ] Flag arbitrage loops where players can profit by converting, buying, or selling items.
- [ ] Document intentional exceptions and special-case pricing decisions.
- [ ] Review whether trial spawner should be sellable/buyable, and determine a fair value if included.
- [ ] Review whether vault should be sellable/buyable, and determine a fair value if included.
- [ ] Review how spawners should be handled, including whether they need separate values by entity type.
- [ ] Make review reports include farmability, ease of access, inflation risk, and human value expectations.
- [ ] Require approval before applying suggested worth changes to tracked config files.

## ShopGUI+

- [ ] Compare ShopGUI+ buy prices against the final worth values.
- [ ] Apply the default `/buy = worth * 100` rule where appropriate.
- [ ] Find items present in `worth.yml` but missing from `/buy`.
- [ ] Find `/buy` items that are missing from `worth.yml`.
- [ ] Review category placement and shop usability after prices are corrected.

## Tooling

- [ ] Add validation scripts for missing items and invalid price relationships.
- [ ] Add a report that lists buy/sell ratios and exceptions.
- [ ] Add a repeatable test process using the local server.
- [ ] Prototype a Paper helper plugin that reads worth values and reports recipe-derived value suggestions.
- [ ] Use Paper recipe APIs to inspect shaped, shapeless, cooking, stonecutting, smithing, and other registered recipes.
- [ ] Use the Paper 26.1.2 `Material` enum as the canonical item/material list for completeness checks.
- [ ] Ensure helper tooling outputs suggested `cmi setworth item -s:value` commands without applying them automatically.
