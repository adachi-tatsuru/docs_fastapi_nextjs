# フロントエンドのテスト駆動開発 (TDD)

## 概要

このドキュメントでは、Next.js を使用したフロントエンド開発におけるテスト駆動開発 (TDD) のアプローチについて説明します。  
厳密な TDD の適用は難しい場合がありますが、コンポーネントの動作を検証するためのテストを追加することで、品質の向上とリグレッションの防止が可能です。

## 開発のプロセス

1. コンポーネントの作成と Storybook での表示
   - デザインに基づいて React コンポーネントを作成します。
   - Storybook を使用して、コンポーネントの表示を確認し、デザインの検証を行います。
2. テストケースの追加
   - コンポーネントの動作を検証するためのテストケースを追加します。
   - テストケースは、コンポーネントのプロパティ、イベントハンドラ、レンダリング結果などを検証します。
3. テストの実行と改善
   - 追加したテストを実行し、コンポーネントの動作を確認します。
   - テストが失敗した場合は、コンポーネントの実装を改善し、テストが通過するようにします。
4. リファクタリングとテストの更新
   - コンポーネントの実装を改善し、リファクタリングを行います。
   - リファクタリングに伴い、テストケースを更新し、すべてのテストが通過することを確認します。

## 利用ツール・ライブラリ

- テストランナー: Jest
- アサーションライブラリ: React Testing Library
- モックライブラリ: MSW (Mock Service Worker)
- コンポーネントの表示: Storybook

## テスト対象

- React コンポーネント

  - プロパティの受け取りとレンダリング結果の検証
  - イベントハンドラの動作の検証
  - 条件付きレンダリングの検証

- ページコンポーネント
  - データの取得と表示の検証
  - ユーザーインタラクションの検証
  - エラーハンドリングの検証

## テストの記述方法

- テストファイルの命名規則: `[テスト対象].test.tsx`
- テストケースの構造:
  - `describe` ブロック: テストグループの説明
  - `test` または `it` ブロック: 個々のテストケースの説明
  - `expect` 文: アサーションの記述

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import MyComponent from "./MyComponent";

describe("MyComponent", () => {
  test("renders correctly with given props", () => {
    render(<MyComponent title="Test Title" />);
    expect(screen.getByText("Test Title")).toBeInTheDocument();
  });

  test("calls onClick handler when button is clicked", () => {
    const handleClick = jest.fn();
    render(<MyComponent onClick={handleClick} />);
    userEvent.click(screen.getByRole("button"));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });
});
```

## ベストプラクティス

- コンポーネントの重要な動作に対してテストを追加する
- テストケースを独立して実行できるようにする
- モックやスタブを活用して、テストの対象を分離する
- テストの可読性を重視し、わかりやすい命名を心がける
- リファクタリング後に必ずテストを実行し、動作を確認する
