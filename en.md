# BattleRingCommands
Ring UI for Actor Command on Battle

by @soryu_rpmakermv

-------------------------------------------------

<br>

## 1. Introduction
Though we often comes up with MOG_BattleHUD to use the ring style of actor commands on battles in RPGMV, <br>
it is a comprehensive plugin with alternation of any other UIs, <br>
That causes a risk of conflict with other similar plguins. <br>
Especially, those who are willing to design their own battle UI with various plugins seperately <br>
may be annoyed to be substituted to unnecessary UIs by MOG_BattleHUD. <br>
However, we hardly can find other plugins which implements only the ring actor commands with original sprites <br>
except for MOG_BattleHUD. <br>

This plugin concentrates on just to implement the ring style of actor commands on battles without interfering <br>
other battle UI layouts. It succeeds to mix with other plugins for battle scene design with high affinity. <br>
Only using this plugin is of course insufficient to implement overall of battle systems. <br>
Although, those who wants to develop novel battle scene for their games will have benefit <br>
in terms of testing the combination of plugins and management of battle plugin components.


## 2. Usage

This plugin offers three types of design, **type-Alpha**, **type-Beta**, and **type-Gamma**. <br>
Take either one script file which you prefer to install.

This plugin series has **sample RPGMV project** which encloses every layout type. <br>
You recommend to confirm it to install the plugin.



### 2.1. Layout Type
提供する３つのタイプのスクリプトコードは本質的にほぼ同一であるが、<br>
それぞれ印象の異なるレイアウトとなっている。<br><br>

いずれも、ある円の周上にアイコンを等間隔に配置し、<br>
注視しているアイコンは、拡大縮小を繰り返す形式で強調表示される。

#### 2.1.1 Type-Alpha
<img width="602" alt="alpha" src="https://user-images.githubusercontent.com/64351233/85850933-bb3f3980-b7e8-11ea-9fd1-a2458b05cea7.png">

Type-αは、平面的な円周上にアイコンを配置するスタイルで、<br>
MOG_BattleHudが提供しているデザインに最も近いものである。<br>

コマンドの選択は**左右のキー**で行う。

#### 2.1.2 Type-Beta
<img width="606" alt="beta" src="https://user-images.githubusercontent.com/64351233/85850929-baa6a300-b7e8-11ea-8bb6-640c9e5575dc.png">

Type-βは、横長の楕円型リングコマンドである。<br>
選択中のコマンドアイコンからの距離に応じて、表示サイズを小さく、透明度を導入することで<br>
疑似的な奥行きを感じさせるデザインとなっている。<br>

コマンドの選択は**左右のキー**で行う。

#### 2.1.2 Type-Gamma
<img width="608" alt="gamma" src="https://user-images.githubusercontent.com/64351233/85850924-b8dcdf80-b7e8-11ea-963b-4ec5b09df533.png">

Type-γは、縦長の楕円型リングコマンドである。<br>
Type-βと同様に、選択中のコマンドアイコンからの距離に応じて、表示サイズを小さく、透明度を導入することで<br>
疑似的な奥行きを感じさせるデザインとなっている。

コマンドの選択は**上下のキー**で行う。

### 2.2. Required Sprite materials

Create a directory **./img/SoRBatCom/** to locate following image files for ring actor commands.<br>

#### 2.2.1 For the ring sprite
- Layout.png  (リング本体)
- Layout2.png  (リング本体の上から被せる画像)

画像サイズは実質的に、無制限である。

#### 2.2.2 For command icons

各コマンドに対応するアイコンは以下の形式のファイルを使用する。

```
Com_[XXX].png
```

[XXX]は、**ゲーム内で実際に使用されるコマンドの名称**である。<br>


また、魔法封じ等の状態異常によって<br>
**使用を禁止されるおそれのあるコマンド**は

```
Com_[XXX]_disabled.png
```

というファイルで別途アイコンを用意する。<br>
ゲーム中、使用禁止状態のコマンドのアイコンはこちらの表示に自動的に切り替わる。<br><br>


いずれのアイコンも、画像サイズは実質的に無制限である。<br>
ツクールMVの標準アイコンに使用禁止マークを付加するために、サンプル画像は36x36でデザインしている。<br><br>



Below snapshot shows a constitution of **./img/SoRBatCom/** in case of **Type-Alpha**, 
which assumes to apply to the default new RPGMV project.<br>

<img width="568" alt="sample" src="https://user-images.githubusercontent.com/64351233/85851612-0279fa00-b7ea-11ea-88a7-ea97e3f34bfa.png">




### 2.3. Configuration

デフォルトデザインのものは設定が済んでいるため修正の必要はないが、<br>
独自のUIデザインを適用する場合のために、下記のプラグインパラメータを提供している。<br>

- Ringbase_X-coordinate
- Ringbase_Y-coordinate 


Layout.png を置く座標 (続く画像類の基準位置となる）

- Ringover_X-coordinate
- Ringover_Y-coordinate


Layout2.png を置く座標

- CommandPadd_X-coordinate
- CommandPadd_Y-coordinate


コマンドアイコンの選択中の配置位置（全コマンドアイコンの基準位置）


- CommandName_X-coordinate
- CommandName_Y-coordinate


選択中のコマンド名称の配置位置

- CommandName_Width


選択中のコマンド名称の描画幅（これを基準に名称表示が中央寄せされる）

- RingCommands_Radius


リングコマンド半径<br>
(Type-βおよびγは、数学的都合でUI描画位置がやや難。)


<br><br>

### 2.4. Note

- 当該キャラクターのターンが回ってきて最初にリングコマンドを際の、初期位置は「戦う」（先頭コマンド）に固定
- スキルウィンドウ等を開いてキャンセルした場合は、直前のコマンドを維持
- FTKR_ExBattleCommand.js による追加オリジナルコマンドは **両立する**


## 3. Implementation (Information for Possible Conflict to other plugins)<br>
### 3.1. Overwritten
- **Window_ActorCommand.prototype.setup** 
- **Window_ActorCommand.prototype.numVisibleRows**
- **Window_ActorCommand.prototype.processCursorMove**

これらは、コマンドウィンドウの外観デザインに関する処理であり、<br>
本プラグインを導入しておきながら、ここへ干渉するような他のプラグインを導入することは<br>
通常のゲームデザインとしては不自然である。<br>
（≒一般的な食事1回のメニューに、ご飯とパンを同時に設定することは普通ない。）<br>
よって、競合問題への危惧は無用だと考える。


### 3.2. Extension

- **Scene_Battle.prototype.commandAttack** をはじめとする、コマンド切り替えに関する諸関数

リングコマンドの表示、非表示の切り替えを挿入

- **Scene_Battle.prototype.updateBattleProcess** 

リングコマンドの処理を挿入




### Version Info.
 - ver 1.00  (Jun 26, 2020)   Released!

