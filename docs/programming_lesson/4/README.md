# プログラミング・レッスン４：　トレリスのテキスト表示

## 手順１

👇　以下の内容の 📄 `./temp/lesson/hello_world.json` ファイルを作ってください。  

```json
{
    "imports": [
        "./examples/data_of_contents/alias_for_color.json"
    ],
    "canvas": {
        "varBounds": {
            "left": 0,
            "top": 0,
            "width": 10,
            "height": 10
        }
    },
    "ruler": {
        "visible": true,
        "foreground": {
            "varColors": [
                "xlPale.xlRed",
                "xlDeep.xlRed"
            ]
        },
        "background": {
            "varColors": [
                "xlDeep.xlRed",
                "xlPale.xlRed"
            ]
        }
    },
    "rectangles" : [
        {
            "varBounds" : {
                "left": 3,
                "top": 4,
                "width": 2,
                "height": 1
            },
            "background": {
                "varColor": "paperColor"
            },
            "mergeCells": true
        }
    ],
    "xlTexts": [
        {
            "location": {
                "x": 3,
                "y": 4
            },
            "text": "Hello, world!",
            "xlAlignment" : {
                "xlHorizontal" : "center",
                "xlVertical" : "center"
            },
            "xlFont": {
                "foreground": {
                    "varColor": "xlStrong.xlRed"
                }
            }
        }
    ]
}
```

👆　`["xlTexts"]` の辺りを説明していきます。  
色は趣味で設定してください。  

そして、以下のコマンドを打鍵してください。  

```shell
import trelliswork as tl
tl.Trellis.build(
    config='./trellis_config.json',
    content='./temp/lesson/hello_world.json',
    temp_dir='./temp',
    workbook='./temp/lesson/hello_world.xlsx')
```

![テキスト描画](../../img/[20250119-0012]print-text4.png)  

👆　テキストを描画できた。  

* `xlHorizontal` には `fill`, `left`, `distributed`, `justify`, `center`, `general`, `centerContinuous`, `right` が入れられるはず。  
* `xlVertical` には `distributed`, `justify`, `center`, `bottom`, `top` が入れられるはず。  


## 次回

次回は［トレリスでの影表示］を予定しています。  
