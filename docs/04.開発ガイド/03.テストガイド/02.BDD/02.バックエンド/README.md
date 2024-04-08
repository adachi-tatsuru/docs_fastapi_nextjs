# バックエンドの振る舞い駆動開発 (BDD)

## 概要

このドキュメントでは、FastAPI を使用したバックエンド開発における振る舞い駆動開発 (BDD) のプロセスと手法について説明します。
BDD は、ソフトウェアの振る舞いに焦点を当てた開発手法で、ステークホルダーとの共通の理解に基づいてシステムを開発します。
本プロジェクトでは、pytest-bdd を使用して、BDD のプラクティスを実践します。

## BDD のプロセス

1. 機能の明確化 (Feature)
   - ステークホルダーとの話し合いを通じて、開発する機能を明確にします。
   - 機能の詳細を Gherkin 構文で記述したフィーチャーファイルを作成します。
2. シナリオの定義 (Scenario)
   - フィーチャーを実現するためのシナリオを定義します。
   - シナリオは、Given（前提条件）、When（アクション）、Then（期待結果）の形式で記述します。
3. ステップ定義の実装 (Step Definition)
   - シナリオを実行するためのステップ定義を、Python で実装します。
   - ステップ定義では、シナリオの Given、When、Then に対応するコードを記述します。
4. テストの実行と結果の確認
   - pytest-bdd を使用して、フィーチャーファイルに定義されたシナリオを実行します。
   - テストの結果を確認し、失敗したシナリオについては、原因を特定して修正します。
5. リファクタリングとメンテナンス
   - テストが安定した状態で、コードのリファクタリングを行います。
   - 新しい要件や変更に合わせて、フィーチャーファイルとステップ定義を更新します。

## 利用ツール・ライブラリ

- BDD フレームワーク: pytest-bdd
- Web フレームワーク: FastAPI
- HTTP クライアント: httpx
- モックライブラリ: pytest-mock

## ディレクトリ構造

```
features/
  ├── steps/
  │   └── *.py
  └── *.feature
tests/
  ├── conftest.py
  └── test_*.py
```

- `features/`: BDD のテストに関連するファイルを格納するディレクトリ
  - `steps/`: ステップ定義ファイル（Python）を格納するディレクトリ
  - `*.feature`: Gherkin 構文で記述されたフィーチャーファイル
- `tests/`: 単体テストや統合テストのファイルを格納するディレクトリ
  - `conftest.py`: テストの設定や前処理を定義するファイル
  - `test_*.py`: 単体テストや統合テストのファイル

## フィーチャーファイルの記述方法

```gherkin
Feature: ユーザー管理
  ユーザーを管理できるようにする

  Scenario: 新しいユーザーを作成する
    Given ユーザー作成APIのエンドポイントが存在する
    When 以下の情報でユーザー作成APIをコールする:
      | name   | email           |
      | John   | john@example.com |
    Then ステータスコードが201であること
    And レスポンスボディにユーザーの情報が含まれていること
```

- `Feature`: フィーチャーの名前と説明を記述します。
- `Scenario`: テストするシナリオを記述します。
- `Given`、`When`、`Then`: シナリオのステップを記述します。

## ステップ定義の実装方法

```python
from pytest_bdd import given, when, then, scenarios
from fastapi.testclient import TestClient
from main import app

scenarios('features/user_management.feature')

@given('ユーザー作成APIのエンドポイントが存在する')
def user_creation_endpoint():
    client = TestClient(app)
    response = client.post('/users')
    assert response.status_code != 404

@when('以下の情報でユーザー作成APIをコールする')
def create_user(user):
    client = TestClient(app)
    response = client.post('/users', json=user)
    assert response.status_code == 201
    return response

@then('ステータスコードが201であること')
def check_status_code(create_user):
    assert create_user.status_code == 201

@then('レスポンスボディにユーザーの情報が含まれていること')
def check_response_body(create_user):
    user = create_user.json()
    assert 'id' in user
    assert user['name'] == 'John'
    assert user['email'] == 'john@example.com'
```

- `scenarios`: フィーチャーファイルのパスを指定します。
- `given`、`when`、`then`: フィーチャーファイルのステップに対応する関数を定義します。
- `TestClient`: FastAPI のテストクライアントを使用して、API のエンドポイントをテストします。

## テストの実行方法

```
pytest --bdd features/
```

- `pytest --bdd`: pytest-bdd を使用してテストを実行するコマンド
- `features/`: テストするフィーチャーファイルが格納されたディレクトリを指定します。

## ベストプラクティス

- シナリオは独立して実行できるようにする
- ステップ定義は再利用可能で、メンテナンスしやすいようにする
- フィーチャーファイルは、ドメイン専門家や非技術者にも理解しやすい言葉で記述する
- テストデータは、フィーチャーファイルとステップ定義で分離する
- テストの実行速度に配慮し、必要に応じてタグを使用してテストを分類する
