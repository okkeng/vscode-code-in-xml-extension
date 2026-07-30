# 作業メモ

## 開発フロー

1. Git プロジェクトを clone する
2. ホスト側（Linux VM または WSL2）で VS Code を開く
3. Dev Container を実体化
4. Dev Container 内で開発する
5. VSIXファイルの作成
6. 動作確認（ローカル）
7. VS Code Marketplaceへリリース

## 1. Git プロジェクトを clone する

<!-- TODO: Update repository URL after GitHub migration -->
```bash
git clone https://github.com/okkeng/vscode-code-in-xml-extension.git
```

> [!CAUTION]
> **資材の更新について**
>
> すべての Git 操作（add, commit, push など）は**ホスト側**で実施する。
>
> 理由：
>
> - SSH キーがホスト側にある
> - 環境固有の設定を .devcontainer に入れない

## 2. ホスト側（Linux VM または WSL2）で VS Code を開く

SSHリモートなどで開発する場合は、VS Code の Remote - SSH 拡張機能を使用して、リモートホストに接続し、Open Folder で clone したプロジェクトを開く。

## 3. Dev Container を実体化

コマンドパレット（VS CodeのF1キー） → `Dev Containers: Reopen in Container` を実行。  
コンテナがビルドされるので切り替わるのを待つ。

## 4. Dev Container 内で開発する

VS Code で開発する

```bash
npm run watch      # TypeScript + esbuild を監視モードで実行
npm test           # テスト実行
```

## 5. VSIXファイルの作成

```bash
npx @vscode/vsce package -o release/vscode-code-in-xml-1.0.0.vsix
```

## 6. 動作確認（ローカル）

### VSIXファイルの直接インストール

```bash
code --install-extension ./release/vscode-code-in-xml-1.0.0.vsix
```

## 7. VS Code Marketplaceへリリース

### リリース手順

1. [Code in XML](https://marketplace.visualstudio.com/items?itemName=okkeng.vscode-code-in-xml) を表示
2. Sign in する。
3. [Marketplace](https://marketplace.visualstudio.com/) へ移動し、`Publish extensions` をクリックする。  
4. `Code in XML` をクリックする。
5. 三点リーダーから `Update` を選択する。
6. vsixファイルをアップロードする。

---

TODO: 2026-07-28 v1.0.1 残作業

- [x] DevContainer 環境構築
- [x] アイコン改善（余白削除）
- [x] README 全面改修
- [x] CHANGELOG 更新（v1.0.1 エントリ）
- [x] BMAC サポートセクション追加（TODO コメント付き）
- [x] GitHub 移行用 TODO コメント配置
- [x] 個人ブランド戦略確認
- [x] テーマ開発方向性決定
- [ ] BMAC アカウント作成
- [ ] Groovy + SQL 事例画像配置
- [ ] README, package.json, memo.md の URL 置換
- [ ] GitHub リポジトリ移行（Transfer）
- [ ] v1.0.1 ビルド
- [ ] Marketplace アップロード
- [ ] 開発用ブランチ作成
- [ ] リリース後git tag 設定
