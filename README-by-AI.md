# test-plugin

Claude Code plugin のお試し。スキルを少しずつ追加していく実験用のプラグイン。

現在含まれるスキル:

- `1` … ランダムに選んだ自然言語へ「一言」を翻訳して表示する。

## 構成

```
test-plugin/
├── .claude-plugin/
│   ├── plugin.json         プラグインのマニフェスト（plugin name = "sta"）
│   └── marketplace.json    このリポジトリ自身をマーケットプレイスとして配布する定義
├── skills/
│   └── 1/
│       └── SKILL.md        スキル本体
├── LICENSE
└── README.md
```

この1リポジトリが「プラグイン本体」と「マーケットプレイス」を兼ねている。
新しいスキルを足すときは `skills/<スキル名>/SKILL.md` を追加するだけ。

## インストール方法（利用者側）

Claude Code のセッション内で、以下のスラッシュコマンドを実行する。

```
/plugin marketplace add stakiran/test-plugin
/plugin install sta@stakiran
```

- `stakiran/test-plugin` … GitHub の `owner/repo`。
- `sta` … `plugin.json` の `name`（= 呼び出し時の名前空間）。
- `stakiran` … `marketplace.json` の `name`。

インストール後、スキルは `/sta:<スキル名>` で呼べる。例: `/sta:1`。

### 管理コマンド

```
/plugin marketplace list              登録済みマーケットプレイス一覧
/plugin marketplace update stakiran   最新へ更新
/plugin marketplace remove stakiran   削除
```

## 公開手順（作者側）

1. **ローカル検証**（GitHub へ push する前に）

   ```
   claude plugin validate .
   ```

   `plugin.json` と `marketplace.json` のスキーマを検証する。

2. **ローカルのまま動作確認**（任意）

   別プロジェクトの Claude Code セッションで、ローカルパスを直接マーケットプレイスとして追加できる。

   ```
   /plugin marketplace add ./path/to/test-plugin
   /plugin install sta@stakiran
   ```

3. **GitHub へ公開**

   ```
   git add -A
   git commit -m "Add plugin manifest and first skill"
   git push origin master
   ```

   リポジトリを public にしておくこと。

4. **スキル追加・バージョン更新時**

   `skills/` にスキルを足す、または既存を直したら `plugin.json` の `version` を上げて commit・push。
   利用者は `/plugin marketplace update stakiran` で更新を取得する。
   `version` を省略すると git のコミット SHA が使われる。

## ライセンス

MIT
