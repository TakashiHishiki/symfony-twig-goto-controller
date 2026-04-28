# Symfony: Twig ↔ Controller

Symfony開発者向けの Visual Studio Code 拡張機能です。
Twigテンプレートと PHPコントローラー間を**双方向**に即座にジャンプできます。

[![VS Code Marketplace](https://img.shields.io/visual-studio-marketplace/v/colscenery.symfony-twig-goto-controller?label=VS%20Code%20Marketplace&logo=visual-studio-code)](https://marketplace.visualstudio.com/items?itemName=colscenery.symfony-twig-goto-controller)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 機能

### Twig → Controller

現在開いているTwigテンプレートをレンダリングしているコントローラーを開きます。

**使い方：**

- `.twig` または `.html` ファイル内で右クリック → **「Symfony: Open Controller for this Twig」**
- Twigファイルを開いた状態で、エディタタイトルバーの `$(go-to-file)` アイコンをクリック

**検索方法：**

1. **`render()` スキャン** — `src/Controller` 配下のすべてのPHPファイルをスキャンし、`render('your/template.html.twig')` の呼び出し箇所を特定して該当行にジャンプします。
2. **命名規則** — テンプレートのパスから候補を導出します（例: `templates/foo/bar.html.twig` → `FooController.php`、`Foo/BarController.php`）。

複数の候補が見つかった場合は、クイックピックリストから選択できます。

---

### Controller → Twig

現在開いているコントローラーがレンダリングするTwigテンプレートを開きます。

**使い方：**

- `.php` ファイル内で右クリック → **「Symfony: Open Twig for this Controller」**
- PHPファイルを開いた状態で、エディタタイトルバーの `$(go-to-file)` アイコンをクリック

**解決の優先順位：**

1. **`render()` 呼び出し** — 開いているコントローラーを読み取り、`render()` 内のすべての `.twig` パスをソース行番号付きで一覧表示します。
2. **命名規則** — コントローラーのファイル名から候補を導出します（例: `Admin/DashboardController.php` → `templates/admin/dashboard/index.html.twig`）。
3. **ファジー名前マッチ** — 上記で見つからない場合、すべてのTwigファイルをベース名でスキャンします。

---

### 選択テキストから開く

どちらの方向でも、選択またはカーソルが当たっているテンプレートパス文字列から操作できます。

**Twig / HTMLファイル内：**
`'admin/dashboard.html.twig'` を選択 → 右クリック → **「Symfony: Open Controller from template path」**

**PHPファイル内：**
`'admin/dashboard.html.twig'` を選択またはホバー → 右クリック → **「Symfony: Open Twig from template path」**

テキストが選択されていない場合、現在行の最も近い `.twig` パス文字列を自動抽出します。

---

## 右クリックコンテキストメニュー

| 対象ファイル | メニュー項目 | 動作 |
|---|---|---|
| `.twig` / `.html` | Symfony: Open Controller for this Twig | コントローラーへジャンプ |
| `.twig` / `.html` + 選択テキスト | Symfony: Open Controller from template path | `render()` 行のコントローラーへジャンプ |
| `.php` | Symfony: Open Twig for this Controller | Twigテンプレートへジャンプ |
| `.php` + 選択テキスト | Symfony: Open Twig from template path | 選択したテンプレートを開く |

---

## 設定

**設定画面**（`Ctrl+,`）を開き、`symfonyTwig` で検索してください。

| 設定項目 | デフォルト値 | 説明 |
|---|---|---|
| `symfonyTwig.templatesDir` | `templates` | Twigテンプレートのルートディレクトリ（プロジェクトルートからの相対パス） |
| `symfonyTwig.controllerDir` | `src/Controller` | コントローラーのルートディレクトリ（プロジェクトルートからの相対パス） |
| `symfonyTwig.searchInPhp` | `true` | 有効にすると、命名規則によるルックアップに加えてPHPファイルの `render()` 呼び出しもスキャンします |

---

## インストール

[拡張機能マーケットプレイス](https://marketplace.visualstudio.com/items?itemName=colscenery.symfony-twig-goto-controller) からインストールできます。

VS Code で `Ctrl+P`（Mac: `Cmd+P`）を開き、以下を貼り付けて Enter を押してください。

```
ext install colscenery.symfony-twig-goto-controller
```

---

## 動作要件

- VS Code `^1.80.0`
- 標準的な Symfony プロジェクト構成（`templates/` と `src/Controller/` が存在すること）

---

## ライセンス

[MIT](LICENSE)
