# protocol-completion-gate-jp

## 目的
日本版運用において、次工程へ進めてよいか / 完了扱いにしてよいかの最終判定を行う protocol を定義する。

## 位置づけ
本ファイルは、completion gate を扱う protocol 別仕様の skeleton 初稿とする。  
`protocol-structure-validation-jp.md` の代替ではなく、構造妥当性確認の後段で最終判定を受ける受け皿である。  
`protocol-hitl-jp.md` の代替でもなく、HITL 接続そのものの設計を置き換えない。  
governance 文書の代替でもなく、artifact schema 本文の代替でもない。  
protocol 別仕様として、完了可否の最終判定受け皿を定義する。

## 扱う対象
- completion 判定条件
- 前進可否条件
- 差戻し条件
- 保留条件
- HITL 接続条件
- completion 判定結果の出力骨格
- 次工程へ進めるか / 戻すか / 停止するかの判定接続

## 基本原則
- structure validation 結果を前提に扱う。
- 内容妥当性・承認状態・HITL 要否・必要参照先の有無を踏まえて最終判定する。
- artifact schema 完成版をここに吸収しない。
- governance 本文をここに吸収しない。
- Orchestrator / Context Manager の制御本文をここに吸収しない。
- 承認経路全文や状態遷移全文をここに吸収しない。
- 完了不可の場合は、差戻し / 保留 / HITL のどこへ接続するかを読めるようにする。

## completion 判定条件
completion gate で最低限扱う判定条件は以下。
- structure validation 結果が確認できる
- 必要な承認状態または判定状態が確認できる
- 必要参照先が揃っている
- 差戻し未解消事項が残っていない
- 前進停止条件に該当していない
- 次工程へ渡すための最低限の条件が満たされている

## 前進可否条件
次工程へ進める条件の骨格は以下。
- 構造妥当性が確保されている
- 必須条件不足が解消されている
- 承認または確認が必要な箇所が未処理で残っていない
- 必要な artifact / protocol 参照先が確認できる
- 保留または停止理由が残っていない

## 差戻し条件
差戻しは、主として completion 判定に必要な条件が不足している場合に行う。  
差戻し条件の骨格は以下。
- structure validation の未解消不備がある
- 必要参照先が不足している
- 承認または確認結果が不足している
- 完了扱いに必要な条件が満たされていない
- 次工程へ渡すには不足が大きい

## 保留条件
以下の場合は、完了扱いにも差戻しにも直ちに決めず保留する。
- 人間判断待ちである
- 必要参照先の到着待ちである
- 例外判断待ちである
- 前進可否を即断できない
- completion 判定に必要な一部条件が未確定である

## HITL 接続条件
以下の場合は `protocol-hitl-jp.md` 側の接続を前提にする。
- 完了可否の最終判断に人間確認が必要
- 高リスク判断が必要
- 例外承認や例外処理が必要
- 条件不足か保留か差戻しかを AI のみで決めるべきでない
- governance 条件や承認状態に関する人間判断が必要

## completion 判定結果の出力骨格
completion 判定結果として最低限出力する骨格は以下。
- 対象ファイル / 対象案件
- 判定日時
- 判定主体
- 完了可否
- 次工程へ進めるか / 戻すか / 停止するか
- 差戻し要否
- 保留要否
- HITL 接続要否
- 判定根拠の参照先

## 次工程へ進めるか / 戻すか / 停止するかの判定接続
completion gate 後の接続は以下を基本とする。
- 次工程へ進める
- 差戻しへ戻す
- 保留のまま停止する
- HITL へ接続する
- 関連 artifact / protocol 参照へ戻る

## 境界

### structure validation との境界
- `protocol-structure-validation-jp.md` は構造妥当性確認を扱う。
- 本ファイルは、その結果を前提に完了可否の最終判定を扱う。
- 本ファイルは structure validation 本文そのものを持たない。

### HITL protocol との境界
- `protocol-hitl-jp.md` は人間介入条件・トリガー・制御を扱う。
- 本ファイルは completion 判定時の HITL 接続要否を扱う。
- 人間介入接続そのものの設計は `protocol-hitl-jp.md` 側で扱う。

### 承認系 protocol との境界
- `protocol-ringi-jp.md` は起案内容側を扱う。
- `protocol-approval-flow-jp.md` は承認状態遷移側を扱う。
- 本ファイルは、起案内容や承認状態そのものではなく、完了可否の最終判定を扱う。

### artifact との境界
- `audit-evidence-jp.md` は監査・追跡・説明責任の artifact である。
- `handoff-artifact-standard-jp.md` は受け渡し artifact である。
- 本ファイルは artifact schema 本文を持たず、必要時に参照接続する。

### governance との境界
- `privacy-handling-jp.md` と `external-collaboration-jp.md` は統制本文を扱う。
- 本ファイルは統制本文そのものではなく、完了可否の判定を扱う。

### agent との境界
- Orchestrator / Context Manager の制御本文は本ファイルで扱わない。
- 本ファイルは局所的な completion gate protocol に留まる。

## 非対象
本ファイルの非対象は以下。
- 法令 / 社内制度固定値
- 承認権限規程本文
- artifact schema 完成版
- governance 規程本文
- agent 制御本文
- 承認経路全文
- 状態遷移全文
- completion gate の完成版フロー設計

## 参照先
- `02_jp_specs/protocols_jp/protocol-structure-validation-jp.md`
- `02_jp_specs/protocols_jp/protocol-hitl-jp.md`
- `02_jp_specs/protocols_jp/protocol-ringi-jp.md`
- `02_jp_specs/protocols_jp/protocol-approval-flow-jp.md`
- `02_jp_specs/artifacts_jp/audit-evidence-jp.md`
- `02_jp_specs/artifacts_jp/handoff-artifact-standard-jp.md`
- `02_jp_specs/governance_jp/privacy-handling-jp.md`
- `02_jp_specs/governance_jp/external-collaboration-jp.md`
- `02_jp_specs/03_jp_requirement_placement_map.md`
- `02_jp_specs/04_glossary_jp.md`

## 注記
- 本ファイルは skeleton 初稿であり、本文完成版ではない。
- completion 判定結果の最終 schema や各条件のしきい値は今後確定する。
- structure validation 結果を前提に扱うが、その本文自体は本ファイルに複製しない。
