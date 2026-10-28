# ADS_SCHEMA_RELEASE_NOTES.md

本文件记录 [`ADS_SCHEMA.md`](ADS_SCHEMA.md) 的版本变化。版本采用 Semantic Versioning：

- MAJOR：不兼容的主体、表、Key 或核心口径变化。
- MINOR：向后兼容地新增表、字段或指标。
- PATCH：不改变接口的说明、约束或索引修正。

## 6.6.0 — 2026-10-28

- 为`ads_sz_gkx_industry_cluster_topic`新增非空字段`industry_chain_stage`，标记Topic在对应集群中的
  `UPSTREAM/MIDSTREAM/DOWNSTREAM`产业链位置。
- 首版按现有关系类型确定性回填：`SUPPORTING→UPSTREAM`、`CORE→MIDSTREAM`、
  `APPLICATION→DOWNSTREAM`；全部3,098条关系均可赋值，不引入人工审核或模型调用。
- 标签是`cluster_code + topic_id`关系属性，不是Topic全局属性；其他既有表结构和数据不修改。

## 6.5.0 — 2026-10-27

- 新增`ads_sz_gkx_industry_cluster`、`ads_sz_gkx_industry_cluster_subfield`和
  `ads_sz_gkx_industry_cluster_topic`，全部使用独立前缀，不修改任何既有表结构或数据。
- Cluster—Subfield固定规则与Subfield—Topic继承关系按操作方授权自动批准；完整成果关系保留在
  Iceberg DWS，Doris集群画像发布去重数与分数计数。
- 专利指标只使用`CITED_SCIENCE_TOPIC`科学引用语义，不冒充专利正文、IPC或主营产业分类。

## 6.4.0 — 2026-10-27

- 为`ads_project_profile`新增人民币名义金额`amount_cny`及汇率、汇率日期、来源、归一状态和策略字段，
  保留原始`amount/currency`不变。
- USD、EUR、JPY、CHF、CAD、AUD沿用2026-10-23固定汇率；GBP、DKK、SEK、CZK、CLP使用操作方提供的
  2026-10-27固定汇率。金额小于等于0时`amount_cny`保持NULL并标记`INVALID_AMOUNT`。
- 为`amount_cny`新增数值倒排索引`idx_project_amount_cny`，用于等值和范围过滤；`ORDER BY`仍由Doris
  执行TopN/排序，不宣称倒排索引可以替代物理排序。
- 已回填63,061条正金额项目，61条非正金额项目保持`amount_cny=NULL`；正金额缺失换算、非正金额误写、
  换算公式不一致均为0。索引构建状态为`FINISHED`，核验见
  [`reports/project_amount_cny_v1/post_run_verification.md`](reports/project_amount_cny_v1/post_run_verification.md)。

## 6.3.3 — 2026-10-27

- 将`ads_project_profile.name`既有倒排索引从`unicode`分词重建为ICU多语言分词，并为
  `ads_project_profile.description`新增ICU多语言全文索引`idx_project_description_multilingual`。
- `name_zh`继续使用6.3.2建立的中文细粒度索引；三项索引均支持`MATCH_ANY`、`MATCH_ALL`和
  `MATCH_PHRASE`，不修改项目字段值、项目身份、逻辑Key或`data_version`。

## 6.3.2 — 2026-10-27

- 为`ads_project_profile.name_zh`新增中文细粒度分词倒排全文索引`idx_project_name_zh`，供后续中文
  项目名称回填后使用。
- 迁移显式构建既有行索引，支持Doris `MATCH_ANY`、`MATCH_ALL`和`MATCH_PHRASE`；不修改项目名称、
  项目身份、逻辑Key或`data_version`。

## 6.3.1 — 2026-10-27

- 将`ads_patent_analysis_cross_metric`从Top 100 Topic扩展为正式Topic全集。当前可审计Topic总数为
  3,484，而不是3,483；全部纳入发布，不人为丢弃一个有效Topic。
- 正式运行4使用`run_id=bdaf2431-7300-43ae-a055-d8985b84baaa`、Iceberg namespace
  `patent_analysis_v1_20261027_r6`、`data_version=202610270301`和指标版本
  `patent_analysis_cited_science_topic_full_matrix_v2`。
- 交叉矩阵发布3,484 Topic × 4公开辖区，共13,936行；其中2,131个零命中组合显式保留为0，避免矩阵
  缺格。覆盖3,484个Topic和4个辖区，`is_topn_truncated=false`，名称缺失、重复Key和非法指标均为0。
- Iceberg与Doris交叉表均为13,936行；任务`current_run_id`已切换到运行4，旧运行继续保留用于审计。

## 6.3.0 — 2026-10-27

- 新增并发布`ads_patent_analysis_topic_patent`，把Iceberg专利—Topic关系完整物化到Doris；逻辑Key为
  `run_id, topic_id, patent_id`，Topic点击后的专利列表不再需要在线连接Iceberg DWS。
- 正式运行3使用`run_id=c2307342-4ca0-496f-b31e-c6a1058f0f4e`、Iceberg namespace
  `patent_analysis_v1_20261027_r5`和`data_version=202610270201`。写入4,135,575条关系，覆盖3,484个
  Topic和1,707,255件专利；与`ads_patent_profile`连接的孤儿专利ID为0。
- 为每个Topic按被引论文证据数、Primary证据数、Topic最高分、关系权重、公开年和稳定专利ID生成
  `core_patent_rank`，前100标记`is_core_patent=true`；共239,178条核心专利关系。该排名是被引科学
  证据强度代理，不代表专利法律、商业或技术价值。
- Iceberg与Doris明细行数一致，逻辑Key重复、中文名缺失、无效排名和核心标记不一致均为0；任务
  `current_run_id`已切换到运行3，旧运行继续保留用于审计。

## 6.2.1 — 2026-10-27

- 将治理视图`iceberg.technology_v2.v_openalex_topic_bilingual`中的已批准Topic中文名称物化到
  `ads_patent_analysis_topic.topic_name_zh`，不使用英文名机器翻译或猜测值。
- 发布运行2：`run_id=a4bf7fc3-a4e7-4ff3-8206-52ec739e4f25`、Iceberg namespace
  `patent_analysis_v1_20261027_r4`、`data_version=202610270101`；运行1及其案例继续保留用于审计。
- 3,484个分析Topic全部取得中文名；Doris Topic表本版本73,122行、中文名空值0，Iceberg
  `dws_patent_topic`的4,135,575条关系中文名空值同样为0。Iceberg—Doris行数一致，逻辑Key重复为0。
- 任务控制面新增独立运行2和案例，任务`current_run_id`已切换到运行2；Schema字段和Topic指标口径不变。

## 6.2.0 — 2026-10-26

- 新增并发布9张专利分析ADS表，覆盖总览、Topic、公开辖区、机构、机构共同受让边、IPC、发明人、
  Topic×辖区交叉指标和数据覆盖率；逻辑Key均包含`run_id`，公共版本为`data_version=202610260403`。
- 建立PostgreSQL控制表`patent_analysis_task`、`patent_analysis_run`、`patent_analysis_task_relation`、
  `patent_analysis_case`和`patent_analysis_artifact`，支持任务状态、重跑/合并关系、案例发布和下载物登记。
- Topic固定为`CITED_SCIENCE_TOPIC`：专利引用的MVP论文所关联的OpenAlex Primary Topic，不是专利
  摘要、权利要求或全文的内容分类。新增Iceberg DWS关系表`dws_patent_topic`，实际写入4,135,575条
  专利—Topic关系，覆盖1,707,255/1,752,444件分析专利（97.4214%）。
- 分析窗口固定为1990—2025公开年，计数单位为publication；2020—2022为对照期、2023—2025为
  近期窗口。CN/US是国家，EP是区域局，WO是国际申请体系，不将后二者伪装成国家。
- 正式Doris结果共138,395行：总览1、Topic 73,122、辖区135、机构1,454、机构边183、IPC
  53,093、发明人10,000、交叉指标400、覆盖率7。Iceberg与Doris逐表行数一致，逻辑Key重复为0。
- 机构仅统计已确认的平台机构解析，覆盖33,807件专利（1.9291%）；IPC覆盖99.8141%；发明人来源
  姓名覆盖95.0851%，但尚未完成人才身份解析。当前法律状态不可用，明确发布为`NOT_AVAILABLE`。
- 新增Doris迁移、Alembic 0038、固定配置、可恢复发布程序、测试、操作说明和运行后验证报告；不修改
  任何来源DWD数据或既有Iceberg对象。

## 6.1.0 — 2026-10-26

- 新增并发布`ads_topic_country_snapshot`，一行表示一个Primary Topic在一个国家或地区的当前完整年度论文
  全球分布快照，逻辑Key为`topic_id, country_location_id`。
- 固定使用2015—2025完整年度；2020—2022为对照期，2023—2025为近期窗口，不把2026部分年度
  混入总量、排名或趋势。
- 同时发布国家参与论文数和按一篇论文命中国家数等权分摊的`paper_fractional_count`；地图正式占比
  使用`paper_fractional_share`，同一Topic合计为1。`paper_coverage_ratio`只表示国家参与覆盖率，
  跨国家之和允许大于1。
- 发布研究产出稳定排名、增长率、趋势方向、国家解析覆盖率、固定窗口和口径版本；证据不足不伪造
  增长率，使用`INSUFFICIENT_EVIDENCE`。
- 新增Doris迁移`sql/doris/ads_schema_6_1_0_topic_country_snapshot.sql`、固定配置
  `config/topic_country_snapshot_v1.json`、发布入口`./scripts/publish_topic_country_snapshot_v1.sh`及
  使用说明`docs/topic_country_snapshot_v1.md`。实际发布209,517行，覆盖4,467个Topic和224个国家/
  地区，结果见`reports/topic_country_snapshot_v1/post_run_verification.md`。

## 6.0.2 — 2026-10-26

- 为`ads_talent_profile.name_zh_candidate`新增中文细粒度分词倒排全文索引
  `idx_talent_profile_name_zh_candidate`，索引参数与既有`name_zh`中文索引一致。
- 显式构建已有100,000行候选姓名数据，支持Doris `MATCH_ANY`、`MATCH_ALL`和`MATCH_PHRASE`；不修改
  候选姓名、来源标识、逻辑Key或`data_version`。

## 6.0.1 — 2026-10-26

- 为`ads_technology_profile.technology_name_en`新增英文分词倒排全文索引
  `idx_technology_profile_name_en`。
- 为`ads_technology_profile.technology_name_zh`新增中文细粒度分词倒排全文索引
  `idx_technology_profile_name_zh`。
- 两个索引均显式构建历史数据，支持Doris `MATCH_ANY`、`MATCH_ALL`和`MATCH_PHRASE`；不修改行数据、
  技术点身份、逻辑Key或`data_version`。

## 6.0.0 — 2026-10-26

- 根据产品方确认，将入选的19,430个ETO Research Cluster直接认定为当前技术分析模块的技术点；
  `technology_node_id`成为唯一技术点主键，`research_cluster_id`仅保留来源血缘。
- `ads_technology_profile.node_identity_type`固定为`ETO_RESEARCH_CLUSTER_TECHNOLOGY`。
- 删除上一版本正式Technology目录遗留的`tech_id`和`mapping_status`字段；本模块不再等待Cluster到
  `dwd_technology`映射。该字段删除属于不兼容变更，因此提升主版本号。
- 新增独立Iceberg发布配置`config/technology_ads_v2.json`；固定输入Snapshot与原19,430技术点范围
  不变，只修订身份口径和输出契约，不修改ETO或DWS来源数据。
- 技术ADS中的论文、专利、机构、年度和证据年份字段由Doris `SMALLINT`扩为`INT`，与Iceberg
  `INTEGER`一致，规避Doris 4.1在nullable Iceberg整数写入SMALLINT时的错误转换；业务值不变。
- 既有颠覆性结果继续以`technology_node_id`关联技术点；92条
  `DISRUPTIVE_CANDIDATE`是论文证据代理候选，不因此升级为市场颠覆或专家确认结论。
- 颠覆性模型发布`paper_disruption_proxy_v1_5_eto_technology_identity`固定读取6.0.0 Technology ADS
  Snapshot；公式和70分业务门槛不变，只将来源身份口径切换为当前技术点清单。

## 5.18.1 — 2026-10-26

- 根据操作方明确要求，新发布`paper_disruption_proxy_v1_4_operator_promoted`将v1.3中的2条
  `DISRUPTIVE_CANDIDATE`和90条`HIGH_IMPACT_WATCH`统一标记为`DISRUPTIVE_CANDIDATE`。
- 最低证据门槛、五维公式、NULL最低排序和固定输入Snapshot均不改变；业务候选综合门槛统一为70，
  不再在当前发布中保留独立`HIGH_IMPACT_WATCH`层级。
- 本次是经操作方批准的业务标签提升，不代表取得新论文、市场、产业替代、技术新颖性或专家审核
  证据。`assessment_method`和`interpretation_note`继续明确这是论文证据代理判断。
- 新结果写入独立Iceberg `technology_disruption_ads_v1_4_20261026`，Doris使用
  `model_version='paper_disruption_proxy_v1_4_operator_promoted'`区分历史模型；旧版本不覆盖、不删除。

## 5.18.0 — 2026-10-26

- 新增`ads_technology_disruption_assessment`，对19,430个候选技术节点建立可复算的论文证据颠覆性
  代理基线；正式发布模型为`paper_disruption_proxy_v1_3`，不得解释为颠覆概率、市场替代或专家结论。
- 综合分使用代表论文对数引用影响25%、平均FWCI 25%、高FWCI论文占比20%、论文—专利连接15%和
  2020—2022对照期至2023—2025近期论文份额增长15%。所有分项先在固定候选总体中转换为百分位。
- 最低证据门槛为至少5篇代表论文、近期至少3篇论文，并至少具有一篇引用计数和一篇FWCI记录；不满足
  时固定标记`INSUFFICIENT_EVIDENCE`，不得因缺失值被识别为颠覆性候选。
- 首轮预检模型以85为综合门槛且未产生候选；v1.2修正百分位NULL排序后真实总体最高分81.100160，仍
  未产生候选。两版均保留独立Iceberg发布用于审计。正式v1.3将综合门槛校准为80，同时把专利连接或
  科研增长辅助门槛提高到80；两个论文影响分项仍须不低于70。满足全部门槛时标记
  `DISRUPTIVE_CANDIDATE`；综合分不低于70的其余合格节点标记`HIGH_IMPACT_WATCH`。
- 新增`ads_technology_disruption_paper_evidence`，只为颠覆性候选和高影响观察节点保存逐篇代表论文、
  被引、FWCI、论文—专利连接、节点内排名与证据角色，支持详情页解释和复核。
- 固定输入为Iceberg `technology_ads_v1_20261016`的Profile、Paper和Hotspot Snapshot；正式结果写入
  独立`technology_disruption_ads_v1_3_20261026`，不修改预检发布、既有Technology ADS或来源数据。
- v1.3实际发布19,430条评估和1,026条逐篇论文证据：颠覆性候选2条、高影响观察90条、未标记3,179条、
  证据不足16,159条；Iceberg与Doris逐表行数一致，重复Key和语义异常均为0。两个候选的对照期论文数
  均为0，必须披露低基期限制并进入人工复核，不得直接作为确定性产业结论。

## 5.17.0 — 2026-10-24

- `ads_talent_profile`新增可空`name_zh_candidate`，专门保存英文名或拼音逆推的当前中文候选名；
  `name_zh`继续只表示有确切来源的标准中文姓名。
- 复用既有`name_zh_source`记录来源：拼音逆推固定使用`PINYIN_INFERENCE`，未来确切来源填写具体来源
  类型。候选名不自动进入默认`name`，也不得用于身份合并或事实关系确认。
- 新增可恢复的DeepSeek批量逆推链路：相同规范化姓名只调用一次，默认每请求25个唯一姓名、16线程，
  逐姓名原子缓存并校验输入hash、返回Key及汉字格式；模型分数强制封顶0.65。
- 候选发布采用Doris partial-column UPSERT，只更新候选名、来源、候选排序分和版本字段，不修改
  `name_zh`、来源数据或既有Iceberg Snapshot。
- 2026-10-25完成100,000名人才、73,804个唯一规范化姓名的推断和发布；DeepSeek截断或漏回Key的
  批次自动递归二分至单姓名重试。最终候选、`PINYIN_INFERENCE`来源和唯一人才均为100,000行，
  `name_zh`仍为0行，候选排序分范围0.0300—0.6500，`data_version=202610240201`。

## 5.16.0 — 2026-10-24

- `ads_research_problem_monthly_metrics`由空契约表升级为真实直接证据月度事实表，从每个问题的首个直接
  事件月生成到统计截止日前最后一个完整月的连续月份网格。
- 月度事实按直接论文发布日期、直接专利公开日期和有日期的直接项目启动日期聚合；人才和机构按其在
  问题直接论文中的首次观察月份计数。LLM月度分布继续仅保存在`monthly_estimate`，不进入真实字段。
- 月度活动分对论文、专利、项目、新增人才和新增机构进行同月截面`log1p`最大值归一，基础权重分别为
  30%、25%、10%、20%、15%；项目维度按真实开始日期覆盖率降低贡献与有效权重。
- 月度热度使用当前月、前1月、前2月活动分的50%/30%/20%平滑；缺少历史月份时仅对已有权重归一。
  环比和三个月增长仅在基期活动分不低于1时计算，避免接近零基数产生极端增长率。
- 已发布Iceberg `research_problem_ads_v14_20261024`和Doris `data_version=202610240101`：月度事实
  91,520行，覆盖406个问题、1929-03至2026-09；论文1,294、专利10,135、项目228条事件对账一致。
  Iceberg与Doris逐表行数一致，月度逻辑Key重复和字段边界异常均为0。

## 5.15.0 — 2026-10-23

- 新增`ads_research_problem_scope_potential_dimension`，把406个问题的五维潜力按问题等权、可用值参与的
  口径聚合到Topic、Field和Domain，并显式记录问题数、有效问题数、覆盖率、中位数及来源问题ID。
- 新增`ads_research_problem_scope_strategy`，物化学科层级的潜力、热点、政策契合、布局缺口、综合战略
  优先级、同层排名、Top问题和推荐机构。综合分按35%潜力、30%热点、20%政策、15%布局缺口计算；
  缺失分项剔除后对可用权重归一，未知政策不按0处理。
- 实际发布1,523个学科范围：1,493个Topic、26个Field、4个Domain；五维明细7,615行。除政策维度外
  四维覆盖100%；政策有值范围为254个Topic、21个Field和4个Domain。
- `ads_research_problem_strategic_advice`新增480条正式范围建议（Topic 450、Field 26、Domain 4），
  使用确定性规则模板并标记`APPROVED_RULE_BASED`；原406条问题级模型建议保持不变，总计886条。
- 仅含1至2个问题的1,043个Topic保留指标但标记`INSUFFICIENT_SCOPE_SUPPORT`，不生成正式建议。
- 新发布使用Iceberg `research_problem_ads_v13_20261023`和Doris
  `data_version=202610231201`，由48张扩展为50张基础问题ADS表；逐表行数一致，重复Key和语义非法项均为0。

## 5.14.0 — 2026-10-23

- 为`ads_research_problem_institution_match`补充事实型`talent_count`，只统计问题证据论文中作者与目标
  机构在同一论文上的署名关系，并按问题、机构、人才去重。
- 新增`direct_talent_count`、`proxy_talent_count`和`talent_evidence_type`；未命中明确写0，四个字段均
  无NULL。
- 417个原全局回退机构—问题对取得同论文人才署名证据，改标
  `candidate_source='EXISTING_SHENZHEN_TALENT_EVIDENCE'`；原全局成果计数仍保留在`global_candidate_*`，
  不冒充问题级成果计数。
- 人才数不进入主导单位贡献排名；主导单位规则继续只使用论文、专利、项目贡献，避免人才与论文重复计权。
- 实际2,586个机构—问题对中725个人才数大于0，机构—问题人才计数合计2,673、单对最大52；覆盖406个
  问题和65家机构，348个问题有多家机构可比较。
- Doris旧版本`data_version=202610200201`的642条记录已精确删除并核验剩余0条。
- 新发布使用Iceberg `research_problem_ads_v12_20261023`和Doris
  `data_version=202610231101`，仍为48张基础问题ADS表。

## 5.13.0 — 2026-10-23

- 新增`ads_research_problem_institution_achievement`，通过论文署名机构、confirmed专利受让机构和
  项目机构关系，物化问题—机构—具体成果证据，禁止仅按问题ID把成果批量归属给所有相关机构。
- 新增`ads_research_problem_institution_discipline_metrics`，按机构和Topic聚合去重问题、论文、专利、
  项目数量、成果年份、明细ID与机构内部重点学科排名。
- 只将`candidate_source='EXISTING_SHENZHEN_EVIDENCE'`计作机构实际参与；全局深圳回退候选继续只用于
  推荐，不进入参与问题数、重点学科或代表成果。
- 专利只使用固定Snapshot中`resolution_status='confirmed'`的关系，并明确不解释为当前专利所有权；
  项目关系区分直接机构关系与受资助论文作者机构兜底。
- 实际发布成果关系4,586条，覆盖65家机构、163个问题和642个已有深圳证据的机构—问题对：论文2,877条、
  项目1,709条；当前固定confirmed专利机构Snapshot与这些机构—问题对无交集，因此专利成果为0条，
  不使用问题级专利计数伪造机构专利归属。机构—Topic聚合5,492条，覆盖865个Topic。
- 新发布使用Iceberg `research_problem_ads_v11_20261023`和Doris
  `data_version=202610231001`，由46张扩展为48张基础问题ADS表。

## 5.12.4 — 2026-10-23

- 使用操作方提供的USD、EUR、JPY、CHF、CAD、AUD固定最新中间价，将252条有效项目金额换算为人民币；
  JPY按`100 JPY = 4.2793 CNY`规范化为`1 JPY = 0.042793 CNY`。
- 回填`ads_research_problem_funding_evidence.funding_amount_cny`、
  `ads_research_problem_yearly_metrics.funding_amount_cny`和
  `ads_research_problem_profile.funding_amount_cny`，并记录汇率、基准日期与归一化状态。
- 汇率日期暂按操作日`2026-10-23`记录，来源标识为`OPERATOR_PROVIDED_LATEST_MID_RATE`；这是固定快照
  名义金额换算，不是逐项目年份历史汇率或购买力折算。
- 区域年度资金仍不回填，避免在没有项目—机构金额分摊证据时把项目总额重复归属多个地区。
- 新发布使用Iceberg `research_problem_ads_v10_20261023`和Doris
  `data_version=202610230401`，旧发布保持不变。

## 5.12.3 — 2026-10-23

- 为`ads_research_problem_profile`的中文标题、问题陈述、知识缺口、研究背景和研究摘要建立中文细粒度
  分词倒排索引，启用短语查询支持。
- 为`ads_research_problem_keyword.keyword_zh`建立中文分词倒排索引，并为`keyword_key`、
  `keyword_type`建立不分词倒排索引，支持规范关键词和类型过滤。
- 对已有历史数据显式执行`BUILD INDEX`；本次只改变Doris物理索引，不改变Iceberg数据、表字段、逻辑Key
  或`data_version=202610230301`。
- 全文查询使用`MATCH_ANY/MATCH_ALL/MATCH_PHRASE`；普通`LIKE`不等同于分词索引检索。

## 5.12.2 — 2026-10-23

- `ads_research_problem_institution_match.institution_type_id`从固定机构画像Snapshot补齐，2,586条记录均有
  稳定机构类型代码。
- 每个问题按论文、专利、项目计数之和选择唯一主导单位；单机构问题直接主导，多机构问题按贡献降序，
  最高值并列时使用带规则版本的稳定哈希抽取，保证幂等重跑结果一致。
- 问题直接证据字段与全局回退候选字段继续隔离。原模型`LEAD`若未被贡献规则选中则改为
  `CORE_PARTNER`，其余角色和所有模型能力评分保持不变。
- 合作领域推荐优先把正式主导单位纳入前三家推荐机构。新发布使用Iceberg
  `research_problem_ads_v9_20261023`和Doris `data_version=202610230301`，旧发布保持不变。

## 5.12.1 — 2026-10-23

- 根据操作方明确批准，将`ads_research_problem_direction`的1,556条研究方向全部发布为
  `review_status='APPROVED'`、`is_official=true`；原DeepSeek的885条APPROVED、660条REVISED和
  11条REJECTED判断继续保存在固定AI Seed中，并写入方向审核理由供追溯，不改写原始模型输出。
- 部署清单的`approved_direction_ids`、潜在方向推荐和合作领域推荐不再排除原REJECTED方向；每个问题
  仍保留3至6条独立方向，表粒度保持“一问题的一方向”，不是“一问题一行”。
- 新发布使用Iceberg `research_problem_ads_v8_20261023`和更高Doris
  `data_version=202610230201`；旧发布保持不变。

## 5.12.0 — 2026-10-23

- 新增国家、广东省、深圳市官方政策基础数据DWD，并以固定Snapshot接入基础问题ADS。政策来源文件
  全程只读，保留来源URL、发布机构、文号、有效状态、日期、核验状态及条款原文。
- `ads_research_problem_policy_evidence`由5.5.0的AI合成政策语境改为官方政策证据：候选召回后由
  DeepSeek进行受约束判定，只允许返回候选政策和候选条款ID，置信度低于0.65的结果不发布。
- 新增`ads_research_problem_policy_yearly_metrics`，按问题、统计年份、政策层级和支持类型聚合政策数、
  有效/被替代政策数、直接支持数、发布机构数、置信度、契合分和日期范围。
- 政策导向维度改用`OFFICIAL_POLICY_EVIDENCE_COMPOSITE_V1`，综合政策数量、层级权威性、时效、
  年份连续性和问题契合度。无官方匹配证据的问题保持NULL并标记`NO_MATCHED_OFFICIAL_POLICY`，
  不以AI生成语料填充。
- 已发布Iceberg `research_problem_ads_v7_20261023`和Doris `data_version=202610230101`：官方政策证据
  39条，覆盖35/406个问题和8份政策；年度聚合39条。Iceberg与Doris逐表行数一致，46张问题ADS表
  重复Key和27项语义边界校验均为0。

## 5.11.0 — 2026-10-22

- 新增`ads_research_problem_collaboration_recommendation`，把已正式发布的DeepSeek研究方向审核结果与
  深圳机构匹配结果组合为问题—潜在合作领域—推荐机构明细，逻辑Key为`recommendation_id`。
- 每个问题选取正式方向前3名和机构匹配前3名，生成合作领域中英文名、牵头机构、候选机构数组、
  合作模式、综合推荐分、方向匹配分、机构能力分、协作准备度、推荐理由和排序。
- 本版本不重新调用大模型；`inference_*`与`source_inference_input_hashes`保留两个上游模型判断的完整
  溯源，`recommendation_method=EVIDENCE_CONSTRAINED_DIRECTION_INSTITUTION_COMPOSITE_V1`明确说明
  当前记录是确定性组合结果。
- 没有问题级直接机构证据的候选固定标记
  `GLOBAL_SHENZHEN_FALLBACK_NO_DIRECT_PROBLEM_EVIDENCE`。尚无机构两两互补性证据，
  `complementarity_score`保持NULL，并由`complementarity_score_status`披露原因。
- 已发布Iceberg `research_problem_ads_v6_20261022`及Doris `data_version=202610220301`：新增表
  1,218行，覆盖406/406个问题，每个问题3个合作领域；Iceberg与Doris行数一致，重复Key和26项
  语义边界校验均为0。

## 5.10.0 — 2026-10-22

- `ads_research_problem_development_snapshot`新增`decline_end_year`、`continuous_decline_years`、
  `decline_rate_avg`、`decline_rate_cagr`、`decline_metric`、`decline_status`和
  `decline_calculation_method`，形成可供时间序列视图直接使用的年度连续衰减周期。
- `decline_start_year`改为当前连续衰减段首年；`observed_decline_years`改为全部相邻年度中观察到的下降
  次数。只有连续自然年份形成同比判断，不跨年度缺口计算。
- 年度生命周期统一只使用截至2025年的完整年度数据，排除可能不完整的2026年度，避免年内数据不足被
  误判为衰减。该计算完全来自年度论文数量，不使用月度模型估算或LLM判断。
- 已发布Iceberg `research_problem_ads_v5_20261022`及Doris `data_version=202610220201`：406个问题中
  `DECLINING`96、`RECOVERING`48、`GROWING`14、`STABLE`123、证据不足125；连续衰减1年82个、
  连续衰减2年14个。两端结果一致。

## 5.9.0 — 2026-10-22

- `ads_research_problem_overview_snapshot`新增`median_relative_growth_rate`，对有效问题的
  `relative_growth - 1`取中位数，使结果可以直接格式化为增长百分比，避免低基期极端倍数扭曲算术平均。
- 新增`relative_growth_sample_count`、`relative_growth_total_problem_count`、
  `relative_growth_coverage_rate`和`relative_growth_statistic_method`，前端可同时披露样本数、总体和覆盖率。
- 保留`avg_relative_growth`以维持向后兼容，但不推荐将其作为总览增长率直接展示。
- 已发布Iceberg `research_problem_ads_v4_20261022`及Doris `data_version=202610220101`。中位增长率为
  `-0.02900810`（即`-2.900810%`），有效样本345/406、覆盖率`0.849754`；两端结果一致。

## 5.8.0 — 2026-10-20

- `ads_institution_profile` 新增去重合作机构数、合作论文数和合作专利数，并增加论文、专利覆盖状态
  与独立合作总量版本。
- 合作机构对论文、直接项目和共同确认受让人专利形成的机构 ID 取并集并跨年份去重；合作论文按
  `institution_id, work_id` 去重，合作专利按 `institution_id, publication_id` 去重，禁止累加机构对
  边指标造成多机构成果重复。
- 论文沿用每篇2至10家机构的已发布合作网络范围；共同专利只接受 confirmed assignee，专利覆盖
  标记为 `PARTIAL`。固定 MVP 总体以外的扩展机构保持 NULL/NOT_AVAILABLE。
- 迁移和可恢复发布入口为 `./scripts/publish_institution_profile_collaboration_totals.sh`。
- 已发布全部 83,745 条机构画像：68,010 家固定 MVP 机构为 `COMPLETE/PARTIAL` 并写入非空计数，
  15,735 家扩展机构为 `NOT_AVAILABLE/NOT_AVAILABLE` 且计数保持 NULL。59,206 家机构有合作机构、
  59,203 家有合作论文、465 家有共同确认受让人专利；负数、合作论文超过总论文数、不可用状态带值、
  数据版本与口径版本异常均为0。核验见
  `reports/institution_collaboration_ads_v1/profile_totals_5_8_0_verification.md`。

## 5.7.0 — 2026-10-20

- `ads_institution_discipline_profile` 新增论文、累计被引、人才三项分项分，以及机构—Topic
  综合科研实力分、Topic 内排名、基准机构数和独立评分版本。
- 每个 Topic 独立建立固定基准总体，三项原始计数使用可处理并列值的平均排名百分位归一化；
  首版按论文 40%、累计被引 35%、人才 25% 加权，避免直接混加不同量纲。
- 评分只解释固定 MVP 论文集合内机构在同一 Topic 的相对科研实力；累计被引尚未按论文年龄或
  FWCI 校正，不得解释为同行评审、投入、专利所有权或产业化能力。
- 使用 Doris Unique Key 部分列更新，保留既有 `project_count` 和基础指标口径版本。迁移与发布入口为
  `./scripts/publish_institution_discipline_strength.sh`。
- 已发布全部 7,232,894 个机构—Topic Key，覆盖 4,512 个 Topic，数据版本为 `202610200701`；
  综合分范围 12.249237—100.000000，Topic 基准人数不一致和排名缺口均为 0。发布改为按 Topic
  CRC32 确定性拆分 32 个分片，以适配当前 Doris BE 内存上限；核验记录见
  `reports/institution_ads_mvp_v1/discipline_strength_5_7_0_verification.md`。

## 5.6.0 — 2026-10-20

- `ads_institution_collaboration_yearly` 新增 `co_project_count`、`project_coverage_status` 和
  `project_source_snapshot_id`，支持按机构对和项目来源开始年查询去重联合项目数。
- 联合项目只接受双方均有合法非空角色的直接 `ads_project_institution` 事实；明确排除
  `funded_output_affiliation`，避免把受资助论文机构共现认定为共同承担。
- 论文机构对与直接项目机构对取并集；项目合作即使没有共同论文也能形成双向合作边。
- 当前直接项目机构覆盖有限：有直接事实的双方为 `PARTIAL`，任一方无直接事实为
  `NOT_AVAILABLE` 且计数保持 NULL。迁移脚本为
  `sql/doris/ads_schema_5_6_0_institution_collaboration_project.sql`。
- 已发布 Iceberg `institution_collaboration_ads_v3_project_20261020` 与 Doris
  `data_version=202610201700`：14,380,246 行逐年一致，严格项目合作正值有向边 270 条、
  有向项目出现 276 次，其中 66 条为无共同论文的纯项目合作边；重复 Key、自环、计数异常和
  缺失反向边均为 0。

## 5.5.0 — 2026-10-20

- 新增`ads_research_problem_monthly_estimate`，使用
  `problem_id, statistics_month, metric_name`长表保存2023—2025月度估算；固定保留
  `estimated_value`、`estimate_method=LLM_TEMPORAL_DISTRIBUTION`、`confidence`和上下界。
  原`ads_research_problem_monthly_metrics`真实事实表继续保持0行，估算不得写入真实计数字段。
- 新增DeepSeek证据约束推理链路，读取`.env`中的`DEEPSEEK_API_KEY/DEEPSEEK_MODEL`，按问题原子缓存、
  16并发运行并严格校验方向ID、机构ID、相似问题候选及预测网格。
- 战略优先级、推荐/牵头机构、机构五维匹配、布局缺口、方向审核、新问题与热度信号均正式写入；
  不设人工审核门槛，但统一标记`AUTO_APPROVED_LLM`并保存模型、提示词、输入hash与生成时间。
- `ads_research_problem_policy_evidence`写入AI生成的政策语境，固定标记
  `is_synthetic=true/source_type=LLM_GENERATED_POLICY_CONTEXT`，不生成或冒充真实政策文号、日期和URL；
  潜力政策维度据此形成明确的AI估算分。
- `ads_research_problem_forecast_yearly`写入2026—2028情景预测和区间，但回测误差保持NULL并标记
  `AI_ESTIMATED_NOT_BACKTESTED`；语义相似度使用`LLM_PAIRWISE_SEMANTIC_JUDGE`，不冒充embedding余弦分。
- 缺少来源金额的真实项目金额、CNY汇率换算、真实政策文件、真实月度事实、预测回测和向量embedding
  继续保持NULL或空表。完整治理口径见`docs/research_problem_deepseek_inference_v1.md`。
- 已发布Iceberg `research_problem_ads_v3_20261020`与Doris `data_version=202610200301`。44张表逐表
  行数一致，逻辑Key重复和23项边界校验均为0；关键行数为月度估算39,024、合成政策语境1,213、
  三年预测4,872、语义相似2,747、机构匹配2,586。核验见
  `reports/research_problem_ads_v3_20261020/deepseek_inference_verification.md`。

## 5.4.0 — 2026-10-20

- 新增`ads_research_problem_deployment`，为406个问题建立部署清单骨架，保存正式优先级、推荐/牵头
  机构、审核、有效期、责任部门和建议投入等级；未补录字段保持NULL并标记`PENDING_DEPLOYMENT_DATA`。
- 新增`ads_research_problem_direction`，承接1,556条现有研究路径作为候选方向；全部保留原模型、提示词、
  证据和审核状态，`is_official=false`，未经人工审核不得作为正式部署方向。
- 新增`ads_research_problem_institution_match`，预置642条深圳区级已有科研证据候选。论文、专利、项目数
  可直接使用；机构类型、人才数、能力分、综合匹配分、角色和推荐理由等待补录，不把关联证据冒充推荐。
- 新增`ads_research_problem_strategic_advice`，为406个问题建立战略建议骨架并带入现有热点分和潜力分；
  战略优先级、政策契合、布局缺口、建议文本、周期和推荐机构保持待补录。
- 新增零行契约表`ads_research_problem_update_signal`，用于后续写入新增问题、热度变化、成果增加、
  优先级变化等跨发布信号；当前未进行增量比较，不生成虚假“新”标签。
- 基础问题ADS由38张扩展为43张。新Iceberg发布为`research_problem_ads_v2_20261020`，Doris使用
  `data_version=202610200201`发布；43张表行数对账一致、逻辑Key重复为0。
- 新表物理DDL为`sql/doris/ads_schema_5_4_0_research_problem.generated.sql`，填数规则和发布结果见
  `docs/research_problem_deployment_ads_v1.md`。

## 5.3.2 — 2026-10-20

- 修正基础研究问题学科名称来源：`ads_research_problem_discipline.topic_name_zh` 不再读取全空的
  `dwd_topic.display_name_zh`，改为连接固定 Snapshot 的
  `technology_v2.dwd_classification_localized_text`，且只接受 OpenAlex Topic 的已审核中文标题最新修订。
- `topic_name_en` 在 `display_name_en` 缺失时回退 OpenAlex `display_name_original`；学科汇总表继续从
  问题—Topic关系聚合名称。学科关联3,584行和学科汇总1,493行的中英文名称缺失均降为0。
- 新Iceberg发布为`research_problem_ads_v1_20261020`，旧发布不覆盖；Doris使用更高
  `data_version=202610200101`完成38表逐表对账与Unique Key更新。
- 新增发布校验，若问题学科表或学科汇总表存在空Topic中英文名则发布失败；并完成全部38张表的
  全空列和高空值列审计。保留的空值均有来源或粒度限制，不使用其他语言、0值或年度数据伪造。
- 核验与剩余数据缺口见
  `reports/research_problem_ads_v1_20261020/topic_localization_verification.md`。

## 5.3.1 — 2026-10-19

- 回填 `ads_institution_industry.project_count`，只更新已由专利证据建立的机构—产业 Key，项目证据
  不得新增机构—产业关系行；完成发布后无命中项目的既有 Key 写0，不再保留NULL。
- Project–Industry 证据固定为 Project/Grant → funded Work → 已发布RoS派生Patent–Work关系 →
  已发布MVP Google Patent exact publication → IPC → 国家知识产权局 IPC–GB/T 4754映射，并保留
  全部输入Snapshot。
- 每个机构—产业 Key 对 `project_id` 去重。一个项目可映射多个产业和四个产业层级，因此产业行
  `project_count` 不要求与 `ads_institution_profile.project_count` 求和相等。
- 指标版本提升为 `institution_industry_cn_gb4754_ipc_2018_project_v1`，数据版本为
  `202610190401`；使用32个互斥分片进行Doris Unique Key局部列更新。发布入口为
  `./scripts/publish_institution_industry_project_count.sh run`。
- 已发布1,354,245个既有机构—产业Key：NULL为0行、零值350,047行、正值1,004,198行，
  `project_count` 合计188,741,198；Project–Industry证据12,603,996行，覆盖303,476个去重项目。
  Stage与Doris对账一致，重复Key为0；核验报告见
  `reports/institution_industry_project_count_v1/post_run_verification.md`。

## 5.3.0 — 2026-10-19

- 在基础研究问题 ADS 上新增16张竞争、生命周期、热度分项、区域、资金、政策、潜力、预测、相似度
  和推荐表，基础问题发布表总数由22张增加到38张。
- `ads_research_problem_project` 保留关联项目的原始金额、币种和金额状态；问题画像和年度表增加项目数、
  有金额项目数、同币种金额汇总和资金覆盖率。没有项目或金额缺失时保持0计数与NULL金额；跨币种不直接
  相加，未接入汇率前 `funding_amount_cny` 和资金可比得分保持NULL。
- 区域年度、当前竞争和机构排名使用固定研究簇机构年度Snapshot，并连接
  `location_v1_4_20261019`。COUNTRY、PROVINCE、CITY可统计；深圳124家机构使用已确认的DISTRICT
  映射。区级历史统计是当前确认位置对历史科研证据的归属，不冒充机构历史地址。
- 热点增加项目活跃分并发布逐分项贡献；资金分因币种不可比不进入总分。发展阶段、活跃跨度、年度连续
  活跃期、峰值和衰减信号可由年度事实计算；月度表保持零行，近3月指标保持NULL并声明年粒度限制。
- 发布五维潜力启发式基线：学术影响、技术转化、资金投入和协作广度可计算，政策导向为空。总分按可用
  维度权重重新归一，明确标记不是机器学习预测；未来三年预测表在模型训练和回测前保持零行。
- 相似问题使用已有问题图的Topic、专利和关系置信特征形成基线，语义向量分保持NULL；推荐表发布Top 5
  图特征相似问题和待复核未来方向，并保留图边或研究路径证据。
- Schema版本提升为5.3.0，指标版本为`research_problem_competition_v1`。执行入口和恢复方法继续使用
  `./scripts/publish_research_problem_ads.sh`，详细口径见`docs/research_problem_ads_v1.md`。
- 已完成正式发布：GLM增强406/406；Iceberg与Doris各38张表逐表对账一致，问题画像406行、论文关联
  313,027行、人才关联241,236行。生成链路强制API并发为1，4问题批次不合规时自动拆为单问题串行补偿。
- 修正关联完整性：论文identity缺失时保留带`openalex:`前缀的来源ID并记录映射状态；人才identity实体
  类型使用`talent`；提出时间直接取DWD最早直接证据论文。详细核验见
  `reports/research_problem_ads_v1_20261019/publication_verification.md`。

## 5.2.1 — 2026-10-19

- 发布 `location_v1_4_20261019`，在 `ads_location` 增加深圳市 9 个 DISTRICT 行，并在
  `ads_location_external_id` 增加 9 条 `AMAP_ADCODE` 映射；既有国家、省、市平台位置 ID 不变。
- 固定选择 `country_code='CN' AND city_name='深圳' AND paper_count>0`、已有中文名且有效的
  124 家 MVP 机构，以中文名调用高德深圳限域 POI API。按操作方明确授权完全采信首条返回，
  不进入人工审核；124 家均由 POI 首条结果解析，无输入提示或地理编码回退。
- `ads_institution_profile` 回填 `district_location_id`、`district_name`、位置 release、解析方法、
  置信度和数据版本；不覆盖名称、论文指标、人才指标或既有城市位置 ID。
- 执行入口为 `./scripts/publish_amap_shenzhen_district.sh ... --execute`，缓存、checkpoint、
  Iceberg/Doris 对账和区分布报告位于 `reports/amap_shenzhen_district_v1_20261019/`。

## 5.2.0 — 2026-10-19

- 新增 22 张基础研究问题 ADS 表，覆盖总览、画像、学科、关键词、年度趋势、热点、知识网络、
  时间轴、溯源和变更记录，以及问题与平台论文、专利、项目、人才、机构的可查询关联。
- 406 个已人工审核问题来自固定 `research_problem_dwd_v1_20261019` Snapshot；关联关系只读取 DWD，
  不使用大模型重新匹配。提出时间定义为最早直接支持论文发表时间，来源机构为该论文全部可映射机构。
- 新增智谱 OpenAI-compatible 增强链路，从 `.env` 读取 `ZHIPU_API_KEY` 和 `ZHIPU_MODEL`，生成研究背景、
  研究现状、语义关系词、规范关键词、技术路线和未来方向。缓存按问题断点续跑并校验输入 hash；
  模型新增内容统一为 `PENDING_REVIEW`。
- 年度热点、关键词和学科趋势沿用研究簇代理指标，并通过 `metric_scope` 明确披露；不把簇级证据冒充
  问题的直接证据。问题证据等级使用 A/B/C 确定性规则。
- AI seed 写入独立 `research_problem_ads_ai_v1_20261019` namespace，业务 ADS 写入独立
  `research_problem_ads_v1_20261019` namespace；所有输入固定 Snapshot，Doris 表使用 Unique Key、
  Merge-on-Write 与 `data_version` sequence column。
- 发布入口为 `./scripts/publish_research_problem_ads.sh`，完整运行及恢复说明见
  `docs/research_problem_ads_v1.md`。

## 5.1.0 — 2026-10-17

- 补齐 4.6.0 的22张候选技术分析表和 4.7.0 的6张技术图谱演进表字段字典；共28张表、543个物理列
  均在 `ADS_SCHEMA.md` 中明确 Doris 类型、含义、逻辑 Key、算法口径和不可过度解释边界。
- 同步为 `ads_schema_4_6_0_technology.sql` 与 `ads_schema_4_7_0_technology_graph.sql` 增加逐列
  `COMMENT` 和表级 `COMMENT`；已有环境分别执行同版本的 `*_comments.sql` 元数据回填脚本。
  本次只补充说明，不改变列名、类型、Key、数据版本、行数或已发布数据。Doris 禁止原位修改 Key、
  HASH distribution 和 sequence column，故既有表回填459个普通列和28个表注释；新建表的543列
  均有注释。
- 新增 `ads_institution_paper`，从固定400万篇MVP core的12,621,620条机构—论文关系中，按机构以
  当前累计被引数、FWCI、发表年份和OpenAlex Work ID稳定排序取Top 20。发布707,290行，覆盖
  64,698家具有论文证据的机构；全量关系不复制到ADS。
- 新增 `ads_institution_patent`，合并confirmed assignee与inventor affiliation两类关系后先按
  机构—Patent publication去重，再按确认受让人优先、授权状态、科学引用论文数、公开年份和
  publication ID稳定排序取Top 20。只发布已存在平台`patent_id`且可关联`ads_patent_profile`的
  记录，共100,358行，覆盖11,324家机构。
- 专利关系分布为ASSIGNEE_ONLY 7,805行、BOTH 98行、INVENTOR_AFFILIATION_ONLY 92,455行。
  inventor affiliation只表示发明人任职/署名关联，不表示机构申请、持有或拥有专利。
- 两张表使用`UNIQUE KEY(institution_id, paper_id/patent_id)`、Merge-on-Write和Key级
  `data_version`；指标版本为`institution_representative_achievement_top20_v1`，数据版本为
  `202610170501`。全部输入固定Iceberg Snapshot，输出写入独立namespace
  `institution_achievement_ads_v1_20261017`。
- Iceberg与Doris逐表行数一致；重复Key、NULL Key、Top 20排名断档、机构孤儿、论文/专利画像孤儿、
  专利关系状态异常均为0。5,000行Stream Load使用确定性label、瞬时BE不可用重试和整表行数
  对账跳过，已验证幂等重跑。
- 迁移为`sql/doris/ads_schema_5_1_0_institution_achievement.sql`；运行入口为
  `./scripts/publish_institution_achievement_ads.sh`；完整口径、固定Snapshot、查询示例和限制见
  `docs/institution_achievement_ads_v1.md`，机器报告见`reports/institution_achievement_ads_v1/`。

## 5.0.0 — 2026-10-17

- `ads_institution_industry` 的关系存在性升级为 confirmed assignee 与 inventor affiliation 两类
  可追溯证据的去重并集。发明人任职证据来自可靠 Author–Inventor 映射，以及专利申请年前后两年内
  的论文署名机构；它表示机构产业技术活动关联，不表示专利所有权。
- 新增 `relationship_evidence_types`、`has_confirmed_assignee_evidence`、
  `has_inventor_affiliation_evidence`、`relationship_evidence_status`、
  `minimum_affiliation_year_distance`、`total_inventor_affiliation_patent_count`、
  `total_linked_patent_count`、`mapped_linked_patent_count` 和发明人任职关系版本字段。
- `patent_count`、分数计数、产业份额、排名和百分位改为两类关系证据按机构—专利组合—产业去重后的
  并集口径；`confirmed_assignee_patent_count` 与 `inventor_affiliation_patent_count` 分开披露。
  同一组合单元同时具有两类证据时总数只计一次，两个证据分项均可计入。
- `mapping_coverage_rate` v2 改为 `mapped_linked_patent_count / total_linked_patent_count`；
  `evidence_quality_status` 继续只表示 IPC–产业映射质量，关系来源读取
  `relationship_evidence_status`，两者不得混用。
- 新增迁移 `sql/doris/ads_schema_5_0_0_institution_industry_affiliation.sql`、固定输入配置
  `config/institution_industry_ads_v2.json`，输出写入新 Iceberg namespace
  `institution_industry_ads_v2_20261017`，不重写 v1 Snapshot。指标版本为
  `institution_industry_cn_gb4754_ipc_2018_v2`，数据版本为 `202610170401`。
- 已发布 DWS 6,017,245 行、ADS 1,354,245 行，覆盖12,701家机构；其中二级产业143,908行。
  限定82,906家有效机构后覆盖12,533家，较v1的3,713家新增8,820家，未覆盖降至70,373家。
  二级产业证据分布为ASSIGNEE_ONLY 28,697行、BOTH 9,109行、
  INVENTOR_AFFILIATION_ONLY 106,102行。Iceberg与Doris行数一致，业务Key重复、关系/产业孤儿、
  分数权重、层级份额和证据状态异常均为0。核验报告见
  `reports/institution_industry_ads_v2/post_run_verification.md`。

## 4.9.1 — 2026-10-17

- 回填 `ads_institution_discipline_profile.project_count`，连接已发布的
  `ads_project_institution` 与 `ads_project_topic`，按机构、Topic 对 `project_id` 去重计数。
- 统计项目的全部关联 Topic，不只统计 Primary Topic；既有机构—Topic Key 无关联项目时明确写 0，
  不再保留 NULL。Grant-Topic 仍是由受资助论文 Topic 推导的关系，不冒充旧 Awards Snapshot
  的来源原生分类。
- 指标版本提升为 `institution_mvp_core_4m_project_topic_v2`，数据版本为 `202610170301`；采用
  Unique Key 局部列更新，仅修改 `project_count`、指标版本、数据版本和更新时间。
- 定向执行入口为 `./scripts/publish_institution_discipline_project_count.sh`，不会重发其他 Project
  ADS 表。物化按 `topic_id` 的xxHash64低5位拆分为32个互斥分片，控制项目关系连接的内存峰值；每个分片
  同时发布正数和零值；Doris批次使用确定性label并带瞬时连接重试，可安全中断和续跑。
  已知完成分片时可用 `--start-bucket N` 从指定分片继续。
- 已发布7,232,894个既有机构—Topic Key：NULL为0行、零值1,809,916行、正值5,422,978行，
  `project_count` 合计268,729,884；重复Key和负数均为0，Stage与Doris对账一致。核验报告见
  `reports/institution_ads_mvp_v1/project_count_4_9_1_verification.md`。

## 4.9.0 — 2026-10-17

- 新增 `ads_talent_research_to_patent_metrics`，以人才固定MVP core去重论文数为分母，以被本人可靠
  关联专利引用的本人去重论文数为分子，保存原始0至1比例、分子、分母、证据计数、覆盖状态和固定
  输入版本；首版不做平滑、百分位或0至100归一化。
- `ads_talent_patent_cited_paper` 新增 `is_paper_authored_by_talent` 与
  `authorship_evidence_status`，在既有人才—专利—被引论文关系上记录固定Authorship核验结果。
- `ads_talent_profile` 冗余当前版本的比例、分子、指标版本和覆盖状态。比例仅表示本人论文进入本人
  关联专利引用链的范围内代理信号，不表示许可、转让、产品化、收入或商业成果转化率。
- 首版固定结果为100,000名人才、579名正向命中人才、1,108个去重人才—论文分子和1,875条
  人才—论文—专利证据关系；来源覆盖不完整，当前有论文分母的人才统一标记`PARTIAL`。
- 迁移为 `sql/doris/ads_schema_4_9_0_talent_research_to_patent.sql`；执行说明见
  `docs/talent_research_to_patent_mvp_v1.md`。

## 4.8.0 — 2026-10-17

- 在 `ads_talent_profile` 向后兼容新增 `country_location_id`、`province_location_id`、
  `city_location_id` 和 `district_location_id`，用于按人才唯一、已解析的当前机构稳定位置 ID 筛选。
- 四级 ID 仅从唯一关联的 `ads_institution_profile` 同名字段复制，不从机构经历自由文本、位置名称或
  代码推断；省级和区县级证据不足时保持 NULL。这些字段表示当前机构位置，不表示人才居住地。
- `profile-location-sync` 已同步扩展部分列写入和空安全对账；可执行迁移为
  `sql/doris/ads_schema_4_8_0_talent_current_institution_location.sql`，既有表和 Key 均不改变。
- 已以 `data_version=202610170201` 回填38,467名具有唯一、已解析当前机构的人才：国家ID 38,467、
  省级ID 36,789、城市ID 38,467、区县ID 0。区县来源当前未覆盖，保持NULL；来源—画像字段不一致为0。
  核验报告见 `reports/talent_ads/profile_location_id_sync_20261017.md`。

## 4.7.0 — 2026-10-16

- 修正4.6.0静态 `ads_technology_profile + ads_technology_graph_edge` 无法独立支撑技术发展播放和
  技术簇群识别的问题。新增6张ADS表，表总数由75张增至81张。
- 新增 `ads_technology_graph_node` 19,430行，将技术名称、主簇群、簇内角色、首次/最近论文年、
  当前论文轨迹阶段和链角色合并为前端首屏节点；完整详情继续回查4.6.0画像及证据表。
- 新增 `ads_technology_community` 1,731行和 `ads_technology_community_member` 19,430行。
  簇群使用固定加权关系、Louvain seed 42和resolution 1.0；1,708个无高/中证据邻边的节点保留
  单节点簇，不为减少簇数而伪造关系。
- 新增 `ads_technology_evolution_yearly` 164,354行，以论文发表年发布累计论文/专利、年度变化、
  起源/峰值里程碑和六类推测阶段。阶段标记为 `PUBLICATION_TIMELINE_INFERENCE`，不是TRL或市场周期。
- 新增 `ads_technology_evolution_edge` 587,252行，保存关系首次/最近证据年、两端首次论文年、起源
  时滞、时间对齐状态和路径资格；`last_evidence_year`不是关系终止时间。
- 新增 `ads_technology_evolution_path_step` 47,909行，提供12,891条最多8步的代表路径。每个目标只
  保留一个确定性最佳前驱链；完整分支必须查询evolution edge，代表路径不能解释为唯一历史因果。
- 六张Iceberg Stage表逻辑键重复和语义异常均为0，且与Doris逐表行数一致。执行入口为
  `./scripts/publish_technology_graph_ads_v1.sh`，DDL为
  `sql/doris/ads_schema_4_7_0_technology_graph.sql`，报告位于
  `reports/technology_graph_ads_v1_20261016/`。

## 4.6.0 — 2026-10-16

- 新增候选技术分析 ADS 完整发布链路，不再只建设首期优先表。固定读取
  `eto_mvp_cluster_dws_enrichment_v1_20261016` 与既有技术链关系 Snapshot，在独立 Iceberg
  namespace `technology_ads_v1_20261016` 物化后，幂等发布到 Doris
  `gkx_technology_analysis_dev`；来源 DWD/DWS 与外部文件保持只读。
- 新增22张 ADS 表，覆盖候选技术画像、图谱边、代表论文/专利、关联机构与企业、科研项目案例、
  年度指标、热点信号与快照、产业化潜力分项/总评/证据、阶段研判/证据、区域年度/机构/评估、
  政策证据、八阶段转化流程、堵点评估/证据和十域数据覆盖。ADS 表总数由53张增至75张。
- 当前发布19,430个候选技术节点、587,252条图谱边、108,337条代表论文、172,644条代表专利、
  2,528,802条技术—机构关系和181,735条科研项目案例。关联企业以论文署名机构、已确认专利机构
  和项目机构中的 `company` 类型识别，共99,821条技术—企业关系，覆盖12,018个候选节点；项目案例
  覆盖13,415个节点，明确标记为 `RESEARCH_PROJECT`，不得解释为已验证市场应用。
- 热点模型固定使用2020—2022对照窗与2023—2025近期窗，按增长40%、新增作者扩散15%、新增机构
  扩散15%、同期影响15%和专利信号15%加权。发布状态为证据不足15,976、持续增长2,539、成熟766、
  观察146和早期新兴3；当前没有达到 `EMERGING` 阈值的节点。
- 产业化潜力采用科学规模20%、科学增长20%、科学影响15%、专利转化20%、企业参与15%和项目证据
  10%的同批百分位模型；同时发布134,941条可追溯论文、专利与项目证据。阶段研判为可解释规则基线，
  发布工程验证9,022条、早期商业化10,408条，不冒充大语言模型联网研判。
- 发布2,711,376条技术—城市—年度指标、2,528,579条技术—城市—机构关系和1,354,081条区域评估。
  深圳稳定位置ID为 `loc_E16782C21F18EBF8A59C1E98F9C9860B`，当前有15,630条年度区域事实，覆盖
  6,233个候选节点；区域分数仅比较论文、专利、项目和企业内部证据。
- `ads_technology_policy_evidence` 与 `ads_technology_bottleneck_evidence` 当前为空表；市场、政策、
  专家因果知识和审核中文翻译尚无注册来源。十域覆盖表以 `NOT_AVAILABLE`/`PENDING` 明确表达缺失，
  技术名称、说明和关键词的中文字段保留NULL或空数组，禁止自动填造。
- 22张 Iceberg Stage 表与22张 Doris 表行数逐表一致，逻辑键重复和语义异常均为0；项目案例年份在
  Doris 使用 `INT` 以兼容 Iceberg Connector，业务语义仍为年份。构建、迁移、加载入口为
  `./scripts/publish_technology_ads_v1.sh`，配置为 `config/technology_ads_v1.json`，Doris DDL 为
  `sql/doris/ads_schema_4_6_0_technology.sql`；物化、Stage校验和加载报告位于
  `reports/technology_ads_v1_20261016/`。

## 4.5.0 — 2026-10-15

- 将 `ads_talent_yearly_location` 从空表预留升级为可发布年度观察事实：固定读取 ORCID 教育/工作
  经历与机构位置 Snapshot；已知结束年的经历按闭区间展开，结束时间未知时只保留开始年，禁止把
  空结束时间推断为持续在任。新增 `primary_experience_type` 和 `orcid_education_count`。
- 新增 `ads_talent_yearly_discipline`，从发布 MVP core 论文按人才、年份、Field 聚合，并以论文数、
  累计被引和 Field ID 确定唯一年度 Primary Field；同一论文同一 Field 先去重。
- 新增 `ads_talent_mobility_event`，严格区分 `EDUCATION_TO_WORK`、`WORK_TO_WORK` 和
  `RESEARCH_FIELD_CHANGE`。工作迁移要求前序结束年不晚于后序开始年；重叠任职、同年多机构、年度
  学科缺口以及2026部分年度均不生成正式迁移事件。
- 新增 `ads_talent_mobility_yearly_flow`，预聚合国家、省、城市、机构和 Field 年度有向边；新增
  `ads_talent_mobility_flow_detail`，为流向详情提供Top 10代表机构对和主要Field。
- `ads_geo_yearly_metrics` 新增独立的 `mobility_coverage_status`，避免用人才存量覆盖状态表达流动
  覆盖。流入、流出人数从事件端点按位置和年份重新去重，不能直接相加边级人数；无已观察严格事件
  的已发布Key写0并标记`PARTIAL`，未运行本版本时保持NULL和`NOT_READY`。
- 首版指标版本为 `talent_observed_mobility_mvp_v1`，数据版本为 `202610150301`。所有输入固定到
  Iceberg Snapshot，物化到独立 namespace 后校验并幂等写入；不修改 ORCID、OpenAlex 或机构来源事实。
- 已发布211,678条年度位置（28,809人）、3,790,547条年度Field（99,998人）、298,384条迁移事件、
  51,489条年度流向边和65,105条TopN明细。事件包括教育到工作7,991条、工作到工作9,276条、
  相邻完整年度Primary Field变化281,117条；2026领域变化0条。
- 地区年度表171,736行已全部回填非空流入、流出和事件数并标记`PARTIAL`。全部新表Key重复、人才/
  机构/Field孤儿、年度位置权重、唯一Primary位置/Field、流向自环、TopN排名异常均为0。
- 迁移、配置、执行入口和说明分别为
  `sql/doris/ads_schema_4_5_0_talent_mobility.sql`、
  `config/talent_mobility_mvp_v1.json`、
  `./scripts/publish_talent_mobility_mvp_v1.sh` 和
  `docs/talent_mobility_mvp_v1.md`；发布核验见
  `reports/talent_mobility_mvp_v1/post_run_verification.md`。

## 4.4.0 — 2026-10-15

- 新增 `ads_emerging_topic_yearly_metrics`、`ads_emerging_topic_snapshot` 和
  `ads_emerging_topic_key_talent`，分别承载Topic年度趋势、当前新兴度判定和关键MVP人才。
- 首版固定使用400万篇MVP core的Primary Topic；正式评分使用2017—2025，2020—2022为对照窗，
  2023—2025为近期窗。2015固定为左截断，2026固定为部分年度且不进入评分。
- 新兴度只在通过近期论文50、活跃年份5、近期作者20和近期机构5四项规模门槛后计算；相对增长、
  加速度、作者扩散、机构扩散、同年同Subfield影响和持续性的权重依次为30%、20%、15%、15%、
  10%和10%。累计引用不进入新兴度。
- 固定发布 `EMERGING/EARLY_EMERGING/WATCH/ESTABLISHED_GROWING/TRANSIENT_SPIKE/MATURE/`
  `INSUFFICIENT_EVIDENCE` 七种状态，区分快速增长的成熟方向、短期尖峰和证据不足。
- 关键人才只从已发布MVP人才中选择，要求近期至少2篇Primary Topic论文，每个入选Topic最多20人；
  FWCI缺失时不写0，使用75%可用权重归一并显式发布覆盖率。
- 已发布53,952条年度趋势、4,496条Topic快照和20,235条关键人才关系；状态分布为
  `EMERGING=133`、`EARLY_EMERGING=219`、`WATCH=806`、`TRANSIENT_SPIKE=53`、
  `MATURE=2,032`、`INSUFFICIENT_EVIDENCE=1,253`，本批`ESTABLISHED_GROWING=0`。
- 三张表Key重复、Topic/人才孤儿、覆盖状态、数值范围和Top 20排名异常均为0；676条关键人才因
  FWCI不可用以0.75覆盖权重归一，19,559条覆盖完整。相同版本重跑源目标行数不变。
- 迁移、配置、执行入口和说明分别为
  `sql/doris/ads_schema_4_4_0_emerging_topic.sql`、
  `config/emerging_topic_mvp_v1.json`、
  `./scripts/publish_emerging_topic_mvp_v1.sh` 和
  `docs/emerging_topic_mvp_v1.md`；核验报告为
  `reports/emerging_topic_mvp_v1/post_run_verification.md`。

## 4.3.0 — 2026-10-15

- 发布 `ads_talent_similarity` 的 `research_topic_single_anchor_v1`：每名人才只选择论文数最高的
  Primary Topic，围绕该 Topic 做一次倒排召回并保留 Top 3。
- Primary Topic 并列依次按2021—2025 Primary论文数、最近年份和Topic ID裁决；没有Primary但有
  普通Topic时使用固定种子哈希作确定性伪随机兜底，禁止真随机破坏幂等。
- 新增 `similarity_topic_id`、`topic_selection_method`、`topic_primary_paper_count`、
  `topic_paper_count` 和 `similar_talent_topic_paper_count` 五个可空业务字段。`research_topic` 必填，
  其他相似类型保持NULL。
- 相似度为双方在主体锚点Topic上的有界聚焦度几何平均；聚焦度只使用论文覆盖率和
  `1-exp(-paper_count/3)`证据系数，不混入引用、学术力、潜力、合作、机构、专利或产业指标。
- 新增只读 `ads_talent_similarity_card`，实时关联候选人才主画像与公共Topic维表，向前端提供姓名、
  头像、当前/最后已解析机构及Topic中英文名；这些展示属性不复制到相似度事实表。
- 固定五个输入Snapshot，物化99,998个锚点和299,994条Top 3结果；当前全部锚点均来自Primary
  Topic，随机兜底0人，另有2人无Topic证据。Primary冲突、关系不一致、重复键、自环、公式、排名、
  人才孤儿和Topic孤儿异常均为0；幂等重跑未重复写入。
- 迁移、配置、发布入口、运行说明和核验报告分别为
  `sql/doris/ads_schema_4_3_0_talent_similarity.sql`、
  `config/talent_similarity_topic_mvp_v1.json`、
  `./scripts/publish_talent_similarity_topic_mvp_v1.sh`、
  `docs/talent_similarity_topic_mvp_v1.md` 和
  `reports/talent_similarity_topic_mvp_v1/post_run_verification.md`。

## 2026-10-24 地区年度人才数发布（无物理 Schema 变更）

- 为 `ads_geo_yearly_metrics.talent_count` 发布 `geo_yearly_observed_talent_mvp_v1`：限定已发布
  100,000 名 MVP 人才，以固定 MVP core 论文的发表年和署名机构已解析位置为同期证据，在
  `location_id, statistics_year` 内按人才去重。
- 本指标直接从人才—论文—署名机构事实重新去重，禁止把
  `ads_geo_yearly_discipline_metrics.talent_count` 跨 Topic 相加；同一人才跨 Topic 会重复。
- 2015–2026 的已发布 Key 无匹配证据时写 0，状态为 `PARTIAL`；2000–2014 写 NULL，状态为
  `NOT_AVAILABLE`。`talent_participation_count` 和 `new_talent_count` 继续保持 NULL。
- 采用 2015–2026 分年 Iceberg CTAS，固定所有输入 Snapshot；Doris 以局部列 Stream Load 和
  `data_version=202610240102` 更新，保留既有论文、项目、机构和流动字段，并对发布前后非目标指标
  汇总执行一致性门禁。
- 没有新增、删除或改型字段，ADS Schema version 不因本次数据发布提升。执行入口为
  `./scripts/publish_geo_yearly_talent_v1.sh`，口径与校验见
  `docs/geo_ads_yearly_talent_v1.md`，实际结果见
  `reports/geo_ads_yearly_talent_v1/post_run_verification.md`。

## 2026-10-14 地区年度 Primary Topic 人才数发布（无物理 Schema 变更）

- 为 `ads_geo_yearly_discipline_metrics.talent_count` 发布
  `geo_yearly_primary_talent_mvp_v1`：限定已发布 100,000 名 MVP 人才，以固定 MVP core 论文的
  发表年、Primary Topic 和署名机构已解析位置为同期证据，在
  `location_id, statistics_year, topic_id` 内按人才去重。
- 2015–2026 的已发布 Key 无匹配证据时写 0，`talent_coverage_status='PARTIAL'`；2000–2014
  继续写 NULL，状态改为 `NOT_AVAILABLE`。2026 按 `2026-09-18` 截止日解释为部分年度。
- `PARTIAL` 明确表示：`associated_talent_count` 仍为 NULL、部分论文无 Primary Topic、少量署名
  机构无位置映射，且 ORCID 年度任职和 `ads_talent_yearly_location` 尚未进入本指标。不得将该指标
  解释为居住人口、当前任职、实际入职或人才流动。
- 采用 2015–2026 分年 Iceberg CTAS，控制 `COUNT(DISTINCT talent)` 聚合内存；固定所有输入
  Snapshot，生成独立 `geo_ads_primary_talent_v1_stage`，再以
  `data_version=202610140401` 幂等发布。执行入口为
  `./scripts/publish_geo_primary_talent_v1.sh`，详细口径与校验见
  `docs/geo_ads_primary_talent_v1.md`，实际发布结果见
  `reports/geo_ads_primary_talent_v1/post_run_verification.md`。
- 本次没有新增、删除或改型字段，ADS Schema version 保持 4.2.0。

## 2026-10-14 Talent Potential 推荐理由中文化（无 Schema 变更）

- 将 `ads_talent_potential_result.potential_reason` 及主画像投影中的展示短语“同主Field”统一改为
  “同主学科”；仅调整中文展示，不改变主 Field ID、比较组、评分、排名、阈值或入选结果。
- 结果数据版本提升为 `202610140304`，主画像投影版本提升为 `202610140305`；发布模板同步修改，
  后续确定性重跑不会恢复旧文案。

## 4.2.0 — 2026-10-14

- 新增 `ads_talent_potential_result`，以 `talent_id, model_version` 保存人才潜力的原始指标、同组
  分项百分位、比较组、覆盖状态、最终分数、入选结果、确定性解释和固定来源版本。
- `talent_potential_mvp_v1` 只使用 2021—2025 五个完整自然年及固定 MVP core Work Snapshot
  `4292018784001736547`。比较组为主 Field × 科研年限段，基础合格组至少 200 人。
- 综合模型固定为 35% 近期 Field-发表年归一化影响力、25% 引用增长、20% 产出增长、15% 第一/通讯
  作者领导力和 5% 新 Topic 拓展；综合分再次转为同组0—100平均并列百分位。
- 近五年论文不少于5篇、至少3个活跃年份、科研年限不少于3年且覆盖完整者才进入评估；潜力百分位
  不低于90时 `is_potential_talent=1`。未评估保持 NULL，不写成0或“非潜力人才”。
- `ads_talent_profile` 增加 `potential_score_version`、`potential_metric_coverage` 和
  `potential_metrics_as_of_date`；原有三个业务字段只投影当前发布结果，`score_version` 继续只表示
  学术力模型版本。
- 当前以结果 `data_version=202610140304`、主画像投影 `data_version=202610140305` 发布100,000行：
  80,170人合格并获得分数，8,038人为潜力人才，
  72,132人已评估未入选，19,830人因证据或比较组不足未评估。Key、分数范围、阈值、NULL语义和
  主画像逐行投影异常均为0。
- 迁移、发布、分片投影和运行说明分别为
  `sql/doris/ads_schema_4_2_0_talent_potential.sql`、
  `sql/doris/publish_talent_potential_mvp_v1.sql`、
  `sql/doris/sync_talent_potential_profile_mvp_v1.sql` 和
  `docs/talent_potential_mvp_v1.md`。本次只读固定 Iceberg/ADS 输入，未修改任何来源数据。

## 2026-10-14 Talent Profile 当前机构位置回填（无 Schema 变更）

- 使用 `ads_talent_profile.current_institution_ids` 唯一机构 ID 关联
  `ads_institution_profile`，只对 `location_resolution_status='resolved'` 的机构回填人才主画像
  `country_code/country_name/province/city/location_display`。
- `location_display` 按国家、省州、城市顺序去空、去重后使用 ` / ` 连接。这些字段明确表示当前机构
  所在地代理，不表示已经核验的人才居住地。
- 未解析位置不使用 `ads_talent_experience` 或 `current_institution` 中的自由文本兜底；没有可靠机构
  位置的人才继续保持 NULL。
- 本次不新增字段或表，ADS Schema 保持 4.1.0；发布入口为
  `uv run --frozen python -m app.cli.main talent-ads profile-location-sync --config
  config/talent_ads_mvp_core_v1.json`。
- 已以 `data_version=202610140201` 发布 38,467 名人才能够；国家、城市和展示文案均为 38,467 条，
  省州为 36,789 条，来源—目标字段差异、未解析位置误填和展示格式异常均为 0。核验报告为
  `reports/talent_ads/profile_location_sync_20261014.md`。

## 4.1.0 — 2026-10-14

- 将 `ads_talent_industry_capability_simulation` 的技术映射模拟与无映射兜底模拟合并为一个全量覆盖
  方案。仍命中正式 IPC/CPC 技术映射的行继续按去重技术—专利组合单元数加权；未命中的行使用
  `SHA256(simulation_seed|talent_id|taxonomy_id|industry_id)` 前 60 bit 映射到 0–100。
- `simulation_coverage_status` 统一为 `TECHNOLOGY_WEIGHTED` 或
  `DETERMINISTIC_HASH_FALLBACK`。后者只生成可复算的情景值，不伪造技术关系，技术命中计数保持 0。
- 全部人才—产业行现在都有 `synthetic_commercial_value_score`、综合模拟分、稳定排名及百分位；同产业
  基准人数与正式 `ads_talent_industry_activity` 行数对账。
- 为满足单一模拟方案要求，继续使用
  `simulation_version='talent_industry_commercial_value_simulation_v1'`，以更高的
  `data_version=202610140101` 原 Key 覆盖旧模拟行，而不并存第二套 v2。发布报告保留本次算法、固定种子、
  技术加权数和兜底数以供审计。
- 正式 `ads_talent_industry_activity` 不修改；所有值继续明确标记为 `SYNTHETIC_SIMULATION`，不得解释为
  许可、转让、收入、估值或人才真实产业能力。

## 4.0.0 — 2026-10-14

- 将 `ads_talent_patent.patent_type` 重命名为 `application_kind`，与
  `ads_patent_profile.application_kind` 保持同名同义。已发布字段重命名不向后兼容，因此主版本
  升至 4.0.0。
- `application_kind` 保留 Google Patents 原始大写代码，不写入本地化文本，不用
  `unknown` 覆盖未识别的原始值。已确认 `A=Patent`；`V` / `D` 的展示分类为
  `unknown`。
- 标准中文展示名称为 `W=PCT 国际申请（《专利合作条约》国际申请）`、
  `T=Translation（译文文献）`。展示字典与原始事实字段分离。
- 迁移先重命名并扩容字段，再从 `ads_patent_profile.application_kind` 按
  `patent_id` 回填人才专利关系；回填使用部分列 Stream Load、新 `data_version`、严格行数
  及空值对账，不修改 Google 来源数据。
- 迁移与运行说明分别为
  `sql/doris/ads_schema_4_0_0_talent_patent_application_kind.sql` 和
  `docs/ads_schema_4_0_0_talent_patent_application_kind.md`。
- 已完成当前 Doris 迁移与回填：85,069 行全部匹配 Patent Profile，非空
  `application_kind` 85,069 行，回读差异 0；原始代码分布为 `A=84,913`、`F=119`、
  `V=28`、`D=9`。核验报告为
  `reports/talent_ads/ads_schema_4_0_0_application_kind_20261014.md`。

## 3.0.0 — 2026-10-14

### 人才分类 MVP v2 修正发布

- 新增可执行发布脚本 `sql/doris/ads_talent_classification_mvp_v2_publish.sql`，向统一 taxonomy 模型发布
  `talent_classification_mvp_v2_2026-09-18`；遗漏 rank 101–200 的 v1 release 标记为 `SUPERSEDED`。
- 领军人才为学术力前 0.1%；专家修正为排名区间 `(0.1%, 1%]`，即当前 rank 101–1,000；青年人才为 MVP 首篇论文位于最近
  5 个自然年且 MVP 全部论文累计被引不少于 10。青年人才与前两类不互斥。
- 当前固定 100,000 人发布产生领军 100、专家 900、青年 6,918，共 7,918 条分类关系；
  `ads_talent_taxonomy_metrics` 按节点保存去重人数，并可对三个节点的 `direct_talent_count` 求和。

- 从 `ads_talent_profile` 删除未定义、未发布计算结果的单值
  `industrial_capability`，并删除无权威来源、无发布逻辑且现有 100,000 行均为 NULL 的
  `talent_type_id` / `talent_type_name` 及无效索引 `idx_talent_type_id`。这是不兼容 Schema 变更，
  因此 ADS Schema 主版本升至 3.0.0。
- `ads_talent_industry_activity.industry_activity_score` 继续作为“人才 × taxonomy × 产业节点”
  粒度的产业技术活动分，不回填主画像，不冒充完整产业力，也不在未定义聚合规则时压缩为人才级单值。
- `ads_talent_yearly_metrics.industrial_capability` 是独立的年度预留字段，本次不删除，不改变年度表结构或口径。
- 保留并扩展 `ads_talent_taxonomy`，以 `taxonomy_kind` 区分产品派生分类、成员身份、人才计划和奖项；
  新建 `ads_talent_taxonomy_node`、`ads_talent_taxonomy_relation`、`ads_talent_taxonomy_closure`
  和 `ads_talent_taxonomy_metrics`，同时支持任意深度树与扁平独立称谓。
- 删除未发布数据的 `ads_talent_classification_node`、`ads_talent_classification`、
  `ads_talent_classification_closure`、`ads_talent_classification_metrics`、
  `ads_talent_label_dictionary` 和 `ads_talent_label`。节点表即统一称谓字典，关系表即唯一 ADS 人才—节点投影，
  不再同时维护 classification 与 label 两套事实。逻辑 ADS 表数由 47 降至 45。
- DWD 权威事实仍分别保存在分类、成员身份、人才计划和奖项表；ADS 只统一检索投影，
  `source_fact_type + source_fact_id` 必须可回溯到 DWD 来源事实。
- 在执行迁移前，下游必须停止选取三个待删列并确认其非 NULL 行数均为 0；迁移后通过
  `information_schema.columns` 确认字段已删除，确认废弃索引不存在，并核对主画像总行数和 `talent_id` 唯一性不变。
- 迁移为 `sql/doris/ads_schema_3_0_0_talent_profile_cleanup.sql`，执行手册为
  `docs/ads_schema_3_0_0_talent_profile_cleanup.md`；本次不重算、不重发布、不修改
  `ads_talent_industry_activity` 或任何来源数据。
- Taxonomy 重构迁移为 `sql/doris/ads_schema_3_0_0_talent_taxonomy_unification.sql`，执行、核验和最终人才
  分类方案见 `docs/ads_schema_3_0_0_talent_taxonomy.md`。已完成当前 Doris 结构迁移：五张新表已创建且
  均为 0 行，旧 classification/label 表不存在，人才主画像仍为 100,000 个唯一 `talent_id`。
  本次未发布 taxonomy 节点或人才关系，核验报告为
  `reports/talent_taxonomy_v3/schema_migration_report.md`。

## 2026-10-13 Talent Profile 当前机构回填（无 Schema 变更）

- 从 `ads_talent_experience` 为每名人才确定性选择最后一段已解析机构的经历，回填
  `ads_talent_profile.current_institution` 与 `current_institution_ids`。
- 排序优先使用可靠的 `is_current=1`，随后按开始时间、结束时间、工作经历和稳定
  `experience_id` 裁决；`is_current=NULL` 不等同于当前在任。
- `current_institution` 同时保留展示名称、类型、地理、档案质量和来源经历信息；没有已解析经历的
  人才保持 NULL，不根据自由文本猜测统一机构 ID。
- 本次不新增字段或表，ADS Schema 保持 2.3.0；发布入口为
  `python -m app.cli.main talent-ads orcid-experience-profile-sync --config
  config/talent_ads_mvp_core_v1.json`。
- 已以 `data_version=202610130001` 回填 49,279 名具备已解析经历的人才；来源经历、VARIANT 内机构
  ID、机构 ID 数组、机构引用完整性和行数对账异常均为 0。其余 50,721 名人才能够没有可用经历，
  两字段按契约保持 NULL。核验报告：
  `reports/orcid_experience_v1/talent_profile_current_institution_sync_20261013.md`。

## 2.3.0 — 2026-10-13

- 新增 `ads_technology_commercial_value_simulation`：对固定目录内每个稳定 `tech_id` 使用固定种子
  和 SHA-256 生成可复现的0–100情景值。全部行强制标记 `SYNTHETIC_SIMULATION`，不表示真实许可、
  转让、收入或估值。
- 新增 `ads_talent_industry_capability_simulation`：仅通过已发布 IPC/CPC `RELATED` 映射及同一件专利
  的产业命中建立人才—技术—产业聚合，按去重专利组合单元数加权技术模拟分；不随机伪造关系。
- 模拟产业力公式为 `0.75 * official_industry_activity_score + 0.25 *
  synthetic_commercial_value_score`。无正式技术命中的行保持模拟分与排名为 NULL，并显式记录覆盖状态。
- 两张模拟表与正式 `ads_talent_industry_activity` 物理隔离；正式商业价值预留、活动分和正式排名均不
  覆盖。ADS 表数由45增至47。
- 迁移、发布入口与运行说明分别为
  `sql/doris/ads_schema_2_3_0_talent_industry_simulation.sql`、
  `./scripts/publish_talent_industry_commercial_value_simulation_v1.sh` 和
  `docs/talent_industry_commercial_value_simulation_v1.md`。
- 已以 `data_version=202610130101` 发布8条技术模拟记录和397,964条人才—产业模拟记录；其中
  1,777条存在正式技术映射并生成模拟产业力，覆盖6,398名人才和1,129个产业节点。业务Key重复、
  分数范围、公式、排名、行数对账、未知状态及正式商业价值字段误填异常均为0。核验报告：
  `reports/talent_industry_commercial_value_simulation_v1/publication_report.json`。

## 2.2.1 — 2026-10-13

- 在平台主体命名表补充 `talent`：ADS 对外统一使用 `talent` / `talent_id`，DWD `author_id`
  仅通过 identity bridge 映射，不作为 ADS 平台主键。
- 将 `ads_talent_industry_activity` 的字段组摘要展开为逐字段契约，逐项明确 Doris 类型、业务语义、
  NULL/0 边界、评分与排名口径、项目归因状态、商业化预留及版本来源。
- 本次仅修正文档完整性，不改变 2.2.0 已发布表结构、数据、评分公式或 `data_version`。

## 2.2.0 — 2026-10-12

- 新增 `ads_talent_industry_activity`，按人才、产业 taxonomy 和产业节点保存专利活动、成熟授权率、
  已确认项目角色背景、可解释分项分、固定产业基准排名与数据覆盖状态。
- 专利优先按 Google family 去重，缺失时回退 publication；多产业和多名已发布关联人才采用分数
  计数。成熟授权率仅使用申请日至少满三年的组合单元，并使用强度为 10 的产业总体先验平滑；
  授权率明确不解释为专利转化率。
- 项目只统计 `is_lead` 和 `is_direct_investigator` 直接事实，排除仅由受资助论文署名推导的关系。
  因当前没有可靠 Project–Industry 事实，项目指标只作为同产业候选人的全局执行背景，显式标记
  `project_attribution_status=TALENT_GLOBAL_CONTEXT`。若发布中完全没有直接项目关系，项目计数和
  分数保持 NULL、覆盖状态为 `NOT_AVAILABLE`，不把未知写成 0。
- `talent_industry_activity_mvp_v1` 的目标权重为 60% 专利活动与 40% 项目执行背景；缺少直接项目
  覆盖时只对可用专利分归一并记录 `activity_metric_weight_coverage=0.6000`。该名称和结果不表示
  完整产业力；完整商业化能力不从专利数量推断。
- 预留已转化专利族数、转化率、转化分、已实现商业价值、币种和商业价值分；本版全部保持 NULL，
  覆盖状态为 `NOT_AVAILABLE`，不填 0，也不把商业化权重重分配到当前分数。
- 迁移为 `sql/doris/ads_schema_2_2_0_talent_industry_activity.sql`，发布模板为
  `sql/doris/publish_talent_industry_activity_mvp_v1.sql`，入口为
  `./scripts/publish_talent_industry_activity_mvp_v1.sh`。ADS 表数由 44 增至 45。
- 已以 `data_version=202610120102` 发布 397,964 行，覆盖 6,398 名人才和 1,129 个产业节点，
  其中四位小类 209,924 行。当前 7,702,366 条人才—项目关系全部是
  `funded_output_author`，因此全部行的项目与商业化维度均保持 `NOT_AVAILABLE`；业务 Key、分数、
  排名、基准人数、版本覆盖、人才/产业孤儿和空位约束异常均为 0。核验报告：
  `reports/talent_industry_activity_mvp_v1/publication_report.json`。

## 2.1.0 — 2026-10-12

- 在 `ads_talent_profile` 增加学术力可解释分项：论文、被引、H 指数、合作广度和
  CWTS Core 来源覆盖分，同时增加 Core 可评价论文数、Core 论文数、占比、默认
  权重覆盖率、固定基准总体人数和稳定排名。
- `talent_academic_mvp_v1` 默认公式为
  `0.20*paper + 0.30*citation + 0.30*h_index + 0.15*collaboration + 0.05*core`；
  前四项使用固定 MVP 人才总体的平均并列排名百分位，Core 分为 Core 论文占
  `is_core` 状态已知论文的比例乘 100。
- Core 分缺失时不当作 0，而是从分子和分母同时剔除 0.05 权重；
  `academic_metric_weight_coverage=0.9500`。页面自定义权重同样只对非 NULL 分项分重新归一。
- 发布只能读取 MVP bundle 固定的、包含 `dwd_source.is_core` 的 Iceberg Snapshot。
  旧 Source Dataset 不原地回填；缺列时 Pipeline 必须失败。
- Doris 增量建表迁移为
  `sql/doris/ads_schema_2_1_0_talent_academic_capability.sql`。当前提交交付 Schema、可重算 SQL
  和校验契约；在新 DWD Source 与新 MVP bundle 发布前，不伪称已回填生产分数。

## 2.0.0 — 2026-10-12

- 新增 `ads_talent_taxonomy`、`ads_talent_classification_node`、
  `ads_talent_classification_closure`、`ads_talent_classification` 和
  `ads_talent_classification_metrics`，以不可变 taxonomy release、任意深度节点树、多对多人才关系
  和可重建节点卡片聚合替代固定三级分类数组。
- 新增 `ads_talent_label_dictionary` 与 `ads_talent_label`，统一提供分类、院士/Fellow 等成员身份、
  人才计划和奖项称谓的检索投影；DWD 各领域事实仍是权威来源，不把不同语义压成单一标签事实。
- 从 `ads_talent_profile` 移除 `classifications`、`classification_l1_ids`、
  `classification_l2_ids`、`classification_l3_ids`、`honor_titles`、`honor_title_ids`、
  `talent_plans` 和 `talent_plan_ids`。保留 `is_academician` 作为定义明确的高频派生兼容字段，
  不新增单值 `level` 或不断增长的 `is_*` 列。
- 人才主分类通过 `ads_talent_classification` 的 `is_primary` 表达，且只在同一人才、同一
  `taxonomy_id + release_id` 内唯一；名称通过节点维表 JOIN 获取。Doris 不强制外键但支持 JOIN，
  所有节点、人才、label 和来源事实引用完整性由发布 Pipeline 的 LEFT JOIN 孤儿校验保证。
- 迁移分两阶段：
  `sql/doris/ads_schema_2_0_0_talent_taxonomy.sql` 只创建新表；完成回填、关系完整性校验、下游切换
  和可恢复备份后，才允许执行
  `sql/doris/ads_schema_2_0_0_talent_taxonomy_finalize.sql` 删除旧列及其倒排索引。禁止直接运行
  finalize 丢弃尚未迁移的称谓数据。
- 这是不兼容主版本升级。ADS 表数由 37 增至 44；本提交只交付结构、契约和迁移顺序，未伪称已向
  Doris 发布 taxonomy、称谓或人才关系数据。

## 1.13.0 — 2026-10-11

- 新增 `ads_institution_technology_power`，按 `institution_id` 保存论文数、累计被引、人才数、
  机构学科画像 Topic 数以及四项标准化分、固定权重、综合技术力分和稳定排名。
- 只有 `paper_count > 0` 的机构进入固定基准总体；每项原始指标使用全体合格机构的平均并列排名
  转换为 0–100 分，不随前端临时选择的对比机构变化。
- `institution_technology_power_mvp_v1` 的综合公式固定为
  `0.35 * paper_score + 0.30 * citation_score + 0.25 * talent_score + 0.10 * topic_score`。
- 该结果只表示固定 MVP core 观察集合内的相对科研技术力，不表示科研投入、专利所有权或产业化
  能力；无论文证据的机构不发布零分行。
- 建表迁移：`sql/doris/ads_schema_1_13_0_institution_technology_power.sql`；发布 SQL：
  `sql/doris/publish_institution_technology_power_mvp_v1.sql`；运行说明：
  `docs/institution_technology_power_mvp_v1.md`。ADS 表数由 36 增至 37。
- 首次发布 64,698 家 `paper_count > 0` 的机构，业务 Key 与排名均无重复，分数越界、权重和
  公式对账异常均为 0；143 家机构因没有已发布机构 Topic 关系而以 `topic_count=0` 参与计算。
  核验报告：`reports/institution_technology_power_mvp_v1/post_run_verification.md`。

## 1.12.0 — 2026-10-11

- 新增 `ads_institution_topic_entry`，按 `institution_id, topic_id` 保存机构在固定 MVP core 的
  Primary Topic 中首次被观察到的论文年份。
- 口径只接受发布的 400 万篇 MVP core 和 `dwd_work_topic.is_primary=true`；同一论文同一机构
  多署名先去重，不把 Associated Topic 的弱关联作为进入证据。
- 2015 年标记为 `BASELINE_LEFT_CENSORED`，2016–2025 为 `COMPLETE`，2026 为
  `PARTIAL_YEAR`。该事实不表示机构成立或真实历史首次进入领域。
- 多 Topic 统计先按机构取所选 Topic 的最早年份再去重，禁止直接相加各 Topic 新增量。
- 迁移脚本：`sql/doris/ads_schema_1_12_0_institution_topic_entry.sql`；发布入口：
  `./scripts/publish_institution_topic_entry_ads.sh`；运行说明：
  `docs/institution_topic_entry_ads_v1.md`。ADS 表数由 35 增至 36。
- 首次发布 Iceberg 与 Doris 均为 3,358,401 行，覆盖 64,555 家机构和 4,468 个具有
  Primary Topic 论文证据的 Topic；业务 Key 重复、机构/Topic 孤儿、状态年份错误和论文计数
  异常均为 0。核验报告：`reports/institution_topic_entry_ads_v1/post_run_verification.md`。

## 1.11.0 — 2026-10-11

- 新增 `ads_industry` 和 `ads_institution_industry`，首版使用国家知识产权局
  《国际专利分类与国民经济行业分类参照关系表（2018）》和 GB/T 4754—2017。
- 产业维表发布门类、大类、中类、小类四级路径；机构产业表按
  `institution_id, taxonomy_id, industry_id` 唯一。
- 机构专利仅使用不可变 `google_patents_institution_v1_20261011` 中的 confirmed
  assignee 关系；不混入发明人任职推导关系。
- 专利优先按 Google family ID 去重，无 family 时回退 publication ID；多产业使用
  `1/N` 分数计数，同机构同层级 `industry_share` 之和对账为 1。
- 完全对应（官方 `*`）与非完全对应参照关系分开计数；首版通过固定
  IPC 2026.01 节点的真实父链展开，不用字符串前缀猜测跨版本归属。
- `project_count` 与 `inventor_affiliation_patent_count` 首版为 NULL，不写 0 冒充确认没有。
- 迁移脚本：`sql/doris/ads_schema_1_11_0_institution_industry.sql`；发布入口：
  `./scripts/publish_institution_industry_ads.sh`。ADS 表数由 33 增至 35。
- 首次正式发布产业节点 1,971 行、机构产业事实 343,429 行，覆盖 3,756 家机构；
  Iceberg 与 Doris 行数一致，机构/产业孤儿、业务 Key 重复、分数权重及层级份额异常均为 0。
- 当前 2018.1 参照表的 7,477 个去重 IPC 映射代码中，224 个历史代码无法在
  IPC 2026.01 真实父链中找到，已保留于质量报告，未使用字符串前缀猜测。
- 运行和口径说明：`docs/institution_industry_ads_v1.md`；核验报告：
  `reports/institution_industry_ads_v1/quality_report.json` 和
  `reports/institution_industry_ads_v1/load_report.json`。

## 1.10.0 — 2026-10-11

- 新增 `ads_institution_collaboration_yearly`，按
  `institution_id, collaborator_institution_id, statistics_year` 发布机构年度有向合作边，支持目标
  机构、合作机构类型、论文/专利来源和时间范围筛选。
- 论文合作固定使用 MVP core、Authorship–Institution 与 Institution Profile Iceberg Snapshot；
  同时发布共同论文数、跨作者合作论文数、同一作者多机构署名论文数、被引、FWCI、OA、地域分类
  和有向合作强度。
- 为避免大型联盟论文的完全图膨胀，只有关联 2–10 家机构的论文进入合作计算；关联 11 家及以上
  机构的论文整篇排除，不截取前 10 家机构。此前按无限制机构共现物化的 63,890,658 行不是正式
  发布口径，必须重建且不得继续下游使用。
- A—B 关系同时发布两个方向；发布校验覆盖业务 Key 唯一、自环为 0、正反边完整以及论文分类计数
  对账。网络排名和中心性按用户选择的来源与时间范围动态计算，不固化年度排名。
- Google Patents Assignee 全量展开当前因 Trino 8 GB 单节点内存限制尚未成功，且本次无人工 confirmed
  映射。为避免将自动候选冒充机构合作，首版专利计数及强度保持 NULL，覆盖状态明确写为
  `NOT_AVAILABLE`；后续只允许使用 confirmed assignee 关系增量发布。
- 新增迁移 `sql/doris/ads_schema_1_10_0_institution_collaboration.sql`、发布入口
  `./scripts/publish_institution_collaboration_ads.sh` 和运行说明
  `docs/institution_collaboration_ads_v1.md`。ADS 表数由 32 增至 33。
- max-10 正式口径已发布到 Doris：14,380,180 条年度有向边、59,203 家参与机构，2015–2026
  年逐年与 Iceberg 对账一致；自环、论文分类计数异常和反向边缺失均为 0。错误口径曾写入 Doris
  的 250,000 行已清空，旧 63,890,658 行 Iceberg 派生表与 namespace 已删除，源 Snapshot 未改动。

## 2026-10-10 地区年度 ADS 字段文档补全（无 Schema 变更）

- 为 `ads_talent_yearly_location`、`ads_geo_yearly_metrics`、
  `ads_geo_yearly_discipline_metrics`、`ads_geo_yearly_institution_type_metrics` 和
  `ads_geo_yearly_index` 补充逐字段 Doris 类型、可空性和业务说明。
- 本次仅修复 1.6.0 逻辑文档遗漏；表结构、逻辑主键、指标口径、数据版本和已发布数据均未变化，
  Schema version 继续为 1.9.0。

## 2026-10-10 中国位置中文名发布（无 Schema 变更）

- 新建不可变 DIM `location_v1_3_20261010`，为中国 1 个国家、31 个省级和 604 个城市位置发布
  中文名称治理补丁；634 个位置有可追溯中文名，2 个歧义城市保持 NULL 等待人工审核。
- 同步更新 Doris `ads_location` 和 `ads_location_external_id` 的 `location_release_id`；位置
  `data_version=202610100301`，不改变既有 `location_id`、层级、坐标或外部 ID 映射。
- 按稳定位置 ID 同步 `ads_institution_profile.country_name/province_name/city_name`，再将已关联
  中国机构的位置展示同步到 `ads_talent_experience.country_name/city`；数据版本分别为
  `202610100302` 和 `202610100304`。其中经历同步只接受同国家机构画像，避免将来源国家冲突的
  机构城市误写入中国经历。
- `ads_talent_profile` 当前没有可用的中国位置 ID 关联，因此不凭自由文本覆盖；地理年度宽表
  只保存 `location_id`，无需冗余名称更新。
- 没有修改 ADS 表结构，因此 Schema 保持 1.9.0；发布入口为
  `./scripts/publish_location_zh_cn.sh`。

## 2026-10-09 Talent Experience 中国机构中文名同步（无 Schema 变更）

- 以 `ads_institution_profile.name_zh` 为权威值，将 48,606 条已关联中国机构的
  `ads_talent_experience.institution_name` 同步为中文名。
- `institution_name_en` 优先使用机构画像英文名，再回退经历原英文名称；48,478 条具有英文名，
  其余 128 条因机构画像和来源均无可靠英文名而保持 NULL。
- 同步数据版本为 `202610090201`，高于基础 ORCID 经历版本，旧批次不能覆盖。
- 同步后 Talent Experience 仍为 140,887 行，业务键重复、机构孤儿和中文名不一致均为 0。
- 无需新增字段或修改表结构，因此 ADS Schema 保持 1.9.0，不创建 1.9.1 migration。
- 核验报告：`reports/orcid_experience_v1/institution_name_sync_verification_20261009.md`。

## 1.9.0 — 2026-10-09

- 新增 `ads_talent_project`，以 `talent_id, project_id` 为唯一键，支持人才查项目和项目反查人才。
- 关系严格区分已对齐的 `dwd_author_grant` Investigator 事实与由 MVP 受资助论文署名推导的
  `funded_output_author`；后者不声明项目负责人或正式成员身份。
- 同步回填 `ads_talent_profile.project_ids`、Top 20 `projects`、`project_count`，并为
  `ads_project_profile` 新增、回填 `talent_count`。
- 按项目 `effective_start_year` 同步 `ads_talent_yearly_metrics.project_count`；缺失开始年的项目
  不进入年度指标。
- 发布口径版本为 `project_mvp_talent_relation_v1`，数据版本为 `202610090200`。
- 迁移脚本：`sql/doris/ads_schema_1_9_0_talent_project.sql`。
- 已发布 7,702,366 条关系，覆盖 93,675 名人才和 1,693,858 个项目；四处关系计数对账一致，
  关系重复键及主体孤儿均为 0。核验报告：
  `reports/project_ads_mvp_v1/ads_schema_1_9_0_verification.md`。

## 1.8.0 — 2026-10-09

- 发布 ORCID employment/education 人才经历，并为 Institution Profile 与 Talent Experience
  增加机构档案等级、解析状态、匹配方法和详情可用性。
- `ads_institution_type` 增加 `funder` 和 `unknown`；后者仅用于来源不足、无法确定类型的名称候选。
- `ads_institution_profile` 增加 `profile_level`、`resolution_status`、`primary_source`。
- `ads_talent_experience` 增加 `institution_profile_level`、
  `institution_resolution_status`、`institution_match_method`、
  `institution_match_confidence`、`institution_detail_available`。
- 为完整保留 ORCID 来源角色原文，将 `degree`/`degree_en` 扩至 512 字符，将
  `position`/`position_en` 扩至 1024 字符。
- OpenAlex full 非 MVP、ROR-only、其他来源 ID 候选及 ORCID 名称候选通过版本化 Institution
  extension 发布；固定 MVP `dwd_institution` 不追加、不覆盖。
- 名称唯一但国家冲突时复用现有 Institution Profile，现有 DWD/ADS 属性优先，并将冲突状态
  保存在 Talent Experience，不用 ORCID 自报位置覆盖机构主数据。

## 2026-10-08 机构人工补录数据发布（无 Schema 变更）

- 审核中国机构补录 CSV，并以 `data_version=202610080201` 发布 828 条机构中文名更新。
- ROR `03xgzn792` 的平台位置校正为中国北京；ROR `04nsks563` 校正为香港。
- 人工值先写入新的 Iceberg DWD Snapshot，再更新 Doris `ads_institution_profile`；旧 DWD
  Snapshot 保留，来源 OpenAlex/ROR 原始事实不改写。
- 后续机构 ADS 重建优先使用已审核 DWD `display_name_zh`，再回退到 ROR 确定性中文名。
- DWD 名称 Snapshot 为 `2417438296715994414`，位置 Snapshot 为
  `2529846747918947389`；机构 ADS 配置已固定到这两个版本。
- Doris 实际影响 829 个唯一机构行（828 条名称更新、2 条位置更新，重叠 1 条）。

## 1.7.0 — 2026-10-08

- 新增 `ads_paper_profile`，严格发布固定 MVP core 的 4,000,000 篇论文；平台 `paper_id`
  复用既有 identity bridge，未把 1,000,000 篇上下文论文带入 ADS。
- 新增 `ads_patent_profile`，按 Google Patent publication 发布 1,768,955 件专利。保留既有
  70,496 个 `pat_` ID，并为剩余 1,698,459 件来源 publication 分配持久平台 ID。
- 新增全局 `ads_patent_cited_paper` 322,951 行，覆盖 228,110 件专利和 120,160 篇发布
  MVP core 论文；该关系不受人才专利子集限制。
- 论文 Profile 保存平台 Topic、当前被引、FWCI、署名/机构数和获取状态；专利 Profile 保存
  发明人、权利人、IPC/CPC、日期及人才/机构/被引论文关系指标。
- 专利 `inventors`、`assignees`、`ipc_classifications`、`cpc_classifications` 均按对象数组发布；
  最终校正版本 `202610080173` 已验证所有非空数组首项为对象，不使用位置数组。
- `is_granted` 统一改为由 `grant_date IS NOT NULL` 决定；同步修正旧人才专利逻辑和 85,069
  条现有关系，其中 1 条原固定为 1 的记录被校正，新旧 Profile 状态不再冲突。
- 兼容性验证通过：现有代表论文、人才专利、人才—专利—论文关系对新主体表的孤儿数均为 0；
  全局关系对两张 Profile 的孤儿数也为 0。
- DDL：`sql/doris/ads_schema_1_7_0_publication_profiles.sql`；发布入口：
  `./scripts/publish_publication_ads.sh`。
- 核验报告：`reports/publication_ads_v1/post_run_verification.md`。

## 1.6.0 — 2026-10-08

- `ads_location` 增加洲级层级、`continent_location_id` 和 `continent_code`；基于 ROR 地址发布
  7 个洲节点，既有国家、省、市平台 ID 保持不变。
- 新增 `ads_talent_yearly_location`、`ads_geo_yearly_metrics`、
  `ads_geo_yearly_discipline_metrics`、`ads_geo_yearly_institution_type_metrics`、
  `ads_geo_yearly_index`。
- `ads_geo_yearly_discipline_metrics` 为宽表，直接包含 Domain/Field/Subfield/Topic 的平台 ID、
  中文名和英文名。
- 已发布：位置 22,220 行、地区年度总指标 171,736 行、地区年度学科指标 10,151,653 行、
  地区年度机构类型指标 349,396 行。
- ORCID Activities 完成前，人才年度位置表和指数表保持空表，所有人才与流动字段保持 NULL；
  2000–2014 年论文字段保持 NULL，不能解释为 0。
- 当前学科表发布 Primary Topic 的论文和项目指标；全 Topic 的 `associated_*` 指标因单节点
  分组资源限制保持 NULL，未以 Primary 指标替代。
- 893,169 条 2000–2014 学科行已用更高数据版本校正为论文数和被引数 NULL，明确表示年度
  论文来源不可用，而不是确认值为 0。
- DDL：`sql/doris/ads_schema_1_6_0_geo_yearly.sql`；发布入口：
  `./scripts/publish_geo_ads.sh`。
- 核验报告：`reports/geo_ads_v1/post_run_verification.md`。

## 1.5.0 — 2026-10-08

- 新增 `ads_discipline_domain`、`ads_discipline_field`、`ads_discipline_subfield`、
  `ads_discipline_topic` 四张公共双语学科维表。
- 所有主键使用公共 identity bridge 中与来源解耦的平台 ID；OpenAlex ID 只作为外部映射。
- Field 保存 Domain，Subfield 保存 Field/Domain，Topic 保存 Subfield/Field/Domain 的完整平台
  ID 路径，并为父级 ID 建立倒排索引，支持从任一级反查 Topic。
- 名称来自 `technology_v2.v_openalex_*_bilingual` 已批准双语视图；完整发布公共分类字典，
  不按 MVP 论文使用情况裁剪。
- 已发布到 Doris：Domain 4 行、Field 26 行、Subfield 252 行、Topic 4,516 行；中英文名称、
  平台 ID 和父级关系完整性核验均通过。
- DDL：`sql/doris/ads_schema_1_5_0_discipline_dimensions.sql`；发布入口：
  `./scripts/publish_discipline_ads.sh`。
- 核验报告：`reports/discipline_ads_v1/post_run_verification.md`。

## 1.4.0 — 2026-10-08

- 新增 `ads_project_profile`、`ads_project_institution`、`ads_project_topic`。
- `ads_institution_profile` 新增 `project_count`，从发布项目–机构关系去重计算。
- 项目平台 ID 使用 `prj_<uuid32>`，通过公共 identity bridge 映射 OpenAlex Grant ID。
- 项目 Topic 由 MVP 受资助论文推测，按论文出现次数、平均 Topic score、稳定哈希确定排名和
  Primary Topic；`topic_id` 倒排索引支持反查项目。
- 项目机构关系直接证据优先；只有完全没有直接匹配的项目才使用论文作者机构兜底。
- OpenAlex 未提供开始年时，使用最早 MVP 受资助论文发表年并明确标记为 inferred。
- 迁移脚本：`sql/doris/ads_schema_1_4_0_project.sql`。

已发布到 Doris：`ads_project_profile` 1,838,841 行、
`ads_project_institution` 22,571,355 行、`ads_project_topic` 11,374,389 行。
1,838,800 个存在 Topic 证据的项目均且仅有一个 Primary Topic；`topic_id` 已建立倒排索引，
支持 Topic 反查 Project。`ads_institution_profile.project_count` 已覆盖全部 68,010 个机构，
其中 20,028 个无关联项目的机构明确写入 0。

核验报告：`reports/project_ads_mvp_v1/post_run_verification.md`。

## 1.3.1 — 2026-10-07

明确机构年度指标口径并发布首批 MVP Institution ADS 数据：

- `new_talent_count`：首次在发布 MVP core 中观察到与机构关联的人才数；
- `fwci`：忽略 NULL、按论文等权 `AVG(fwci)`、不设置最低覆盖率；
- `patent_count`：按申请年统计 `inventor_affiliation` 发明人任职关联专利数，不代表专利权属；
- `project_count` 和机构 Topic `project_count` 因 Grant–Institution/Topic 尚未解析而保持 NULL。

机构平台 ID 使用 `ins_<uuid32>`，并在公共 identity bridge 持久保存 OpenAlex、ROR、Wikidata
映射。论文指标严格过滤固定的 4,000,000 篇发布 MVP core，不包含 1,000,000 篇上下文论文。

已发布到 Doris：`ads_institution_profile` 68,010 行、
`ads_institution_discipline_profile` 7,232,894 行、
`ads_institution_yearly_metrics` 816,120 行；三张表业务 Key 均无重复。
3 个同时指向多个机构的 Wikidata ID 被判定为歧义映射并排除，不影响 OpenAlex/ROR 主映射。

## 1.3.0 — 2026-10-07

发布平台公共位置维度，并使机构画像使用稳定的平台位置 ID。

### 新增表

- `ads_location`：COUNTRY → PROVINCE → CITY → DISTRICT 公共位置层级。
- `ads_location_external_id`：ISO、ROR subdivision、GeoNames 及未来区划来源到平台位置 ID 的
  持久 bridge。

### 机构画像调整

- 增加 `location_id`、国家/省/市/区四级平台位置 ID。
- `region_name` 改为语义明确的 `province_name`，并增加 `district_name`。
- 增加位置解析状态、方法、置信度、位置质量与 release 字段。
- 为国家、省、市、区位置 ID 增加过滤索引。
- 区级字段当前为空；未来独立区划数据必须先进入公共位置维表，再关联机构画像。

### 数据发布

- 正式来源固定为 Iceberg `location_v1_1_20261007`。
- 发布 22,213 个位置和 22,213 个外部 ID 映射。
- `ads_institution_profile` 迁移前为 0 行，因此字段改名和新增没有业务数据转换。
- 迁移脚本：`sql/doris/ads_schema_1_3_0_location.sql`。
- 核验报告：`reports/talent_ads/ads_schema_1_3_0_location_verification_20261007.md`。

## 1.2.0 — 2026-10-07

根据机构产品口径精简机构画像并重构机构学科画像。

### 结构变化

- 从 `ads_institution_profile` 删除 `h_index`；机构主画像不发布机构 H 指数。
- `ads_institution_discipline_profile` 的粒度由
  `institution_id, discipline_type, discipline_id` 改为 `institution_id, topic_id`。
- 删除 `discipline_type`、`discipline_id`、`parent_discipline_id` 及通用名称字段。
- 每条 Topic 记录直接增加 Field、Subfield、Topic 的 ID、中文名和英文名。
- 增加 `project_count`，表示该机构在该 Topic 下关联的去重科研项目数；项目对应 DWD Grant。
- `discipline_rank` 改为 `topic_rank`。
- 删除 `ads_institution_collaboration`，当前版本不提供独立机构合作画像表。

### 数据影响与执行状态

- 变更前 `ads_institution_profile`、`ads_institution_discipline_profile`、
  `ads_institution_collaboration` 均为 0 行。
- 旧学科表已删除并按新 Topic 粒度重建，没有业务数据需要转换。
- 机构合作表已从 Doris 删除；该表迁移前为 0 行，无业务数据可恢复。
- 迁移脚本：`sql/doris/ads_schema_1_2_0_institution_refinement.sql`。
- 核验报告：`reports/talent_ads/ads_schema_1_2_0_institution_verification_20261007.md`。

## 1.1.0 — 2026-10-07

新增机构 ADS 服务结构，并统一人才 ADS 与机构 ADS 的机构类型编码。

### 新增表

- `ads_institution_type`：机构类型维表，初始化 8 个稳定英文类型代码。
- `ads_institution_profile`：机构主画像。
- `ads_institution_discipline_profile`：机构 Domain/Field/Subfield/Topic 画像。
- `ads_institution_yearly_metrics`：机构年度指标。
- `ads_institution_collaboration`：机构间有向合作画像。

### 审核修正

- 将原机构草案中的 `works_count`、`works_share`、`international_works_count`、
  `open_access_works_count`、`collaborative_works_count` 和 `avg_citations_per_work`
  统一改为 `paper_*` 命名；DWD `work` 只保留在上游边界。
- 所有新表增加 `data_version`、`update_time`，并使用 `data_version` 作为 Doris Sequence 列。
- 移除业务表的 `ON UPDATE CURRENT_TIMESTAMP`，避免数据库时间绕过发布批次版本。
- 未计算计数改为可空，维持 `NULL=未知/未计算，0=确认没有` 的统一约定。
- 单 BE 基线统一为 4 桶（低基数类型维表为 1 桶）、ZSTD、存储格式 V2、倒排索引 V3。
- ARRAY 别名索引改为成员过滤，不对数组错误配置全文 parser。

### 机构类型兼容性

- `ads_talent_experience.institution_type TINYINT` 改为
  `institution_type_id VARCHAR(32)`。
- `ads_talent_institution_cooperation.institution_type TINYINT` 改为
  `institution_type_id VARCHAR(32) NOT NULL DEFAULT 'other'`。
- 企业筛选由 `institution_type=2` 改为 `institution_type_id='company'`。
- 两张人才关系表迁移前均为 0 行，因此类型列调整没有转换或丢失业务数据。

### 执行状态

- 5 张机构表已在 `gkx_technology_analysis_dev` 创建。
- `ads_institution_type` 已写入 8 条初始化记录；其余 4 张表仅建结构，尚未写入业务数据。
- 建表文件：`sql/doris/institution_ads_doris_4_1.sql`。
- 人才机构类型迁移：`sql/doris/ads_schema_1_1_0_institution_alignment.sql`。
- 核验报告：`reports/talent_ads/ads_schema_1_1_0_institution_verification_20261007.md`。

## 1.0.0 — 2026-10-07

首个正式受治理的 Doris ADS Schema，从此前未版本化的 Talent ADS DDL 收敛而来。

### 主体命名

- 明确 `paper` 是论文，对应上游 DWD `work`；ADS 不再暴露 `work_id` 字段。
- 明确 `project` 是科研项目，对应上游 DWD `grant`。
- 明确 `institution` 统一承载科研机构、大学、科研院所、企业、医院和政府机构。
- 取消 `enterprise` 独立主体；企业通过 `institution_type=2` 表示。

### 不兼容字段与表名变更

| 旧名称 | 新名称/处理 |
|---|---|
| `ads_talent_research_achievement.work_id` | `paper_id` |
| `ads_talent_patent_cited_paper.work_id` | `paper_id`；UNIQUE KEY 同步变为 `talent_id, patent_id, paper_id` |
| `ads_talent_enterprise_cooperation` | `ads_talent_institution_cooperation` |
| `enterprise_id` | `institution_id` |
| — | 新增 `institution_type TINYINT NOT NULL DEFAULT 9` |
| `ads_talent_profile.current_enterprise_ids` | 删除；统一使用 `current_institution_ids` 与机构类型 |
| `enterprise_cooperation_project_count` | `institution_cooperation_project_count` |
| `co_enterprise_index` | `institution_cooperation_index` |
| `co_enterprise_index_version` | `institution_cooperation_index_version` |
| `co_enterprise_index_annotation` | `institution_cooperation_index_annotation` |
| `ads_talent_yearly_metrics.enterprise_cooperation_count` | `institution_cooperation_count` |

### ID 兼容性

- 字段改名不改变 ID 值，不重建 identity bridge。
- 历史论文平台 ID 的 `wrk_` 前缀继续有效；它是持久 ID 值，不代表 ADS 字段仍使用 `work` 命名。
- OpenAlex、Google Patents 及未来来源 ID 仍通过独立 bridge 映射到平台 ID。

### 在线迁移与数据影响

- 迁移前 `ads_talent_enterprise_cooperation` 为 0 行。
- `current_enterprise_ids` 非空数组为 0 行；其余被改名的 enterprise 指标非 NULL 行为 0。
- 两个 `work_id` 列采用 Doris `RENAME COLUMN`，已发布数据原位保留。
- 删除的 `current_enterprise_ids` 在 Doris 中没有业务值可恢复；旧字段定义可从 Git 历史和本版本说明追溯。
- 迁移脚本：
  [`sql/doris/talent_ads_schema_1_0_0_migration.sql`](sql/doris/talent_ads_schema_1_0_0_migration.sql)。
