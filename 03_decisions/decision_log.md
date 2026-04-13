# decision_log

このファイルには、設計変更の理由を記録する。

## 記録ルール
- 1件1判断で残す
- 変更前 / 変更後 / 理由 / 影響範囲 / 日付 を必ず書く
- 本家由来か、日本語化か、日本独自追加かを明記する
- 方針確定・構造変更・運用ルール変更は必ず残す
- 後で見返したときに、なぜその判断をしたか分かる粒度で書く

## テンプレート
- 日付:
- 対象:
- 変更前:
- 変更後:
- 理由:
- 影響範囲:
- 種別: 本家由来 / 日本語化 / 日本独自追加
- 次アクション:

---

- 日付: 2026-04-13
- 対象: 中核テンプレ本体に残す範囲
- 変更前: `01_ai_employee_spec_jp.md` は設計原則・必須機能・今後詰める項目が混在し、本家 major sections の骨格も不足していた。
- 変更後: `01_ai_employee_spec_jp.md` は中核テンプレ本体として扱い、本家 major sections を章見出しレベルで保持する。
- 理由: 中核テンプレから本家 section の器を落とすと、後続で要件の置き場判断がぶれやすくなるため。
- 影響範囲: `02_jp_specs/01_ai_employee_spec_jp.md`
- 種別: 本家由来
- 次アクション: 本家 section 見出しを空骨格として追加する。

---

- 日付: 2026-04-13
- 対象: 別受け皿へ逃がす範囲
- 変更前: Protocol 詳細、artifact schema、運用統制差分が中核テンプレ本体へ混入しうる状態だった。
- 変更後: Protocol 詳細は protocol別仕様、artifact schema は artifact標準、統制差分は governance文書へ逃がす方針に固定する。
- 理由: Agent / Protocol / Artifact / Governance の責務混在を防ぐため。
- 影響範囲: `02_jp_specs/01_ai_employee_spec_jp.md` `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 本家由来
- 次アクション: 配置表で受け皿を要件ごとに固定する。

---

- 日付: 2026-04-13
- 対象: 日本独自要件の配置方針
- 変更前: 日本独自要件は列挙されていたが、どこに置くかの正本がなかった。
- 変更後: `03_jp_requirement_placement_map.md` を新設し、日本独自要件を中核テンプレ本体 / agent別仕様 / protocol別仕様 / artifact標準 / governance文書のどこに置くかを固定する。
- 理由: 日本独自要件の配置先を明示しないと、後続文書で再混在しやすいため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: 主レイヤー・判断状態を含む配置表を維持する。

---

- 日付: 2026-04-13
- 対象: 配置設計専用ファイル新設方針
- 変更前: `02_mapping_keep_change_add.md` に方針整理と配置設計を同居させる案があった。
- 変更後: `02_mapping_keep_change_add.md` は Keep / Change / Add の方針整理に留め、配置設計の正本は `03_jp_requirement_placement_map.md` に分離する。
- 理由: 構造マッピング資料と配置設計を同居させると粒度不一致が悪化するため。
- 影響範囲: `02_jp_specs/02_mapping_keep_change_add.md` `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本語化
- 次アクション: 配置判断は `03_jp_requirement_placement_map.md` を正本として運用する。

---

- 日付: 2026-04-13
- 対象: Orchestrator / Context Manager 責務保持の置き場方針
- 変更前: `05_official_agents_jp_mapping.md` だけで Orchestrator / Context Manager の責務保持まで担おうとしていた。
- 変更後: `05_official_agents_jp_mapping.md` は接続整理ファイルとし、責務保持の正本は `agents_jp/agent-Orchestrator-jp.md` と `agents_jp/agent-Context-Manager-jp.md` に分離する。
- 理由: mapping は見取り図、agent別仕様は責務保持正本として分離した方が本家構造と整合し、責務縮退も防げるため。
- 影響範囲: `02_jp_specs/05_official_agents_jp_mapping.md` `02_jp_specs/agents_jp/agent-Orchestrator-jp.md` `02_jp_specs/agents_jp/agent-Context-Manager-jp.md`
- 種別: 本家由来
- 次アクション: mapping には接続カテゴリを、agent別仕様には skeleton を保持する。

---

- 日付: 2026-04-13
- 対象: 稟議の正式受け皿
- 変更前: `03_jp_requirement_placement_map.md` では、稟議は protocol別仕様候補として挙がっていたが、判断状態は暫定だった。
- 変更後: 稟議は protocol別仕様に正式配置し、初期ファイル名を `02_jp_specs/protocols_jp/protocol-ringi-jp.md` とする。
- 理由: 稟議は起案、添付、決裁経路、差戻し理由などの手順を持つため、独立 protocol として分離した方が責務が明確になるため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: `protocol-ringi-jp.md` の skeleton 作成候補を後続で整理する。

---

- 日付: 2026-04-13
- 対象: 承認フローの正式受け皿
- 変更前: `03_jp_requirement_placement_map.md` では、承認フローは protocol別仕様候補として挙がっていたが、判断状態は暫定だった。
- 変更後: 承認フローは protocol別仕様に正式配置し、初期ファイル名を `02_jp_specs/protocols_jp/protocol-approval-flow-jp.md` とする。
- 理由: 承認フローは状態遷移、承認条件、差戻し、例外処理を伴うため、稟議とは分離した独立 protocol とする方が安全なため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: `protocol-approval-flow-jp.md` の skeleton 作成候補を後続で整理する。

---

- 日付: 2026-04-13
- 対象: 監査証跡の正式受け皿
- 変更前: `03_jp_requirement_placement_map.md` では、監査証跡は artifact標準候補として挙がっていたが、判断状態は暫定だった。
- 変更後: 監査証跡は単独 artifact 標準に正式配置し、初期ファイル名を `02_jp_specs/artifacts_jp/audit-evidence-jp.md` とする。
- 理由: 監査証跡は handoff 専用ではなく、横断的な observability / data contract の記録物として扱う方が再利用性と監査確認性が高いため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: `audit-evidence-jp.md` の skeleton 作成候補を後続で整理する。

---

- 日付: 2026-04-13
- 対象: 個人情報 / 機微情報管理の正式受け皿
- 変更前: `03_jp_requirement_placement_map.md` では、個人情報 / 機微情報管理は governance文書候補として挙がっていたが、判断状態は暫定だった。
- 変更後: 個人情報 / 機微情報管理は別 governance 文書に正式配置し、初期ファイル名を `02_jp_specs/governance_jp/privacy-handling-jp.md` とする。
- 理由: 個人情報 / 機微情報管理は Ethical_Guardrails / Forbidden_Patterns 側の横断統制であり、agent個別差分へ押し込むべきでないため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: `privacy-handling-jp.md` の skeleton 作成候補を後続で整理する。

---

- 日付: 2026-04-13
- 対象: 委託先 / 外部連携管理の正式受け皿
- 変更前: `03_jp_requirement_placement_map.md` では、委託先 / 外部連携管理は governance文書候補として挙がっていたが、判断状態は暫定だった。
- 変更後: 委託先 / 外部連携管理は別 governance 文書に正式配置し、初期ファイル名を `02_jp_specs/governance_jp/external-collaboration-jp.md` とする。
- 理由: 委託先 / 外部連携管理は社外共有境界、委託条件、外部連携責任を扱うため、個人情報管理とは別の横断統制文書として分離した方が責任境界が明確なため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: `external-collaboration-jp.md` の skeleton 作成候補を後続で整理する。

---

- 日付: 2026-04-13
- 対象: handoff artifact 標準の正式受け皿
- 変更前: 引き継ぎ文化と日本版 handoff artifact 標準は artifact 側候補として認識されていたが、独立 artifact 標準としての判断が未記録だった。
- 変更後: `02_jp_specs/artifacts_jp/handoff-artifact-standard-jp.md` を独立 artifact 標準として配置し、受け渡し artifact の正本とする。
- 理由: handoff は audit evidence の代替ではなく、次工程への受け渡し単位として独立させた方が責務と再開条件が明確になるため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md` `02_jp_specs/artifacts_jp/handoff-artifact-standard-jp.md`
- 種別: 日本独自追加
- 次アクション: handoff artifact の最小項目と参照先を本文で整備する。

---

- 日付: 2026-04-13
- 対象: audit evidence と handoff artifact の正本 / 参照の線引き
- 変更前: audit evidence と handoff artifact の双方が、判断・差戻し・承認・次アクションを扱うため、正本 / 参照の線引きが明文化不足だった。
- 変更後: audit evidence は監査・追跡・説明責任の正本、handoff artifact は受け渡しの正本とし、必要な情報は相互参照するが本文を吸収統合しない方針に固定する。
- 理由: 監査証跡と受け渡し artifact を混在させると、説明責任と次工程再開の責務が曖昧になるため。
- 影響範囲: `02_jp_specs/artifacts_jp/audit-evidence-jp.md` `02_jp_specs/artifacts_jp/handoff-artifact-standard-jp.md`
- 種別: 日本独自追加
- 次アクション: 参照キーと正本保持範囲を後続で明文化する。

---

- 日付: 2026-04-13
- 対象: governance 2本の境界明文化方針
- 変更前: `privacy-handling-jp.md` と `external-collaboration-jp.md` は概ね分かれていたが、共有論点の境界が本文で一段弱かった。
- 変更後: privacy は情報種別起点の共有可否 / 制約、external は外部共有起点の条件 / 責任境界を扱うと本文で明文化する方針に固定する。
- 理由: 共有論点の近接領域を放置すると、A4再検証で同じ境界指摘が再発しやすいため。
- 影響範囲: `02_jp_specs/governance_jp/privacy-handling-jp.md` `02_jp_specs/governance_jp/external-collaboration-jp.md`
- 種別: 日本独自追加
- 次アクション: 両文書で共有論点の境界を一段だけ明文化する。

---

- 日付: 2026-04-13
- 対象: protocol-completion-gate-jp の主要受け皿化
- 変更前: 完了判定機能は placement 上では protocol別仕様に置く方針だったが、独立受け皿としての本文作成判断が未記録だった。
- 変更後: `02_jp_specs/protocols_jp/protocol-completion-gate-jp.md` を主要受け皿として作成し、完了可否の最終判定を受ける protocol として扱う。
- 理由: structure validation の後段として、完了可否の最終判定受け皿を独立させた方が protocol 系の接続が明確になるため。
- 影響範囲: `02_jp_specs/protocols_jp/protocol-completion-gate-jp.md` `02_jp_specs/03_jp_requirement_placement_map.md`
- 種別: 日本独自追加
- 次アクション: skeleton 初稿を作成し、A4で構造検証する。

---

- 日付: 2026-04-13
- 対象: 新規主要受け皿作成フェーズから横断整合フェーズへの移行
- 変更前: protocol / artifact / governance の主要受け皿を順次新規作成するフェーズが続いていた。
- 変更後: 主要受け皿の初期作成を一旦閉じ、配置正本・判断記録・現在地説明の横断整合を優先するフェーズへ移行する。
- 理由: 受け皿が揃った段階で、placement_map・decision_log・overview のズレを補正した方が公開・引き継ぎ前の戻りが少ないため。
- 影響範囲: `02_jp_specs/03_jp_requirement_placement_map.md` `03_decisions/decision_log.md` `02_jp_specs/00_overview.md`
- 種別: 日本独自追加
- 次アクション: 横断整合の最小修正として 3 本を優先更新する。

---

- 日付: 2026-04-13
- 対象: 共通参照キーの最小集合
- 変更前: protocol / artifact / governance をまたぐ参照キーは使われていたが、最小集合としての判断が明文化されていなかった。
- 変更後: 共通参照キーの最小集合を `correlation_id` / 対象タスク・対象案件ID / 日時 / 主体 / 関連artifact参照ID に固定する。
- 理由: 接続面の追跡可能性を維持しつつ、各本文で必要以上のキー増殖を防ぐため。
- 影響範囲: `02_jp_specs/04_glossary_jp.md` `02_jp_specs/05_official_agents_jp_mapping.md`
- 種別: 日本独自追加
- 次アクション: 接続面で使う正規語として glossary に固定する。

---

- 日付: 2026-04-13
- 対象: validation 分類の扱い
- 変更前: template validation / decomposition validation / handoff validation などの分類名が、将来の新規 protocol 群として増殖しうる状態だった。
- 変更後: validation 分類は新規 protocol を増やす前提ではなく、既存 `protocol-structure-validation-jp.md` を傘として扱い、分類名は glossary 上で正規化する方針に固定する。
- 理由: 接続面固定より先に validation 系の受け皿を細分化すると、戻りと用語揺れが増えるため。
- 影響範囲: `02_jp_specs/04_glossary_jp.md` `02_jp_specs/05_official_agents_jp_mapping.md` `02_jp_specs/protocols_jp/protocol-structure-validation-jp.md`
- 種別: 日本独自追加
- 次アクション: official agents mapping 側で validation 接続を既存受け皿基準で整理する。

---

- 日付: 2026-04-13
- 対象: `05_official_agents_jp_mapping.md` の位置づけ
- 変更前: `05_official_agents_jp_mapping.md` は agent再編と責務接続整理の文書だったが、接続面の主文書としての位置づけが明文化不足だった。
- 変更後: `05_official_agents_jp_mapping.md` を、Agent ⇄ Protocol ⇄ Artifact ⇄ Governance の接続面を整理する主文書として扱う方針に固定する。
- 理由: 主要受け皿の骨格が揃った段階では、個別本文の深掘りより先に、横断接続面の正本を明確化した方が戻りが少ないため。
- 影響範囲: `02_jp_specs/05_official_agents_jp_mapping.md` `02_jp_specs/04_glossary_jp.md`
- 種別: 日本独自追加
- 次アクション: official agents mapping 側で protocol / artifact / governance の接続整理を読めるように補強する。
