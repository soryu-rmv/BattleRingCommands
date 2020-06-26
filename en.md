# BattleRingCommands
Ring UI for Actor Command on Battle

by @soryu_rpmakermv

-------------------------------------------------

<br>

## 1. Introduction
Though we often comes up with MOG_BattleHUD to use the ring style of actor commands on battles in RPGMV, <br>
it is a comprehensive plugin with alternation of any other UIs. That causes a risk of conflict with other<br>
similar plguins. Especially, those who are willing to design their own battle UI with various plugins seperately <br>
may be annoyed to be substituted to unnecessary UIs by MOG_BattleHUD. However, we hardly can find other plugins <br>
which implements only the ring actor commands with original sprites except for MOG_BattleHUD. <br>

This plugin concentrates on just to implement the ring style of actor commands on battles without interfering <br>
other battle UI layouts. It succeeds to mix with other plugins for battle scene design with high affinity. <br>
Only using this plugin is of course insufficient to implement overall of battle systems. <br>
Although, those who wants to develop novel battle scene for their games will have benefit <br>
in terms of testing the combination of plugins and management of battle plugin components.


## 2. Usage

This plugin offers three types of design, **type-Alpha**, **type-Beta**, and **type-Gamma**. <br>
Take either one script file which you prefer to install.

This plugin series has **sample RPGMV project** which encloses every layout type. <br>
You recommend to confirm it to install the plugin. <br>
**(The layout is presented in Japanese, replace your region language for some following settings.)** <br>


### 2.1. Layout Type
Each three layout types are designed by potentially same, <br>
which gives different impression to players. <br>

Every Command icon is aligned on the circumference at regular intervals. <br>
The icon which is currently focused is drawed with emphasis by scaling its sprite.


#### 2.1.1 Type-Alpha
<img width="602" alt="alpha" src="https://user-images.githubusercontent.com/64351233/85850933-bb3f3980-b7e8-11ea-9fd1-a2458b05cea7.png">

In Type-Alpha, icons are aligned on the circumference of a perfect circle, <br>
which is the most similart to the design provided by MOG_BattleHud.<br>

Selection of the command is conducted by using **left and right keys**. <br> 

#### 2.1.2 Type-Beta
<img width="606" alt="beta" src="https://user-images.githubusercontent.com/64351233/85850929-baa6a300-b7e8-11ea-8bb6-640c9e5575dc.png">

In Type-Beta, icons are aligned on the circumference of a elipse whose major axis is horizontal.<br> 
To direct the depth of ring UI, the more far icons from the current focused icon, the smaller they are displayed with opacity.<br> <br> 

Selection of the command is conducted by using **left and right keys**. <br> 

#### 2.1.2 Type-Gamma
<img width="608" alt="gamma" src="https://user-images.githubusercontent.com/64351233/85850924-b8dcdf80-b7e8-11ea-963b-4ec5b09df533.png">

In Type-Gamma, icons are aligned on the circumference of a elipse whose major axis is vertical.<br> 
As Type-Beta, to direct the depth of ring UI, some icons are scaled with opacity.<br> <br> 

Selection of the command is conducted by using **up and down keys**. <br> 


### 2.2. Required Sprite materials

Create a directory **./img/SoRBatCom/** to locate following image files for ring actor commands.<br>

#### 2.2.1 For the ring sprite
- Layout.png  (Ring sprite)
- Layout2.png  (An upper layered sprite for the Ring)

There are no limitation of the size of sprites.



#### 2.2.2 For command icons

You have to prepare images for command icons as folowing format.<br>
(That follows MOG_BattleCommand style.)


```
Com_[XXX].png
```

Here, \[XXX\] is **a terminology for the battle command which used in your game**. <br>




#### 2.2.3 Appendix (You need other plugins to control command enable/disable, not skills)

Additionally, you have to prepare another image for <br>
**commands which supposed to be disabled by some actor states** <br>
(i.e. magic spells are disabled due to spell sealing states.)  as


```
Com_[XXX]_disabled.png
```

to alter icons under appropriate states. <br><br>

Any icons have no limitation for their size.<br>
In the sample project, to create disabled icons based on  default RPGMV icons,<br>
icons are designed as the size of image 36x36. <br><br><br><br>


**!!Appendix!!** <br>
To test this feature anyway, here presents supplementary script <br>
to disable specific commands under skill sealing states. <br>

[IsEnabled_SkillTypes](https://github.com/soryu-rmv/IsEnabled_SkillTypes/blob/master/en.md)

If you have already installed similar plugins, there are no need to use this. <br>
The sample project for SoR_BattleRingCommands involves this plugin. <br><br><br><br>



Below snapshot shows a constitution of **./img/SoRBatCom/** in case of **Type-Alpha**, <br>
which assumes to apply to the default new RPGMV project.<br>

<img width="568" alt="sample" src="https://user-images.githubusercontent.com/64351233/85851612-0279fa00-b7ea-11ea-88a7-ea97e3f34bfa.png">




### 2.3. Configuration

You have no need to adjust following parameters to test the sciript. <br>
But for your original UI design, following parameters help you. <br>

- Ringbase_X-coordinate
- Ringbase_Y-coordinate 


The position to place Layout.png (This is a criteria for following sprite.）

- Ringover_X-coordinate
- Ringover_Y-coordinate


The position to place Layout2.png  

- CommandPadd_X-coordinate
- CommandPadd_Y-coordinate

The position for command icons (the 1st icon)


- CommandName_X-coordinate
- CommandName_Y-coordinate

The position of focusing command's name

- CommandName_Width

Width of displaying name of focusing command (Based on this, centering of name string is conducted.)

- RingCommands_Radius

Radius of ring command<br>
(Note that adjusting the layout with different radius for Type-Beta and Gamma <br>
may cause some difficulties due to its mathematical treatment.)<br>


<br><br>

### 2.4. Note

- The initial command indication is fixed to the first command (Attack in default) when each actor's trun comes.
- When players cancel to back from skill window, and other target selection scenes, the command index is kept. 
- This plugin is **compatible with FTKR_ExBattleCommand.js**. (Available of support for original commands)


## 3. Implementation (Information for Possible Conflict to other plugins)<br>
### 3.1. Overwritten
- **Window_ActorCommand.prototype.setup** 
- **Window_ActorCommand.prototype.numVisibleRows**
- **Window_ActorCommand.prototype.processCursorMove**

They are the process to design a window layout for actor command. <br>
In spite of applying this SoR_BattleRingCommand, importing other plugins to change such function <br>
is unnatural in terms of the game UI design. (Do you have both breads AND rice for a lunch...?) <br>

Thus, it is considered that this overwritten makes no problems for the conflict to other plugins.


### 3.2. Extension

- Functions such as **Scene_Battle.prototype.commandAttack**
- **Scene_Battle.prototype.updateBattleProcess**  for shifting command input

To insert ring command layout and its update during the scene for actor command choice.



### Version Info.
 - ver 1.00  (Jun 26, 2020)   Released!

