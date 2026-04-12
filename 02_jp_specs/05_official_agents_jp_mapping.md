# 05_official_agents_jp_mapping

## 目的
本家 DevCrew_s のエージェント構造を、日本版として再編する。

本ファイルでは、以下の2軸で整理する。

- 役割再編（Role Recomposition）
- 機能接続（Function / Protocol Integration）

単純な1対1マッピングは行わない。

---

## 1. 前提（本家整合）

本家は以下の4レイヤーで構成される。

- Agent: 役割定義
- Protocol: 標準化された手順
- Human: 方針判断・例外承認・HITL
- Artifact: handoff / task_packet / validation_report 等

日本版でもこの構造を維持する。

---

## 2. 日本版の役割再編

### ■ 制御レイヤー

| 日本版 | 本家対応 | 役割 |
|---|---|---|
| Orchestrator | Orchestrator | タスク分解、委譲、全体制御、quality gate挿入 |
| Context Manager | Context Manager | 記憶管理、ログ、handoff情報管理 |

---

### ■ 業務実行レイヤー（統合）

| 日本版 | 本家構成 | 役割 |
|---|---|---|
| PMO / プロジェクト管理AI | Project Manager + Product Owner + Business Analyst | 計画、優先順位、進行管理、要件整理 |
| 設計統括AI | System Architect | 設計方針、構造定義、技術判断 |
| ナレッジ管理AI | Knowledge系 | 情報検索、整理、再利用 |
| 実行系AI（業務別） | 各専門Agent | 実務処理 |

---

## 3. 日本版で追加する機能（Agent化しない）

---

### ■ 完了判定機能

接続先：
- Orchestrator
- Quality Gate

役割：
- 完了条件の確認
- artifactの充足確認
- 次工程への受け渡し可否判定

判定基準：
- 目的達成
- 矛盾なし
- 必須要素充足
- 次工程で使用可能

実装：
- validation_report
- quality gate

---

### ■ 構造検証機能

接続先：
- Template Validation
- Decomposition Validation
- Handoff Validation

役割：
- 抜け漏れ検出
- 重複検出
- 粒度の不整合検出

適用対象：
- 要件
- タスク分解
- handoff context

※ 全文書への一律適用はしない

---

### ■ 日本版 HITL 制御

接続先：
- NotifyHuman
- Orchestrator

役割：
- 人間呼び出し条件の制御

人間の役割：
- 方針判断
- 例外承認
- HITL責任

---

### ■ 日本版業務プロトコル

例：
- 稟議プロトコル
- 承認フロー
- 社内報告プロトコル

---

## 4. 機能接続構造

Orchestrator
- Delegation
- Handoff
- Quality Gate（完了判定）
- Validation（構造検証）
- NotifyHuman（HITL）
- Context Manager

Context Manager
- Short-term memory
- Long-term memory
- Shared memory
- Handoff data

各業務AI
- タスク実行
- artifact生成
- validation対象

---

## 5. 設計原則

- Agentを増やさない（機能はProtocolで実装）
- 会話に依存しない（artifact + protocolで反復）
- 完了は構造で決まる（自己申告禁止）
- 人間は例外責任のみ

---

## 6. 次アクション

- 本家エージェントの責務分解
- 日本版再編の確定
- 各AIテンプレート作成
- 日本版プロトコル設計
