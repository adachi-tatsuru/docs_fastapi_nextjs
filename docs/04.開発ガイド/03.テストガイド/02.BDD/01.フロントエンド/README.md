# フロントエンドの振る舞い駆動開発 (BDD)

## 概要

このドキュメントでは、フロントエンド開発における振る舞い駆動開発 (BDD) のプロセスと手法について説明します。  
BDD は、ソフトウェアの振る舞いに焦点を当てた開発手法で、ステークホルダーとの共通の理解に基づいてシステムを開発します。  
本プロジェクトでは、Playwright と Cucumber を使用して、BDD のプラクティスを実践します。

## BDD のプロセス

1. 機能の明確化 (Feature)
   - ステークホルダーとの話し合いを通じて、開発する機能を明確にします。
   - 機能の詳細を Gherkin 構文で記述したフィーチャーファイルを作成します。
2. シナリオの定義 (Scenario)
   - フィーチャーを実現するためのシナリオを定義します。
   - シナリオは、Given（前提条件）、When（アクション）、Then（期待結果）の形式で記述します。
3. ステップ定義の実装 (Step Definition)
   - シナリオを実行するためのステップ定義を、TypeScript（Playwright）で実装します。
   - ステップ定義では、シナリオの Given、When、Then に対応するコードを記述します。
4. テストの実行と結果の確認
   - Cucumber を使用して、フィーチャーファイルに定義されたシナリオを実行します。
   - テストの結果を確認し、失敗したシナリオについては、原因を特定して修正します。
5. リファクタリングとメンテナンス
   - テストが安定した状態で、コードのリファクタリングを行います。
   - 新しい要件や変更に合わせて、フィーチャーファイルとステップ定義を更新します。

## 利用ツール・ライブラリ

- BDD フレームワーク: Cucumber
- Web ブラウザ自動化: Playwright
- プログラミング言語: TypeScript

## ディレクトリ構造

```
features/
  ├── step_definitions/
  │   └── *.steps.ts
  ├── support/
  │   ├── hooks.ts
  │   └── world.ts
  └── *.feature
```

- `features/`: BDD のテストに関連するファイルを格納するディレクトリ
  - `step_definitions/`: ステップ定義ファイル（TypeScript）を格納するディレクトリ
  - `support/`: テストの設定やフック、ワールドオブジェクトの定義ファイルを格納するディレクトリ
  - `*.feature`: Gherkin 構文で記述されたフィーチャーファイル

## フィーチャーファイルの記述方法

```gherkin
Feature: ログイン機能
  ユーザーがログインできるようにする

  Scenario: 正しいユーザー情報でログインする
    Given ログインページを開いている
    When ユーザー名に "test_user" と入力する
    And パスワードに "test_password" と入力する
    And ログインボタンをクリックする
    Then ホームページが表示される
```

- `Feature`: フィーチャーの名前と説明を記述します。
- `Scenario`: テストするシナリオを記述します。
- `Given`、`When`、`Then`: シナリオのステップを記述します。

## ステップ定義の実装方法

```typescript
import { Given, When, Then } from "@cucumber/cucumber";
import { expect } from "@playwright/test";

Given("ログインページを開いている", async function () {
  await this.page.goto("https://example.com/login");
});

When("ユーザー名に {string} と入力する", async function (username) {
  await this.page.fill("#username", username);
});

When("パスワードに {string} と入力する", async function (password) {
  await this.page.fill("#password", password);
});

When("ログインボタンをクリックする", async function () {
  await this.page.click("#login-button");
});

Then("ホームページが表示される", async function () {
  await expect(this.page).toHaveURL("https://example.com/home");
});
```

- `Given`、`When`、`Then`: フィーチャーファイルのステップに対応する関数を定義します。
- `this.page`: Playwright のページオブジェクトを参照します。
- `expect`: Playwright のアサーションを使用して、期待する結果を検証します。

## テストの実行方法

```bash
npx cucumber-js features/**/*.feature
```

- `npx cucumber-js`: Cucumber を実行するコマンド
- `features/**/*.feature`: テストするフィーチャーファイルのパスを指定します。

## ベストプラクティス

- シナリオは独立して実行できるようにする
- ステップ定義は再利用可能で、メンテナンスしやすいようにする
- フィーチャーファイルは、ドメイン専門家や非技術者にも理解しやすい言葉で記述する
- テストデータは、フィーチャーファイルとステップ定義で分離する
- テストの実行速度に配慮し、必要に応じてタグを使用してテストを分類する
