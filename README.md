# TIL(Today I Learned)

こちらのリポジトリは学習記録用のリポジトリです。

## ファイル作成のテンプレ
### 月ごとのフォルダを作成
```Shell
$ mkdir YYYY-MM
```

### 日ごとのTILファイルを作成
```Shell
$ echo "# TIL for YYYY-MM-DD" > YYYY-MM/YYYY-MM-DD.md
```

## tilファイル作成用シェルスクリプト
`.bashrc`やら`.zshrc`に追加してホームディレクトリで`source .bashrc`とかで読み込む
```bash
til() {
    eval "touch $1-$2-$3.md" && echo "# TIL for $1-$2-$3" > "$1-$2-$3.md" && echo "Created TIL file: $1-$2-$3.md"
    eval "code $1-$2-$3.md" && echo "Opened TIL file in VSCode: $1-$2-$3.md"
}
```

使うときは
```Shell
til 2025 5 31
```
のように入力すると「# TIL for 2025-5-31」と書かれた`2025-5-31.md`というファイルが作成されます