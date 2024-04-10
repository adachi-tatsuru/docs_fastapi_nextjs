# フロントエンドのコーディング規約

## 概要

このドキュメントでは、フロントエンド開発におけるコーディング規約について説明します。  
コーディング規約は、コードの可読性、保守性、および一貫性を向上させるためのガイドラインです。

- フレームワーク: Next.js (React)
  - ルーティング: App Router
- 言語: TypeScript
- フォーム: React Hook Form, Zod
- API:
  - GraphQL (urql, GraphQL Code Generator)
  - REST API (OpenAPI, Orval, React Query)
- テスト: Jest, React Testing Library, Playwright, Cucumber
- デモ: Storybook
- モック: MSW (Mock Service Worker)
- 状態管理: Zustand, Recoil
- リンター: ESLint, Stylelint

## 命名規則

- 変数、関数、コンポーネントの命名は、キャメルケース（例: `userName`）を使用する
- 定数の命名は、アッパースネークケース（例: `MAX_LENGTH`）を使用する
- コンポーネントの命名は、パスカルケース（例: `UserProfile`）を使用する
- フォルダ名は、ケバブケース（例: `user-profile`）を使用する
- features の命名は、`<action>(動詞)` で始まる形式に統一する（例: `view-profile`）
- domains の命名は、`<domain>-<property>-<ui>` の形式に統一する（例: `avatar-circle`）

## コードフォーマット

- インデントは、スペース 2 つを使用する
- ブレースは、同じ行に配置する（例: `if (condition) {`）
- コンマの後には、スペースを入れる（例: `[1, 2, 3]`）

## コメント

- コメントは、コードの上部に配置し、`//`を使用する
- 複数行のコメントには、`/** */`を使用する
- 関数やコンポーネントには、JSDoc スタイルのコメントを記述する

## コンポーネントディレクトリ構造

コンポーネントは、以下のディレクトリ構造で管理します。  
上位ディレクトリから下位ディレクトリへの参照（依存）のみを許可する。

- `web-components`: WebComponents 向けにカスタム要素を定義
  - feature や provider を組み合わせてカスタム要素を定義します
- `providers`: アプリケーションに必要な Provider を格納
  - urql などのライブラリを shared/lib で定義し、providers がそれらを参照します
- `features`: ビジネス価値を提供するための機能を格納
  - domains や shared を組み合わせます。API 呼び出しや状態管理、zod バリデーションを担当します
  - 以下の構造のサブディレクトリを作成します
    - `hooks`: UI に依存する hooks を格納
      - useDisclosure
    - `stores`: ドメイン依存の状態管理を格納
      - useReducer,React Hook Form
    - `ui`: React の UI コードを格納
      - \*.(stories|test|).tsx
- `domains`: プロダクトのドメイン UI を格納
  - ドメインは、GraphQL Schema に該当します。与えられたデータ・状態操作を入力に UI を表現します
  - 以下の構造のサブディレクトリを作成します
    - `hooks`: UI に依存する hooks を格納
      - useDisclosure
    - `stores`: ドメイン依存の状態管理を格納
      - useReducer,React Hook Form
    - `ui`: React の UI コードを格納
      - \*.(stories|test|).tsx
- `shared`: 再利用可能なプロダクト非依存のコードを格納
  - ライブラリやユーティリティを配置します
  - `next/link` や `next/image` などは、必ずラッパーを作成して shared に配置します
    - nextjs の 仕様変更時に、ラッパーを修正するだけで済むようにする

各ディレクトリには、`index.ts`を配置し、ディレクトリ単位でインポートできるようにします。  
また、階層構造を作らずフラットに配置することを推奨します。

## GraphQL Fragment / OpenAPI

- GraphQL を使用する場合、domains 層には、ドメインに必要なデータを示す GraphQL Fragment を定義します。  
  features 層は、domains 層の GraphQL Fragment を用いて API 通信のクエリを記述します。
- REST API を使用する場合、OpenAPI を使用して API のスキーマを定義します。  
  Orval と React Query を使用して、型安全な API クライアントを生成し、API データの取得と更新を行います。

## コンポーネントコンポジション

異なるドメイン間で参照したい場合は、features 層で、コンポーネント・コンポジションやコンポーネント・インジェクションのパターンを使用します。

## モック

API のモックには、MSW（Mock Service Worker）を使用します。  
API のモックを定義することで、フロントエンドの開発をバックエンドの開発と独立して進めることができます。

## Storybook

[UI Stack](https://www.scotthurff.com/posts/why-your-user-interface-is-awkward-youre-ignoring-the-ui-stack/)という考え方で Story を整理します。

- コンポーネントのデモとドキュメンテーションに Storybook を使用する
- ストーリーの命名規則を統一し、プレフィックスに絵文字を使用する
- `✨ Ideal State`: 理想的な状態
  - 理想状態は、すべてのデータが正常に読み込まれ、ユーザーがアプリケーションやウェブサイトを最も効果的に使用できる状態
- `⏳ Loading State`: ローディング中
  - ローディング状態は、データが読み込まれるまでの間に表示される状態
- `🫥 Blank State`: 空の状態
  - 空の状態は、データが存在しない場合に表示される状態
- `🍕 Partial State`: 部分的な状態
  - 部分的な状態は、データが一部のみ読み込まれた状態
- `🔥 Error State`: エラー状態
  - 何らかの問題が発生し、アプリケーションが正常に機能しない状態
- `🤖 (Interaction)Testing`: インタラクションテスト
  - ユーザーインターフェースがユーザーの操作に対して正しく反応するかを検証するテスト

## リンター

- ESLint を使用して、JavaScript と TypeScript のコードの品質とスタイルを確保する
- Stylelint を使用して、CSS と SASS のコードの品質とスタイルを確保する
- プロジェクトのルートに`.eslintrc`と`.stylelintrc`ファイルを配置し、ルールを設定する
- コミット前に、自動的にリンターを実行するようにする
- 依存関係の Lint には、`eslint-plugin-strict-dependencies`を使用する

## ドキュメント

- コーディング規約やアーキテクチャの決定事項は、Markdown で文書化する
- ドキュメントの構造は、`bulletproof-react`を参考にする
- ドキュメントの作成手順は以下の通りとする
  1. Figma などのビジュアルコラボレーションツールでたたき台を作成する
  2. チームメンバーと議論を通じて、設計を決定する
  3. 決定した内容や Figma のリンクを、Markdown にまとめる
- ドキュメントのテストには、以下のツールを使用するか検討する
  - デッドリンクのチェック: `markdown-link-check`
  - Markdown 構文のチェック: `markdownlint`
  - テキストのチェック: `textlint`
