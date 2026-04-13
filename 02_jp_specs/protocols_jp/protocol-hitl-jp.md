# protocol-hitl-jp

## 目的
日本版運用において、どの条件で人間介入へ接続するかを protocol として定義する。

## 位置づけ
本ファイルは、Human-in-the-Loop を扱う protocol 別仕様の skeleton 初稿とする。  
governance 文書の代替ではなく、条件・トリガー・接続制御を扱う protocol である。  
承認フロー protocol の代替でもなく、状態遷移全文や承認経路全文を保持しない。  
Artifact ではなく protocol 別仕様として、人間介入接続の受け皿を定義する。

## 扱う対象
- HITL条件
- HITLトリガー
- HITL制御
- 前進停止条件
- 人間へ渡す理由
- 人間へ渡した後の戻し先 / 接続先の骨格

## 基本原則
- 人間へ渡す条件を明示する。
- HITL条件、HITLトリガー、HITL制御を混ぜずに扱う。
- 状態遷移全文や承認経路全文をここに吸収しない。
- governance の統制本文をここに吸収しない。
- agent 制御本文をここに吸収しない。
- artifact schema 本文をここに吸収しない。

## HITL条件
人間介入が必要となる条件の骨格は以下。
- 高リスク・高影響で AI のみでは前進可否を決められない
- 権限確認が必要
- 例外処理が必要
- 情報種別や共有可否の判断が必要
- 起案内容または承認状態だけでは前進不可である
- 誤処理コストが高く、停止判断が必要

## HITLトリガー
HITL条件が実際に発火する契機の骨格は以下。
- 起案内容の妥当性が未確定
- 決裁対象または承認対象が曖昧
- 権限不一致または権限未確認
- 高機微情報や社外共有が関与する
- 通常経路外の承認または例外連携が必要
- 差戻し / 保留 / 停止の判断が必要

## HITL制御
HITL発火後の接続制御の骨格は以下。
- 人間確認待ちへ遷移する
- 前進停止または保留へ切り替える
- 差戻しへ切り替える
- 人間判断後に元の protocol または次工程へ戻す
- 人間判断結果を記録し、必要な参照先へ接続する

## 前進停止条件
以下の場合は、AIのみで前進せず停止または保留する。
- 人間確認なしでは誤処理リスクが高い
- 判断根拠が不足している
- 権限確認ができていない
- 情報種別や共有可否が未確定
- 通常経路では扱えない例外案件である

## 人間へ渡す理由
人間へ渡す理由として最低限扱うのは以下。
- 判断責任が人間側にあるため
- 権限確認が必要なため
- 高リスク判断が必要なため
- 例外判断が必要なため
- 情報種別や共有可否の判定が必要なため

## 戻し先 / 接続先の骨格
HITL 後の戻し先 / 接続先は以下を基本とする。
- 元の protocol へ戻す
- 次工程へ handoff する
- 差戻しへ接続する
- 保留のまま停止する
- approval / validation 結果参照へ接続する

## 境界

### 承認系 protocol との境界
- `protocol-ringi-jp.md` は起案内容側を扱う。
- `protocol-approval-flow-jp.md` は承認状態遷移側を扱う。
- 本ファイルは、人間介入へ渡す条件・トリガー・制御だけを扱う。

### governance との境界
- `privacy-handling-jp.md` は情報種別起点の共有可否 / 制約を扱う。
- `external-collaboration-jp.md` は外部共有起点の条件 / 責任境界を扱う。
- 本ファイルは、それらの統制本文ではなく、人間介入接続条件を扱う。

### artifact との境界
- `audit-evidence-jp.md` は監査・追跡・説明責任の artifact である。
- `handoff-artifact-standard-jp.md` は次工程への受け渡し artifact である。
- 本ファイルは artifact schema 本文を持たず、必要時に参照接続する。

### agent との境界
- Orchestrator の全体進行管理は本ファイルで扱わない。
- Context Manager の鮮度管理・共有記憶整合は本ファイルで扱わない。
- 本ファイルは局所的な人間介入接続 protocol に留まる。

## 非対象
本ファイルの非対象は以下。
- 法令 / 社内制度固定値
- 承認権限規程本文
- artifact schema 本文
- governance 規程本文
- Orchestrator / Context Manager の制御本文
- 承認経路全文
- 状態遷移全文
- HITL の完成版フロー設計

## 参照先
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
- protocol-hitl-jp は Human 側の制度本文ではなく、接続条件を扱う protocol である。
- 承認経路や逐次手順の詳細は後続で別途整理する。
