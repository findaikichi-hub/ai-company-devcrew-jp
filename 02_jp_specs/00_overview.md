# 00_overview

## 目的
本家 DevCrew_s を土台に、日本企業向けにローカライズした AI社員 / AIエージェント仕様テンプレート群を作る。

## 基本方針
- 単なる翻訳ではなく、日本の業務運用に合う形へ再設計する
- 本家の構造を参照し、方向性を外しすぎない
- 差分は明示的に記録する
- まずは横断型テンプレートを優先する
- 本家の specification-first の考え方を継承する

## 日本版で重視する要素
- 敬語
- 稟議
- 承認フロー
- 責任分界
- 監査ログ
- 個人情報
- 委託先管理
- 引き継ぎ文化

## 特に重要な設計観点

### 劣化対策
- 短期記憶
- 長期記憶
- 共有記憶
- ログ蓄積
- メトリクス
- 失敗記録
- 仕様更新

### AI間連携
- 構造化メッセージ
- correlation_id
- task_packet
- validation_report
- 非同期メッセージング
- 役割分担の明確化

## 初期スコープ
- AI社員 Spec Template 日本版
- PMO / プロジェクト管理AI
- 情シス受付・一次対応AI
- 議事録→要約→タスク化AI
- 稟議ドラフトAI
- 社内FAQ・ナレッジ検索AI
- 手順書更新AI

---

## 日本版で採用する反復協働の考え方

日本版では、AI社員同士の連携を会話の往復としてではなく、
artifact と protocol を通じた反復協働として捉える。

### 反復の基本単位
- delegation
- handoff
- validation
- quality gate
- rework / 再委譲

### 意味
- 初回出力はドラフトとする
- ドラフトは、他AIとの自由会話で醸成するのではなく、標準化された手順で洗練する
- 次工程への受け渡しは、task packet、handoff 文書、validation report などの artifact を中心に行う
- 完了は、個別AIの自己判断ではなく、protocol 上の検証と orchestration によって決まる

---

## 日本版で追加設計すべき機能
日本版では、以下を独立した人格役ではなく、制御機能または protocol 群として追加・明確化する。

### 完了判定機能
- quality gate の通過条件
- orchestration 上の完了条件
- 次工程への受け渡し可能性の判定

### 構造検証機能
- template validation
- decomposition validation
- handoff completeness validation
- 必要に応じた MECE 確認

---

## 人間の関与方針
- 人間は常時介入しない
- 日常処理は AI と protocol で進める
- 人間は以下に限定して関与する
  - 方針判断
  - 例外承認
  - HITL ゲート責任
