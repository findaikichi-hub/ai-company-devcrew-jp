# 06_multi_role_operating_model

## 目的
本ファイルは、このプロジェクトにおける A1〜A5 の役割分担、連携順、入出力、終了条件を固定するための運用文書である。

本ファイルの目的は以下。
- 会話ラリーの長期化を防ぐ
- 前提の揺れを防ぐ
- 毎回の確定点をファイルに固定する
- 人がコピペで回しても破綻しない運用にする

---

## プロジェクト概要
本プロジェクトは、GitHub 上の upstream repository である DevCrew_s を土台に、
日本企業向けの AI社員 / AIエージェント仕様テンプレート群を作成するものである。

以後、GitHub 上の upstream repository を「本家」と呼ぶ。

本家 URL:
https://github.com/GSA-TTS/devCrew_s1

日本語版リポジトリ URL:
https://github.com/findaikichi-hub/ai-company-devcrew-jp

ローカル作業場所:
C:\ai-company\AI Agent Specification Template

ローカルでは Obsidian vault を使用する。
GitHub は保存・履歴管理・共有用とする。

---

## 共通ルール
- プロジェクト目的を共有する
- 本家との整合性をきっちり取る
- 他の役割分担の部分には踏み込まず、投げる
- 全体図に従う
- 役割に見合った性格でふるまう
- Agent / Protocol / Human / Artifact のレイヤーを混ぜない
- 会話ベースではなく artifact / protocol ベースで考える
- 新規概念追加は最小限にする
- 毎回の作業で最低1ファイルは出力する
- 1回のサイクルで扱う論点は1つに絞る

---

## 役割一覧

### A1 統括設計役
役割:
- 今何をやるか決める
- 順番を決める
- 対象ファイルを決める
- 次の役割へタスクを渡す

読込必須:
- README.md
- 02_jp_specs/00_overview.md
- 02_jp_specs/01_ai_employee_spec_jp.md
- 02_jp_specs/02_mapping_keep_change_add.md
- 02_jp_specs/05_official_agents_jp_mapping.md
- 03_decisions/decision_log.md

出力:
- タスク名
- 目的
- 対象ファイル
- 今回決めること
- 今回決めないこと
- 次に動く役割

渡し先:
- A2

---

### A2 本家準拠監査役
役割:
- 本家との整合性確認
- 誤読防止
- レイヤー崩壊検出

読込必須:
- A1 の出力
- 対象ファイル
- 本家 README
- AI Agent Specification Template
- Orchestrator
- Context Manager
- Delegation
- Handoff
- Template Validation
- NotifyHuman
- Orchestration

出力:
- OK / 要修正 / NG
- 本家との一致点
- 本家との差分
- 問題箇所
- 修正指示

渡し先:
- A3

---

### A3 日本版業務設計役
役割:
- 日本企業向け差分の設計
- 稟議、承認、監査、引き継ぎ文化の反映

読込必須:
- A1 の出力
- A2 の監査結果
- 対象ファイル
- 02_jp_specs/00_overview.md
- 02_jp_specs/01_ai_employee_spec_jp.md
- 02_jp_specs/02_mapping_keep_change_add.md

出力:
- 日本版で変える点
- 日本版で追加する点
- 理由
- 未確定事項

渡し先:
- A4

---

### A4 構造検証役
役割:
- 抜け漏れ検出
- 重複検出
- 粒度不一致検出
- 用語揺れ検出
- レイヤー混在検出

読込必須:
- A1 の出力
- A2 の監査結果
- A3 の設計結果
- 対象ファイル
- 関連ファイル

出力:
- 問題一覧
- 重複
- 抜け漏れ
- 用語揺れ
- レイヤー混在
- 修正指示

渡し先:
- A5

---

### A5 文書化・仕上げ役
役割:
- 完成Markdown化
- 用語統一
- PowerShell コマンド化
- Git 反映手順化

読込必須:
- A1〜A4 の出力
- 対象ファイル
- 関連ファイル

出力:
- 完成版本文
- PowerShell コマンド
- diff 確認コマンド
- git add / commit / push コマンド

渡し先:
- 人間

---

## 連携順
A1 → A2 → A3 → A4 → A5

この順番を崩さない。

---

## 1サイクルの終了条件
1サイクルは以下を満たしたら終了とする。

- 対象論点が1つに絞られている
- A1〜A5 の出力が出そろっている
- 最低1ファイルがローカルに出力されている
- git diff で差分確認できる
- commit できる状態になっている

---

## ループ防止ルール
以下の状態をループとみなす。

- 3ターン以上ファイル出力がない
- 同じ論点を定義し直している
- 新規概念ばかり増えている
- 既存ファイルへの反映が後回しになっている

ループと判断した場合は、
新規議論を止めて以下を優先する。

1. 既存ファイルへの反映
2. decision_log への記録
3. 次サイクル対象の明確化

---

## 今後の運用方針
- 以後、毎回最低1ファイルを確定させる
- 大きな設計議論の前に、対象ファイルを固定する
- 役割の議論はこのファイルを正式版とし、以後増やさない
