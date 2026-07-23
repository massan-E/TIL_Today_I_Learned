# TIL(Today I Learned)

学習記録用のディレクトリです。もともとは別コミュニティでアウトプットしたものをほぼそのままコピペして載せていくリポジトリでしたが、現在は `massans_growth`（本人専用カリキュラム）配下に組み込み、カリキュラムを進める中で学んだことのメモ置き場も兼ねています。

日ごとに `YYYY-MM/YYYY-MM-DD.md` の形で1ファイル作り、`vim` でカタカタ書いていくスタイルです。

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
`.bashrc`やら`.zshrc`に追加して`source .zshrc`とかで読み込む。
事前に til ディレクトリの場所を `TIL_DIR` に設定しておく（これでどのディレクトリから実行しても正しい場所に作られる）。
```bash
export TIL_DIR="$HOME/Development/Learning/massans_growth/til"

til() {
    # 引数なし → 今日の日付。til YYYY MM DD で任意の日付も可（ゼロ埋めされる）
    local y m d
    if [ -n "$3" ]; then
        y="$1"; m=$(printf "%02d" "$2"); d=$(printf "%02d" "$3")
    else
        y=$(date +%Y); m=$(date +%m); d=$(date +%d)
    fi
    local dir="$TIL_DIR/${y}-${m}"
    local file="${dir}/${y}-${m}-${d}.md"
    mkdir -p "$dir"                      # 月フォルダを自動作成
    if [ ! -f "$file" ]; then
        echo "# TIL for ${y}-${m}-${d}" > "$file"
        echo "Created TIL file: $file"
    else
        echo "Open existing TIL file: $file"
    fi
    vi "$file"
}
```

使い方：
- `til` … 引数なしなら**今日の日付**のファイルを作って `vi` で開く
- `til 2025 5 31` … 任意の日付も指定可（`5`→`05` のようにゼロ埋めされる）

月フォルダ（`YYYY-MM/`）は自動作成され、`TIL_DIR` を基準にするのでどのディレクトリから実行しても正しい場所に作られる。既存ファイルは上書きせずそのまま開くだけ。