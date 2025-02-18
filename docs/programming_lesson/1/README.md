# プログラミング・レッスン１：　トレリスの座標

## 手順１

![列の幅30pixels](../../img/[20250113-1408]column-width-30-pixels.png)  

👆　Excel のワークシートの全ての列の幅を 30 pixels にします。  


## 手順２

![行の高さ30pixels](../../img/[20250113-1411]row-height30pixels.png)  

👆　Excel のワークシートの全ての行の高さを 30 pixels にします。  


## 手順３

![ワークブック・ファイル](../../img/[20250113-1411]no1file.png)  

👆　ファイル名を `no1.xlsx` などにして保存してください。  

レッスンでは 📁 `temp` ディレクトリー下にファイルを置きます。  
レッスン中では、誤操作でファイルの削除や上書きなど、ファイルの破損が起こる可能性があります。  
**temp ディレクトリーの中のファイルは、操作ミスなどにより損失や破損をしても構わないという快諾を頂いた前提で話しを進めていきます。**  


## 手順４

ターミナルに、以下のコマンドを打鍵してください。

```shell
py
```

👆　あるいは、`python` や `python3` といったコマンドかもしれません。環境に合わせてください。  
以降、インタープリターのモードに入ります。  

以下のスクリプトを打鍵してください。  

```py
import trelliswork as tl
tl.Trellis.init()
```

👆　指示が出てきますので、指示に従ってください。以下のファイルが作られます。  
📄 `./temp/lesson/hello_world.json`  

```py
exit()
```

👆　インタープリターのモードから抜けます。  


ファイルの内容は、例えば以下のようなものです。  

```json
{
    "imports": [
        "./examples/data_of_contents/alias_for_color.json"
    ],
    "canvas": {
        "varBounds": {
            "left": 0,
            "top": 0,
            "width": 100,
            "height": 100
        }
    },
    "ruler": {
        "visible": true,
        "foreground": {
            "varColors": [
                "xlPale.xlWhite",
                "xlDeep.xlWhite"
            ]
        },
        "background": {
            "varColors": [
                "xlDeep.xlWhite",
                "xlPale.xlWhite"
            ]
        }
    }
}
```

👆　left と top は 0 にしておいてください


## 手順５

Python のインタープリターを使って、以下のコマンドを打鍵してください。  

```shell
tl.Trellis.build(
    config='./trellis_config.json',
    content='./temp/lesson/hello_world.json',
    temp_dir='./temp',
    workbook='./temp/lesson/hello_world.xlsx')
```

📄 `./temp/lesson/hello_world.xlsx` ファイルが作成されています。確認してください（下図）  

![定規](../../img/[20250113-1515]ruler.png)  

👆　［定規］がレンダリング（描画）されました。  

![定規全体図](../../img/[20250113-1518]whole_ruler.png)  

👆　［定規］の全体図  


## 手順６

この手順では、定規の見方を説明していきます。  

![レクタングル](../../img/[20250113-1551]rectangle.png)  

👆　トレリスでは、長方形の位置とサイズの指定に、（エクセルのセル番号ではなく）、［トレリスの定規］の番号を使います。  

![レクタングル２](../../img/[20250113-1606]right-and-bottom.png)  

👆　また、width, height の代わりに、right, bottom を使っても構いません。  
width と height はそれぞれ独立しているので、 width だけ right を使うといったことも可能です。  
width と right が両方指定されている場合、right を優先して使います。 right を削除したとき width に残っている値を使うかどうかは未定義です。  

right は長方形の右側の外、 bottom は長方形の下側の外であることに違和感を持つかもしれません。  
これは数学では **半開区間** と呼ばれるもので、珍しいものではありません。  
情報系の人の間では半開区間は便利だと使いまくられているので、right は右側の外に出ているものとし、bottom は下側の外に出ているものとして使ってみてください。  

![セコンド・ナンバー](../../img/[20250113-1624]second-number.png)  

👆　トレリスの［定規］の番号では表せない　N列や　12行目を指定したいときには、上図のような書き方で指定できます。  

例： `3o2`  

トレリスの［定規］番号の後ろに、スペースを開けずに小文字の `o` を付け、その後ろにスペースを開けずに 1 または 2 を付けてください。  
例えば `3o2` （文字列）に、 `0o1` （文字列）を足すと 4 （整数）になります。  
`3o3` や `4o0` という書き方も認められますが、 4 と等しいです。  

アメリカの野球ではピッチャーが何回まで投げたかを表すのに　３回の２アウトを　`3.2`　と書いたりする 📖[投球回（Innings pitched）](https://ja.wikipedia.org/wiki/%E6%8A%95%E7%90%83%E5%9B%9E) という書き方があり、 3.2 + 0.1 の答えが 4 になります。  
これは野球ならではで、数学は好きに定義してよいというルールを上手く使った例ですが、  
それを［トレリスの定規］でもそのまま使おうとすると 3.2 に 0.1 を足したら 3.3 だろ、と誤解を与え（プログラマー自身もドツボにハマる）かねません。  
これを避けるため、小数点 `.` を、形に似ている小文字の `o` に変え、これは小数ではないよ、ということが分かるように分けました。深い意味はありません。  

この算術は野球で普通に使われていて珍しいものではないので、使ってみてください。  

上述の Innings pitched と VarRectangle はクラスとして実装されています。以下のファイルから探してみてください。  

* 📄 [Trelliswork ＞ InningsPitched クラス](https://github.com/muzudho/trelliswork/blob/main/src/trelliswork/shared_models/depth120/innings_pitched.py) - 正規表現 `class\s+InningsPitched` で検索してください  
* 📄 [Trelliswork ＞ VarRectangle クラス](https://github.com/muzudho/trelliswork/blob/main/src/trelliswork/shared_models/depth130/var_rectangle.py) - 正規表現 `class\s+VarRectangle` で検索してください  


## 手順７

👇　手順４で作った 📄 `./temp/lesson/hello_world.json` ファイルの内容について、  

```json
{
    "imports": [
        "./examples/data_of_contents/alias_for_color.json"
    ],
    "canvas": {
        "varBounds": {
            "left": "0o1",
            "top": "0o2",
            "width": "10o1",
            "height": "10o2"
        }
    },
    "ruler": {
        "visible": true,
        "foreground": {
            "varColors": [
                "xlPale.xlWhite",
                "xlDeep.xlWhite"
            ]
        },
        "background": {
            "varColors": [
                "xlDeep.xlWhite",
                "xlPale.xlWhite"
            ]
        }
    }
}
```

👆　left を `"0o1"`、 top を `"0o2"`、 width を `"10o1"`、 height を `"10o2"` に変更して保存してください。  

そして以下のコマンドを打鍵してください。  

```shell
tl.Trellis.build(
    config='./trellis_config.json',
    content='./temp/lesson/hello_world.json',
    temp_dir='./temp',
    workbook='./temp/lesson/hello_world.xlsx')
```

![投球回を使って指定した定規](../../img/[20250115-0056]ruler-left-right-using-innings-pitched.png)  

👆　［投球回］を使っても［定規］のサイズを指定できることを示せました。  

トレリスでは上１行、左２列をウィンドウ固定するので、 left と top は 0 にして使うことを推奨します。  


## 手順８

👇　手順７で作った 📄 `./temp/lesson/hello_world.json` ファイルの内容について、  

```json
{
    "imports": [
        "./examples/data_of_contents/alias_for_color.json"
    ],
    "canvas": {
        "varBounds": {
            "left": "0o1",
            "top": "0o2",
            "width": "10o1",
            "height": "10o2"
        }
    },
    "ruler": {
        "visible": false
    }
}
```

👆　`["ruler"]["visible"]` （このように表記するとします）が true だったところを、 false に変えてください。  

手順７と同様に、以下のコマンドを打鍵してください。  

```shell
tl.Trellis.build(
    config='./trellis_config.json',
    content='./temp/lesson/hello_world.json',
    temp_dir='./temp',
    workbook='./temp/lesson/hello_world.xlsx')
```

![定規を非表示](../../img/[20250115-1900]invisible-ruler.png)  

👆　［定規］を不可視にしました。ただし、定規を前提とした［投球回］や［長方形］の機能は消えていません。  


## 次回

次回の記事：　📖 [トレリスの色システム](../2/README.md)  
