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
