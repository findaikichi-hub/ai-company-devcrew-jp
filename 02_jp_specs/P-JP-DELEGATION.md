# P-JP-DELEGATION: 日本版 標準委譲プロトコル

## Metadata
- Protocol ID: P-JP-DELEGATION
- Category: Japanese Operations / Coordination
- Version: 0.1
- Status: Draft
- Base Reference: P-DELEGATION-DEFAULT
- Owner: Orchestrator
- Applicable Agents: Orchestrator, PMO / プロジェクト管理AI, 設計統括AI, 業務実行系AI, ナレッジ管理AI

---

## Objective
日本企業向け AI社員運用において、タスク委譲を標準化する。

本プロトコルは以下を目的とする。
- agent 間の委譲を artifact ベースで明確にする
- 会話依存ではなく、task packet / acceptance criteria / handoff 条件で委譲する
- 承認要否、稟議要否、人間関与条件を委譲時点で明示する
- 責任分界と監査証跡を残す
- 後続工程で再利用可能な委譲記録を残す

---

## Position in Architecture
本プロトコルは Agent ではなく Protocol である。
委譲の判断主体は個別 agent の裁量に依存せず、Orchestrator と周辺 protocol 群に接続される。

接続先:
- Orchestrator
- P-HANDOFF 相当
- Template Validation / 構造検証
- Quality Gate
- NotifyHuman / HITL

---

## Trigger
以下のいずれかで起動する。

- 上位目標を Orchestrator が分解し、別 agent へ処理を委譲する必要がある
- ある agent が、自身の責務外または専門外の処理を別 agent に渡す必要がある
- ある成果物を別工程へ引き継ぐ必要がある
- 検証、再作業、補足調査のために再委譲が必要である
- 稟議、社内説明、監査用に委譲記録を明示的に残す必要がある

---

## Non-Goals
本プロトコルは以下を目的としない。

- 雑な口頭依頼の代替
- direct agent-to-agent 会話の自由化
- 完了判定の代替
- 構造検証の代替
- 人間の常時承認フローの代替

---

## Required Inputs
委譲時には最低限以下を持つこと。

- task_summary
- purpose
- source_agent
- target_agent
- deliverables
- acceptance_criteria
- deadline_or_priority
- required_artifacts
- downstream_consumer
- risk_flags
- hitl_requirement
- ringi_requirement
- audit_requirement

---

## Core Principle
委譲は会話ではなく artifact で行う。

委譲時に最低限生成または更新される artifact:
- task_packet.md または task_packet.json
- delegation_record.md
- 必要に応じて reference links / source artifacts
- 完了後は validation_report または handoff note

---

## Task Packet Schema (Minimum)
以下を日本版の最小 task packet 項目とする。

```yaml
task_packet:
  task_id: ""
  title: ""
  purpose: ""
  source_agent: ""
  target_agent: ""
  business_context: ""
  requested_action: ""
  deliverables:
    - ""
  acceptance_criteria:
    - ""
  required_inputs:
    - ""
  constraints:
    - ""
  deadline_or_priority: ""
  downstream_consumer: ""
  risk_flags:
    contains_pii: false
    external_impact: false
    policy_change: false
    financial_impact: false
    unresolved_ambiguity: false
  hitl_requirement:
    required: false
    reason: ""
  ringi_requirement:
    required: false
    reason: ""
  audit_requirement:
    required: true
    retention_note: ""
