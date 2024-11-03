# Programming the Farming Drone (Report)

## Introduction
"The Farmer was Replaced" is a unique game that builds farminig mechanics with advanced technologies, whose role is auto agriculture. Thought it's primarily a farming game, it includes strategies and management elements where the player must give importance to reesources. The game revoles around a farm where a drone takes tasks previously handled by farmers. It focus is on how the is game will impact the farm and the farmer. Its main goal is to harvest grass to unlock more tiles or resources. Its aim is to harvest resources using the drone in the most efficient way possible to unlock new features and areas.

# Table of Contents
- [Code Snippets and Explanation](#code-snippets-and-explanation)
- [Challenges and Learnings](#challenges-and-learnings)
- [References](#references)

# Code-Snippets-and-Explanation

## Step 1: Farming on 1 tile

**Code:**

```python
while True:
    if can_harvest():
        harvest()
    else:
        do_a_flip():
        harvest()
```
**Explanation:**

---
After I have harvested enough hay, i have unlocked loops and speed of drones.The While fuction is a loop that can hold 2 conditions True or False, depending on the conditions it can be a infinite loop if it is True conditon and a never run loop if it is False condition. In this case I have created a infinite loop that will keep harvesting hay, Though i have increased the speed of the drone, the speed of drone is faster than the grass or hay growing speed.Inoder to slove this problem i have also unlocked a new feature called can_harvest() where i used this feature in a if else statement which the drone will only harvest when the grass has grown completely and else it will do a flip and then only harvest giving grass time to grow while it does a flip.

**Demo:**

Video Demo:
[Step 1 Video]()
[Step 1 Screenshot]()
[Google Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the above code i was able to get enough hay to increase the speed of the drone and upgrade the yield of the grass. I was also able to expand the area form 1 Tile to 3 Tile. And i was able to unlock plants with it.
 - These features were unlocked too: plant(Entities.Bush), move() functions.

## Step 2: Farming on 3x1 tile

**Code:**

```python
while True:
    plant(Entities.Bush)
     move(South)
     harvest()
     move(South)
     harvest()
     move(North)
     harvest()
     move(North)
     do_a_flio()
     do_a_flip()
     if can_harvest():
        harvest()
```
**Explanation:**

---
After unlocking the 3 by 1 tile and plants. I used these codes to first plant a bush then move the drone from south to north while i harvest the hay on the way and when the reach the plant i will do two flips giving it time to grow wood and if ready i will hervest the wood.

**Demo:**

Video Demo:
[Step 2 Video]()
[Step 2 Screenshot]()
[Google Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the code above I was able to get enough hay and wood  to unlock the 3*3 tile and upgreade the spped of drone and yield of hay,I was also able to unlock senses where the drone can see what is underneath it.
 - These features were unlocked too: num_items(), Operators like <,>,=.

---
 ## Step 3: Farming on 3x3 tile

**Code:**

```python
while True:
    for x in range(get_world_size()):
        move(East)
        trade(Items.Carrot_seed)
        for y in range (get_world_size()):
            if num_items(Items.Carrot) < 150:
                if can_harvest():
                    harvest()
                    till()
                    plant(Entities.Carrot)
                move(South)
            else:
                return
```
**Explanation:**

---
This code moves the farming drone across a grid-like world, the while true is the inifinate loop whcih means the codes wiill continue unless a specific condition stops it. For x in range(get_word_size()) gives the full dimensions of the world which allows the loop to move from one end to the other end of the grid. x loop controls the horizontal movement and the y loop controls the vertical movememnts. Since the carrots can not be hervested directly we need to use trade(itesm.carrot_seed) to trade for carrot_seed at each tile acroos the grid, it makes sure that the drone has seeds to plant after harvesting. The if num_items is the new fuction i unlocked ealier that checks if the drone has enough number of required items in its inventory, if not enough items it will continue and else stop. The till() is a new function that is required to obtain carrot which prepares the tile for plating by tilling the soil. The plant(entities.carrot) function plants a carrot seed in the tilled soil which will start the growth of a new carrot. And the if the Drone has obtained the required number of items in its inventory the function returns which will end the loop stopping further actions. I had a replaced the above items from carrot to bush whenever i needed wood to trade with carrot seeds and when i needed wood to unlock other new features.

**Demo:**

Video Demo:
[Step 3 Video]()
[Step 3 Screenshot]()
[Google Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the code above I was able to get enough hay, wood and carrots to unlock 4*4 tiles, increased the speed of the drone, have unlocked variables, have unlocked trees, have unlocked watering and unloced Functions.
 - These features were unlocked too: get_water() , trade(Items.Empty_Tanl) , use_item(Items.Water_Tank), def functions

---
## Step 4: Farming on 4x4 tile

**Code:**

```python
def reset_drone():
    while get_pos_x() != 0:
        move(East)
    while get_pos_y() != get_world_size() -1:
        move(North)

def harvest_grid():
    for x in range(get_world_size()):
        for y in range(get_world_size()):
            if get_ground_type() != Grounds.Soil:
                till()
            if can_harvest():
                harvest()
            move(South)
        move(East)
harvest_grid()

Total_grid = get_world_size() * get_world_size()
Requriments = 2000
checks = 0
reset_drone()
harvest_grid()
while num_items(Items.Pumpkin) < Requriments:
    while checks != Total_grid:
        checks = 0
        for x in range(get_world_size()):
            for y in range(get_world_size()):
                if can_harvest():
                    checks = checks + 1
                else:
                    if num_items(Items.Pumpkin_Seed) > 5:
                        trade(Items.Pumpkin_seed)
                    water_me(.75)
                    plant(Entities.Pumpkin)
                move(South)
            move(East)
    harvest()
    checks = 0
```
**Explanation:**

---
The purpose of the first function is to bring the drone to its initial position where the get_pos_x() loop moves it to leftmost position by reoeatedly moving to east and the get_pos_y() loop moves it to the top of the grid. The second harvest function that will harvest or till the area across the grid, it makes sure that the ground is till before planting anything in the area and harvest everything that can be harvested. Now that i have alrady unlocked variables, i will use a total gird varible to calculate the total number of cells in the grid based on world size. A requirement variable to set a target of required items. A check to keep track of how many cells have been checked so far. Then i call the reset drone function and the harvest function to set the drone to starting position and the grid is harvested initially. Then i use a while loop that continues until i obtain the target items. Then i use sub while loops under the main loop to check each cell to see if it can be harvested or planting and watering if needed. A if
can_harvest(): checks += 1 ,increases with number of crops ready to harvest.A else statement if the crops aren't ready, trades seeds if less than 5, waters the cell 75% and plants the seed.After checking all the cells, the drone harvest the available items. Finally, the checks variable to reset the next iteration.


**Demo:**

Video Demo:
[Step 4 Video]()
[Step 4 Screenshot]()
[Google Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the code above I was able to unlock Sunflowers, MultiTrade, Utilities, Lists , Fertilizer and Polyculture. 
 - These features were unlocked too: measure() , trade(Items.Carrot_Seed), min() , max(), abs() , and random(), 

---
## Step 5: Farming on 5x5 tile

**Code:**

```python
def trade_req(items_tt, req):
    while num_items(items_tt) < req:
        if not trade(items_tt):
            return False
    return True

def water_me(percent):
    if get_water() < percent:
        use_item(Items.Water_Tank)

TOTAL_GRID = get_world_size() * get_world_size()
REQURIMENTS = 2000
checks = 0
reset_drone()
harvest_grids()
while num_items(Items.Pumpkin) < REQURIMENTS:
    while checks != TOTAL_GRID:
        checks = 0
        for x in range(get_world_size()):
            for y in range(get_world_size()):
                if get_entity_type() != Entities.Pumpkin and not get_entity_type() == None:
                    harvest()
                elif get_entity_type() == Entities.Pumpkin:
                    checks = checks + 1
                else:
                    while not trade_req(Items.Pumpkin_Seed, 5):
                        plant_crops(Entities.Carrots, 50)
                        reset_drone()
                        harvest_grids()
                    water_me(.75)
                    plant(Entities.Pumpkin)
                move(South)
            move(East)
    harvest()
    checks = 0
```
**Explanation:**

---
The first trade req fuction is trade for a specific number of items, it checks if the number of items of the type is less than the req if it is try to trade for more.But if it fails, it returns false and stops and when required is met it returns true.
The Water me function is to water the crops if the moisture level is less. A total grid variable was given to calculate the total number of cells in grid. Requriments is the target amount, check variable tracks the number of cells containing items, The rest drone and harvest function to bring the drone to its initial position. The main num_items while loop continues uless the target amount is met, While check loop to handle any prvious plants ready to harvest or not. For the x and y range gives the x and y coordnates of the grid. The if get entity type and not get entity type conditions for harvesting that empty or not pumpkin entity. The elif condtion if cell has a pumpkin increase check by 1.Else if the cell is empty , it checks if there is enought seeds and makes sure that the seed value doesn't go below 5, but if not it plants carrots and resets the drone's position, The water me and plant entities to ensure that ocnce there is enought seeds, it waters the cell to 75% moistur and plants a pumpkin. The the drones moves to next cell and after finsihing the grid it does a final harvest. 
**Demo:**

Video Demo:
[Step 5 Video]()
[Step 5 Screenshot]()
[Go0gle Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the code above I was able to unlock Lists , Fertilizer , Polyculture, and Dictionaries 
 - These features were unlocked too: list[], list.append(), list pop(),list.remove(), list.insert(), len(list), use.item(Items.Fertilizer), trade(Items.Fertilizer), get_entity_type() , Entities.Treasure, Entities.Hedge, get_companion(), [Entities.Carrots, 3, 5], Entities.Grass , Entities.Bush, Entities.Carrots, and Entities.Tree.

---
## Step 6: Farming on 6x6 tile

**Code:**

```python
def plant_sunflower(req):
    WATER_PERCENT = 0.65
    reset_drone()
    harvest_grid()

    while num_items(Items.Power) < req:
        for x in range(get_world_size()):
            for y in range(get_world_size()):
                while not trade_req(Items.Sunflower_Seed, 5):
                    plant_carrots()
                water_me(WATER_PERCENT)
                if num_items(Items.Power) < req:
                    if can_harvest():
                        harvest()
                    if get_ground_type() != Grounds.Soil:
                        till()
                    plant(Entities.Sunflower)
                    move(South)
            move(East)

    max_petals = 0
    list_petals = []
    coords = []

    for x in range(get_world_size()):
        for y in range(get_world_size()):
            num_petals = measure()
            list_petals.append(num_petals)
            coords.append([get_pos_x(), get_pos_y()])
            move(South)
        move(East)

    max_petals = max(list_petals)
    count = 0
    for numpetals in list_petals:
        if numpetals == max_petals:
            break
        count += 1

    goto(coords[count][0], coords[count][1])
    coords.pop(count)
    harvest()
    num_maxes += 1

```
**Explanation:**

---
The water percentage is 0.65 mositure of the cell, the reset_drone() and harvest() is the fuction that will bring the drone to its initial position. The mian while loop to continue the number of items() until it meets the target the amount which governs the planting and maintance of crops. The for loops looks over the grid dimensions and get world size which is the full are of the grid. The while not loop if required
amount of sunflower seeds is not available and plants other crops. The water me fuction to provide water in the tile when nessary , the can harvest and get ground type to check if it is soil it calls till() to prepare the ground to plant crop. And the movements to move four sides of the grid. The finding maximum petals fucntion to tract the maximum while they store the values in lists. The measure() captures the number of petals in lists, once the loops are done the max_petals holds the hightest value. Then it shows the occurences of max and save the corrdinates. Finally the to havest the max petal location, the drone moves to the maxium petal using the goto()
then harevst it there. The num_maxes variable to keep track of the number of max petal plants harvested.

Video Demo:
[Step 6 Video]()
[Step 6 Screenshot]()
[Google Drive Link](https://drive.google.com/drive/folders/1V77aALlfDiZ7lyLWqI4VcP_zHm1lKEDt?dmr=1&ec=wgc-drive-globalnav-goto)

---
**Notes**
 - Using the code above, I was able to harvest enough pumpkins to meet the requirements for this stage.
 - These features were unlocked too: advanced navigation functions and automated resource management for larger grids.

---
# Challenges and Learnings

## Challenges

The challenges I faced was that navigating a larger grid (6x6 and beyond) required adjusting the movement logic to make sure the drone covered all tiles without missing any. At first, I was having issues where the drone would skip tiles or do actions twice on the same tile, so I had to spend time fine-tuning the loops. Managing resources like seeds and water was also more challenging on a bigger grid. I had to make sure the drone didn’t run out of seeds halfway through the grid and had to figure out when to trade for more. Timing between harvesting, tilling, and planting was really important to keep the drone productive, because without good timing, some tiles would stay unharvested, which slowed down everything. The larger grid also caused some new errors, like the drone trying to do actions on tiles it shouldn't (like trying to plant on ground that wasn’t tilled). Fixing these errors was important to make sure the drone’s actions were smooth and reliable. The bigger tile size also showed how repetitive movements could make the drone slower. So I had to work on movement patterns to reduce unnecessary actions and improve efficiency.

## Learnings

I learned some techniques to improve the drone's efficiency moving through each tile in a more systematic way by making the loop structures better. This helped the drone cover every tile without doing extra movements that weren’t needed. I also worked on methods to automate trading and inventory checks, so the drone always had what it needed (like seeds) and used them efficiently while it was running. Working with larger grid sizes helped me understand algorithms better, especially ones that deal with tile-based movement and conditions. This’ll be useful when scaling up to even bigger grids or making more complex patterns later on. Managing seeds and water efficiently became super important too—I learned how to cut down on unnecessary trades and make sure the drone wasn’t wasting resources, which helped to avoid downtime. Testing and debugging was also really important as the code got more complicated with nested loops and conditions. I got better at spotting and fixing issues, making the drone more reliable on bigger grids. Working on the 6x6 grid also showed me how important scalable algorithms are. I used get_world_size() and loops that can adapt, so it’ll be easier to adjust the code for even larger grid sizes if I need to.

## References

1. [Resource 1 Youtube](https://www.youtube.com/watch?v=-hdhyKf2aN8&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=1)
2. [Resource 2 Youtube](https://www.youtube.com/watch?v=VyOFQ8rrPGM&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=2)
3. [Resource 3 Youtube](https://www.youtube.com/watch?v=yK8fcRk6pBA&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=3)
4. [Resource 4 Youtube](https://www.youtube.com/watch?v=hp5XZy6HVl8&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=4)
5. [Resource 5 Youtube](https://www.youtube.com/watch?v=3M32udDt4uU&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=5)
6. [Resource 6 Youtube](https://www.youtube.com/watch?v=JgsFGppJtsc&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=6)
7. [Resource 7 Youtube](https://www.youtube.com/watch?v=r7jnecHDlg0&list=PLateWiNrGEtoIy8aeWse6dQOCToetjXJg&index=7)