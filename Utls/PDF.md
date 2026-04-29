#pdf

## PDFを画像（PNG/JPG）に変換する
```terminal
$ sudo apt update
$ sudo apt install -y poppler-utils
$ mkdir OUPUT_DIR
$ pdftoppm -png -r 300 INPUT.pdf OUPUT_DIR/page

page-100.PNG
```

- `png`: 出力形式を **PNG** にする
- `r 300`: 解像度を300dpiにする（高画質）
- `input.pdf`: 変換したいPDFファイル
- `output_image`: 生成される画像ファイルのプレフィックス
-
## PDFをページごとに分割する

```terminal
$ sudo apt update
$ sudo apt install poppler-utils
$ pdfseparate input.pdf page-%d.pdf
```

- `%d` にページ番号が入る

## ページ分割で抽出する

```terminal
$ sudo apt update
$ sudo apt upgrade -y
$ sudo apt install pdftk -y
# 全ページを1ページずつ分割
$ pdftk input.pdf burst
# 1ページ目と3~5ページ目だけを抽出
$ pdftk input.pdf cat 1 3-5 output selected_pages.pdf
```