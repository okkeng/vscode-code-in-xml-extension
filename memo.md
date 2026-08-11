# 作業メモ

## 開発フロー

1. Git プロジェクトを clone する
2. ホスト側（Linux VM または WSL2）で VS Code を開く
3. Dev Container を実体化
4. Dev Container 内で開発する
5. VSIXファイルの作成
6. 動作確認（ローカル）
7. VS Code Marketplaceへリリース

### 1. Git プロジェクトを clone する

#### リポジトリ

```bash
git clone https://github.com/arukumo/vscode-code-in-xml.git
```

#### ブランチルール

リリースしている資源 = `main` ブランチ  
開発する際は、`release/<バージョン>` ブランチを作成する。  
リリースブランチに対し、`feature` ブランチで修正する。  
作成した作業ブランチ（`release` ブランチ/`feature` ブランチ）はマージ後削除する。

```plaintext
main
┣ release/1.0.1
┗ release/1.0.2
    ┣ feature/<機能>
    ┗ feature/<機能>
```

#### Git更新について

DevContainer環境を作成したが、プラグインをホスト側に入れたくないため（他の案件と混ざる）。  
Git操作（add, commit, push など）はホスト側で行った方がいいかも。理由は以下  

- SSH キーがホスト側にある
- 環境固有の設定を .devcontainer に明に入れない

### 2. ホスト側（VM または WSL2）で VS Code を開く

SSHリモートなどで開発する場合は、VS Code の Remote - SSH 拡張機能を使用してリモートホストに接続し、Open Folder で clone したプロジェクトを開く。

### 3. Dev Container を実体化

コマンドパレット（VS CodeのF1キー） → `Dev Containers: Reopen in Container` を実行。  
コンテナがビルドされるので切り替わるのを待つ。

### 4. Dev Container 内で開発する

VS Code で開発する

```bash
npm run watch      # TypeScript + esbuild を監視モードで実行
npm test           # テスト実行
```

### 5. VSIXファイルの作成

```bash
npx @vscode/vsce package -o release/vscode-code-in-xml-1.0.0.vsix
```

### 6. VSIXファイルの直接インストール（ローカル）

```bash
code --install-extension ./release/vscode-code-in-xml-1.0.0.vsix
```

### 7. VS Code Marketplaceへリリース

1. [Marketplace](https://marketplace.visualstudio.com/vscode) を表示
2. `Sign in` する。
3. `Publish extensions` をクリックする。  
4. `Code in XML` をクリックする。
5. 三点リーダーから `Update` を選択する。
6. vsixファイルをアップロードする。
