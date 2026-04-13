# protocol-structure-validation-jp

## 目的
日本版運用において、成果物や引き継ぎ内容の構造妥当性を確認する protocol を定義する。

## 位置づけ
本ファイルは、構造妥当性確認を扱う protocol 別仕様の skeleton 初稿とする。  
completion gate の代替ではなく、完了判定の前段で構造妥当性を確認する受け皿である。  
HITL protocol の代替でもなく、artifact schema 本文の代替でもない。  
protocol 別仕様として、構造妥当性確認の受け皿を定義する。

## 扱う対象
- 構造検証条件
- 構造不備の検知
- 必須項目不足の検知
- 差戻し条件
- 再提出条件
- validation 結果の出力骨格
- 次工程へ進めるか / 戻すかの判定接続

## 基本原則
- 内容の正しさ全文ではなく、まず構造妥当性を扱う。
- artifact schema 完成版をここに吸収しない。
- governance 本文をここに吸収しない。
- Orchestrator / Context Manager の制御本文をここに吸収しない。
- completion 判定全文をここに吸収しない。
- 構造不備は再提出可能な粒度で返す。

## 構造検証条件
構造妥当性確認で最低限扱う条件は以下。
- 必須見出しまたは必須区分が存在する
- 必須参照先が確認できる
- 正本で持つべき本文と参照で済ませる本文が混在していない
- 対象ファイルの責務境界が読める
- 非対象が明示されている
- 用語が既存 glossary と大きく矛盾していない

## 構造不備の検知
以下のいずれかに該当する場合、構造不備として扱う。
- 必須見出し不足
- 必須項目不足
- 正本 / 参照の線引き不明
- 境界不明
- 非対象未記載
- 参照先不足
- 用語揺れにより責務が曖昧

## 必須項目不足の検知
必須項目不足として最低限検知する対象は以下。
- 目的
- 位置づけ
- 扱う対象
- 基本原則
- 境界または非対象
- 出力または結果の骨格
- 参照先

## 差戻し条件
差戻しは、主として構造妥当性が不足している場合に行う。  
差戻し条件の骨格は以下。
- 必須見出し不足
- 必須項目不足
- 境界が読めない
- 他レイヤー責務を吸収している
- 正本 / 参照の線引きが不明
- 次工程へ渡すには構造が不安定

## 再提出条件
再提出は、差戻し理由に対する補完または修正が行われた場合に進める。  
再提出条件の骨格は以下。
- 差戻し理由が明示されている
- 不足見出しまたは不足項目が補われている
- 境界が再度読めるようになっている
- 他レイヤー責務の吸収が除去されている
- validation 結果の再確認が可能である

## validation 結果の出力骨格
validation 結果として最低限出力する骨格は以下。
- 対象ファイル
- 検証日時
- 検証主体
- 構造妥当 / 差戻し要否
- 不足項目一覧
- 境界上の懸念
- 次工程へ進めるか / 戻すかの判定接続
- 参照した基準または参照先

## 次工程へ進めるか / 戻すかの判定接続
構造妥当性確認後の接続は以下を基本とする。
- 次工程へ進める
- 差戻しへ戻す
- 再提出待ちにする
- HITL へ接続する
- completion gate 側の判定へ渡す

## 境界

### completion gate との境界
- 本ファイルは構造妥当性確認を扱う。
- completion gate は完了可否の最終判定を扱う。
- 本ファイルは completion 判定全文を持たない。

### HITL protocol との境界
- `protocol-hitl-jp.md` は人間介入条件・トリガー・制御を扱う。
- 本ファイルは構造不備時の validation を扱う。
- 人間介入接続そのものの設計は `protocol-hitl-jp.md` 側で扱う。

### artifact との境界
- `audit-evidence-jp.md` は監査・追跡・説明責任の artifact である。
- `handoff-artifact-standard-jp.md` は受け渡し artifact である。
- 本ファイルは artifact schema 本文を持たず、必要時に参照接続する。

### governance との境界
- `privacy-handling-jp.md` と `external-collaboration-jp.md` は統制本文を扱う。
- 本ファイルは統制本文そのものではなく、構造妥当性確認を扱う。

### agent との境界
- Orchestrator / Context Manager の制御本文は本ファイルで扱わない。
- 本ファイルは局所的な validation protocol に留まる。

## 非対象
本ファイルの非対象は以下。
- 法令 / 社内制度固定値
- 承認経路本文
- completion 判定全文
- artifact schema 完成版
- governance 規程本文
- agent 制御本文
- 構造 validation の完成版フロー設計

## 参照先
- `02_jp_specs/protocols_jp/protocol-hitl-jp.md`
- `02_jp_specs/protocols_jp/protocol-ringi-jp.md`
- `02_jp_specs/protocols_jp/protocol-approval-flow-jp.md`
- `02_jp_specs/governance_jp/privacy-handling-jp.md`
- `02_jp_specs/governance_jp/external-collaboration-jp.md`
- `02_jp_specs/artifacts_jp/audit-evidence-jp.md`
- `02_jp_specs/artifacts_jp/handoff-artifact-standard-jp.md`
- `02_jp_specs/03_jp_requirement_placement_map.md`
- `02_jp_specs/04_glossary_jp.md`

## 注記
- 本ファイルは skeleton 初稿であり、本文完成版ではない。
- validation 結果の最終 schema や completion gate との最終接続条件は今後確定する。
- 内容の正しさ全文ではなく、構造妥当性確認を優先して扱う。
