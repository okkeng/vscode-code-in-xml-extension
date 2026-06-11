# 作業メモ

## VSIXファイルの作成

```bash
npx @vscode/vsce package -o release/vscode-code-in-xml-1.0.0.vsix
```

## VSIXファイルのローカルインストール

```bash
code --install-extension ./release/vscode-code-in-xml-1.0.0.vsix
```

## VS Code Marketplaceリリース手順

1. [Code in XML](https://marketplace.visualstudio.com/items?itemName=okkeng.vscode-code-in-xml) を表示
2. Sign in する。
3. [Marketplace](https://marketplace.visualstudio.com/) へ移動し、`Publish extensions` をクリックする。  
4. `Code in XML` をクリックする。
5. 三点リーダーから `Update` を選択する。
6. vsixファイルをアップロードする。
