# Claude Code プラグインお試し

## 利用者向け インストール方法

```
/plugin marketplace add stakiran/test-plugin
/plugin install sta@stakiran
```

わかりにくいので順に

- 1: まずは指定ソースから、あなたの環境に追加する
    - マーケットプレイスを追加する、と表現する
    - ⭕Anthropic が用意してる中央市場
    - ❌各自のローカル環境にインストールされる、特定ユーザー製のカタログ
    - 今回の場合、stakiran がつくった test-plugin というカタログをインストールする
- 2: カタログを入れただけでは使えないので、さらにインストール操作もする
    - すでに 1: にて「stakiranマーケットプレイス」を追加済
    - マーケットプレイスからプラグインをインストールしたい → プラグイン名を指定する
    - 今回は sta にしている

つまり:

- marketplace/
    - plugin/
    - plugin/
    - ...

ファイルの対応

marketplace.json

```json
{
  "name": "stakiran 🐰ここがマーケットプレイス名",
  "owner": {
    "name": "stakiran"
  },
  "description": "stakiran のお試しプラグインを配布するマーケットプレイス。",
  "plugins": [
    {
      "name": "sta 🐰ここがプラグイン名",
      "source": "./",
      "description": "Claude Code プラグインのお試し。スキルを少しずつ追加していく実験用プラグイン。"
    }
  ]
}
```

plugin.json

```json
{
  "name": "sta 🐰ここがプラグイン名",
  "description": "Claude Code プラグインのお試し。スキルを少しずつ追加していく実験用プラグイン。",
  "version": "0.1.0",
  "author": {
    "name": "stakiran"
  },
  "homepage": "https://github.com/stakiran/test-plugin",
  "repository": "https://github.com/stakiran/test-plugin",
  "license": "MIT"
}
```

## 開発者向けメモ

## Q: ローカルで手軽にテストするには？
Ans: `claude --plugin-dir (プラグインのディレクトリ)` で新しいセッションを立ち上げる

## Q: プラグイン更新して公開し直した、これをインストールしてみても更新が入ってないんだが
Ans: 更新時に plugin.json の version を上げる必要がある。でないと claude code が更新アリとみなさない

利用側も含めると、こう:

- 開発側:
    - 1: skill を追加・編集
    - 2: plugin.json の version を上げる（ここ重要。据え置きだと更新が検知されない）
    - 3: commit → push
- 利用側:
    - 4: /plugin marketplace update stakiran … 実体の更新を取り込む
    - 5: /reload-plugins … セッションに反映（オートコンプリート表示も更新）

## Q: 今は test-plugin マーケットプレイスの中に sta プラグインがあるのだと思ってます。ここに sta2 プラグインを追加する場合、どうすればいいのですか？plugin2.json をつくればいいんですか？
Ans: いいえ、常に .claude-plugin/xxxx.json の形で指定する

指定のパターン:

- パターン1: 両方
    - .claude-plugin/
        - marketplace.json
        - plugin.json
- パターン2: マーケットプレイスのみ
    - .claude-plugin/
        - marketplace.json
- パターン2: プラグインのみ
    - .claude-plugin/
        - plugin.json
