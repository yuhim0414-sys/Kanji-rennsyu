# 漢字パーツあわせ

小学校で習う漢字 1026 字を、パーツの組み立て・書くテスト・選ぶテストで学べる漢字ゲームです。
1 つの HTML ファイル（`index.html`）だけで動きます。サーバーやインストールは不要です。

## できること

- **れんしゅう**：パーツを指で運んで漢字を組み立てる（部首名つき、1 回までやり直し可）
- **テスト**：かく（手書きを自動判定）／くみたてる／えらぶ（4 択）
- **じてん**：意味・音訓・書き順・部品を調べる。上の検索欄で読み・漢字・部首名から探せる
- **にがて**：まちがえた字がたまり、「こくふく れんしゅう」（見る → くみたてる → かく）で減らす
- **きろく**：点数票と漢字ずかん。先生用画面（暗証番号つき）で No.1〜No.4 の全員分を確認・コピー
- 学年・学期（光村図書 2024 年度版の新出順）・問題数（3／5／10）を選んで出題
- れんぞくまる、完成アニメーション

## GitHub Pages で公開する手順

1. GitHub で新しいリポジトリを作る（例：`kanji-parts`）
2. このフォルダの中身（`index.html`、`README.md`、`.nojekyll`、`tools/`）をアップロードする
3. リポジトリの **Settings → Pages** で、Source を「Deploy from a branch」、Branch を `main` / `(root)` にして保存
4. 数分後に `https://<ユーザー名>.github.io/kanji-parts/` で開ける

タブレットではブラウザの「ホーム画面に追加」をすると、アプリのように起動できます。

## 記録の保存について

- 子どもの記録（にがて・点数・ずかん・名前・先生用暗証番号）は、**使っている端末のブラウザ（localStorage）にだけ**保存されます。
- GitHub やほかのサーバーには送られません。リポジトリに子どもの情報は含まれません。
- 端末ごと・ブラウザごとに別々です。ブラウザのサイトデータを消すと記録も消えます。
- 暗証番号は子どもよけ程度のもので、強い保護ではありません。

## データを作り直すとき（`tools/`）

`index.html` は `tools/app.html`（画面とプログラム）にデータを埋め込んで作っています。

```sh
cd tools
git clone --depth 1 https://github.com/KanjiVG/kanjivg.git
curl -L -o kanji.json https://raw.githubusercontent.com/davidluzgouveia/kanji-data/master/kanji.json
python3 build_data.py   # data.json を作る
python3 build.py        # ../kanji-parts.html を作る（index.html として使うときは <head> を付ける）
```

| ファイル | 中身 |
|---|---|
| `grades.py` | 学年別漢字配当表（2020 年度〜、1026 字） |
| `order.txt` | 学年ごとの光村図書の新出順 |
| `words.txt` | 出題に使うことば（`字=ことば\|その字の読み`） |
| `means.txt` | 子ども向けの意味 |
| `hints.json` | 読みのヒント（検索用） |

ことば・意味は手作業で作ったものです。直したいときは `words.txt` / `means.txt` を編集して作り直してください。

## 出典とライセンス

- 字形・書き順データ：[KanjiVG](https://kanjivg.tagaini.net/)（© Ulrich Apel、[CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)）。
  `index.html` に埋め込んだ字形データはこれをもとに加工したもので、同じ CC BY-SA 3.0 で提供されます。
- 読み：[KANJIDIC](https://www.edrdg.org/wiki/index.php/KANJIDIC_Project)（EDRDG、CC BY-SA 4.0）を
  [kanji-data](https://github.com/davidluzgouveia/kanji-data) 経由で利用。
- 光村図書の新出順：ミチムラ式漢字カードの[番号対照表](https://kanji.cloud/card/2024-number-comparison/)を参照。
- 部品名の一部：ミチムラ式部品カードの名称を参考にしています。
- フォント：Klee One、Zen Maru Gothic（Google Fonts、SIL Open Font License）。
