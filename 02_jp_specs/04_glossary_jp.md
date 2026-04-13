# 04_glossary_jp

## 目的
日本版で用語揺れを防ぐための正規語を定義する。  
本ファイルを用語正規表の正本とする。

| 用語 | 正規語として使うか | 用語カテゴリ | 定義 | 非推奨語 / 使わない語 | 本家英語見出し対応 | 備考 |
|---|---|---|---|---|---|---|
| AI社員 | 使う | 役割語 | 日本企業文脈での総称。業務上の役割を持つ AI の総称。 | なし | Agent / Agent Role | 日本版本文の標準表記として使う |
| AIエージェント | 使う | 役割語 | 仕様上の一般概念。agent specification の単位。 | なし | Agent / Agent Specification | 本家対応説明時の表記として使う |
| 業務AI | 使う | 役割語 | 日本版で業務実行を担う AI。 | 汎用AI | Agent Role | 実行系AIと混同しない |
| 実行系AI | 使う | 役割語 | 業務別の実務処理を担う AI 群。 | 作業AI | Agent Role | `05_official_agents_jp_mapping.md` で使用 |
| 構造検証 | 使う | 制御語 | template / decomposition / handoff の妥当性を確認する機能の総称。 | MECEチェック（総称としては使わない） | Validation / Enforceable_Standards | validation の日本語正規語 |
| validation | 参照語 | 制御語 | 構造検証・妥当性確認の英語参照語。 | 単独の日本語正規語扱いはしない | Validation | 単独正本にしない |
| HITL条件 | 使う | Human語 | 人間介入が必要となる条件。 | 承認条件（総称としては使わない） | Human-in-the-Loop_(HITL)_Triggers | trigger と区別する |
| HITLトリガー | 使う | Human語 | HITL条件が発火した具体イベント。 | HITL発火点 | Human-in-the-Loop_(HITL)_Triggers | 本家見出し対応あり |
| HITL制御 | 使う | 制御語 | HITL条件とトリガーを踏まえて NotifyHuman 等へ接続する制御。 | HITL運用 | Human-in-the-Loop / Notification | Protocol側概念 |
| handoff artifact | 使う | Artifact語 | 引き継ぎに使う成果物。task packet / handoff note / validation report 等を含む。 | 引き継ぎ資料（曖昧語としては使わない） | Core_Data_Contracts | Artifact名として使用 |
| handoff context | 使う | Artifact語 | 引き継ぎ時に必要な文脈情報。 | handoff情報（曖昧語としては使わない） | Coordination_Patterns / Memory_Architecture | Artifactそのものとは分ける |
| correlation_id | 使う | 接続語 | protocol / artifact / governance をまたいで追跡可能性を確保する共通参照キー。 | 相関ID（本文正規語にはしない） | Core_Data_Contracts / Observability_Requirements | 共通参照キーとして使用 |
| task packet | 使う | Artifact語 | 委譲・実行依頼・次工程連携のために渡す task 単位の成果物。 | task情報（曖昧語としては使わない） | Core_Data_Contracts | handoff artifact と関係する独立 artifact |
| validation report | 使う | Artifact語 | validation 結果を記録・参照する成果物。 | validation結果メモ | Validation / Enforceable_Standards | `protocol-structure-validation-jp.md` の出力参照先として使用 |
| validation 分類 | 参照語 | 制御語 | template validation / decomposition validation / handoff validation などの分類名。 | validation系 protocol 群（総称としては使わない） | Validation | 新規 protocol を増やす前提ではなく、既存 `protocol-structure-validation-jp.md` の傘分類として扱う |

## 運用ルール
- 他ファイルは本ファイルの正規語に合わせる。
- 新しい用語を追加する場合は、decision_log に判断を残してから追記する。
- 正規語を優先使用する。
- 参照語は本家対応説明時のみ使う。
- 非推奨語 / 使わない語は本文正規表記に使わない。
- 日本版本文の標準表記は `AI社員` とし、本家対応説明時は `AIエージェント` を使う。
- validation 分類語は、既存 `protocol-structure-validation-jp.md` の傘分類として扱い、新規 protocol 名の正本とはみなさない。
