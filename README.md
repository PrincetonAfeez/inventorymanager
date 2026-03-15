#inventorymanager
Python Script that handles inventory management
Project: The "86-List" Inventory Manager
Concept Focus: Lists, Dictionaries, For-Loops, and Strings.

The Scenario: You are performing an end of night inventory

The Task: 
1. Establish your products and total inventory counts. 
For each product, establish Inventory on the line, Inventory in the Walk-In and Safety Stock in Freezer
Establish starting inventory (Service Ready on the line, Weekly Usage stored in Walk-In, Safety Stock in Freezer)
Total inventory = Daily Usage + Safety Stock in Freezer
Calculate Daily Usage = Inventory on the line + Inventory in the Walk-In

2. Generate your product mix
At the end of each shift, ask the user "How many [Dish Name] were sold today?" 
Produce Product mix afer service

3. Establish your Waste Log
Then ask the user "How many [Dish Name] were comps?" 
Alert the user that total comps should include Server Errors + Kitchen Errors + Bad/Damaged items
Comps = Waste log (Server Errors + Kitchen Errors + Bad/Damaged items)

4. Establish Inventory On-Hand
Subtract product mix + comps from total inventory

5. Reports
For each product, print one comprehensive lists:
-Starting inventory count, subtract your product mix, subtract your comps and produce a list of inventory on hand
-Location & Count of each product
-If inventory count > inventory on hand, raise an exception ("Sorry, this is not adding up, please update your product mix, comps and inventory count"), then ask for those numbers again
-If inventory on hand < Inventory Count, ALERT items are missing
-Add to 86 Lists when total inventory = 0, ALERTS in ALL CAPS so the managers can see them clearly.
-Add to Prep list for the next shift if total inventory <= 50% of Daily Usage, ALERT in ALL CAPS so the kitchen can see them clearly.
-Add products to Shopping list if total inventory <= 25% of Daily Usage, ALERT in ALL CAPS so the managers can see them clearly.
-At the end print 86 List, Prep list and Shopping List.

Pseudocode:

Phase 1: The Setup (The "Brain")
Before the shift starts, you need to know what you have.

1. Define a Custom Exception: Create a simple class called InventoryError. This is how you'll tell Python, "Hey, the math doesn't add up!"
2. Create your Product List: Create a list containing dictionaries. Each dictionary is one product.
*Example: {"name": "Burger", "line_inv": 10, "walk_in_inv": 20, "freezer_inv": 5, "safety_stock": 10}.
3. Calculate Initial Totals: For each product:
*Set daily_usage = line_inv + walk_in_inv

Phase 2: The Shift Data (The "Input")
This is the part where the user enters what happened during the night.
4. Loop through each product:
*Start a while True loop (This is your "Validation Gate").
*Inside a try block:
    -Ask: "How many [Product] sold?" (Convert to int).
    -Ask: "How many [Product] comps?" (Remind them this includes errors/damaged).
    -Ask: "Count the [Product] in the kitchen now." (Physical Count).
    -Calculate on_hand_inv = starting_inv - (sold + comps).
    -The Logic Checks:
        *IF physical_count > on_hand_inv: raise InventoryError.
        *IF physical_count < on_hand_inv: Print a warning "ALERT: ITEMS MISSING".
    -If everything is okay:
        *Save the sold, comps, and physical_count into that product's dictionary.
        *Use break to exit the while loop and move to the next product.
*Inside an except ValueError block:
    -Print "Please enter numbers only!"
*Inside an except InventoryError block:
    -Print "Sorry, this is not adding up, please update your numbers." (This keeps them in the loop to try again).

Phase 3: The Reporting (The "Output")
Now that you have all the data, it's time to alert the managers.
5. Create three empty lists: eighty_six_list, prep_list, and shopping_list.
6. Loop through the products one last time:
*Print the Summary: Show the product name, what you started with, what was sold/comped, and what is left.
*Check Thresholds:
    -IF total_inventory == 0: Add name (in UPPERCASE) to eighty_six_list.
    -IF total_inventory <= (0.5 * daily_usage): Add name (in UPPERCASE) to prep_list.
    -IF total_inventory <= (0.25 * daily_usage): Add name (in UPPERCASE) to shopping_list.
7. Final Print:
*Print the eighty_six_list with a big header: "86 LIST - DO NOT SELL".
*Print the prep_list with a header: "KITCHEN PREP FOR TOMORROW".
*Print the shopping_list with a header: "ORDERING LIST FOR MANAGER".
