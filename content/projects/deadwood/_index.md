+++
title = "Deadwood"
description = "A MVC board game developed in an Object-Oriented Programming class."
template = "project.html"
draft = false
[extra]
tech = "Java, Swing, XML"
repo = "https://github.com/xNS5/Deadwood"
logo = "deadwood.jpg"
alt = "The deadwood logo, a picture of a person riding a fake horse wearing a 10-gallon hat. Behind them is a backdrop of clouds. "
+++

## About Deadwood

Deadwood is a free board game by [Cheapass Games](https://cheapass.com/free-games/deadwood/). This was a project for my OOP class, done in 
Java and Swing. This was the first large-scale project I've done, and I decided to do it on my own despite it being a group project. 

In Deadwood, each player is an "actor" trying to make a living. Each actor moves from set to set, taking on a role, and attempts to complete the scene to make money. The 
player with the most money at the end of the game is the winner. 

### The Game

#### Game Components

* **Players**: The game supports between 2-8 players.
* **Boards**: There are 4 panels that make up the board. Each panel contains sets for the player to work on, provided their rank is greater than or equal to the role's. Each set contains a section
for a card to be placed, as well as a spot for a user to take a role as an "extra". If a user takes a role, they get a payout on successfully completing the scene regardless whether they take a role as a main
character or as an extra.
* **Cards**: Cards contain a scene, roles, and a budget.
* **Dice**: The dice on the board represent the player game pieces. The side of the dice represents the player's rank, and whether a roll is a success or failure.
* **Money**: Currency, used to upgrade user ranks.
* **Credits**: An alternative form of currency, also used to upgrade user ranks.
* **Counters**: Shot counters. These are values that track how many times an actor has to successfully act before the scene wraps.

#### Movement

* Players who aren't currently working can move from set to set.
* If a player is working a role, whether it's a main role or an extra role, they can only act or rehearse. They're stuck until the role has completed.
* A user can upgrade their rank at the casting office using either credits or money.

#### Working a Role

A player earns money and credits by working roles. The game die determines whether the shot succeeds or fails. A successful shot is when the die rolls a value greater than or equal to the budget. Otherwise, it's a failure.
When a player is working a card, on success the player removes a shot counter and earns two credits. On failure, they earn nothing. If a player is working off the card, on success they earn one credit and one dollar. On failure,
they earn one dollar. Each card has one to three shots which must be completed before the user moves on to another set. 

#### Wrapping a Scene

When the last scene has finished, the scene wraps and the card is removed from the board. For players working a main role, the players role dice equal to the budget of the movie (e.g. 4 dice for a $4 million budget) and the bonuses are distributed
to players from the highest rank role to lowest.

#### Day's End

The day is considered "over" when there is one scene left on the board. All players are moved back to the start ("trailers"), the board gets wiped and new scenes are placed on the board. This repeats until all the days are over.

The formal rulebook can be seen on the [Cheapass Games Website](https://cheapass.com//wp-content/uploads/2016/07/Deadwood-Free-Edition-Rules.pdf).

## Technologies Used

I had some prior experience with Swing for a side project, but it wasn't as complex or detailed compared to Deadwood.
On top of game logic, I needed to design a GUI -- which is a project on its own. In the last Swing project I worked on,
I remember spending a lot of time organizing elements. Given the scale of Deadwood and the number of elements that needed
to be created, I was initially intimidated by the task. Thankfully, [Intellj IDEA](https://www.jetbrains.com/idea/) had a nifty
Swing designer tool which sped up development. Using this tool, I was able to effectively drag and drop elements (buttons, tables, etc.)
without having to go too heavily into editing the Swing code.


<img class="project_demo_desktop" src="/images/deadwood_start.png" alt="A screenshot of the Deadwood game on Desktop. On the left is the game board with each set, the top lists the current player, current day, and how many days the game has total. To the right of the board
are 5 buttons: one for moving the player, working, taking a role, upgrading, and ending the current player's turn. Beneath those buttons is a table listing the player data. The first
player named 'Michael' is rank 1, has 400 dollars, 0 credits, and 0 rehearsal chips. The second player, 'Taco', is rank 1, has 0 dollars, 0 credits, and 0 rehearsal chips."/>

I was familiar with Java enough at the time to where this wasn't an overly challenging project compared to creating a TCP chat client in C,
for example, but there were so many moving parts and rules to test to where the project was more time-consuming than anything.

What made the most sense to me for this project was to use a composition software development design pattern. The way I looked at it,
the board has anywhere from 2-3 sets per quadrant, and 2-8 players per game. Each set has a place for a card and extras. In each card, there are 1-3 roles that a player
can take. I used a singleton design pattern for the board, and created attributes and fields in each class to contain players and cards. In order
to help with the game logic, I created ENUM values which denoted what state the player was currently in (e.g. working, rehearsing, just completed, etc.)

<img class="project_demo_desktop" src="/images/deadwood_move.png" alt="A screenshot of a 2 player Deadwood game. The player 'Michael' is on Main Street working as an extra, and player 'Taco' is selecting a role on a card. To the right of the board the user has the 'Take Role' button selected,
and the application is listing off all the available roles on the set, both on and off the card and their ranks."/>

The static data for this game is contained in two XML files. The board XML files contain information such as neighboring sets, locations, the number of takes, extra roles and associated role information,
and lastly where all of these elements are located on the board (x/y/h/w). The card XMl files list the name of each card, associated images, the scene numbers and descriptions, roles, and their respective locations on the card. 


## Thoughts

The first iteration of this project was a command line version. This command line version was by far the jankiest one I've worked on to date. I didn't have that firm of a grasp as to what needed to be done, or the rules for that matter, so 
it barely worked. The second iteration required the use of a Swing GUI. It was at this point that I realized that this application was largely state driven. Given that a user is doing `x`, they can only do `y` or `z` for example. Once I 
had that logic worked out, effectively rewriting my entire project, the remaining tasks were simple but tedious and repetitive. It reminded me of modifying HTML/CSS on a static webpage -- making small tweaks here and there which either worked or didn't. 

Once I had all the Swing elements created, testing and fixing bugs took up the rest of my time. Due to the chronological nature of the game, I had to play the game at least a hundred times to test out specific features. For example
the end-of-game bonus, upgrading ranks, actions before/during/after completing a scene, and resetting the board after all the cards had been completed. To speed up testing of particular features, I created a test file with prepopulated
data (name, player die color, amount of credits/money, rank) to test out features that I would have otherwise had to play for a long time to test.

There are a few things that I could have done to streamline the code and the overall experience:

* I thought that it would be more efficient to place user objects in the scene objects; when the scene completes, all I would have to do is access the list of users on the particular set
to assign bonuses. 
* I didn't really adhere to any traditional design patterns for this project. I was focused on the mentality that each object contains objects themselves to where I wasn't really able to 
find ways to use the design patterns learned in class.
* Not working this project solo. This project was sizable, and working on it alone was a challenge. I had good reason for working on this alone, and I still think that my decision to work alone 
was justified, but I most likely wouldn't have had to spend as long on it if I worked with another person. 