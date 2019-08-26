# Combat Routine Creation Guide
If you are experienced with combat routine creation already and are just want a summary of each of the different settings skip to #link section.
This guide will start by introducing the core concepts by demonstrating how to create a basic combat routine explaning how things work along the way.

## 1.Getting Started
Before creating a profile it's first a good idea to get yourself familiar with the core concepts of how a combat routine works. The main purpose of a combat routine is to tell the bot what to do when in combat. 


### The Different Sequences
A combat routine is broken into a set of ordered sequences : ``Buff``, ``Pre-Pull`` and ``Combat``. Each of these have there own specific purpose and conditions under which they will be executed.

*Example low level rogue combat routine*

![alt text](https://i.imgur.com/WlAoCmq.png "Combat Sequences")

Each of the sequences are evaluated and executed in the order listed. In the example above, 'Cheap Shot In Stealth' in the ``Combat Sequence`` will always be evaluated first. If the conditions associated with it are met it will be executed, if not it will move onto the next item in the sequence - 'Garrote'.

#### Buff Sequence
The ``Buff Sequence`` is **only performed out of combat**. The ``Buff Sequence`` should generally be used for ensuring the player has buffs, pets summoned or certain conditions before doing anything else (even moving). For example, a Mage might have 'Summon Water Elemental' and 'Buff Arcane Intellect'.

**Important:** The bot will only move onto the ``Pre-Pull Sequence`` if all the items in ``Buff Sequence`` are done or their conditions are met.

#### Pre-Pull Sequence
The pre-pull sequence is **only performed out of combat, just before pulling an enemy**. A good example usage of this might be stealthing as a rogue and then pickpoketing before entering combat or using a cooldown before pulling an elite mob.

**Important:** The bot will only move onto the ``Combat Sequence`` if all the items in ``Pre-Pull Sequence`` are done or their conditions are met.

#### Combat Sequence
The combat sequence is **only performed when in combat**. This is for the set of actions to perform when actually fighting an enemy. This is most likely where the majority of logic will be.

### Creating a simple ``Combat Sequence``
With this knowledge lets start creating a simple Rogue combat routine. For now we will ignore the ``Buff`` and ``Pre-Pull`` sequences.

1. Open the Combat Routine Editor from the Bot Config Screen.
You can find the combat routine editor in the ``Bot Config Editor`` under the ``Combat Routine`` section :
![alt text](https://i.imgur.com/PNfrnFl.png "Combat Routine Editor")
2. Click the 'New' button.
3. Set the ``PlayerClass`` to Rogue from the dropdown list
4. Open up the sequence editor window by clicking the 'Edit Combat Sequence' button.
5. Add a sequence item by clicking the 'Add' button.
6. At this point you should be displayed a screen something like this : 
![alt text](https://i.imgur.com/6fmD79N.png "Combat Sequence Editor") 

Lots of settings which will be described in later sections, but for now lets just get the bot using the spell 'Sinister Strike'.
1. Give the sequence item a more friendly name than 'Item Name' by setting the ``Name`` property to 'Sinister Strike'.
2. In the ``Action`` properties settings, set property ``Code`` to 'Sinister Strike' and the ``Type`` to ``Cast Spell Name``. Leave the rest of the action properties as they are.
3. Change the ``Range`` property to 3 - this is the distance the player needs to be within the target in order to perform the action.

Once you have done this it should look something like : 
![alt text](https://i.imgur.com/U6Ukhxg.png "Sinister Strike") 

Now save the combat routine by closing the ``Combat Sequence Editor`` window, clicking ``Save As`` and giving it a name.
Example ``.json`` file from following these steps : [1.Tutorial-Rogue-Combat-Routine.json](../1.Tutorial-Rogue-Combat-Routine.json)

In order to use the newly created combat routine, under the ``Combat Routine`` tab of the ``Bot Config Editor`` put in the file path of where you saved it.

#### Testing our new combat routine!
The fun part! Select the 'combat bot' from the bot dropdown and hit the ``Start Bot`` button. If you want the bot to auto attack you must first enable the ``Auto-Attack`` setting found under the ``Combat Bot`` settings tab on the ``Bot Config Editor``.

You should now see the bot using 'Sinister Strike' over and over, not much of a combat routine but it works...

### Adding Conditions
Conditions allow the bot to make decisions about if a action should be executed. 
Lets add another spell to the combat routine, 'Eviscerate'! We want the bot to cast 'Eviscerate' when the player has 3 combo points **and** enough energy to cast it.

1. Open the combat routine editor and load the profile we created in the preivous step using the ``Load`` button.
2. Open the ``Combat Sequence Editor``
3. With the ``Combat Sequence Editor`` open , click the ``Add`` button to add a second sequence item to the list.
4. Go through the steps we did before but this time with a spell name of 'Eviscerate'.
5. Select the new sequence item and click on the ``Condition`` dropdown button - this will open the ``Condition Editor`` :
![alt text](https://i.imgur.com/fTDGpf1.png "Condition Editor") 
6. With the ``Condition Editor`` window open (It has a title of 'Collection Control'), select 'Special Power Condition' from the dropdown and click 'Add' :
7. Update the ``ConditionName`` property to something more friendly - 'When > 3 combo points'
8. Update the ``ConditionValueType`` property to AboveOrEqual.
9. Update the ``Value`` property to 3. Now you should have something like this :
![alt text](https://i.imgur.com/Eu5zj6q.png "Special Power Condition")

Our first condition is done! Now lets add the second one, 'When > 35 Energy'.
Follow the steps above, except this time select the condition type ``Power Condition``.
In the end you should have something like : 
![alt text](https://i.imgur.com/WduAdNG.png "Power Condition")

Once you are done editing the conditions click the ``OK`` button at the bottom of the editor.

Finally , before we are done we need to make the bot first try to 'Eviscerate' before casting 'Sinister Strike'. To do this use the up and down arrows on the ``Combat Sequence Editor`` to change the order of items. You should end up with a combat sequence looking like : 
![alt text](https://i.imgur.com/7G04YHR.png "Power Condition")

Done! Close the editor window and click 'Save As'.
Example ``.json`` file from following these steps : [2.Tutorial-Rogue-Combat-Routine.json](../2.Tutorial-Rogue-Combat-Routine.json)

Run the combat bot again and you should see the bot now using ``Eviscerate`` - you are now a combat routine developer!

## 2. Item Properties

## 3. Conditions

## 4. Action Properties



















