A grow-a-garden style game where you buy seeds from the seed shop, plant your seed on your plot in specified grow areas, your plant grows, and then buds a geode, which you can then collect and then crack the geode for a chance at different rarities of gems. There will be randomized scaling of plants that, when grown, will stay grown and replenish their geodes over time, along with one-time use plants that, when the geode is collected, it vanishes.

This game will be using Profile Store by lolerus for the data if possible [ProfileStore \- Save your player data easy (DataStore Module) \- Resources / Community Resources \- Developer Forum | Roblox](https://devforum.roblox.com/t/profilestore-save-your-player-data-easy-datastore-module/3190543)

There will be 6 plots, although the server's size will be set to 5, there are just 6 plots in case a server accidentally gets 6 players. When a user joins, they are automatically assigned a plot and spawn right in front of it. There's a sign for each plot that displays the owner's username. Each plot has 2 grow areas (for now), a base part, a part labeled spawn where players are spawned right above, and a workshop where users can crack their geodes. 

To purchase seeds, you go up to the shop NPC and use a proximity prompt to open up the shop. The shop should restock every 5 minutes with random seeds.  
— The shop GUI that opens has a label for the time left until the next restock in the top left corner. The shop should restock every 5 minutes. On the left half of the shop GUI there should be each seed listed inside a scrolling frame showing an image of the seed (using placeholders for now, I will add the actual image later on), the price of the seed, and the stock of the seed. If the stock of the seed is empty, it should change the text label to red and say no more stock. When you click on a seed (there's a invisible text button over the whole seed template frame) it should then display on the right side of the shop gui a viewport frame which will show what the plant looks like, the plant will be spinning in the viewport frame, there should be a text label for the description of the selected seed, a buy button (text button) that displays how many coins it costs and when clicked if the user has enough money it purchases that seed and depletes the stock by one until the stock is empty, if the stock is empty you buy button should turn red and state out of stock. There is also another text button under the buy with coins button that lets you buy it with Robux, and this can be bought even if the stock is empty. There's also a close button at the top right. Seeds bought will go to the user's hotbar, and if the hotbar is full, it will just go to their backpack. 

For the inventory/backpack setup, there should be a hotbar with 10 slots that's always visible, and on mobile, there should only be 5 hotbar slots, similar to how a grow a garden does it. You can toggle your backpack open by clicking a text button on the upper left side of the screen, and you can close it by clicking the same button or clicking an x button on the actual inventory. Similar to the hotbar, the inventory should show 10 item slots per row, and on mobile, it should only show 5 item slots per row. You should be able to filter between showing all, geodes/gems, seeds, tools, and another slot for future features like pets or cosmetics. You should be able to drag and drop stuff from your inventory/hotbar, similar to grow a garden. If the user clicks or presses a slot in their hotbar, it should equip it. Seeds and tools should be able to stack, but geodes and crystals shouldn't since they will all be different sizes, different mutations, etc. Items (seeds, tools, etc) should just show the text of what it is for example, let's say you have a common geode and it's 1.24kg and has a frozen and hot mutation, it should display as \[Frozen, Hot\] Common Geode \[1.24 kg\]

When you have a seed equipped you can then place it on a grow spot in your plot only users should not be able to place seeds/tools or do anything with other people's plots besides spending some Robux to steal a geode. You should not be able to place multiple seeds on top of each other; they should have to be slightly spread out. When the seed is planted, the plant starts growing based on a randomized scale, changing the size of the plant. 

For example seeds may have a 20% chance to grow at a scale of 0.60-0.89, a 50% chance to grow at a scale of 0.90-1.29, 20% chance to grow at a scale of 1.3-1.69, 9% chance to grow at a scale of 1.70-2.09, and a 1% chance to grow at a scale of 2.10-5.00

\#\#\# 📑 Mandatory Constants & Tables

\`\`\`lua  
\-- Scale odds (plant size factor)  
ScaleOdds \= {  
    {min \= 0.60, max \= 0.89, weight \= 0.20},  
    {min \= 0.90, max \= 1.29, weight \= 0.50},  
    {min \= 1.30, max \= 1.69, weight \= 0.20},  
    {min \= 1.70, max \= 2.09, weight \= 0.09},  
    {min \= 2.10, max \= 5.00, weight \= 0.01},  
}

There are different types of plants. There are plants that just grow once and when the geode is harvested, the plant and geode are deleted, and there are replenishing plants, which after the plant finishes its growth cycle it start to generate geodes which, when harvested, keep the plant there and regrow the geode. For replenishing plants they follow the normal scaling odds but the geodes that grow from the replenishing plant are given their own scale odds skewed based on the replenishing plants size, such as if the replenish plant is 2.4 scale then the odds of the geodes being around that scale are way larger and the odds of being a smaller scale are minimized. If the plant is non-replenishing, then the geode just scales at the same size of the plant's scale. 

Each plant has a default weight, such as a geode sprout may have a default weight of 0.8KG but since the plant grew with a 1.2 scale factor, the weight would then be 0.96 kg.  
Geode value is changed based on the scale factor.

Different plants have different growth cycles, such as a geode sprout, which may have 4 stages of growth, while a bush, which may have 10\. I also think there should be geode stages, so when there's a replenishing plant, it's easy. There would really only need to be 4 stages of the geode's growth. 

There should also be offline growth like grow a garden where if you plant a seed and come back later on it will be grown based on how long you were gone.

Here's A lil chart of some plants and cracked geodes.

| Seed Name | Grow Time | Price | Gem Chance (after the geode is broken, the odds of it being a certain gem.) | Description | Regrow T/F | Harvested geode name |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Geode Sprout | 30 seconds  | $30 | 70% Common 25% Uncommon 5% Rare | Flower stem that grows A geode instead of flower | F | Sprout Geode |
| Hanging Geode | 60 seconds | $60 | 50% Common 35% Uncommon 15% Rare | Another flower stem, but the geode is hung upside down | F | Hanging Geode |
| Geode Bush | 120 seconds, After initial plant is grown Geodes grow at a rate of 45 seconds at a max of 4 geodes | $250 | 40% Uncommon, 35% Rare, 25% Rare+ | Bush type thing that can grow up to 4 geodes  | T | Bush Geode |
| Crystal Cactus | 150 seconds | $350 | 35% Rare, 30% Rare+ 35% Very Rare | cactus | F | Cactus Geode |

| Cracked Geode(Gem) Rarity | Gem sell price | Geode Name |
| :---- | :---- | :---- |
| Common | $50/kg | Quartz |
| Uncommon | $75/kg | Onyx |
| Rare | $110/kg | Amethyst |
| Rare+ | $150/kg | Dyed Agate |
| Very Rare | $ 210/kg | Cathedral |
| Very Rare+ | $ 300/kg | Apophyllite |

Events– There should be events that can happen that have a small chance of adding a mutation to separate plants although I'm not too focused on this now so at the moment there should be 2 random events, wind gusts and flood which apply the gust modifier and soaked modifier. These will add a multiplier to your geode value, not sure on exact values for now. Geodes should be getting these modifiers not the plant itself if that makes sense, if you have a replenishing bush you don't want the bush to be winded only the geodes.

When you harvest a geode it will have a name/type based on the plant that it grew from such as a sprout geode from a geode sprout or a hanging geode from a Hanging geode plant, these geodes then have a chance to be cracked into certain gems based on what plant they are from such as a geode sprout when cracked has a 70% Common gem 25% Uncommon gem  
5% Rare gem

Each plot has a workbench which when you open it through the proximity prompt a gui pops up showing your current geodes on the left side in a scrolling frame, you can click a geode which will then break and then show which gem you got on the right hand side. There should also be a button somewhere to crack all if you don't want to individually crack each gem and in the description area on the right it will just say all geodes cracked\! There also needs to be a close button on this gui.

Opening any new ScreenGui must Close() an existing one to prevent overlap.

Game loop recap: Coins → Seeds → Geodes → Gems → Coins.

For anything with robux just use placeholders for now as it's not my main focus

There needs to be Mobile Detection for stuff like the inventory 

All currency/item changes must run **server-side** only; never trust client values.  
\-- Profile template for DataManager  
DefaultProfile \= {  
    Currency     \= 0,  
    Inventory    \= {},  \-- \[GUID\] \= itemStruct  
    ActivePlants \= {},  \-- \[GUID\] \= plantStruct  
    Receipts     \= {},  
    LastLogin    \= 0,  
}

