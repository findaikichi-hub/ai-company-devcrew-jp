# 05_official_agents_jp_mapping

## 目的
本家 DevCrew_s のエージェント構造を、日本版として再編する。

本ファイルでは、以下の2軸で整理する。
- 役割再編（Role Recomposition）
- 機能接続（Function / Protocol Integration）

単純な1対1マッピングは行わない。  
本ファイルは、日本版における Agent ⇄ Protocol ⇄ Artifact ⇄ Governance の接続面を整理する主文書とする。  
ただし、各 agent / protocol / artifact / governance 本文そのものの正本ではない。

---

## 1. 前提（本家整合）

本家は以下の4レイヤーで構成される。
- Agent: 役割定義
- Protocol: 標準化された手順
- Human: 方針判断・例外承認・HITL
- Artifact: handoff / task packet / validation report 等

日本版でもこの構造を維持する。

※ 本ファイルは agent再編と責務接続の整理を行う。  
※ agent責務の正本は `agents_jp/*.md` に置く。  
※ protocol / artifact / governance の詳細本文は各ファイルを正本とし、本ファイルは接続整理の主文書に留める。

---

## 2. 日本版の役割再編

### ■ 制御レイヤー

| 日本版 | 本家対応 | 役割 | 正本 |
|---|---|---|---|
| Orchestrator | Orchestrator | タスク分解、委譲、全体制御、quality gate 接続を担う制御中枢。責務の全量は agent別仕様で保持する。 | `agents_jp/agent-Orchestrator-jp.md` |
| Context Manager | Context Manager | 記憶管理、handoff、共有状態保持を担う文脈管理中枢。責務の全量は agent別仕様で保持する。 | `agents_jp/agent-Context-Manager-jp.md` |

### ■ 業務実行レイヤー（統合）

| 日本版 | 本家構成 | 役割 |
|---|---|---|
| PMO / プロジェクト管理AI | Project Manager + Product Owner + Business Analyst | 計画、優先順位、進行管理、要件整理 |
| 設計統括AI | System Architect | 設計方針、構造定義、技術判断 |
| ナレッジ管理AI | Knowledge系 | 情報検索、整理、再利用 |
| 実行系AI（業務別） | 各専門Agent | 実務処理 |

---

## 3. 日本版で追加する機能（Agent化しない）

### ■ 完了判定機能
接続先：
- Orchestrator
- Quality Gate

役割：
- 完了条件の確認
- artifactの充足確認
- 次工程への受け渡し可否判定

実装：
- `protocol-completion-gate-jp.md`
- 関連 artifact / protocol 参照
- 詳細は protocol別仕様で扱う

### ■ 構造検証機能
接続先：
- 構造妥当性確認
- 差戻し / 再提出
- completion gate 前段

役割：
- 抜け漏れ検出
- 重複検出
- 粒度不整合検出

実装：
- `protocol-structure-validation-jp.md`
- validation 分類は新規 protocol を増殖させず、本 protocol を傘として扱う

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

実装：
- `protocol-hitl-jp.md`

### ■ 日本版業務プロトコル
例：
- `protocol-ringi-jp.md`
- `protocol-approval-flow-jp.md`

---

## 4. 機能接続構造

### Orchestrator の接続カテゴリ
- Coordination pattern: Delegation / Handoff / Quality Gate / Validation / NotifyHuman
- Data contract: task packet / validation report / handoff artifact
- Resource / permission: 実行枠・優先度・権限制御への接続
- Recovery / rollback: failure recovery / transactional rollback への接続
- Observability / notification: workflow 監視 / 通知 / escalation への接続
- Context connection: Context Manager

### Context Manager の接続カテゴリ
- Coordination pattern: handoff / shared memory / state transfer
- Data contract: handoff artifact / cache artifact / context record
- Resource / permission: cache / persistent memory / shared state への接続
- Recovery / rollback: context recovery / stale context 回避 / retention 管理
- Observability / notification: cache監視 / freshness確認 / violation通知 への接続

### 各業務AI の接続カテゴリ
- task execution
- artifact生成
- validation対象
- handoff対象

※ Orchestrator / Context Manager の責務詳細は本ファイルで完結させず、agent別仕様を正本とする。

---

## 5. 主要 protocol 群の接続整理

| protocol | 主目的 | 主な接続元 | 主な接続先 | 備考 |
|---|---|---|---|---|
| `protocol-ringi-jp.md` | 起案内容側の確認 | 実行系AI / PMO / Orchestrator | `protocol-approval-flow-jp.md` / `protocol-hitl-jp.md` / `handoff-artifact-standard-jp.md` | 起案内容・必要添付・差戻し条件を扱う |
| `protocol-approval-flow-jp.md` | 承認状態遷移の確認 | `protocol-ringi-jp.md` / Orchestrator | `protocol-hitl-jp.md` / `protocol-completion-gate-jp.md` / `audit-evidence-jp.md` | 承認状態・差戻し・例外承認を扱う |
| `protocol-hitl-jp.md` | 人間介入条件・トリガー・制御 | 承認系 protocol / governance 条件 / Orchestrator | Human / `protocol-completion-gate-jp.md` / `handoff-artifact-standard-jp.md` / `audit-evidence-jp.md` | HITL条件・HITLトリガー・HITL制御の正本 |
| `protocol-structure-validation-jp.md` | 構造妥当性確認 | Orchestrator / 各業務AI / handoff対象 | 差戻し / 再提出 / `protocol-completion-gate-jp.md` / `validation report` | validation 分類は本 protocol を傘とする |
| `protocol-completion-gate-jp.md` | 完了可否の最終判定 | `protocol-structure-validation-jp.md` / `protocol-approval-flow-jp.md` / `protocol-hitl-jp.md` | 次工程 / 差戻し / 保留 / HITL / `handoff-artifact-standard-jp.md` | 完了判定の最終受け皿 |

---

## 6. artifact / governance との接続整理

### artifact の役割差
- `audit-evidence-jp.md`
  - 監査・追跡・説明責任の正本
  - 判断根拠、実行履歴、承認履歴、差戻し履歴を保持する
- `handoff-artifact-standard-jp.md`
  - 次工程への受け渡しの正本
  - handoff元 / handoff先 / 現在状態 / 次アクション / 再開条件を保持する

※ audit evidence と handoff artifact は相互参照してよいが、本文を吸収統合しない。

### governance の役割差
- `privacy-handling-jp.md`
  - 情報種別起点の共有可否 / 制約を扱う
- `external-collaboration-jp.md`
  - 外部共有起点の条件 / 責任境界を扱う

※ governance 文書は統制本文の正本であり、protocol 側は接続条件のみ扱う。

---

## 7. 共通参照キーと接続面の考え方
接続面で最低限そろえる共通参照キーは以下。
- `correlation_id`
- 対象タスク / 対象案件 ID
- 日時
- 主体
- 関連 artifact 参照 ID

これらは、protocol / artifact / governance をまたいで追跡可能性を維持するための最小集合とする。

---

## 8. 設計原則
- Agentを増やさない（機能はProtocolで実装）
- 会話に依存しない（artifact + protocolで反復）
- 完了は構造で決まる（自己申告禁止）
- 人間は例外責任のみ
- 接続面の主文書と本文正本を混同しない
- validation 分類は、まず既存 `protocol-structure-validation-jp.md` を傘として扱う

---

## 9. 次アクション
- agent別仕様の skeleton 維持
- 接続面の用語正規を glossary 側で固定
- 接続面固定の判断を decision_log に追記
- 各本文の完成版化は別サイクルで扱う
