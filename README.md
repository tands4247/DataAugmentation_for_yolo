★前提
yoloの学習データを対象とする
labelImg等を使ったアノテーション済みであることが前提

★データ拡張の処理一覧
・二値化
・ダウンサンプリング（解像度低下）
・モルフォロジー・収縮処理
・反転
・ぼかし（平滑化）
・ガンマ変換とヒストグラム均一化
・ノイズ
・ラベル部分のランダムマスク処理
・回転


★各拡張処理のパラメータ変更やバリエーションの増やし方
内部コードにてコメントアウトで方法を解説しているのでそちらを参照
基本はmain.pyで処理を定義しているが、以下の処理はlibフォルダ内で定義されているためそちらを参照
・ガンマ変換とヒストグラム均一化
・ノイズ
・ラベル部分のランダムマスク処理
・回転


★バージョンについて（あくまで実行を確認したバージョンなためこれに合わせる必要はない）
・python : 3.12.1
・opencv : 4.9.0
・numpy  : 1.26.3


★実行前ディレクトリ構成
注意）anotationフォルダの名前は任意だがその他の構成、フォルダ名は固定
注意）anotationフォルダはアノテーション直後を想定してフォルダ内部は画像とラベルが混同している状態で実行
（labelImg等アノテーションツールは画像とそのラベルが同一フォルダで出力されるため）


├── controllers
│   ├── userController.ts
│   └── chatController.ts
├── services
│   ├── userService.ts
│   └── chatService.ts
├── models
│   ├── user.ts
│   └── chat.ts
└── configs

.
└── data_augmentation/
    ├── anotation/    ⇚フォルダ名は任意
    │   ├── classes.txt
    │   ├── アノテーション済み画像.jpg      ⇚
    │   └── アノテーション済みラベル.txt    ⇚フォルダ内に画像とラベルが混同
    ├── lib/
    │   ├── bokashi.py
    │   ├── helpers.py
    │   ├── LUT.py
    │   ├── maskImage.py
    │   ├── myClass.py
    │   ├── noise.py
    │   └── rotate.py
    ├── main.py
    └── README.md



★実行方法
1. data_augmentationフォルダまで移動
cd /・・・/data_augmentation
2. main.pyを実行。第一引数にアノテーション済みの実行対象フォルダを指定（必須）
例）python main.py ./anotation

実行が成功するとカレントディレクトリ内にopuputフォルダが作成され、拡張した画像、ラベルが別々に保存される
またデータ拡張前の画像とラベル(引数で指定したアノテーション済みのもの)もoutputフォルダに出力される。
.
└── output
    ├── classes.txt
    ├── images/
    │   ├── 拡張後の画像.jpg
    │   └── ・・・
    └── labels/
        ├── 拡張後のラベル.txt
        └── ・・・
