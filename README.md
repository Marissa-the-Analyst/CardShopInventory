# CardShopInventory
I've been diving back into Pokémon lately since a card shop opened near me. The store lacks a proper inventory system and functions more like an upscale yard sale, using price guns to stick prices on product. In this scenario, I asked the question, what if someone came in looking for 1 specific card? Multiplied by 2 different platforms! 

### Finished products ### 

- View the Excel Dashboard [click here](https://1drv.ms/x/c/4816316897784cf5/IQA2-5E-PcMXQrIk6Q9BCeoWAXSh5LEdrPhP826JXVRFK64?e=IfaXuc)  

- View the Tableau Dashboard [click here](https://public.tableau.com/app/profile/marissa.nash/viz/CardStorage/Dashboard1) 

### Inspiration ### 

My resurgence in Pokémon has led me on a quest to collect all 1025 Pokémon cards. As a child, I got them for Christmas or after a long grocery trip. Now, the cards are much more desirable and expensive (to my dismay). Regardless, that many Pokémon meant that much more data! As of March 28th, I am a mere 15 cards away from completing all 1025. To source these cards, I’ve been diving into bulk bins at the card shop. Bins that can almost certainly hold 3000-5000 cards each. While it’s relaxing and fun to dig through these bins for treasure, when you’re down to 15 cards, it makes it difficult to find any! <br> 

Even for the more expensive cards, imagine as a business, you’re looking for a card someone ordered or requested, but if you can’t find it, you’ve lost a sale! If someone called the store and asked, “Do you have xyz Pikachu?” and you had to put them on hold and scour 3 different storage areas, that wouldn’t be very efficient and once again the sale is in danger. <br> 

I enjoyed [Inventory Management Dashboard(v2)|Tableau Public‘s](https://public.tableau.com/app/profile/lawer.akrofi/viz/InventoryManagementDashboardv2/InventoryManagementDashboard) take on creating a comprehensive inventory system while displaying KPIs about order fulfillment. The “detailed” section in particular gave me the inspiration to create this dashboard. <br> 

### Programs Used ### 

- Copilot for Data Generation  

    - These card representations and values are completely fictional 

- Excel for Data Collection, Cleaning, Visualization 

- Tableau for Data Visualization 

### Scope of Work ### 

**Deliverables** <br> 

- A table of Pokémon card inventory 

- A table of Pokémon card orders 

- A table of card shop capacities 

- A table of booster inventory 

- 2 similar visualizations across 2 different programs 

### Goals ### 

**General** <br> 

I wanted to create a straightforward search bar that allowed the user to search for the Pokémon card and find out exactly where it is located. Simulating a card shop environment, I drafted synthetic card data and realistic storage area and methods that align with my own observations while perusing my local card shop. There’s definitely a larger angle to pursue with shop capacity that can help make planning decisions for ordering more product, adjusting bulk intake process, or planning giveaways, but I decided to narrow the scope to meet an immediate need for the stakeholder. <br> 

**Why 2 Programs?** <br> 

I choose to recreate this visualization in 2 different programs, to practice my mastery over each one of them. By having a predefined goal, I’m able to directly examine the differences between each program and apply an analytical perspective on how I may go about achieving the same goal across different platforms. Plus, it helps to have that flexibility when every company utilizes a different tool.  

### Data Source and Collection ### 

I began collecting data by browsing TCG Player and inputting each card manually into Excel using that data. CRTL + Shift + V made my hands ache! Eventually, I realized that the actual content on the cards didn’t have to be accurate since the purpose was just showing an example inventory system. That’s when I went to Copilot to help create some synthetic, and inaccurate data. I then organized it loosely into different pricing bins. I figured bulk would ideally be organized by set. Older sets going in the first bins and newer sets in the later bins. Pricier cards can go in binders and cases. 

For the capacities and orders, I utilized Excel formulas like RANDBETWEEN to generate order numbers. Then for order placed and packed dates I manually just did a random range of dates and subtracted the two columns to get ship time.  

## Viz Design and Creation ## 
#### Excel #### 

I played around trying to mimic the inspiration display in Excel as close to the reference as possible. This project was a great refresher in how developing dashboards in Excel works. I also came to recognize the significant limitations of cloud Excel versus desktop Excel. <br> 

<img width="899" height="564" alt="image" src="https://github.com/user-attachments/assets/ce430ade-59df-455d-b6b4-9684e25306ee" />

Just look at how painful these merged cells look on my first go around. I was so confused about why it wasn’t working very well. <br> 

Once I re-familiarized myself with creating shapes and utilizing textboxes, I was able to easily add the 7 quick info KPIs and focus on the “Card Look-Up" section. This formula is the star of the “search” function on the dashboard: <br> 
=FILTER(CHOOSECOLS(Table1, 2, 3, 6), ISNUMBER(SEARCH($E$13,Table1[Card Name])),"No results") <br> 
 
Breaking it down in to plan English: <br> 
#### CHOOSECOLS #### 

- Selects the columns you want to display in the filtered result 

#### SEARCH ($E$13, Table1[Card Name]) #### 

- Checks all of the “Card Name” column for the value listed in the “search box”, E13. This works well because search is case-insensitive. If found it returns the numerical starting position, if not found it returns an error. 

#### ISNUMBER #### 

- Checks if SEARCH found a number and gives a TRUE or FALSE result.  

#### FILTER(array, include, [if_empty]) #### 

- Filters the columns to only show the rows that are TRUE and returns “No Result” if false.  

### Cons of this formula ### 

If there were a Pokémon simply named “pika” both “Pika” and “Pikachu” would show in the results 

## Tableau ## 

While Excel took a few hours to remember, Tableau was still fresh in my mind! This project also required very similar tools to the [Stardew Valley Recipes Project](). <br> 

**Search Bar** 
I directly took the formula for creating a search bar from the Stardew Valley project. It uses a parameter to “hold” the searched value and uses a calculated field to filter the results. Below is the calculated field formula: <br> 

{ FIXED [Card Name] : MAX(CONTAINS(LOWER([Card Name]), LOWER([Card Search]))) }  

<br> 
Lower ensures that both the search string and the card are read the same regardless of case. CONTAINS checks if the Card Name contains any of the Card Search strings and returns TRUE or FALSE. The MAX checks for *any* row within the table returns true and if they do it gives an aggregated value of TRUE. <br> 
<br>

**Detailed Table** <br> 
I used a Tableau table extension to seamlessly display the data searched without having to navigate Tableau’s finnicky native table system.  

### Opportunities ### 
There is no way to connect it with a point of sales system. Like to regularly update it. If someone packed a card, they would have to manually remove that entry from the source dataset. Digging in deeper to how inventory management systems are built and managed could help develop more detailed dashboards in the future. It would also have been cool to be click on an order and just have it auto populate the order details. 

### Reflection ### 
I enjoyed the practical nature of this project. It reminds me a lot of what I work with at my day job and tackles a lot of the problems I’m seeing during my visits to my local card shop. There are definitely arguments for and against implementing a system like this, but on a small scale, I think it is helpful for tracking inventory, preventing overstock, and getting customers serviced quicker.  
