# handoff-artifact-standard-jp

## 目的
日本企業向け運用において、作業途中または工程完了時に、次工程へ引き継ぐための handoff artifact の骨格を定義する。

## 位置づけ
本ファイルは、handoff artifact を表す artifact 標準の第二稿とする。  
次工程へ渡すための受け渡し artifact を定義するものであり、監査・追跡・説明責任を主目的とする `audit-evidence-jp.md` の代替ではない。

## 扱う対象
- 次工程へ渡す作業結果
- 次工程で必要となる前提情報
- 未完了事項
- 保留事項
- 差戻し理由の引き継ぎ
- 再開条件
- 関連参照先
- handoff context

## 共通参照キー
handoff artifact が最低限持つ共通参照キーは以下。
- correlation_id
- 対象タスク / 対象案件 ID
- 日時
- 主体
- 関連 artifact 参照 ID

## 最小項目
handoff artifact の最小項目は、少なくとも以下を持つ。
- correlation_id
- 対象タスク / 対象案件 ID
- handoff 元
- handoff 先
- handoff 実施日時
- 現在状態
- 引き継ぐ対象
- 完了済み事項
- 未完了事項
- 保留事項
- 次アクション
- 参照先
- 再開条件

## 正本で持つ本文
handoff artifact が正本で持つ本文は以下。
- handoff 元
- handoff 先
- handoff 実施日時
- 現在状態
- 引き継ぐ対象
- 完了済み事項
- 未完了事項
- 保留事項
- 次アクション
- 再開条件
- handoff context への参照
- 次工程が再開するための最小本文

## 参照で済ませる本文
handoff artifact に複製せず、参照で済ませる本文は以下。
- audit evidence の詳細判断本文
- protocol 実行結果
- validation 結果
- approval 結果
- decision log
- task packet
- validation report
- handoff context の詳細本文

## task packet / validation report / handoff context の位置づけ
- task packet は関連 artifact として参照する。
- validation report は独立 artifact / result として参照する。
- handoff context は context 単位として参照する。
- これらを handoff artifact 本文へ吸収統合しない。

## 参照先 / 接続先
handoff artifact は、必要に応じて以下を参照可能にする。
- 関連 protocol 実行結果
- 関連 artifact
- 関連 decision log
- 関連 validation 結果
- 関連 approval 結果
- 関連 handoff context
- 関連 task packet
- 関連 validation report

## handoff artifact の役割
handoff artifact は、次工程が再解釈なしで作業再開できるようにするための受け渡し単位である。  
そのため、何を渡すか、どこまで終わっているか、何が未了か、何を次にやるかが読める粒度を優先する。

## audit evidence との境界
- handoff artifact は、次工程への受け渡しを目的とする。
- audit evidence は、監査・追跡・説明責任を目的とする。
- handoff artifact に監査上重要な判断が含まれる場合でも、監査証跡の正本は `audit-evidence-jp.md` 側で保持する。
- handoff artifact は audit evidence の代替としない。
- audit evidence から handoff artifact を参照可能にしてよいが、両者を吸収統合しない。

## 非対象
本ファイルの非対象は以下。
- audit evidence の詳細判断本文
- protocol 手順本文
- governance 規程本文
- agent 制御本文
- 社内制度固定値
- artifact schema 完成版
- 承認権限規程そのもの
- Orchestrator の全体進行管理
- Context Manager の鮮度管理ルール全文

## 注記
- 本ファイルは第二稿であり、本文完成版ではない。
- task packet、handoff context、validation report の最終 schema は今後確定する。
- `03_jp_requirement_placement_map.md` の配置先定義に基づく実ファイル化である。
- `audit-evidence-jp.md` と競合させず、参照関係で接続する。
