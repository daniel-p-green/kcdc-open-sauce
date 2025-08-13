# JFS Shopping Sheet Optimization (LLM-assisted, no full inventory system)

## Problem
The JFS Shopping Sheet template encodes category caps (e.g., Vegetable≤6, Fruit≤2, Soup≤2, Crackers≤1, Pasta/Rice≤1, Peanut Butter≤1) and flags like KOSHER. This JFS does not run full inventory/order management. Staff still need fast, fair selections per client and an aggregate pick-list without maintaining a heavy system.

## Approach
- Maintain a lightweight daily inventory snapshot (CSV).
- Maintain a simple client list with kosher flag and notes (CSV).
- Use an LLM to propose items under the template caps, honoring kosher and notes (e.g., “no nuts”, “low sodium”).
- Validate/clamp with Python so caps and stock are never exceeded.
- Emit per-client pick lists and an aggregated warehouse pick list.

## Minimal inputs
- inventory.csv
item_name,category,kosher,quantity_available,low_stock,tags
Black Beans,Beans,yes,120,false,gluten_free
Chicken Soup,Soup,yes,40,false,low_sodium
Whole Wheat Pasta,Pasta/Rice,yes,80,false,whole_grain
Saltine Crackers,Crackers,yes,25,true,
Apples,Fruit,yes,100,false,
Carrots,Fresh Produce,yes,120,false,
Ground Turkey,Protein,yes,40,false,
Peanut Butter,Baking Items/Staples,yes,50,false,nut

- clients.csv
client_name,kosher,notes
Levi Family,yes,needs low sodium; no nuts
Garcia Household,no,likes beans & pasta

Category caps auto-derived from the template text:
- Vegetables: 6
- Fruit: 2
- Beans: 2
- Soup: 2
- Crackers: 1 (low stock, avoid if possible)
- Tomato/Pasta Sauce: 2
- Pasta/Rice: 1
- Peanut Butter: 1
- Staff-only categories (Personal Products, Pet Food) excluded from auto-pick

## Outputs
- client_picklists.csv: per-client, per-category itemized selections.
- aggregate_picklist.csv: total quantities per item for warehouse pick.

## Why this fits JFS without inventory tracking
- Only a daily “what’s in today” CSV is required.
- The LLM proposes; the validator guarantees caps/stock fairness.
- Staff can tweak inputs or outputs as needed.

## Next steps
- Add a small “variety rotation” CSV to avoid giving the same items week-to-week.
- Join with routing outputs to emit route-specific bundles for drivers.
- Optional: Telegram admin command to trigger picks and return CSVs in chat.
