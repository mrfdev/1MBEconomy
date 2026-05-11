# TODO

## Setup

- [ ] Add live-server CMI `worth.yml` to the repo for analysis.
- [ ] Add current ShopGUI+ `/buy` configuration files for later comparison.
- [ ] Add notes for the local `servers/` test server focused on `26.1.2`.

## Worth.yml First Pass

- [ ] Build or import a complete in-game item list for the target server version.
- [ ] Define and document the item blacklist.
- [ ] Confirm the unofficial blacklist: lingering potions, potions, splash potions, tipped arrows, ominous bottles, and creative-only blocks like test block and test instance block.
- [ ] Check that every allowed item exists in the core `worth.yml`.
- [ ] Normalize item names and formatting so diffs stay readable.
- [ ] Identify missing, duplicated, obsolete, or renamed items.

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
