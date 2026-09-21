You certainly know the games Lapse: A Forgotten Future and Reigns: her majesty. They are android games.
I want to make a prototype of a similar game.

You play in a medival fantasy rpg setting, similar to dungeons and dragons. You handle requests from nobles, clergy, soldiers, citizens, and other characters while trying to preserve. You can enter taverns, caves or forests to interact with characters, the environment or to pursue a quest.

You can find the description of its core mechanics and gameplay loop in @description_of_game_core_features_and_gameloop.txt

The prototype will be very small. 
It will be coded using plain html and js

For a small prototype, focus on proving the central loop: **create a character → make four-way decisions → change four gauges → trigger consequences → reach an ending → replay with discoveries**.

Gouges:
- **Money:** Wealth, supplies, and ability to pay for services.
- **Status:** Reputation, charisma, political access, and social standing.
- **Magic** Magical energy or connection to the supernatural. Too low blocks magical paths; too high causes arcane overload.
- **Health:** Physical condition and ability to survive wounds, poison, and illness.

This gives the player four different types of pressure: resource scarcity, social consequences, and magical danger/opportunities and physical and mental health. Character classes can interact with them differently without requiring different cards influencing the gauges.

## Prototype scope

The first version should contain:

- One playable region
- Four character classes
- Four races
- A name-selection screen
- Four gauges
- Around 32 cards (8 for each race)
- One main story quest
- Two or three side quests
- A small inventory (maximum of four items that are always displayed under the character/event card)
- A few relationships (observable in a relationship screen)
- Several death conditions
- Eight possible endings (one for each gauge being maxed out or empty)
- A simple local leaderboard
- Replayable runs with unlocked content

Do not attempt a full procedural RPG yet. The prototype should use a curated sequence of cards with branching conditions.

## 1. Character creation

Create a character-creation screen with:

- Class selection:
  - Wizard
  - Rogue
  - Knight
  - Ranger
- Race selection:
  - Human
  - Elf
  - Dwarf
  - Orc
- Name input
- Overview of chosen options
- Confirm button

Each class should have a small mechanical identity. They are not seen by the player but they influence the consequences of cards and what cards are available to a class. Use them as a guide when creating class specific cards.

| Class | Starting advantage | Starting weakness |
|---|---|---|
| Wizard | Better interaction with magic and curses | Less health or money |
| Rogue | Better results in stealth, theft, and traps | Lower status |
| Knight | More health and military options | Higher upkeep or lower flexibility |
| Ranger | Better forest, animal, and travel events | Fewer political options |

Races should provide smaller modifiers so that class remains the main choice.

Possible racial traits:

- Human: balanced stats and better social options
- Elf: improved magic, forest, or perception outcomes
- Dwarf: improved health, mining, crafting, or resistance
- Orc: improved intimidation and combat, reduced initial status

The prototype does not need a complex skill system. Class and race modifiers can simply unlock or alter card responses.

## 2. Main game state

The game needs one central state object containing:

- Character name
- Class
- Race
- Current location
- Current story chapter
- Money
- Status
- Magic
- Health
- Inventory
- Items
- Relationships
- Active quests
- Completed objectives
- Flags recording previous decisions
- Unlocked cards
- Unlocked characters
- Current run length
- Cause of death or ending
- Whether the main quest is complete

Important decision flags might include:

- Helped the village
- Stole from the temple
- Joined the rebels
- Accepted the cursed ring
- Befriended the wolf
- Angered the duke
- Learned the truth about the prophecy

These flags allow later cards to react to earlier choices.

## 3. Gauge rules

Define clear limits for each gauge before creating cards.

For example:

- Money: 0–100
- Status: 0–100
- Magic: 0–100
- Health: 0–100

Possible ending conditions:

- Money reaches 0: cannot pay for food, equipment, or protection
- Status reaches 0: exiled, imprisoned, or politically ruined
- Magic reaches 0: no energy to live
- Health reaches 0: character dies

You can also allow positive extremes to create special endings:

- Money reaches 100: famous for being rich and gets killed in a robbery
- Status reaches 100: crowned, feared, or made into a political threat and dies
- Magic reaches 100: triggers a catastrophic magical overload, dying due to fanaticism
- Certain relationships reach a maximum: unlocks a romance or alliance ending

For the first prototype, use only four gauges. Avoid adding experience points, level-ups, hunger,  armor, and weapon durability.

## 4. Card data system

Cards should be data-driven rather than individually hardcoded. Each card should contain:

- Card ID
- Location
- Speaker or subject
- Description
- Illustration or placeholder image
- Four response labels
- Effects for each response
- Requirements for each response
- Follow-up card or event (if empty a random new card follows)
- Possible item rewards
- Possible relationship changes
- Story flags added or removed
- Whether the card can repeat
- Conditions for appearing
- Conditions for disappearing

A card could conceptually contain responses such as:

- Left: Pay the guard
- Right: Threaten the guard
- Up: Sneak past
- Down: Ask for mercy

Responses should be able to:

- Change one or more gauges
- Add or remove an item
- Start a quest
- Start a fight
- Change a relationship
- Set a story flag
- Unlock another card
- Move the player to another location
- Trigger an immediate ending
- Schedule a delayed consequence

## 5. Four-direction decision input

Implement four input methods:

- Swipe left
- Swipe right
- Swipe up
- Swipe down

The input system should:

1. Detect the selected direction.
2. Check whether the response is available.
3. Display a failure message if a requirement is missing.
4. Apply the response effects.
5. Record the decision.
6. Trigger any follow-up event.
7. Load the next card.

For example, a response might require:

- A flower in the inventory
- At least 30 Status
- The Rogue class
- A specific relationship level
- Completion of an earlier quest
- Magic below a certain threshold

If a response is unavailable, show why:

> You need a flower to give this character a gift.

Do not silently disable choices. Showing the requirement makes the choice feel like part of the role-playing system.

## 6. Locations

Implement a small location system with perhaps four locations:

- Castle
- Tavern
- Forest
- Cave

Each location should have:

- A name
- A visual background or color
- A pool of possible cards
- Specific characters and enemies
- Location-specific quests
- A method for leaving or traveling elsewhere

Examples:

- Castle: nobles, clergy, court politics, military requests
- Tavern: rumors, mercenaries, merchants, romance, gambling
- Forest: animals, rangers, herbs, bandits, ancient magic
- Cave: monsters, treasure, traps, curses, major quest clues

The player does not need free movement. A card can offer a travel decision, or the player can select a destination after completing a special encounter.

## 7. Event categories

Prepare a small set of cards in several categories:

- Noble requests
- Clergy requests
- Soldier encounters
- Citizen problems
- Merchant transactions
- Romantic encounters
- Rival encounters
- Animal encounters
- Enemy encounters
- Environmental events
- Quest discoveries
- Travel events
- Consequences from earlier choices

For the first content pass, create approximately:

- 5 castle cards
- 5 tavern cards
- 5 forest cards
- 5 cave cards
- 5 general travel or character cards
- 5 main-quest cards
- 5 delayed-consequence cards

That gives enough variety to make the loop testable without requiring a huge narrative.

## 8. Combat and dangerous encounters

Do not build a full combat system yet. Represent combat as a card decision.

Example:

> A goblin blocks the cave entrance.

Possible responses:

- Fight
- Negotiate
- Sneak past
- Offer food

The result can depend on:

- Class
- Race
- Health
- Money
- Inventory
- Magic
- Previous decisions

A failed combat response might:

- Reduce Health
- Decrease magic
- Consume an item
- Start a later revenge event
- End the run

This preserves the role-playing feeling while keeping the prototype centered on cards.

## 9. Inventory and mystical items

Implement a small inventory system with 4 possible items.

Suggested prototype items:

- Healing herb
- Enchanted flower
- Ancient key
- Cursed ring

Each item should have:

- Item ID
- Name
- Description
- Icon
- Whether it can be used on a card
- Effects when used

An item can alter a card:

1. Unlock a previously unavailable response.
3. Unlock previously unavailable cards.

Example:

> Without the flower, “Give the partner a flower” is unavailable.  
> With the flower, the response becomes available and improves the relationship.

## 10. Relationships

Start with two relationship tracks:

- Romantic partner
- Rival adventurer

Each relationship can have a value such as -2 to +2:

- -2: hostile
- -1: distrustful
- 0: neutral
- +1: friendly
- +2: devoted or allied

Relationship changes should affect later cards. For example:

- A friendly partner gives the player an item.
- A rival spreads rumors and lowers Status.
- A neglected relationship produces a delayed confrontation.

You do not need dialogue trees yet. A relationship value and a handful of conditional cards are enough.

## 11. Quest and objective system

Create one main quest and several optional objectives.

Main quest:

> Discover why monsters are appearing near the kingdom and locate the source of an ancient curse.

Chapters:

1. Hear rumors in the tavern.
2. Investigate the forest.
3. Discover a strange symbol.
4. Enter the cave.
5. Choose whether to destroy, control, or join the source of the curse.
6. Reach one of several endings.

Optional objectives:

- Save three villagers
- Recover a stolen relic
- Find the missing ranger
- Defeat or befriend a forest creature
- Acquire the cursed ring

Objectives should unlock:

- New cards
- New items
- New endings
- New characters to encounter
- New starting bonuses in later runs

## 12. Delayed consequences

The event system should support consequences that occur several cards later.

Examples:

- Refusing a noble causes guards to search for you later.
- Stealing from a temple causes a cleric to recognize you in the cave.
- Helping a wounded stranger makes them return with a useful item.
- Accepting a cursed ring slowly increases Magic and decreases Health.
- Ignoring a village problem allows monsters to attack it later.

Implement this with a list of pending events. Each pending event can contain:

- Event ID
- Number of cards before activation
- Conditions
- Resulting card
- Result if ignored

This will make choices feel more meaningful than simple immediate stat changes.

## 13. Endings

Create a small ending system where each ending has:

- Ending ID
- Title
- Description
- Conditions
- Whether it counts as death, victory, or another conclusion
- Cause-of-death category, if relevant

Initial endings could include:

- Killed in battle
- Executed after losing Status
- Starved after losing all Money
- Consumed by the curse
- Betrayed by a companion
- Became ruler of the kingdom
- Destroyed the ancient evil
- Joined the ancient evil
- Escaped into the wilderness

The game should check ending conditions after every decision and after every delayed event.

## 14. Replay and unlocks

After a run ends, display:

- Character name
- Class and race
- Number of cards survived
- Final location
- Ending title
- Cause of death or conclusion
- Important decisions
- Newly unlocked content

For replayability, preserve meta-progression such as:

- Discovered cards
- Discovered endings
- Unlocked items
- Unlocked characters
- Completed objectives
- Best survival length
- Total endings found

The player should not retain all power between runs. Unlocking more possibilities is better than simply making the next character stronger.

## 15. Local leaderboard

Since the prototype uses plain HTML and JavaScript, make the leaderboard local-only using browser storage.

Track:

- Character name
- Class
- Race
- Survival score
- Number of decisions
- Ending
- Cause of death
- Date of run

A simple survival score could be:

\[
\text{Score} =
\text{decisions survived}
+ 5(\text{completed objectives})
+ 10(\text{main quest chapters})
\]

Display rankings by:

- Longest survival
- Highest score
- Most endings discovered

A global online leaderboard would require a server and should be excluded from the first prototype.

## 16. Screens and interface

The prototype should have these screens:

1. **Title screen**
   - New game
   - Continue
   - Leaderboard
   - Unlocks

2. **Character creation**
   - Class
   - Race
   - Name
   - Overview of chosen options
   - Confirm

3. **Main game screen**
   - Location (not written but perceived as background image)
   - Card
   - Character or event name
   - Description below card
   - Four response directions
   - Four gauges
   - Inventory bar below card description
   - Show Quest button

4. **Inventory bar**
   - Owned items
   - Item description on hover

5. **Quest and relationship panel**
   - Active objectives
   - Completed objectives
   - Relationship values
   - Important story flags

6. **Ending screen**
   - Ending narrative
   - Cause of death or victory
   - Survival score
   - Unlocks
   - Replay button

## 17. Core functions the JavaScript should implement

Organize the code around these functions:

- `createCharacter()`
- `startNewGame()`
- `loadGame()`
- `saveGame()`
- `drawCurrentCard()`
- `getAvailableCards()`
- `checkCardConditions()`
- `getAvailableResponses()`
- `handleSwipe(direction)`
- `handleResponse(responseId)`
- `applyEffects(effects)`
- `changeStat(stat, amount)`
- `checkStatLimits()`
- `addItem(itemId)`
- `removeItem(itemId)`
- `useItem(itemId, cardId)`
- `changeRelationship(id, amount)`
- `startQuest(questId)`
- `updateQuest(questId)`
- `setStoryFlag(flag)`
- `checkStoryFlag(flag)`
- `scheduleEvent(eventId, delay)`
- `updatePendingEvents()`
- `moveToLocation(locationId)`
- `checkEndingConditions()`
- `showEnding(endingId)`
- `calculateScore()`
- `unlockContent(contentId)`
- `recordRun()`
- `renderStats()`
- `renderInventory()`
- `renderCard()`
- `renderLocation()`
- `renderQuestPanel()`

The most important functions are `handleResponse`, `applyEffects`, `getAvailableCards`, and `checkEndingConditions`. Together, they form the actual game engine.

## Recommended build order

1. Create the HTML layout.
2. Create the four gauges and character state.
3. Add character creation.
4. Add one card with four responses.
5. Implement swipe and button input.
6. Implement stat changes and death conditions.
7. Add several cards using a data-driven format.
8. Add locations.
9. Add inventory and item requirements.
10. Add story flags and delayed events.
11. Add quests and relationships.
12. Add endings.
13. Add unlocks and replay support.
14. Add local leaderboard.
15. Add visual polish and animations.

The first playable milestone should be extremely small: **one class, one location, five cards, four gauges, one item, and two endings**. Once that loop feels enjoyable, expand it to the full character, location, quest, and replay systems.
