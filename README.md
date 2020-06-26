# BattleRingCommands
戦闘用アクターリングコマンド

by 蒼竜 @soryu_rpmakermv

-------------------------------------------------

<br>

## 1. はじめに
グラフィカルな戦闘画面UI変更スクリプトといえば、MOG_BattleHUDなどが有名であるが、<br>
デザイン全体に干渉する総合的なスクリプトである都合、他プラグインとの競合が危惧される。<br>
特に、他のデザイン系プラグインとの併用での実装を進めていた場合、使用者によっては<br>
過剰な変更と感じられる部分があり、その膨大な設定項目の存在も含めて、乗り換えには一大決心が必要である。<br>
しかし、画像を用いたアクターコマンドの表示表現のみを大きく変更できるプラグインは<br>
せいぜいマップ画面上でのものに限られており、MOG_BattleHUDを利用せざるを得ない状況にある。<br>

このプラグインは、MOG_BattleHUDのような画像ベースにしたグラフィカルな戦闘中のアクターコマンドの<br>
リングコマンド化のみを実現することに特化し、他の機能に一切手を付けないことで、他のデザイン系プラグインとの親和性の<br>
高いものを目指した。本プラグイン単体では戦闘画面デザイン全体としては当然不十分であるが、<br>
他のプラグインとの融合や、各自の細かなスクリプト修正等を含めたオリジナリティの高いデザインを希望する<br>
製作者にとって、システム管理の利便性を向上させるものとして期待できる。


## 2. 使い方
以下に示すように、デザインの基本形として**Type-α**、**Type-β**および**Type-γ**の**いずれか希望する１つを**<br>
異なるスクリプトファイルで導入する。<br>

それぞれのタイプを試験できる**サンプルプロジェクトを提示する**ので、<br>
導入までの流れは、そちらも併せて確認されたい。<br>


### 2.1. レイアウトタイプ
提供する３つのタイプのスクリプトコードは本質的にほぼ同一であるが、<br>
それぞれ印象の異なるレイアウトとなっている。

#### 2.1.1 Type-α
<img width="602" alt="alpha" src="https://user-images.githubusercontent.com/64351233/85850933-bb3f3980-b7e8-11ea-9fd1-a2458b05cea7.png">

Type-αは、平面的な円周上にアイコンを配置するスタイルで、<br>
MOG_BattleHudが提供しているデザインに最も近いものである。<br>

コマンドの選択は**左右のキー**で行う。

#### 2.1.2 Type-β
<img width="606" alt="beta" src="https://user-images.githubusercontent.com/64351233/85850929-baa6a300-b7e8-11ea-8bb6-640c9e5575dc.png">

Type-βは、横長の楕円型リングコマンドである。<br>
選択中のコマンドアイコンからの距離に応じて、表示サイズを小さく、透明度を導入することで<br>
疑似的な奥行きを感じさせるデザインとなっている。<br>

コマンドの選択は**左右のキー**で行う。

#### 2.1.2 Type-γ
<img width="608" alt="gamma" src="https://user-images.githubusercontent.com/64351233/85850924-b8dcdf80-b7e8-11ea-963b-4ec5b09df533.png">

Type-γは、縦長の楕円型リングコマンドである。<br>
Type-βと同様に、選択中のコマンドアイコンからの距離に応じて、表示サイズを小さく、透明度を導入することで<br>
疑似的な奥行きを感じさせるデザインとなっている。

コマンドの選択は**上下のキー**で行う。

### 2.2. 必要画像素材

画像配置場所として、**./img/SoRBatCom/** というフォルダを作成し、ここに以下の画像ファイルを保存する。

#### 2.2.1 リング部分
- Layout.png  (リング本体)
- Layout2.png  (リング本体の上から被せる画像)

#### 2.2.2 コマンドアイコン

各コマンドに対応するアイコンは以下の形式のファイル名を使用する。

```
Com_[XXX].png
```

[XXX]は、**ゲーム内で実際に使用されるコマンドの名称**である。<br>


また、魔法封じ等の状態異常によって<br>
使用を禁止されるおそれのあるコマンドは

```
Com_[XXX]_disabled.png
```

というアイコンを別途用意する。<br>
ゲーム中、使用禁止状態のコマンドのアイコンはこちらの表示に自動的に切り替わる。<br>



下の画像は **Type-α** を利用する場合のフォルダ構成を示したもので、<br>
標準的なRPGツクールMVの新規プロジェクトの状態で利用することを想定して設定したものである。<br>

<img width="568" alt="sample" src="https://user-images.githubusercontent.com/64351233/85851612-0279fa00-b7ea-11ea-88a7-ea97e3f34bfa.png">




### 2.3. 設定

項目と説明量がやや多いため、別ページに記載する。<br>

→ [パラメータ設定](https://github.com/soryu-rmv/BattleStatusHUD/blob/master/parameters.md)

<br><br>

### 2.4. 諸注意・仕様

- 当該キャラクターのターンが回ってきて最初にリングコマンドを際の、初期位置は「戦う」（先頭コマンド）に固定
- スキルウィンドウ等を開いてキャンセルした場合は、直前のコマンドを維持
- FTKR_ExBattleCommand.js による追加オリジナルコマンドは **両立する**


## 3. 実装（競合）情報<br>
### 3.1. 上書き定義
- **Window_ActorCommand.prototype.setup** 
- **Window_ActorCommand.prototype.numVisibleRows**
- **Window_ActorCommand.prototype.processCursorMove**

これらは、コマンドウィンドウの外観デザインに関する処理であり、<br>
本プラグインを導入しておきながら、ここへ干渉するような他のプラグインを導入することは<br>
通常のゲームデザインとしては不自然である。<br>
（≒一般的な食事1回のメニューに、ご飯とパンを同時に設定することは普通ない。）<br>
よって、競合問題への危惧は無用だと考える。


### 3.2. 処理継ぎ足し

- **Scene_Battle.prototype.commandAttack** をはじめとする、コマンド切り替えに関する諸関数

リングコマンドの表示、非表示の切り替えを挿入

- **Scene_Battle.prototype.updateBattleProcess** 

リングコマンドの処理を挿入



### バージョン情報
 - ver 1.00  (Jun 26, 2020)   公開
