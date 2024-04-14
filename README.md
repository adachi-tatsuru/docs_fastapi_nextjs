# ドキュメントテンプレート

- ステークホルダーに対して、プロジェクトの目的、進行状況、成果物を共有するためのドキュメントテンプレートです。

## ドキュメントの目的

- 品質保証
- 継続性確保
- 目標共有
- 進行状況把握
- 知識共有
- 成果物共有
- 成果物再利用
- 品質向上
- 運用・保守支援

## ドキュメントの構成

```
docs/
│
├── 00.各フェーズ/ # このディレクトリは、内部資料のため、公開しない
│   ├── 01.要件定義フェーズ/
│   │   └── README.md
│   ├── 02.設計フェーズ/
│   │   └── README.md
│   └── 03.開発フェーズ/
│       ├── 00.マイルストーンテンプレート/
│       │   ├── 01.計画/
│       │   │   └── README.md
│       │   ├── 02.実装/
│       │   │   ├── 01.フロントエンド/
│       │   │   │   ├── README.md
│       │   │   │   └── 01.TDD/
│       │   │   │       └── README.md
│       │   │   └── 02.バックエンド/
│       │   │       ├── README.md
│       │   │       └── 01.TDD/
│       │   │           └── README.md
│       │   ├── 03.BDD/
│       │   │   ├── 01.フロントエンド/
│       │   │   │   └── README.md
│       │   │   └── 02.バックエンド/
│       │   │       └── README.md
│       │   └── 04.振り返り/
│       │       └── README.md
│       ├── 01.マイルストーン1/
│       │   ...
│       └── NN.マイルストーンN/
│           ...
│
├── 01.プロジェクト概要/
│   ├── 01.プロジェクトの目的/
│   │   └── README.md
│   └── 02.スケジュール/
│       └── README.md
│
├── 02.要求定義/
│   ├── 01.要求仕様書/
│   │   └── README.md
│   ├── 02.機能要件定義書/
│   │   └── README.md
│   └── 03.非機能要件定義書/
│       └── README.md
│
├── 03.設計/
│   │   # 最初に全体の枠組みを設定します。
│   ├── 01.全体設計/
│   │   └── README.md
│   │   # インフラを計画します。ただし、反復的に変更される可能性があるため、最終的な設計は後回しにします。
│   ├── 02.インフラ設計/
│   │   └── README.md
│   │   # 全体設計直後にセキュリティ基準とポリシーを設定します。
│   ├── 03.セキュリティ設計/
│   │   └── README.md
│   │   # データの構造が明確になる必要があります。
│   ├── 04.データモデリング設計/
│   │   └── README.md
│   │   # データモデリングを基に具体的なDBの構造を定めます。
│   ├── 05.DB設計/
│   │   └── README.md
│   │   # セキュリティとデータ構造が定まった上で、外部との接点を設計します。
│   ├── 06.API設計/
│   │   ├── README.md
│   │   └── 01.エンドポイント定義/
│   │       └── README.md
│   │   # APIの仕様が決定された上で、ユーザーインターフェイスを設計します。
│   ├── 07.画面定義/
│   │   ├── README.md
│   │   ├── pages/
│   │   │   ├── README.md / の画面定義
│   │   │   ├── about/
│   │   │   │   └── index.md # /about の画面定義
│   │   │   └── ...
│   │   └── components/
│   │       ├── component1/
│   │       │   └── index.md # component1 の定義
│   │       ├── component2/
│   │       │   └── index.md # component2 の定義
│   │       └── ...
│   │   # 画面の設計が完了して、全体のパフォーマンス目標を確認・最適化します。
│   ├── 08.パフォーマンス設計/
│   │   └── README.md
│   │   # 全体の設計が出揃った後に、エラー管理と例外処理の計画を行います。
│   ├── 09.エラー処理設計/
│   │   └── README.md
│   │   # 最後に特殊な要件や追加的なポイントを検討します。
│   └── 10.その他の考慮事項/
│       └── README.md
│
├── 04.開発ガイド/
│   ├── 01.開発環境/
│   │   └── README.md
│   ├── 02.コーディング規約/
│   │   ├── README.md
│   │   ├── 01.フロントエンド/
│   │   │   └── README.md
│   │   └── 02.バックエンド/
│   │       └── README.md
│   └── 03.テストガイド/
│       ├── README.md
│       ├── 01.TDD/
│       │   ├── README.md
│       │   ├── 01.フロントエンド/
│       │   │   └── README.md
│       │   └── 02.バックエンド/
│       │       └── README.md
│       └── 02.BDD/
│           ├── README.md
│           ├── 01.フロントエンド/
│           │   └── README.md
│           └── 02.バックエンド/
│               └── README.md
│
└── 05.運用保守/
    ├── 01.運用ガイド/
    │   └── README.md
    └── 02.保守ガイド/
        └── README.md
```

## 前提条件

### 共通

| ツール         | タグ                         | 参考                                                    | 備考                                 |
| -------------- | ---------------------------- | ------------------------------------------------------- | ------------------------------------ |
| Docker         | コンテナ化                   | [Docker 公式](https://www.docker.com/)                  | コンテナ技術のデファクトスタンダード |
| Docker Compose | コンテナオーケストレーション | [Docker Compose 公式](https://docs.docker.com/compose/) | 複数のコンテナを管理するためのツール |

### フロントエンド

| ツール                | タグ                      | 参考                                                                                        | 備考                                     |
| --------------------- | ------------------------- | ------------------------------------------------------------------------------------------- | ---------------------------------------- |
| Node.js               | ランタイム                | [Node.js 公式](https://nodejs.org/)                                                         | JavaScript のサーバーサイド実行環境      |
| Yarn                  | パッケージマネージャ      | [Yarn 公式](https://yarnpkg.com/)                                                           | 高速なパッケージ管理ツール               |
| Next.js               | フレームワーク            | [Next.js 公式](https://nextjs.org/)                                                         | React ベースの静的サイトジェネレーター   |
| TypeScript            | 言語                      | [TypeScript 公式](https://www.typescriptlang.org/)                                          | JavaScript に型を提供する言語            |
| Jest                  | テストフレームワーク      | [Jest 公式](https://jestjs.io/ja/)                                                          | JavaScript のテストフレームワーク        |
| React Testing Library | テストユーティリティ      | [React Testing Library 公式](https://testing-library.com/docs/react-testing-library/intro/) | React コンポーネントのテスト用ライブラリ |
| Storybook             | UI コンポーネント         | [Storybook 公式](https://storybook.js.org/)                                                 | UI コンポーネントの開発環境              |
| ESLint                | フォーマット、リンター    | [ESLint 公式](https://eslint.org/)                                                          | JavaScript の静的解析ツール              |
| Stylelint             | フォーマット、リンター    | [Stylelint 公式](https://stylelint.io/)                                                     | CSS の静的解析ツール                     |
| Prettier              | フォーマット              | [Prettier 公式](https://prettier.io/)                                                       | コードフォーマッター                     |
| Cucumber              | BDD、テストフレームワーク | [Cucumber 公式](https://cucumber.io/)                                                       | ビヘイビア駆動開発(BDD)のフレームワーク  |
| Playwright            | E2E テスト                | [Playwright 公式](https://playwright.dev/)                                                  | ブラウザテストのためのツール             |

### バックエンド

| ツール     | タグ                     | 参考                                                  | 備考                                                                                |
| ---------- | ------------------------ | ----------------------------------------------------- | ----------------------------------------------------------------------------------- |
| FastAPI    | フレームワーク           | [FastAPI 公式](https://fastapi.tiangolo.com/)         | 高速で、Python 3.6+の型ヒントを使用したモダンな Web フレームワーク                  |
| Uvicorn    | ASGI サーバ              | [Uvicorn 公式](https://www.uvicorn.org/)              | FastAPI の推奨する非同期サーバ                                                      |
| Gunicorn   | WSGI サーバ              | [Gunicorn 公式](https://gunicorn.org/)                | Uvicorn と組み合わせて使用されることが多い                                          |
| SQLAlchemy | ORM                      | [SQLAlchemy 公式](https://www.sqlalchemy.org/)        | データベース操作を抽象化するためのライブラリ                                        |
| Alembic    | マイグレーションツール   | [Alembic 公式](https://alembic.sqlalchemy.org/)       | データベーススキーマのバージョン管理                                                |
| Pydantic   | データバリデーション     | [Pydantic 公式](https://pydantic-docs.helpmanual.io/) | FastAPI で広く使用される、Python の型ヒントを利用したデータバリデーションライブラリ |
| pytest     | テストフレームワーク     | [pytest 公式](https://docs.pytest.org/en/stable/)     | Python のテストフレームワーク                                                       |
| pytest-cov | カバレッジ               | [pytest-cov 公式](https://pytest-cov.readthedocs.io/) | テストカバレッジを計測するためのプラグイン                                          |
| pytest-bdd | BDD テストフレームワーク | [pytest-bdd 公式](https://pytest-bdd.readthedocs.io/) | BDD テストを実行するためのプラグイン                                                |
| flake8     | リンター                 | [flake8 公式](https://flake8.pycqa.org/en/latest/)    | Python のリンター                                                                   |
| black      | フォーマッタ             | [black 公式](https://black.readthedocs.io/en/stable/) | Python のフォーマッタ                                                               |
| isort      | ソートツール             | [isort 公式](https://pycqa.github.io/isort/)          | Python の import 文をソートするツール                                               |
| mypy       | 型チェッカ               | [mypy 公式](https://mypy.readthedocs.io/en/stable/)   | Python の型チェッカ                                                                 |
