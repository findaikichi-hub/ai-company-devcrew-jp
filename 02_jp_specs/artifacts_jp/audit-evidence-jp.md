# audit-evidence-jp

## 目的
日本企業における監査証跡として、何をどの粒度で残すべきかの骨格を定義する。

## 位置づけ
本ファイルは、監査証跡を表す artifact 標準の第二稿とする。  
handoff artifact の代替ではなく、監査・追跡・説明責任のための独立 artifact を定義する。

## 扱う対象
- 判断根拠
- 実行履歴
- 承認履歴
- 差戻し履歴
- 参照元
- 変更履歴
- 追跡識別子

## 入力
本ファイルで証跡化対象とする入力カテゴリは以下。
- 判断イベント
- 実行イベント
- 承認イベント
- 差戻しイベント
- 参照元情報
- 関連 artifact 参照情報
- 関連 protocol 実行結果参照情報
- 変更前後差分参照情報

※ ここで定義するのは入力カテゴリであり、完全 schema や固定フォーマットではない。

## 出力
本ファイルで残す出力カテゴリは以下。
- audit evidence 本体
- 最小項目を含む証跡記録
- 関連 artifact 参照
- 関連 protocol 実行結果参照
- validation / approval 結果参照
- 次アクション参照

## 基本原則
- 監査証跡は handoff 専用 artifact に吸収しない。
- 後から「誰が・何を・なぜ」判断したかを追える粒度を確保する。
- 必要以上の本文複製ではなく、追跡可能性を優先する。
- 参照元不明の記録を正規証跡として扱わない。

## 監査証跡の最小項目
- correlation_id
- 対象タスク / 対象案件
- 実施日時
- 実施主体
- 判断内容
- 判断根拠
- 参照元
- 承認 / 差戻し有無
- 次アクション

## 追跡性
監査証跡は、少なくとも以下を満たす。
- 後から「誰が・何を・なぜ」判断したか追えること
- 参照元不明の記録を正規証跡にしないこと
- 手戻りや差戻しの履歴が消えないこと
- 関連 artifact と関連 protocol 実行結果へ接続できること
- 変更前後差分が参照可能であること

## 参照関係

### handoff artifact との関係
- handoff artifact に含まれる判断・差戻し・承認情報のうち、監査上必要なものは audit evidence から参照可能にする。
- ただし、audit evidence は handoff artifact の代替としない。
- handoff 本文そのものを audit evidence に複製しない。

### protocol 実行結果との関係
- 関連する protocol 実行結果は、audit evidence から参照可能にする。
- protocol 手順本文そのものは audit evidence に取り込まない。
- 実行結果は、判断や差戻しの根拠確認に必要な範囲で参照する。

### validation / approval 結果参照
- validation 結果は、判断根拠または前進可否の参照先として扱う。
- approval 結果は、承認有無・差戻し有無・次アクション確認の参照先として扱う。
- validation / approval の完全本文や制度詳細は本ファイルで保持しない。

## 参照性の骨格
- 人間が監査時に読めること
- 後続AIが状態理解に使えること
- 変更前後差分が確認できること

## 非対象
本ファイルの非対象は以下。
- handoff artifact の完全本文
- protocol 手順本文
- governance 規程本文
- 社内制度固定値
- 保存期間 / 媒体 / 監査頻度の確定値
- 承認権限規程そのもの
- Orchestrator の全体制御手順
- Context Manager の鮮度管理ルール全文

## 接続先
- `02_jp_specs/03_jp_requirement_placement_map.md`
- `03_decisions/decision_log.md`
- `02_jp_specs/04_glossary_jp.md`
- `02_jp_specs/01_ai_employee_spec_jp.md`
- `02_jp_specs/agents_jp/agent-Orchestrator-jp.md`
- `02_jp_specs/agents_jp/agent-Context-Manager-jp.md`

## 注記
- 本ファイルは第二稿であり、本文完成版ではない。
- 保存期間・媒体・監査実施頻度は確定しない。
- handoff artifact 標準とは分離して保持する。
- protocol / governance / agent の本文責務は本ファイルに混入させない。
