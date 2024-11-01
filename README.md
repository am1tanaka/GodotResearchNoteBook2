[Godot Engine研究ノート２](https://techbookfest.org/product/4TTGRqssf60xCYKEEmNrQp)のサポートページです。

<a href="https://techbookfest.org/product/4TTGRqssf60xCYKEEmNrQp">
<img src="images/cover.png" alt="Godot Engine研究ノート２" style="height: 300px">
</a>

（[https://techbookfest.org/product/4TTGRqssf60xCYKEEmNrQp](https://techbookfest.org/product/4TTGRqssf60xCYKEEmNrQp)）


ご意見、ご要望、間違いの報告などは、[Issues](https://github.com/am1tanaka/GodotResearchNoteBook2/issues)にお願いします。

## 正誤表

### p95 25行目

誤「Outline thickness は、輪郭を付ける設定です。Godot 側でできるので通常は、不要です。」

正「ビットマップフォントでは、Godot側で、輪郭が設定できないようです。ここで設定すると、輪郭付きのフォントを作成できます。」

## 補足

入稿後に分かったことや気づいた補足です。

### p80「6.4 AnimatinoTree を設定したあとのアニメの追加」

書籍の方法よりも、AnimationPlayerや、AnimationTreeのActiveを無効にするのがセオリーのようです（図1）。

![図1. AnimationPlayerのActiveを無効](images/img00.png)

設定を戻すのを忘れるケアレスミスの原因になり兼ねないため、好ましい対策とは思えません。[こちら(Chris' Tutorials. Animation Tree State Machine Setup w/ Conditions & BlendSpace2D - Godot 4 Resource Gatherer Tutorial)の動画](https://youtu.be/WrMORzl3g1U?feature=shared)を見たところ、Activeは無効にしておいて、スクリプトで実行時に有効にしていました。

やはり、編集中は自動的には動かさず、再生ボタンなどを用意してほしいです。

### p84 16行目 ShapeCast2D、および、ShapeCast3Dのcollision_resultの説明に、colliderが抜けていた

ShapeCast2D、および、ShapeCast3Dのcollision_resultが返す配列に列挙されるDictionaryには、colliderが含まれていました。

[GODOT DOCS. ShapeCast3D.collision_result](https://docs.godotengine.org/ja/4.x/classes/class_shapecast3d.html#class-shapecast3d-property-collision-result)には、[PhysicsDirectSpaceState3D.get_rest_info](https://docs.godotengine.org/ja/4.x/classes/class_physicsdirectspacestate3d.html#class-physicsdirectspacestate3d-method-get-rest-info)メソッドの戻り値と同じ結果が入っていると書かれています。そこにはcolliderは含まれておらず、書籍にもそのまま書いていました。

Godot4.3で戻り値を確認したところ、接触相手のobjectのインスタンスが、colliderに代入されていました。instance_from_id関数を使って、collider_idからオブジェクトを取得しなくて済むので助かります。

### ビットマップフォントのfntでエラーが出る

Godot4.3に読み込むと、fntファイルがエラーになることがありました。

Godot4.3では、アルファが無効なものは使えないようです。BMFontで出力するときに、Export optionsのChrnのAの値がglyphだと、アルファが無効で出力されるようです。outlineにすれば、問題なく出力できました。

なお、glyph設定で出力する必要があれば、次の手順で修正できます。

1. fntをテキスト形式で出力する
2. テキストエディターで、fntファイルを開く
3. 2行目の`alphaChnl`の値を`1`に修正する
4. 上書き保存する


## 本書の執筆環境

前回に続いて、今回も[Techbooster](https://techbooster.booth.pm/)さんの[ReVIEW-Template](https://github.com/TechBooster/ReVIEW-Template)を拝借して、本文の入稿データを作成しました。Windowsでの環境の構築については、以下に記載しています。

- [【Windows】Re:VIEWで書籍用のPDFを作成する](https://am1tanaka.hatenablog.com/entry/2023/09/15/235402)
- [【Windows】Re:VIEWの校正環境を構築する](https://am1tanaka.hatenablog.com/entry/2023/09/23/223924)
- [Re:VIEW関連の記事一覧](https://am1tanaka.hatenablog.com/archive/category/Re%3AVIEW)

## 関連リンク
- [STORM OF BALLS](https://am1tanaka.itch.io/storm-of-balls)
- [Minecart Rails](https://am1tanaka.itch.io/minecart-rails)
- [グラチェン!!](https://godotplayer.com/games/grachan)
- [場面切り替えサンプル](https://github.com/am1tanaka/ChangeSceneSample)
- [次元ドア](https://itch.io/jam/brackeys-11/rate/2524745)
- [カタチナゲル](https://am1.games/katachi/)
