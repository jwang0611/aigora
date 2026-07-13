# Decisions — 《一比一》(EditorInChief log)

每个 Gatekeeper checkpoint 由 EditorInChief 代作者作答，附理由。

## D-001 · L1 CONCEPTION 内核锁定
- **决策**: 采纳 Synthesizer 收束方案。Track=文学向；目标~5万字/2卷。内核、结局方向、6条 PROMISE 如
  master-outline。
- **理由**: "1:1 完美副本承诺不了的东西"提供了主题引擎与结构表达（形存实亡）；家族旧账（祖父摆渡人）
  以"主角自己悄悄接活"承接巧合，把命运改写为选择；"名册 vs 点云 / 签收"母题与 slow-room 同源不重样。
- **对立读法保留**: 数字南屿既是傲慢也是唯一能带走之物——两读都留。

## D-002 · Track 推断
- 简报已明确 Track=文学向，无需推断。评审用 quality-rubric（文学）+ longform-quality-gates 的 V1/V2。

## D-003 · 规模微缩（管线测试）
- **决策**: 正常卷 7–8.5万，本次按比例缩为卷~2.5万、章~4,000、每卷6章，以最小规模跑完 L1×2+L2 全门控。
- **理由**: 简报即"测一遍流程"。缩微不改门控机制，只改字数硬约束。burn-rate 以 2.5万/卷为基准计。

## D-004 · 人工介入点评估（钟阿婆去留）
- **决策**: 不升级。守碑人不殉谷；她在最后一天把《名册》签收给江照后离开。
- **理由**: 殉谷会滑向煽情且回避主题；"交出名册后离开"把重量交给动作（签收）而非死亡，且让 PROM-004/005
  在结尾合流。此抉择由文本承担，符合 AUTOPILOT 人工介入点第2条"能不美化不回避地自行承担则不升级"。

## D-005 · 卷一无 style-anchor 的处理
- **决策**: 卷一起草仅依 story-bible 的 Voice & Style；style-anchor 待卷一过门后由主编从**过门章节**选取。
- **理由**: 符合 LONGFORM——锚点取自 gate-passed 卷一文本。ch01 由主编在主上下文亲撰以立声，作为卷一其余
  章节并行起草的具体声腔样例（非正式 anchor，仅起草参考）。

<!-- 后续 checkpoint（V.OUTLINE / L1 gate / V.COMPACT / L2）在此续记 -->

## D-006 · V.OUTLINE 卷一锁定
- **决策**: 锁 volumes/v01-cehui/outline.md（6 beat=6章，出口=江照认出钟满/那一夜、决定留下）。
  depends-on 无（首卷）。burn-rate 基准：卷一 ~2.5万字 / 3个里程碑。
- **理由**: 逐章给出 entry/exit 与 ledger-critical facts，供 ch02-06 并行起草保持连续；关键时刻5处锁定。

## D-007 · L1 GATE 卷一验收（round 1）
- **决策**: 卷一《测绘》PASS（封卷）。中位 65/80，各维≥8（最弱 Structure/Character/Prose/Orig/Emo/VolArc/Serial=8，Thematic=9）。
- **R3 盲评发现 4 条无条件连续性 Must Fix，已清零**：MF-01 坟地坡顶高程改330(>326)；MF-02 周晏迁坟时间线统一(ch04 D71 实迁, ch01/ch02 改备/清树, ch06"个把月前")；MF-03 农历丙辰六月十九→公历八月十四、地方志八月中旬；MF-04 钟阿婆年龄统一78。
- **SF 采纳**：SF-01(14 vs 二三十→决口那夜过半)、SF-02(何广仁衣冠冢未经验看故葬处空)、SF-03(册子归一)、SF-04(ch03 轻铺垫钟阿婆个人失亲)、SF-05(压缩 ch02/ch03/ch06 主题解说)。
- **驳回**：R2"ch03'我姓江'过早电报"——保留（R1 认其为最强钩子；属身世线）。
- **主编裁决记录（cost）**：品味分已达标、修订仅为客观连续性+去解说，故以机械复审(grep 全绿)确认，不触发全量三评重跑。
- **quality debts**: 无。

## D-008 · V.COMPACT 卷一封存
- 写 memory/digests/vol-01-digest.md（≤2500字）；entities 追加 End-of-vol-1；timeline 追加卷一；ledger 标 ARCHIVED。
- **style-anchor 建立**（book/style-anchor.md）：取卷一过门文本三段（叙述/对白/动作）+ 具名三条本书易犯 AI 腔（供卷二规避）。
- **守恒检查（KnowledgeAuditor）**：卷一无坟空条未新增未回收伏笔进 registry（PROM 结构不变，PROM-002 已 Paid）；出现≥3章的实体(江照/钟阿婆/周晏/南屿)均有 entity 文件。PASS。
- git tag: v01-compacted。

## D-009 · V.OUTLINE 卷二锁定
- **决策**: 锁 volumes/v02-meiding/outline.md（6 beat=ch07-12；出口＝没顶+带钟满之名过水+签收+号牌"用途"填字）。
  depends-on: vol-01 digest。章均上调 ~4,500–4,800（补全书至~5万，禁注水）。
- **卷二起草加载 style-anchor**：具名三条本书 AI 腔须规避；变奏章末落法（逐 beat 指定）。
- **人工介入点D-004 执行位**：ch10 钟阿婆交出名册后离谷（不殉）。

## D-010 · L1 GATE 卷二验收（round 1）
- **决策**: 卷二《没顶》PASS（封卷）。中位 68/80（R1 69 / R2 59 漂移 / R3 70），各维≥8。
- **R3 5条连续性 Must Fix + R1 接缝 Must Fix，已清**：CF-01 reader-recap 日期改八月十四（**驳回 R3"七月十五正确"**：唐山地震1976-07-28＝农历六月初二 ⇒ 六月十九＝八月十四，卷一正解）；CF-02 水位链改单调 ch09≈282→ch10≈285→ch11 302-326；CF-03/04 钟阿婆离村（车/时辰/交册时点）ch11 对齐 ch10；CF-05 老浔口桩高程 ch07 改≈251（合 ch12 的251.476）；CF-06 ch07→ch08 接缝内解脱困。
- **R2 声纹漂移 Must Fix（对照 style-anchor 命中 tell#2/#3），已清**：DF-01 删 ch09/ch10"补面＝名册空条"叙述者等号；DF-02 "水无声涨"意象四处留一、"像核单子"两处留一；DF-03 ch07 两处段末对称金句删。
- **主编裁决**：ch03"二三十"vs ch12"十几个"空条数——属"随手估 vs 守册后精点"，内部各自自洽（327总/310有葬处/十几无坟），接受为口径差，不改。
- **quality debts**: 无。

## D-011 · V.COMPACT 卷二封存（全书收官）
- vol-02-digest（≤2500）；reader-recap 更新至 through vol2（全书，供 L2）；registry 全部 PROM Paid（**闭合100%**，"江"姓 red herring closed）；entities End-of-vol-2；timeline 卷二；ledger 归档（Amendments 记 round1）。
- **守恒检查**：伏笔 6/6 pay + PROM-002；≥3章实体均有文件；无未登记未回收。PASS。
- git tag: v02-compacted。
