# pdf2md
Claude Codeを使ってPDF形式の資料を、画像を含めてどの程度Markdown形式に変換できるかを試した資料です。スクショ画像等はそのまま利用し、フロー図やシーケンス図等は、draw.ioやMermaidで作成しなおした後に、管理しやすい形にすることを目指しました。

## 1. 前提
- [Road Trip Advisor Web Application](https://www.bellevuecollege.edu/wp-content/uploads/sites/135/2019/04/SDD_RoadTrip.pdf) 英語で記載された学習用のサンプル仕様書を、MarkDownに変換し、最終的には日本語に翻訳して保存します。
- 使用するツールは、VSCodeと必要な拡張機能、AIはClaude Codeを採用
- スクショ画像はそのまま利用、フロー図等については、claude codeを使用して変換したところで完成版としている（従って正解ファイルと比べると、ずれやゆがみがある。それらはVSCode拡張機能で draw.io ファイルを編集し仕上げる前提とする。）
## 2. 結論
ひとまず結論。

- 文字やレイアウトは、ほとんど問題なく変換できているように見える
- 簡単な図についての再現率は高い。
- 複雑な図の変換精度は70%〜80%といったところ。変換に失敗した箇所はdraw.ioを使ってマニュアルで対応する形でもよいと考える。
- 何度か試していると画像の変換にもぶれが生じるので、プロンプトの指示等で全てを解決しようと思わない方がよい。（ある程度まで変換できていたら、あとは手動で編集する方が早いと思われる）

> ◾️ 変換前ファイル
> - [Road Trip Advisor Web Application](https://www.bellevuecollege.edu/wp-content/uploads/sites/135/2019/04/SDD_RoadTrip.pdf)
>
> ◾️ 変換後ファイル
> - [Road Trip Advisor Web Application(MD形式)](results/SDD_RoadTrip_jp.pdf)

## 3. 準備
必要なツール等

- VSCode
- VSCode拡張機能
  - Draw.io integration
    - draw.io編集用
  - Markdown PDF
    - mdからpdfに変換
  - Markdown Preview Mermaid Support
    - mermaidをサポートしたmdのプレビュー
  - vscode-pdf
    - VSCode上でpdfをプレビュー
- Claude Code

## 4. 変換実施

※注意※ 以降の作業は、claude codeを使用してます。github copilotを使うと別の結果になり

1. pdfをmarkdown形式に変換するように指示を出す
```
@SDD_RoadTrip.pdf をMarkDownに変換してください。
## 制約: 
- MarkDownに準拠する
- 見出し構造を維持する
- 表は崩さない
- 画像または図の部分は別途保存して参照形式とする
- 画像または図の見た目は変わらないようにする
- 画像や図の説明箇所はテキストとして保存する
```

2. 画像ファイルをDraw.io形式に変換する
```
@figure1_system_overview.png をdraw.io形式で作成しなおしてください。
オリジナルの画像は残した状態で、結果をpng形式に変換し @SDD_RoadTrip.md の対応箇所に挿入してください。
```

ほかの画像についても同様な方法で画像をdraw.io形式に変換していく

3. シーケンス図をMermaid形式に変換する
```
@figure_sequence.png をmermaid形式に変換してください。
```

4. 最後に翻訳する
```
@SDD_RoadTrip.md内のテキスト箇所について、英文を日本語に翻訳し、SDD_RoadTrop_jp.md という名前で保存して
```

ここまでの作業で完成したのが、[Road Trip Advisor Web Application(MD形式)](results/SDD_RoadTrip_jp.pdf)です。
繰り返しとなりますが、何度か試すと結果も変わってくるので、プロンプトの指示内容は、その都度変更していく必要があります。
