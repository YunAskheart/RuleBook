# Sequences, Phases, Queues, Resolution

# 流程、时点、队列、处理

Definition: Player Actions are actions a player chooses to take on their turn while nothing is happening, such as attacking, playing a card, using your Hero Power and ending your turn.  
定义：玩家动作是玩家在空闲点能发起的动作，如攻击，使用一张牌，使用英雄技能及结束回合。

Definition: A Sequence is what begins when a Player Action is taken. A Sequence consists of one or more Phases, that are resolved in order.  
定义：流程是从玩家动作作为开始产生的一系列结算步骤。一个流程包含一个或多个依次结算的时点。

Definition: Phases are surrounding blocks created whenever one or more triggers/Events are raised. When the outermost Phase resolves, Hearthstone will run several Steps, including processing Deaths and updating Auras.  
定义：时点是当一个或更多的触发技/事件发起的时候创造的环绕区间。当最外层的时点结算完毕，炉石传说会发起一些步骤，包括死亡处理和光环更新。

Hearthstone splits Turns into Sequences.  
炉石传说将回合分为若干流程。

Player Actions (such as Combat, playing a card and ending the turn) form a Sequence of one or more Phases.  
玩家动作（例如战斗，使用牌，结束回合）会形成一个有一个或多个时点的流程。

Examples  
例子结算
结算
Sending a Character to attack another character creates a Sequence of two Phases - "Preparation" and "Attack".  
让一结算色攻击另一个角色会创造一个拥有两个时点-“准备”和“攻击”的流程。

Whenever a minion is summoned, a Sequence immediately begins with an "On Summon" and ends with an "After Summon" Phase.  
当一个随从被召唤时，会创造一个从“召唤时”开始到“召唤后”结束的流程。

Definition: An Event is any change in the game state. For example: Damage Event, Heal Event, Death Event, etc. (Additionally, all Phases have an associated Event(s).)  
定义：事件是指游戏状态的任意改变。例如：伤害事件，治疗事件，死亡事件，等等（额外地，所有时点都有相联系的事件）。

Definition: A Trigger is something that reacts to an Event, i.e. triggered effects, Secrets and Deathrattles.  
定义：触发技是指一些对事件的响应，如，触发效果，奥秘，亡语等。

Definition: Resolving means playing out all related consequences, one at a time.  
定义：结算意为完成所有相关的结果，一次一个。

Rule 1a: A Phase, trigger or Event is only resolved when all of its consequences are resolved.  
规则1a：一个时点，触发技或事件仅当它们所有的结果被结算后才算被结算完。

Rule 1b: When resolving simultaneous events, Hearthstone must resolveone event before it begins resolving the next.  
规则1b:当结算复数事件时，炉石传说必须在结算下一个之前先结算完第一个。

Rule 1c: Death and Auras are not checked during the standard resolution of Events.  
规则1c：死亡和光环不会在标准的结算事件中检查。


The process of resolving an event is similar to a depth-first search - Imagine every circle being an event and every arrow representing a trigger starting a new event. The numbers on each circle are the order Hearthstonewould resolve them in.  
结算一个事件的过程类似于深度优先搜索-想像每个圆是一个事件且每个箭头代表触发一个新的事件。每个圆的数字代表炉石将会结算它们的顺序。

When multiple events are awaiting resolution, the need to resolve an event before starting the next is a depth-first resolution. (If multiple events could be partially resolved, that would be breadth-first).  
当复数事件等待结算时，要在结算下一个事件前先结算前一个的是深度优先结算。（如果多个事件能局部解决，那将是广度优先）

The moment a new trigger/Event is raised, Hearthstone begins to resolve it and immediately begins exploring its consequences, before resolving those remaining for the current trigger/Event. When a trigger/Event isresolved,Hearthstone picks up where it left off.  
 当一个新的触发技/事件发生时，炉石传说会先结算它并在结算那些还在等待的触发技/事件前，先展开它的结果，当一个触发技/事件被结算后，炉石会从它原先的地方继续结算。

Examples  
例子

You Flamestrike a Dragon Egg and Knife Juggler. The Dragon Egg immediately spawns a Black Whelp, causing the Knife Juggler to trigger and throw a knife (even though both are mortally wounded, because death is not checked during resolution). There are no further consequences, so the phase is resolved. Hearthstone kills both minions, removing them from the board.  
你对一个龙卵和飞刀杂耍者使用烈焰风暴。龙卵会立刻召唤一个黑色雏龙，导致飞刀杂耍者触发并掷出一把刀(即使它们都受到致命伤，因为在结算时并不会检查死亡）由于没有更多的结果，所以时点结算完毕。炉石杀死所有随从，从场上移除它们。

Definition: A Queue is a sequential container where multiple simultaneous triggers or Events are held.  
定义：一个队列是存放多个同时点触发技或事件的有序容器。
Rule 2a: When we start to resolve a Phase or Event, A Queue is created and filled with all triggers that can respond, in order of play.  
规则2a：当我们开始结算一个时点或事件时，会创造一个按使用顺序填充所有触发技的队列。
Rule 2b: If multiple events are considered simultaneously (such as damage, healing, Deaths or 'return to hand' effects) they are Queued by order of play, then for each, triggers are Queued by order of play (as per Rule 2a).  
规则2b：如果多个事件会被同时考虑（如伤害，治疗，死亡，或‘回到手牌’效果等）它们会按照使用顺序排列，然后，对于每个事件，触发会按照使用顺序排列（按照规则2a）。
Rule 2c: A Queue becomes immutable once Hearthstone starts to resolve the first entry in it. No new entries can be added to the Queue after this point.  
规则2c：一旦炉石开始解决一个队列的第一个项目，该队列将不可改变。新触发技不能在这个时点后被加入队列。

Order of play means the order the Entities each Event/trigger is associated with entered play, from oldest to newest.  
使用顺序意为与事件/触发技相联系的实体进入游戏的顺序，从最早的到最新的。
Minions, Heroes, Weapons, Secrets, attached Enchantments and added Deathrattles are all Entities, and all exist in the same order of play list together.  
随从，英雄，武器，奥秘，结界和结附的亡语都是实体，都存在于相同的使用顺序列表。  
Minions and Secrets summoned while resolving an Event cannot respond to Events that are in the middle of resolution, because their associated Queues are now immutable. However, they can Queue on any later Phases and Events created.  
在结算一个事件中召唤的随从和奥秘不能在该事件结算中触发效果，因为与此事件相关联的队列已经不可更改。然而，它们能在以后的时点和新生成的事件中加入队列。

Examples:  
例子：  
If you trade your Sylvanas Windrunner into your opponent's, the oldest Sylvanas will have its Deathrattle activate first.  
如果你用你的希尔瓦娜斯·风行者攻击你的对手的希尔瓦娜斯·风行者，旧的希尔瓦娜斯·风行者将会先触发它的亡语。  
If you Arcane Explosion three Grim Patrons and a Frothing Berserker, all the damage occurs, then each "On Damage" Event is resolved based on the order of play.  
如果你对三个恐怖的奴隶主和一个暴乱狂战士使用魔爆术，所有的伤害同时发生，然后每个“受到伤害时”事件会按照随从的使用顺序依次结算。  
If a Mad Scientist dies and plays Duplicate, Duplicate does not get triggered. That Death Event has already begun resolving before the Duplicate entered play. If a second minion also died after Mad Scientist, the Duplicate was in play and thus can trigger.  
如果一个疯狂的科学家死亡且其亡语将复制置入战场，复制将不会触发。此死亡事件在事件进入游戏前已经开始结算。如果第二个随从也在疯狂的科学家后死亡，复制已经进入游戏因此可以触发。  
If you play a spell, Troggzor the Earthinator summons a Burly Rockjaw Trogg. The Burly Rockjaw Trogg does not trigger from the same spell because the consequences of playing the spell have already begun resolving.  
如果你使用一个法术，颤地者特罗格佐耳会召唤一个石腭穴居人壮汉。该石腭穴居人壮汉不会因此法术而触发，因为“使用法术时”已经开始结算。  

Notes and exceptions:  
注意和例外：  
Some triggers have a Priority that supersedes order of play and always triggers earlier or later. One example is Redemption which always Queues last.  
一些触发有自己的优先度取代使用顺序，总是最早或最晚触发。一个例子即救赎总是排列在队尾。  
Baron Rivendare also cannot add additional triggers once a Queue has been populated.   
一旦一个队列已经完成，瑞文戴尔男爵就不能增加额外的触发。  
Mechanics that play a minion from your hand or from your deck have a bug that makes the new minion the oldest, not newest. (For more information, see the Force play section.)  
从你的手上或卡组直接使用一个随从的机制有一些bug会让新的随从变成最老的，而非最新的。（更多信息参阅强制使用章节）

Rule 3: Once a Phase begins, nested Phases with their own Queues may start and end inside of it, but only the outermost Phase ending initiates the Death Creation Step.  
规则3：一旦一个时点开始结算，有着各自队列的嵌套的时点会在其内部开始和结束，但是只有最外层的时点结束后才会开始死亡创造步骤。  

This means that you will NEVER see an Entity be killed in the middle of a Phase, no matter how complexly nested it becomes.  
这意味着你不可能看见一个实体在一个时点中间被杀死，无论嵌套多么复杂。  
This also means that even though Sequences like summoning a minion have many Phases, if it occurs as a consequence of another Player Action instead of being due to playing a card, the entire thing happens before any Deaths occur.  
这也意味着虽然一个流程如召唤一个随从可能包含许多时点，如果它作为结果出现在另一个玩家动作而不是使用牌，这整个流程会在任何死亡发生前结算完。  

Examples:
例子：  
You play Knife Juggler then Dr. Boom. When Dr. Boom's Battlecry (a Phase) begins, Boom Bots are summoned, and each one triggers the Knife Juggler to throw knives at enemy minions. Even though minion summoning is a Sequence of multiple Phases, we are already inside of a Phase, so the entire Battlecry remains inside of one Phase, rather than starting and stopping. Finally when the Battlecry resolves, Deaths are processed and the Deathrattles go off.  
你使用飞刀杂耍者和砰砰博士。当砰砰博士的战吼（一个时点）开始后，砰砰机器人被召唤，然后每个触发飞刀杂耍者向敌方随从掷出飞刀。虽然随从召唤是由多个时点组成的流程，但是这些已经在一个时点里，所以整个战吼持续在一个时点里，而不是开始或结束。最后战吼结算完毕，死亡事件开始生成且亡语开始生效。  
You play three Unstable Ghoul. Your opponent plays an Acolyte of Pain, damages it to 1 Health and casts Flamestrike. All three Unstable Ghouls's Deaths are considered in one Phase, meaning that the Acolyte of Pain is hit, triggered and draws three cards, despite being mortally wounded after the first Deathrattle. Finally the Phase ends and the Acolyte of Pain is killed.  
你使用三个蹒跚的食尸鬼。你的对手使用苦痛侍僧，将它伤害到生命值为1，然后施放烈焰风暴。所有三个蹒跚的食尸鬼的死亡在同一个时点，意味着苦痛侍僧会受到伤害，触发并抽三张牌，尽管它在第一次亡语后已经受了致命伤。最后时点结束，苦痛侍僧被杀死。  
Your opponent has a Cult Master and Novice Engineer both at 1 Health. You play a Mad Bomber, and both are reduced to 0 Health during the Battlecry Phase. Regardless of order of play, and regardless of the order the minions are mortally wounded by the bombs, the Cult Master cannot draw a card from the Novice Engineer dying because both deaths occur simultaneously after the Phase ends.  
你的对手使用一个诅咒教派领袖和工程师学徒都只有1生命值。你使用疯狂投弹者，对方所有随从的生命值在战吼时被减少至0。无论使用顺序如何，诅咒教派领袖都不能因工程师学徒死亡而触发抽牌效果，因为它们在时点结束后同时死亡。  
Exceptions:
例外:
There are three effects in the game that break this rule and kill minions in the middle of a Phase. For more information, see the Forced Death Phase section.  
游戏中有三个效果打破了这条规则而在一个时点中杀死随从。详情参阅强制死亡章节。  

Rule 4a: After the outermost Phase ends, Hearthstone does an Aura Update (Health/Attack), then does the Death Creation Step (Looks for all mortally wounded (0 or less Health)/pending destroy (hit with a destroy effect) Entities and kills them, removing them from play simultaneously), then does an Aura Update (Other). Entities that have been removed from play cannot trigger, be triggered, or emit auras, and do not take up space.  
规则4a：在最外层的时点结束后，炉石会进行一次光环更新（攻击力/生命值），然后开始死亡创造步骤（寻找所有受了致命伤（生命值为0或更低）/确定要消灭（被消灭效果命中）的实体并杀死它们，将它们从场上清除），然后进行一次光环更新（其他）。已经从场上移除的实体不能触发，被触发，或者发出光环，且不占用空间。  
Rule 4b: As a result of the timing of the two different Aura Updates, Health from lost auras are not recalculated following the Death Creation Step, but all other effects of Auras stop immediately.  
规则4b：作为两次不同时间光环更新的结果，失去光环不会导致生命值在死亡创建步骤后重新计算，但所有其他光环效果会立刻停止。  
Rule 4c: The full list of Auras that are known to update in Aura Update (Other) (excluding Solo Adventure-only content) is as follows: Baron Rivendare, Auchenai Soulpriest, Brann Bronzebeard, Mal'Ganis's Immune effect, Prophet Velen.  
规则4c：已知会在的光环更新（其他）（不包括冒险模式专属卡牌）更新的光环全列表为：瑞文戴尔男爵，奥金尼灵魂祭司，布莱恩·铜须，玛尔加尼斯的免疫效果，先知维纶。  
Rule 4d: Enchantments apply and modify Health/Attack/Mana costs the moment they are attached. However, during Aura Update (Health/Attack), the Enchantment List is re-processed and Health/Attack Auras, having a priority later than Health/Attack Enchantments, will be moved to the end of the Enchantment List during this timing. (However, Mana Cost Auras have no special priority compared to Mana Cost Enchantments.)  
规则4d：结界在结附时生效并修改生命值/攻击力/法力值消耗。然而，在光环更新（生命值/攻击力）时，结界列表会重新处理，且生命值/攻击力光环，比生命值/攻击力结界有较低的优先级，会被移至结界列表的最后。（然而，法力值消耗光环与法力值消耗结界相比没有特别的优先级。）  
When a minion is played, its Aura is sent for the first time before the Battlecry Phase. When a minion is summoned or stolen, it does not start emitting its aura until the outermost Phase ends.  
当一个随从被使用时， 它的光环会在战吼时前发出。当一个随从被召唤或被窃取，它不会立刻发出它的光环，而是等到最外层的时点结束才生效。   
Until the moment it is removed from play, the Entity can be brought back from 0 or less Health by healing or Health buffs, and still shares auras. This is important when multiple minions are attacked simultaneously, or when a hero dies in the same Sequence as minions with Deathrattles.  
直到一个实体被移出游戏前，它可以从0或更低的生命值被治疗或生命值增益救回，且光环持续生效。这在多个随从同时被攻击，或一个英雄在和亡语随从相同的流程中死亡时非常重要。  
If you kill a minion with an aura and a minion with a Deathrattle simultaneously, non-Health effects of the aura are not active during the following Death Phase because the minion is removed from play. However, Health effects of the aura will be active, because Hearthstone does not recalculate Health changes after the minions are killed. However, a health-granting aura such as Mal'Ganis can save a minion from dying, even if it enters play the same Phase the other minion was mortally wounded, because the aura recalculation is done before the Death Creation Step.  
如果你同时杀死一个有着光环的随从和一个有亡语的随从，光环的非生命值效果不会在之后的“死亡时”生效，因为随从已经从场上移除。然而，生命值效果的光环将保持有效，因为炉石传说不会重新计算生命值变化两次。然而，一个生命值增加的光环如玛尔加尼斯可以将一个随从从死亡线拯救，甚至它在其他随从受致命伤的时点进入场上，因为光环更新（生命值/攻击力）会在死亡创建步骤前进行。  
Auras are not recalculated at any point in the middle of a Phase, including due to minions entering/leaving play and due to minions being stolen.  
光环不会在一个是时点中的任何时候更新， 包括随从的进入、离开和被窃取。  
Some auras in the game have a higher Priority than others. This means that order of play does not matter if one aura's Priority is simply higher. For example, Summoning Portal's aura always comes first (meaning also having a Mechwarper makes Harvest Golems cost 0 mana, regardless of play order) and Lightspawn's aura always comes last.  
一些游戏中的光环会比其他有着更高的优先级。这意味着在一个光环的优先级高于另一个时使用顺序不再重要。例如，召唤传送门的光环总是第一个生效，（意味着同样拥有机械跃迁者可以使麦田傀儡的法力值消耗为0，无论使用顺序如何）光耀之子的光环总是最后生效。  
Despite not visually updating, enchantments take effect the moment they are created.  
尽管不在视觉上更新，结界在他们被创造的时刻立即生效。  

Examples:  
例子：  
You play a Stormwind Champion, Explosive Sheep and Mana Wyrm. You damage the Champion and Sheep to 1 Health, with the Mana Wyrm at 4 Health (current and maximum). You play Cone of Cold, simultaneously killing and removing from play the Champion and Sheep. Because only non-Health effects of auras are recalculated after the Death Creation Step, in the following Death Phase, the Mana Wyrm goes from 4 Health to 2, not 3 to 1, and ends as an x/2 instead of an x/1.  
你使用一个暴风城勇士，一个自爆绵羊和法力浮龙。你将暴风城勇士和自爆绵羊伤害到1生命值，且法力浮龙4生命值（当前及最大值）。你使用了冰锥术，同时杀死了暴风城勇士和自爆绵羊并将它们从场上移除。因为只有光环的非生命效果会在死亡创建步骤后重新计算，在之后的死亡时中，法力浮龙从生命值4减少至2，而非从3减少至1，随后以x/2的状态结束而不是x/1。  
You play an Auchenai Soulpriest and a Zombie Chow, damage the Auchenai Soulpriest to x/4 and then cast Circle of Healing. After the Spell Text Phase ends, both the Soulpriest and Zombie Chow are killed and removed from play. Because non-Health effects of auras end following the Death Creation Step, the Zombie Chow heals your opponent for 5, instead of damaging them for 5.  
你使用一个奥金尼灵魂祭司和一个肉用僵尸，将奥金尼的灵魂祭司伤害到x/4，然后使用一个治疗之环。在法术生效时结束后，奥金尼灵魂祭司和肉用僵尸都被杀死并从场上移除。因为光环的非生命效果会在死亡创建步骤后结束，肉用僵尸将为你的对手恢复5点生命值，而不是造成5点伤害。  
You have a Cult Master and a Bloodfen Raptor. Your opponent plays Flamestrike. The Phase in which the spell is cast resolves, and both minions are killed simultaneously. The Cult Master cannot trigger on the Bloodfen Raptor's Death because it is removed from play at the same time.  
你有一个诅咒教派领袖和一个血沼迅猛龙。你的对手使用烈焰风暴。在法术生效时结算完后，所有随从被同时杀死。诅咒教派领袖不能因血沼迅猛龙的死亡而触发因为它们被同时从场上移除。  
Your hero is at 2 Health and attacks a Zombie Chow with his Fiery War Axe. You and the Zombie Chow die and are removed from play - it is too late for the Zombie Chow's Deathrattle to save you, and you lose the game. Similarly, if you suicide into an Abomination, the Deathrattle of which kills a Zombie Chow, you are already dead and gain no healing.  
你的英雄处于2点生命值且用炽炎战斧攻击肉用僵尸。你和肉用僵尸同时死亡和从场上移除——僵尸用它的亡语救你太晚了，从而你输了这场游戏。类似的，如果你通过攻击憎恶自杀，憎恶的亡语杀死了肉用僵尸，你已经死去因而不会得到治疗。  
Your hero is at 5 Health. You cast Hellfire against an enemy Leper Gnome and Zombie Chow. Both enemy minions die simultaneously, and regardless of order of play, you are hurt for 2 Health and healed for 5 Health, ending at 5 Health once more before Hearthstone checks for new Deaths.  
你的英雄处于5点生命值。你对敌方的麻疯侏儒和肉用僵尸施放地狱烈焰。所有敌方随从同时死亡，无论使用顺序如何，你都会受到2点伤害和恢复5点生命值，然后在炉石检查死亡前以5点生命值结束。  
You play an Abomination and Mal'Ganis (order irrelevant), weaken both to 3 Health and cast Hellfire. The Hellfire does not damage you, but mortally wounds both minions. After the Spell Text Phase ends, both minions are removed from play and you stop being Immune, so when the Abomination's Deathrattle goes off you take 2 damage.  
你使用一个憎恶和玛尔加尼斯（顺序无关紧要），都被伤害到3生命值，然后你使用地狱烈焰。地狱烈焰不会对你造成伤害，但对所有随从造成致命伤。在法术生效时结束后，所有随从从场上移除然后你结束免疫状态，故当憎恶的亡语生效时，你会受到2点伤害。  
You have a Knife Juggler and Haunted Creeper, and your enemy has Mal'Ganis at 1 Health and a 1/1 Imp buffed to 3/3 by the Aura. You attack the Haunted Creeper into Mal'Ganis, and both Die and are removed from play. However, following the Death Creation Step, the Health effects of Auras that have left play are not immediately recalculated. Thus, as Haunted Creeper's Deathrattle triggers, and two knives are thrown at the Imp, it is still a 3/3 and reduced to 3/1. Finally, auras are recalculated again, and the Imp survives as a 1/1 instead of dying.  
你有一个飞刀杂耍者和鬼灵爬行者，你的对手有生命值为1的玛尔加尼斯和一个1/1被光环增益至3/3的小鬼。你用鬼灵爬行者攻击玛尔加尼斯，双方都死亡并从场上移除。然而，在死亡创建步骤，已经移除的光环的生命值效果不会立刻重新计算。因此，当鬼灵爬行者的亡语触发时，两个飞刀将被掷向小鬼，它仍旧是3/3故减少至1/3。最后，光环重新计算，小鬼以1/1状态存活而非死亡。  
You have a Stormwind Champion and a damaged 5/1 minion and Redemption is in play. Your opponent casts Fireball on your Stormwind Champion, reducing it to 0 Health. Because we run Aura Update (Health/Attack) before the Death Creation Step, Stormwind Champion's aura is still in effect during the following Death Phase, where Redemption triggers and summons a new 6/1 Stormwind Champion. In the next Aura Update (Health/Attack) the 5/1 minion remains a 5/1 minion because as far as Hearthstone is concerned, the aura never left or got added again. (If there was a timer at which the aura was found to be missing, it would have been dropped to a 4/1, then buffed to a 5/2.)  
你有一个暴风城勇士和一个受伤的5/1随从和使用中的救赎。你的对手对你的暴风城勇士施放火球术，将其生命值减少至0。因为我们在死亡创建步骤前进行光环（生命值/攻击力）更新，暴风城勇士的光环在后面的死亡时仍旧生效，死亡时救赎触发并召唤一个新的暴风城勇士。在下一个光环（生命值/攻击力）更新时，5/1随从仍旧是5/1随从因为对炉石而言，光环从未消失或重新加上。（如果存在一个时段光环被发现失去，该随从会被降至4/1，然后被增益至5/2。）  
If you have an Auchenai Soulpriest and a Zombie Chow and your opponent has a Voidcaller that will force play Mal'Ganis and you play Circle of Healing, regardless of order of play, Auras such as Mal'Ganis's Immune effect do not update mid-Phase, so your opponent's Hero will take 5 damage from the Zombie Chow Deatrhrattle.  
如果你有一个奥金尼灵魂祭司和一个肉用僵尸且你的对手有一个将会强制召唤玛尔加尼斯的空灵召唤者，你是用治疗之环，无论使用顺序如何，光环如玛尔加尼斯的免疫不会在时点中更新，故你的对手的英雄会受到肉用僵尸亡语造成的5点伤害。  

Rule 5: While characters cannot be killed in the middle of a Phase, 'negative' (damaging/destroying/hindering/misdirecting) triggers ignore mortally wounded characters. Also, Secrets abort if their specific target is mortally wounded or they otherwise cannot meaningfully trigger. However, 'beneficial' (healing/buffing) triggers count mortally wounded, and AoE effects count mortally wounded.  
规则5：角色不能在一个时点中间被杀死，‘负面’（伤害/消灭/妨碍/误导）触发技忽略受了致命伤的角色。当然，当奥秘的特定目标受了致命伤或不再是合法目标时，奥秘也会取消。然而，‘正面’(治疗/buff)触发技会计入受了致命伤的角色，且AoE效果会计入受了致命伤的角色。  
Rule 5b: An exception to Rule 5, Lightwell ignores mortally wounded minions.  
规则5b：规则5的一个例外，光明之泉无视受了致命伤的随从。

Knife Juggler is an example of a negative trigger that ignores mortally wounded characters. If all targets are mortally wounded, it aborts.  
飞刀杂耍者是一个负面触发技的例子，它忽略受了致命伤的随从。如果所有目标都受了致命伤，它的触发技会取消。  
Freezing Trap is an example of a Secret that aborts if its target is mortally wounded. Similarly, Noble Sacrifice aborts if there is no space for the Defender it would summon, and thus no way to trigger.  
冰冻陷阱是一个奥秘的例子，如果目标受了致命伤，它会取消。  
Dark Cultist's Deathrattle is an example of a positive trigger that considers mortally wounded characters valid!  
黑暗教徒的亡语是一个正面触发技的例子，它会考虑受了致命伤的角色！  
Examples:
例子：  
If you play two Knife Jugglers and then Unleash the Hounds, no enemy will be reduced to lower than 0 Health by a knife, because Knife Juggler is a damaging trigger.  
如果你使用两个飞刀杂耍者然后使用关门放狗，没有敌人会被飞刀减至低于0的生命值，因为飞刀杂耍者是一个伤害型触发技。  
If you play Explosive Trap then Freezing Trap, your enemy's Novice Engineer attacking into it will trigger the Explosive Trap and be reduced to -1 Health. The Freezing Trap is a hindering Secret and thus aborts having no target it considers valid.  
如果你使用爆炸陷阱然后使用冰冻陷阱，敌方工程师学徒攻击你的英雄会触发爆炸陷阱然后被减至-1生命值。冰冻陷阱是个妨碍型奥秘因而它会因无合法目标而取消。  
Misdirection and Clumsy effects like Ogre Brute, being hindering triggers, pretend mortally wounded characters don't exist and can't redirect an attack onto one.  
误导和健忘效果如食人魔步兵，作为妨碍型触发技，会忽略受了致命伤的随从而不会攻击它们。  
If you play an Explosive Sheep, Dark Cultist and Chillwind Yeti and your opponent plays Flamestrike - First, the Explosive Sheep and Dark Cultist's Deaths are resolved in a single Phase. First, the Explosive Sheep goes off and mortally wounds the remaining Chillwind Yeti - but the Dark Cultist doesn't ignore mortally wounded characters, and the Chillwind Yeti is buffed and survives as a 4/2.  
如果你使用依次使用自爆绵羊，黑暗教徒和冰风雪人，你的对手使用烈焰风暴——自爆绵羊和黑暗教徒的亡语会在一个时点结算。首先，自爆绵羊生效而对剩下的冰风雪人造成致命伤，但黑暗教徒的效果不会忽略受了致命伤的角色，故冰风雪人会被增益至4/2存活。  
If you play an Auchenai Soulpriest, Acolyte of Pain buffed to 1/5 and two Unstable Ghouls, then play Circle of Healing (killing both Unstable Ghouls and reducing the Acolyte of Pain to a 1/1), in the following Death Phase the two Unstable Ghouls, by Rule 5, will both hit the Acolyte of Pain and cause it to draw a card, finally being removed from play as a 1/-1 with 3 total cards drawn.  
如果你使用奥金尼灵魂祭司，被增益至1/5的苦痛侍僧，和两个蹒跚的食尸鬼，然后使用治疗之环（杀死两个蹒跚的食尸鬼并将苦痛侍僧的伤害成1/1），在接下来的死亡时，由规则5，两个蹒跚的食尸鬼都会对苦痛侍僧造成伤害而导致其抽牌效果触发，最终以1/-1移出场上并总计抽了3张牌。  
If you play a Baron Geddon followed by a Healing Totem, then end your turn, during the End of Turn Phase, Baron Geddon reduces the Healing Totem to 0 Health, then the Healing Totem heals itself for 1, and when we reach the Death Creation Step, the Healing Totem remains alive. This also works, for example, with Imp Master and Healing Totem.  
如果你使用一个迦顿男爵然后召唤治疗图腾，在你的回合结束时，迦顿男爵将治疗图腾的生命值伤害至0，然后治疗图腾将其自身治疗至1，在之后的死亡创建步骤，治疗图腾仍然存活。这也对小鬼召唤师和治疗图腾生效。  

Exceptions:
例外：
While mortally wounded is checked, pending destroy is not! If your opponent's Emperor Cobra (played first) hits your Grim Patron (played second), despite the Poison going off before the Grim Patron triggers, the Grim Patron only checks that it's not mortally wounded - it isn't, and so a new Grim Patron is summoned.  
虽然受了致命伤会被检测，但确定要消灭并不会！如果你的对手的帝王眼镜蛇（先使用）攻击你的恐怖的奴隶主（后使用），尽管毒害效果会在恐怖的奴隶主之前触发，但恐怖的奴隶主仅检测其是否受了致命伤-它并没有，所以一个新的恐怖的奴隶主会被召唤。  
Mirror Entity still triggers if the minion is mortally wounded, for example if Snipe triggered first, and even triggers if the minion is removed from play!  
镜像实体在随从受了致命伤仍旧会触发，例如，狙击先触发了。镜像实体甚至会在目标随从移除游戏后触发！  

Rule 6: Subsequent Phases of a Sequence will not run if a subject is required but is no longer in play. However, this is the only requirement - If the target of the action has some requirements beyond that, the requirements are not re-checked.  
规则6：一个流程中的子时点，如果其条件中的对象不再存在，该时点不会结算。然而，这是唯一的条件——如果该动作的目标有一些其他条件，则这些条件不会再次检测。

Rule 7: If one or more Deaths happened after the outermost Phase ended, a new Phase (called a “Death Phase”) begins, where Deaths are Queued in order of play. For each Death, all Death Event triggers (Deathrattles, on-Death Secrets and on-Death triggered effects) are Queued and resolved in order of play. When this is complete, the Death has been resolved.  
规则7：如果一个或更多的死亡在最外层时点结束后同时发生，一个新的时点（称作“死亡时”）会开始，每个角色的死亡会按使用顺序依次排队。对于每一个死亡，所有死亡事件触发技（亡语，死亡时的奥秘，死亡时的触发技）会依次按使用顺序排队结算。当这些完成后，死亡结算完毕。

Rule 8: A Death Phase can have yet another Death Phase after it. This process repeats forever until no new Deaths occur, and we can finally move on to the next intended Phase in the Sequence.  
规则8：死亡时可能会在结束后生成另一个死亡时。这个过程会重复进行直到没有新的死亡生成，然后才进入流程中的下一个时点。

Rule 9: Finally when the Sequence ends and the player gets control again, Hearthstone checks if the game has ended in a Win, Loss or Draw.  
规则9：当一个流程结束后，炉石传说会检测游戏是否结束，胜利、失败或平局。

Rule 10: Minions and effects have no memory of earlier board state. The moment an event takes place the board state is updated. Whenever a Queue is populated or an effect resolved (or continued), the most up to date board state is used.  
规则10：随从和效果没有之前的状态记忆。一个事件发生的时候游戏状态会随之更新。当一个队列填充完或一个效果结算完后（或持续生效），最新的游戏状态会被使用。

Rule 10b: Triggered effects with a condition do not check their condition until the moment they queue or the moment they trigger (or sometimes both). Again, they have no memory of prior game states, and their condition succeeds or fails based on the current game state.  
规则10b：含条件的触发技只会在它们加入队列或触发（或者都需要）的时候检测条件。它们没有游戏之前状态的记忆，它们的条件是否满足取决于当前的游戏状态。

Death Phases and consequences of Death
死亡时及死亡的后果

Player Action Sequences
玩家动作流程

Start and end of turn  
结束回合  
Now that we know the 10 Rules, we can very simply describe what happens between turns:  
End of Turn Phase: All 'end of turn' Triggers (as well as the special case Shadow Madness) are Queued and resolved.  
回合结束时：所有“回合结束时”的触发技（包括特例暗影狂乱）加入队列结算。
Hearthstone checks for win/loss/draw. The game is a draw if turn 89 (aka Player 1's 45th turn) just ended. It is now your opponent's turn. Hearthstone wears off expired enchantments (like Ice Block's effect and Bloodlust's effect), resets all counters related to 'this turn' (such as Deaths and cards played this turn), fills your opponent's mana, flips which player's weapons are sheathed/unsheathed, flips which player's Secrets are active, unflips your opponent's Hero Power and removes exhaustion from all characters.  
炉石传说检测是否胜利/失败/平局。游戏会在第89回合（玩家1的第45回合）判定为平局。然后是你的对手的回合，炉石传说会移除过期的结界（如寒冰屏障的效果和嗜血的效果），重置所有‘本回合’的计数器（如本回合死亡数和使用的手牌），充满你的对手的法力水晶，翻转每个玩家的武器使其出鞘/入鞘，翻转每个玩家的奥秘，重置的你对手的英雄技能，移除所有角色的疲倦状态。  
Start of Turn Phase: All 'start of turn' Triggers (including Corruption and Nightmare and Competitive Spirit) are Queued and resolved.  
回合开始时：所有“回合开始时”的触发技（包括腐蚀术的效果，噩梦的效果和争强好胜）会被排队结算。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。  
Draw a Card Phase: Your opponent draws one card, and any consequences are resolved now.  
抽卡时： 你的对手抽一张卡， 且所有后果在这里结算。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。  

Playing a spell  
使用法术牌  
When you play a spell, the following Sequence takes place:  
当你使用一张法术牌时，以下流程会发生：  
The card is removed from your hand and enters Play and its Mana cost is paid. If it targets, the target is remembered (and its validity is not checked again).  
该牌从你手上移除并进入场上且支付其法力消耗。如果它取对象，它的对象会被记住 （其合法性将不再检测）。  
On Play Phase: All triggers on playing a card/casting a spell/playing a Secret Queue and resolve here, such as Unbound Elemental, Questing Adventurer, Mana Wyrm, Burly Rockjaw Trogg, Secretkeeper and Violet Teacher. Counterspell also triggers here - Counterspell will not stop triggers in this Phase, but will prevent the Overload and all further Phases and send the spell to the Graveyard. Preparation/Kirin Tor Mage also triggers here.  
使用时：所有在使用牌时/施放法术时/使用奥秘时的触发技会在此排队结算，如无羁元素，任务达人，法力浮龙，石腭穴居人壮汉，奥秘守护者和紫罗兰教师。法术反制也会在此触发——法术反制不会中止该时点的其他触发技，但会防止过载和后面的时点并将法术牌送入墓地。伺机待发和肯瑞托法师也会在此触发。  
Targeting Phase: Dragonkin Sorcerer, Eydis Darkbane and Fjola Lightbane Queue and Resolve here.  
成为目标时：龙人巫师，黑暗邪使艾蒂丝和光明邪使菲奥拉会被排队结算。  
Spellbender Phase: Spellbender queues and resolves here. (the Death Creation Step and Summon Resolution Step is skipped following this Phase.)  
确定目标时：扰咒术会在此排队结算。（该时点后的死亡创造步骤和召唤结算步骤会被跳过）
Spell Text Phase: The entirety of the spell text takes place in one Phase. All triggers to its events are fully resolved. (If it is a Secret, nothing happens here - it already entered play.)  
法术生效时：法术的全部效果会在此一个时点发生。所有此事件的触发技会结算完。（如果是一个奥秘，则此时点无事发生——它已经进入了场上）  
After Spell Phase: Wild Pyromancer, Flamewaker and Djinni of Zephyrs Queue and resolve here.  
使用法术后：狂野炎术士，火妖和西风灯神会排队结算。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。  

Playing a weapon  
使用武器牌  
When you play a weapon, the following Sequence takes place:  
当你使用一张武器牌时，下列流程将会发生：    
The card is removed from your hand and its Mana cost is paid. If it targets, the target is remembered.  
该牌从你手上移除并进入场上且支付其法力消耗。如果它取对象，它的对象会被记住 （其合法性将不再检测）。  
On Play Phase: All triggers on playing a card Queue and resolve here, such as Questing Adventurer, Fel Reaver and Illidan Stormrage.  
使用时：所有在使用牌时的触发技会在此排队结算，如任务达人， 魔能机甲和伊利丹·怒风。  
Equipping Phase: Your old weapon is destroyed and removed from play and your new weapon is equipped. The Battlecry of your new weapon (if any) is resolved. The Deathrattle of your old weapon (if any) is resolved.  
装备时：你的旧武器被消灭及从场上移除且装备你的新武器。你的新武器的战吼（如果有）会在此结算。你的旧武器的亡语（如果有）会在此结算。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。

Playing/summoning a minion  
使用/召唤随从  
When you Play a minion, the following Sequence takes place, which ends early if the minion leaves play (such as due to death):  
当你使用一张随从牌，下列流程将会发生，如果随从在流程中从场上移除（如死亡），流程将会终止。  

The card is removed from your hand and its Mana cost is paid. The card enters Play as a minion, creating a Summon Event and becoming interactible. (Cobalt Guardian and Murloc Tidecaller Queue and resolve before the played minion enters play due to the Pre-Summon Reaction Bug.) If it targets, the target is remembered (and its validity is not checked again).  
该牌从你手上移除并进入场上且支付其法力消耗。该牌进入场上并成为一个随从，创造一个召唤事件，变为可交互状态（钴制卫士和鱼人招潮者会由于预召唤响应BUG在随从进场前排队结算）。如果它取对象，它的对象会被记住 （其合法性将不再检测）。  
On Play Phase: Hobgoblin, Questing Adventurer, Fel Reaver, Unbound Elemental, Tunnel Trogg, Illidan Stormrage and Crowd Favorite Queue and resolve here.  
使用时：大胖，任务达人，魔能机甲，无羁元素，坑道穴居人，伊利丹·怒风和人气选手会在此排队结算。  
(Because of the Summon Resolution Step, Starving Buzzard, One-eyed Cheat, Undertaker and more Queue and resolve for the played minion here. )  
（因为召唤结算步骤，饥饿的秃鹫，独眼欺诈者，送葬者等会在此排队结算。）  
Battlecry Phase: The Battlecry/Combo/Choose One is fully resolved here. (If Brann Bronzebeard was under your control when the Phase began, run Aura Update (Health/Attack) then resolve the Battlecry again.)  
战吼时：战吼/连击/抉择的效果会在此结算。（如果你在战吼时开始时操控布莱恩·铜须，则进行光环更新（攻击力/生命值），然后再次结算战吼。）
After Play Phase: Mirror Entity, Repentance, Snipe, Sacred Trial and Rumbling Elemental Queue and resolve here. (the Death Creation Step and Summon Resolution Step are skipped following this Phase.)
使用后：镜像实体，忏悔，狙击，审判和顽石元素在此排队结算。（该时点后的死亡创造步骤和召唤结算步骤会被跳过）
After Summon Phase: Ship's Cannon, Knife Juggler, and Sword of Justice Queue and resolve here.  
召唤后：船载火炮，飞刀杂耍者和公正之剑会在此排队结算。
Hearthstone checks for winloss/draw.  
炉石传说检测是否胜利/失败/平局。  

If a minion is merely summoned rather than played, it is inside of a larger Phase, so we are currently not processing Deaths, updating Auras or checking for win/loss/draw. The Sequence is now far simpler:  
如果一个随从只是单纯被召唤而非使用，它会处在一个时点中，因而不需要处理死亡，更新光环或检测胜负。这个流程会变得简单很多：  

The card is generated (or moved from your hand/deck if due to a Force Play mechanic) and enters Play, creating a Summon Event and becoming interactible. (Cobalt Guardian and Murloc Tidecaller Queue and resolve before the played minion enters play due to the Pre-Summon Reaction Bug.)  
一张衍生卡将会被生成（如果是通过强制使用机制，则从你的手牌/牌库）并进入战场，创造一个召唤事件并变为可交互状态。（钴制卫士和鱼人招潮者会由于预召唤响应BUG在随从进场前排队结算）。
After Summon Phase  
召唤后  

Minions removed from play during summoning  
随从在召唤时从游戏移除  
A few effects can cause minions to be removed from play after a minion enters play but before its summoning completes, usually by mortally wounding them.  
一些效果能导致一个随从在其召唤事件完成前被移除场上，通常通过对其造成致命伤。  
If the minion being played or the target of its Battlecry is removed, the Battlecry is not canceled, but uses the minion's new position and attributes in the Graveyard instead of its old in play status. Note that when minions are placed in the Graveyard, they are restored to default attributes, including their original maximum Health.  
如果一个随从或其战吼目标被移除场上，战吼不会取消，而是用它们在墓地的位置和状态代替。注意当随从被放置在墓地时，它们会恢复至初始属性，包括它们的最大生命值。  
If the minion being summoned is removed from play before the After Play Phase, each Secret may or may not trigger depending on the secret. For instance Mirror Entity will trigger targeting the minion in the Graveyard, while Snipe will simply not trigger. However, the After Summon Phase is cancelled entirely.  
如果随从在使用后前从场上移除，每个奥秘是否触发取决于奥秘本身。例如，镜像实体会选择墓地的随从触发，而狙击不会触发。然而，召唤后会彻底取消。

Combat  
战斗  
When you order a minion to attack another minion, the following Sequence takes place: (As with other Sequences, if the attacker or defender leaves play for any reason, the current Phase will finish resolving but the Sequence will end early afterwards.)  
当你令一个角色进攻另一个角色时，下列流程会依次触发：（如同其他流程一样，如果攻击者或防御者在中途从场上移除，当前时点结算完后，流程会终止。）  
Combat Preparation Phase: A Proposed Attack Event is resolved. If the defender changes, another Proposed Attack Event is created and placed in this Phase's Event Queue after the current Proposed Attack Event. (It will begin to resolve when the current Proposed Attack Event finishes resolving.) Finally, an Attack Event is resolved. Additionally, the attacker will lose Stealth.  
战斗准备时：一个准备攻击事件会被结算。如果防御者变更，另一个准备攻击事件会被生成并放在该时点队尾。（它将会在当前准备攻击事件结算后开始结算。）最终，准备攻击时结算完毕。额外的，攻击者会在此时失去潜行。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。  
Combat Phase: Damage is dealt simultaneously in the order (attack, counterattack) and resolved. The attacker's weapon loses durability (unless prevented due to the weapon being Immune from Gorehowl's Enchantment). An After Attack Event is resolved even if 0 damage was dealt to the defender.  
战斗时：互相同时造成伤害并按照（攻击，反击）结算。攻击者的武器会失去耐久度。一个攻击后事件会结算（甚至只对防御者造成0点伤害）。  
Hearthstone checks for win/loss/draw.  
炉石传说检测是否胜利/失败/平局。  
The subjects of Combat are the attacker and defender. Even if the attacker or defender (or both) is mortally wounded or leaves play, triggers that ask what the current attacker/defender is will continue to be able to queue and resolve (assuming their other conditions are satisfied.)  
战斗的对象是攻击者和防御者。即使攻击者或防御者（或者两者都）受了致命伤或从场上移除，与当前攻击者/防御者有关的触发技仍会排队结算。

Proposed Attack Event  
准备攻击事件
Triggers on the Proposed Attack Event include those that can change the defender, cause the attacker to become mortally wounded or leave play, and so on.  
准备攻击事件的触发技包括下列：改变防御者，使攻击者受到致命伤或从场上移除等等。  
At the start of resolving a Proposed Attack Event, triggers queue based on the defender at that moment, and will remain in the queue even if the defender changes.  
在准备攻击事件开始时，触发技根据当前防御者排序结算，即使防御者变更也会继续结算。  
When the defender changes, a new Proposed Attack Event is inserted into the Combat Preparation Phase's Event Queue after the currently resolving one. (It will therefore resolve once the current Proposed Attack Event finishes resolving, and therefore use the defender at that point in time.)
当防御者改变时，一个新的准备攻击事件会在当前的结算完后，加入当前的战斗准备时的队列。  
(As a reminder: Queuing conditions are only required to be true when the Event they trigger on starts to resolve, whereas trigger conditions are only required to be true when the trigger resolves.)  
（记住：排队时触发技的条件不需要满足，触发技的条件只需要在结算时满足。）  
A full list is as follows:  
一个完整列表：  

Freezing Trap has a queuing condition of 'attacker is an enemy minion' and a trigger condition of 'attacker is not mortally wounded'.  
冰冻陷阱的排队条件是攻击者是敌方随从，触发条件是攻击者未受致命伤。  
Misdirection has a queuing condition of 'defender is your hero and there is a third, not mortally wounded Character in play' and a trigger condition of 'attacker is in play and - if it is a minion - not mortally wounded, and there is a third, not mortally wounded Character in play'.  
误导的排队条件是防御者是你的英雄且存在第三方未受致命伤的角色，触发条件是攻击者存活且存在第三方未受致命伤的角色。
Explosive Trap has a queuing condition of 'defender is your hero'.  爆炸陷阱的排队条件是防御者是你的英雄。  
Snake Trap has a queuing condition of 'defender is a friendly minion' and a trigger condition of 'board is not full'.  
毒蛇陷阱的排队条件是防御者是一个友方随从且触发条件是我方场上未满。  
Noble Sacrifice has a trigger condition of 'board is not full'.    
崇高牺牲的触发条件是场上未满。  
Vaporize has a queuing condition of 'attacker is an enemy minion and defender is your hero' and a trigger condition of 'attacker is in play and not mortally wounded'.  
蒸发的排队条件是攻击者是一个敌方随从且防御者是你的
Clumsy and Mogor the Ogre cannot trigger on a later Proposed Attack Event if they fail the 50% chance.[168]
Clumsy has a queuing condition of 'attacker is this minion'.
Mogor the Ogre has a queuing condition of 'attacker is a minion'.
Attack Event[edit | edit source]
Triggers on the Attack Event include those that need to occur only once the final defender is known, or those that do not significantly affect the game state. The Attack Event is only resolved if the previous Proposed Attack Event did not change the defender. A full list is as follows:

Truesilver Champion has a condition of 'attacker is your hero'.[169][170][171]
Ice Barrier has a condition of 'defender is your hero'.[172][173][174]
Gorehowl has a condition of 'attacker is your hero and defender is a minion'. It attaches an Enchantment called "Bloodrage" to Gorehowl, which makes Gorehowl Immune and triggers on the After Attack Event.[175][176]
Cutpurse has a condition of 'attacker is this minion and defender is a hero'. It implicitly requires the Cutpurse to still be in play.[177]
Power Word: Glory has a condition of 'attacker is this minion'. It implicitly requires the attacker to still be in play, as it gets detached when the attacker leaves play.[178]
Blessing of Wisdom has a condition of 'attacker is this minion'. It implicitly requires the attacker to still be in play, as it gets detached when the attacker leaves play.[179][180][181]
After Attack Event[edit | edit source]
An After Attack Event is resolved as long as the attack was successful, even if it dealt 0 damage.

(Note that unlike other triggers that go 'after' something, such as Rumbling Elemental and Djinni of Zephyrs, the After Attack Event is resolved in the same Phase, not a later Phase, as the combat damage, meaning death processing and aura updates are not done in-between.)

Triggers on the After Attack Event are as follows:

Gorehowl has a condition of 'attacker is your hero and defender is a minion' and attaches to itself an Enchantment granting -1 Attack.
Gorehowl's Enchantment "Bloodrage" has a condition of 'attacker is your hero' and triggers to detach, ending Gorehowl's temporary Immune state.[182]
Bear Trap has a condition of 'defender is your hero and board is not full'.[183][184]
Foe Reaper 4000/Magnataur Alpha has a condition of 'attacker is this minion'.[185]
