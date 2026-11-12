# ADS_SCHEMA.md

## 1. 主体名称与边界

**Schema version：9.27.2。** 本文件是下游 Doris ADS 逻辑结构与业务命名的唯一真实来源；
可执行物理 DDL 包括 `sql/doris/` 下的 Talent、Institution 基线文件及版本化
`ads_schema_*` 迁移文件；新增公共学科维表的 DDL 为
[`sql/doris/ads_schema_1_7_0_publication_profiles.sql`](sql/doris/ads_schema_1_7_0_publication_profiles.sql)；
人才公开资料、简介、证据、荣誉/经历候选与媒体报道迁移为
[`sql/doris/ads_schema_6_32_0_talent_public_enrichment.sql`](sql/doris/ads_schema_6_32_0_talent_public_enrichment.sql)；
经核验荣誉详情迁移为
[`sql/doris/ads_schema_6_33_0_talent_honor_detail.sql`](sql/doris/ads_schema_6_33_0_talent_honor_detail.sql)；
完美数据原表补充发布迁移为
[`sql/doris/ads_schema_9_10_0_perfect_data_inplace.sql`](sql/doris/ads_schema_9_10_0_perfect_data_inplace.sql)，
发布入口为[`scripts/publish_showcase_enrichment_v1.sh`](scripts/publish_showcase_enrichment_v1.sh)；
完美机构官方报告迁移为
[`sql/doris/ads_schema_9_15_0_institution_report.sql`](sql/doris/ads_schema_9_15_0_institution_report.sql)，
发布入口为[`scripts/publish_institution_reports_v1.sh`](scripts/publish_institution_reports_v1.sh)；
人才年度流向边当前单一原因展示字段迁移为
[`sql/doris/ads_schema_9_16_0_talent_mobility_reason.sql`](sql/doris/ads_schema_9_16_0_talent_mobility_reason.sql)，
物化与发布入口继续复用[`scripts/publish_talent_mobility_mvp_v1.sh`](scripts/publish_talent_mobility_mvp_v1.sh)；
人才年度学术影响力代理分口径迁移为
[`sql/doris/ads_schema_9_17_0_talent_yearly_academic.sql`](sql/doris/ads_schema_9_17_0_talent_yearly_academic.sql)，
发布入口为[`scripts/publish_talent_yearly_academic_v1.sh`](scripts/publish_talent_yearly_academic_v1.sh)；
重点技术交叉关联矩阵及完整下钻证据迁移为
[`sql/doris/ads_schema_9_11_0_technology_cross_showcase.sql`](sql/doris/ads_schema_9_11_0_technology_cross_showcase.sql)；
完美技术交叉关联论文与循证协同原理迁移为
[`sql/doris/ads_schema_9_18_0_perfect_technology_edge.sql`](sql/doris/ads_schema_9_18_0_perfect_technology_edge.sql)；
完美技术动态、模型内容与统一证据迁移为
[`sql/doris/ads_schema_9_19_0_technology_dynamic.sql`](sql/doris/ads_schema_9_19_0_technology_dynamic.sql)，
统一论文/专利ID、百分比投影与逐事件内容迁移为
[`sql/doris/ads_schema_9_20_0_technology_dynamic_event_content.sql`](sql/doris/ads_schema_9_20_0_technology_dynamic_event_content.sql)，
实体事件类型、时间点及关联ID迁移为
[`sql/doris/ads_schema_9_21_0_technology_dynamic_entity_events.sql`](sql/doris/ads_schema_9_21_0_technology_dynamic_entity_events.sql)，
技术动态证据表仅保留事件行的清理迁移为
[`sql/doris/ads_schema_9_22_0_technology_dynamic_event_only.sql`](sql/doris/ads_schema_9_22_0_technology_dynamic_event_only.sql)，
发布入口为[`scripts/publish_technology_dynamic_perfect_v1.sh`](scripts/publish_technology_dynamic_perfect_v1.sh)；
人才社会影响与人才培养代理分迁移为
[`sql/doris/ads_schema_9_23_0_talent_social_cultivation.sql`](sql/doris/ads_schema_9_23_0_talent_social_cultivation.sql)，
发布入口为
[`scripts/publish_talent_social_cultivation_v1.sh`](scripts/publish_talent_social_cultivation_v1.sh)；
15名重点人才影响描述及模型血缘迁移为
[`sql/doris/ads_schema_9_24_0_talent_impact_description.sql`](sql/doris/ads_schema_9_24_0_talent_impact_description.sql)，
发布入口为
[`scripts/publish_talent_impact_description_v1.sh`](scripts/publish_talent_impact_description_v1.sh)；
深圳GKX产业集群年度发展方案原表补充迁移为
[`sql/doris/ads_schema_9_12_0_sz_gkx_industry_annual_plan.sql`](sql/doris/ads_schema_9_12_0_sz_gkx_industry_annual_plan.sql)，
发布入口为
[`scripts/publish_sz_gkx_industry_annual_plan_v1.sh`](scripts/publish_sz_gkx_industry_annual_plan_v1.sh)；
技术趋势折线图确定性关键节点事件迁移为
[`sql/doris/ads_schema_9_13_0_technology_milestone_event.sql`](sql/doris/ads_schema_9_13_0_technology_milestone_event.sql)，
物化与发布入口继续复用[`app/technology_ads/service.py`](app/technology_ads/service.py)；
论文Primary Source便利投影迁移为
[`sql/doris/ads_schema_9_14_0_paper_primary_source_projection.sql`](sql/doris/ads_schema_9_14_0_paper_primary_source_projection.sql)，
物化与发布入口继续复用[`scripts/publish_publication_ads.sh`](scripts/publish_publication_ads.sh)；
论文标题ICU多语言全文检索索引迁移为
[`sql/doris/ads_schema_9_24_1_paper_title_multilingual_search_index.sql`](sql/doris/ads_schema_9_24_1_paper_title_multilingual_search_index.sql)；
人才、技术、机构、项目和技术热点信号多字段全文检索索引迁移为
[`sql/doris/ads_schema_9_26_1_multifield_search_indexes.sql`](sql/doris/ads_schema_9_26_1_multifield_search_indexes.sql)；
技术阶段典型任务、代表性案例示意及模型血缘迁移为
[`sql/doris/ads_schema_9_27_0_technology_stage_content.sql`](sql/doris/ads_schema_9_27_0_technology_stage_content.sql)，
发布入口为
[`scripts/publish_technology_stage_content_v1.sh`](scripts/publish_technology_stage_content_v1.sh)；
荣誉详情双语名称与两院院士匹配发布迁移为
[`sql/doris/ads_schema_9_9_0_talent_honor_bilingual_academician.sql`](sql/doris/ads_schema_9_9_0_talent_honor_bilingual_academician.sql)；
15人科研诚信演示分迁移为
[`sql/doris/ads_schema_6_34_0_talent_integrity_score_demo.sql`](sql/doris/ads_schema_6_34_0_talent_integrity_score_demo.sql)；
15人媒体报道情感与风险初评迁移为
[`sql/doris/ads_schema_6_35_0_talent_media_sentiment.sql`](sql/doris/ads_schema_6_35_0_talent_media_sentiment.sql)；
15人媒体热点话题与价值观来源证据迁移为
[`sql/doris/ads_schema_6_36_0_talent_topic_value.sql`](sql/doris/ads_schema_6_36_0_talent_topic_value.sql)；
15人政治展示分及子项证据迁移为
[`sql/doris/ads_schema_6_37_0_talent_political_score_demo.sql`](sql/doris/ads_schema_6_37_0_talent_political_score_demo.sql)；
ADS候选队列表移除迁移为
[`sql/doris/ads_schema_7_0_0_remove_candidate_tables.sql`](sql/doris/ads_schema_7_0_0_remove_candidate_tables.sql)；
机构新闻冗余人才/经历数组移除迁移为
[`sql/doris/ads_schema_8_0_0_institution_news_cleanup.sql`](sql/doris/ads_schema_8_0_0_institution_news_cleanup.sql)；
颠覆性技术候选市场热度模型估计迁移为
[`sql/doris/ads_schema_8_1_0_technology_market_heat.sql`](sql/doris/ads_schema_8_1_0_technology_market_heat.sql)；
前沿技术证据与转化风险迁移为
[`sql/doris/ads_schema_8_2_0_technology_hotspot_risk.sql`](sql/doris/ads_schema_8_2_0_technology_hotspot_risk.sql)；
技术年度投资额人民币规则模拟迁移为
[`sql/doris/ads_schema_8_3_0_technology_investment_estimate.sql`](sql/doris/ads_schema_8_3_0_technology_investment_estimate.sql)；
媒体聚焦文章关系、日指标、来源—目标边和总览迁移为
[`sql/doris/ads_schema_8_5_0_media_focus.sql`](sql/doris/ads_schema_8_5_0_media_focus.sql)；
媒体热点、情感偏向和媒体—技术耦合估算迁移为
[`sql/doris/ads_schema_8_6_0_media_focus_insights.sql`](sql/doris/ads_schema_8_6_0_media_focus_insights.sql)；
热点热度和月度增长迁移为
[`sql/doris/ads_schema_8_7_0_media_hotspot_growth.sql`](sql/doris/ads_schema_8_7_0_media_hotspot_growth.sql)；
热点热度历史回填和首月100%增长口径修正为
[`sql/doris/ads_schema_8_8_0_media_growth_baseline.sql`](sql/doris/ads_schema_8_8_0_media_growth_baseline.sql)；
媒体—技术年度趋势、原始政策词证据和滞后相关迁移为
[`sql/doris/ads_schema_8_9_0_media_technology_yearly_trend.sql`](sql/doris/ads_schema_8_9_0_media_technology_yearly_trend.sql)；
机构代表专利虚拟技术转化额及机构合计迁移为
[`sql/doris/ads_schema_8_10_0_institution_patent_transfer_amount.sql`](sql/doris/ads_schema_8_10_0_institution_patent_transfer_amount.sql)，
发布入口为
[`scripts/publish_institution_patent_transfer_amount_v1.sh`](scripts/publish_institution_patent_transfer_amount_v1.sh)；
媒体来源画像规范化及来源—目标边冗余字段移除迁移为
[`sql/doris/ads_schema_9_0_0_media_source_profile.sql`](sql/doris/ads_schema_9_0_0_media_source_profile.sql)；
媒体来源中文展示名迁移为
[`sql/doris/ads_schema_9_1_0_media_source_name_zh.sql`](sql/doris/ads_schema_9_1_0_media_source_name_zh.sql)，
固定翻译映射为
[`config/media_source_name_zh_v1.json`](config/media_source_name_zh_v1.json)；
媒体最新新闻突发候选、触发原因和简报草稿迁移为
[`sql/doris/ads_schema_9_2_0_media_breaking_event_candidate.sql`](sql/doris/ads_schema_9_2_0_media_breaking_event_candidate.sql)；
媒体—技术完整相关矩阵、Granger预测检验、滚动耦合与机制草稿迁移为
[`sql/doris/ads_schema_9_5_0_media_technology_coupling_analysis.sql`](sql/doris/ads_schema_9_5_0_media_technology_coupling_analysis.sql)；
媒体网络影响力代理、文章关键词频次、固定官网刊登路径和目标地域桥表迁移为
[`sql/doris/ads_schema_9_6_0_media_network_interaction.sql`](sql/doris/ads_schema_9_6_0_media_network_interaction.sql)；
媒体智能推荐卡片、逐篇相似度证据和事实三元组迁移为
[`sql/doris/ads_schema_9_7_0_media_smart_recommendation.sql`](sql/doris/ads_schema_9_7_0_media_smart_recommendation.sql)，
发布入口为
[`scripts/publish_media_smart_recommendations_v1.sh`](scripts/publish_media_smart_recommendations_v1.sh)；
人才—企业合作画像、合作项目/论文/专利下钻和非空版本化合作分迁移为
[`sql/doris/ads_schema_9_8_0_talent_institution_cooperation.sql`](sql/doris/ads_schema_9_8_0_talent_institution_cooperation.sql)，
发布入口为
[`scripts/publish_talent_institution_cooperation_v1.sh`](scripts/publish_talent_institution_cooperation_v1.sh)；
MVP论文摘要扩展迁移为
[`sql/doris/ads_schema_6_7_0_paper_abstract.sql`](sql/doris/ads_schema_6_7_0_paper_abstract.sql)；
专利分析分类、申请人及机构下钻扩展迁移为
[`sql/doris/ads_schema_6_8_0_patent_analysis_enhancement.sql`](sql/doris/ads_schema_6_8_0_patent_analysis_enhancement.sql)；
专利分析全局申请人节点迁移为
[`sql/doris/ads_schema_6_9_0_patent_analysis_assignee.sql`](sql/doris/ads_schema_6_9_0_patent_analysis_assignee.sql)；
最大覆盖专利—机构节点关系迁移为
[`sql/doris/ads_schema_6_10_0_patent_analysis_patent_institution.sql`](sql/doris/ads_schema_6_10_0_patent_analysis_patent_institution.sql)；
国家/地区×Topic单元格增长与年度趋势迁移为
[`sql/doris/ads_schema_6_11_0_patent_analysis_cross_trend.sql`](sql/doris/ads_schema_6_11_0_patent_analysis_cross_trend.sql)；
机构合作Subfield年度关系迁移为
[`sql/doris/ads_schema_6_12_0_institution_collaboration_subfield.sql`](sql/doris/ads_schema_6_12_0_institution_collaboration_subfield.sql)；
技术簇主Field/Subfield分类迁移为
[`sql/doris/ads_schema_6_13_0_technology_community_discipline.sql`](sql/doris/ads_schema_6_13_0_technology_community_discipline.sql)；
颠覆性技术评估中文名称冗余迁移为
[`sql/doris/ads_schema_6_14_0_technology_disruption_name_zh.sql`](sql/doris/ads_schema_6_14_0_technology_disruption_name_zh.sql)；
颠覆性技术预警详情与影响评估迁移为
[`sql/doris/ads_schema_6_15_0_technology_disruption_detail.sql`](sql/doris/ads_schema_6_15_0_technology_disruption_detail.sql)；
颠覆性技术评估领先Topic双语快照迁移为
[`sql/doris/ads_schema_6_16_0_technology_disruption_leading_topic.sql`](sql/doris/ads_schema_6_16_0_technology_disruption_leading_topic.sql)；
深圳关联项目缺失金额的确定性模拟与真假标识迁移为
[`sql/doris/ads_schema_6_17_0_project_shenzhen_simulated_amount.sql`](sql/doris/ads_schema_6_17_0_project_shenzhen_simulated_amount.sql)；
技术点年度热度、论文和新增引用曲线迁移为
[`sql/doris/ads_schema_6_18_0_technology_hotspot_yearly.sql`](sql/doris/ads_schema_6_18_0_technology_hotspot_yearly.sql)；
深圳机构Field与Primary Topic项目关联资金物化迁移为
[`sql/doris/ads_schema_6_19_0_shenzhen_institution_funding.sql`](sql/doris/ads_schema_6_19_0_shenzhen_institution_funding.sql)，
发布SQL为
[`sql/doris/publish_shenzhen_institution_funding_v1.sql`](sql/doris/publish_shenzhen_institution_funding_v1.sql)；
深圳机构关联项目全额经费主画像字段迁移为
[`sql/doris/ads_schema_6_20_0_institution_project_funding.sql`](sql/doris/ads_schema_6_20_0_institution_project_funding.sql)，
发布SQL为
[`sql/doris/publish_institution_project_funding_v1.sql`](sql/doris/publish_institution_project_funding_v1.sql)；
机构技术力中文名称快照迁移为
[`sql/doris/ads_schema_6_21_0_institution_technology_power_name_zh.sql`](sql/doris/ads_schema_6_21_0_institution_technology_power_name_zh.sql)，
回填SQL为
[`sql/doris/publish_institution_technology_power_name_zh_v1.sql`](sql/doris/publish_institution_technology_power_name_zh_v1.sql)；
科研资源短板、十城基准与Subfield年度趋势迁移为
[`sql/doris/ads_schema_6_25_0_resource_shortage.sql`](sql/doris/ads_schema_6_25_0_resource_shortage.sql)，
发布入口为[`scripts/publish_resource_shortage_v1.sh`](scripts/publish_resource_shortage_v1.sh)；
科研资源统一项目金额与来源字段迁移为
[`sql/doris/ads_schema_6_27_0_resource_shortage_unified_funding.sql`](sql/doris/ads_schema_6_27_0_resource_shortage_unified_funding.sql)；
城市与机构年度Field科研资源独立重算表迁移为
[`sql/doris/ads_schema_9_25_0_resource_field_yearly.sql`](sql/doris/ads_schema_9_25_0_resource_field_yearly.sql)；
城市与机构年度Domain科研资源独立重算表迁移为
[`sql/doris/ads_schema_9_26_0_resource_domain_yearly.sql`](sql/doris/ads_schema_9_26_0_resource_domain_yearly.sql)；
科研资源优化建议及逐指标证据迁移为
[`sql/doris/ads_schema_6_28_0_resource_optimization_recommendation.sql`](sql/doris/ads_schema_6_28_0_resource_optimization_recommendation.sql)，
发布SQL为
[`sql/doris/publish_resource_optimization_recommendation_v1.sql`](sql/doris/publish_resource_optimization_recommendation_v1.sql)；
智能推荐与动态更新迁移为
[`sql/doris/ads_schema_6_26_0_smart_recommendation.sql`](sql/doris/ads_schema_6_26_0_smart_recommendation.sql)，
首版发布SQL为
[`sql/doris/publish_smart_recommendation_mvp_v1.sql`](sql/doris/publish_smart_recommendation_mvp_v1.sql)；
ORCID 经历及机构扩展迁移为
[`sql/doris/ads_schema_1_8_0_orcid_experience.sql`](sql/doris/ads_schema_1_8_0_orcid_experience.sql)；
人才—项目关系迁移为
[`sql/doris/ads_schema_1_9_0_talent_project.sql`](sql/doris/ads_schema_1_9_0_talent_project.sql)；
机构年度合作网络迁移为
[`sql/doris/ads_schema_1_10_0_institution_collaboration.sql`](sql/doris/ads_schema_1_10_0_institution_collaboration.sql)；
机构产业参与画像迁移为
[`sql/doris/ads_schema_1_11_0_institution_industry.sql`](sql/doris/ads_schema_1_11_0_institution_industry.sql)。
机构产业关系增加发明人任职证据的迁移为
[`sql/doris/ads_schema_5_0_0_institution_industry_affiliation.sql`](sql/doris/ads_schema_5_0_0_institution_industry_affiliation.sql)。
机构合作增加直接联合项目指标的迁移为
[`sql/doris/ads_schema_5_6_0_institution_collaboration_project.sql`](sql/doris/ads_schema_5_6_0_institution_collaboration_project.sql)。
机构—Topic 综合科研实力评分迁移为
[`sql/doris/ads_schema_5_7_0_institution_discipline_strength.sql`](sql/doris/ads_schema_5_7_0_institution_discipline_strength.sql)，
发布 SQL 为
[`sql/doris/publish_institution_discipline_strength_v1.sql`](sql/doris/publish_institution_discipline_strength_v1.sql)。
机构主画像合作总量迁移为
[`sql/doris/ads_schema_5_8_0_institution_profile_collaboration_totals.sql`](sql/doris/ads_schema_5_8_0_institution_profile_collaboration_totals.sql)。
机构产业项目数口径与字段注释迁移为
[`sql/doris/ads_schema_5_3_1_institution_industry_project_count.sql`](sql/doris/ads_schema_5_3_1_institution_industry_project_count.sql)。
机构代表论文和代表专利 Top 20 迁移为
[`sql/doris/ads_schema_5_1_0_institution_achievement.sql`](sql/doris/ads_schema_5_1_0_institution_achievement.sql)。
基础研究问题 ADS 迁移由固定 Iceberg Stage Schema 生成至
`sql/doris/ads_schema_5_16_0_research_problem.generated.sql`，发布说明见
[`docs/research_problem_ads_v1.md`](docs/research_problem_ads_v1.md)。
机构首次观察进入 Topic 迁移为
[`sql/doris/ads_schema_1_12_0_institution_topic_entry.sql`](sql/doris/ads_schema_1_12_0_institution_topic_entry.sql)。
机构科研技术力 MVP 评分迁移为
[`sql/doris/ads_schema_1_13_0_institution_technology_power.sql`](sql/doris/ads_schema_1_13_0_institution_technology_power.sql)。
人才分类 taxonomy、统一称谓及人才主画像瘦身迁移为
[`sql/doris/ads_schema_2_0_0_talent_taxonomy.sql`](sql/doris/ads_schema_2_0_0_talent_taxonomy.sql)；
旧列只允许在完成回填与对账后通过
[`sql/doris/ads_schema_2_0_0_talent_taxonomy_finalize.sql`](sql/doris/ads_schema_2_0_0_talent_taxonomy_finalize.sql)
删除。
人才学术力分项指标迁移为
[`sql/doris/ads_schema_2_1_0_talent_academic_capability.sql`](sql/doris/ads_schema_2_1_0_talent_academic_capability.sql)。
人才拼音逆推中文候选名迁移为
[`sql/doris/ads_schema_5_17_0_talent_name_candidate.sql`](sql/doris/ads_schema_5_17_0_talent_name_candidate.sql)。
候选中文姓名全文索引迁移为
[`sql/doris/ads_schema_6_0_2_talent_name_candidate_search_index.sql`](sql/doris/ads_schema_6_0_2_talent_name_candidate_search_index.sql)。
人才产业技术活动 MVP 迁移为
[`sql/doris/ads_schema_2_2_0_talent_industry_activity.sql`](sql/doris/ads_schema_2_2_0_talent_industry_activity.sql)。
技术商业价值与人才产业力模拟迁移为
[`sql/doris/ads_schema_2_3_0_talent_industry_simulation.sql`](sql/doris/ads_schema_2_3_0_talent_industry_simulation.sql)。
人才主画像废弃占位字段清理迁移为
[`sql/doris/ads_schema_3_0_0_talent_profile_cleanup.sql`](sql/doris/ads_schema_3_0_0_talent_profile_cleanup.sql)，
执行和核验见
[`docs/ads_schema_3_0_0_talent_profile_cleanup.md`](docs/ads_schema_3_0_0_talent_profile_cleanup.md)。
人才级产业力汇总结果与主画像投影迁移为
[`sql/doris/ads_schema_9_3_0_talent_industrial_capability.sql`](sql/doris/ads_schema_9_3_0_talent_industrial_capability.sql)，
发布和核验见
[`docs/talent_industrial_capability_v1.md`](docs/talent_industrial_capability_v1.md)。
人才—产业节点评分增加论文基础、小样本收缩和学术门槛的迁移为
[`sql/doris/ads_schema_9_4_0_talent_industry_activity_scoring.sql`](sql/doris/ads_schema_9_4_0_talent_industry_activity_scoring.sql)，
发布与人才级汇总必须按v2链路依次重算。
人才 taxonomy 与统一属性关系重构迁移为
[`sql/doris/ads_schema_3_0_0_talent_taxonomy_unification.sql`](sql/doris/ads_schema_3_0_0_talent_taxonomy_unification.sql)，
执行和人才分类方案见
[`docs/ads_schema_3_0_0_talent_taxonomy.md`](docs/ads_schema_3_0_0_talent_taxonomy.md)。
人才专利申请类型字段重命名与回填迁移为
[`sql/doris/ads_schema_4_0_0_talent_patent_application_kind.sql`](sql/doris/ads_schema_4_0_0_talent_patent_application_kind.sql)，
执行和核验见
[`docs/ads_schema_4_0_0_talent_patent_application_kind.md`](docs/ads_schema_4_0_0_talent_patent_application_kind.md)。
版本化人才潜力结果迁移为
[`sql/doris/ads_schema_4_2_0_talent_potential.sql`](sql/doris/ads_schema_4_2_0_talent_potential.sql)，
发布、主画像投影和核验见
[`docs/talent_potential_mvp_v1.md`](docs/talent_potential_mvp_v1.md)。
人才单一 Primary Topic 相似度迁移为
[`sql/doris/ads_schema_4_3_0_talent_similarity.sql`](sql/doris/ads_schema_4_3_0_talent_similarity.sql)，
计算、Top 3 发布和前端展示视图见
[`docs/talent_similarity_topic_mvp_v1.md`](docs/talent_similarity_topic_mvp_v1.md)。
新兴 Topic 年度趋势、当前判定和关键人才迁移为
[`sql/doris/ads_schema_4_4_0_emerging_topic.sql`](sql/doris/ads_schema_4_4_0_emerging_topic.sql)，
固定窗口、门槛、评分、发布与查询说明见
[`docs/emerging_topic_mvp_v1.md`](docs/emerging_topic_mvp_v1.md)。
人才年度位置、年度学科和流动事件/流向迁移为
[`sql/doris/ads_schema_4_5_0_talent_mobility.sql`](sql/doris/ads_schema_4_5_0_talent_mobility.sql)，
固定输入、严格事件口径、发布与查询说明见
[`docs/talent_mobility_mvp_v1.md`](docs/talent_mobility_mvp_v1.md)。
候选技术图谱、热点、潜力、阶段、区域与转化堵点迁移为
[`sql/doris/ads_schema_4_6_0_technology.sql`](sql/doris/ads_schema_4_6_0_technology.sql)，
既有表字段与表注释回填为
[`sql/doris/ads_schema_4_6_0_technology_comments.sql`](sql/doris/ads_schema_4_6_0_technology_comments.sql)。
技术点中英文名称全文索引迁移为
[`sql/doris/ads_schema_6_0_1_technology_name_search_indexes.sql`](sql/doris/ads_schema_6_0_1_technology_name_search_indexes.sql)。
技术图谱年度演进、Louvain簇群和代表路径迁移为
[`sql/doris/ads_schema_4_7_0_technology_graph.sql`](sql/doris/ads_schema_4_7_0_technology_graph.sql)，
既有表字段与表注释回填为
[`sql/doris/ads_schema_4_7_0_technology_graph_comments.sql`](sql/doris/ads_schema_4_7_0_technology_graph_comments.sql)。
论文证据颠覆性技术候选基线迁移为
[`sql/doris/ads_schema_5_18_0_technology_disruption.sql`](sql/doris/ads_schema_5_18_0_technology_disruption.sql)。
人才主画像当前机构四级位置 ID 冗余迁移为
[`sql/doris/ads_schema_4_8_0_talent_current_institution_location.sql`](sql/doris/ads_schema_4_8_0_talent_current_institution_location.sql)。
人才本人论文被本人关联专利引用指标迁移为
[`sql/doris/ads_schema_4_9_0_talent_research_to_patent.sql`](sql/doris/ads_schema_4_9_0_talent_research_to_patent.sql)。
人才已观察引用中的本人自引、他引与他引率迁移为
[`sql/doris/ads_schema_6_31_0_talent_observed_citation.sql`](sql/doris/ads_schema_6_31_0_talent_observed_citation.sql)，
固定口径、执行与查询说明见
[`docs/talent_observed_citation_mvp_v1.md`](docs/talent_observed_citation_mvp_v1.md)。
机构学科画像项目数回填与核验入口为
[`sql/doris/ads_schema_4_9_1_institution_discipline_project_count.sql`](sql/doris/ads_schema_4_9_1_institution_discipline_project_count.sql)。
Topic论文全球国家当前快照迁移为
[`sql/doris/ads_schema_6_1_0_topic_country_snapshot.sql`](sql/doris/ads_schema_6_1_0_topic_country_snapshot.sql)，
固定窗口、分数计数、发布与地图查询说明见
[`docs/topic_country_snapshot_v1.md`](docs/topic_country_snapshot_v1.md)。
专利分析总览、覆盖率及交叉指标迁移为
[`sql/doris/ads_schema_6_2_0_patent_analysis.sql`](sql/doris/ads_schema_6_2_0_patent_analysis.sql)，
专利—Topic明细及核心专利代理排名迁移为
[`sql/doris/ads_schema_6_3_0_patent_topic_patent.sql`](sql/doris/ads_schema_6_3_0_patent_topic_patent.sql)，
固定输入、Topic语义、发布与限制说明见
[`docs/patent_analysis_v1.md`](docs/patent_analysis_v1.md)。
项目中文名称全文索引迁移为
[`sql/doris/ads_schema_6_3_2_project_name_zh_search_index.sql`](sql/doris/ads_schema_6_3_2_project_name_zh_search_index.sql)。
项目默认名称与原始描述的多语言全文索引迁移为
[`sql/doris/ads_schema_6_3_3_project_multilingual_search_indexes.sql`](sql/doris/ads_schema_6_3_3_project_multilingual_search_indexes.sql)。
深圳GKX产业集群独立体系迁移为
[`sql/doris/ads_schema_6_5_0_sz_gkx_industry.sql`](sql/doris/ads_schema_6_5_0_sz_gkx_industry.sql)。
集群—Topic产业链上中下游标签迁移为
[`sql/doris/ads_schema_6_6_0_sz_gkx_industry_chain_stage.sql`](sql/doris/ads_schema_6_6_0_sz_gkx_industry_chain_stage.sql)。
项目金额人民币归一及范围过滤索引迁移为
[`sql/doris/ads_schema_6_4_0_project_amount_cny.sql`](sql/doris/ads_schema_6_4_0_project_amount_cny.sql)。
逻辑文档与可执行 DDL 必须同版本变更，版本历史记录在
[`ADS_SCHEMA_RELEASE_NOTES.md`](ADS_SCHEMA_RELEASE_NOTES.md)。

平台主体统一使用以下名称：

| 主体 | 中文名称 | 上游关联 | ADS 命名规则 |
|---|---|---|---|
| `talent` | 人才 | DWD `author` + 平台 identity bridge | 对外主体、表名和字段名使用 `talent` / `talent_id`；来源 `author_id` 仅作映射，不作为 ADS 平台主键 |
| `technology` | 技术 | 固定 `technology_catalog_release` | 使用目录内稳定 `tech_id`；名称仅为固定发布快照，不以名称充当身份 |
| `paper` | 论文 | DWD `work` | 对外表名、字段名使用 `paper` / `paper_id`；不得暴露 `work_id` |
| `patent` | 专利 | Patent DWD/DWS | 使用 `patent` / `patent_id` |
| `institution` | 科研机构 | DWD `institution` | 大学、科研院所、企业、医院、政府机构等统一使用 `institution` |
| `project` | 科研项目 | DWD `grant` | 对外表名、字段名使用 `project` / `project_id` |

`enterprise` 不是独立主体。企业是 `institution` 的一种类型，当前稳定类型代码为
`institution_type_id='company'`。因此 ADS 不建立
`enterprise_id`、`current_enterprise_ids` 或 `ads_*_enterprise_*` 表。需要企业子集时，
通过 `institution_type_id='company'` 筛选机构数据。机构类型代码由
`ads_institution_type` 统一维护，不使用来源行号或不可扩展的数字枚举。

上游 DWD 的 `work_id` 和 `grant` 是基础层协议名，可以继续出现在读取、连接及映射 SQL 内；
进入 ADS 输出边界后必须分别命名为 `paper_id` 和 `project`。术语变更不重算实体身份：已经
分配的论文平台 ID（包括历史 `wrk_<uuid32>` 值）继续永久使用，只把承载它的 ADS 字段命名为
`paper_id`。

## 2. 公共约束

- 数据库：`gkx_technology_analysis_dev`；存储引擎：Apache Doris OLAP。
- 当前 203 张表均为 `UNIQUE KEY` + Merge-on-Write 当前状态表；事实与画像表按其主体 ID
  HASH 分桶，低基数机构类型维表使用 1 个桶。
- 所有平台主体 ID 使用 `VARCHAR(64)`，与任何单一来源 ID 解耦；外部 ID 通过持久 identity
  bridge 映射，不由来源 ID、姓名、批次顺序或行号推导。
- `data_version BIGINT NOT NULL` 是同一业务 Key 的单调版本；`update_time DATETIME(3) NOT NULL`
  是 UTC 生成时间。所有表都包含这两个公共列。
- `NULL` 表示未知或未计算；`0` 和空数组表示已经确认没有。ARRAY 去重且不含 NULL 元素。
- `VARIANT` 只存有界展示快照；完整事实与历史保留在 Iceberg DWD/DWS。
- ADS 不声明伪外键。ETL 必须校验非空 Key、唯一性、ID bridge 完整性、计数口径和关系完整性。

## 3. 表清单

| 表 | 粒度 | UNIQUE KEY | 状态 |
|---|---|---|---|
| `ads_talent_profile` | 一名人才一行 | `talent_id` | 已发布 |
| `ads_talent_integrity_score_demo` | 一名人才在一个固定演示评分版本一行 | `talent_id, score_version` | 6.34.0新增；非事实认定 |
| `ads_talent_media_sentiment_assessment` | 一名人才在一个固定媒体评估版本一行 | `talent_id, assessment_version` | 6.35.0新增；有限样本初评 |
| `ads_talent_topic_value_summary` | 一名人才的一个标准话题或价值主题一行 | `release_id, talent_id, expression_type, expression_code` | 6.36.0新增；保存提及次数 |
| `ads_talent_topic_value_evidence` | 一篇报道对一个话题或价值主题的一条来源证据一行 | `release_id, expression_evidence_id` | 6.36.0新增；支持点击下钻 |
| `ads_talent_political_assessment_demo` | 一名人才在一个固定政治展示分版本一行 | `talent_id, assessment_version` | 6.37.0新增；非政治推断 |
| `ads_talent_political_subscore_demo` | 一名人才的科学精神或一个价值主题子项一行 | `talent_id, assessment_version, subscore_code` | 6.37.0新增；支持子项展示 |
| `ads_talent_political_subscore_evidence` | 一个政治展示分子项的一条指标或来源证据一行 | `talent_id, assessment_version, subscore_evidence_id` | 6.37.0新增；支持点击下钻 |
| `ads_talent_public_enrichment` | 一名人才在一个公开资料采集发布中的可展示快照一行 | `talent_id, release_id` | 6.32.0新增并发布15人MVP |
| `ads_talent_profile_evidence` | 一个发布中的一条人才字段断言一行 | `release_id, assertion_id` | 6.32.0新增并发布 |
| `ads_talent_biography_evidence` | 一个发布中的一段简介底稿一行 | `release_id, biography_source_id` | 6.32.0新增并发布 |
| `ads_talent_honor_detail` | 一个发布中的一项经核验奖项或学术身份一行 | `release_id, honor_detail_id` | 6.33.0新增；9.9.0增加中英文名称并接入两院院士匹配发布 |
| `ads_talent_media_report` | 一个发布中的一条人才媒体报道候选一行 | `release_id, media_mention_id` | 6.32.0新增并发布；情感/风险未计算 |
| `ads_talent_potential_result` | 一名人才一个潜力模型版本一行 | `talent_id, model_version` | 4.2.0新增并发布MVP v1 |
| `ads_talent_taxonomy` | 一个不可变人才 taxonomy 发布一行 | `taxonomy_id, release_id` | 3.0.0统一语义 |
| `ads_talent_taxonomy_node` | 一个 taxonomy release 的一个节点一行 | `taxonomy_id, release_id, node_id` | 3.0.0新增 |
| `ads_talent_taxonomy_closure` | 一个 taxonomy release 的一条祖先—后代路径一行 | `taxonomy_id, release_id, ancestor_node_id, descendant_node_id` | 3.0.0新增 |
| `ads_talent_taxonomy_relation` | 一名人才与一个 taxonomy 节点的一条关系一行 | `talent_taxonomy_relation_id` | 3.0.0新增 |
| `ads_talent_taxonomy_metrics` | 一个 taxonomy release 的一个节点聚合一行 | `taxonomy_id, release_id, node_id` | 3.0.0新增 |
| `ads_talent_experience` | 一名人才一段经历一行 | `talent_id, experience_id` | 1.8.0 已发布 ORCID 教育/工作经历 |
| `ads_institution_news` | 一家正式履历机构一条官网新闻一行 | `release_id, institution_news_id` | 8.0.0 删除冗余人才/经历数组 |
| `ads_institution_report` | 一份外部机构报告一行 | `report_id` | 9.15.0新增；首版覆盖26家完美机构 |
| `ads_talent_research_achievement` | 一名人才一项代表成果一行 | `talent_id, achievement_id` | 已发布 |
| `ads_talent_topic_profile` | 一名人才一个 Topic 一行 | `talent_id, topic_id` | 已发布 |
| `ads_talent_collaborator` | 一条有向人才合作关系一行 | `talent_id, collaborator_talent_id` | 已发布 |
| `ads_talent_similarity` | 一名人才一个相似类型的一个候选一行 | `talent_id, similar_talent_id, similarity_type` | 4.3.0发布research_topic Top 3 |
| `ads_talent_yearly_metrics` | 一名人才一个自然年一行 | `talent_id, year` | 已发布 |
| `ads_talent_yearly_discipline` | 一名人才一年一个Field一行 | `talent_id, statistics_year, field_id` | 4.5.0新增并发布 |
| `ads_talent_mobility_event` | 一名人才一次严格识别的迁移事件一行 | `mobility_event_id` | 4.5.0新增并发布 |
| `ads_talent_mobility_yearly_flow` | 一年一条地区/机构/Field有向流向边一行 | `flow_id` | 4.5.0新增；9.16.0增加当前单一原因展示字段 |
| `ads_talent_mobility_flow_detail` | 一条流向边一个TopN明细项一行 | `flow_id, detail_type, detail_id, related_detail_id` | 4.5.0新增并发布 |
| `ads_talent_institution_cooperation` | 一名人才一个合作机构一行 | `talent_id, institution_id` | 9.8.0发布企业合作MVP v1 |
| `ads_talent_institution_cooperation_project` | 一名人才与一家机构的一个合作项目一行 | `talent_id, institution_id, project_id` | 9.8.0新增；同篇受资助论文证据 |
| `ads_talent_institution_cooperation_paper` | 一名人才与一家机构在一个项目下的一篇共同论文一行 | `talent_id, institution_id, project_id, paper_id` | 9.8.0新增；完整论文证据 |
| `ads_talent_institution_cooperation_patent` | 一名人才与一家机构的一件共同专利一行 | `talent_id, institution_id, patent_id` | 9.8.0新增；confirmed assignee证据 |
| `ads_talent_patent` | 一名人才一件专利一行 | `talent_id, patent_id` | 已发布 |
| `ads_talent_patent_cited_paper` | 一名人才的一件专利引用一篇论文一行 | `talent_id, patent_id, paper_id` | 已发布 |
| `ads_talent_research_to_patent_metrics` | 一名人才一个不可变指标版本一行 | `talent_id, metric_version` | 4.9.0新增 |
| `ads_talent_observed_citation_metrics` | 一名人才一个不可变已观察引用指标版本一行 | `talent_id, metric_version` | 6.31.0新增并发布MVP v1 |
| `ads_paper_profile` | 一篇发布 MVP core 论文一行 | `paper_id` | 1.7.0新增并发布 |
| `ads_patent_profile` | 一件 MVP Google Patent publication 一行 | `patent_id` | 1.7.0新增并发布 |
| `ads_patent_cited_paper` | 一件专利引用一篇发布 MVP core 论文一行 | `patent_id, paper_id` | 1.7.0新增并发布 |
| `ads_patent_analysis_summary` | 一个分析运行一行 | `run_id` | 6.2.0新增并发布 |
| `ads_patent_analysis_topic` | 一个运行的一个Topic在一个统计期间一行 | `run_id, topic_id, relation_type, period_key` | 6.2.0新增并发布；Topic为被引论文Primary Topic |
| `ads_patent_analysis_topic_patent` | 一个运行的一个Topic与一件专利一行 | `run_id, topic_id, patent_id` | 6.3.0新增并发布；核心专利为证据强度代理Top 100 |
| `ads_patent_analysis_jurisdiction` | 一个运行的一个公开辖区在一个统计期间一行 | `run_id, jurisdiction_code, period_key` | 6.2.0新增并发布 |
| `ads_patent_analysis_institution` | 一个运行的一个已确认受让机构一行 | `run_id, institution_id, period_key` | 6.2.0新增并发布 |
| `ads_patent_analysis_institution_edge` | 一个运行的一对共同受让机构一行 | `run_id, source_institution_id, target_institution_id, relation_type` | 6.2.0新增并发布 |
| `ads_patent_analysis_ipc` | 一个运行的一个IPC来源代码或部类一行 | `run_id, classification_code, classification_level, period_key` | 6.2.0新增并发布 |
| `ads_patent_analysis_inventor` | 一个运行的一个来源姓名Key一行 | `run_id, inventor_key, period_key` | 6.2.0新增并发布；Top 10000 |
| `ads_patent_analysis_cross_metric` | 一个运行的一对分析维度及一个指标一行 | `run_id, dimension_x_type, dimension_x_id, dimension_y_type, dimension_y_id, metric_code` | 6.2.0新增；6.3.1发布完整Topic×辖区矩阵 |
| `ads_patent_analysis_cross_year` | 一个运行的一个辖区、Topic和自然年一行 | `run_id, jurisdiction_code, topic_id, statistics_year` | 6.11.0新增并发布完整1990—2025年度矩阵 |
| `ads_patent_analysis_coverage` | 一个运行的一个数据域覆盖率一行 | `run_id, data_domain` | 6.2.0新增并发布 |
| `ads_patent_analysis_classification` | 一个运行、分类体系、版本和分类节点一行 | `run_id, scheme, release_id, classification_code` | 6.8.0新增并发布IPC/CPC字典快照 |
| `ads_patent_analysis_assignee` | 一个运行的一个全局来源申请人名称Key一行 | `run_id, assignee_key` | 6.9.0新增并发布；专利去重后全局申请人节点，不跨Topic重复计数 |
| `ads_patent_analysis_patent_institution` | 一个运行的一件专利与一个来源申请人Key一行 | `run_id, patent_id, assignee_key` | 6.10.0新增并发布；confirmed与未确认关系全部保留 |
| `ads_patent_analysis_topic_cpc` | 一个运行的一个Topic与一个CPC分类一行 | `run_id, topic_id, cpc_code` | 6.8.0新增并发布；完整非TopN分布 |
| `ads_patent_analysis_topic_assignee` | 一个运行的一个Topic与一个来源申请人名称Key一行 | `run_id, topic_id, assignee_key` | 6.8.0新增并发布；来源名称覆盖94.9828% |
| `ads_patent_analysis_topic_institution` | 一个运行的一个Topic与一个已确认平台机构一行 | `run_id, topic_id, institution_id` | 6.8.0新增并发布；确认解析覆盖1.9291% |
| `ads_patent_analysis_jurisdiction_institution` | 一个运行的一个公开辖区与一个已确认平台机构一行 | `run_id, jurisdiction_code, institution_id` | 6.8.0新增并发布 |
| `ads_patent_analysis_institution_classification` | 一个运行的一个机构与一个IPC/CPC分类一行 | `run_id, institution_id, scheme, classification_code` | 6.8.0新增并发布 |
| `ads_patent_analysis_institution_year` | 一个运行的一个机构与一个自然年一行 | `run_id, institution_id, statistics_year` | 6.8.0新增并发布 |
| `ads_patent_analysis_institution_inventor` | 一个运行的一个机构与一个来源发明人姓名Key一行 | `run_id, institution_id, inventor_key` | 6.8.0新增并发布 |
| `ads_patent_analysis_ipc_topic` | 一个运行的一个IPC代码与一个Topic一行 | `run_id, ipc_code, topic_id` | 6.8.0新增并发布；完整非TopN分布 |
| `ads_patent_analysis_entity_patent` | 一个运行的辖区、IPC或机构代表专利一行 | `run_id, entity_type, entity_id, patent_id` | 6.8.0新增并发布；每实体最多20件代理排名 |
| `ads_institution_type` | 一个机构类型一行 | `institution_type_id` | 已发布，含 OpenAlex 类型及 unknown 兜底类型 |
| `ads_location` | 一个平台位置一行 | `location_id` | 已发布 |
| `ads_location_external_id` | 一个外部位置编码映射一行 | `id_namespace, external_id` | 已发布 |
| `ads_discipline_domain` | 一个学科 Domain 一行 | `domain_id` | 1.5.0新增并发布 |
| `ads_discipline_field` | 一个学科 Field 一行 | `field_id` | 1.5.0新增并发布 |
| `ads_discipline_subfield` | 一个学科 Subfield 一行 | `subfield_id` | 1.5.0新增并发布 |
| `ads_discipline_topic` | 一个学科 Topic 一行 | `topic_id` | 1.5.0新增并发布 |
| `ads_emerging_topic_yearly_metrics` | 一个Topic一个自然年一行 | `topic_id, statistics_year` | 4.4.0新增并发布 |
| `ads_emerging_topic_snapshot` | 一个Topic一行 | `topic_id` | 4.4.0新增并发布 |
| `ads_emerging_topic_key_talent` | 一个Topic一名关键人才一行 | `topic_id, talent_id` | 4.4.0新增并发布 |
| `ads_institution_profile` | 一个机构一行 | `institution_id` | 已发布；1.4.0增加项目总数 |
| `ads_institution_paper` | 一个机构的一篇代表论文；每机构最多20篇 | `institution_id, paper_id` | 5.1.0新增并发布 |
| `ads_institution_patent` | 一个机构的一件代表专利；每机构最多20件 | `institution_id, patent_id` | 5.1.0新增并发布 |
| `ads_institution_discipline_profile` | 一个机构的一个 Topic 一行，并展开 Field/Subfield | `institution_id, topic_id` | 已发布 |
| `ads_institution_yearly_metrics` | 一个机构一个自然年一行 | `institution_id, statistics_year` | 已发布 |
| `ads_institution_collaboration_yearly` | 一个目标机构与一个合作机构在一个自然年一行 | `institution_id, collaborator_institution_id, statistics_year` | 1.10.0新增并发布论文合作；专利合作字段预留 |
| `ads_institution_collaboration_subfield_yearly` | 一个目标机构、合作机构、自然年与合作Subfield一行 | `institution_id, collaborator_institution_id, statistics_year, subfield_id` | 6.12.0新增；只使用共同论文与confirmed共同受让专利证据 |
| `ads_institution_topic_entry` | 一个机构在一个 Primary Topic 的首次观察进入事实一行 | `institution_id, topic_id` | 1.12.0新增并发布 |
| `ads_institution_technology_power` | 一个具有 MVP core 论文证据的机构一行 | `institution_id` | 1.13.0新增并发布；四指标科研技术力 MVP 评分 |
| `ads_industry` | 一个产业分类体系的一个节点一行 | `taxonomy_id, industry_id` | 1.11.0新增并发布 |
| `ads_institution_industry` | 一个机构在一个分类体系的一个产业节点一行 | `institution_id, taxonomy_id, industry_id` | 1.11.0新增；5.0.0发布assignee与发明人任职证据并集 |
| `ads_sz_gkx_industry_cluster` | 深圳GKX独立体系的一个产业集群一行 | `cluster_code` | 6.5.0新增并发布 |
| `ads_sz_gkx_industry_cluster_subfield` | 一个集群关联一个Subfield一行 | `cluster_code, subfield_id` | 6.5.0自动批准并发布 |
| `ads_sz_gkx_industry_cluster_topic` | 一个集群关联一个Topic一行 | `cluster_code, topic_id` | 6.5.0按Subfield继承；6.6.0增加产业链位置 |
| `ads_talent_industry_activity` | 一名人才在一个分类体系的一个产业节点一行 | `talent_id, taxonomy_id, industry_id` | 2.2.0新增并发布 |
| `ads_talent_industrial_capability_result` | 一名人才在一个产业力模型版本一行 | `talent_id, model_version` | 9.3.0新增；论文基础覆盖全体人才，产业活动证据可空 |
| `ads_technology_commercial_value_simulation` | 一个固定目录技术的一个模拟版本一行 | `catalog_release_id, tech_id, simulation_version` | 2.3.0新增并发布；仅限模拟 |
| `ads_talent_industry_capability_simulation` | 一名人才在一个产业节点的一个模拟版本一行 | `talent_id, taxonomy_id, industry_id, simulation_version` | 4.1.0统一为全量覆盖模拟；仅限模拟 |
| `ads_project_profile` | 一个科研项目一行 | `project_id` | 1.4.0新增 |
| `ads_talent_project` | 一名人才关联一个科研项目一行 | `talent_id, project_id` | 1.9.0新增并发布 |
| `ads_project_institution` | 一个项目关联一个机构一行 | `project_id, institution_id` | 1.4.0新增 |
| `ads_project_topic` | 一个项目关联一个Topic一行 | `project_id, topic_id` | 1.4.0新增 |
| `ads_shenzhen_institution_field_funding` | 一家深圳机构一个Field一行 | `institution_id, field_id` | 6.19.0新增并发布 |
| `ads_shenzhen_institution_direction_funding` | 一家深圳机构一个Primary Topic一行 | `institution_id, primary_topic_id` | 6.19.0新增并发布；携带Subfield和Field |
| `ads_talent_yearly_location` | 一名人才一年一个观察位置一行 | `talent_id, statistics_year, location_id` | 4.5.0已发布 |
| `ads_geo_yearly_metrics` | 一个位置一个自然年一行 | `location_id, statistics_year` | 1.6.0已发布 |
| `ads_geo_yearly_discipline_metrics` | 一个位置一年一个Topic一行 | `location_id, statistics_year, topic_id` | 1.6.0已发布 |
| `ads_topic_country_snapshot` | 一个Topic在一个国家/地区的当前完整年度论文分布快照 | `topic_id, country_location_id` | 6.1.0新增并发布 |
| `ads_geo_yearly_institution_type_metrics` | 一个位置一年一种机构类型一行 | `location_id, statistics_year, institution_type_id` | 1.6.0已发布 |
| `ads_geo_yearly_index` | 一个位置一年一种指数一行 | `location_id, statistics_year, index_code` | 1.6.0预留空表 |
| `ads_resource_benchmark_city` | 一个基准版本的一座城市一行 | `benchmark_version, city_location_id` | 6.25.0新增并发布固定十城基准 |
| `ads_city_subfield_resource_yearly` | 一座基准城市一年一个Subfield一行 | `city_location_id, statistics_year, subfield_id` | 6.25.0新增并发布2015—2025完整网格 |
| `ads_institution_subfield_resource_yearly` | 一家十城机构一年一个有证据Subfield；深圳补齐零值网格 | `institution_id, statistics_year, subfield_id` | 6.25.0新增并发布 |
| `ads_city_field_resource_yearly` | 一座基准城市一年一个Field一行 | `city_location_id, statistics_year, field_id` | 9.25.0新增并发布2015—2025完整网格 |
| `ads_institution_field_resource_yearly` | 一家十城机构一年一个有证据Field；深圳补齐零值网格 | `institution_id, statistics_year, field_id` | 9.25.0新增并发布 |
| `ads_city_domain_resource_yearly` | 一座基准城市一年一个Domain一行 | `city_location_id, statistics_year, domain_id` | 9.26.0新增并发布2015—2025完整网格 |
| `ads_institution_domain_resource_yearly` | 一家十城机构一年一个有证据Domain；深圳补齐零值网格 | `institution_id, statistics_year, domain_id` | 9.26.0新增并发布 |
| `ads_research_resource_shortage_yearly` | 一个城市或机构一年一个Subfield的一项资源指标 | `target_type, target_id, statistics_year, subfield_id, metric_code, benchmark_version` | 6.25.0新增；差距超过50%标关键短板 |
| `ads_resource_optimization_recommendation` | 一个城市或机构一个年度一个Subfield一条聚合优化建议 | `recommendation_id` | 6.28.0新增；仅使用已评估、正值、关键短板 |
| `ads_resource_optimization_recommendation_evidence` | 一条优化建议的一项来源短板指标证据 | `recommendation_id, metric_code, benchmark_version` | 6.28.0新增；可回溯目标、基准、差距和覆盖状态 |
| `ads_technology_profile` | 一个技术点一行 | `technology_node_id` | 4.6.0新增；6.0.0确认为ETO Cluster技术点 |
| `ads_technology_graph_edge` | 一条候选技术关系一行 | `edge_id` | 4.6.0新增并发布 |
| `ads_technology_graph_edge_paper` | 一条完美技术关系的一篇组合级论文 | `edge_id, paper_id` | 9.18.0新增；首版物化一条edge |
| `ads_technology_graph_edge_institution` | 一条重点技术关系的一家核心共同机构 | `edge_id, institution_id` | 9.11.0新增 |
| `ads_technology_graph_edge_patent` | 一条重点技术关系的一件完整共同专利 | `edge_id, patent_id` | 9.11.0新增 |
| `ads_technology_graph_edge_project` | 一条重点技术关系的一个既有重点项目 | `edge_id, project_id` | 9.11.0新增 |
| `ads_technology_graph_node` | 一个可视化技术节点一行 | `technology_node_id` | 4.7.0新增，携带主簇群与演进摘要 |
| `ads_technology_community` | 一个图算法技术簇群一行 | `community_id` | 4.7.0新增并发布 |
| `ads_technology_community_member` | 技术簇群的一个成员节点 | `community_id, technology_node_id` | 4.7.0新增并发布 |
| `ads_technology_evolution_yearly` | 技术节点一个观察年份 | `technology_node_id, statistics_year` | 4.7.0新增并发布 |
| `ads_technology_evolution_edge` | 一条带时间的候选技术关系 | `evolution_edge_id` | 4.7.0新增并发布 |
| `ads_technology_evolution_path_step` | 一条代表路径的一个步骤 | `path_id, step_order` | 4.7.0新增并发布 |
| `ads_technology_paper` | 技术节点的一篇代表论文 | `technology_node_id, paper_id` | 4.6.0新增并发布 |
| `ads_technology_patent` | 技术节点的一件代表专利 | `technology_node_id, patent_id` | 4.6.0新增并发布 |
| `ads_technology_institution` | 技术节点的一个关联机构 | `technology_node_id, institution_id` | 4.6.0新增并发布 |
| `ads_technology_application_case` | 技术节点的一个项目案例 | `technology_node_id, application_case_id` | 4.6.0新增；仅科研项目代理 |
| `ads_technology_yearly_metrics` | 技术节点一年 | `technology_node_id, statistics_year` | 4.6.0新增并发布 |
| `ads_technology_milestone_event` | 技术节点的一类确定性关键事件 | `event_id` | 9.13.0新增；首版五类规则事件 |
| `ads_technology_dynamic` | 一个发布中的一条完美技术动态 | `release_id, dynamic_id` | 9.19.0新增；首版15条 |
| `ads_technology_dynamic_content` | 一条完美技术动态的DeepSeek循证内容 | `release_id, dynamic_id` | 9.19.0新增；事件、背景及行业影响 |
| `ads_technology_dynamic_evidence` | 一条技术动态的一项关键事件 | `release_id, dynamic_id, evidence_type, evidence_id` | 9.22.0仅保存45条EVENT |
| `ads_technology_dynamic_event_content` | 一条技术动态的一个事件的DeepSeek循证内容 | `release_id, dynamic_id, event_id` | 9.20.0新增；逐事件完整覆盖 |
| `ads_technology_hotspot_signal` | 技术节点的一个语义信号 | `technology_node_id, signal_id` | 4.6.0新增并发布 |
| `ads_technology_hotspot_snapshot` | 技术节点一个热点模型版本 | `technology_node_id, model_version` | 4.6.0新增并发布 |
| `ads_technology_hotspot_yearly` | 技术节点一个自然年的热度曲线点 | `technology_node_id, statistics_year, model_version` | 6.18.0新增；论文按发表年、引用按收到引用年 |
| `ads_technology_potential_dimension` | 技术潜力评估的一个维度 | `technology_node_id, model_version, scenario_id, dimension_code` | 4.6.0新增并发布 |
| `ads_technology_potential_assessment` | 技术的一次潜力评估 | `assessment_id` | 4.6.0新增并发布 |
| `ads_technology_potential_evidence` | 潜力评估的一条证据 | `assessment_id, evidence_id` | 4.6.0新增并发布 |
| `ads_technology_stage_assessment` | 技术的一次阶段研判 | `assessment_id` | 4.6.0发布确定性基线 |
| `ads_technology_assessment_evidence` | 阶段研判的一条证据 | `assessment_id, evidence_id` | 4.6.0新增并发布 |
| `ads_technology_region_yearly_metrics` | 技术—城市—年份 | `technology_node_id, location_id, statistics_year` | 4.6.0新增并发布 |
| `ads_technology_region_institution` | 技术—城市—机构 | `technology_node_id, location_id, institution_id` | 4.6.0新增并发布 |
| `ads_technology_region_assessment` | 技术—城市的一次评估 | `technology_node_id, location_id, model_version` | 4.6.0新增并发布 |
| `ads_technology_policy_evidence` | 技术—地区的一条政策证据 | `technology_node_id, location_id, policy_id` | 4.6.0建表；当前无数据 |
| `ads_technology_transfer_stage` | 一个转化阶段 | `stage_code` | 4.6.0新增并发布8阶段 |
| `ads_technology_bottleneck_assessment` | 技术在一个阶段的堵点评估 | `assessment_id, stage_code, bottleneck_code` | 4.6.0发布证据缺口诊断 |
| `ads_technology_bottleneck_evidence` | 堵点评估的一条外部证据 | `assessment_id, stage_code, evidence_id` | 4.6.0建表；当前无数据 |
| `ads_technology_data_coverage` | 技术节点的一个数据域覆盖状态 | `technology_node_id, domain_code` | 4.6.0新增并发布 |
| `ads_technology_disruption_assessment` | 一个技术点的一个颠覆性代理模型评估 | `assessment_id` | 5.18.0新增；论文证据基线 |
| `ads_technology_disruption_paper_evidence` | 一次颠覆性候选或高影响观察评估的一篇代表论文证据 | `assessment_id, paper_id` | 5.18.0新增 |
| `ads_research_problem_release` | 一个基础问题发布批次 | `release_id` | 5.2.0新增 |
| `ads_research_problem_overview_snapshot` | 一个总览统计日 | `snapshot_date` | 5.2.0新增 |
| `ads_research_problem_profile` | 一个基础研究问题 | `problem_id` | 5.2.0新增 |
| `ads_research_problem_discipline` | 一个问题关联一个Topic | `problem_id, topic_id` | 5.2.0新增 |
| `ads_research_problem_discipline_metrics` | 一个Topic当前统计 | `topic_id` | 5.2.0新增 |
| `ads_research_problem_discipline_yearly` | 一个Topic一个观察年份 | `topic_id, statistics_year` | 5.2.0新增 |
| `ads_research_problem_semantic_relation` | 一个问题的一条语义三元组 | `semantic_relation_id` | 5.2.0新增；待复核 |
| `ads_research_problem_keyword` | 一个问题的一个规范关键词 | `problem_keyword_id` | 5.2.0新增；待复核 |
| `ads_research_problem_keyword_metrics` | 一个规范关键词当前统计 | `keyword_key` | 5.2.0新增 |
| `ads_research_problem_keyword_yearly` | 一个规范关键词一个观察年份 | `keyword_key, statistics_year` | 5.2.0新增 |
| `ads_research_problem_research_path` | 一个问题的一条研究路径或未来方向 | `research_path_id` | 5.2.0新增；待复核 |
| `ads_research_problem_yearly_metrics` | 一个问题一个观察年份 | `problem_id, statistics_year` | 5.2.0新增 |
| `ads_research_problem_hotspot_snapshot` | 一个问题一个热点模型版本 | `problem_id, model_version` | 5.2.0新增 |
| `ads_research_problem_paper` | 一个问题关联一篇平台论文 | `problem_id, paper_id` | 5.2.0新增 |
| `ads_research_problem_patent` | 一个问题关联一件平台专利 | `problem_id, patent_id` | 5.2.0新增 |
| `ads_research_problem_project` | 一个问题关联一个平台项目 | `problem_id, project_id` | 5.2.0新增 |
| `ads_research_problem_talent` | 一个问题关联一名平台人才 | `problem_id, talent_id` | 5.2.0新增 |
| `ads_research_problem_institution` | 一个问题关联一个平台机构 | `problem_id, institution_id` | 5.2.0新增 |
| `ads_research_problem_graph_edge` | 两个问题间的一条关系 | `edge_id` | 5.2.0新增 |
| `ads_research_problem_event` | 一个问题的一条时间轴事件 | `event_id` | 5.2.0新增 |
| `ads_research_problem_provenance` | 一个问题一个来源域的溯源记录 | `provenance_id` | 5.2.0新增 |
| `ads_research_problem_change_log` | 一个问题的一条状态变更 | `change_id` | 5.2.0新增 |
| `ads_research_problem_monthly_metrics` | 一个问题一个连续观测月份的直接证据月度事实 | `problem_id, statistics_month` | 5.16.0写入真实日期聚合与月度热度 |
| `ads_research_problem_monthly_estimate` | 一个问题一个月份一个估算指标 | `problem_id, statistics_month, metric_name` | 5.5.0新增；与月度事实严格隔离 |
| `ads_research_problem_development_snapshot` | 一个问题一个发展模型版本 | `problem_id, model_version` | 5.3.0新增 |
| `ads_research_problem_heat_component` | 一个问题一个热度分项 | `problem_id, model_version, component_code` | 5.3.0新增 |
| `ads_research_problem_region_yearly_metrics` | 一个问题一个地区一个年份 | `problem_id, location_level, location_id, statistics_year` | 5.3.0新增 |
| `ads_research_problem_region_snapshot` | 一个问题一个地区的当前竞争画像 | `problem_id, location_level, location_id, model_version` | 5.3.0新增 |
| `ads_research_problem_region_institution` | 一个问题在一个地区的一家机构 | `problem_id, location_id, institution_id` | 5.3.0新增 |
| `ads_research_problem_competition_rank` | 一个问题一个范围一个主体一个排名维度 | `problem_id, competition_scope, subject_id, ranking_dimension` | 5.3.0新增 |
| `ads_research_problem_funding_evidence` | 一个问题关联项目的资金证据 | `problem_id, project_id` | 5.3.0新增 |
| `ads_research_problem_policy_evidence` | 一个问题关联一项官方政策证据 | `problem_id, policy_id` | 5.12.0接入真实政策DWD并发布 |
| `ads_research_problem_policy_yearly_metrics` | 一个问题在一个年份、政策层级和支持类型的统计 | `problem_id, statistics_year, policy_level, support_type` | 5.12.0新增并发布 |
| `ads_research_problem_potential_dimension` | 一次潜力评估的一个维度 | `assessment_id, dimension_code` | 5.3.0新增 |
| `ads_research_problem_potential_assessment` | 一个问题的一次潜力评估 | `assessment_id` | 5.3.0新增 |
| `ads_research_problem_potential_evidence` | 一个潜力维度的一条证据 | `assessment_id, dimension_code, evidence_id` | 5.3.0新增 |
| `ads_research_problem_forecast_yearly` | 一个问题一个模型年份指标预测；当前为空 | `problem_id, forecast_model_version, forecast_year, target_metric` | 5.3.0新增；等待预测模型 |
| `ads_research_problem_similarity` | 一个问题与另一个问题的相似度 | `problem_id, similar_problem_id, model_version` | 5.3.0新增图特征基线 |
| `ads_research_problem_recommendation` | 一条问题推荐结果 | `recommendation_id` | 5.3.0新增 |
| `ads_research_problem_recommendation_evidence` | 一条推荐的一条证据 | `recommendation_id, evidence_id` | 5.3.0新增 |
| `ads_research_problem_deployment` | 一个问题一个部署版本 | `problem_id, deployment_version` | 5.4.0新增；待补录部署决策 |
| `ads_research_problem_direction` | 一个问题的一条研究方向；同一问题允许多条 | `direction_id` | 5.12.1按操作方批准策略全部发布为APPROVED |
| `ads_research_problem_institution_match` | 一个问题与一家深圳机构的匹配版本 | `problem_id, institution_id, model_version` | 5.14.0补充同证据论文署名机构人才事实 |
| `ads_research_problem_institution_achievement` | 一个问题、机构与一项经机构关系验证的成果 | `achievement_relation_id` | 5.13.0新增 |
| `ads_research_problem_institution_discipline_metrics` | 一家机构在一个问题学科Topic下的成果聚合 | `institution_id, topic_id, model_version` | 5.13.0新增 |
| `ads_research_problem_scope_potential_dimension` | 一个Topic/Field/Domain范围的一个潜力维度 | `scope_type, scope_id, dimension_code, model_version` | 5.15.0新增并发布 |
| `ads_research_problem_scope_strategy` | 一个Topic/Field/Domain范围的一条战略优先级结果 | `scope_type, scope_id, strategy_version` | 5.15.0新增并发布 |
| `ads_research_problem_strategic_advice` | 一条问题或学科范围的战略建议 | `advice_id` | 5.15.0补充正式Topic/Field/Domain建议 |
| `ads_research_problem_update_signal` | 一个问题的一条增量变化信号 | `signal_id` | 5.4.0新增；等待跨发布比较 |
| `ads_research_problem_collaboration_recommendation` | 一个问题的一个潜在合作领域推荐 | `recommendation_id` | 5.11.0新增并发布 |
| `ads_talent_capability_model` | 一个已发布人员能力与问题匹配模型版本 | `model_version` | 6.22.0新增并发布 |
| `ads_talent_capability_assessment` | 一名人才在一个固定模型下的人才级能力评分 | `talent_id, model_version` | 6.22.0新增并发布 |
| `ads_talent_capability_dimension_metric` | 一名人才一个评分维度下的一项解释指标 | `talent_id, model_version, dimension_code, metric_code` | 6.22.0新增并发布 |
| `ads_talent_research_problem_discipline_match_topic` | 一名人才与一个深圳相关问题的一个候选Topic证据 | `talent_id, problem_id, topic_id, match_model_version` | 6.22.0新增并发布 |
| `ads_talent_research_problem_discipline_match` | 一名人才与一个深圳相关基础研究问题的匹配结果 | `talent_id, problem_id, match_model_version` | 6.22.0新增并发布 |
| `ads_recommendation_run` | 一次智能推荐模型运行一行 | `recommendation_run_id` | 6.26.0新增并发布 |
| `ads_scientific_update_signal` | 一次运行中一个主体的一条新增或变更信号 | `signal_id` | 6.26.0新增并发布 |
| `ads_recommendation_paper` | 一次运行的一篇Top论文 | `recommendation_run_id, paper_id` | 6.26.0新增并发布 |
| `ads_recommendation_talent` | 一次运行推荐的一名高H指数人才 | `recommendation_run_id, talent_id` | 6.26.0新增并发布 |
| `ads_recommendation_resource_direction` | 一次运行推荐的一个Topic资源方向 | `recommendation_run_id, topic_id` | 6.26.0新增并发布 |
| `ads_recommendation_investment_direction` | 一次运行推荐的一个Technology投资方向 | `recommendation_run_id, technology_node_id` | 6.26.0新增并发布 |
| `ads_recommendation_evidence` | 一个推荐结果的一条可追溯证据 | `recommendation_run_id, recommendation_type, recommendation_id, evidence_id` | 6.26.0新增并发布 |

## 4. `ads_talent_profile`

一名人才一行的当前主画像。论文指标必须由发布的 MVP core 数据重算，不读取 OpenAlex full
中 `dwd_author.works_count` 或 `dwd_author.cited_by_count` 作为 ADS 指标。

主画像不保存未定义的单值产业力。9.3.0起，人才级单值只能使用
`ads_talent_industrial_capability_result`定义的版本化论文基础—产业证据聚合结果，并将当前版本投影到
`industrial_capability_*`字段。人才在各产业节点的结果仍查询
`ads_talent_industry_activity.industry_activity_score`；该分数是节点级产业技术活动分，不得直接取最大值或任意一行
伪造人才级产业力。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份 | `talent_id` | `VARCHAR(64) NOT NULL` | North Star统一人才ID，与外部来源ID解耦 |
| 身份 | `openalex_author_id` | `VARCHAR(64)` | OpenAlex Author ID，来源映射便利列，不作为平台主键 |
| 身份 | `orcid` | `VARCHAR(32)` | ORCID |
| 姓名 | `name` | `VARCHAR(512)` | ETL去除空串后优先中文，其次英文和原始姓名 |
| 姓名 | `name_zh` | `VARCHAR(512)` | 有确切来源的标准中文姓名；拼音逆推结果不得写入 |
| 姓名 | `name_zh_candidate` | `VARCHAR(512)` | 拼音逆推的当前中文候选名；不是已核验事实，前端必须标记“推测” |
| 姓名 | `name_en` | `VARCHAR(512)` | 标准英文姓名 |
| 姓名 | `name_original` | `VARCHAR(512)` | 上游原始姓名 |
| 姓名 | `name_pinyin` | `VARCHAR(512)` | 中文姓名全拼，如 shi yigong |
| 姓名 | `name_pinyin_compact` | `VARCHAR(512)` | 无空格拼音，如 shiyigong |
| 姓名 | `name_initials` | `VARCHAR(64)` | 拼音首字母，如 syg |
| 姓名 | `name_aliases` | `ARRAY<STRING>` | 姓名别名集合 |
| 姓名 | `name_zh_source` | `VARCHAR(64)` | 当前中文值来源；拼音逆推固定为`PINYIN_INFERENCE`，未来确切来源填写具体来源类型 |
| 姓名 | `name_zh_confidence` | `DECIMAL(5,4)` | 候选排序分0至1，不表示姓名为真的概率 |
| 基础资料 | `gender` | `TINYINT` | 0未知 1男 2女 9未说明 |
| 基础资料 | `birth_year` | `SMALLINT` | 出生年份 |
| 基础资料 | `avatar_url` | `VARCHAR(2048)` | 头像地址 |
| 基础资料 | `web_url` | `VARCHAR(2048)` | 个人主页 |
| 基础资料 | `title` | `VARCHAR(255)` | 职称 |
| 基础资料 | `telephone` | `VARCHAR(64)` | 联系电话 |
| 基础资料 | `email` | `VARCHAR(320)` | 邮箱 |
| 基础资料 | `talent_bio` | `STRING` | 中文简介 |
| 基础资料 | `talent_bio_en` | `STRING` | 英文简介 |
| 影响描述 | `impact_description` | `STRING` | 基于固定论文、专利、职称和已核验荣誉证据生成的中文影响描述；不是人工核验事实 |
| 影响描述 | `impact_description_nature` | `VARCHAR(64)` | 固定`LLM_EVIDENCE_GROUNDED_SYNTHESIS` |
| 影响描述 | `impact_description_provider` | `VARCHAR(64)` | 实际模型服务提供方 |
| 影响描述 | `impact_description_model` | `VARCHAR(128)` | 实际模型名称 |
| 影响描述 | `impact_description_prompt_version` | `VARCHAR(96)` | 固定Prompt版本 |
| 影响描述 | `impact_description_input_hash` | `VARCHAR(64)` | 规范化输入证据SHA-256 |
| 影响描述 | `impact_description_generated_at` | `DATETIME(3)` | 模型内容生成时间UTC |
| 影响描述 | `impact_description_review_status` | `VARCHAR(48)` | 当前固定`MODEL_GENERATED_NOT_HUMAN_VERIFIED` |
| 影响描述 | `impact_description_evidence` | `VARIANT` | 支撑论文、专利、荣誉ID、证据计数、不确定性说明与置信度的有界快照 |
| 当前机构 | `current_institution` | `VARIANT` | 当前机构完整展示快照 |
| 当前机构 | `current_institution_ids` | `ARRAY<VARCHAR(64)>` | 当前机构ID；企业也属于机构，通过机构类型区分 |
| 当前机构 | `country_location_id` | `VARCHAR(64)` | 当前已解析机构的平台国家位置ID |
| 当前机构 | `province_location_id` | `VARCHAR(64)` | 当前已解析机构的平台省级位置ID；无法可靠确定时为空 |
| 当前机构 | `city_location_id` | `VARCHAR(64)` | 当前已解析机构的平台城市位置ID |
| 当前机构 | `district_location_id` | `VARCHAR(64)` | 当前已解析机构的平台区县位置ID；当前来源不足时可为空 |
| 高频派生状态 | `is_academician` | `TINYINT` | 是否院士0否1是NULL未知 |
| 项目 | `projects` | `VARIANT` | 仅代表项目TopN展示快照，不保存全量项目事实 |
| 项目 | `project_ids` | `ARRAY<VARCHAR(64)>` | 参与项目ID |
| 学科分类 | `discipline_domains` | `VARIANT` | MVP core完整去重Domain对象数组，每项含id、name、name_en |
| 学科分类 | `discipline_fields` | `VARIANT` | MVP core完整去重Field对象数组，每项含id、name、name_en |
| 学科分类 | `discipline_subfields` | `VARIANT` | MVP core完整去重Subfield对象数组，每项含id、name、name_en |
| 学科分类 | `discipline_topics` | `VARIANT` | MVP core完整去重Topic对象数组，每项含id、name、name_en；统计查询topic_profile |
| 学科分类 | `domain_ids` | `ARRAY<VARCHAR(64)>` | Domain ID集合 |
| 学科分类 | `field_ids` | `ARRAY<VARCHAR(64)>` | Field ID集合 |
| 学科分类 | `subfield_ids` | `ARRAY<VARCHAR(64)>` | Subfield ID集合 |
| 学科分类 | `topic_ids` | `ARRAY<VARCHAR(64)>` | Topic ID集合 |
| 评分 | `academic_capability` | `DECIMAL(10,4)` | 0至100学术力默认分；只对标准化分加权 |
| 评分 | `academic_capability_rank` | `BIGINT` | 固定MVP基准总体中的学术力稳定降序排名 |
| 评分 | `academic_benchmark_talent_count` | `BIGINT` | 学术力标准化时固定基准总体人数 |
| 评分 | `academic_metric_weight_coverage` | `DECIMAL(5,4)` | 实际有值指标的默认权重之和，0至1 |
| 评分 | `paper_score` | `DECIMAL(9,6)` | 论文数0至100平均排名百分位分 |
| 评分 | `citation_score` | `DECIMAL(9,6)` | 累计被引0至100平均排名百分位分 |
| 评分 | `h_index_score` | `DECIMAL(9,6)` | H指数0至100平均排名百分位分 |
| 评分 | `collaboration_score` | `DECIMAL(9,6)` | 合作广度0至100平均排名百分位分 |
| 评分 | `core_source_score` | `DECIMAL(9,6)` | 100乘CWTS Core论文占已知Core状态论文比例 |
| 社会影响代理 | `social_impact_score` | `DECIMAL(9,6)` | 0至100社会影响代理分；v1严格等于当前学术力，不代表现实社会贡献 |
| 社会影响代理 | `social_impact_score_version` | `VARCHAR(64)` | 当前投影的社会影响代理评分版本 |
| 社会影响代理 | `social_impact_score_nature` | `VARCHAR(64)` | v1固定`ACADEMIC_IMPACT_PROXY` |
| 社会影响代理 | `social_impact_metric_coverage` | `DECIMAL(5,4)` | 当前实际输入指标权重覆盖率；v1复制学术力覆盖率 |
| 社会影响代理 | `social_impact_as_of_date` | `DATE` | 社会影响输入指标截止日；v1复制学术指标截止日 |
| 人才培养代理 | `talent_cultivation_score` | `DECIMAL(9,6)` | 0至100人才培养代理分；只对固定领军人才分类适用 |
| 人才培养代理 | `higher_education_teaching_years` | `DECIMAL(7,2)` | 经确认高校教职区间去重后的日历年数；不可计算时为NULL |
| 人才培养代理 | `talent_cultivation_evidence_status` | `VARCHAR(32)` | `YEAR_PRECISION/BASE_ONLY_UNKNOWN_DURATION/NOT_APPLICABLE` |
| 人才培养代理 | `talent_cultivation_score_version` | `VARCHAR(64)` | 当前投影的人才培养代理评分版本；非领军人才为NULL |
| 人才培养代理 | `talent_cultivation_as_of_date` | `DATE` | 任教年限计算截止日；非领军人才为NULL |
| 人才培养代理 | `talent_cultivation_score_reason` | `STRING` | 基础分、有效任教年限、公式和覆盖限制说明 |
| 评分 | `talent_potential` | `DECIMAL(10,4)` | 当前潜力模型中同主学科、同科研年限组的0至100综合百分位投影 |
| 评分 | `score_version` | `VARCHAR(32)` | 学术力评分模型版本；不得用于承载潜力模型版本 |
| 评分 | `is_potential_talent` | `TINYINT` | 当前潜力模型百分位不低于90为1，已评估未命中为0，未评估为NULL |
| 评分 | `potential_reason` | `STRING` | 仅潜力人才保留的确定性推荐理由；完整解释查询结果表 |
| 评分 | `potential_score_version` | `VARCHAR(64)` | 当前投影的潜力模型版本 |
| 评分 | `potential_metric_coverage` | `DECIMAL(5,4)` | 当前潜力模型实际进入综合分的权重和，0至1 |
| 评分 | `potential_metrics_as_of_date` | `DATE` | 当前潜力结果的指标统计截止日 |
| 产业力 | `industrial_capability_score` | `DECIMAL(9,6)` | 当前人才级产业力综合分，范围0–94.9；必须结合证据状态解释 |
| 产业力 | `industrial_capability_level` | `VARCHAR(32)` | 当前分数档位代码：`WEAK/POTENTIAL_FOUNDATION/RESEARCH_FOUNDATION/INITIAL/STRONG/OUTSTANDING/LEADING` |
| 产业力 | `industrial_capability_research_score` | `DECIMAL(9,6)` | 论文数、被引、MVP core H指数和CWTS Core来源分得到的0–100论文科研基础分 |
| 产业力 | `industrial_capability_industry_score` | `DECIMAL(9,6)` | 二级产业小样本收缩、Top 3加权和有界广度奖励后的0–100产业活动证据分；无证据时为NULL |
| 产业力 | `industrial_capability_evidence_status` | `VARCHAR(32)` | `RESEARCH_ONLY`或`INDUSTRY_EVIDENCE`；区分仅论文推导与已有产业活动事实 |
| 产业力 | `industrial_capability_primary_industry_id` | `VARCHAR(64)` | 小样本收缩后得分最高的二级产业ID；无产业证据时为NULL |
| 产业力 | `industrial_capability_source_industry_count` | `INT` | 参与汇总的二级产业数；无产业证据时为0 |
| 产业力 | `industrial_capability_strong_industry_count` | `INT` | 收缩后产业分不低于70的二级产业数 |
| 产业力 | `industrial_capability_score_version` | `VARCHAR(64)` | 当前投影的人才级产业力模型版本 |
| 产业力 | `industrial_capability_research_as_of_date` | `DATE` | 论文科研基础输入统计截止日 |
| 产业力 | `industrial_capability_industry_as_of_date` | `DATE` | 产业活动输入统计截止日；`RESEARCH_ONLY`时为NULL |
| 诚信演示分 | `research_integrity_score` | `DECIMAL(5,2)` | 0至100当前展示分；本版为人工固定演示值 |
| 诚信演示分 | `research_integrity_rating` | `VARCHAR(16)` | 分数不低于92显示“优秀”，否则“普通” |
| 诚信演示分 | `research_integrity_score_version` | `VARCHAR(64)` | 当前投影的固定评分版本 |
| 诚信演示分 | `research_integrity_score_nature` | `VARCHAR(64)` | 本版固定`SYNTHETIC_DEMO_NOT_EVIDENCE_BASED` |
| 媒体舆情 | `media_sentiment_score` | `DECIMAL(5,2)` | 当前30条媒体报道按人才聚合的百分制分数 |
| 媒体舆情 | `media_sentiment_rating` | `VARCHAR(16)` | 分数不低于85为“正面”，否则“普通” |
| 媒体舆情 | `media_risk_level` | `VARCHAR(16)` | 基于有限报道显式风险词的初步等级 |
| 媒体舆情 | `media_sentiment_reason` | `STRING` | 报道数、奖项/科研贡献信号、风险词和样本限制说明 |
| 媒体舆情 | `media_sentiment_assessment_version` | `VARCHAR(64)` | 当前投影的固定评估版本 |
| 媒体舆情 | `media_sentiment_score_nature` | `VARCHAR(64)` | 本版固定`RULE_BASED_LIMITED_MEDIA_SAMPLE` |
| 政治展示分 | `political_score` | `DECIMAL(5,2)` | 科学精神与价值观各50%的产品占位分 |
| 政治展示分 | `political_qualification_status` | `VARCHAR(16)` | 不低于75为“合格”，否则“普通” |
| 政治展示分 | `political_scientific_spirit_score` | `DECIMAL(5,2)` | `min(H-index,100)`占位分 |
| 政治展示分 | `political_value_orientation_score` | `DECIMAL(5,2)` | 逐价值主题子项的平均分 |
| 政治展示分 | `political_score_reason` | `STRING` | 公式、指标、价值主题数量和限制说明 |
| 政治展示分 | `political_assessment_version` | `VARCHAR(64)` | 当前展示分版本 |
| 政治展示分 | `political_score_nature` | `VARCHAR(64)` | 固定`SYNTHETIC_DEMO_NOT_POLITICAL_INFERENCE` |
| 科研指标 | `paper_count` | `BIGINT` | 累计去重论文数；NULL未计算，0确认为零；其他计数同理 |
| 科研指标 | `citations_count` | `BIGINT` | 累计引用数 |
| 科研指标 | `observed_citation_count` | `BIGINT` | 当前版本已观察引用边数；不是完整累计被引 |
| 科研指标 | `observed_classifiable_citation_count` | `BIGINT` | 当前版本可判定本人自引或他引的引用边数 |
| 科研指标 | `observed_self_citation_count` | `BIGINT` | 当前版本本人自引边数 |
| 科研指标 | `observed_non_self_citation_count` | `BIGINT` | 当前版本他引边数 |
| 科研指标 | `observed_non_self_citation_rate` | `DECIMAL(12,8)` | 他引数除以可判定引用数；无可判定引用时NULL |
| 科研指标 | `observed_citation_metric_version` | `VARCHAR(64)` | 当前投影的已观察他引率指标版本 |
| 科研指标 | `observed_citation_coverage_status` | `VARCHAR(32)` | PARTIAL/NOT_CLASSIFIABLE/NOT_AVAILABLE |
| 科研指标 | `h_index` | `INT` | H指数 |
| 科研指标 | `corresponding_count` | `BIGINT` | 通讯作者论文数 |
| 科研指标 | `core_eligible_paper_count` | `BIGINT` | 主发表来源is_core为非NULL的MVP core去重论文数 |
| 科研指标 | `core_paper_count` | `BIGINT` | 主发表来源is_core=true的MVP core去重论文数 |
| 科研指标 | `core_paper_ratio` | `DECIMAL(9,6)` | core_paper_count/core_eligible_paper_count，分母0为NULL |
| 科研指标 | `patent_application_count` | `BIGINT` | 累计专利申请数 |
| 科研指标 | `patent_grant_count` | `BIGINT` | 累计专利授权数 |
| 科研指标 | `patent_family_count` | `BIGINT` | 累计去重专利族数 |
| 科研指标 | `patent_metrics_as_of_date` | `DATE` | 专利指标统计截止日，不覆盖论文等其他指标截止日 |
| 科研指标 | `patent_metric_definition_version` | `VARCHAR(64)` | 专利指标口径版本 |
| 科研指标 | `research_to_patent_citation_rate` | `DECIMAL(12,8)` | 当前版本本人论文被本人关联专利引用率，范围0至1；不是商业成果转化率 |
| 科研指标 | `research_to_patent_cited_paper_count` | `BIGINT` | 当前版本被本人关联专利引用的本人去重MVP core论文数 |
| 科研指标 | `research_to_patent_metric_version` | `VARCHAR(64)` | 当前投影的本人论文专利引用指标版本 |
| 科研指标 | `research_to_patent_coverage_status` | `VARCHAR(32)` | 当前指标覆盖状态PARTIAL/NOT_AVAILABLE |
| 科研指标 | `project_count` | `BIGINT` | 参与项目数 |
| 科研指标 | `partner_institution_count` | `BIGINT` | 合作高校科研机构数 |
| 科研指标 | `institution_cooperation_project_count` | `BIGINT` | 机构合作项目数；可按机构类型筛选企业合作 |
| 科研指标 | `collaborating_expert_count` | `BIGINT` | 去重合作人才数 |
| 科研指标 | `international_collaboration_count` | `BIGINT` | 国际合作论文数，口径由指标版本定义 |
| 科研指标 | `patent_grant_rate` | `DECIMAL(9,6)` | 同口径授权数除以申请数；分母为0时NULL，不是专利转化率 |
| 状态与检索 | `status` | `TINYINT NOT NULL DEFAULT 1` | 1正常 0失效 |
| 状态与检索 | `source` | `TINYINT NOT NULL DEFAULT 0` | 0系统 1用户新增 |
| 状态与检索 | `create_time` | `DATETIME(3) NOT NULL` | 档案初次创建时间UTC，更新时保留 |
| 状态与检索 | `name_search_variants` | `ARRAY<STRING>` | 含标准中英文名和别名的小写规范化精确检索集合 |
| 状态与检索 | `name_updated_at` | `DATETIME(3)` | 名称最后修订时间UTC |
| 状态与检索 | `country_code` | `VARCHAR(8)` | 当前已解析机构所在地国家代码 |
| 状态与检索 | `country_name` | `VARCHAR(128)` | 当前已解析机构所在地国家名称 |
| 状态与检索 | `province` | `VARCHAR(128)` | 当前已解析机构所在地省或州 |
| 状态与检索 | `city` | `VARCHAR(128)` | 当前已解析机构所在地城市 |
| 状态与检索 | `location_display` | `VARCHAR(512)` | 国家、省州、城市去空去重后的机构所在地展示文案 |
| 状态与检索 | `tags` | `ARRAY<STRING>` | 展示标签，筛选优先使用标准ID |
| 机构合作 | `institution_cooperation_index` | `DECIMAL(10,4)` | 人才整体机构合作指数，不能直接相加各机构分数 |
| 机构合作 | `institution_cooperation_index_version` | `VARCHAR(64)` | 整体机构合作指数版本 |
| 机构合作 | `institution_cooperation_index_annotation` | `VARIANT` | 机构合作指数构成的有界展示快照 |
| 质量与版本 | `profile_completeness` | `DECIMAL(5,4)` | 档案完整度0至1 |
| 质量与版本 | `metrics_as_of_date` | `DATE` | 累计指标统计截止日 |
| 质量与版本 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 质量与版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 质量与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

`current_institution` 与 `current_institution_ids` 从 `ads_talent_experience` 中该人才确定性排序后的
最后一段、且已解析 `institution_id` 的经历派生。排序依次为：`is_current=1` 优先、开始年份与
准确开始日期降序、结束年份与准确结束日期降序、工作经历优先、`experience_id` 降序。
`is_current` 为 NULL 时不得把结束时间缺失解释为当前在任。`current_institution_ids` 当前保存该
唯一机构 ID；`current_institution` 保存机构展示字段、档案质量以及来源 `experience_id` 和经历
时间，便于追溯。没有可用经历的人才保持 NULL，不从姓名或自由文本猜测机构身份。

`country_location_id/province_location_id/city_location_id/district_location_id` 与
`country_code/country_name/province/city/location_display` 都是当前机构所在地代理字段，不表示已经核验的
人才居住地。仅当 `current_institution_ids` 唯一关联 `ads_institution_profile` 且机构
`location_resolution_status='resolved'` 时写入；展示名称取机构画像当前发布值，
`location_display` 按国家、省州、城市顺序去空、去重后以 ` / ` 连接。未解析机构位置不得使用经历
自由文本兜底，相关字段保持 NULL。四级位置 ID 必须逐值复制机构画像同名字段，不得由名称、代码或
层级关系临时推导；省级或区县级来源不足时对应字段保持 NULL。

姓名治理采用最小双字段隔离：只有取得可追溯确切来源时才能填写`name_zh`；仅由英文名或拼音逆推得到
的结果写入`name_zh_candidate`，并将`name_zh_source`写为`PINYIN_INFERENCE`。未来确切来源可使用
`INSTITUTION_OFFICIAL_PROFILE`、`PERSONAL_OFFICIAL_PAGE`、`AUTHOR_PROVIDED`或`MANUAL_VERIFIED`等明确
类型覆盖来源标识并填写`name_zh`。`name`默认展示字段不自动采用候选名，避免把推测姓名冒充事实；
需要展示候选的客户端必须同时读取`name_zh_candidate`和`name_zh_source`并显式标记“推测”。姓名候选
不得参与人才身份合并、论文署名确认或Author–Inventor对齐。
`name_zh_candidate`使用中文细粒度倒排全文索引，查询采用Doris `MATCH_ANY`、`MATCH_ALL`或
`MATCH_PHRASE`；命中候选名仍不改变其`PINYIN_INFERENCE`推测属性。

`discipline_domains/fields/subfields/topics` 均为对象数组，每项固定含 `id`、`name`（中文）和
`name_en`（英文）；四级中文名称来自 `technology_v2.v_openalex_*_bilingual` 视图。

`ads_talent_profile` 不保存单值“人才类型”。“专家、领军人才、青年人才”等分类必须通过
taxonomy 节点及人才关系表表达；人才计划、奖项或成员身份也通过同一套 taxonomy 节点及关系表表达。
`is_academician` 是高频兼容派生字段：存在当前有效且已核验的
`academy_member` 称谓关系时为 1，已确认不存在时为 0，未完成核验时为 NULL。不得继续增加
`is_fellow`、`is_jieqing`、`is_young_talent` 等布尔列。

2.0.0 从人才主画像删除 `classifications`、`classification_l1_ids`、
`classification_l2_ids`、`classification_l3_ids`、`honor_titles`、`honor_title_ids`、
`talent_plans` 和 `talent_plan_ids`。完整分类、荣誉成员身份、人才计划和奖项通过下述关系表查询；
主画像不再承担可无限增长的称谓集合。

### 4.0.1 人才学术力 MVP 评分

`score_version='talent_academic_mvp_v1'` 只使用固定 400 万篇 MVP core 论文及其
固定 OpenAlex Source Snapshot，不读取 `dwd_author.works_count` 或
`dwd_author.cited_by_count`。基准总体是该版本中至少关联一篇 MVP core 论文的
全部发布人才，其人数写入 `academic_benchmark_talent_count`；前端临时筛选不得改变
标准化总体。

原始指标为：

- `paper_count`：人才的 MVP core 去重论文数。
- `citations_count`：上述论文截至 `metrics_as_of_date` 的非负累计被引之和。
- `h_index`：只在上述 MVP core 论文集内重算的 H 指数。
- `collaborating_expert_count`：在 MVP core 中与该人才合著的去重已发布 MVP 人才数。
- `core_eligible_paper_count`：主发表 Source 成功关联且 `is_core` 非 NULL 的论文数。
- `core_paper_count`：上述论文中 `dwd_source.is_core=true` 的论文数。`is_core`
  只表示 CWTS Core Sources 覆盖，不表示 WoS Core、JCR 分区、影响因子或期刊等级。

#### 标准化公式

`paper_count`、`citations_count`、`h_index` 和 `collaborating_expert_count` 分别在固定基准
总体中转为 0–100 分。对任一指标 `X`，并列值使用平均名次：

```text
average_rank_X(i) = (lowest_rank_X(i) + highest_rank_X(i)) / 2

score_X(i) =
    N = 1 时：100
    N > 1 时：100 * (average_rank_X(i) - 1) / (N - 1)
```

因此得到 `paper_score`、`citation_score`、`h_index_score` 和
`collaboration_score`。相同原始值必须得到相同分数。Core 指标不做人群排名，直接按
可解释比例计算：

```text
core_paper_ratio =
    core_eligible_paper_count = 0 时：NULL
    否则：core_paper_count / core_eligible_paper_count

core_source_score = 100 * core_paper_ratio
```

`is_core=NULL` 表示未知，不得当作 false 进入分母。发布 Pipeline 必须检查固定
`dwd_source` Snapshot 存在 `is_core` 列；旧 DWD Dataset 不允许原地补列或把缺失填为 false。

#### 默认学术力公式

默认权重为论文 0.20、被引 0.30、H 指数 0.30、合作广度 0.15、Core 覆盖 0.05：

```text
academic_capability =
    (0.20 * paper_score
   + 0.30 * citation_score
   + 0.30 * h_index_score
   + 0.15 * collaboration_score
   + 0.05 * core_source_score [仅在非NULL时参与])
    /
    (0.20 + 0.30 + 0.30 + 0.15
   + 0.05 [仅在core_source_score非NULL时参与])
```

`academic_metric_weight_coverage` 保存实际进入默认公式的权重之和，Core 有值时为
`1.0000`，无值时为 `0.9500`。总分保留四位小数并限制在 0–100。
`academic_capability_rank` 按总分降序，同分时依次按 `citation_score DESC`、
`paper_score DESC`、OpenAlex Author ID 升序产生唯一稳定排名。

页面自定义模型只能对上述已标准化的分项分设置非负权重，不得对原始计数直接相加。
用户选择的指标集合为 `S` 时，在查询层即时复算：

```text
custom_academic_capability = sum(w_i * score_i, i in S and score_i is not null)
                           / sum(w_i, i in S and score_i is not null)
```

所有选中指标均为 NULL 或所有权重均为 0 时返回 NULL。自定义权重不改写
`academic_capability`、`score_version` 或固定排名；需要保存的模型配置应另行版本化。

### 4.0.1.1 人才社会影响与人才培养代理分 v1

`social_impact_academic_proxy_v1`覆盖固定100,000人学术力基准总体，定义为：

```text
social_impact_score = academic_capability
social_impact_metric_coverage = academic_metric_weight_coverage
social_impact_as_of_date = metrics_as_of_date
```

该指标性质固定为`ACADEMIC_IMPACT_PROXY`，只表达当前论文证据下的学术影响代理，不表示现实社会贡献、
政策影响、公众传播或经济影响。期刊质量分尚未进入v1；未来接入后必须提升评分版本，按学科和发表年份
标准化，缺失时按可用权重归一，并避免与当前学术力中的CWTS Core来源分重复计算。

`talent_cultivation_teaching_tenure_proxy_v1`只对
`talent_classification_mvp_v5_2026-11-04/leading_talent`当前有效人才计算：

```text
talent_cultivation_score = min(100, 50 + 2.5 * min(higher_education_teaching_years, 20))
```

任教区间只接受`experience_type=2`、`institution_type_id='education'`、机构解析状态为confirmed类、
职位明确属于教职且起始年非空的正式`ads_talent_experience`。结束年非空时使用结束年；只有
`is_current=1`时才延伸到固定截止日2026-11-09。结束时间为空且`is_current`未知时不得推断当前在任。
同一人才重叠或首尾相接的合格区间先求并集，再按包含起止年的日历年计数，避免重复累计。

领军人才没有可计算区间时仍保留基础分50，年限为NULL并标记`BASE_ONLY_UNKNOWN_DURATION`；存在可计算
区间时标记`YEAR_PRECISION`；非领军人才分数、年限、版本和截止日保持NULL，状态标记
`NOT_APPLICABLE`。该指标只衡量经确认高校教职时长代理，不代表指导学生数量、学生发展结果或教学质量。
发布配置、执行和质量验收见
[`docs/talent_social_cultivation_v1.md`](docs/talent_social_cultivation_v1.md)。

### 4.0.2 人才潜力 MVP v1

`talent_potential_mvp_v1` 衡量的是相同主学科、相近科研年限人才中的近期成长信号，不是累计
学术成就、未来成果保证或官方人才认定。它不得使用 `academic_capability`、累计 H 指数或累计
论文/引用总量作为直接分项，避免把学术力换权重后再次包装为“潜力”。完整版本结果保存在
`ads_talent_potential_result`；`ads_talent_profile` 的三个潜力业务字段及三个版本字段只是当前发布
版本的查询投影。

#### 固定输入、观察窗口和比较组

- 输入论文固定为 `talent_ads_mvp_core_v2_stage.talent_core_paper`，对应 Iceberg Snapshot
  `4292018784001736547`；年度指标固定为 `metric_definition_version='mvp_core_4m_v1'`。
- `metrics_as_of_date=2026-09-18`。趋势只使用 2021—2025 五个已经结束的自然年，不使用尚未结束的
  2026 年，也不对 2026 年做年化推测。
- 主 Field 从 `ads_talent_topic_profile` 聚合确定：按人才、Field 汇总 Topic `paper_count` 和
  `citation_count`，依次按 `field_paper_count DESC, field_citation_count DESC, field_id ASC`
  选择唯一 Field。它只服务于本模型比较，不改写人才学科事实。
- `first_paper_year` 是 `ads_talent_yearly_metrics.paper_count>0` 的最小年份；
  `academic_age_years=2025-first_paper_year+1`。
- 科研年限段固定为 `0_4`、`5_9`、`10_14` 和 `15_PLUS`；比较组
  `cohort_id=primary_field_id || ':' || career_stage`。基础合格人数少于 200 的组不发布分数，
  不允许回退到页面临时人群重新排名。

#### 原始指标公式

令完整年份 `t∈{2021,2022,2023,2024,2025}`，`x_t=t-2023`，因此
`Σx_t=0` 且 `Σx_t²=10`。

1. **近期影响力 `recent_impact_raw`，目标权重 0.35。** 对人才近五年每篇论文，以人才的
   `primary_field_id + publication_year` 为固定基准总体，对当前非负 `cited_by_count` 计算平均并列
   百分位：

   ```text
   paper_impact_percentile =
       N = 1 时：100
       N > 1 时：100 * (average_rank(cited_by_count) - 1) / (N - 1)

   recent_impact_raw = AVG(paper_impact_percentile)
   ```

   该值对学科和论文年龄做相对化，但仍受当前引用 Snapshot 覆盖影响，不解释为因果影响力。

2. **产出增长 `output_momentum_raw`，目标权重 0.20。** 缺失年份按已确认的 0 篇处理，使用
   `ln(1+paper_count)` 降低极端值影响，计算五点 OLS 斜率：

   ```text
   output_momentum_raw = Σ[x_t * ln(1 + paper_count_t)] / 10
   ```

3. **引用增长 `citation_momentum_raw`，目标权重 0.25。** `citation_count_t` 表示该人才 MVP
   论文在自然年 t 收到的引用，不是 t 年发表论文截至当前的累计引用：

   ```text
   citation_momentum_raw = Σ[x_t * ln(1 + citation_count_t)] / 10
   ```

4. **学术领导力 `leadership_ratio_raw`，目标权重 0.15。** 在 2023—2025 发表论文中按
   `work_id` 去重；第一作者或通讯作者满足任一条件即计一次：

   ```text
   leadership_ratio_raw =
       count_distinct(work_id where authorship_index=0 OR is_corresponding=true)
       / count_distinct(work_id)
   ```

5. **研究拓展 `topic_expansion_raw`，目标权重 0.05。** 等于 2021—2025 年
   `new_topic_count` 之和。低权重用于表达近期研究边界拓展，不把跨 Topic 本身解释为质量。

#### 分项标准化、综合分和最终潜力分

只有 `primary_field_id` 非空、截至 2025 年科研年限不少于 3 年、近五年论文不少于 5 篇、近五年
至少 3 个活跃发表年份，且近期影响力和领导力可计算的人才进入基础评估总体。每个原始指标均在
固定 `cohort_id` 内按与学术力相同的平均并列排名公式转换为 0—100 分：

```text
component_score_X =
    N = 1 时：100
    N > 1 时：100 * (average_rank_X - 1) / (N - 1)

potential_composite_score =
    (0.35 * recent_impact_score
   + 0.25 * citation_momentum_score
   + 0.20 * output_momentum_score
   + 0.15 * leadership_score
   + 0.05 * topic_expansion_score)
    / potential_metric_weight_coverage
```

MVP v1 的合格行五项均需可用，因此 `potential_metric_weight_coverage=1.0000`；未评估行保存
`0.0000`，且综合分为 NULL。未来版本允许缺项时，必须只对非 NULL 分项重新归一，并发布新的
`model_version`，不得原地改变 v1。

中间综合分再次在同一 `cohort_id` 内转换为平均并列百分位，得到对外分数：

```text
talent_potential =
    N = 1 时：100
    N > 1 时：100 * (average_rank(potential_composite_score) - 1) / (N - 1)
```

`potential_rank` 是同组稳定唯一降序排名；同分依次按 `recent_impact_score DESC`、
`citation_momentum_score DESC`、`talent_id ASC` 裁决。排名只用于稳定排序，不改变并列人才相同的
`talent_potential`。

#### 入选、NULL 语义和推荐理由

```text
is_potential_talent =
    1     当 eligibility_status='ELIGIBLE' 且 talent_potential >= 90
    0     当 eligibility_status='ELIGIBLE' 且 talent_potential < 90
    NULL  当未满足评估条件
```

未评估原因使用稳定代码：`MISSING_PRIMARY_FIELD`、`INSUFFICIENT_CAREER_HISTORY`、
`INSUFFICIENT_RECENT_PAPERS`、`INSUFFICIENT_ACTIVE_YEARS`、
`INSUFFICIENT_METRIC_COVERAGE` 或 `COHORT_TOO_SMALL`。不得把这些状态改写为 0 分或“非潜力人才”。

`potential_reason` 由固定模板生成，包含同组潜力百分位、近期影响力分、引用增长分、近五年论文数、
活跃年份、模型版本和截止日，不使用 LLM 自由生成。结果表为已评估未入选者和未评估者保留简短原因；
主画像仅在 `is_potential_talent=1` 时投影推荐理由，其他行保持 NULL。

### 4.0.3 `ads_talent_potential_result`

一名人才在一个不可变潜力模型版本中一行。逻辑主键为 `talent_id + model_version`；表内同时保存
原始指标、分项标准化分、比较组、覆盖状态、最终结果和来源版本，支持重算、解释和历史版本并存。

| 字段 | Doris 类型 | 含义 |
|---|---|---|
| `talent_id` | `VARCHAR(64) NOT NULL` | North Star统一人才ID |
| `model_version` | `VARCHAR(64) NOT NULL` | 潜力模型不可变版本；MVP固定为`talent_potential_mvp_v1` |
| `metrics_as_of_date` | `DATE NOT NULL` | 模型输入指标截止日 |
| `observation_start_year` | `SMALLINT NOT NULL` | 完整年份窗口起始年，MVP为2021 |
| `observation_end_year` | `SMALLINT NOT NULL` | 完整年份窗口结束年，MVP为2025 |
| `primary_field_id` | `VARCHAR(64)` | 用于比较组的唯一主Field |
| `first_paper_year` | `SMALLINT` | MVP core首次论文年 |
| `academic_age_years` | `SMALLINT` | 截至观察窗口末年的科研年限 |
| `career_stage` | `VARCHAR(16)` | 固定科研年限段 |
| `cohort_id` | `VARCHAR(160)` | 主Field与科研年限段组成的比较组ID |
| `cohort_talent_count` | `BIGINT` | 满足基础评估条件的同组人数；不足200仍记录人数但不发布分数 |
| `recent_5y_paper_count` | `BIGINT NOT NULL` | 观察窗口内论文数 |
| `recent_5y_citation_count` | `BIGINT NOT NULL` | 观察窗口内收到的引用数 |
| `recent_5y_active_year_count` | `TINYINT NOT NULL` | 观察窗口内有论文的年份数 |
| `recent_5y_new_topic_count` | `BIGINT NOT NULL` | 观察窗口内首次进入Topic数 |
| `recent_impact_raw` | `DECIMAL(12,6)` | 论文Field-发表年引用百分位均值 |
| `output_momentum_raw` | `DECIMAL(18,9)` | 对数年度论文数OLS斜率 |
| `citation_momentum_raw` | `DECIMAL(18,9)` | 对数年度收到引用数OLS斜率 |
| `leadership_ratio_raw` | `DECIMAL(12,8)` | 最近3个完整年份第一或通讯作者论文占比 |
| `topic_expansion_raw` | `DECIMAL(18,6)` | 观察窗口首次进入Topic数，用数值类型参与排名 |
| `recent_impact_score` | `DECIMAL(9,6)` | 同组近期影响力平均并列百分位分 |
| `output_momentum_score` | `DECIMAL(9,6)` | 同组产出增长平均并列百分位分 |
| `citation_momentum_score` | `DECIMAL(9,6)` | 同组引用增长平均并列百分位分 |
| `leadership_score` | `DECIMAL(9,6)` | 同组学术领导力平均并列百分位分 |
| `topic_expansion_score` | `DECIMAL(9,6)` | 同组研究拓展平均并列百分位分 |
| `potential_metric_weight_coverage` | `DECIMAL(5,4) NOT NULL` | 实际进入综合分的固定权重和 |
| `potential_composite_score` | `DECIMAL(9,6)` | 分项加权并按可用权重归一的中间分 |
| `talent_potential` | `DECIMAL(10,4)` | 中间综合分在同组内的最终百分位 |
| `potential_rank` | `BIGINT` | 同组稳定唯一排名 |
| `is_potential_talent` | `TINYINT` | 1入选、0已评估未入选、NULL未评估 |
| `eligibility_status` | `VARCHAR(40) NOT NULL` | 合格状态或稳定未评估原因代码 |
| `potential_reason` | `STRING` | 确定性模板解释；结果表保留全部状态解释 |
| `metric_definition_version` | `VARCHAR(64) NOT NULL` | 潜力指标定义版本 |
| `source_metric_definition_version` | `VARCHAR(64) NOT NULL` | 来源年度指标定义版本 |
| `source_core_work_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定MVP core Work Iceberg snapshot ID |
| `data_version` | `BIGINT NOT NULL` | Key级单调发布版本 |
| `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

### 4.0.4 人才分类总体方案与使用流程

ADS 人才分类只使用一套 Taxonomy 模型，不再区分 classification 和 label 两套事实：

```text
ads_talent_taxonomy                  分类体系及不可变发布
        ↓
ads_talent_taxonomy_node             节点、名称、父链及认定规则
        ↓
ads_talent_taxonomy_relation         人才到直接节点的唯一 ADS 关系事实
        ├─ ads_talent_taxonomy_closure  祖先/后代展开加速
        └─ ads_talent_taxonomy_metrics  节点展示聚合（可重建）
```

| 表 | 作用 | 主要写入者 | 典型使用方式 |
|---|---|---|---|
| `ads_talent_taxonomy` | 定义分类体系、类型和不可变 release | Taxonomy 发布 Pipeline | 选择当前已发布版本，区分派生分类、成员身份、计划和奖项 |
| `ads_talent_taxonomy_node` | 保存节点、标准名称、父节点和规则，是唯一称谓字典 | Taxonomy 发布 Pipeline | 渲染筛选树、解析节点名称；平面标签使用无父节点的可选根节点 |
| `ads_talent_taxonomy_relation` | 保存人才到直接节点的唯一 ADS 投影 | 分类计算或 DWD 事实投影 Pipeline | 筛选人才、展示认定来源与状态；只写直接节点，不冗余写祖先节点 |
| `ads_talent_taxonomy_closure` | 保存同一 release 的全部祖先—后代路径 | 从 node 父链确定性生成 | 一次 JOIN 查询父节点整棵子树，禁止人工维护 |
| `ads_talent_taxonomy_metrics` | 保存节点卡片和列表所需的可重建聚合 | 指标聚合 Pipeline | 快速展示人数、机构和主题；不得作为分类事实反向生成 relation |

标准发布顺序为：先创建新的 taxonomy release，再写入全部 node；校验父链无环后生成 closure；
从固定评分规则或 DWD 权威事实生成 relation；最后从 relation 和 closure 重建 metrics。全部校验通过后，
将新 release 标记为 `PUBLISHED`，旧 release 标记为 `SUPERSEDED`。已发布 release 不得原地修改。

读取时先从 `ads_talent_taxonomy` 选定 `PUBLISHED` release。查询某个节点的直接人才只连接 relation；
查询包含子级的完整分类使用 closure 展开；仅展示节点统计时读取 metrics。历史复现必须显式指定
`taxonomy_id + release_id`，不能只按名称或只按 `taxonomy_id` 查询。

#### 人才层次分类 MVP v5 与境外人才分类 MVP v1

当前方案使用两个平级的产品派生 taxonomy。人才层次分类负责学术层次和青年科研梯队；境外人才分类负责
按当前机构所在地归属洲。二者拥有独立的 `taxonomy_id + release_id`，不得把境外地域节点挂到人才层次树中。

```text
taxonomy_id   = talent_classification
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = talent_classification_mvp_v5_2026-11-04

高层次学术人才 high_level_academic_talent
├── 领军人才 leading_talent
└── 专家 expert
青年科研梯队 young_research_echelon
└── 青年人才 young_talent
```

```text
taxonomy_id   = overseas_talent_region
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = overseas_talent_region_mvp_v1_2026-11-04

亚洲人才 asia_talent
欧洲人才 europe_talent
北美洲人才 north_america_talent
南美洲人才 south_america_talent
非洲人才 africa_talent
大洋洲人才 oceania_talent
```

固定基准总体是 `talent_academic_mvp_v1` 已发布且至少关联一篇 MVP core 论文的 100,000 名人才，
统计截止日为 2026-09-18。直接节点分配如下：

| 直接节点 | 规则 | 当前预期人数 | 关系写入要求 |
|---|---|---:|---|
| `leading_talent` | 排名位于固定基准总体前 0.1% | 100 | `is_primary=TRUE` |
| `expert` | 排名大于前 0.1% 边界且不超过前 1% | 900 | `is_primary=TRUE` |
| `young_talent` | MVP 首篇论文位于最近 5 个自然年，且 MVP 全部论文累计被引不少于 10 | 6,918 | `is_primary=FALSE`；可与前两类重叠 |

专家区间严格解释为 `(0.1%, 1%]`，即当前固定 100,000 人总体的 rank 101–1,000；其中
rank 101–200（`(0.1%, 0.2%]`）属于专家。最近 5 个自然年包含统计截止年，计算为
`first_paper_year >= YEAR(metrics_as_of_date) - 4`。`first_paper_year` 取
`ads_talent_yearly_metrics` 中 `paper_count > 0` 的最小年份；“全部论文被引用不少于 10”解释为
人才在同一 MVP 论文全集中的累计 `ads_talent_profile.citations_count >= 10`，不是每篇论文分别达到 10 次。

关系统一使用 `assignment_method='RULE'`、`verified_status='UNVERIFIED'`、
`assignment_version='talent_classification_mvp_v2'`。`evidence` 至少保存评分版本、指标口径版本、
截止日、总分、排名、基准人数、首篇论文年和累计被引。该分类是产品规则结果，不代表官方或人工评审认定。

平级的境外人才分类使用 `ads_talent_profile.country_code <> 'CN'`，并将 `country_location_id` 精确连接
`ads_location` 的 `COUNTRY` 行，以 `continent_code` 映射 `AS/EU/NA/SA/AF/OC` 六个叶节点。当前固定
位置版本为 `location_v1_5_20261103`，六个叶节点人数分别为 3,697、5,413、6,311、130、149、1,156，
合计 16,856。该分类只是“当前机构所在地代理”，不是国籍、公民身份、出生地或族裔判断；国家代码为空的
61,533 人不应被当作中国人才或境外人才。香港、澳门、台湾按位置维度中的非 `CN` 代码归入亚洲节点。
地域关系固定 `is_primary=FALSE`、`assignment_version='talent_overseas_region_mvp_v1'`，证据保存国家代码、
国家位置ID、洲代码、位置版本和人才画像数据版本。

#### 人才获奖学科分类 MVP v2

人才获奖学科分类是与人才层次、境外地域平级的 `AWARD` taxonomy，只消费
`ads_talent_honor_detail.honor_type='award' AND verification_status='verified'`；院士、Fellow和其他成员身份
不得进入获奖判断。分类复用26个 `ads_discipline_field` 标准 Field，不维护第二套学科名称。

```text
taxonomy_id   = talent_award_field
taxonomy_kind = AWARD
release_id    = talent_award_field_mvp_v2_2026-11-04

获奖人才 award_recipient
├── 26个标准Field获奖人才节点（node_id=field_id）
└── 学科暂未识别的获奖人才 unclassified_award_field
未获任何奖项人员 no_award
```

taxonomy 本身已经表达“人才获奖学科分类”，因此不创建冗余 `award_status` 节点。`award_recipient` 与
`no_award` 是两个平级根节点；前者只组织Field子树，后者直接接受未获奖补集关系。

固定人才总体为 `score_version='talent_academic_mvp_v1'` 的100,000人。奖项来源固定为
`talent_honor_structured_mvp_v1_20261101`：70条已核验award事实覆盖13人，全部13人均通过
`talent_potential_mvp_v1.primary_field_id` 归入标准Field；其余99,987人按当前产品口径归入 `no_award`。
`no_award` 的严格数据语义是“固定奖项release中没有已核验award事实”，不是超出当前数据范围的终身未获奖
断言；该限定必须写入 relation evidence 和 metrics feature_summary。

每名基准人才只写一条直接关系并设置 `is_primary=TRUE`：有已核验奖项时写主Field节点，主Field为空时写
`unclassified_award_field`，否则写 `no_award`。不得展开人才完整 `field_ids` 数组，否则一名人才会进入十余个
学科并放大人数。当前Field获奖人才分布为：免疫学与微生物学2、环境科学2，其余物理学与天文学、计算机
科学、医学、材料科学、生物化学/遗传学/分子生物学、神经科学、药理学/毒理学/药剂学、心理学、能源各1。
未命中的标准Field节点保留0人数，为后续奖项数据预留稳定筛选树。

发布 SQL 为
[`sql/doris/ads_talent_award_field_taxonomy_mvp_v2.sql`](sql/doris/ads_talent_award_field_taxonomy_mvp_v2.sql)，
执行、查询和验收见
[`docs/talent_award_field_taxonomy_mvp_v2.md`](docs/talent_award_field_taxonomy_mvp_v2.md)。

#### 人才院士分类与人才会士分类 MVP v1

院士与Fellow是可同时成立的两种学术身份，不放入同一棵互斥荣誉树，而是发布两个与获奖学科平级的
`MEMBERSHIP` taxonomy。奖项记录不参与这两个分类；`honor_type='member'`和未命中院士规则的其他学术
成员身份继续保留在`ads_talent_honor_detail`，不强行归入院士或Fellow。

```text
taxonomy_id = talent_academician
release_id  = talent_academician_mvp_v1_2026-11-05

中国院士 china_academician
外国院士 foreign_academician
无院士称号人才 no_academician
```

```text
taxonomy_id = talent_fellow
release_id  = talent_fellow_mvp_v1_2026-11-05

会士（Fellow） fellow
无会士称号人才 no_fellow
```

taxonomy本身已经分别表达院士和会士分类，因此不创建`academician`、`fellow_status`或统一
`honor_status`包装节点。五个节点全部是`parent_node_id=NULL`、`node_type='ROOT'`、`node_level=1`的可选择
根节点，各自只生成一条`depth=0`自闭包。

院士分类固定使用`verification_status='verified' AND honor_type='academy_member'`：

1. `china_academician`只接收授予机构为`Chinese Academy of Sciences`或
   `Chinese Academy of Engineering`且称号不含`Foreign/外籍`的普通院士。该名称描述两院身份，不表示
   人才国籍，当前74人。
2. `foreign_academician`接收称号明确包含`Foreign/外籍`的外籍院士，或授予机构命中冻结外国/国际科学院
   映射的身份。首版映射包括芬兰科学院、德国国家科学院利奥波第那、印度科学院、美国国家科学院、
   丹麦皇家科学院和世界科学院。分类依据授予机构及称号，不依据人才国籍、姓名或当前所在地，当前16人。
3. 一人可以同时属于中国院士和外国院士，当前重叠1人；中国院士关系Primary优先，外国院士关系仍保留但
   `is_primary=FALSE`。两类院士并集89人，其余99,911人进入`no_academician`。

会士分类固定使用`verification_status='verified' AND honor_type='fellow'`。13条Fellow详情覆盖4人，同一人才
多个Fellow称号聚合为一条`fellow`关系；其余99,996人进入`no_fellow`。会士taxonomy严格二分，每人恰好
一条关系和一条Primary。

固定基准总体均为`score_version='talent_academic_mvp_v1'`的100,000人。正向身份关系使用
`assignment_method='SOURCE'`、`verified_status='VERIFIED'`；`no_academician/no_fellow`补集使用
`assignment_method='RULE'`、`verified_status='UNVERIFIED'`。补集节点只表示固定发布中未观察到对应已核验
身份，不是终身无院士或Fellow称号断言。

院士关系总数为100,001、去重人才100,000、Primary 100,000；会士三项均为100,000。关系证据保存详情数、
授予机构数、最早/最晚可用年份、固定荣誉release、院士机构映射版本和人才画像版本。具体荣誉名称、授予
机构、年份和来源链接仍以`ads_talent_honor_detail`为事实明细，不在分类关系中复制完整列表。

发布 SQL 为
[`sql/doris/ads_talent_academician_fellow_taxonomies_mvp_v1.sql`](sql/doris/ads_talent_academician_fellow_taxonomies_mvp_v1.sql)，
执行与验收见
[`docs/talent_academician_fellow_taxonomies_mvp_v1.md`](docs/talent_academician_fellow_taxonomies_mvp_v1.md)。

##### 院士来源补录、taxonomy v2 与主画像同步

`talent_academician_mvp_v2_2026-11-09`补充只读两院院士名录记录`CAS-3412358`：李亚栋
（`tal_212de193e131482f8da6c9597344112c`）于2011年当选中国科学院院士，来源为中国科学院学部官方
个人页。该事实以独立不可变release
`talent_academician_source_confirmation_v1_20261109`写入`ads_talent_honor_detail`；v1 taxonomy保留历史
关系并标记`SUPERSEDED`，不得原地把`no_academician`改成正向关系。

v2从全部`verification_status='verified' AND honor_type='academy_member'`详情确定性重建关系：中国院士
75人、外国院士16人、两类重叠1人，并集90人，`no_academician`为99,910人；关系总数仍为100,001，
去重人才和Primary均为100,000。李亚栋只进入`china_academician`，关系为当前、Primary、已核验，
`selected_or_elected_year=2011`。

`ads_talent_profile.is_academician`只投影当前`PUBLISHED`院士taxonomy中`is_current=TRUE AND
verified_status='VERIFIED'`的`china_academician/foreign_academician`并集：正向关系写1。`no_academician`
是未核验的固定发布补集，不是确认不存在院士身份，因此继续投影NULL而不是0。发布器必须校验荣誉详情、
taxonomy关系、节点指标和主画像投影完全一致，并在发布前后核对来源文件path、size、mtime与SHA-256。

发布SQL、执行入口和验收说明分别为
[`sql/doris/publish_talent_academician_sync_v2.sql`](sql/doris/publish_talent_academician_sync_v2.sql)、
[`scripts/publish_talent_academician_sync_v2.sh`](scripts/publish_talent_academician_sync_v2.sh)和
[`docs/talent_academician_sync_v2.md`](docs/talent_academician_sync_v2.md)。

#### 人才学科领域分类与科研活跃度分类 MVP v1

两套产品派生taxonomy均固定使用`score_version='talent_academic_mvp_v1'`的100,000人，并要求每名人才在
每个taxonomy中恰好一条直接关系、恰好一条Primary。学科分类只使用唯一主Field；活跃度分类只执行一个
有序`CASE`，所以两套taxonomy内部的直接分类都严格互斥，人数分别可以相加为100,000。

##### 人才学科领域分类

```text
taxonomy_id   = talent_discipline_field
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = talent_discipline_field_mvp_v1_2026-11-05

4个标准Domain根节点（不可直接分配）
└── 26个标准Field叶节点（直接分配）
学科暂未识别人才 unclassified_discipline_field（平级可选根节点）
```

四个Domain为健康科学、社会科学、物理科学、生命科学，直接复用`ads_discipline_domain`；26个Field直接复用
`ads_discipline_field`，节点ID固定为平台`field_id`，不维护第二套学科名称。Domain只提供树形展示与子树人数，
人才不写Domain关系，通过closure从唯一Field关系展开。

主Field固定来自`ads_talent_potential_result.model_version='talent_potential_mvp_v1'`的`primary_field_id`，指标
截止日为2026-09-18。99,998人命中26个标准Field，2人`primary_field_id IS NULL`进入
`unclassified_discipline_field`。四个Domain主Field人数为健康科学17,929、社会科学12,791、物理科学51,493、
生命科学17,785，另有未识别2人，合计100,000。

`ads_talent_profile.field_ids`记录人才全部MVP core论文涉及的Field：当前共1,047,456项、平均每人10.47个，
99,235人涉及多个Field，全部展开会使分类失去主学科区分度并产生约百万关系。因此首版只写唯一
`primary_field_id`；`field_ids`仅用于证据中的数量、一致性校验和未来独立的交叉学科分析。当前所有非空
`primary_field_id`都包含在对应`field_ids`中，差异为0。

每名人才关系固定`is_primary=TRUE`、`assignment_method='RULE'`、`verified_status='UNVERIFIED'`、
`assignment_version='talent_discipline_field_mvp_v1'`。关系证据保存主Field模型版本、截止日、全部Field数量及
人才画像版本，不复制完整`field_ids`数组。

##### 人才科研活跃度分类

```text
taxonomy_id   = talent_research_activity
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = talent_research_activity_mvp_v1_2026-11-05

高度活跃人才 highly_active
持续活跃人才 sustained_active
近期活跃人才 recent_active
近期沉寂人才 recently_inactive
历史活跃人才 historical_active
活跃度未识别人才 activity_unclassified
```

六个节点都是可选择的平级根节点。2026年数据尚不完整，因此禁止用于本发布分类；近三年完整窗口固定为
2023—2025，前置近期窗口为2021—2022。某年`paper_count>0 OR project_count>0`即记一个活跃年。项目数按
`effective_start_year`计入启动年份，只是项目启动关联证据，不表示项目全周期持续活跃或正式项目成员身份。

为降低不同学科发表习惯差异，“高度活跃”不使用全局论文阈值，而是在每个唯一主Field内按2023—2025论文
总数升序，以`CEIL(field_cohort_count*0.75)`位置的论文数作为精确nearest-rank第75分位阈值，并在release内
冻结。阈值范围当前为25至135篇；例如艺术与人文学科25、工程学47、医学51、物理学与天文学135。

有序互斥规则和当前人数为：

| 优先级 | 节点 | 规则 | 人数 |
|---:|---|---|---:|
| 1 | `highly_active` | 2023—2025至少2个活跃年，且论文数达到主Field P75 | 25,502 |
| 2 | `sustained_active` | 近三年至少2个活跃年，未命中高度活跃 | 64,907 |
| 3 | `recent_active` | 近三年恰有1个活跃年 | 6,841 |
| 4 | `recently_inactive` | 2023—2025无活动，2021—2022有活动 | 2,334 |
| 5 | `historical_active` | 2021—2025无活动，2021年前有活动 | 414 |
| 6 | `activity_unclassified` | 没有可用带年份论文或项目启动证据 | 2 |

规则按表中顺序只返回一个节点，六类合计100,000。关系固定`is_primary=TRUE`、
`assignment_method='RULE'`、`verified_status='UNVERIFIED'`、
`assignment_version='talent_research_activity_mvp_v1'`。证据保存窗口、主Field与P75阈值、近三年论文数和项目
启动数、活跃年数、最近论文/项目启动年份及版本。该分类只描述固定数据窗口中的可观察科研活动，不表示
在职、全职科研、退休或真实项目成员状态。

发布 SQL 为
[`sql/doris/ads_talent_discipline_activity_taxonomies_mvp_v1.sql`](sql/doris/ads_talent_discipline_activity_taxonomies_mvp_v1.sql)，
执行与验收见
[`docs/talent_discipline_activity_taxonomies_mvp_v1.md`](docs/talent_discipline_activity_taxonomies_mvp_v1.md)。

#### 人才创新链参与类型 MVP v1

当前MVP数据不能可靠判断基础研究、概念验证、实验室验证、中试验证、工程化、监管与标准化、产业化、
市场规模化等八个创新成熟阶段。论文、项目、授权专利和论文被专利引用都不足以单独证明人才已进入中试、
工程化或产业化。因此首版不发布虚假的八阶段结论，而是创建与人才层次、境外地域和获奖学科平级的
“人才创新链参与类型”派生taxonomy，只描述当前数据中可直接观察的创新活动证据。

```text
taxonomy_id   = talent_innovation_chain_type
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = talent_innovation_chain_type_mvp_v1_2026-11-04

科研创新人才 research_innovation
专利创新人才 patent_innovation
科技关联人才 science_technology_linkage
创新链类型未识别人才 innovation_type_unclassified
```

taxonomy本身已经表达“人才创新链参与类型”，因此不创建包装父节点。四个分类节点均为
`parent_node_id=NULL`、`node_type='ROOT'`、`node_level=1`的可选平级根节点；closure只保存四条
`depth=0`自关系。该结构是平面分类，不把四类解释为先后成熟阶段。

固定总体为`ads_talent_profile.score_version='talent_academic_mvp_v1'`的100,000人。每名人才按照以下优先级
写入且只写入一条当前Primary关系：

1. `research_to_patent_cited_paper_count > 0`：归入`science_technology_linkage`。
2. 否则，`patent_application_count > 0 OR patent_grant_count > 0`：归入`patent_innovation`。
3. 否则，`paper_count > 0 OR project_count > 0`：归入`research_innovation`。
4. 以上均不满足：归入`innovation_type_unclassified`。

该优先级只用于生成互斥主分类，保证四类人数可以相加，不表示成熟度高低。关系固定使用
`assignment_method='RULE'`、`is_primary=TRUE`、`verified_status='UNVERIFIED'`、
`assignment_version='talent_innovation_chain_type_mvp_v1'`；关系ID为
`talent_innovation_chain_type_mvp_v1:{node_id}:{talent_id}`。`evidence`保存论文数、项目数、专利申请数、
授权数、本人论文被本人关联专利引用数、指标版本、覆盖状态、统计日期和人才画像数据版本。

四类的严格语义如下：

| 节点 | 定义和边界 | 当前人数 |
|---|---|---:|
| `research_innovation` | 观察到论文或科研项目，但未观察到专利及科研—专利引用关联 | 93,510 |
| `patent_innovation` | 观察到专利申请或授权，但未观察到科研—专利引用关联；不表示已工程化或产业化 | 5,911 |
| `science_technology_linkage` | 固定范围内至少一篇本人论文被本人关联专利引用；不表示已技术转让或产业化 | 579 |
| `innovation_type_unclassified` | 当前范围内没有前三类可用证据 | 0 |

当前`research_to_patent_metric_version='talent_research_to_patent_citation_mvp_v1'`且覆盖状态为`PARTIAL`，
所以未观察到科技关联不能解释为真实世界中不存在关联。学术指标截止日为2026-09-18，专利指标截止日为
2026-10-06。四类合计100,000人，既不遗漏也不重复。

本分类不能使用`industrial_capability_evidence_status`、专利模拟价值或其他模型分数替代事实证据，也不能把
`patent_grant_count > 0`解释为工程化、把`research_to_patent_cited_paper_count > 0`解释为概念验证。未来只有
接入样机/测试、中试、标准/审批、技术许可/转让、投产和市场采用等专项事实后，才能另建八阶段成熟度
taxonomy，不能在本平面参与类型中原地改变节点语义。

发布 SQL 为
[`sql/doris/ads_talent_innovation_chain_type_mvp_v1.sql`](sql/doris/ads_talent_innovation_chain_type_mvp_v1.sql)，
执行和验收见
[`docs/talent_innovation_chain_type_mvp_v1.md`](docs/talent_innovation_chain_type_mvp_v1.md)。

#### 重点项目承担人才 MVP v2

该分类与人才层次、境外地域、获奖学科和创新链参与类型平级。展示名称按业务需求使用“重点项目承担人才”，
但当前项目人员证据全部来自资助论文作者关系，因此分类的严格数据语义是“真实金额重点项目成果关联代理”，
不是正式项目负责人、项目骨干、经费获得者或承担身份认定。

```text
taxonomy_id   = talent_key_project_engagement
taxonomy_kind = DERIVED_CLASSIFICATION
release_id    = talent_key_project_engagement_mvp_v2_2026-11-05

重点项目承担人才 key_project_talent
无重点项目承担人才 no_key_project_talent
```

taxonomy本身已经表达“重点项目承担人才”，因此不创建`key_project_engagement`包装节点。
`key_project_talent`和`no_key_project_talent`直接作为两个可选择的平级根节点，均为
`parent_node_id=NULL`、`node_type='ROOT'`、`node_level=1`；两个节点互斥，并覆盖固定
`score_version='talent_academic_mvp_v1'`的全部100,000人。重点项目采用以下MVP金额代理规则：

```sql
amount_cny_value_type = 'SOURCE_CONVERTED'
AND amount_cny >= 1000000
```

只使用项目来源金额经固定汇率换算的人民币金额。`SIMULATED_SHENZHEN_MEDIAN_V1`、
`SIMULATED_GLOBAL_SHENZHEN_MEDIAN_V1`和`UNAVAILABLE`全部排除。100万元是产品固定代理阈值，不是官方
重点项目认定标准，也不是人才个人获批、到账或承担金额。

人才至少通过`ads_talent_project`关联一个合格项目时进入`key_project_talent`；否则作为固定总体补集进入
`no_key_project_talent`。当前63,061个项目具有真实换算金额，其中38,367个不少于100万元，33,206个关联
当前MVP人才，共形成199,777条人才—合格项目成果关系。最终叶节点人数为：

| 节点 | 当前人数 | 严格数据语义 |
|---|---:|---|
| `key_project_talent` | 22,467 | 至少署名一个真实换算金额不少于100万元项目资助的MVP论文 |
| `no_key_project_talent` | 77,533 | 固定数据范围内未观察到上述项目成果关联 |

`ads_talent_project`当前7,702,366条关系全部为`funded_output_author`，直接Investigator和负责人关系均为0，
所以不能证明其为项目负责人、正式成员或实际承担者；“无重点项目承担人才”也不能解释为现实世界中从未
承担重点项目。关系统一使用`assignment_method='RULE'`、`is_primary=TRUE`、
`verified_status='UNVERIFIED'`和`assignment_version='talent_key_project_engagement_mvp_v2'`。证据保存阈值、
金额类型、合格项目数、最大真实换算金额、直接/负责人关系数、项目指标版本及截止日。

发布 SQL 为
[`sql/doris/ads_talent_key_project_engagement_mvp_v2.sql`](sql/doris/ads_talent_key_project_engagement_mvp_v2.sql)，
执行和验收见
[`docs/talent_key_project_engagement_mvp_v2.md`](docs/talent_key_project_engagement_mvp_v2.md)。v2验证后，含冗余
包装节点的v1已从在线taxonomy表清理；历史SQL、文档和报告仅保留作审计。

#### 其他称谓和单独标签

`MEMBERSHIP`、`PROGRAM`、`AWARD` 分别投影自 `dwd_author_honor_membership`、
`dwd_author_talent_program`、`dwd_author_award`。DWD 仍是权威事实，ADS relation 只负责检索投影。
无层级的单独标签建成 `parent_node_id=NULL` 的可选根节点，并生成 `depth=0` 自闭包；禁止恢复
旧 classification/label 表形成第二套分类事实。

### 4.1 `ads_talent_taxonomy`

一行代表一套不可变人才 taxonomy 发布。产品派生分类、成员身份、人才计划和奖项共用该发布头，
但 DWD 权威事实仍按各自领域表分开保存。九大类等宏观分类是 taxonomy 节点，不是人才主画像的固定列。
该表用于 release 发现和版本治理，不保存节点或人才关系。发布 Pipeline 写入；业务查询只选择
`publish_status='PUBLISHED'` 的明确 release，并与 node/relation 连接。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 稳定人才分类体系ID |
| Key | `release_id` | `VARCHAR(64) NOT NULL` | 不可变分类体系发布ID |
| 语义 | `taxonomy_kind` | `VARCHAR(32) NOT NULL` | `DERIVED_CLASSIFICATION/MEMBERSHIP/PROGRAM/AWARD` |
| 名称 | `taxonomy_code` | `VARCHAR(64) NOT NULL` | 稳定业务代码 |
| 名称 | `name_zh` | `VARCHAR(256) NOT NULL` | 分类体系中文名 |
| 名称 | `name_en` | `VARCHAR(256)` | 分类体系英文名 |
| 名称 | `description` | `STRING` | 分类范围与用途说明 |
| 发布 | `effective_date` | `DATE` | 生效日期 |
| 发布 | `publish_status` | `VARCHAR(32) NOT NULL` | DRAFT/PUBLISHED/SUPERSEDED |
| 发布 | `root_node_count` | `BIGINT NOT NULL` | 根节点数 |
| 发布 | `node_count` | `BIGINT NOT NULL` | 全部节点数 |
| 发布 | `content_hash` | `VARCHAR(64) NOT NULL` | 发布内容稳定SHA-256 |
| 发布 | `published_at` | `DATETIME(3)` | 发布时间UTC |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`taxonomy_kind` 使用 `DERIVED_CLASSIFICATION / MEMBERSHIP / PROGRAM / AWARD`；新增枚举必须提升 Schema 版本。
`publish_status` 使用 `DRAFT / PUBLISHED / SUPERSEDED`。已发布 release 的节点成员、父子关系和
认定规则不可原地修改；变化必须使用新的 `release_id`。

### 4.2 `ads_talent_taxonomy_node`

一行代表固定 taxonomy release 中的一个标准节点，同时是 ADS 唯一称谓字典。树形分类使用父子关系；
独立称谓可作为 `parent_node_id=NULL` 的根节点，不需要第二套 label dictionary。
该表用于筛选树、标准名称和认定规则展示。发布 Pipeline 在 taxonomy 之后写入；应用不得用名称充当ID，
也不得把节点行解释为人才已经属于该分类。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 分类体系ID |
| Key | `release_id` | `VARCHAR(64) NOT NULL` | 分类体系发布ID |
| Key | `node_id` | `VARCHAR(128) NOT NULL` | 发布内稳定节点ID |
| 节点 | `parent_node_id` | `VARCHAR(128)` | 直接父节点ID；根节点为空 |
| 节点 | `node_code` | `VARCHAR(128) NOT NULL` | 稳定业务代码 |
| 节点 | `node_type` | `VARCHAR(16) NOT NULL` | ROOT/BRANCH/LEAF |
| 节点 | `node_level` | `SMALLINT NOT NULL` | 根节点为1的展示层级 |
| 节点 | `name_zh` | `VARCHAR(256) NOT NULL` | 节点中文名 |
| 节点 | `name_en` | `VARCHAR(256)` | 节点英文名 |
| 节点 | `aliases` | `ARRAY<STRING>` | 别名、简称和旧称 |
| 治理 | `description` | `STRING` | 节点定义和边界 |
| 治理 | `assignment_rule` | `STRING` | 可审计认定规则 |
| 治理 | `issuer_institution_id` | `VARCHAR(64)` | 成员身份、计划或奖项的颁发/所属机构ID |
| 来源 | `source_entity_type` | `VARCHAR(32)` | DWD 来源实体类型；纯派生节点可空 |
| 来源 | `source_entity_id` | `VARCHAR(128)` | DWD 来源实体稳定ID；纯派生节点可空 |
| 治理 | `sort_order` | `BIGINT NOT NULL` | 同父节点稳定展示顺序 |
| 治理 | `is_selectable` | `BOOLEAN NOT NULL` | 是否允许直接分配人才 |
| 治理 | `is_active` | `BOOLEAN NOT NULL` | 本发布中是否有效 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`node_type` 使用 `ROOT / BRANCH / LEAF`。`node_level` 只用于显示和质量校验，不能代替父子关系。
`source_entity_type + source_entity_id` 在具备 DWD 定义实体时必须非空且可追溯；规则派生分类节点可以为空。

### 4.3 `ads_talent_taxonomy_closure`

闭包表预先保存全部祖先—后代路径，使点击父节点后能够直接筛选全部子树人才，不要求在线递归。
每个节点必须包含一条 `ancestor_node_id=descendant_node_id, depth=0` 的自关系。
该表只由 node 的直接父链生成，用于子树展开，不是独立业务事实，也不接受人工增删路径。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 分类体系ID |
| Key | `release_id` | `VARCHAR(64) NOT NULL` | 分类体系发布ID |
| Key | `ancestor_node_id` | `VARCHAR(128) NOT NULL` | 祖先节点ID；包括自身 |
| Key | `descendant_node_id` | `VARCHAR(128) NOT NULL` | 后代节点ID；包括自身 |
| 路径 | `depth` | `SMALLINT NOT NULL` | 两节点距离；自关系为0 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

闭包表必须从同一 release 的直接父链确定性生成。禁止人工分别维护父链和闭包；发布校验必须检查
无环、根节点可达、自关系完整和路径深度一致。

### 4.4 `ads_talent_taxonomy_relation`

一行代表人才与 taxonomy 节点的一条直接关系。分类、成员身份、人才计划和奖项只在该表保存一份 ADS 投影；
具备层级时通过 closure 查询祖先，不重复写多条派生关系。
规则分类 Pipeline 或 DWD 事实投影 Pipeline 写入该表；人才列表和详情页以它为分类事实入口，并通过
node 获取名称、通过 closure 获取祖先语义。删除或重算 metrics 不得影响该表。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_taxonomy_relation_id` | `VARCHAR(128) NOT NULL` | 来源事实或规则结果确定的稳定关系ID |
| 关系 | `talent_id` | `VARCHAR(64) NOT NULL` | 人才平台ID |
| 关系 | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 分类体系ID |
| 关系 | `release_id` | `VARCHAR(64) NOT NULL` | 分类体系发布ID |
| 关系 | `node_id` | `VARCHAR(128) NOT NULL` | 直接 taxonomy 节点ID |
| 有效期 | `effective_date` | `DATE` | 生效日期 |
| 有效期 | `end_date` | `DATE` | 结束日期 |
| 时间 | `selected_or_elected_year` | `SMALLINT` | 入选、当选或获奖年份 |
| 有效期 | `is_current` | `BOOLEAN NOT NULL` | 当前是否有效 |
| 有效期 | `is_primary` | `BOOLEAN NOT NULL` | 是否为同一taxonomy release内的当前主节点 |
| 认定 | `assignment_method` | `VARCHAR(32) NOT NULL` | SOURCE/RULE/MANUAL/MODEL |
| 认定 | `confidence` | `DECIMAL(5,4)` | 认定置信度0至1 |
| 认定 | `verified_status` | `VARCHAR(32) NOT NULL` | UNVERIFIED/VERIFIED/DISPUTED |
| 认定 | `assignment_version` | `VARCHAR(64)` | 规则、人工流程或模型版本 |
| 证据 | `source_fact_type` | `VARCHAR(32)` | 支撑事实类型 |
| 证据 | `source_fact_id` | `VARCHAR(128)` | 支撑事实稳定ID |
| 证据 | `reason` | `STRING` | 认定理由 |
| 证据 | `evidence` | `VARIANT` | 有界证据展示快照 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`talent_id + node_id` 不能作为唯一键，因为同一人可在不同年份重复获得同一奖项或称谓。
`assignment_method` 使用 `SOURCE / RULE / MANUAL / MODEL`。`is_primary` 只在同一人才、同一
`taxonomy_id + release_id` 内解释；发布前必须保证当前关系中最多一条 Primary，不存在“跨全部
taxonomy 的全局唯一人才层次”。未经审核的模型推荐不能写成 `verified_status='VERIFIED'`。

该表是多对多桥表，不是“一名人才一行”：同一人才可在同一 release 关联多个直接 node，也可横跨多套
taxonomy。`taxonomy_id + release_id + node_id` 是关系的版本上下文和可校验连接键；Doris 列式存储只
扫描查询所需列，重复低基数字段也可压缩。不得改成每人一个 node 数组，否则会削弱按节点筛选、关系级
来源/有效期、幂等更新和唯一性校验。若未来证据大字段成为主要存储压力，可在保持本桥表键和语义不变的
前提下，把 `reason/evidence` 拆到按关系ID连接的冷详情表，不能合并多条关系事实。

#### 两个平级 taxonomy 的关系生成规则

`taxonomy_id='talent_classification'`、
`release_id='talent_classification_mvp_v5_2026-11-04'` 按以下规则写入本表：

1. `academic_capability_rank <= CEIL(academic_benchmark_talent_count * 0.001)`：写入
   `node_id='leading_talent'`，即学术力前 0.1% 的领军人才。
2. `academic_capability_rank > CEIL(academic_benchmark_talent_count * 0.001)` 且
   `academic_capability_rank <= CEIL(academic_benchmark_talent_count * 0.01)`：写入
   `node_id='expert'`，即学术力排名区间 `(0.1%, 1%]` 的专家；当前 rank 101–1,000 均命中。
3. `first_paper_year >= YEAR(metrics_as_of_date) - 4` 且 `citations_count >= 10`：写入
   `node_id='young_talent'`。首篇论文年取 MVP 年度表中 `paper_count > 0` 的最小年份，引用数是
   MVP 全部论文累计被引。
4. 青年人才关系独立写入、`is_primary=FALSE`，不得因已存在领军人才或专家关系而排除；前两类关系
   `is_primary=TRUE` 且按当前区间规则互斥。
5. 关系ID固定为
   `talent_classification_mvp_v5:{node_id}:{talent_id}`，重跑同一固定发布不得产生重复关系。

`taxonomy_id='overseas_talent_region'`、
`release_id='overseas_talent_region_mvp_v1_2026-11-04'` 独立写入地域关系：

1. `country_code <> 'CN'` 且国家位置成功解析到六个支持洲代码之一时，按 `continent_code` 写入唯一洲节点。
2. 六个洲节点都是该 taxonomy 的可选根节点，关系 `is_primary=FALSE`；不创建 `overseas_talent` 父节点。
3. 关系ID固定为 `overseas_talent_region_mvp_v1:{node_id}:{talent_id}`。
4. 人才可同时存在于人才层次分类和境外人才分类；Primary 唯一性只在各自 taxonomy release 内检查。

发布 SQL 为
[`sql/doris/ads_talent_taxonomy_split_level_overseas.sql`](sql/doris/ads_talent_taxonomy_split_level_overseas.sql)。
当前人才层次分类写入 7,918 条关系，境外人才分类写入 16,856 条关系。错误嵌套两者的 v4 已从 ADS 在线表
清理；历史规则仍由版本化 SQL、文档和发布报告留档。业务查询必须先按所需 `taxonomy_id` 选择各自的
`PUBLISHED` release。

`taxonomy_id='talent_award_field'`、
`release_id='talent_award_field_mvp_v2_2026-11-04'` 为每名固定基准人才写一条Primary关系：有已核验award
事实且主Field非空时写 `node_id=primary_field_id`；有奖但主Field为空时写
`unclassified_award_field`；其余人才写 `no_award`。获奖关系为 `VERIFIED`，`no_award` 补集关系为
`UNVERIFIED`。关系ID固定为 `talent_award_field_mvp_v2:{node_id}:{talent_id}`。

`taxonomy_id='talent_academician'`允许同一人才同时写入中国院士和外国院士关系，但只允许一条Primary；
无任一正向院士关系时才写`no_academician`。`taxonomy_id='talent_fellow'`为每名基准人才写`fellow`或
`no_fellow`之一。两个taxonomy的Primary唯一性分别校验，不能跨taxonomy互斥。

`taxonomy_id='talent_discipline_field'`只按唯一`primary_field_id`或未识别补集写一条关系，不展开
`field_ids`。`taxonomy_id='talent_research_activity'`按高度活跃到未识别的固定CASE优先级写一条关系。两套
taxonomy都必须校验每名基准人才关系数等于1且Primary数等于1。

`taxonomy_id='talent_innovation_chain_type'`、
`release_id='talent_innovation_chain_type_mvp_v1_2026-11-04'`为每名固定基准人才写一条互斥Primary关系。
判断顺序固定为科研—专利关联、专利成果、科研活动、未识别；不得改变CASE顺序后仍沿用同一release。
四类全部是规则派生的`UNVERIFIED`关系，不能作为官方创新阶段或成果转化认定。

`taxonomy_id='talent_key_project_engagement'`、
`release_id='talent_key_project_engagement_mvp_v2_2026-11-05'`为固定100,000人各写一条根节点Primary关系。
正向节点必须能连接到至少一个`SOURCE_CONVERTED`且`amount_cny>=1000000`的项目，反向节点是固定总体补集；
不得用模拟金额生成正向关系。两类均为金额与成果关联代理产生的`UNVERIFIED`关系。

### 4.5 `ads_talent_taxonomy_metrics`

节点卡片的当前发布统计，一行一个节点。该表是可重建聚合，不是人才分类事实来源。
它由 relation、closure 及相关 ADS 指标表批量重建，供列表计数和节点概览快速读取；任何分类判断都必须
回到 relation，不能依据 metrics 中的展示快照认定单个人才。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 分类体系ID |
| Key | `release_id` | `VARCHAR(64) NOT NULL` | 分类体系发布ID |
| Key | `node_id` | `VARCHAR(128) NOT NULL` | taxonomy 节点ID |
| 计数 | `direct_talent_count` | `BIGINT NOT NULL` | 直接分配到节点的去重人才数 |
| 计数 | `subtree_talent_count` | `BIGINT NOT NULL` | 闭包展开后的子树去重人才数 |
| 计数 | `current_talent_count` | `BIGINT NOT NULL` | 当前有效子树去重人才数 |
| 计数 | `verified_talent_count` | `BIGINT NOT NULL` | 已核验当前子树去重人才数 |
| 计数 | `institution_count` | `BIGINT` | 节点人才关联机构数 |
| 展示快照 | `top_institutions` | `VARIANT` | 有界Top机构展示快照 |
| 展示快照 | `top_topics` | `VARIANT` | 有界Top Topic展示快照 |
| 展示快照 | `representative_talents` | `VARIANT` | 有界代表人才展示快照 |
| 展示快照 | `feature_summary` | `VARIANT` | 有界核心特征快照 |
| 口径与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 统计截止日 |
| 口径与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 聚合口径版本 |
| 口径与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 口径与版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`direct_talent_count` 只统计直接分配到本节点的人才；`subtree_talent_count` 通过 closure 展开后按
人才去重。多个子节点之间可能重叠，因此父节点人数不能简单相加子节点人数。
`talent_classification_mvp_v5` 的两个根分组不接受直接分配，因此 `direct_talent_count=0`；高层次学术人才
子树人数为 1,000，青年科研梯队子树人数为 6,918。三个学术层次叶节点的 `direct_talent_count`、
`subtree_talent_count` 和 `current_talent_count` 分别保持 100、900、6,918。分类关系数只对三个叶节点的
`direct_talent_count` 求和，结果为 7,918。`overseas_talent_region_mvp_v1` 的六个洲节点都是根节点，
`direct/subtree/current` 分别相同，合计 16,856。两个 taxonomy 的人数不可直接相加为去重人才数；跨分类
去重必须按 `talent_id` 查询 relation。

`talent_award_field_mvp_v2` 的两个根节点中，`award_recipient` 子树为13人，`no_award` 为99,987人；
`unclassified_award_field` 为0人。26个Field节点全部生成，即使当前人数为0也不删除；Field节点合计人数
必须等于获奖人才子树人数。

`talent_academician_mvp_v1`三个根节点的`direct/subtree/current`人数分别为中国院士74、外国院士16、
无院士称号99,911；两类院士重叠1人，因此三节点人数不可相加作为总体，关系数为100,001、去重人才为
100,000。`talent_fellow_mvp_v1`两个根节点人数为会士4、无会士称号99,996，合计100,000。正向节点的
`verified_talent_count`等于人数，两个补集节点的`verified_talent_count=0`。

`talent_discipline_field_mvp_v1`的26个Field叶节点直接人数合计99,998，未识别根节点2人；四个Domain的
直接人数为0，子树人数合计99,998。`talent_research_activity_mvp_v1`六个平级根节点的
`direct/subtree/current`人数依次为25,502、64,907、6,841、2,334、414、2，合计100,000。两套分类均为
规则派生，全部节点`verified_talent_count=0`。

`talent_innovation_chain_type_mvp_v1`是四个平级根节点组成的平面taxonomy，因此每个节点的
`direct_talent_count/subtree_talent_count/current_talent_count`相同，依次为科研创新93,510、专利创新5,911、
科技关联579、未识别0，合计100,000。所有关系均为规则派生且未经人工核验，所以
`verified_talent_count=0`。

`talent_key_project_engagement_mvp_v2`只有两个平级根节点，每个节点的
`direct_talent_count/subtree_talent_count/current_talent_count`相同，分别为22,467和77,533，合计100,000。
全部关系未经正式项目角色核验，因此两个节点的`verified_talent_count`均为0。

人数不写入 `ads_talent_taxonomy_node`。node 属于不可变 release 的分类定义，而人数会随关系有效状态、
统计截止日和统计口径变化；混写会迫使计数刷新修改不可变字典，并失去 `direct/subtree/current/verified`
四种口径。节点列表展示时按 `taxonomy_id + release_id + node_id` LEFT JOIN metrics；metrics 缺失表示聚合
尚未生成，不能默认解释为 0。

### 4.6 为什么人才 taxonomy 使用 JOIN，而不是继续扩展宽表

Doris 没有物理外键约束，但完整支持等值 `JOIN`。外键约束负责阻止非法引用；`JOIN` 只是按值
连接数据，两者不是同一能力。人才分类采用“关系表 JOIN 小型节点维表”，原因如下：

1. 人才与分类天然是多对多关系，单个 `level` 列无法表达同一人才同时属于多个分类。
2. 分类树深度和节点数量会变化，固定 `classification_l1/l2/l3` 会把产品配置固化为表结构。
3. 分类名称、别名、父链和认定规则按 release 版本化后，可以复现历史口径。
4. `ads_talent_taxonomy_node` 是小型维表，Doris 可将其作为 Join 的小表；高频节点卡片另由
   `ads_talent_taxonomy_metrics` 预聚合，不需要为避免所有 JOIN 而污染人才主画像。
5. 主画像宽表仍保留姓名和核心指标，分类详情只在需要分类筛选或展示时连接，避免每次 taxonomy
   变化都重写全部人才行和大型 VARIANT/ARRAY 列。

查询一名人才在各 taxonomy 中的当前主分类：

```sql
SELECT
    r.talent_id,
    r.taxonomy_id,
    r.release_id,
    r.node_id AS primary_talent_level_id,
    n.name_zh AS primary_talent_level_name
FROM ads_talent_taxonomy_relation r
JOIN ads_talent_taxonomy_node n
  ON r.taxonomy_id = n.taxonomy_id
 AND r.release_id = n.release_id
 AND r.node_id = n.node_id
WHERE r.is_primary = TRUE
  AND r.is_current = TRUE;
```

查询某父节点整棵子树下的人才：

```sql
SELECT DISTINCT r.talent_id
FROM ads_talent_taxonomy_closure c
JOIN ads_talent_taxonomy_relation r
  ON c.taxonomy_id = r.taxonomy_id
 AND c.release_id = r.release_id
 AND c.descendant_node_id = r.node_id
WHERE c.taxonomy_id = 'talent_classification'
  AND c.release_id = 'talent_classification_mvp_v5_2026-11-04'
  AND c.ancestor_node_id = 'young_research_echelon'
  AND r.is_current = TRUE;
```

由于 Doris 不会强制外键，发布 Pipeline 必须执行以下逻辑约束：taxonomy release、父节点、closure
两端节点、人才关系节点、人才主体和 source fact 的孤儿数均为 0；节点业务键与关系
ID 无重复；当前 Primary 在同一人才和 taxonomy release 内最多一条。生产查询可以使用 INNER JOIN，
但发布验收必须先用 LEFT JOIN 反查孤儿，避免非法关系被 INNER JOIN 静默过滤。

至少执行以下节点孤儿与当前 Primary 唯一性检查，结果都必须为零行：

```sql
SELECT r.taxonomy_id, r.release_id, r.node_id, COUNT(*) AS orphan_count
FROM ads_talent_taxonomy_relation r
LEFT JOIN ads_talent_taxonomy_node n
  ON r.taxonomy_id = n.taxonomy_id
 AND r.release_id = n.release_id
 AND r.node_id = n.node_id
WHERE n.node_id IS NULL
GROUP BY r.taxonomy_id, r.release_id, r.node_id;

SELECT talent_id, taxonomy_id, release_id, COUNT(*) AS primary_count
FROM ads_talent_taxonomy_relation
WHERE is_primary = TRUE AND is_current = TRUE
GROUP BY talent_id, taxonomy_id, release_id
HAVING COUNT(*) > 1;
```

2.0.0 classification/label 表只是历史迁移定义，已被 3.0.0 统一 taxonomy 模型取代。当前部署必须执行
`ads_schema_3_0_0_talent_taxonomy_unification.sql`，不得向旧 classification/label 表发布新数据。

### 4.7 人才公开资料增强与证据（6.32.0；7.0.0候选表边界修订）

本组表服务人才详情页的基础资料、简介、经核验荣誉/经历与媒体报道展开。完整网页文档、候选队列、
不可变发布和历史事实保存在 Iceberg DWD/DWS；ADS 只保存正式产品投影。首版发布标识为
`talent_profile_enrichment_mvp_v1_20261101`，采集证据截止 `2026-11-01`。

`ads_talent_public_enrichment` 的字段契约如下：

| 字段组 | 字段 | 说明 |
|---|---|---|
| Key/身份 | `talent_id, release_id, openalex_author_id, orcid` | 统一人才、发布与外部身份 |
| 展示身份 | `name, name_zh, identity_institution_name, h_index_at_selection` | 采集选择时快照，不替代主画像实时指标 |
| 已核验资料 | `birth_year, web_url, current_title, profile_evidence_as_of_date` | 只投影 `source_confirmed` 断言；未知保持NULL |
| 双语简介 | `talent_bio, talent_bio_en` | 基于多个来源归纳，不复制长段官方文本 |
| 简介治理 | `biography_source_urls, biography_summary_method, biography_summary_version, biography_review_status` | 来源、方法、版本与人工审核状态 |
| 覆盖计数 | `profile_assertion_count, image_candidate_count, biography_evidence_count, honor_candidate_count, experience_candidate_count, media_report_count` | 对应明细条数 |
| 公共 | `data_version, update_time` | 单调版本与UTC生成时间 |

其余正式明细表包含 `release_id`、各自稳定明细 ID、`talent_id`、`openalex_author_id`、
`data_version` 和 `update_time`。专属字段如下：

| 表 | 专属字段 | 语义约束 |
|---|---|---|
| `ads_talent_profile_evidence` | `attribute_code, value_type, value_text, document_id, source_url, evidence_text, evidence_as_of_date, claim_scope, verification_status, verified_at` | 任何出生年、主页、职称和头像展示均可回到原文证据 |
| `ads_talent_biography_evidence` | `document_id, source_url, language, source_material, candidate_type, review_status` | 保存用于归纳简介的短底稿，不保存整页正文 |
| `ads_talent_honor_detail` | `honor_type, organization_name, organization_name_zh, honor_name, honor_name_zh, honor_year, honor_description, honor_reason, source_url, evidence_text, source_candidate_ids, verification_status` | 一项荣誉一行；英文/原名称与中文展示名并存；介绍、年份和理由只在来源明确支持时填写，原文链接必填 |
| `ads_talent_media_report` | `media_article_id, document_id, title, publisher, published_at_raw, published_at, canonical_url, summary_candidate, match_confidence, matched_name_variants, matched_name_language, match_basis_json, verification_status, sentiment_label, sentiment_score, risk_level, topic_codes, topic_names_zh, value_codes, value_names_zh, topic_value_context, topic_value_extraction_method, topic_value_extraction_version` | 人员匹配依据必须可解释；6.35.0写入情感/风险，6.36.0写入话题与价值主题 |

7.0.0 删除 `ads_talent_image_candidate`、`ads_talent_honor_candidate` 和
`ads_talent_experience_candidate`。对应候选数据继续保留在 Iceberg DWD/DWS，不因 ADS 删除而丢失；
经确认的荣誉写入 `ads_talent_honor_detail`，机构已存在且解析状态为 confirmed 的履历才写入
`ads_talent_experience`。机构未进入 `ads_institution_profile` 或仅有弱解析记录的履历继续停留在候选层。

`ads_talent_profile.talent_bio/talent_bio_en` 投影双语简介；`birth_year/web_url/title` 仅从已确认断言
部分更新。`gender` 和 `avatar_url` 不推断、不自动回填。所有简介首版为
`AI_ASSISTED_MULTI_SOURCE_SYNTHESIS + PENDING_REVIEW`，不能解释为机构原文或已人工背书。

媒体补采发布 `talent_media_refresh_mvp_v2_20261101` 不改变表结构：向
`ads_talent_media_report` 写入15人各2条、共30条 `source_confirmed` 报道，标题、摘要和发布日期
完整率均为100%。经数据审核，首批 `talent_profile_enrichment_mvp_v1_20261101` 的15条媒体候选已从
ADS删除；不可变DWD历史保留审计。当前ADS只保留新发布的30条 `source_confirmed` 记录。日期来自
发布者页面的明确日期；摘要为基于原文归纳的短摘要，日期状态与摘要方法保存在
`match_basis_json`。6.35.0使用固定词表和可复算规则评估当前30条报道，并写入单篇情感标签、0至1分数和
初步风险等级；人才聚合结果写入`ads_talent_media_sentiment_assessment`及人才主画像。该评估每人仅2篇
报道，`coverage_status=LIMITED_2_ARTICLES`，不能解释为完整互联网舆情或事实风险结论。

话题与价值观发布`talent_media_topic_value_mvp_v1_20261102`使用固定标准词表处理同一30条报道：
`ads_talent_media_report`保存每篇报道的标准话题/价值主题数组和来源摘要上下文；
`ads_talent_topic_value_summary`按人才和标准项保存去重报道提及次数；
`ads_talent_topic_value_evidence`保存标题、媒体、发布日期、上下文、原文URL、来源类型和表达依据，支持
点击任一话题或价值主题下钻。`PUBLIC_STATEMENT_PARAPHRASE`表示访谈/会议中的公开表述归纳，
`SOURCE_GROUNDED_VALUE_THEME`表示来源支持的价值主题，不得展示为学者逐字引语。

政治展示分发布`talent_political_score_demo_v1_20261102`只用于满足页面占位需求：科学精神子项使用
`min(H-index,100)`，每个价值主题根据公开表述归纳或来源支持主题获得固定90/95分，两篇报道支持时
增加2分；价值观总分为各主题平均值，政治展示分为科学精神和价值观各50%。子项与证据分别保存于
`ads_talent_political_subscore_demo`和`ads_talent_political_subscore_evidence`。该结果明确标记
`SYNTHETIC_DEMO_NOT_POLITICAL_INFERENCE`，不测量意识形态、政治立场、忠诚度、中立性或现实风险。
它也不替代问题匹配模型中历史存在的`political_orientation_score=50`缺省占位口径。

## 5. `ads_talent_experience`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id` | `VARCHAR(64) NOT NULL` | 统一人才ID |
| Key | `experience_id` | `VARCHAR(64) NOT NULL` | 稳定经历ID，上游分配，不能每批重新编号 |
| 时间与类型 | `experience_type` | `TINYINT NOT NULL` | 1教育2工作 |
| 时间与类型 | `start_year` | `SMALLINT` | 起始年份；仅知年份时不伪造具体日期 |
| 时间与类型 | `end_year` | `SMALLINT` | 结束年份 |
| 时间与类型 | `start_date` | `DATE` | 已知的准确起始日期 |
| 时间与类型 | `end_date` | `DATE` | 已知的准确结束日期 |
| 时间与类型 | `is_current` | `TINYINT` | 0已结束1当前NULL未知，结束年为空不代表仍在任 |
| 机构 | `institution_type_id` | `VARCHAR(32)` | 机构类型稳定代码，逻辑关联ads_institution_type；企业为company |
| 机构 | `institution_id` | `VARCHAR(64)` | 统一机构ID |
| 机构 | `institution_name` | `VARCHAR(512)` | 机构展示名 |
| 机构 | `institution_name_en` | `VARCHAR(512)` | 机构英文名 |
| 机构档案质量 | `institution_profile_level` | `VARCHAR(32) NOT NULL` | full/structured/source_id_only/name_only |
| 机构档案质量 | `institution_resolution_status` | `VARCHAR(48) NOT NULL` | 机构身份解析状态 |
| 机构档案质量 | `institution_match_method` | `VARCHAR(64)` | ror_exact/unique_normalized_name/source_id/name_only等 |
| 机构档案质量 | `institution_match_confidence` | `DECIMAL(5,4)` | 机构匹配置信度 |
| 机构档案质量 | `institution_detail_available` | `TINYINT NOT NULL` | 1有结构化详情0仅名称或来源ID候选 |
| 经历内容 | `department` | `VARCHAR(512)` | 院系部门 |
| 经历内容 | `department_en` | `VARCHAR(512)` | 院系部门英文名 |
| 经历内容 | `degree` | `VARCHAR(512)` | 学位或来源教育角色原文 |
| 经历内容 | `degree_en` | `VARCHAR(512)` | 学位英文名 |
| 经历内容 | `major` | `VARCHAR(512)` | 专业 |
| 经历内容 | `major_en` | `VARCHAR(512)` | 专业英文名 |
| 经历内容 | `position` | `VARCHAR(1024)` | 职位或来源工作角色原文 |
| 经历内容 | `position_en` | `VARCHAR(1024)` | 职位英文名 |
| 地理 | `country_code` | `VARCHAR(8)` | 国家代码 |
| 地理 | `country_name` | `VARCHAR(128)` | 国家名称 |
| 地理 | `city` | `VARCHAR(128)` | 城市 |
| 关联与快照 | `project_ids` | `ARRAY<VARCHAR(64)>` | 关联项目ID |
| 关联与快照 | `paper_ids` | `ARRAY<VARCHAR(64)>` | 关联论文内部ID |
| 关联与快照 | `event_ids` | `ARRAY<VARCHAR(64)>` | 关联事件ID |
| 关联与快照 | `honor_ids` | `ARRAY<VARCHAR(64)>` | 关联荣誉ID |
| 关联与快照 | `projects` | `VARIANT` | 代表项目展示快照 |
| 关联与快照 | `papers` | `VARIANT` | 代表论文展示快照 |
| 关联与快照 | `events` | `VARIANT` | 代表事件展示快照 |
| 关联与快照 | `contributions` | `VARIANT` | 贡献描述快照 |
| 关联与快照 | `news` | `VARIANT` | 代表新闻快照 |
| 关联与快照 | `honors` | `VARIANT` | 荣誉展示快照 |
| 评分与版本 | `influence_score` | `DECIMAL(10,4)` | 经历影响力评分 |
| 评分与版本 | `score_version` | `VARCHAR(64)` | 评分版本 |
| 评分与版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 评分与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

`institution_name` 是机构默认展示名：已关联中国 Institution Profile 且 `name_zh` 非空时使用
机构中文名，否则回退来源机构名；`institution_name_en` 保存机构英文名。两者必须复用
`ads_institution_profile` 的已发布名称，不在 Talent Experience 内独立翻译或维护第二套机构名称。
已关联中国机构时，`country_name` 和 `city` 同样复用 `ads_institution_profile` 当前发布的位置
展示值；机构画像再按 `country/province/city_location_id` 复用 `ads_location.name_zh`，无可靠
中文名时才保留原展示值。

## 5.1 `ads_institution_news`

本表为机构新闻查询宽表，一家机构的一条新闻一行。机构范围只从指定重点人才的
`ads_talent_experience` 读取，必须满足 `institution_detail_available=1` 且
`institution_resolution_status LIKE 'confirmed%'`；`dwd_author_experience_candidate` 明确不参与。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `release_id` | `VARCHAR(128) NOT NULL` | 不可变机构新闻发布 ID |
| Key | `institution_news_id` | `VARCHAR(64) NOT NULL` | 机构、发布日期和标题生成的稳定新闻 ID |
| 机构 | `institution_id` | `VARCHAR(64) NOT NULL` | 统一机构 ID |
| 机构 | `institution_name` | `VARCHAR(512) NOT NULL` | 正式经历中的机构展示名 |
| 机构 | `institution_name_en` | `VARCHAR(512)` | 正式经历中的机构英文名 |
| 新闻 | `title` | `VARCHAR(2048) NOT NULL` | 新闻原始标题 |
| 新闻 | `title_zh` | `VARCHAR(2048)` | 已核验中文标题；未翻译时为空 |
| 新闻 | `publisher` | `VARCHAR(512) NOT NULL` | 发布方 |
| 新闻 | `publisher_domain` | `VARCHAR(512) NOT NULL` | 发布方域名 |
| 新闻 | `published_date` | `DATE NOT NULL` | 官网明确发布日期 |
| 新闻 | `published_at_raw` | `VARCHAR(128) NOT NULL` | 官网日期原文 |
| 新闻 | `canonical_url` | `VARCHAR(4096) NOT NULL` | 文章直达链接或官网列表证据链接 |
| 新闻 | `article_url_status` | `VARCHAR(32) NOT NULL` | direct_article/listing_page_only |
| 新闻 | `summary` | `TEXT` | 来源支持的摘要；首批缺失保持空值 |
| 来源质量 | `source_channel` | `VARCHAR(48) NOT NULL` | official_newsroom/official_research_news/official_press_release |
| 来源质量 | `source_language` | `VARCHAR(16) NOT NULL` | 来源语言 |
| 来源质量 | `verification_status` | `VARCHAR(32) NOT NULL` | official_source_confirmed/review_required/rejected |
| 来源质量 | `experience_source_table` | `VARCHAR(64) NOT NULL` | 固定为 ads_talent_experience |
| 版本 | `data_version` | `BIGINT NOT NULL` | Unique Key sequence 版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS 生成时间 UTC |

首批发布 `institution_news_priority_talents_v1_20261102` 覆盖第一梯队 5 名人才正式教育/工作履历中的
21 家已确认机构，每家 3 条、共 63 条官网新闻。直达文章链接无法从官方列表稳定解析时保留列表页，
并以 `article_url_status=listing_page_only` 明确标识；不得把列表页冒充文章直达链接。8.0.0 删除
`talent_ids` 与 `experience_ids`：新闻以机构为主体，消费者按 `institution_id` 连接
`ads_talent_experience` 获取人才与经历，避免在新闻行重复保存多值关系。

## 5.2 `ads_institution_report`

本表为机构画像的外部报告宽表，一份报告一行，逻辑主键为`report_id`。机构名称交互必须使用
`institution_id`连接`ads_institution_profile`，不得使用展示名称反查。首版发布ID为
`institution_reports_perfect_v1_20261106`，覆盖`perfect_data_v1_20261106`的全部26家机构，每家一条
官方机构网站、官方知识库或官方报告页面记录。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key与发布 | `report_id, release_id` | `VARCHAR(64), VARCHAR(96)` | 稳定报告ID与不可变发布ID |
| 外部标识 | `external_report_id, report_number` | `VARCHAR(256)` | 外部报告标识与来源报告编号；来源没有编号时为空 |
| 标题与日期 | `title, title_zh` | `STRING` | 来源题名和中文展示题名 |
| 标题与日期 | `published_date, published_date_precision, publication_year` | `DATE, VARCHAR(32), SMALLINT` | 日期及其精度；年度或财年报告不得把年末日期冒充精确发布日期 |
| 作者 | `authors, corporate_authors` | `ARRAY<STRING>` | 个人作者与团体作者原文；不得把机构相关人才虚构为报告作者 |
| 出版 | `publisher, publication_country` | `STRING, VARCHAR(128)` | 发布机构与出版国家/地区 |
| 来源 | `canonical_url` | `STRING` | 官方报告、官方详情页或官方知识库直达链接 |
| 摘要 | `abstract_en, abstract_zh, abstract_method` | `TEXT, TEXT, VARCHAR(64)` | 双语摘要及摘要方法 |
| 关键词 | `keywords_en, keywords_zh` | `ARRAY<STRING>` | 双语关键词 |
| 文件 | `page_count, file_type, file_path, file_checksum_sha256` | `INT, VARCHAR(32), STRING, VARCHAR(64)` | 页数、文件格式与受控文件信息；未下载时路径和校验和为空 |
| 合同 | `contract_number` | `VARCHAR(256)` | 来源合同号、项目号或报告编号 |
| 正文 | `content, content_scope` | `TEXT, VARCHAR(32)` | 可合法保存的正文或摘要；范围为FULL_TEXT/PARTIAL_TEXT/ABSTRACT_ONLY/METADATA_ONLY |
| 分类 | `resource_type, classification_codes` | `VARCHAR(64), ARRAY<VARCHAR(128)>` | 报告资源类型与来源分类 |
| 文献 | `related_references, related_reference_ids` | `JSON, ARRAY<VARCHAR(64)>` | 相关文献展示快照与平台论文ID |
| 作者详情 | `related_authors, author_institutions` | `JSON` | 作者角色及作者—机构对应关系 |
| 机构关系 | `institution_id, source_institution_name` | `VARCHAR(64), STRING` | 主机构ID及来源名称 |
| 机构关系 | `related_institution_ids` | `ARRAY<VARCHAR(64)>` | 其他已解析相关机构ID；首版至少包含主机构 |
| 人才关系 | `primary_talent_id, author_ids, related_author_ids` | `VARCHAR(64), ARRAY<VARCHAR(64)>` | 有来源署名支持时才关联平台人才 |
| 匹配治理 | `author_match_status, institution_match_status` | `VARCHAR(32)` | 作者匹配与机构匹配状态 |
| 来源治理 | `source_type, verification_status, collected_at` | `VARCHAR(48), VARCHAR(32), DATETIME(3)` | 来源渠道、核验状态和采集时间 |
| 版本 | `data_version, update_time` | `BIGINT, DATETIME(3)` | Unique Key sequence版本与UTC更新时间 |

首版26条均以机构或机构下属正式部门为团体作者，`institution_match_status=CONFIRMED`、
`verification_status=SOURCE_CONFIRMED`。当前没有足够的报告署名证据将记录直接匹配到15名MVP人才，
所以`primary_talent_id`为空、`author_ids=[]`、`author_match_status=UNMATCHED`。这表示作者匹配未知，
不表示相关人才与机构或报告主题无关。

发布必须检查：26家机构覆盖缺失数为0、报告必填字段为空数为0、孤儿机构数为0、重复外部报告ID数为0。
前端从教育/工作经历点击机构后，可用相同`institution_id`分别查询机构画像、相关专家、机构报告与项目。
配置和发布报告位于
[`config/institution_reports_v1.json`](config/institution_reports_v1.json)及
[`reports/institution_reports_perfect_v1_20261106/publication_report.md`](reports/institution_reports_perfect_v1_20261106/publication_report.md)。

## 6. `ads_talent_research_achievement`

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | 人才平台 ID |
| achievement_id | VARCHAR(64) NOT NULL | 跨成果类型稳定 ID；paper 成果当前与 `paper_id` 相同 |
| achievement_type | VARCHAR(32) NOT NULL | `paper`、`patent`、`project`、`award` 等 |
| achievement_rank | INT | 人才内部代表成果顺序 |
| paper_id | VARCHAR(64) | 论文平台 ID，关联 DWD Work |
| patent_id | VARCHAR(64) | 专利平台 ID |
| project_id | VARCHAR(64) | 项目平台 ID，关联 DWD Grant |
| title / title_zh | STRING | 标题及中文标题 |
| year | SMALLINT | 成果年份 |
| venue | VARCHAR(1024) | 期刊、会议或发布机构 |
| author_position | INT | 作者位次，1 为第一作者 |
| author_role | VARCHAR(128) | 作者角色文案 |
| is_corresponding | TINYINT | 是否通讯作者 |
| cited_by_count | BIGINT | 当前论文被引数 |
| topic_ids | ARRAY<VARCHAR(64)> | Topic ID 集合 |
| topics | VARIANT | Topic 展示快照 |
| fulltext_url | VARCHAR(2048) | 全文地址 |
| achievement_score | DECIMAL(10,4) | 代表性评分 |
| achievement_reason | STRING | 入选原因 |
| selection_tags | ARRAY<STRING> | 入选维度 |
| selection_version | VARCHAR(64) | 筛选规则版本 |
| data_version / update_time | BIGINT NOT NULL / DATETIME(3) NOT NULL | 公共版本字段 |

当前 paper 代表成果规则为：每名人才按 `cited_by_count DESC, publication_year DESC NULLS LAST,
OpenAlex work_id ASC` 确定性排序取 Top 10；`work_id` 只作为上游并列裁决字段，不进入 ADS。

## 7. `ads_talent_topic_profile`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与分类 | `talent_id` | `VARCHAR(64) NOT NULL` | 统一人才ID |
| Key 与分类 | `topic_id` | `VARCHAR(64) NOT NULL` | 统一Topic ID |
| Key 与分类 | `topic_name` | `VARCHAR(512)` | Topic英文或原始名称 |
| Key 与分类 | `topic_name_zh` | `VARCHAR(512)` | Topic中文名称 |
| Key 与分类 | `domain_id` | `VARCHAR(64)` | 所属Domain ID |
| Key 与分类 | `field_id` | `VARCHAR(64)` | 所属Field ID |
| Key 与分类 | `subfield_id` | `VARCHAR(64)` | 所属Subfield ID |
| 论文 | `paper_count` | `BIGINT` | 该Topic关联去重论文数 |
| 论文 | `total_paper_count` | `BIGINT` | 同口径人才全部去重论文数 |
| 论文 | `paper_coverage_ratio` | `DECIMAL(9,6)` | Topic论文数除以总论文数，分母0为NULL，跨Topic之和可大于1 |
| 引用 | `citation_count` | `BIGINT` | 该Topic论文累计引用数 |
| 引用 | `total_citation_count` | `BIGINT` | 人才论文累计引用总数，与分子同口径 |
| 引用 | `citation_coverage_ratio` | `DECIMAL(9,6)` | 引用覆盖率，分母0为NULL，跨Topic不可相加解释为概率 |
| 作者角色 | `first_author_count` | `BIGINT` | 该Topic第一作者论文数 |
| 作者角色 | `corresponding_author_count` | `BIGINT` | 该Topic通讯作者论文数 |
| 年份 | `first_year` | `SMALLINT` | 最早论文年 |
| 年份 | `latest_year` | `SMALLINT` | 最近论文年 |
| 年份 | `recent_3y_paper_count` | `BIGINT` | 含as_of_year在内最近3个自然年的论文数 |
| 年份 | `recent_5y_paper_count` | `BIGINT` | 含as_of_year在内最近5个自然年的论文数 |
| 年份 | `as_of_year` | `SMALLINT` | 滚动年度统计基准年 |
| 年份 | `metrics_as_of_date` | `DATE` | 统计截止日 |
| 评分与版本 | `topic_score` | `DECIMAL(10,4)` | 主题研究评分 |
| 评分与版本 | `topic_rank` | `INT` | 该人才内部主题排序 |
| 评分与版本 | `score_version` | `VARCHAR(64)` | 主题评分及统计口径版本 |
| 评分与版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 评分与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

## 8. `ads_talent_collaborator`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id` | `VARCHAR(64) NOT NULL` | 主体人才ID |
| Key | `collaborator_talent_id` | `VARCHAR(64) NOT NULL` | 合作人才ID，不得等于主体ID |
| 合作指标 | `co_paper_count` | `BIGINT` | 合作去重论文数 |
| 合作指标 | `co_project_count` | `BIGINT` | 合作去重项目数 |
| 合作指标 | `co_patent_count` | `BIGINT` | 合作去重专利数 |
| 合作指标 | `first_collaboration_year` | `SMALLINT` | 首次合作年 |
| 合作指标 | `latest_collaboration_year` | `SMALLINT` | 最近合作年 |
| 合作指标 | `collaboration_score` | `DECIMAL(10,4)` | 合作强度评分 |
| 合作指标 | `collaboration_rank` | `INT` | 主体人才内部合作排序 |
| 口径与版本 | `patent_metrics_as_of_date` | `DATE` | 共同专利指标统计截止日 |
| 口径与版本 | `patent_metric_definition_version` | `VARCHAR(64)` | 共同专利指标口径版本 |
| 口径与版本 | `score_version` | `VARCHAR(64)` | 评分版本 |
| 口径与版本 | `metrics_as_of_date` | `DATE` | 统计截止日 |
| 口径与版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 口径与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

## 9. `ads_talent_similarity`

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | 主体人才ID |
| similar_talent_id | VARCHAR(64) NOT NULL | 相似人才ID，不得等于主体ID |
| similarity_type | VARCHAR(32) NOT NULL | research_topic、career_path、technology、industry、combined |
| similarity_topic_id | VARCHAR(64) | `research_topic`使用的主体唯一锚点Topic ID，关联`ads_discipline_topic.topic_id` |
| topic_selection_method | VARCHAR(48) | `HIGHEST_PRIMARY_TOPIC`或`DETERMINISTIC_RANDOM_FALLBACK` |
| topic_primary_paper_count | BIGINT | 主体在锚点Topic上的Primary论文数；随机兜底为0 |
| topic_paper_count | BIGINT | 主体在锚点Topic上的全部关联去重论文数 |
| similar_talent_topic_paper_count | BIGINT | 候选在同一Topic上的全部关联去重论文数 |
| similarity_score | DECIMAL(9,6) | 约定归一化到0至1，原始余弦须ETL转换 |
| similarity_rank | INT | 同一主体和相似类型内的排序 |
| model_version | VARCHAR(64) NOT NULL | 当前模型版本，同类型仅保留一套当前结果 |
| calculated_at | DATETIME(3) NOT NULL | 模型计算时间UTC |
| similarity_reason | VARIANT | 少量解释，不复制候选人才画像 |
| data_version | BIGINT NOT NULL | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| update_time | DATETIME(3) NOT NULL | ADS记录生成时间UTC，ETL显式提供 |

### 9.1 `research_topic_single_anchor_v1`

首版 Topic 相似度一名人才只选择一个锚点 Topic、只执行一次倒排召回并最多发布 Top 3，不计算完整
Topic 向量或第二 Topic 补召回。固定输入为：

| 输入 | Iceberg Snapshot |
|---|---:|
| `talent_ads_mvp_core_v1_stage.talent_core_paper` | `1745748265521826297` |
| `talent_ads_mvp_core_v1_stage.talent_core_topic` | `785816626074646060` |
| `mvp_cn_orcid_v1_228713aa0da9.dwd_work` | `3691395969244640547` |
| `mvp_cn_orcid_v1_228713aa0da9.dwd_work_topic` | `5257814859155844864` |
| `north_star_identity_v1.entity_source_identity` | `1397638178481863711` |

锚点先按人才和 `dwd_work_topic.is_primary=true` 的 Topic 统计去重论文数，再依次按
`primary_paper_count DESC`、2021—2025 五个完整自然年的 Primary 论文数降序、最近 Primary 论文年份
降序、`topic_id ASC` 选择唯一最高 Primary Topic，方法为 `HIGHEST_PRIMARY_TOPIC`。同一论文多个
Primary Topic、`dwd_work.primary_topic_id` 与关系表不一致或 Topic 身份无法映射均为发布阻断异常。

没有有效 Primary Topic、但仍有普通 Topic 证据时，以固定种子
`talent_topic_fallback_v1` 对 `talent_id + topic_id` 计算 `xxhash64`，选择哈希最小的 Topic，方法为
`DETERMINISTIC_RANDOM_FALLBACK`。禁止使用每次重跑会改变结果的真随机。完全没有 Topic 证据的人才
不生成结果，不能虚构 Topic 或写成0分。

设人才 `a` 的唯一锚点为 `T(a)`。候选只要求在 `T(a)` 上有真实论文证据，候选自己的锚点可以不同。
单 Topic 聚焦度及相似度固定为：

```text
evidence_factor(a,t) = 1 - exp(-paper_count(a,t) / 3)

topic_focus(a,t)
  = paper_count(a,t) / total_paper_count(a)
  * evidence_factor(a,t)

similarity_score(a,b)
  = sqrt(topic_focus(a,T(a)) * topic_focus(b,T(a)))
```

分数位于0至1，只表达同一 Topic 上的研究聚焦程度和证据充分度，不表达科研水平、引用影响力或合作
关系。A→B 与 B→A 可以不存在或分数不同。为避免展开全部候选，每个 Topic 先按
`topic_focus DESC, topic_paper_count DESC, talent_id ASC` 保留 Top 4；对主体排除本人后，再按
`similarity_score DESC, candidate_topic_focus DESC, candidate_topic_paper_count DESC,
similar_talent_id ASC` 保留 Top 3。候选不足时保留实际数量，不跨 Topic 补齐。

`research_topic` 行必须填写五个 Topic 业务字段；其他相似类型不得伪造 Topic，保持 NULL。
`similarity_reason` 只保存 `algorithm`、双方 `topic_focus` 的有界解释，不复制姓名、机构或 Topic
名称。当前发布使用 `model_version='research_topic_single_anchor_v1'`、
`data_version=202610150101`、`calculated_at=2026-10-15 02:00:00 UTC`。

### 9.2 `ads_talent_similarity_card` 前端展示视图

前端不直接拼接关系、人才和 Topic 三张表。只读视图 `ads_talent_similarity_card` 以
`similar_talent_id` 关联 `ads_talent_profile`，返回候选姓名、头像、`current_institution` 和机构 ID；
以 `similarity_topic_id` 关联 `ads_discipline_topic`，返回 Topic 中英文名，同时保留分数、排名、选择
方法、模型版本和计算时间。

姓名、头像和机构不物理复制到相似度事实表。姓名或机构更新不触发相似度重算，也不会留下陈旧快照。
“最后机构”统一使用 `ads_talent_profile.current_institution` 的既有口径：它来自人才经历确定性排序后
最后一段已解析机构经历，可能是明确当前机构，不能另造语义含糊的 `last_institution`。没有已解析
机构时展示字段保持 NULL，不从自由文本猜测。

## 10. `ads_talent_yearly_metrics`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id` | `VARCHAR(64) NOT NULL` | 统一人才ID |
| Key | `year` | `SMALLINT NOT NULL` | 指标自然年 |
| 论文与引用 | `paper_count` | `BIGINT` | 当年发表论文数 |
| 论文与引用 | `citation_count` | `BIGINT` | 当年收到的引用数，不是当年发表论文的累计引用 |
| 论文与引用 | `first_author_paper_count` | `BIGINT` | 当年第一作者论文数 |
| 论文与引用 | `corresponding_author_paper_count` | `BIGINT` | 当年通讯作者论文数 |
| 专利 | `patent_application_count` | `BIGINT` | 当年申请专利数 |
| 专利 | `patent_grant_count` | `BIGINT` | 当年授权专利数 |
| 专利 | `patent_metrics_as_of_date` | `DATE` | 年度专利指标统计截止日，不覆盖论文等其他指标截止日 |
| 专利 | `patent_metric_definition_version` | `VARCHAR(64)` | 年度专利指标口径版本 |
| 项目与合作 | `project_count` | `BIGINT` | 当年开始参与的去重项目数 |
| 项目与合作 | `collaborator_count` | `BIGINT` | 当年合作人才去重数 |
| 项目与合作 | `institution_count` | `BIGINT` | 当年任职或学习机构去重数 |
| 项目与合作 | `institution_cooperation_count` | `BIGINT` | 当年合作机构去重数；可按机构类型筛选企业 |
| 项目与合作 | `new_topic_count` | `BIGINT` | 该人才首次出现于当年的Topic数 |
| 评分与版本 | `academic_capability` | `DECIMAL(10,4)` | 2015起三年滚动、学科内百分位的年度学术影响力代理分；2026为YTD |
| 评分与版本 | `industrial_capability` | `DECIMAL(10,4)` | 该年度产业力评分 |
| 评分与版本 | `score_version` | `VARCHAR(64)` | 评分版本 |
| 评分与版本 | `metric_definition_version` | `VARCHAR(64)` | 年度指标口径版本 |
| 评分与版本 | `metrics_as_of_date` | `DATE` | 统计截止日，未结束年份为年内累计 |
| 评分与版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 评分与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

年度论文数采用发布 MVP core 口径。`citation_count` 表示该人才论文在该自然年收到的引用数，
不是该年发表论文截至当前的累计被引数。

9.17.0起，`academic_capability`使用
`score_version='talent_yearly_academic_impact_3y_field_percentile_v1'`填充2015—2026全部已有年度键。
每年使用当年及前两年的指标和；2015、2016分别为一个和两个可用年度的短窗口，2017—2025为完整
三年窗口，2026按`metrics_as_of_date=2026-09-18`解释为YTD。指标执行`ln(1+x)`后，以平均并列排名
计算0—100百分位；原始指标为0时分项固定为0。

有当年Primary Field的人才在`year, field_id`基准内比较，没有当年Primary Field时退回同年全体人才
基准。总分固定为：年度收到引用数50%、论文数20%、第一作者与通讯作者角色次数20%、合作者数5%、
首次出现Topic数5%。第一作者与通讯作者是角色次数，同一论文同时满足两种角色时计两次。

该字段是固定MVP core观察集合内的学术影响力代理分，不是论文质量、完整全球影响力、官方人才认定或
未来成果保证。发布使用Unique Key部分列更新，不得覆盖同一年度行已有论文、引用、项目或专利字段。
完整固定输入、执行和验收见
[`docs/talent_yearly_academic_v1.md`](docs/talent_yearly_academic_v1.md)。

## 11. `ads_talent_institution_cooperation`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与类型 | `talent_id` | `VARCHAR(64) NOT NULL` | 统一人才ID |
| Key 与类型 | `institution_id` | `VARCHAR(64) NOT NULL` | 统一机构ID，名称查机构画像 |
| Key 与类型 | `institution_type_id` | `VARCHAR(32) NOT NULL DEFAULT 'other'` | 机构类型稳定代码，逻辑关联ads_institution_type；企业为company |
| 合作事实 | `project_count` | `BIGINT` | 共同项目去重数 |
| 合作事实 | `paper_count` | `BIGINT` | 共同论文去重数 |
| 合作事实 | `patent_count` | `BIGINT` | 共同专利去重数 |
| 合作事实 | `first_cooperation_year` | `SMALLINT` | 首次合作年 |
| 合作事实 | `latest_cooperation_year` | `SMALLINT` | 最近合作年 |
| 金额 | `cooperation_amount` | `DECIMAL(20,2)` | 合作项目可用人民币金额之和，包含来源换算与明确标记的估算值；无可用金额为空 |
| 金额 | `real_cooperation_amount` | `DECIMAL(20,2)` | `SOURCE_CONVERTED`合作项目金额之和 |
| 金额 | `estimated_cooperation_amount` | `DECIMAL(20,2)` | `SIMULATED_*`或`LLM_ESTIMATED_*`合作项目金额之和 |
| 金额 | `amount_value_type` | `VARCHAR(32)` | `REAL_ONLY/ESTIMATED_ONLY/MIXED/UNAVAILABLE`；无合作项目时为空 |
| 金额 | `amount_known_project_count` | `BIGINT NOT NULL` | 具有可用人民币金额的合作项目数 |
| 金额 | `amount_unavailable_project_count` | `BIGINT NOT NULL` | 缺少人民币金额的合作项目数 |
| 金额 | `currency` | `VARCHAR(3)` | ISO 4217记账币种；同Key所有项目先折算到同币种 |
| 金额 | `fx_rate_date` | `DATE` | 汇率基准日，逐笔历史汇率时不填单一日期 |
| 金额 | `amount_conversion_policy` | `VARCHAR(128)` | 汇率来源和折算策略版本；跨币种不可直接求和 |
| 分类与评分 | `field_ids` | `ARRAY<VARCHAR(64)>` | 涉及Field ID |
| 分类与评分 | `topic_ids` | `ARRAY<VARCHAR(64)>` | 涉及Topic ID |
| 分类与评分 | `evidence_type_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 实际存在的共同论文、共同专利或直接项目证据类型 |
| 分类与评分 | `cooperation_score` | `DECIMAL(10,4) NOT NULL` | 0至100合作分；每条关系必填 |
| 分类与评分 | `cooperation_score_version` | `VARCHAR(64) NOT NULL` | 合作评分公式版本；每条关系必填 |
| 分类与评分 | `cooperation_score_annotation` | `VARIANT` | 合作评分构成快照 |
| 分类与评分 | `top_projects_snapshot` | `VARIANT` | 仅TopN项目展示含起止日期成果链接和经费说明，完整明细查事实层 |
| 版本 | `metrics_as_of_date` | `DATE` | 统计截止日 |
| 版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或调度批次序号；必填，重试保持原值 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，ETL显式提供 |

企业合作查询使用本表并增加 `institution_type_id='company'`，不再维护企业专用关系表。

MVP v1只有满足以下任一条件的关系进入本表：人才与企业出现在同一篇项目资助论文；人才为专利关联
发明人且企业为同一publication的`confirmed` assignee。仅分别出现在同一项目的不同论文不构成合作。

合作分版本`talent_company_cooperation_score_v1`固定为：项目数对数封顶40分、共同论文数对数封顶30分、
共同专利数对数封顶15分、最近十年衰减15分。构成项必须同时写入`cooperation_score_annotation`，不得把
该分解释为合同金额、合作质量认定或主体信用分。

合作金额只汇总`ads_talent_institution_cooperation_project`中的项目金额。来源换算、确定性模拟和未来
明确标记的LLM估算均可进入总额，但必须分别写入真实与估算分项；无合作项目时金额字段为空。当前没有
预算科目和支出流水，`funding_usage_status='NOT_AVAILABLE'`，不得生成资金使用情况。

### 11.1 `ads_talent_institution_cooperation_project`

逻辑主键为`talent_id, institution_id, project_id`。保存项目名称、简介、起止时间、共同论文数、
Topic/Field、来源金额、人民币金额、金额性质和资金使用覆盖状态。项目准入必须有同篇受资助论文证据。

### 11.2 `ads_talent_institution_cooperation_paper`

逻辑主键为`talent_id, institution_id, project_id, paper_id`。每行保存同一受资助论文中的人才作者和
企业署名机构共同证据，以及三个固定输入Snapshot ID。

### 11.3 `ads_talent_institution_cooperation_patent`

逻辑主键为`talent_id, institution_id, patent_id`。机构关系只接受固定Patent Run中的
`resolution_status='confirmed' AND is_confirmed=true`；该关系不声明专利由某个项目产生，也不表示当前权属。

## 12. `ads_talent_patent`

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | 人才平台 ID |
| patent_id | VARCHAR(64) NOT NULL | 专利平台 ID |
| inventor_order | INT | 发明人位次 |
| application_date | DATE | 申请日 |
| publication_date | DATE | 公开日 |
| grant_date | DATE | 授权日 |
| application_kind | VARCHAR(64) | Google Patents 原始大写申请类型代码；与 `ads_patent_profile.application_kind` 一致 |
| patent_state_id | VARCHAR(64) | 法律状态 ID |
| patent_status | VARCHAR(128) | 法律状态展示名 |
| family_id | VARCHAR(128) | 规范化专利族 ID |
| is_granted | TINYINT | 是否授权；不等同于当前有效 |
| cited_paper_count | BIGINT | 专利引用且成功关联到发布 MVP core 的去重论文数；不是专利被引数 |
| data_version / update_time | BIGINT NOT NULL / DATETIME(3) NOT NULL | 公共版本字段 |

`application_kind` 保留 Google Patents 原始大写代码，不在事实字段中写入中文展示值。
当前展示字典为：`A=Patent（专利）`、`U=Utility（实用新型）`、
`F=Design（外观设计）`、`W=PCT（PCT 国际申请，即《专利合作条约》国际申请）`、
`P=Provisional（临时申请）`、`T=Translation（译文文献）`。`V`、`D` 及其他未登记代码的
展示分类为 `unknown（未知）`，但事实字段仍保留原始代码，不将 `V` / `D` 覆盖成
`unknown`。`A` 只解释为 Google 的 `Patent`，不越权翻译为“发明专利”。`kind_code` 是各司法辖区的
文献种类/阶段代码，不得写入 `application_kind`。

## 13. `ads_talent_patent_cited_paper`

该表支持由 `patent_id` 查询其引用论文，也支持由 `paper_id` 反查引用它的专利。

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | 与该专利建立可靠关系的人才平台 ID |
| patent_id | VARCHAR(64) NOT NULL | 专利平台 ID |
| paper_id | VARCHAR(64) NOT NULL | 论文平台 ID，关联 DWD Work |
| paper_title | STRING | 论文原始或英文标题快照 |
| paper_title_zh | STRING | 论文中文标题快照 |
| paper_year | SMALLINT | 发布年份 |
| evidence_sources | ARRAY<STRING> | RoS、PQR、Google NPL 等去重证据来源 |
| is_paper_authored_by_talent | TINYINT | 被引论文是否由该人才署名；0否1是NULL未计算 |
| authorship_evidence_status | VARCHAR(32) | `MATCHED`或`NOT_MATCHED_IN_FIXED_SCOPE`；NULL表示未计算 |
| data_version | BIGINT NOT NULL | Key 级版本 |
| update_time | DATETIME(3) NOT NULL | UTC 生成时间 |

`is_paper_authored_by_talent=1` 必须由同一固定 MVP core Snapshot 的完整 Authorship 事实确认，
不得通过姓名相等推断。该标记只表示人才与被引论文之间存在署名关系，同时人才通过固定
Author–Inventor/Patent 关系关联该专利；它不是许可、转让、产品化或收入事实。

### 13.0.1 `ads_talent_research_to_patent_metrics`

一名人才一个不可变指标版本一行。首版固定
`metric_version='talent_research_to_patent_citation_mvp_v1'`，逻辑主键为
`talent_id + metric_version`。

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | North Star统一人才ID |
| metric_version | VARCHAR(64) NOT NULL | 不可变指标版本 |
| research_to_patent_cited_paper_count | BIGINT NOT NULL | 本人关联专利引用的本人去重MVP core论文数；分子 |
| total_paper_count | BIGINT NOT NULL | 同一固定MVP core范围内本人去重论文总数；分母 |
| research_to_patent_citation_rate | DECIMAL(12,8) | 分子除以分母；分母为0时NULL，否则范围0至1 |
| matched_patent_count | BIGINT NOT NULL | 至少引用一篇本人论文的本人关联去重Patent publication数 |
| matched_relation_count | BIGINT NOT NULL | 去重人才—论文—Patent publication证据关系数 |
| coverage_status | VARCHAR(32) NOT NULL | 当前为PARTIAL；分母不可用时NOT_AVAILABLE |
| source_core_work_snapshot_id | VARCHAR(128) NOT NULL | 固定400万MVP core Work Snapshot ID |
| source_patent_run_id | VARCHAR(64) NOT NULL | 固定Patent MVP发布Run ID |
| metrics_as_of_date | DATE NOT NULL | 专利指标统计截止日 |
| data_version / update_time | BIGINT NOT NULL / DATETIME(3) NOT NULL | 公共版本字段 |

确定性公式：

```text
research_to_patent_cited_paper_count =
    count(distinct paper_id)
    where talent is an author of paper_id
      and talent is reliably linked to patent_id
      and patent_id cites paper_id

research_to_patent_citation_rate =
    research_to_patent_cited_paper_count / total_paper_count
```

分子按 `talent_id + paper_id` 去重；同一论文被多件本人关联专利引用只计一次。完整审计关系查询
`ads_talent_patent_cited_paper` 中 `is_paper_authored_by_talent=1` 的行。首版不做平滑、百分位或
0–100归一化；画像中的四个同名前缀字段只是当前版本投影。由于专利、Author–Inventor 与NPL解析
均非全球完整覆盖，当前有论文分母的人才统一标记 `PARTIAL`，不得把该比例称为商业成果转化率。

### 13.0.2 `ads_talent_observed_citation_metrics`

一名人才一个不可变指标版本一行。首版固定
`metric_version='talent_observed_non_self_citation_mvp_v1'`，逻辑主键为
`talent_id + metric_version`。该表只统计当前MVP已经物化、且指向人才MVP core论文的引用边，不能解释为
OpenAlex或全球文献的完整他引率。

| 字段 | 类型 | 说明 |
|---|---|---|
| talent_id | VARCHAR(64) NOT NULL | North Star统一人才ID |
| metric_version | VARCHAR(64) NOT NULL | 不可变指标版本 |
| observed_citation_count | BIGINT NOT NULL | 当前MVP已物化引用边中指向本人MVP core论文的引用边数 |
| classifiable_citation_count | BIGINT NOT NULL | 能够判定本人自引或他引的引用边数 |
| self_citation_count | BIGINT NOT NULL | 引用方作者包含该人才本人的引用边数 |
| non_self_citation_count | BIGINT NOT NULL | 引用方作者完整且不包含该人才本人的引用边数 |
| unclassified_citation_count | BIGINT NOT NULL | 引用方署名缺失或存在空Author ID且未命中本人的引用边数 |
| observed_cited_paper_count | BIGINT NOT NULL | 至少收到一条已观察引用边的本人去重MVP core论文数 |
| observed_non_self_citation_rate | DECIMAL(12,8) | 他引数除以可判定引用数；分母为0时NULL |
| coverage_status | VARCHAR(32) NOT NULL | PARTIAL/NOT_CLASSIFIABLE/NOT_AVAILABLE |
| citation_scope | VARCHAR(64) NOT NULL | 固定`MVP_SELECTED_CITING_WORK_TO_MVP_CORE` |
| source_core_work_snapshot_id | VARCHAR(128) NOT NULL | 固定400万MVP core Work Snapshot ID |
| source_reference_snapshot_id | VARCHAR(128) NOT NULL | 固定MVP引用边Iceberg Snapshot ID |
| source_authorship_snapshot_id | VARCHAR(128) NOT NULL | 固定MVP论文署名Iceberg Snapshot ID |
| metrics_as_of_date | DATE NOT NULL | 指标统计截止日 |
| data_version / update_time | BIGINT NOT NULL / DATETIME(3) NOT NULL | 公共版本字段 |

引用边按`talent_id + citing_work_id + cited_work_id`去重。引用方作者包含该人才时记本人自引；引用方
署名存在、全部Author ID非空且不包含该人才时记他引；其余记不可判定。确定性恒等式与公式为：

```text
classifiable_citation_count = self_citation_count + non_self_citation_count

observed_citation_count =
    classifiable_citation_count + unclassified_citation_count

observed_non_self_citation_rate =
    non_self_citation_count / classifiable_citation_count
```

`classifiable_citation_count=0`时比例必须为NULL。当前引用边只以MVP selected Work为引用方，因此有可
判定结果也统一标记`PARTIAL`；观察到引用但均不可判定时为`NOT_CLASSIFIABLE`，未观察到引用时为
`NOT_AVAILABLE`。画像中的七个`observed_*`字段只是当前版本便利投影；版本比较、不可判定计数、范围和
Snapshot追溯必须读取本表。

## 13.1 `ads_paper_profile`

发布 MVP core 的论文主体表，一篇论文一行。只发布固定的 4,000,000 篇 core，不把 1,000,000
篇上下文论文带入 ADS。`paper_id` 复用公共 identity bridge 中既有 `wrk_<uuid32>` 值；前缀是
持久 ID 协议，不改变 ADS 使用 `paper` 命名的规则。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份 | `paper_id` | `VARCHAR(64) NOT NULL` | 平台统一论文ID；保持既有wrk_身份值 |
| 身份 | `openalex_work_id` | `VARCHAR(64) NOT NULL` | OpenAlex Work ID |
| 身份 | `doi` | `VARCHAR(512)` | 规范化DOI |
| 标题 | `title` | `STRING NOT NULL` | 首选展示标题，确定性兜底到OpenAlex Work ID |
| 标题 | `title_zh` | `STRING` | 明确中文标题，不自动翻译 |
| 标题 | `title_en` | `STRING` | 明确英文标题 |
| 标题 | `title_original` | `STRING` | 来源原始标题 |
| 摘要 | `abstract_zh` | `STRING` | 仅来源明确标记为中文的摘要；不自动翻译 |
| 摘要 | `abstract_en` | `STRING` | 仅来源明确标记为英文的摘要；不自动翻译 |
| 摘要 | `abstract_original` | `STRING` | OpenAlex来源倒排索引确定性重建的原始摘要 |
| 发布 | `publication_date` | `DATE` | 发布日期 |
| 发布 | `publication_year` | `SMALLINT NOT NULL` | 发布年份 |
| 发布 | `paper_type` | `VARCHAR(64)` | OpenAlex论文类型 |
| 发布 | `language` | `VARCHAR(32)` | 来源语言代码 |
| 发布 | `primary_source_id` | `VARCHAR(64)` | OpenAlex Primary Source ID |
| 发布来源 | `primary_source_name` | `VARCHAR(1024)` | 固定Source Snapshot中的原始优先名称；依次取原始、英文、中文名称 |
| 发布来源 | `primary_source_name_zh` | `VARCHAR(1024)` | 来源明确提供的中文名称；不自动翻译 |
| 发布来源 | `primary_source_type` | `VARCHAR(64)` | OpenAlex来源类型，如journal/conference/repository |
| 发布来源 | `primary_source_issn_l` | `VARCHAR(64)` | Primary Source的ISSN-L |
| 发布来源 | `primary_source_publisher` | `VARCHAR(1024)` | 来源明确提供的Publisher名称；不以Host Organization冒充 |
| 发布来源 | `primary_source_is_core` | `TINYINT` | CWTS Core Sources标记；NULL表示状态未知，不等于JCR、影响因子或期刊等级 |
| 学科 | `primary_topic_id` | `VARCHAR(64)` | 平台统一Primary Topic ID |
| 学科 | `openalex_primary_topic_id` | `VARCHAR(64)` | OpenAlex Primary Topic ID |
| 学科 | `topic_ids` | `ARRAY<VARCHAR(64)>` | 论文关联的平台Topic ID去重集合 |
| 指标 | `cited_by_count` | `BIGINT` | 当前被引次数 |
| 指标 | `fwci` | `DECIMAL(14,6)` | 论文FWCI |
| 指标 | `author_count` | `BIGINT NOT NULL` | DWD署名行数 |
| 指标 | `institution_count` | `BIGINT NOT NULL` | DWD署名关联去重机构数 |
| 获取与状态 | `is_open_access` | `TINYINT` | 是否开放获取 |
| 获取与状态 | `open_access_status` | `VARCHAR(32)` | 开放获取类型 |
| 获取与状态 | `open_access_url` | `STRING` | 开放获取URL |
| 获取与状态 | `landing_page_url` | `STRING` | 落地页URL |
| 获取与状态 | `pdf_url` | `STRING` | PDF URL |
| 获取与状态 | `is_retracted` | `TINYINT` | 是否撤稿 |
| 获取与状态 | `is_paratext` | `TINYINT` | 是否为paratext |
| 卷期页 | `volume` | `VARCHAR(128)` | 卷 |
| 卷期页 | `issue` | `VARCHAR(128)` | 期 |
| 卷期页 | `first_page` | `VARCHAR(128)` | 起始页 |
| 卷期页 | `last_page` | `VARCHAR(128)` | 结束页 |
| 口径与版本 | `data_sources` | `ARRAY<STRING> NOT NULL` | 数据来源 |
| 口径与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标数据截止日 |
| 口径与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 指标口径版本 |
| 口径与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 口径与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS生成时间UTC |

`primary_topic_id` 和 `topic_ids` 使用平台 Topic ID，可关联 `ads_discipline_topic`；OpenAlex ID
只保留在 `openalex_primary_topic_id`。标题按中文、英文、原始标题、展示名、OpenAlex Work ID
依次确定性兜底，保证 `title` 非空；该顺序不表示自动翻译。`title`作为展示与全文检索字段，发布时
必须解码HTML字符实体、移除HTML/XML/MathML标签、隐藏脚本/样式内容和非法控制字符，并归一连续空白；
标签内的可见文字、正常多语言Unicode字符及数学符号必须保留。清洗后为空时回退到OpenAlex Work ID；
`title_original`继续保留来源原文用于溯源，不执行上述展示清洗。

六个`primary_source_*`便利字段只从固定`dwd_source` Snapshot按`primary_source_id=source_id`左连接
投影，不改变论文粒度。名称、中文名、类型、ISSN-L、Publisher和Core状态缺失时保持`NULL`；其中
`primary_source_publisher`不得用Host Organization兜底，`primary_source_is_core`只表示CWTS Core
Sources覆盖，不表示JCR分区、影响因子或期刊等级。

摘要只从固定 MVP core 选择范围对应的 `dwd_work_abstract` 稀疏扩展表发布。没有可用来源摘要时三个
摘要字段均为 `NULL`；不从标题生成摘要，不自动翻译，也不让 ADS 发布程序直接读取原始 Snapshot。

`title`使用`idx_paper_profile_title_multilingual`倒排全文索引。索引固定使用ICU多语言分词器，支持中文、
英文、日文及其他Unicode文字，启用小写归一、空停用词表、短语位置和V3字典压缩。前台全文搜索必须将
带显式字段的已转义DSL作为参数传入`SEARCH(:title_search_dsl)`，例如单词查询传`title:quantum`、多词
任一命中传`title:ANY(quantum computing)`；不得继续使用`LIKE '%关键词%'`并假定倒排索引能够加速。
调用方必须按SEARCH DSL规则转义用户输入，禁止把未转义输入直接拼接进SQL或DSL。`ignore_above`只约束
不分词字符串索引，本分词索引不设置该属性。迁移显式执行`BUILD INDEX`，保证迁移前已经发布的固定
4,000,000篇论文进入索引。

已有环境执行：

```bash
./scripts/compose.sh exec -T doris-fe bash -lc \
  'MYSQL_PWD="$DORIS_PASSWORD" mysql --protocol=TCP -h127.0.0.1 -P9030 -uroot --show-warnings' \
  < sql/doris/ads_schema_9_24_1_paper_title_multilingual_search_index.sql
```

前台参数化查询示例：

```sql
SELECT paper_id, title, publication_year
FROM ads_paper_profile
WHERE SEARCH(:title_search_dsl)
ORDER BY publication_year DESC, paper_id
LIMIT :result_limit;
```

## 13.2 `ads_patent_profile`

MVP Google Patents publication 主体表，一件公开文献一行，不按专利族折叠。平台 ID 使用
`pat_<uuid32>` 并通过公共 identity bridge 映射；本次保留既有 70,496 个 ID，为其余来源
publication 分配新 ID。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份 | `patent_id` | `VARCHAR(64) NOT NULL` | 平台统一专利publication ID |
| 身份 | `google_patent_publication_id` | `VARCHAR(128) NOT NULL` | Google Patents来源publication_id |
| 身份 | `publication_number` | `VARCHAR(128)` | 专利公开号 |
| 身份 | `application_number` | `VARCHAR(128)` | 专利申请号 |
| 身份 | `pct_number` | `VARCHAR(128)` | PCT号 |
| 身份 | `family_id` | `VARCHAR(128)` | Google专利族ID，带google命名空间 |
| 分类 | `jurisdiction_code` | `VARCHAR(16)` | 司法辖区/国家代码 |
| 分类 | `kind_code` | `VARCHAR(32)` | 文献种类代码 |
| 分类 | `application_kind` | `VARCHAR(64)` | 申请类型 |
| 标题与摘要 | `title` | `STRING NOT NULL` | 首选展示标题，确定性兜底到来源ID |
| 标题与摘要 | `title_zh` | `STRING` | 来源明确标记为中文的标题 |
| 标题与摘要 | `title_en` | `STRING` | 来源明确标记为英文的标题 |
| 标题与摘要 | `title_original` | `STRING` | 来源原始标题 |
| 标题与摘要 | `abstract_zh` | `STRING` | 来源明确标记为中文的摘要 |
| 标题与摘要 | `abstract_en` | `STRING` | 来源明确标记为英文的摘要 |
| 标题与摘要 | `abstract_original` | `STRING` | 来源原始摘要 |
| 标题与摘要 | `language` | `VARCHAR(32)` | 来源标题语言代码 |
| 日期 | `priority_date` | `DATE` | 优先权日 |
| 日期 | `filing_date` | `DATE` | 申请日 |
| 日期 | `publication_date` | `DATE NOT NULL` | 公开日 |
| 日期 | `grant_date` | `DATE` | 授权日 |
| 日期 | `application_year` | `SMALLINT` | 申请年份 |
| 日期 | `publication_year` | `SMALLINT` | 公开年份 |
| 日期 | `grant_year` | `SMALLINT` | 授权年份 |
| 日期 | `is_granted` | `TINYINT NOT NULL` | grant_date非空为1；不表示当前有效 |
| 当事人 | `inventors` | `VARIANT` | 来源发明人对象数组，含name/country_code |
| 当事人 | `inventor_count` | `INT NOT NULL` | 来源发明人数 |
| 当事人 | `assignees` | `VARIANT` | 来源权利人对象数组，含name/country_code |
| 当事人 | `assignee_count` | `INT NOT NULL` | 来源权利人数 |
| 分类号 | `ipc_codes` | `ARRAY<STRING>` | IPC代码数组 |
| 分类号 | `cpc_codes` | `ARRAY<STRING>` | CPC代码数组 |
| 分类号 | `primary_ipc_code` | `VARCHAR(64)` | 来源first标记的首个IPC代码 |
| 分类号 | `primary_cpc_code` | `VARCHAR(64)` | 来源first标记的首个CPC代码 |
| 分类号 | `ipc_classifications` | `VARIANT` | IPC完整对象数组 |
| 分类号 | `cpc_classifications` | `VARIANT` | CPC完整对象数组 |
| 关系指标 | `linked_talent_count` | `BIGINT NOT NULL` | 可靠关联的MVP人才数 |
| 关系指标 | `linked_institution_count` | `BIGINT NOT NULL` | 可靠关联的MVP机构数 |
| 关系指标 | `cited_paper_count` | `BIGINT NOT NULL` | 引用且成功关联到发布MVP core的去重论文数 |
| 来源与版本 | `source_dataset` | `VARCHAR(128)` | Google来源数据集 |
| 来源与版本 | `source_batch` | `VARCHAR(128)` | Google来源批次 |
| 来源与版本 | `data_sources` | `ARRAY<STRING> NOT NULL` | 数据来源 |
| 来源与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标数据截止日 |
| 来源与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 指标口径版本 |
| 来源与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 来源与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS生成时间UTC |

`is_granted` 仅由 `grant_date IS NOT NULL` 决定，不表示专利当前有效。`cited_paper_count` 只统计
成功关联到发布 MVP core 的去重论文，与 `ads_patent_cited_paper` 按专利聚合严格一致。

## 13.3 `ads_patent_cited_paper`

全局专利—论文关系，不要求专利先与 MVP 人才关联；支持由专利查引用论文以及由论文反查引用
它的专利。论文端仍严格限定发布 MVP core。

| 字段 | 类型 | 说明 |
|---|---|---|
| patent_id | VARCHAR(64) NOT NULL | 关联 `ads_patent_profile` |
| paper_id | VARCHAR(64) NOT NULL | 关联 `ads_paper_profile` |
| patent_title / paper_title | STRING NOT NULL | 发布时标题快照 |
| paper_title_zh | STRING | 论文中文标题快照 |
| paper_year | SMALLINT NOT NULL | 论文发布年份 |
| evidence_count | BIGINT NOT NULL | 上游去重证据数 |
| evidence_sources | ARRAY<STRING> NOT NULL | RoS、PQR、Google NPL 等证据来源 |
| match_methods | ARRAY<STRING> NOT NULL | NPL 到论文的匹配方法 |
| data_version / update_time | BIGINT NOT NULL / DATETIME(3) NOT NULL | 公共版本字段 |

`ads_talent_patent_cited_paper` 是带人才语境的三元关系；本表是去掉人才维度后的全局二元关系，
两者不可互相替代。前者所有 `(patent_id, paper_id)` 必须能在本表命中。

## 14. `ads_institution_type`

平台机构类型维表。类型 ID 使用稳定英文代码；当前初始化 `education`、`healthcare`、
`company`、`archive`、`nonprofit`、`government`、`facility`、`other` 八类。

| 字段 | 类型 | 说明 |
|---|---|---|
| institution_type_id | VARCHAR(32) NOT NULL | 稳定类型代码 |
| name / name_zh / name_en / name_original | VARCHAR(128) | 默认、中文、英文及来源原名 |
| openalex_id | VARCHAR(255) | OpenAlex 类型 URL；便利映射，不是平台主键 |
| description | STRING | 类型说明 |
| sort_order | SMALLINT NOT NULL DEFAULT 0 | 展示顺序 |
| is_active | BOOLEAN NOT NULL DEFAULT 1 | 是否启用 |
| data_version | BIGINT NOT NULL | Key 级版本 |
| update_time | DATETIME(3) NOT NULL | UTC 生成时间 |

## 15. `ads_institution_profile`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与类型 | `institution_id` | `VARCHAR(64) NOT NULL` | 机构统一ID |
| Key 与类型 | `institution_type_id` | `VARCHAR(32) NOT NULL` | 机构类型ID，逻辑关联ads_institution_type |
| 名称 | `name` | `STRING NOT NULL` | 机构默认名称 |
| 名称 | `name_zh` | `STRING` | 机构中文名称 |
| 名称 | `name_en` | `STRING` | 机构英文名称 |
| 名称 | `name_original` | `STRING` | 机构原始名称 |
| 名称 | `acronyms` | `ARRAY<STRING>` | 机构缩写列表 |
| 名称 | `aliases` | `ARRAY<STRING>` | 机构别名列表 |
| 名称 | `description` | `STRING` | 机构简介 |
| 来源映射 | `openalex_id` | `VARCHAR(64)` | OpenAlex机构ID |
| 来源映射 | `ror_id` | `VARCHAR(64)` | ROR机构ID |
| 来源映射 | `wikidata_id` | `VARCHAR(64)` | Wikidata ID |
| 来源映射 | `data_sources` | `ARRAY<STRING>` | 数据来源列表 |
| 档案治理 | `profile_level` | `VARCHAR(32) NOT NULL` | full/structured/source_id_only/name_only |
| 档案治理 | `resolution_status` | `VARCHAR(48) NOT NULL` | 机构身份解析状态 |
| 档案治理 | `primary_source` | `VARCHAR(32)` | openalex/ror/ringgold/fundref/grid/lei/orcid |
| 位置ID | `location_id` | `VARCHAR(64)` | 当前选定的平台位置ID |
| 位置ID | `country_location_id` | `VARCHAR(64)` | 平台国家位置ID |
| 位置ID | `province_location_id` | `VARCHAR(64)` | 平台省级位置ID |
| 位置ID | `city_location_id` | `VARCHAR(64)` | 平台城市位置ID |
| 位置ID | `district_location_id` | `VARCHAR(64)` | 平台区县位置ID；当前来源不足时为空 |
| 地理展示 | `country_code` | `VARCHAR(8)` | ISO国家或地区代码 |
| 地理展示 | `country_name` | `VARCHAR(128)` | 国家或地区名称 |
| 地理展示 | `province_name` | `VARCHAR(128)` | 省级行政区名称 |
| 地理展示 | `city_name` | `VARCHAR(128)` | 城市名称 |
| 地理展示 | `district_name` | `VARCHAR(128)` | 区县名称；当前来源不足时为空 |
| 地理展示 | `latitude` | `DECIMAL(10,7)` | 纬度 |
| 地理展示 | `longitude` | `DECIMAL(10,7)` | 经度 |
| 位置质量 | `location_resolution_status` | `VARCHAR(16)` | resolved/unresolved |
| 位置质量 | `location_resolution_method` | `VARCHAR(32)` | 位置确定规则 |
| 位置质量 | `location_confidence` | `DECIMAL(4,3)` | 位置解析置信度，0到1 |
| 位置质量 | `location_quality_status` | `VARCHAR(32)` | unique/attribute_conflict |
| 位置质量 | `location_release_id` | `VARCHAR(64)` | 位置体系发布版本 |
| 展示 | `homepage_url` | `STRING` | 机构主页 |
| 展示 | `image_url` | `STRING` | 机构图片或Logo URL |
| 展示 | `established_year` | `SMALLINT` | 成立年份 |
| 指标 | `paper_count` | `BIGINT` | 发布口径内去重论文总数；NULL表示未计算 |
| 指标 | `cited_by_count` | `BIGINT` | 发布口径内论文当前被引总次数 |
| 指标 | `talent_count` | `BIGINT` | 发布口径内关联人才数 |
| 指标 | `project_count` | `BIGINT` | 当前机构关联的去重科研项目总数；直接机构关系优先，受资助论文机构仅作兜底 |
| 经费 | `associated_project_funding_amount_cny` | `DECIMAL(24,4)` | 关联项目人民币金额全额之和；等于真实额加模拟额，跨机构不可加总 |
| 经费 | `associated_project_funding_real_amount_cny` | `DECIMAL(24,4)` | `SOURCE_CONVERTED`项目的来源换算金额之和 |
| 经费 | `associated_project_funding_simulated_amount_cny` | `DECIMAL(24,4)` | `SIMULATED_SHENZHEN_MEDIAN_V1`项目的模拟金额之和 |
| 经费 | `associated_project_funding_real_project_count` | `BIGINT` | 具有来源换算金额的关联去重项目数 |
| 经费 | `associated_project_funding_simulated_project_count` | `BIGINT` | 具有模拟金额的关联去重项目数 |
| 经费 | `associated_project_funding_real_coverage_rate` | `DECIMAL(9,6)` | 真实项目数除以真实与模拟项目数之和 |
| 经费 | `associated_project_funding_amount_mix_type` | `VARCHAR(32)` | REAL_ONLY/SIMULATED_ONLY/MIXED/NO_PROJECT_EVIDENCE |
| 经费 | `associated_project_funding_scope_status` | `VARCHAR(64)` | 固定ASSOCIATED_PROJECT_FULL_AMOUNT_NOT_DISBURSEMENT |
| 经费 | `associated_project_funding_version` | `VARCHAR(64)` | 关联项目经费范围、求和与真假拆分口径版本 |
| 专利转化模拟 | `representative_patent_transfer_amount_cny` | `DECIMAL(24,4)` | 本机构代表专利Top20虚拟技术转化额之和；不是全量专利或真实收入 |
| 专利转化模拟 | `representative_patent_transfer_patent_count` | `BIGINT` | 参与虚拟金额求和的代表专利记录数；无代表专利机构为0 |
| 专利转化模拟 | `representative_patent_transfer_scope_status` | `VARCHAR(64)` | 固定`REPRESENTATIVE_PATENT_TOP20_SIMULATED` |
| 专利转化模拟 | `representative_patent_transfer_amount_version` | `VARCHAR(64)` | 代表专利虚拟转化额聚合口径与规则版本 |
| 合作总量 | `collaborator_institution_count` | `BIGINT` | 跨年份、跨已发布合作证据去重的合作机构数 |
| 合作总量 | `collaborative_paper_count` | `BIGINT` | 关联2至10家机构的MVP core合作论文去重数 |
| 合作总量 | `collaborative_patent_count` | `BIGINT` | 至少两家confirmed assignee机构共同关联的专利publication去重数 |
| 合作总量 | `collaboration_paper_coverage_status` | `VARCHAR(32)` | COMPLETE/NOT_AVAILABLE；论文合作统计覆盖状态 |
| 合作总量 | `collaboration_patent_coverage_status` | `VARCHAR(32)` | PARTIAL/NOT_AVAILABLE；专利合作统计覆盖状态 |
| 合作总量 | `collaboration_totals_version` | `VARCHAR(64)` | 三项合作总量的范围、去重键和来源版本 |
| 指标 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 指标 | `metric_definition_version` | `VARCHAR(64)` | 机构指标口径版本 |
| 状态与版本 | `is_active` | `BOOLEAN NOT NULL DEFAULT 1` | 是否有效 |
| 状态与版本 | `create_time` | `DATETIME(3) NOT NULL` | 机构档案首次创建时间UTC，更新时保留 |
| 状态与版本 | `data_version` | `BIGINT NOT NULL` | 同一机构ID单调递增的源版本或批次序号 |
| 状态与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，发布程序显式提供 |

机构论文与引用指标必须按批准的发布数据口径重算，不能直接复制来源 full 快照聚合值。
机构主画像不提供 `h_index`。

6.20.0只为当前有效深圳机构发布关联项目全额经费：先按`institution_id, project_id`去重，再把该机构
每个关联项目的`ads_project_profile.amount_cny`计入一次，不采用机构权重。一个项目关联多家机构时会在
每家机构各计全额，因此该字段适合单机构展示和比较，但禁止跨机构求和解释为深圳经费总量；跨机构、
学科和研究方向汇总必须使用§18.1的证据权重分配表。无项目证据的深圳机构金额和项目数写0并标记
`NO_PROJECT_EVIDENCE`；非深圳机构保持NULL，表示本版本未发布。金额只是关联项目金额，不是机构实际
到账、承担额或深圳财政投入。详细方法与字段使用见
[`docs/institution_project_funding_profile_v1.md`](docs/institution_project_funding_profile_v1.md)。

合作总量不能从 `ads_institution_collaboration_yearly` 的机构对计数直接求和。一篇三机构论文会形成
多个机构对，但在每家机构的 `collaborative_paper_count` 中只能按 `institution_id, work_id` 计一次；
共同专利同理按 `institution_id, publication_id` 去重。`collaborator_institution_count` 对论文合作、
直接项目合作与 confirmed assignee 共同专利产生的合作机构 ID 取并集，再跨年份去重。

论文合作沿用 §17.1 的网络范围：每篇论文关联2至10家机构，11家及以上的大型联盟论文整体排除；
因此该字段表示发布合作网络范围内的合作论文总数，而不是所有来源论文的无条件计数。专利合作只接受
同一 publication 上至少两家 `resolution_status='confirmed'` 的 assignee 机构；发明人任职关系不作为
机构共同专利。专利机构解析覆盖不完整，所以有统计资格的 MVP 机构写 `PARTIAL`，不得把0解释为
完整来源中绝对不存在合作专利。不在固定 MVP 机构总体中的扩展机构三个计数保持 NULL，并写
`NOT_AVAILABLE`，避免用0冒充已计算结果。

`profile_level` 固定为 `full / structured / source_id_only / name_only`；
`resolution_status` 区分 `confirmed / confirmed_historical / source_id_unresolved /
name_only_unresolved / superseded`。只有 `full` 和 `structured` 可视为存在详细 Profile；
Talent Experience 必须冗余 `institution_profile_level` 和 `institution_detail_available`，使前端
无需以 NULL 猜测详情能力。仅名称机构使用 `institution_type_id='unknown'`，所有未计算指标为
NULL，不得写 0。

机构中文名发布顺序为：已审核 DWD `dwd_institution.display_name_zh` → ROR 确定性中文名 →
NULL。人工补录发布时 `data_sources` 增加 `manual_curation`，并使用更大的 Key 级
`data_version`；不得用旧来源重跑静默覆盖人工值。人工位置校正必须来自版本化的
`dwd_institution_location`，不能直接把 CSV 中的自由文本地址写入 ADS。

机构位置层级统一为 CONTINENT → COUNTRY → PROVINCE → CITY → DISTRICT。OpenAlex/ROR 基础发布可靠覆盖
到城市；`location_v1_4_20261019` 首次发布深圳 9 个区级位置，并为 124 家已有中文名且
`paper_count>0` 的深圳 MVP 机构填写 `district_location_id` 和 `district_name`。区级位置必须先写入
`ads_location`，通过 `parent_location_id` 关联深圳市，并在 `ads_location_external_id` 保存
`AMAP_ADCODE` 映射；不得仅写无法治理的区名字符串。

## 15.1 `ads_location`

公共位置维表，供 institution 以及未来通过 institution 继承位置的 talent、project 使用。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与层级 | `location_id` | `VARCHAR(64) NOT NULL` | 平台统一位置ID，与任何单一来源解耦 |
| Key 与层级 | `location_level` | `VARCHAR(16) NOT NULL` | CONTINENT/COUNTRY/PROVINCE/CITY/DISTRICT |
| Key 与层级 | `parent_location_id` | `VARCHAR(64)` | 直接父级平台位置ID |
| 层级路径 | `continent_location_id` | `VARCHAR(64)` | 所属洲平台位置ID；洲行等于自身 |
| 层级路径 | `country_location_id` | `VARCHAR(64)` | 所属国家平台位置ID；国家行等于自身 |
| 层级路径 | `province_location_id` | `VARCHAR(64)` | 所属省级平台位置ID |
| 层级路径 | `city_location_id` | `VARCHAR(64)` | 所属城市平台位置ID |
| 层级路径 | `district_location_id` | `VARCHAR(64)` | 所属区县平台位置ID；区县行等于自身 |
| 名称 | `name` | `VARCHAR(256) NOT NULL` | 当前发布默认名称 |
| 名称 | `name_en` | `VARCHAR(256)` | 英文名称 |
| 名称 | `name_zh` | `VARCHAR(256)` | 中文名称；无可靠来源时为空 |
| 外部便利字段 | `continent_code` | `VARCHAR(16)` | AF/AN/AS/EU/NA/OC/SA |
| 外部便利字段 | `country_code` | `VARCHAR(8)` | ISO 3166-1 alpha-2国家或地区代码 |
| 外部便利字段 | `subdivision_code` | `VARCHAR(64)` | 来源行政区编码 |
| 外部便利字段 | `geonames_id` | `BIGINT` | GeoNames城市ID，仅用于外部互操作 |
| 坐标与质量 | `latitude` | `DECIMAL(10,7)` | 代表纬度 |
| 坐标与质量 | `longitude` | `DECIMAL(10,7)` | 代表经度 |
| 坐标与质量 | `quality_status` | `VARCHAR(32)` | unique/attribute_conflict |
| 坐标与质量 | `location_release_id` | `VARCHAR(64) NOT NULL` | 位置体系发布版本 |
| 状态与版本 | `is_active` | `BOOLEAN NOT NULL DEFAULT 1` | 是否为当前有效位置 |
| 状态与版本 | `data_version` | `BIGINT NOT NULL` | 同一位置ID单调递增的发布版本 |
| 状态与版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC |

中国国家、省、市展示时优先使用经治理的 `name_zh`；`name_zh` 为空表示尚无可靠中文来源，
不得按英文名或拼音自动翻译。引用位置 ID 的宽表必须从本表同步相应层级中文展示值，并随
`location_release_id` 提升 Key 级 `data_version`，不得在各宽表独立维护另一套翻译。

## 15.2 `ads_location_external_id`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `id_namespace` | `VARCHAR(64) NOT NULL` | ISO_3166_1_ALPHA2/ROR_SUBDIVISION/GEONAMES等 |
| Key | `external_id` | `VARCHAR(128) NOT NULL` | 来源命名空间内的外部位置ID |
| 映射 | `location_id` | `VARCHAR(64) NOT NULL` | 映射的平台统一位置ID |
| 映射 | `is_primary` | `BOOLEAN NOT NULL DEFAULT 1` | 是否为该命名空间主映射 |
| 映射 | `mapping_status` | `VARCHAR(32) NOT NULL` | confirmed/conflict |
| 版本 | `source_release` | `VARCHAR(64) NOT NULL` | 产生映射的来源版本 |
| 版本 | `location_release_id` | `VARCHAR(64) NOT NULL` | 位置体系发布版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | 同一外部ID映射的单调发布版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC |

平台位置 ID 不编码 GeoNames、ROR 或 ISO。外部编码只能通过本 bridge 关联；新增区级独立来源时
使用新的 `id_namespace`，同时复用或分配平台 `location_id`。

## 15.3 `ads_institution_paper`

一个机构的一篇代表论文一行，逻辑主键为`institution_id, paper_id`，每个机构最多20行。本表是机构
详情页的有界下钻服务表，不是全量机构—论文事实；完整关系继续保留在固定Iceberg事实层。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key与排名 | `institution_id`, `paper_id` | `VARCHAR(64) NOT NULL` | 平台机构与论文ID；联合逻辑主键 |
| Key与排名 | `paper_rank` | `INT NOT NULL` | 机构内部稳定排名，范围1至20且连续 |
| 来源身份 | `openalex_institution_id`, `openalex_work_id` | `VARCHAR(64) NOT NULL` | 审计用OpenAlex来源ID，不作为ADS主键 |
| 标题 | `doi`, `title`, `title_zh`, `title_en`, `title_original` | 多类型 | DOI与多语言标题快照；中文不自动翻译 |
| 发表 | `publication_date`, `publication_year`, `paper_type`, `language` | 多类型 | 发表日期、年份、类型和来源语言 |
| 学科 | `primary_topic_id`, `topic_ids`, `primary_source_id` | 多类型 | 平台Primary Topic、全部Topic与OpenAlex来源ID |
| 影响 | `cited_by_count`, `fwci` | `BIGINT`, `DECIMAL(14,6)` | 截至指标日的累计被引和论文FWCI |
| 机构署名 | `institution_authorship_count`, `institution_author_count` | `BIGINT NOT NULL` | 本机构署名位置数和可识别去重作者数 |
| 作者角色 | `has_first_author`, `has_corresponding_author` | `TINYINT NOT NULL` | 本机构是否关联第一作者或通讯作者 |
| 获取 | `is_open_access`, `fulltext_url` | `TINYINT`, `STRING` | OA标记与PDF、OA、落地页确定性兜底URL |
| 筛选 | `selection_reason`, `selection_method`, `selection_version` | 多类型 | 入选说明、方法代码和不可变规则版本 |
| 血缘 | `core_paper_snapshot_id`, `authorship_institution_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定论文范围及机构署名事实Snapshot |
| 版本 | `metrics_as_of_date`, `data_version`, `update_time` | 公共类型 | 指标截止日、Key级版本与UTC生成时间 |

首版固定从4,000,000篇MVP core和12,621,620条去重机构—论文关系中选择，排序规则为：

```text
cited_by_count DESC,
fwci DESC NULLS LAST,
publication_year DESC NULLS LAST,
openalex_work_id ASC
```

排名在完整机构论文集合上计算后取`paper_rank<=20`，不得先按年份、Topic或语言过滤后再补足20篇。
一篇论文关联多个机构时，可分别进入多个机构的Top 20，这是有效的多对多关系，不是重复数据。

## 15.4 `ads_institution_patent`

一个机构的一件代表Patent publication一行，逻辑主键为`institution_id, patent_id`，每个机构最多
20行。关系同时支持确认受让人和发明人任职关联，但必须显式区分证据语义。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key与排名 | `institution_id`, `patent_id` | `VARCHAR(64) NOT NULL` | 平台机构与Patent publication ID；联合逻辑主键 |
| Key与排名 | `patent_rank` | `INT NOT NULL` | 机构内部稳定排名，范围1至20且连续 |
| 来源身份 | `google_patent_publication_id`, `publication_number`, `application_number` | `VARCHAR` | Google Patents来源标识 |
| 分类 | `jurisdiction_code`, `kind_code`, `application_kind`, `family_id` | `VARCHAR` | 司法辖区、文献类型、原始申请类型和Google专利族ID |
| 标题 | `title`, `title_zh`, `title_en`, `title_original` | `STRING` | 多语言标题快照；中文不自动翻译 |
| 日期 | `application_date`, `publication_date`, `grant_date`, `is_granted` | 多类型 | 申请、公开、授权日期及授权标志；不表示当前有效 |
| 科学连接 | `cited_paper_count` | `BIGINT NOT NULL` | 成功关联MVP core的去重科学论文数 |
| 转化模拟 | `technology_transfer_amount_cny` | `DECIMAL(24,4)` | 单条代表专利虚拟技术转化额，币种CNY；不是实际交易或许可收入 |
| 转化模拟 | `technology_transfer_amount_value_type` | `VARCHAR(32)` | 固定`SIMULATED_RULE_V1`，前端必须展示模拟属性 |
| 转化模拟 | `technology_transfer_amount_version` | `VARCHAR(64)` | 确定性金额计算规则版本 |
| 关系 | `relationship_types` | `ARRAY<STRING> NOT NULL` | `CONFIRMED_ASSIGNEE`和/或`INVENTOR_AFFILIATION` |
| 关系 | `has_confirmed_assignee`, `has_inventor_affiliation` | `TINYINT NOT NULL` | 两类证据布尔标记 |
| 关系 | `relationship_status` | `VARCHAR(40) NOT NULL` | `ASSIGNEE_ONLY/INVENTOR_AFFILIATION_ONLY/BOTH` |
| 筛选 | `selection_reason`, `selection_method`, `selection_version` | 多类型 | 入选说明、方法代码和不可变规则版本 |
| 血缘 | `patent_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定Google Patent Snapshot |
| 血缘 | `patent_institution_snapshot_id`, `patent_institution_release_id` | `VARCHAR(128) NOT NULL` | 固定确认受让机构关系Snapshot与发布版本 |
| 血缘 | `inventor_affiliation_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定发明人任职关系Snapshot |
| 版本 | `metrics_as_of_date`, `data_version`, `update_time` | 公共类型 | 指标截止日、Key级版本与UTC生成时间 |

两类关系先按`institution_id, google_patent_publication_id`合并；同一机构同一publication同时命中两类
证据时只保留一行并标记`BOTH`。排序规则为：

```text
has_confirmed_assignee DESC,
is_granted DESC,
cited_paper_count DESC,
publication_year DESC NULLS LAST,
google_patent_publication_id ASC
```

首版只发布能够映射到既有平台`patent_id`并关联`ads_patent_profile`的Patent publication，不能为扩大
覆盖临时生成无画像的专利ID。`CONFIRMED_ASSIGNEE`表示固定消歧发布中的确认assignee关系，但Google
来源不能区分original/current assignee，因此仍不得解释为当前专利所有权。
`INVENTOR_AFFILIATION`只表示可靠Author–Inventor连接下的发明人任职/署名机构关联，前端不得显示为
“机构申请”“机构持有”或“机构拥有”。

8.10.0为每条代表专利生成确定性的CNY虚拟转化额，并在机构主画像中聚合。该金额只覆盖本表Top20，
所有记录均标记`SIMULATED_RULE_V1`；前端必须同时读取模拟标记，不能将其展示为实际成交额。全部
机构画像均发布聚合字段，无代表专利的机构写0。公式、字段及执行方法见
[`docs/institution_patent_transfer_amount_v1.md`](docs/institution_patent_transfer_amount_v1.md)。

两张代表成果表的发布、固定Snapshot、行数核验与查询示例见
[`docs/institution_achievement_ads_v1.md`](docs/institution_achievement_ads_v1.md)。

## 16. `ads_institution_discipline_profile`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 机构统一ID |
| Key | `topic_id` | `VARCHAR(64) NOT NULL` | Topic统一ID |
| Field | `field_id` | `VARCHAR(64) NOT NULL` | Field统一ID |
| Field | `field_name_zh` | `STRING` | Field中文名称 |
| Field | `field_name_en` | `STRING` | Field英文名称 |
| Subfield | `subfield_id` | `VARCHAR(64) NOT NULL` | Subfield统一ID |
| Subfield | `subfield_name_zh` | `STRING` | Subfield中文名称 |
| Subfield | `subfield_name_en` | `STRING` | Subfield英文名称 |
| Topic | `topic_name_zh` | `STRING` | Topic中文名称 |
| Topic | `topic_name_en` | `STRING` | Topic英文名称 |
| 指标 | `paper_count` | `BIGINT` | 该Topic关联的去重论文数 |
| 指标 | `cited_by_count` | `BIGINT` | 该Topic论文当前被引次数 |
| 指标 | `talent_count` | `BIGINT` | 该Topic关联人才数 |
| 指标 | `project_count` | `BIGINT` | 该Topic关联的去重科研项目数；project对应DWD Grant |
| 指标 | `paper_share` | `DECIMAL(12,8)` | 该Topic论文占机构论文比例，0到1 |
| 指标 | `citation_share` | `DECIMAL(12,8)` | 该Topic论文被引占机构被引比例，0到1 |
| 指标 | `topic_rank` | `INT` | 机构内部Topic排名 |
| 科研实力 | `paper_strength_score` | `DECIMAL(9,6)` | 论文数在同一Topic机构总体中的0至100平均排名百分位分 |
| 科研实力 | `citation_strength_score` | `DECIMAL(9,6)` | 累计被引数在同一Topic机构总体中的0至100平均排名百分位分 |
| 科研实力 | `talent_strength_score` | `DECIMAL(9,6)` | 人才数在同一Topic机构总体中的0至100平均排名百分位分 |
| 科研实力 | `research_strength_score` | `DECIMAL(9,6)` | 三项标准化分按固定权重加权得到的0至100综合科研实力分 |
| 科研实力 | `research_strength_rank` | `BIGINT` | 同一Topic内综合科研实力稳定排名 |
| 科研实力 | `research_strength_benchmark_count` | `BIGINT` | 同一Topic内进入评分的机构数 |
| 科研实力 | `research_strength_version` | `VARCHAR(64)` | 评分总体、标准化、权重和排序规则版本 |
| 版本 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本 | `metric_definition_version` | `VARCHAR(64)` | 机构学科指标口径版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或批次序号 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，发布程序显式提供 |

每条记录必须对应一个 Topic，并在同一行携带其 Field、Subfield 的 ID、中英文名称；不保存
`discipline_type`、`parent_discipline_id` 或 Domain。Field/Subfield 汇总由 Topic 行按对应 ID
聚合得到。三级名称使用 `technology_v2.v_openalex_*_bilingual` 发布视图。

`project_count` 是该机构在该 Topic 下关联的去重科研项目数，`project` 对应 DWD Grant；
发布程序必须按批准的 MVP Grant 数据、机构身份映射和 Grant-Topic 关系计算。
当前发布连接 `ads_project_institution` 与 `ads_project_topic`，按全部关联 Topic 对
`project_id` 去重计算；不只统计 Primary Topic。已发布机构—Topic Key 没有关联项目时写 0，
不再以 NULL 表示尚未计算。当前 Grant-Topic 来自受资助论文 Topic 推导，并非旧 Awards
Snapshot 的来源原生分类。

### 16.1 机构—Topic 综合科研实力评分

评分只使用本表已发布的 `paper_count`、`cited_by_count` 和 `talent_count`，分别表示论文产出、
累计学术影响和科研人才规模。每个 Topic 独立建立基准总体；`paper_count > 0` 的机构—Topic 行
进入评分。同一机构在不同 Topic 的分数来自不同总体，不能把分数相加解释为机构总实力；机构级
比较继续使用 §17.4 的 `ads_institution_technology_power`。

对同一 Topic 的任一原始指标 `X`，并列值使用其占据名次的平均值：

```text
average_rank_X(i) = (lowest_rank_X(i) + highest_rank_X(i)) / 2

score_X(i) =
    N = 1 时：100
    N > 1 时：100 * (average_rank_X(i) - 1) / (N - 1)
```

`research_strength_version='institution_topic_research_strength_v1'` 固定使用以下公式：

```text
research_strength_score =
      0.40 * paper_strength_score
    + 0.35 * citation_strength_score
    + 0.25 * talent_strength_score
```

三项分项分和综合分均限制在 0–100。同一 Topic 只有一家机构时，三项分和综合分均为 100。
`research_strength_rank` 按综合分降序；综合分相同时依次按被引分、论文分、人才分和
`institution_id` 排序，保证排名唯一且可复算。累计被引具有论文年龄效应，首版没有 Topic 粒度
FWCI 或引用窗口校正，因此该分数是固定 MVP 数据范围内的相对、描述性指标，不是同行评审结论，
也不表示项目投入、专利所有权或产业化能力。

## 17. `ads_institution_yearly_metrics`

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 机构统一ID |
| Key | `statistics_year` | `SMALLINT NOT NULL` | 统计年份 |
| 论文与引用 | `paper_count` | `BIGINT` | 当年发布的去重论文数 |
| 论文与引用 | `cited_by_count` | `BIGINT` | 当年发布论文截至统计日的当前累计被引次数 |
| 论文与引用 | `citation_count` | `BIGINT` | 机构论文在该自然年收到的引用次数 |
| 论文与引用 | `international_paper_count` | `BIGINT` | 当年国际合作论文数 |
| 论文与引用 | `open_access_paper_count` | `BIGINT` | 当年开放获取论文数 |
| 论文与引用 | `fwci` | `DECIMAL(18,8)` | 忽略NULL后按论文等权AVG(fwci)；无最低覆盖率 |
| 论文与引用 | `avg_citations_per_paper` | `DECIMAL(18,6)` | 篇均被引次数 |
| 其他指标 | `talent_count` | `BIGINT` | 当年关联人才数 |
| 其他指标 | `new_talent_count` | `BIGINT` | 当年首次在发布MVP core中观察到与机构关联的人才数；不是实际入职人数 |
| 其他指标 | `patent_count` | `BIGINT` | 按申请年统计的发明人任职关联专利数；不表示专利权属 |
| 其他指标 | `project_count` | `BIGINT` | 当年项目数 |
| 其他指标 | `collaborator_count` | `BIGINT` | 当年合作机构数 |
| 版本 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本 | `metric_definition_version` | `VARCHAR(64)` | 机构年度指标口径版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key单调递增的源版本或批次序号 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | ADS记录生成时间UTC，发布程序显式提供 |

`paper_count` 是当年发布论文数；`cited_by_count` 是当年发布论文截至统计日的累计被引；
`citation_count` 是机构论文在该自然年收到的引用数，三者不可混用。

`new_talent_count` 明确定义为该自然年首次在发布 MVP core 中观察到与机构关联的 MVP 人才数，
不是实际入职人数。`fwci` 忽略 NULL 后按论文等权计算 `AVG(fwci)`，不做额外加权，也不设置
最低覆盖率；无非空 FWCI 论文时保持 NULL。`patent_count` 是按专利申请年统计的
“发明人任职关联专利数”，来源关系必须为 `inventor_affiliation`，不表示申请人、权利人或
机构拥有的专利。

当前发布口径、固定 Snapshot、字段填充状态与行数核验见
[`docs/institution_ads_mvp_v1.md`](docs/institution_ads_mvp_v1.md)。

## 17.1 `ads_institution_collaboration_yearly`

机构年度有向合作边表，服务目标机构选择后的合作网络、来源类型筛选、时间范围筛选和多跳关系
遍历。一项 A—B 合作必须发布 `A → B` 与 `B → A` 两行；`institution_id` 与
`collaborator_institution_id` 不得相同。跨年查询必须先按所选年份聚合基础计数，再计算节点度、
加权度、排名或中心性，不得直接累加年度排名。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 目标机构平台ID |
| Key | `collaborator_institution_id` | `VARCHAR(64) NOT NULL` | 合作机构平台ID；不得等于目标机构 |
| Key | `statistics_year` | `SMALLINT NOT NULL` | 论文发表年或专利公开年 |
| 目标机构快照 | `institution_name` | `STRING NOT NULL` | 目标机构发布时名称快照 |
| 目标机构快照 | `institution_type_id` | `VARCHAR(32) NOT NULL` | 目标机构类型 |
| 合作机构快照 | `collaborator_institution_name` | `STRING NOT NULL` | 合作机构发布时名称快照 |
| 合作机构快照 | `collaborator_institution_type_id` | `VARCHAR(32) NOT NULL` | 合作机构类型 |
| 合作机构快照 | `collaborator_country_code` | `VARCHAR(8)` | 合作机构国家代码 |
| 合作机构快照 | `collaborator_country_name` | `VARCHAR(128)` | 合作机构国家名称 |
| 合作机构快照 | `collaborator_province_name` | `VARCHAR(128)` | 合作机构省级名称 |
| 合作机构快照 | `collaborator_city_name` | `VARCHAR(128)` | 合作机构城市名称 |
| 论文合作 | `co_paper_count` | `BIGINT NOT NULL` | 两个机构共同出现的去重论文数 |
| 论文合作 | `cross_author_co_paper_count` | `BIGINT NOT NULL` | 至少由不同署名位置代表两个机构的论文数 |
| 论文合作 | `multi_affiliation_paper_count` | `BIGINT NOT NULL` | 仅由同一署名位置多机构署名形成的论文数 |
| 论文合作 | `shared_author_count` | `BIGINT` | 合作论文涉及的去重可解析作者数；未计算时为空 |
| 论文合作 | `co_paper_cited_by_count` | `BIGINT` | 合作论文截至统计日累计被引数之和 |
| 论文合作 | `co_paper_fwci` | `DECIMAL(18,8)` | 合作论文非空FWCI等权平均值 |
| 论文合作 | `open_access_co_paper_count` | `BIGINT NOT NULL` | 开放获取合作论文数 |
| 专利合作 | `co_patent_count` | `BIGINT` | 两机构均为confirmed assignee的去重专利公开文献数 |
| 专利合作 | `co_patent_family_count` | `BIGINT` | 共同权利人专利的去重可靠专利族数 |
| 项目合作 | `co_project_count` | `BIGINT` | 双方均有直接项目角色的去重联合项目数；论文推导关系不参与 |
| 分类 | `cooperation_type_ids` | `ARRAY<STRING> NOT NULL` | paper_coauthorship/patent_co_assignee/project_co_investigator |
| 分类 | `is_domestic_collaboration` | `BOOLEAN` | 两个机构国家相同 |
| 分类 | `is_international_collaboration` | `BOOLEAN` | 两个机构国家不同 |
| 分类 | `is_cross_region_collaboration` | `BOOLEAN` | 同一国家且省级位置不同 |
| 强度 | `paper_collaboration_strength` | `DECIMAL(12,6)` | 共同论文数/目标机构当年论文数 |
| 强度 | `patent_collaboration_strength` | `DECIMAL(12,6)` | 版本化专利合作强度 |
| 强度 | `collaboration_strength` | `DECIMAL(12,6)` | 按可用来源计算的综合合作强度 |
| 强度 | `strength_version` | `VARCHAR(64)` | 合作强度公式版本 |
| 覆盖与质量 | `paper_coverage_status` | `VARCHAR(32) NOT NULL` | COMPLETE/PARTIAL/NOT_AVAILABLE |
| 覆盖与质量 | `patent_coverage_status` | `VARCHAR(32) NOT NULL` | COMPLETE/PARTIAL/NOT_AVAILABLE |
| 覆盖与质量 | `project_coverage_status` | `VARCHAR(32) NOT NULL` | PARTIAL/NOT_AVAILABLE；当前直接项目机构事实不完整 |
| 覆盖与质量 | `relationship_quality_status` | `VARCHAR(32) NOT NULL` | VERIFIED/PARTIAL/LOW_CONFIDENCE |
| 来源与版本 | `data_sources` | `ARRAY<STRING> NOT NULL` | 实际参与本行计算的数据来源 |
| 来源与版本 | `paper_source_snapshot_id` | `VARCHAR(128)` | 论文机构事实输入Snapshot |
| 来源与版本 | `patent_source_snapshot_id` | `VARCHAR(128)` | 专利共同权利人输入Snapshot |
| 来源与版本 | `project_source_snapshot_id` | `VARCHAR(128)` | 直接项目机构事实输入Snapshot |
| 来源与版本 | `identity_release_id` | `VARCHAR(64) NOT NULL` | 机构身份映射发布版本 |
| 来源与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| 来源与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 指标口径版本 |
| 来源与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 来源与版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

论文合作来自发布 MVP core 中 `dwd_work_authorship_institution` 的机构共现，并按论文去重。只有关联
机构数为 2–10 的论文进入合作计算；关联 11 家及以上机构的论文整篇排除，不截取来源顺序中的前
10 家机构，也不从该论文生成任何机构边。该阈值属于 `metric_definition_version` 的正式口径。
`cross_author_co_paper_count` 要求两个机构至少能由不同 `authorship_index` 代表；如果一篇论文的
两个机构只来自同一署名位置，则计入 `multi_affiliation_paper_count`。两者之和必须严格等于
`co_paper_count`。首版 `shared_author_count` 尚未在有界内存条件下完成跨论文精确去重，保持 NULL。

`paper_collaboration_strength` 定义为“该机构对当年共同论文数 ÷ 目标机构当年论文数”，因此是有向
指标；首版在专利关系不可用时，`collaboration_strength` 等于论文合作强度。跨年度或改变数据来源
后必须使用相同版本公式重算，不能直接对年度强度求和。

专利合作只允许消费两个及以上 `resolution_status='confirmed'` 平台机构共同出现的 Google Patent
assignee 事实。`unique_candidate`、`ambiguous`、名称相似或发明人任职关系均不得写入专利合作指标；
专利引用论文也不是机构合作。当前 Assignee 消歧发布没有 confirmed 关系，因此专利字段为 NULL、
`patent_coverage_status='NOT_AVAILABLE'`，不得写 0 冒充“确认没有”。

项目合作只使用 `ads_project_institution` 中角色为 `awarded`、`lead_affiliation`、
`co_lead_affiliation` 或 `investigator_affiliation` 的直接机构事实，并按项目来源 `start_year`
归入年度。双方在同一项目出现时形成两个方向的机构边，`co_project_count` 对 `project_id` 去重。
`funded_output_affiliation` 仅表示受资助论文的机构署名，不得参与联合项目计数。当前直接项目机构
覆盖有限，因此有直接事实的双方标记 `project_coverage_status='PARTIAL'`；任一方完全没有直接项目
机构事实时计数保持 NULL 并标记 `NOT_AVAILABLE`，不得以 0 冒充确认无联合项目。

`paper_coverage_status`、`patent_coverage_status` 使用 `COMPLETE / PARTIAL / NOT_AVAILABLE`；
`relationship_quality_status` 使用 `VERIFIED / PARTIAL / LOW_CONFIDENCE`。首版存在不同署名位置的
论文边为 `VERIFIED`，仅有同一作者多机构署名证据的边为 `LOW_CONFIDENCE`。发布入口和核验口径见
[`docs/institution_collaboration_ads_v1.md`](docs/institution_collaboration_ads_v1.md)。

## 17.1.1 `ads_institution_collaboration_subfield_yearly`

机构年度合作领域表，一行表示一个有向机构对在一个自然年内由真实合作成果支持的一个Subfield。
逻辑Key为`institution_id, collaborator_institution_id, statistics_year, subfield_id`。本表专门服务
合作领域筛选，不使用两个机构各自学科画像的集合交集，因此不会把“双方分别研究同一领域”误报为
“双方在该领域发生合作”。

论文领域只使用双方共同论文的Primary Topic，并通过公共Topic维表的祖先关系映射到平台Subfield。
专利领域只使用双方均为`confirmed` assignee的共同Patent publication，再由该专利引用科学论文的
Primary Topic映射到Subfield；这是`CITED_SCIENCE_TOPIC`语义，不表示专利正文技术分类。一个共同专利
可关联多个Subfield，但同一机构对、年份、Subfield内按`publication_id`去重。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 目标机构平台ID |
| Key | `collaborator_institution_id` | `VARCHAR(64) NOT NULL` | 合作机构平台ID；不得等于目标机构 |
| Key | `statistics_year` | `SMALLINT NOT NULL` | 合作论文发表年或共同专利公开年 |
| Key | `subfield_id` | `VARCHAR(64) NOT NULL` | 平台Subfield ID，可关联`ads_discipline_subfield` |
| 领域证据 | `co_paper_count` | `BIGINT NOT NULL` | 该Subfield内双方共同出现的去重论文数 |
| 领域证据 | `co_patent_count` | `BIGINT NOT NULL` | 该Subfield内双方confirmed assignee共同专利数 |
| 覆盖分母 | `pair_co_paper_count` | `BIGINT NOT NULL` | 机构对当年全部合作论文数 |
| 覆盖分子 | `classified_co_paper_count` | `BIGINT NOT NULL` | 可映射到Subfield的合作论文数 |
| 覆盖分母 | `pair_co_patent_count` | `BIGINT NOT NULL` | 机构对当年全部confirmed共同受让专利数 |
| 覆盖分子 | `classified_co_patent_count` | `BIGINT NOT NULL` | 可由引用科学Topic映射到Subfield的共同专利数 |
| 覆盖 | `paper_subfield_coverage_rate` | `DECIMAL(9,6)` | `classified_co_paper_count / pair_co_paper_count` |
| 覆盖 | `patent_subfield_coverage_rate` | `DECIMAL(9,6)` | `classified_co_patent_count / pair_co_patent_count` |
| 分类 | `evidence_type_ids` | `ARRAY<STRING> NOT NULL` | `paper_coauthorship`和/或`patent_co_assignee` |
| 覆盖 | `paper_coverage_status` | `VARCHAR(32) NOT NULL` | COMPLETE/PARTIAL/NOT_AVAILABLE |
| 覆盖 | `patent_coverage_status` | `VARCHAR(32) NOT NULL` | COMPLETE/PARTIAL/NOT_AVAILABLE |
| 血缘 | `paper_source_snapshot_id` | `VARCHAR(128)` | 固定机构论文输入Snapshot |
| 血缘 | `patent_source_snapshot_id` | `VARCHAR(128)` | 固定confirmed专利机构关系Snapshot |
| 血缘 | `work_source_snapshot_id` | `VARCHAR(128)` | 固定论文主体Snapshot |
| 血缘 | `topic_source_snapshot_id` | `VARCHAR(128)` | 固定论文Topic关系Snapshot |
| 版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| 版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 合作Subfield口径版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

查询某Subfield下的机构合作组合时，必须先按`subfield_id`和时间范围过滤，再按有向机构对聚合
`co_paper_count`与`co_patent_count`。论文或专利覆盖状态为`PARTIAL/NOT_AVAILABLE`时必须随结果返回；
没有Subfield映射的合作成果不会凭空进入其他领域，也不得解释为不存在合作成果。

## 17.2 `ads_institution_topic_entry`

一行表示一个平台机构在固定 400 万篇 MVP core 中第一次以 **Primary Topic** 发表论文的
观察事实。逻辑主键为 `institution_id, topic_id`。本表服务单 Topic 新增机构趋势以及多 Topic
选择后的机构去重，不表示机构成立时间，也不声称是机构真实历史上的首次研究活动。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 机构平台ID |
| Key | `topic_id` | `VARCHAR(64) NOT NULL` | Topic平台ID |
| 来源身份 | `openalex_institution_id` | `VARCHAR(64) NOT NULL` | 审计用OpenAlex机构ID |
| 来源身份 | `openalex_topic_id` | `VARCHAR(64) NOT NULL` | 审计用OpenAlex Topic ID |
| 首次观察 | `first_observed_year` | `SMALLINT NOT NULL` | MVP core内Primary Topic首次论文发表年 |
| 首次观察 | `first_year_paper_count` | `BIGINT NOT NULL` | 首次观察年去重论文数 |
| 首次观察 | `observed_paper_count` | `BIGINT NOT NULL` | 2015–2026观察窗内该机构该Primary Topic去重论文数 |
| 口径状态 | `observation_status` | `VARCHAR(32) NOT NULL` | BASELINE_LEFT_CENSORED/COMPLETE/PARTIAL_YEAR |
| 口径状态 | `topic_relation_scope` | `VARCHAR(32) NOT NULL` | 固定PRIMARY_TOPIC |
| 来源与版本 | `data_sources` | `ARRAY<STRING> NOT NULL` | 实际使用的数据源 |
| 来源与版本 | `core_paper_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定MVP core机构论文Snapshot |
| 来源与版本 | `work_topic_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定Work–Topic Snapshot |
| 来源与版本 | `identity_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定身份映射Snapshot |
| 来源与版本 | `identity_release_id` | `VARCHAR(64) NOT NULL` | 平台身份发布版本 |
| 来源与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| 来源与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 口径版本 |
| 来源与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 来源与版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`topic_relation_scope` 首版固定为 `PRIMARY_TOPIC`。`first_observed_year=2015` 的记录标记为
`BASELINE_LEFT_CENSORED`，表示机构最迟在基线年已被观察到，不能解释为 2015 年真实新增；
2016–2025 标记为 `COMPLETE`；尚未完整结束的 2026 年标记为 `PARTIAL_YEAR`。

单 Topic 年度新增量按 `topic_id, first_observed_year` 对机构去重。多个 Topic 合并分析时，必须
先对每个机构取所选 Topic 中最小的 `first_observed_year`，再按年份计数；不得直接相加各 Topic
的年度人数。运行入口、固定 Snapshot 和查询示例见
[`docs/institution_topic_entry_ads_v1.md`](docs/institution_topic_entry_ads_v1.md)。

## 17.3 产业分类与机构产业参与

`ads_industry` 是版本化产业分类维表，首版发布国家知识产权局 2018 年 IPC–
国民经济行业参照表中的 GB/T 4754—2017 节点。不同产业分类体系即使代码相同也不合并。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 产业分类体系稳定代码 |
| Key | `industry_id` | `VARCHAR(64) NOT NULL` | 平台产业节点ID |
| 节点 | `industry_code` | `VARCHAR(32) NOT NULL` | 来源分类代码 |
| 节点 | `industry_name_zh` | `VARCHAR(512) NOT NULL` | 官方中文名称 |
| 节点 | `industry_name_en` | `VARCHAR(512)` | 英文名称；无可靠来源时为空 |
| 节点 | `industry_level` | `TINYINT NOT NULL` | 1门类/2大类/3中类/4小类 |
| 节点 | `industry_level_name` | `VARCHAR(32) NOT NULL` | section/division/major_group/group |
| 节点 | `parent_industry_id` | `VARCHAR(64)` | 直接父节点ID |
| 节点 | `parent_industry_code` | `VARCHAR(32)` | 直接父节点来源代码 |
| 路径 | `section_industry_id` | `VARCHAR(64) NOT NULL` | 所属门类ID |
| 路径 | `division_industry_id` | `VARCHAR(64)` | 所属大类ID |
| 路径 | `major_group_industry_id` | `VARCHAR(64)` | 所属中类ID |
| 路径 | `group_industry_id` | `VARCHAR(64)` | 所属小类ID |
| 路径 | `is_leaf` | `BOOLEAN NOT NULL` | 是否四位行业小类 |
| 版本 | `taxonomy_release_id` | `VARCHAR(64) NOT NULL` | 分类发布版本 |
| 版本 | `source_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定DWD节点Snapshot |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`ads_institution_industry` 是机构产业技术参与关系，不是机构主营行业、工商登记行业或专利所有权表。
关系存在性使用以下两类可追溯证据的去重并集：

1. `confirmed_assignee`：`dwd_patent_institution_google.resolution_status='confirmed'` 的
   Patent assignee–Institution 关系。
2. `inventor_affiliation`：已经可靠关联到 OpenAlex Author 的发明人，在专利申请年前后两年内，
   其论文署名机构经 active identity bridge 解析为平台机构。该证据只表示发明人同期与机构存在
   可追溯的科研任职/署名关系，不表示机构申请、持有或拥有专利。

任一证据能够连接到专利 IPC 并命中产业参照关系，即可建立机构—产业行。两类证据不得相互冒充，
必须在行上分别标注；同一机构—专利组合—产业同时命中两类证据时只形成一个关系计数。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id` | `VARCHAR(64) NOT NULL` | 平台机构ID |
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 产业分类体系稳定代码 |
| Key | `industry_id` | `VARCHAR(64) NOT NULL` | 平台产业节点ID |
| 产业快照 | `industry_code` | `VARCHAR(32) NOT NULL` | 来源分类代码 |
| 产业快照 | `industry_name_zh` | `VARCHAR(512) NOT NULL` | 产业官方中文名快照 |
| 产业快照 | `industry_name_en` | `VARCHAR(512)` | 产业英文名快照 |
| 产业快照 | `industry_level` | `TINYINT NOT NULL` | 1门类/2大类/3中类/4小类 |
| 产业快照 | `industry_level_name` | `VARCHAR(32) NOT NULL` | section/division/major_group/group |
| 产业快照 | `parent_industry_id` | `VARCHAR(64)` | 直接父产业节点ID |
| 产业快照 | `parent_industry_code` | `VARCHAR(32)` | 直接父产业来源代码 |
| 专利规模 | `patent_count` | `BIGINT NOT NULL` | 两类关系证据并集内，Google family ID优先、publication兜底的去重专利组合单元数；不表示机构专利所有权 |
| 专利规模 | `patent_publication_count` | `BIGINT NOT NULL` | 去重Patent publication数 |
| 专利规模 | `granted_patent_count` | `BIGINT NOT NULL` | 至少一个publication有grant_date的专利组合单元数 |
| 专利规模 | `recent_5y_patent_count` | `BIGINT NOT NULL` | 统计截止年及前四年公开的专利组合单元数 |
| 专利规模 | `fractional_patent_count` | `DECIMAL(20,8) NOT NULL` | 按同一专利命中的四位产业数分数计数并向上汇总 |
| 映射质量 | `complete_match_patent_count` | `BIGINT NOT NULL` | 至少命中一条官方星号完全对应规则的专利数 |
| 映射质量 | `reference_match_only_patent_count` | `BIGINT NOT NULL` | 仅命中非星号参照关系的专利数 |
| 关系证据 | `confirmed_assignee_patent_count` | `BIGINT NOT NULL` | 本机构产业行内具有confirmed assignee证据的去重专利组合单元数 |
| 关系证据 | `inventor_affiliation_patent_count` | `BIGINT` | 本机构产业行内具有发明人任职证据的去重专利组合单元数；旧版本未计算时为空 |
| 关系证据 | `relationship_evidence_types` | `ARRAY<STRING>` | 实际证据类型去重数组：confirmed_assignee和/或inventor_affiliation |
| 关系证据 | `has_confirmed_assignee_evidence` | `BOOLEAN` | 是否至少有一个confirmed assignee证据组合单元 |
| 关系证据 | `has_inventor_affiliation_evidence` | `BOOLEAN` | 是否至少有一个发明人任职证据组合单元 |
| 关系证据 | `relationship_evidence_status` | `VARCHAR(40)` | ASSIGNEE_ONLY/INVENTOR_AFFILIATION_ONLY/BOTH；旧版本为空 |
| 关系证据 | `minimum_affiliation_year_distance` | `BIGINT` | 任职证据论文年与专利申请年的最小绝对差，当前只能为0至2；无任职证据为空 |
| 映射质量 | `project_count` | `BIGINT` | 现有专利证据机构产业Key内的去重项目数；项目产业证据来自受资助成果被产业专利引用；已发布未命中为0，未发布为NULL |
| 映射质量 | `evidence_quality_status` | `VARCHAR(32) NOT NULL` | COMPLETE_ONLY/MIXED/REFERENCE_ONLY |
| 覆盖与排名 | `total_confirmed_assignee_patent_count` | `BIGINT NOT NULL` | 机构全部confirmed assignee专利组合单元数 |
| 覆盖与排名 | `total_inventor_affiliation_patent_count` | `BIGINT` | 机构全部发明人任职关联专利组合单元数；不限是否命中产业，旧版本为空 |
| 覆盖与排名 | `total_linked_patent_count` | `BIGINT` | 两类证据按专利组合单元去重后的机构全部关联专利并集，旧版本为空 |
| 覆盖与排名 | `mapped_patent_count` | `BIGINT NOT NULL` | 当前指标版本中至少映射一个产业的关联专利组合单元数 |
| 覆盖与排名 | `mapped_linked_patent_count` | `BIGINT` | 两类证据并集内至少映射一个产业的关联专利组合单元数；v2等于mapped_patent_count |
| 覆盖与排名 | `mapping_coverage_rate` | `DECIMAL(12,8) NOT NULL` | v2为mapped_linked_patent_count/total_linked_patent_count；v1为assignee口径 |
| 覆盖与排名 | `industry_share` | `DECIMAL(12,8) NOT NULL` | 同机构同层级fractional_patent_count占比 |
| 覆盖与排名 | `institution_industry_rank` | `INT NOT NULL` | 产业在本机构同层级内排名 |
| 覆盖与排名 | `industry_institution_rank` | `INT NOT NULL` | 机构在本产业内排名 |
| 覆盖与排名 | `activity_percentile` | `DECIMAL(12,8) NOT NULL` | 机构在本产业的活动百分位，越大越靠前 |
| 来源与版本 | `data_sources` | `ARRAY<STRING> NOT NULL` | 实际参与计算的数据来源 |
| 来源与版本 | `taxonomy_release_id` | `VARCHAR(64) NOT NULL` | 产业分类发布版本 |
| 来源与版本 | `source_ipc_release` | `VARCHAR(32) NOT NULL` | 官方参照表所用IPC版本 |
| 来源与版本 | `target_ipc_release` | `VARCHAR(32) NOT NULL` | 专利匹配使用的当前IPC字典版本 |
| 来源与版本 | `patent_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定Patent DWD Snapshot |
| 来源与版本 | `patent_institution_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定Patent-Institution Snapshot |
| 来源与版本 | `patent_institution_release_id` | `VARCHAR(128) NOT NULL` | Patent-Institution确认发布版本 |
| 来源与版本 | `inventor_affiliation_snapshot_id` | `VARCHAR(128)` | 固定发明人任职关系Snapshot；旧版本为空 |
| 来源与版本 | `inventor_affiliation_release_id` | `VARCHAR(128)` | 发明人任职关系发布版本；旧版本为空 |
| 来源与版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| 来源与版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 指标口径版本 |
| 来源与版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 来源与版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

### 17.3.1 关系生成与去重顺序

关系必须按下列固定顺序生成：

```text
confirmed assignee ─┐
                    ├─ Institution + Patent publication + evidence_type
inventor affiliation┘
        ↓ active identity bridge
Institution + Google family（缺失时publication）+ evidence_type
        ↓ Patent IPC + 固定IPC真实父链产业映射
Institution + patent组合单元 + 四位产业 + evidence_type
        ↓ 跨证据类型去重
Institution + patent组合单元 + 四位产业
        ↓ 四级产业路径上卷
ads_institution_industry
```

`patent_count` 对两类证据取并集：同一机构、同一专利组合单元、同一产业同时具有 assignee 与
任职证据时只计一次；对应组合单元会分别进入
`confirmed_assignee_patent_count` 和 `inventor_affiliation_patent_count`，因此两个分项之和可以大于
`patent_count`。同一发明人关联多篇论文、同一专利关联多名发明人或同一机构出现多个来源记录，
均不得放大专利计数。不同机构通过各自发明人关联同一专利是有效的多机构产业关系，分别计入各机构。

Google family ID 非空时作为组合单元，缺失时回退 publication ID。一个组合单元命中 N 个四位
产业小类时，每个小类获得 `1/N` 的 `fractional_patent_count`；该权重在证据类型合并后计算，不能
让同时具有两类证据的专利获得双倍权重。向中类、大类和门类上卷时求和；`industry_share` 在同一
机构、同一产业层级内归一化，各产业之和必须为 1。排名和百分位基于两类证据并集的
`fractional_patent_count`。

### 17.3.2 发明人任职证据约束

发明人任职关系只能消费已发布的 Author–Inventor 可靠映射，不得临时使用姓名模糊匹配。机构来自
发明人在论文上的署名机构，论文 `publication_year` 与专利 `filing_date` 年份的绝对差必须不超过
2；专利申请日或论文年份缺失时不得生成该证据。OpenAlex institution ID 必须通过固定 Snapshot
中的 active identity bridge 转换为平台 `institution_id`。`minimum_affiliation_year_distance` 保存
命中证据中的最小年份差，用于解释证据时效，不用于宣称正式雇佣关系。

前端和 API 对 `INVENTOR_AFFILIATION_ONLY` 只能描述为“发明人任职关联”或“产业技术活动关联”，
不得描述为“机构专利”“机构持有”“机构申请”或“专利权人”。只有
`has_confirmed_assignee_evidence=true` 时才可展示申请人/权利人关联标签。

### 17.3.3 IPC质量、覆盖率与版本

2018 参照表中带 `*` 的 IPC 是官方标记的完全对应；未带 `*` 的为参照关系。
两者均进入基础覆盖统计，但通过 `complete_match_patent_count`、
`reference_match_only_patent_count` 和 `evidence_quality_status` 分开披露，不把非完全对应
冒充高置信证据。`evidence_quality_status` 只描述 IPC–产业映射质量，不描述机构关系类型；机构关系
类型必须读取 `relationship_evidence_status`。官方参照表基于 IPC 2018.1；首版通过 IPC 2026.01 真实父链展开，
无法在新 release 中找到的历史 IPC 保留在质量报告中，不执行字符串猜测。

v2 的 `mapping_coverage_rate` 分母是两类证据并集的全部关联专利组合单元，分子是其中至少映射一个
产业的组合单元。`total_confirmed_assignee_patent_count` 与
`total_inventor_affiliation_patent_count` 分别披露来源覆盖，但可能包含同一组合单元，不可直接相加
代替 `total_linked_patent_count`。所有来源 Snapshot、identity Snapshot、关系发布版本和指标版本
必须固定；任一来源变化都必须使用新数据版本重新发布。

`project_count` 只在已由专利证据建立的机构—产业 Key 内发布，不允许项目证据新增关系行。项目产业
证据固定为 Project/Grant → funded Work → 已发布RoS派生Patent–Work关系 → Google Patent IPC → 产业映射；
每格对 `project_id` 去重，发布完成后无命中写0。该证据表示项目受资助成果被该产业专利引用，不是
项目来源原生行业或项目直接专利产出。一个项目可进入多个产业及多个层级，所有产业行求和不得与
`ads_institution_profile.project_count` 直接对账。发布入口为
`./scripts/publish_institution_industry_project_count.sh run`。
发布入口为 `./scripts/publish_institution_industry_ads.sh config/institution_industry_ads_v2.json run`。

## 17.4 `ads_institution_technology_power`

一个具有发布 MVP core 论文证据的机构一行，用四个现有机构指标形成简单、可解释的科研技术力
MVP 分数。该分数只表示机构在固定 MVP 观察集合中的相对位置，不表示科研投入、专利所有权、
工程设施或产业化能力。

`institution_name_zh`只做展示冗余，不参与基准总体、标准化、评分或排名。发布必须按
`institution_id`从`ads_institution_profile.name_zh`复制所有非空中文名，不使用默认名称或机器翻译
填补来源空值；画像没有中文名时本字段保持NULL。机构画像中文名发生变化时，应以更高`data_version`
重新同步该快照。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与展示 | `institution_id` | `VARCHAR(64) NOT NULL` | 机构平台ID |
| Key 与展示 | `institution_name` | `STRING NOT NULL` | 机构当前发布名称快照 |
| Key 与展示 | `institution_name_zh` | `STRING` | 机构中文名称快照；冗余自`ads_institution_profile.name_zh`，来源无中文名时为空 |
| Key 与展示 | `institution_type_id` | `VARCHAR(32) NOT NULL` | 机构类型稳定代码 |
| 原始指标 | `paper_count` | `BIGINT NOT NULL` | 发布MVP core中的机构去重论文数 |
| 原始指标 | `cited_by_count` | `BIGINT NOT NULL` | 上述论文截至统计日的累计被引次数 |
| 原始指标 | `talent_count` | `BIGINT NOT NULL` | 上述论文关联的去重MVP人才数 |
| 原始指标 | `topic_count` | `BIGINT NOT NULL` | 机构学科画像中存在论文证据的去重Topic数 |
| 标准化分 | `paper_score` | `DECIMAL(9,6) NOT NULL` | 论文数量在固定合格机构总体中的0至100平均排名百分位分 |
| 标准化分 | `citation_score` | `DECIMAL(9,6) NOT NULL` | 累计被引在固定合格机构总体中的0至100平均排名百分位分 |
| 标准化分 | `talent_score` | `DECIMAL(9,6) NOT NULL` | 人才数量在固定合格机构总体中的0至100平均排名百分位分 |
| 标准化分 | `topic_score` | `DECIMAL(9,6) NOT NULL` | 专题数量在固定合格机构总体中的0至100平均排名百分位分 |
| 固定权重 | `paper_weight` | `DECIMAL(5,4) NOT NULL` | 论文分权重，MVP v1固定为0.3500 |
| 固定权重 | `citation_weight` | `DECIMAL(5,4) NOT NULL` | 被引分权重，MVP v1固定为0.3000 |
| 固定权重 | `talent_weight` | `DECIMAL(5,4) NOT NULL` | 人才分权重，MVP v1固定为0.2500 |
| 固定权重 | `topic_weight` | `DECIMAL(5,4) NOT NULL` | 专题分权重，MVP v1固定为0.1000 |
| 综合结果 | `technology_power_score` | `DECIMAL(9,6) NOT NULL` | 四项标准化分按固定权重加权得到的0至100技术力分 |
| 综合结果 | `technology_power_rank` | `BIGINT NOT NULL` | 技术力降序排名；同分依次按被引分、论文分、人才分和机构ID排序 |
| 综合结果 | `benchmark_institution_count` | `BIGINT NOT NULL` | 本指标版本中paper_count大于0的固定基准机构数 |
| 版本 | `metrics_as_of_date` | `DATE NOT NULL` | 输入机构指标统计截止日 |
| 版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 公式、总体、空值和排序规则版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级单调版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

四个原始指标定义如下：

- `paper_count`：发布 MVP core 中机构关联的去重论文数，直接使用同版本
  `ads_institution_profile.paper_count`。
- `cited_by_count`：上述论文截至 `metrics_as_of_date` 的累计被引次数，直接使用同版本机构画像；
  这是累计被引，不是论文在某一个自然年收到的 `citation_count`。
- `talent_count`：上述论文关联的去重 MVP 人才数，直接使用同版本机构画像。
- `topic_count`：从 `ads_institution_discipline_profile` 按机构去重 `topic_id` 得到，只表示有机构
  论文证据的 Topic 数量；该机构学科画像包含已发布 Topic 关系，不限于 Primary Topic。Topic
  关系缺失时按已确认的 0 处理。

### 基准总体和标准化公式

只有 `paper_count > 0` 的机构进入本指标版本的基准总体并发布评分行。基准总体在发布时固定，
其机构数写入每行 `benchmark_institution_count=N`；前端选择或取消机构不得触发重新标准化。

对任一原始指标 `X`，将全部合格机构按 `X` 从小到大排列。并列值使用其占据名次的平均值：

```text
average_rank_X(i) = (lowest_rank_X(i) + highest_rank_X(i)) / 2

score_X(i) =
    N = 1 时：100
    N > 1 时：100 * (average_rank_X(i) - 1) / (N - 1)
```

因此 `paper_score`、`citation_score`、`talent_score`、`topic_score` 均位于 0–100；相同原始值
必须得到相同的标准化分。该规则等价于发布 SQL 中由正序 `RANK()` 和倒序 `RANK()` 求平均并列
名次，不采用会随前端临时对比名单变化的局部 Min-Max。

### 技术力计算公式

`metric_definition_version='institution_technology_power_mvp_v1'` 的权重固定为：论文 0.35、
累计被引 0.30、人才 0.25、专题 0.10，权重之和必须为 1。前端可直接展示表内已计算结果；
如果前端复算，必须使用以下公式，不能对原始计数直接加权：

```text
technology_power_score =
      0.35 * paper_score
    + 0.30 * citation_score
    + 0.25 * talent_score
    + 0.10 * topic_score
```

综合分保留六位小数并限制在 0–100。`technology_power_rank` 按综合分降序产生；综合分相同时依次
比较 `citation_score DESC`、`paper_score DESC`、`talent_score DESC`、`institution_id ASC`，
因此排名稳定且唯一。`paper_count=0` 或未知的机构不发布评分行，而不是写入 0 分；已经确认没有
累计被引、人才或 Topic 关系时，对应原始指标为 0 并正常参与固定总体标准化。

建表迁移为
[`sql/doris/ads_schema_1_13_0_institution_technology_power.sql`](sql/doris/ads_schema_1_13_0_institution_technology_power.sql)，
发布 SQL 为
[`sql/doris/publish_institution_technology_power_mvp_v1.sql`](sql/doris/publish_institution_technology_power_mvp_v1.sql)，
运行和核验说明见
[`docs/institution_technology_power_mvp_v1.md`](docs/institution_technology_power_mvp_v1.md)。

## 17.5 `ads_talent_industry_activity`

一名人才在一个版本化产业节点一行，发布当前可由固定事实支持的产业技术活动 MVP。该表不把
授权率称为转化率，不把发明人称为专利权人，也不在缺少合同、许可、转让、产品化和收入事实时
生成商业价值。完整产业力字段继续保持 NULL，当前评分名称固定为“产业技术活动分”。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id` | `VARCHAR(64) NOT NULL` | 平台统一人才ID，逻辑关联 `ads_talent_profile.talent_id` |
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 产业分类体系稳定代码，首版固定为 `CN_GB4754_IPC` |
| Key | `industry_id` | `VARCHAR(64) NOT NULL` | 平台产业节点ID，逻辑关联同 taxonomy 的 `ads_industry.industry_id` |
| 产业快照 | `industry_code` | `VARCHAR(32) NOT NULL` | 产业来源代码快照，例如 GB/T 4754 代码 |
| 产业快照 | `industry_name_zh` | `VARCHAR(512) NOT NULL` | 产业官方中文名称快照 |
| 产业快照 | `industry_level` | `TINYINT NOT NULL` | 产业层级：1门类、2大类、3中类、4小类 |
| 专利规模 | `patent_family_count` | `BIGINT NOT NULL` | 人才在该产业关联的去重专利组合单元数；Google family优先，缺失时回退publication |
| 专利规模 | `granted_family_count` | `BIGINT NOT NULL` | 上述组合单元中至少一个publication存在授权日的数量；不表示当前仍有效 |
| 专利规模 | `recent_5y_family_count` | `BIGINT NOT NULL` | 统计截止年及前四年公开的去重专利组合单元数 |
| 专利分数计数 | `fractional_patent_count` | `DECIMAL(20,8) NOT NULL` | 按命中产业数及同组合单元已发布关联人才数分摊后的专利贡献 |
| 专利分数计数 | `fractional_granted_patent_count` | `DECIMAL(20,8) NOT NULL` | 已授权组合单元按相同规则分摊后的贡献 |
| 专利分数计数 | `fractional_recent_5y_patent_count` | `DECIMAL(20,8) NOT NULL` | 近五年组合单元按相同规则分摊后的贡献 |
| 成熟授权率 | `mature_application_family_count` | `BIGINT NOT NULL` | 申请日至统计截止日至少满三年的可评价专利组合单元数 |
| 成熟授权率 | `mature_granted_family_count` | `BIGINT NOT NULL` | 成熟可评价组合单元中至少一个publication已授权的数量 |
| 成熟授权率 | `patent_grant_rate` | `DECIMAL(12,8)` | `mature_granted_family_count / mature_application_family_count`；分母为0时为空，不是转化率 |
| 成熟授权率 | `smoothed_patent_grant_rate` | `DECIMAL(12,8)` | 使用强度10的同产业总体先验平滑后的成熟授权率；无成熟申请或产业先验时为空 |
| 项目背景 | `lead_project_count` | `BIGINT` | 已确认负责人或共同负责人项目数；直接项目源整体未覆盖时为空，不写0 |
| 项目背景 | `direct_project_count` | `BIGINT` | 已确认直接Investigator项目数；排除仅有受资助论文署名的推导关系，源未覆盖时为空 |
| 项目背景 | `project_attribution_status` | `VARCHAR(32) NOT NULL` | `TALENT_GLOBAL_CONTEXT`表示人才全局项目背景、未归因到本产业；不可计算时为`NOT_AVAILABLE` |
| 项目背景 | `project_metric_coverage_status` | `VARCHAR(32) NOT NULL` | 直接项目角色事实覆盖状态：`AVAILABLE`或`NOT_AVAILABLE` |
| 专利分项分 | `patent_family_score` | `DECIMAL(9,6) NOT NULL` | `fractional_patent_count`在固定产业基准总体中的0–100平均并列百分位分 |
| 专利分项分 | `patent_grant_count_score` | `DECIMAL(9,6) NOT NULL` | `fractional_granted_patent_count`在固定产业基准总体中的0–100平均并列百分位分 |
| 专利分项分 | `recent_patent_score` | `DECIMAL(9,6) NOT NULL` | `fractional_recent_5y_patent_count`在固定产业基准总体中的0–100平均并列百分位分 |
| 专利分项分 | `patent_grant_rate_score` | `DECIMAL(9,6)` | 平滑成熟授权率在有值人才中的0–100平均并列百分位分；不可评价时为空 |
| 专利评分 | `patent_metric_weight_coverage` | `DECIMAL(5,4) NOT NULL` | 专利活动公式实际可用权重之和；授权率可用时1.0000，否则0.7500 |
| 专利评分 | `patent_activity_score` | `DECIMAL(9,6) NOT NULL` | 专利族、授权族、近五年专利和平滑授权率分按固定权重归一后的0–100分 |
| 项目分项分 | `lead_project_score` | `DECIMAL(9,6)` | 负责人项目数在同产业候选人才中的0–100平均并列百分位分；项目源未覆盖时为空 |
| 项目分项分 | `direct_project_score` | `DECIMAL(9,6)` | 直接参与项目数在同产业候选人才中的0–100平均并列百分位分；项目源未覆盖时为空 |
| 项目评分 | `project_execution_score` | `DECIMAL(9,6)` | `0.70*lead_project_score + 0.30*direct_project_score`；任一必要分项不可用时为空 |
| 综合评分 | `activity_metric_weight_coverage` | `DECIMAL(5,4) NOT NULL` | 产业活动证据原始公式实际可用权重；项目可用时1.0000，否则0.6000 |
| 综合评分 | `research_foundation_score` | `DECIMAL(9,6) NOT NULL` | 论文数、被引、MVP core H指数和CWTS Core来源分得到的0–100论文科研基础分`Q` |
| 综合评分 | `industry_evidence_score` | `DECIMAL(9,6) NOT NULL` | 专利与可用项目证据分按产业基准人数向50收缩后的0–100产业活动证据分`I` |
| 综合评分 | `pre_gate_weighted_score` | `DECIMAL(9,6) NOT NULL` | 论文基础40%与产业证据60%的门槛前加权分：`0.40*Q+0.60*I` |
| 综合评分 | `academic_gate_score` | `DECIMAL(9,6) NOT NULL` | 论文科研基础对节点最终分的上限：`35+0.60*Q` |
| 综合评分 | `industry_activity_score` | `DECIMAL(9,6) NOT NULL` | `round(min(94.9,pre_gate_weighted_score,academic_gate_score),1)`；是人才在该产业节点的综合活动分，不是商业价值 |
| 综合排名 | `industry_activity_rank` | `BIGINT NOT NULL` | 同taxonomy release、同产业固定总体中的稳定唯一降序排名 |
| 综合排名 | `industry_activity_percentile` | `DECIMAL(9,6) NOT NULL` | 同产业固定总体中的0–100平均并列百分位，越大表示相对位置越高 |
| 综合排名 | `benchmark_talent_count` | `BIGINT NOT NULL` | 该产业评分与排名使用的固定基准人才数 |
| 商业化预留 | `commercialized_family_count` | `BIGINT` | 已核验发生许可、转让或产品化的专利组合单元数；当前无事实源，保持NULL |
| 商业化预留 | `commercialization_rate` | `DECIMAL(12,8)` | 已核验转化组合单元占具备观察条件组合单元的比例；当前保持NULL，不得用授权率代替 |
| 商业化预留 | `commercialization_score` | `DECIMAL(9,6)` | 转化成效标准化分；当前保持NULL且不参与MVP评分 |
| 商业价值预留 | `realized_commercial_value` | `DECIMAL(24,4)` | 已核验且已实现的许可、转让、里程碑或分成价值；当前保持NULL，不由专利数量推测 |
| 商业价值预留 | `commercial_value_currency` | `VARCHAR(3)` | 已实现商业价值的基准ISO 4217币种；价值为空时同样为空 |
| 商业价值预留 | `commercial_value_score` | `DECIMAL(9,6)` | 已实现商业价值标准化分；当前保持NULL且不参与MVP评分 |
| 覆盖状态 | `commercialization_coverage_status` | `VARCHAR(32) NOT NULL` | 商业转化事实覆盖状态；当前固定为`NOT_AVAILABLE` |
| 覆盖状态 | `commercial_value_coverage_status` | `VARCHAR(32) NOT NULL` | 已实现商业价值事实覆盖状态；当前固定为`NOT_AVAILABLE` |
| 产业版本 | `taxonomy_release_id` | `VARCHAR(64) NOT NULL` | 产业分类体系不可变发布版本，首版为`2018` |
| 输入版本 | `patent_mapping_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定IPC–产业展开映射Iceberg Snapshot ID |
| 统计版本 | `metrics_as_of_date` | `DATE NOT NULL` | 专利与指标统计截止日 |
| 统计版本 | `score_version` | `VARCHAR(64) NOT NULL` | 评分模型版本，当前固定为`talent_industry_activity_mvp_v2` |
| 统计版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 原始指标、归一化、权重和覆盖处理的口径版本 |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 同一人才—taxonomy—产业Key的单调发布版本；重试保持一致 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | 本批ADS记录的确定性UTC生成时间 |

专利优先按 Google family ID 去重，缺失时回退 publication ID。同一专利组合单元命中多个四位
产业时按产业分数计数；同一组合单元关联多个已发布人才时再按人才数分摊。向产业父层汇总时对
叶子贡献求和，不重复放大一个组合单元。

成熟授权率只评价申请日早于统计截止日三年的组合单元：

```text
patent_grant_rate = mature_granted_family_count / mature_application_family_count

smoothed_patent_grant_rate =
    (mature_granted_family_count + 10 * industry_prior_grant_rate)
    / (mature_application_family_count + 10)
```

没有成熟申请时两项授权率及授权率分均为 NULL。授权率不是专利转化率。

各原始指标在固定 `taxonomy_id + taxonomy_release_id + industry_id` 基准总体中使用平均并列
排名转为 0–100 分。专利活动分为：

```text
patent_activity_score =
    (0.25 * patent_family_score
   + 0.30 * patent_grant_count_score
   + 0.20 * recent_patent_score
   + 0.25 * patent_grant_rate_score [仅在非NULL时参与])
    / patent_metric_weight_coverage
```

`patent_metric_weight_coverage` 在授权率可评价时为 `1.0000`，否则为 `0.7500`。项目只接受
`ads_talent_project.is_lead=true` 或 `is_direct_investigator=true` 的直接关系；
`funded_output_author` 不冒充项目成员。当前缺少可靠 Project–Industry 事实，因此项目指标在存在
直接关系源覆盖时也只能作为人才的全局项目执行背景，
`project_attribution_status='TALENT_GLOBAL_CONTEXT'`，不能展示为该产业项目数。若整个发布中没有
任何直接项目关系，则项目计数和分数保持 NULL，两个项目状态均为 `NOT_AVAILABLE`：

```text
project_execution_score = 0.70 * lead_project_score + 0.30 * direct_project_score

raw_industry_evidence_score =
    (0.60 * patent_activity_score
   + 0.40 * project_execution_score [仅在非NULL时参与])
    / activity_metric_weight_coverage
```

`activity_metric_weight_coverage` 在项目直接事实可用时为 `1.0000`，否则为 `0.6000`。当前发布的
`ads_talent_project` 全部为 `funded_output_author`，所以项目维度保持未知，当前原始产业证据分等于专利
活动分；不得把项目计数写成 0 或生成虚假的中位项目分。

v2对原始产业证据分进行小样本收缩，并引入与人才级产业力相同的论文科研基础`Q`：

```text
research_foundation_score Q =
    (0.15 * paper_score
   + 0.35 * citation_score
   + 0.35 * h_index_score
   + 0.15 * core_source_score [仅在非NULL时参与])
    / (0.85 + 0.15 [仅在core_source_score非NULL时参与])

reliability = min(1, sqrt(benchmark_talent_count / 100))
industry_evidence_score I =
    50 + reliability * (raw_industry_evidence_score - 50)

pre_gate_weighted_score = 0.40 * Q + 0.60 * I
academic_gate_score = 35 + 0.60 * Q

industry_activity_score =
    round(min(94.9, pre_gate_weighted_score, academic_gate_score), 1)
```

收缩使只有1名候选人才的节点100原始证据分降为55；基准总体达100人时不再收缩。
最终分保留一位小数且上限为94.9，不再产生99.x或100分。`industry_activity_rank`和
`industry_activity_percentile`在同产业内按v2最终分重算；原始分项、`patent_activity_score`和项目分仍保留作为解释证据。

`score_version='talent_industry_activity_mvp_v2'`。这不是完整商业价值评分。商业化六个数值字段在
接入已核验转化与收入事实前全部保持 NULL，两个覆盖状态固定为 `NOT_AVAILABLE`，不允许填 0，
也不允许把缺失的商业化权重重分配到当前分数。

迁移、发布、配置和运行说明分别为
[`sql/doris/ads_schema_2_2_0_talent_industry_activity.sql`](sql/doris/ads_schema_2_2_0_talent_industry_activity.sql)、
[`sql/doris/publish_talent_industry_activity_mvp_v1.sql`](sql/doris/publish_talent_industry_activity_mvp_v1.sql)、
[`config/talent_industry_activity_mvp_v1.json`](config/talent_industry_activity_mvp_v1.json) 和
[`docs/talent_industry_activity_mvp_v1.md`](docs/talent_industry_activity_mvp_v1.md)。

## 17.6 `ads_technology_commercial_value_simulation`

一个固定技术目录中的技术在一个模拟版本一行。该表只承载可复现的情景值，所有行显式标记
`value_nature='SYNTHETIC_SIMULATION'`、`is_synthetic=true`，不得解释为许可、转让、产品收入或
估值事实，也不得写入 `ads_talent_industry_activity` 的正式商业价值预留字段。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `catalog_release_id` | `VARCHAR(64) NOT NULL` | 不可变技术目录发布ID |
| Key | `tech_id` | `VARCHAR(64) NOT NULL` | 固定目录内稳定技术ID |
| Key | `simulation_version` | `VARCHAR(64) NOT NULL` | 模拟算法与口径版本 |
| 名称快照 | `technology_name_zh` | `VARCHAR(512) NOT NULL` | 固定目录中文名称快照 |
| 名称快照 | `technology_name_en` | `VARCHAR(512) NOT NULL` | 固定目录英文名称快照 |
| 模拟值 | `synthetic_commercial_value_score` | `DECIMAL(9,6) NOT NULL` | 由固定种子与稳定技术ID生成的0–100确定性伪随机分；不是真实商业价值 |
| 生成规则 | `generation_method` | `VARCHAR(64) NOT NULL` | 固定为 `SHA256_U64_UNIFORM_0_100` |
| 生成规则 | `simulation_seed` | `VARCHAR(128) NOT NULL` | 非秘密固定种子，用于完全复算 |
| 映射覆盖 | `formal_patent_mapping_count` | `INT NOT NULL` | 固定 mapping release 中该技术的已批准 IPC/CPC 映射数 |
| 映射覆盖 | `talent_rollup_eligibility` | `VARCHAR(32) NOT NULL` | `ELIGIBLE` 或 `NO_FORMAL_PATENT_MAPPING` |
| 数据性质 | `value_nature` | `VARCHAR(32) NOT NULL` | 固定为 `SYNTHETIC_SIMULATION` |
| 数据性质 | `is_synthetic` | `BOOLEAN NOT NULL` | 固定为 `true` |
| 输入版本 | `mapping_release_id` | `VARCHAR(64) NOT NULL` | 人才聚合使用的正式映射发布ID |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调版本 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

生成公式为 `SHA256(simulation_seed | catalog_release_id | tech_id)`，取摘要前8字节无符号整数，
除以 `2^64-1` 后乘100并四舍五入至六位小数。固定输入必得固定结果，不依赖执行顺序。

## 17.7 `ads_talent_industry_capability_simulation`

一名人才在一个产业节点、一个模拟版本一行。4.1.0 将原技术映射路径与确定性兜底路径合并为
一个全量覆盖模拟方案；同一 `simulation_version` 内每条正式产业活动记录都产生模拟商业价值分、
综合分、排名和百分位，不再因为技术映射缺失而留下 NULL。

有技术映射时，人才—技术关联不随机生成：只接受固定发布的 IPC/CPC `RELATED` 映射，并要求同一件
已发布专利同时命中技术分类与产业分类；技术模拟分按人才—产业—技术命中的去重专利组合单元数
加权。没有命中正式技术映射时，不伪造技术关系，`matched_technology_count` 和
`matched_technology_family_count` 仍为 0；仅以固定种子及人才—产业稳定 Key 生成可复算的兜底情景分。
两种路径都属于合成模拟，不是商业化事实，正式表不回填。
为兼容已发布 Doris 表，四个历史可空数值列继续保留物理 `NULL` 类型；4.1.0 发布契约要求它们
逻辑非空，Pipeline 在发布后逐列校验，任何 NULL 都使任务失败。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id` | `VARCHAR(64) NOT NULL` | 平台统一人才ID |
| Key | `taxonomy_id` | `VARCHAR(64) NOT NULL` | 产业分类体系ID |
| Key | `industry_id` | `VARCHAR(64) NOT NULL` | 产业节点ID |
| Key | `simulation_version` | `VARCHAR(64) NOT NULL` | 模拟算法与口径版本 |
| 产业快照 | `industry_code` | `VARCHAR(32) NOT NULL` | 产业代码快照 |
| 产业快照 | `industry_name_zh` | `VARCHAR(512) NOT NULL` | 产业中文名快照 |
| 产业快照 | `industry_level` | `TINYINT NOT NULL` | 产业层级 |
| 正式输入 | `official_industry_activity_score` | `DECIMAL(9,6) NOT NULL` | 原样引用的正式产业技术活动分，不被模拟结果覆盖 |
| 技术覆盖 | `matched_technology_count` | `INT NOT NULL` | 同一专利经正式IPC/CPC映射命中的去重技术数 |
| 技术覆盖 | `matched_technology_family_count` | `BIGINT NOT NULL` | 技术—专利组合单元配对去重后的计数 |
| 模拟值 | `synthetic_commercial_value_score` | `DECIMAL(9,6)` | 0–100且逻辑非空；有映射时按技术命中组合单元数加权，无映射时使用确定性哈希兜底 |
| 权重 | `activity_weight` | `DECIMAL(5,4) NOT NULL` | 正式产业技术活动分权重，首版0.7500 |
| 权重 | `commercial_value_weight` | `DECIMAL(5,4) NOT NULL` | 模拟技术商业价值分权重，首版0.2500 |
| 模拟结果 | `simulated_industry_capability_score` | `DECIMAL(9,6)` | 逻辑非空；`0.75*正式活动分 + 0.25*模拟商业价值分`，仅供情景分析 |
| 模拟结果 | `simulated_industry_capability_rank` | `BIGINT` | 逻辑非空；同产业全量模拟总体中的稳定唯一排名 |
| 模拟结果 | `simulated_industry_capability_percentile` | `DECIMAL(9,6)` | 逻辑非空；同产业全量模拟总体中的0–100平均并列百分位 |
| 模拟结果 | `simulation_benchmark_talent_count` | `BIGINT NOT NULL` | 同产业全量模拟基准人才数，与该产业正式活动行数一致 |
| 覆盖状态 | `simulation_coverage_status` | `VARCHAR(40) NOT NULL` | `TECHNOLOGY_WEIGHTED` 或 `DETERMINISTIC_HASH_FALLBACK`，说明分数生成路径而非事实覆盖率 |
| 数据性质 | `value_nature` | `VARCHAR(32) NOT NULL` | 固定为 `SYNTHETIC_SIMULATION` |
| 数据性质 | `is_synthetic` | `BOOLEAN NOT NULL` | 固定为 `true` |
| 输入版本 | `catalog_release_id` | `VARCHAR(64) NOT NULL` | 固定技术目录发布ID |
| 输入版本 | `mapping_release_id` | `VARCHAR(64) NOT NULL` | 固定正式分类映射发布ID |
| 输入版本 | `patent_mapping_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定IPC—产业映射Iceberg Snapshot ID |
| 输入版本 | `base_score_version` | `VARCHAR(64) NOT NULL` | 正式产业技术活动输入评分版本 |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调版本 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

统一模拟方案的计算规则如下：

```text
if matched_technology_count > 0:
    synthetic_commercial_value_score =
        sum(technology_family_count * technology_synthetic_score)
        / sum(technology_family_count)
    simulation_coverage_status = TECHNOLOGY_WEIGHTED
else:
    hash_input = simulation_seed | talent_id | taxonomy_id | industry_id
    hash_value = SHA256(hash_input) 的前 60 bit 无符号整数
    synthetic_commercial_value_score = 100 * hash_value / (2^60 - 1)
    simulation_coverage_status = DETERMINISTIC_HASH_FALLBACK

simulated_industry_capability_score =
    0.75 * official_industry_activity_score
  + 0.25 * synthetic_commercial_value_score
```

兜底哈希只生成数值，不生成技术命中、专利关系或商业化事实。排名在同一
`taxonomy_id + industry_id` 的全部正式活动人才中计算；综合分相同时依次按正式活动分降序、
`talent_id` 升序产生稳定唯一排名。平均并列百分位允许同分人才取得相同百分位。

当前统一发布继续使用
`simulation_version='talent_industry_commercial_value_simulation_v1'`，并以
`data_version=202611040301`引用`base_score_version='talent_industry_activity_mvp_v2'`覆盖该模拟版本旧行；
1,777行走技术加权路径，其余396,187行走确定性兜底路径。发布必须对账397,964条正式活动输入与模拟输出，并校验所有
模拟分、综合分、排名和百分位非空且在合法范围。这里的数量是本次固定发布事实，后续输入版本变化
必须在发布报告中记录新数量，不得把它当作永久 Schema 常量。

模拟表与正式表物理隔离，正式 `commercial_value_score`、`realized_commercial_value`、
`industry_activity_score` 及正式排名不更新。迁移、发布模板、配置及运行说明见
[`sql/doris/ads_schema_2_3_0_talent_industry_simulation.sql`](sql/doris/ads_schema_2_3_0_talent_industry_simulation.sql)、
[`sql/doris/publish_talent_industry_simulation_v1.sql`](sql/doris/publish_talent_industry_simulation_v1.sql)、
[`config/talent_industry_commercial_value_simulation_v1.json`](config/talent_industry_commercial_value_simulation_v1.json) 和
[`docs/talent_industry_commercial_value_simulation_v1.md`](docs/talent_industry_commercial_value_simulation_v1.md)。

## 17.8 `ads_talent_industrial_capability_result`

一名人才在一个不可变模型版本一行，将全体人才的论文科研基础与已发布人才—产业活动证据
聚合为人才级产业力综合分。该分数是可解释的产业研究与技术活动指标，不是已实现商业价值、
专利转化率、产品收入或任职于产业界的证明。完整版本结果保存于本表，当前版本便利字段投影到
`ads_talent_profile`。

| 字段 | Doris类型 | 说明 |
|---|---|---|
| `talent_id` | `VARCHAR(64) NOT NULL` | 平台统一人才ID |
| `model_version` | `VARCHAR(64) NOT NULL` | 不可变模型版本，首版为`talent_industrial_capability_research_industry_v1` |
| `research_foundation_score` | `DECIMAL(9,6) NOT NULL` | 全体人才均有的0–100论文科研基础分`Q` |
| `industry_evidence_score` | `DECIMAL(9,6)` | 有产业证据人才的0–100汇总分`I`；无证据为NULL |
| `pre_gate_weighted_score` | `DECIMAL(9,6)` | 有产业证据时`0.40*Q+0.60*I`；无证据时为NULL |
| `academic_gate_score` | `DECIMAL(9,6)` | 有产业证据时的论文质量上限`35+0.60*Q`；无证据时为NULL |
| `industrial_capability_score` | `DECIMAL(9,6) NOT NULL` | 最终0–94.9产业力综合分，保留一位小数 |
| `industrial_capability_level` | `VARCHAR(32) NOT NULL` | 按固定阈值生成的七档分类代码 |
| `evidence_status` | `VARCHAR(32) NOT NULL` | `RESEARCH_ONLY`或`INDUSTRY_EVIDENCE` |
| `primary_industry_id` | `VARCHAR(64)` | 收缩分最高的二级产业ID；无产业证据为NULL |
| `source_industry_count` | `INT NOT NULL` | 参与汇总的二级产业数；无产业证据为0 |
| `strong_industry_count` | `INT NOT NULL` | 收缩分不低于70的二级产业数 |
| `research_metrics_as_of_date` | `DATE NOT NULL` | 论文科研基础输入统计截止日 |
| `industry_metrics_as_of_date` | `DATE` | 产业活动输入统计截止日；无产业证据为NULL |
| `source_academic_score_version` | `VARCHAR(64) NOT NULL` | 论文分项输入的学术评分版本 |
| `source_industry_score_version` | `VARCHAR(64)` | 产业活动输入评分版本；无产业证据为NULL |
| `metric_definition_version` | `VARCHAR(64) NOT NULL` | 公式、权重、阈值和覆盖处理口径版本 |
| `data_version` | `BIGINT NOT NULL` | 同一业务Key单调版本，重试保持一致 |
| `update_time` | `DATETIME(3) NOT NULL` | 确定性UTC生成时间 |

### 17.8.1 论文科研基础分

为避免把论文数量或合作广度直接等同于论文水平，`Q`不直接复用`academic_capability`，而使用
已发布的四个标准化分项：

```text
research_foundation_score Q =
    (0.15 * paper_score
   + 0.35 * citation_score
   + 0.35 * h_index_score
   + 0.15 * core_source_score [仅在非NULL时参与])
    /
    (0.85 + 0.15 [仅在core_source_score非NULL时参与])
```

`paper_score`、`citation_score`、`h_index_score`任一为NULL时发布失败，不静默降低论文质量权重。
`core_source_score`无可评价来源时允许为NULL，其余0.85权重归一化。

### 17.8.2 产业活动证据分

当前模型固定使用`CN_GB4754_IPC/2018`分类体系的二级产业节点，不同时聚合门类、中类和小类，
避免同一专利贡献在父子节点重复累加。v2节点表已经将原始专利/项目分按基准人数向50收缩，因此人才级汇总
直接读取`ads_talent_industry_activity.industry_evidence_score`，不对`industry_activity_score`再次收缩，也不重复引入论文门槛。
按产业证据分降序、
`benchmark_talent_count DESC`、`industry_id ASC`稳定排序，取前三个节点：

```text
top3_score = weighted_average(top1, top2, top3; weights=0.60,0.30,0.10)
```

不足三个节点时只对实际存在权重归一化。设收缩分不低于70的二级产业数为`K`：

```text
breadth_bonus = min(5, 1.8 * log2(1 + K))
industry_evidence_score I = min(100, top3_score + breadth_bonus)
```

### 17.8.3 人才级综合分与档位

无产业活动证据时不设置固定保底分，而是按论文科研基础连续评分，并将上限限制在60分以下：

```text
if evidence_status = RESEARCH_ONLY:
    industrial_capability_score = round(0.60 * Q, 1)
```

有产业活动证据时，论文科研基础占40%，产业活动证据占60%，同时论文科研基础构成显式上限：

```text
pre_gate_weighted_score = 0.40 * Q + 0.60 * I
academic_gate_score = 35 + 0.60 * Q

industrial_capability_score =
    round(min(94.9, pre_gate_weighted_score, academic_gate_score), 1)
```

因此`Q=20/40/60/80/100`时，即使产业活动证据分极高，最终分也分别不得超过
`47/59/71/83/94.9`。当前档位固定为：

| 分数范围 | `industrial_capability_level` | 中文含义 |
|---|---|---|
| 0–19.9 | `WEAK` | 产业基础较弱 |
| 20–39.9 | `POTENTIAL_FOUNDATION` | 产业潜在基础 |
| 40–59.9 | `RESEARCH_FOUNDATION` | 产业研究基础 |
| 60–69.9 | `INITIAL` | 初步产业能力 |
| 70–79.9 | `STRONG` | 产业能力较强 |
| 80–89.9 | `OUTSTANDING` | 产业能力突出 |
| 90–94.9 | `LEADING` | 产业能力领先 |

档位不代替`evidence_status`。`RESEARCH_ONLY`人才不得在产品中展示为已有产业活动；排名、筛选和解释必须
允许按证据状态区分。发布必须覆盖全部`ads_talent_profile`业务Key，检查分数范围、分支公式、主产业归属、输入版本、
主画像投影一致性和无孤儿。

迁移、发布模板、配置和运行说明分别为
[`sql/doris/ads_schema_9_3_0_talent_industrial_capability.sql`](sql/doris/ads_schema_9_3_0_talent_industrial_capability.sql)、
[`sql/doris/publish_talent_industrial_capability_v1.sql`](sql/doris/publish_talent_industrial_capability_v1.sql)、
[`config/talent_industrial_capability_v1.json`](config/talent_industrial_capability_v1.json) 和
[`docs/talent_industrial_capability_v1.md`](docs/talent_industrial_capability_v1.md)。

## 18. Project ADS

`ads_project_profile` 是 project 主体表，平台 ID 使用与来源解耦的 `prj_<uuid32>`，OpenAlex
Grant ID 只通过 identity bridge 映射。开始年优先采用来源 `start_year`，缺失时采用 MVP
受资助论文最早发表年，并通过 `start_year_source` 和 `start_year_is_inferred` 明示推测性质。
`funder_project_id` 使用 `STRING` 原样保留来源中可能拼接的多个资助方项目编号，不截断。
`talent_count` 从发布的 `ads_talent_project` 按 `project_id` 去重计算；已确认没有发布关系时写 0。
`name_zh` 使用中文细粒度倒排全文索引，中文项目名称回填后可使用 Doris `MATCH_ANY`、
`MATCH_ALL` 或 `MATCH_PHRASE` 检索；索引不改变名称来源、项目身份或数据版本。
`name` 与 `description` 承载来源原文，允许中文、英文、日文及混合语言，统一使用 ICU 多语言
倒排全文索引；应用不得假定这两个字段只有英文。变更分词器必须重建对应索引。

项目金额保留来源`amount`和`currency`，同时发布`amount_cny`及逐行汇率审计字段：

| 字段 | Doris类型 | 说明 |
|---|---|---|
| `amount_cny` | `DECIMAL(24,4)` | 来源金额固定汇率换算值，或缺失时的确定性模拟人民币金额 |
| `amount_cny_exchange_rate` | `DECIMAL(18,8)` | 1单位原币对应人民币元数 |
| `amount_cny_exchange_rate_date` | `DATE` | 该币种汇率快照日期 |
| `amount_cny_exchange_rate_source` | `VARCHAR(64)` | 操作方提供的汇率来源类型 |
| `amount_cny_normalization_status` | `VARCHAR(40)` | `CONVERTED_TO_CNY_FIXED_RATE/INVALID_AMOUNT/CURRENCY_MISSING/FX_RATE_MISSING`；没有来源金额时为空 |
| `amount_cny_conversion_policy` | `VARCHAR(64)` | 当前为`FIXED_SNAPSHOT_CNY_PER_CURRENCY_UNIT_V2`；仅成功换算时填写 |
| `amount_cny_value_type` | `VARCHAR(48) NOT NULL` | `SOURCE_CONVERTED`为来源换算，`SIMULATED_SHENZHEN_MEDIAN_V1`为原深圳范围模拟，`SIMULATED_GLOBAL_SHENZHEN_MEDIAN_V1`为同规则全库扩展 |

固定汇率如下；均为“1单位原币对应人民币元数”：

| 汇率日期 | 币种与汇率 |
|---|---|
| `2026-10-23` | USD 6.7180；EUR 7.5140；JPY 0.042793；CHF 8.1710；CAD 4.7804；AUD 4.6982 |
| `2026-10-27` | GBP 8.9349；DKK 0.9984；SEK 0.6699；CZK 0.3059；CLP 0.006746 |

`amount<=0`固定标记为`INVALID_AMOUNT`且`amount_cny=NULL`。`amount_cny`上的倒排索引用于等值和范围
过滤；Doris的`ORDER BY amount_cny`仍执行TopN/排序，不能把倒排索引解释为物理排序索引。该固定快照
是名义金额横向换算，不代表项目发生年份的历史汇率或购买力。

6.17.0只在Doris Serving层为当前深圳统一城市ID关联且`amount_cny`缺失的项目补充模拟人民币金额。
基准中位数固定为当前2,063个来源换算项目的`581,984.8125`元；按`project_id`与固定seed的CRC32
确定性生成0.8000至1.2000系数，因此同一项目重跑结果不变。模拟值只写`amount_cny`，不修改来源
`amount`、`currency`、汇率及归一状态。聚合和导出必须同时返回`amount_cny_value_type`，不得把
`SIMULATED_SHENZHEN_MEDIAN_V1`解释为真实拨款、项目承担金额或财政投入事实。

8.4.0对剩余全部`amount_cny IS NULL`项目使用同一冻结中位数和±20%确定性哈希规则，
标记为`SIMULATED_GLOBAL_SHENZHEN_MEDIAN_V1`。该扩展只提供可比分析的模拟代理金额，不提高来源
经费覆盖率；任何展示和聚合必须同时区分`SOURCE_CONVERTED`和两种`SIMULATED_*`类型。

### 18.1 深圳机构学科与研究方向项目关联资金

`ads_shenzhen_institution_field_funding`按`institution_id, field_id`物化Field概览；
`ads_shenzhen_institution_direction_funding`按`institution_id, primary_topic_id`物化研究方向明细，并
携带Topic所属Subfield和Field。每个项目只使用`ads_project_topic.is_primary=true`的唯一Topic，避免
普通Topic多值造成金额重复。

项目可能关联多家机构。发布先对至少关联一家深圳机构的项目读取全部机构关系，再按机构
`evidence_paper_count`占项目全部机构证据数的比例分配金额；全部证据数为0时才等分。非深圳机构参与
分母后再过滤深圳机构，禁止把跨城项目全额归给深圳。Field表从方向表聚合，不独立重算来源，必须按
机构和Field对账项目数、方向数、合计金额、真实金额和模拟金额。

两表分别保存`real_amount_cny`和`simulated_amount_cny`，`allocated_amount_cny`严格等于二者之和；
`amount_scope_status`固定为`PROJECT_RELATED_NOT_DISBURSEMENT`。完整字段、公式、前端查询、发布结果和
恢复命令见
[`docs/shenzhen_institution_funding_ads_v1.md`](docs/shenzhen_institution_funding_ads_v1.md)。

`ads_talent_project` 是人才与科研项目的完整 ADS 关系入口，粒度为一名人才关联一个项目一行，
逻辑主键为 `talent_id, project_id`。字段如下：

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key 与类型 | `talent_id` | `VARCHAR(64) NOT NULL` | 平台统一人才ID |
| Key 与类型 | `project_id` | `VARCHAR(64) NOT NULL` | 平台统一科研项目ID |
| Key 与类型 | `relation_type` | `VARCHAR(64) NOT NULL` | direct_investigator/direct_and_funded_output/funded_output_author |
| 直接角色 | `investigator_role_codes` | `ARRAY<VARCHAR(32)>` | 来源确认角色lead/co_lead/investigator；推导关系为空 |
| 直接角色 | `is_direct_investigator` | `BOOLEAN NOT NULL` | 是否来自已确认Author-Grant对齐 |
| 直接角色 | `is_lead` | `BOOLEAN NOT NULL` | 是否存在已确认负责人角色；推导关系不得置真 |
| 匹配质量 | `match_method` | `VARCHAR(64) NOT NULL` | 直接身份对齐方法或mvp_funded_paper_authorship |
| 匹配质量 | `match_confidence` | `DECIMAL(5,4)` | 身份或关系匹配置信度 |
| 匹配质量 | `verified_status` | `VARCHAR(32)` | unverified/verified/disputed；仅直接关系适用 |
| 论文证据 | `funded_paper_count` | `BIGINT NOT NULL` | 该人才在该项目下的MVP受资助论文数 |
| 论文证据 | `first_evidence_year` | `SMALLINT` | 最早受资助论文年份 |
| 论文证据 | `latest_evidence_year` | `SMALLINT` | 最近受资助论文年份 |
| 版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 关系口径版本 |
| 版本 | `data_version` | `BIGINT NOT NULL` | Key级数据版本 |
| 版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`relation_type` 固定为 `direct_investigator`、`direct_and_funded_output` 或
`funded_output_author`。前两者必须存在 `dwd_author_grant` 的已对齐事实；
`funded_output_author` 仅表示该人才署名了项目资助的 MVP 论文，不表示其为负责人或正式成员，
因此 `is_direct_investigator=false`、`is_lead=false` 且角色数组为空。直接关系与论文关系并存时
合并为一行并保留两类证据。

`ads_talent_profile.project_ids/projects/project_count` 必须从本表同步生成：`project_ids` 保存完整
去重关系，`projects` 仅保存确定性排序后的 Top 20 展示快照。`ads_project_profile.talent_count`
同样从本表生成。`ads_talent_yearly_metrics.project_count` 按项目 `effective_start_year` 统计；
缺少有效开始年的关系只进入累计画像，不虚构年度。

`ads_project_institution` 保存项目与机构多对多关系。优先使用来源 OpenAlex Institution、ROR、
唯一精确名称；一个项目完全没有直接匹配时，才以受资助论文作者机构兜底。

`ads_project_topic` 保存项目与 Topic 多对多关系，支持 project → topic，并通过 `topic_id` 倒排
索引支持 topic → project。当前旧 Awards Snapshot 没有来源 Topic，因此按关联 MVP 论文中
Topic 的去重论文出现次数降序排名；第一名为 Primary Topic。并列时依次比较平均 Topic score，
仍并列则使用 `grant_id + topic_id` 稳定哈希作确定性伪随机裁决，禁止真正随机导致跨批次漂移。

### 18.2 完美数据原表补充发布（9.10.0）

9.10.0将首版完美数据直接补充到既有`ads_talent_profile`、`ads_institution_profile`、
`ads_project_profile`和`ads_talent_project`，不创建平行实体表，也不改变前端按原实体表读取详情的
路径。发布ID为`perfect_data_v1_20261106`，固定覆盖15名人才、26家机构和38个项目。原有
`relation_type`、`verified_status`及其他事实字段保持不变；新增字段只承载详情内容、前端标签和
补充数据的后台治理信息。该发布不得反向更新DWD。

四张原表统一增加`is_perfect_data`、`perfect_data_release_id`、
`perfect_data_review_status`、`perfect_data_value_nature`和`perfect_data_version`。这些字段用于明确
本批数据的名单、版本和策展/推测性质，不要求前端另行分流。首版审核状态为
`APPROVED_FOR_SHOWCASE_BY_OPERATOR_RULE`，表示操作方批准补齐规则，不表示逐条人工事实核验。

#### 18.2.1 人才与人才—项目角色

15名人才直接在`ads_talent_profile`标记为完美数据。49条选定关系仍存于`ads_talent_project`；新增
`frontend_role`与`frontend_role_label`。只有官方直接证据明确为负责人或共同负责人才分别写
`lead`或`co_lead`，其余写`project_member/项目成员`。`funded_output_author`不得因此变为直接项目
事实，`unverified`也不得自动提升。资助方与个人CV冲突时以资助方为准；当前网页与历史档案冲突时
以当前网页为主；已结束项目保留历史角色，不按当前机构反推历史关系。

#### 18.2.2 机构简介与典型案例

26家机构使用`ads_institution_profile.description`保存一段200至300字中文简介，并在新增JSON字段
`typical_cases`中保存固定四类案例：`SCIENTIFIC_BREAKTHROUGH`、`TECHNOLOGY_TRANSFER`、
`MAJOR_RESEARCH_PROGRAM`和`SOCIAL_IMPACT`。每个案例均含标题、摘要、关联实体、来源URL、
`relation_strength`与`is_synthetic`。优先从既有代表论文、代表专利、关联项目和机构新闻派生；缺失
时允许`SYNTHETIC_FALLBACK`补齐，但必须在JSON内部保留标记。

#### 18.2.3 项目详情、阶段成果与关联专利

38个项目继续使用`ads_project_profile`。`name_zh`和`description_zh`分别承载中文名称与项目背景；
新增`research_objectives_zh`、`technical_route_zh`、`result_summary_zh`保存研究目标、技术路线与
成果摘要。`stage_results`为JSON数组，每项目固定三阶段：方案设计、研究实施和成果形成，各阶段均有
期间、目标、成果和`evidence_nature`。
首版重点项目的`name_zh`只保留中文方向名称或已有中文专名，不在中文字段后拼接来源英文项目名；
来源原名继续由`name`和`name_original`保留。同一方向下的多个项目允许共用同一中文展示名，身份仍以`project_id`为准。

`related_patents`为JSON数组，`related_patent_count`为对应计数。每项目固定5族代表专利，每个元素
包含专利ID、标题、排序、后台关系类型、前端标签、关联理由、技术转化金额及金额性质。后台允许
`DIRECT`、`SUPPORTED`和`INFERRED_CANDIDATE`，前端统一显示“关联专利”。首版190条均为
`INFERRED_CANDIDATE`。金额缺失时按`project_id + patent_id`稳定哈希生成50万至500万元，并标记
`SIMULATED_RULE_V1`；前端只能称为模拟技术转化金额。

#### 18.2.4 完整性验收与旧表清理

发布必须满足：15名人才、26家机构和38个项目均在原表可定位；机构简介字数为200至300且每家4个
案例；项目名称、背景、目标、路线和成果摘要均非空；每项目3个阶段、5族专利；人才—项目前端角色
非空。原地写入通过后，精确移除历史试运行创建的7张`ads_showcase_*`表，最终数据库中该前缀表数
必须为0。配置、发布入口和最终完整名单分别为
[`config/showcase_enrichment_v1.json`](config/showcase_enrichment_v1.json)、
[`scripts/publish_showcase_enrichment_v1.sh`](scripts/publish_showcase_enrichment_v1.sh)和
[`reports/perfect_data_v1_20261106/publication_report.md`](reports/perfect_data_v1_20261106/publication_report.md)。

### 18.3 重点技术交叉关联矩阵与详情（9.11.0）

9.11.0从`ads_technology_graph_edge`固定挑选30条重点技术交叉关联，覆盖首版完美数据的10个主题，
每个主题3条。筛选只接受`evidence_level=HIGH`、共同专利3至50件、两端中文名称和年度论文数据完整
且2020—2022基线论文数大于0的边；优先选择与既有38个重点项目或26家重点机构有真实ADS关联的
候选，不为满足覆盖而伪造项目或机构关系。发布ID继续使用`perfect_data_v1_20261106`。

矩阵直接读取`ads_technology_graph_edge`新增字段。`association_score`复制固定边的
`relation_confidence_score`，便于前端稳定取数，但仍是同关系类型内可比较的启发式分数，不是事实概率。
强度等级按分数确定：90及以上为`VERY_HIGH/极强`，75至90为`HIGH/强`，低于75的已选高证据边为
`MEDIUM_HIGH/中高`。`paper_growth_rate=(recent_paper_count-baseline_paper_count)/
baseline_paper_count`；基线和近期分别是两端技术在2020—2022、2023—2025三个完整自然年的论文数
之和，因此前端显示百分比时乘100。`total_paper_count`为两端全观察期论文数之和，可能包含两端共同论文，
不得解释为去重组合论文数。

#### 18.3.1 `ads_technology_graph_edge`新增展示与治理字段

| 字段 | Doris类型 | 说明 |
|---|---|---|
| `combination_name_zh` | `STRING` | `起点技术 × 终点技术`中文组合名 |
| `cross_theme_code` | `VARCHAR(64)` | 首版完美数据主题代码 |
| `association_strength_level` | `VARCHAR(16)` | `VERY_HIGH`、`HIGH`或`MEDIUM_HIGH` |
| `association_strength_label_zh` | `VARCHAR(16)` | 极强、强或中高 |
| `association_score` | `DECIMAL(9,6)` | 矩阵关联度；复制固定边置信分，不是概率 |
| `baseline_paper_count` | `BIGINT` | 两端2020—2022论文数之和 |
| `recent_paper_count` | `BIGINT` | 两端2023—2025论文数之和 |
| `paper_growth_rate` | `DECIMAL(18,6)` | 近期三年相对基线三年的论文增长率 |
| `total_paper_count` | `BIGINT` | 两端全观察期论文数之和，未跨端去重 |
| `synergy_principle_zh` | `STRING` | 引用、共同专利和关系类型约束的协同说明 |
| `core_institution_count` | `INT` | 已发布核心共同机构数；首版每边5家 |
| `cooperation_patent_count` | `BIGINT` | 已发布共同专利明细数，必须等于`shared_patent_count` |
| `related_featured_project_count` | `INT` | 有既有应用案例证据的首版重点项目数 |
| `is_priority_cross_association` | `BOOLEAN` | 是否进入重点交叉关联矩阵 |
| `perfect_data_release_id` | `VARCHAR(96)` | 完美数据发布ID |
| `perfect_data_review_status` | `VARCHAR(64)` | 操作方规则审核状态 |
| `perfect_data_value_nature` | `VARCHAR(32)` | 首版固定`OBSERVED_DERIVED` |
| `perfect_data_version` | `BIGINT` | 完美数据版本 |

#### 18.3.2 `ads_technology_graph_edge_institution`

一条重点边的5家核心共同机构。只有同一`institution_id`同时出现在两端
`ads_technology_institution`时才发布；先排已选重点机构，再按两端论文、专利、项目证据总数降序。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `edge_id`, `institution_id` | `VARCHAR(64)` | 重点边与平台机构 |
| 展示 | `institution_name_zh`, `institution_name_original` | `STRING` | 名称快照 |
| 分端证据 | `source_paper_count`, `target_paper_count` | `BIGINT` | 两端论文数 |
| 分端证据 | `source_patent_count`, `target_patent_count` | `BIGINT` | 两端专利数 |
| 分端证据 | `source_project_count`, `target_project_count` | `BIGINT` | 两端项目数 |
| 排序 | `combined_evidence_count`, `institution_rank` | `BIGINT/INT` | 六项证据之和与边内排名 |
| 关联 | `is_featured_institution` | `BOOLEAN` | 是否属于既有26家重点机构 |
| 治理 | `evidence_nature` | `VARCHAR(32)` | 固定`COMMON_INSTITUTION_OBSERVED` |
| 版本 | `perfect_data_release_id`, `data_version`, `update_time` | `VARCHAR/BIGINT/DATETIME(3)` | 发布与版本信息 |

#### 18.3.3 `ads_technology_graph_edge_patent`

重点边的完整共同专利明细，不使用仅含单节点Top 20的`ads_technology_patent`反推。来源固定为
`eto_mvp_cluster_dws_v1_20261016.dws_research_cluster_patent` snapshot
`3040518449308406315`，以同一`publication_id`同时关联两端research cluster为准。每边明细数必须和
`ads_technology_graph_edge.shared_patent_count`逐条对账。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `edge_id`, `patent_id` | `VARCHAR(64)` | 重点边与平台专利 |
| 专利 | `publication_number`, `country_code`, `kind_code`, `google_family_id` | `VARCHAR` | 公开号、地区、文献类型和专利族 |
| 时间 | `priority_date`, `filing_date`, `publication_date`, `publication_year`, `grant_date` | `DATE/INT` | 专利日期 |
| 展示 | `patent_title_original` | `STRING` | 原始标题 |
| 证据 | `source_cited_seed_paper_count`, `target_cited_seed_paper_count` | `BIGINT` | 各端去重seed论文数 |
| 排序 | `patent_rank` | `INT` | 公开年份倒序、专利ID升序 |
| 治理 | `evidence_type`, `source_snapshot_id` | `VARCHAR/BIGINT` | 共同专利口径与固定snapshot |
| 版本 | `perfect_data_release_id`, `data_version`, `update_time` | `VARCHAR/BIGINT/DATETIME(3)` | 发布与版本信息 |

#### 18.3.4 `ads_technology_graph_edge_project`

保存30条重点边与项目之间已经存在于`ads_technology_application_case`的关系。9.11.0只选择既有38个
重点项目；9.18.0允许完美技术边增加同时连接两端、且具有`RESEARCH_PROJECT_EVIDENCE`的非重点项目。
`related_side`为`SOURCE`、`TARGET`或`BOTH`；没有既有证据的边允许0条项目记录，不使用主题相似度补写
项目关系。`source_application_case_id`和`target_application_case_id`保留原应用案例Key，供详情页继续下钻。

#### 18.3.5 完美技术交叉关联（9.18.0）

首版完美技术边固定为`edge_6dc3fbe131eae3f9fe8b47055ffeb70a`，对应“用于汗液分析的可穿戴传感器
贴片 × 用于组织液分析的微针生物传感器”。`ads_technology_graph_edge_paper`物化两端25篇代表论文，
其中17篇参与18条跨技术seed论文引用；每篇保存所属端、跨边引用方向、对端论文ID、专利连接数、
组合级确定性排名及固定Paper/Reference Snapshot。核心论文排名不使用大模型。

该边在`ads_technology_graph_edge_project`发布3条`related_side='BOTH'`科研项目，关系均来自两端已有
`FUNDED_SEED_OUTPUT`，不是市场采用或产业化案例。共同机构继续使用既有5行，`core_institution_id`
投影`institution_rank=1`的机构，不改变机构表和排名。

3条项目同时在`ads_project_profile.name_original/name_en`保存资助机构发布的官方英文名称，
`name_zh`保存平台中文译名，`perfect_data_value_nature='PLATFORM_TRANSLATION'`明确中文并非资助机构
官方译名；`ads_technology_graph_edge_project.project_name_zh`从该中文名重新物化。NIH项目的来源误写
编号`R21DK13266`按NIH RePORTER校正为核心项目编号`R21DK132666`，不改变平台`project_id`。

`ads_technology_graph_edge`新增`perfect_edge_paper_count`、`core_institution_id`及
`synergy_principle_enriched_zh`。增强协同原理由DeepSeek读取固定论文、引用、共同专利、双端项目和
共同机构证据后生成；同时保存`synergy_principle_generation_method`、模型Provider/版本、Prompt版本、
输入Hash、证据JSON、审核状态和生成时间。模型不得创建输入外ID或把解释性推断写成观测事实；前端仅在
审核状态通过时展示增强字段，否则回退到`synergy_principle_zh`规则说明。

发布验收必须满足：重点边30条；每边组合名、强度、增长率、论文数和协同说明非空；每边5家核心共同
机构；所有共同专利完整写入且逐边等于`shared_patent_count`；Key无重复；来源Iceberg snapshot只读。

## 19. 公共学科维表

四张公共维表发布完整 OpenAlex Domain → Field → Subfield → Topic 分类字典，不按当前 MVP
论文使用情况裁剪。该字典不是 OpenAlex 全量论文事实数据；完整发布可以保证未来新增人才、机构、
项目关系中的合法 Topic 始终能够解析名称和祖先路径。

| 表 | 平台 Key | 来源映射 | 父级平台 ID | 双语字段 |
|---|---|---|---|---|
| `ads_discipline_domain` | `domain_id` | `openalex_domain_id` | — | `name_zh`, `name_en` |
| `ads_discipline_field` | `field_id` | `openalex_field_id` | `domain_id` | `name_zh`, `name_en` |
| `ads_discipline_subfield` | `subfield_id` | `openalex_subfield_id` | `field_id`, `domain_id` | `name_zh`, `name_en` |
| `ads_discipline_topic` | `topic_id` | `openalex_topic_id` | `subfield_id`, `field_id`, `domain_id` | `name_zh`, `name_en` |

平台 Key 从公共 identity bridge 获取，分别使用既有 `dom_`、`fld_`、`sub_`、`top_` ID，
不以 OpenAlex ID 生成平台 ID。子级表冗余祖先平台 ID，使 Domain/Field/Subfield → Topic 的
筛选不必递归；名称来自 `technology_v2.v_openalex_*_bilingual` 中已批准的中英文结果。

`ads_talent_topic_profile.topic_id`、`ads_institution_discipline_profile.topic_id` 和
`ads_project_topic.topic_id` 均关联 `ads_discipline_topic.topic_id`。业务关系表中的名称字段是
发布时展示快照，四张公共维表是当前学科名称和层级的权威 ADS 查询入口。

## 20. 地区年度 ADS

### 20.1 `ads_talent_yearly_location`

`ads_talent_yearly_location` 使用固定 ORCID 教育/工作经历和已解析机构位置生成年度观察事实。
不得使用人才当前机构反推历史位置。结束年已知的经历按闭区间展开；结束年缺失且
`is_current` 未可靠提供时，只记录开始年，不向统计截止年延展。区间内部年度标记
`is_imputed=true`，以区别直接边界证据。

粒度为一名人才在一个自然年的一个观察位置一行。同一人才同一年可以有多个位置；
`is_primary_location`、`location_rank` 和 `allocation_weight` 用于表达多位置分配，不得通过删行
强制变成单一位置。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `talent_id` | `VARCHAR(64)` | 否 | 人才平台 ID；逻辑主键之一 |
| `statistics_year` | `SMALLINT` | 否 | 事实所属自然年；逻辑主键之一 |
| `location_id` | `VARCHAR(64)` | 否 | 观察位置平台 ID，关联 `ads_location.location_id`；逻辑主键之一 |
| `continent_location_id` | `VARCHAR(64)` | 是 | 所属洲平台位置 ID 快照 |
| `country_location_id` | `VARCHAR(64)` | 是 | 所属国家平台位置 ID 快照 |
| `province_location_id` | `VARCHAR(64)` | 是 | 所属省/一级行政区平台位置 ID 快照 |
| `city_location_id` | `VARCHAR(64)` | 是 | 所属城市平台位置 ID 快照 |
| `district_location_id` | `VARCHAR(64)` | 是 | 所属区/县平台位置 ID 快照 |
| `primary_institution_id` | `VARCHAR(64)` | 是 | 该人才在此位置和年度的主要证据机构平台 ID |
| `primary_experience_type` | `TINYINT` | 是 | 主要证据经历类型：1教育、2工作；同等条件工作优先 |
| `institution_count` | `BIGINT` | 是 | 该人才在此位置和年度关联的去重机构数 |
| `evidence_paper_count` | `BIGINT` | 是 | 支撑该年度位置判断的去重论文数 |
| `orcid_education_count` | `BIGINT` | 是 | 与该年度位置相交的 ORCID 教育经历数 |
| `orcid_employment_count` | `BIGINT` | 是 | 与该年度位置相交的 ORCID employment 记录数 |
| `latest_evidence_date` | `DATE` | 是 | 该行采用证据中的最晚日期 |
| `is_primary_location` | `BOOLEAN` | 是 | 是否为该人才该年度的主位置 |
| `location_rank` | `INT` | 是 | 同一人才同一年内的位置排序，从 1 开始 |
| `allocation_weight` | `DECIMAL(12,8)` | 是 | 同一人才同一年分配到该位置的权重；计算规则由指标版本定义 |
| `assignment_method` | `VARCHAR(64)` | 是 | 年度位置判定方法代码 |
| `assignment_confidence` | `DECIMAL(5,4)` | 是 | 年度位置判定置信度，范围为 0–1 |
| `is_imputed` | `BOOLEAN` | 是 | 是否由时间区间或相邻年度推断，而非当年直接证据 |
| `metrics_as_of_date` | `DATE` | 是 | 指标事实统计截止日 |
| `metric_definition_version` | `VARCHAR(64)` | 是 | 指标与位置分配口径版本 |
| `data_version` | `BIGINT` | 否 | 同一逻辑 Key 的单调版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC 生成时间 |

### 20.2 `ads_geo_yearly_metrics`

`ads_geo_yearly_metrics` 按 `location_id, statistics_year` 保存洲、国家、省和城市年度汇总。
论文指标来自发布 MVP core，实际年份覆盖 2015–2026；2000–2014 的论文字段为 NULL 且
`paper_coverage_status='NOT_AVAILABLE'`。项目按 `effective_start_year` 统计。`talent_count` 已按
发布 MVP core 论文署名机构的同期位置证据发布；其余人才存量字段保持 NULL。流动字段已按严格观察事件发布，独立使用
`mobility_coverage_status='PARTIAL'`。`institution_count` 是当年有论文或启动项目的
去重活跃机构数，不是按成立年份推算的存续机构数；`new_institution_count` 才按成立年份统计。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `location_id` | `VARCHAR(64)` | 否 | 位置平台 ID，关联 `ads_location.location_id`；逻辑主键之一 |
| `statistics_year` | `SMALLINT` | 否 | 统计自然年；逻辑主键之一 |
| `location_level` | `VARCHAR(16)` | 否 | 位置层级：`CONTINENT / COUNTRY / PROVINCE / CITY / DISTRICT` |
| `paper_count` | `BIGINT` | 是 | 该位置当年发布的去重论文数；同一论文可计入多个位置 |
| `paper_fractional_count` | `DECIMAL(20,8)` | 是 | 按论文在同一位置层级命中的位置数等权分摊后的论文数 |
| `cited_by_count` | `BIGINT` | 是 | 当年发布论文截至统计日的累计被引次数之和 |
| `citation_count` | `BIGINT` | 是 | 该位置论文在该自然年收到的引用数；当前未发布 |
| `project_count` | `BIGINT` | 是 | `effective_start_year` 为当年的去重项目数；同一项目可计入多个位置 |
| `project_fractional_count` | `DECIMAL(20,8)` | 是 | 按项目在同一位置层级命中的位置数等权分摊后的项目数 |
| `direct_project_count` | `BIGINT` | 是 | 至少有直接项目—机构关系的项目数 |
| `inferred_project_count` | `BIGINT` | 是 | 仅由受资助论文作者机构兜底推断的项目数 |
| `talent_count` | `BIGINT` | 是 | 2015–2026 年发布 MVP core 中，通过论文署名机构在该位置被观察到的年度去重发布人才数；2000–2014 为 NULL |
| `talent_participation_count` | `BIGINT` | 是 | 未按人才去重的年度位置参与次数；当前未发布 |
| `new_talent_count` | `BIGINT` | 是 | 当年首次在该位置观察到的人才数；当前未发布 |
| `institution_count` | `BIGINT` | 是 | 当年有论文或启动项目的去重活跃机构并集数 |
| `paper_active_institution_count` | `BIGINT` | 是 | 当年存在发布论文的去重机构数 |
| `project_start_institution_count` | `BIGINT` | 是 | 当年存在启动项目关系的去重机构数 |
| `new_institution_count` | `BIGINT` | 是 | `established_year` 为当年的去重机构数 |
| `inbound_talent_count` | `BIGINT` | 是 | 当年严格观察事件中流入该位置的去重人才数；已发布部分覆盖值 |
| `outbound_talent_count` | `BIGINT` | 是 | 当年严格观察事件中流出该位置的去重人才数；已发布部分覆盖值 |
| `mobility_event_count` | `BIGINT` | 是 | 当年严格观察事件中涉及该位置的去重事件数；已发布部分覆盖值 |
| `paper_coverage_status` | `VARCHAR(32)` | 否 | 论文指标覆盖状态；当前使用 `COMPLETE / NOT_AVAILABLE` |
| `project_coverage_status` | `VARCHAR(32)` | 否 | 项目指标覆盖状态；当前发布值为 `COMPLETE` |
| `institution_coverage_status` | `VARCHAR(32)` | 否 | 机构指标覆盖状态；当前发布值为 `PARTIAL` |
| `talent_coverage_status` | `VARCHAR(32)` | 否 | 人才指标覆盖状态；2015–2026 为 `PARTIAL`，2000–2014 为 `NOT_AVAILABLE` |
| `mobility_coverage_status` | `VARCHAR(32)` | 否 | 流动指标覆盖状态；`PARTIAL` 表示仅统计严格识别的已观测事件 |
| `location_resolved_ratio` | `DECIMAL(9,6)` | 是 | 进入聚合口径的事实中成功解析到平台位置的比例；当前未发布 |
| `metrics_as_of_date` | `DATE` | 是 | 指标事实统计截止日 |
| `metric_definition_version` | `VARCHAR(64)` | 是 | 指标口径版本 |
| `data_version` | `BIGINT` | 否 | 同一逻辑 Key 的单调版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC 生成时间 |

`talent_count` 当前使用 `geo_yearly_observed_talent_mvp_v1`：从固定发布的 100,000 名 MVP 人才—
论文—署名机构事实出发，以论文发表年和署名机构已解析位置为同期证据，在
`location_id, statistics_year` 内按人才来源 ID 去重。它与 20.3 的 Primary Topic 人才指标共用
人才范围和位置证据，但必须直接从人才事实重新去重，禁止跨 Topic 求和。一个人才可在同年计入多个
真实署名位置以及叶子位置的祖先位置，故跨位置或层级相加也不代表全局去重人数。

2015–2026 有已发布位置—年度 Key 但无匹配人才证据时写 0；2000–2014 写 NULL。`PARTIAL` 表示
当前仅覆盖固定 MVP core 论文观察口径，尚未纳入 ORCID 年度任职区间和完整年度人才位置模型。
2026 为截至 `metrics_as_of_date=2026-09-18` 的未结束年度累计值。本指标不表示居住、入职、在岗或
人才流动；`talent_participation_count` 和 `new_talent_count` 仍保持 NULL。执行与门禁见
[`docs/geo_ads_yearly_talent_v1.md`](docs/geo_ads_yearly_talent_v1.md)。

### 20.3 `ads_geo_yearly_discipline_metrics`

`ads_geo_yearly_discipline_metrics` 是 Topic 粒度宽表，每行直接携带 Domain、Field、Subfield、
Topic 的平台 ID 及中英文名称。当前 `paper_count`、`project_count` 使用 Primary Topic；
`associated_paper_count`、`associated_project_count` 尚未完成分批全 Topic 聚合，保持 NULL。
`talent_count` 从发布 MVP core 的人才—论文—署名机构事实按 Primary Topic 计算；
`associated_talent_count` 尚未发布，保持 NULL。`institution_count` 尚未完成跨论文和项目的
Primary Topic 去重，当前也保持 NULL。2000–2014 的论文数、论文被引数和人才数按不可用处理为
NULL。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `location_id` | `VARCHAR(64)` | 否 | 位置平台 ID，关联 `ads_location.location_id`；逻辑主键之一 |
| `statistics_year` | `SMALLINT` | 否 | 统计自然年；逻辑主键之一 |
| `topic_id` | `VARCHAR(64)` | 否 | Topic 平台 ID，关联 `ads_discipline_topic.topic_id`；逻辑主键之一 |
| `domain_id` | `VARCHAR(64)` | 否 | Topic 所属 Domain 平台 ID 快照 |
| `domain_name_zh` | `STRING` | 否 | Domain 中文名快照 |
| `domain_name_en` | `STRING` | 否 | Domain 英文名快照 |
| `field_id` | `VARCHAR(64)` | 否 | Topic 所属 Field 平台 ID 快照 |
| `field_name_zh` | `STRING` | 否 | Field 中文名快照 |
| `field_name_en` | `STRING` | 否 | Field 英文名快照 |
| `subfield_id` | `VARCHAR(64)` | 否 | Topic 所属 Subfield 平台 ID 快照 |
| `subfield_name_zh` | `STRING` | 否 | Subfield 中文名快照 |
| `subfield_name_en` | `STRING` | 否 | Subfield 英文名快照 |
| `topic_name_zh` | `STRING` | 否 | Topic 中文名快照 |
| `topic_name_en` | `STRING` | 否 | Topic 英文名快照 |
| `paper_count` | `BIGINT` | 是 | Primary Topic 为该 Topic 的当年去重论文数 |
| `associated_paper_count` | `BIGINT` | 是 | 任一关联 Topic 为该 Topic 的当年去重论文数；当前未发布 |
| `cited_by_count` | `BIGINT` | 是 | `paper_count` 对应论文截至统计日的累计被引次数之和 |
| `project_count` | `BIGINT` | 是 | Primary Topic 为该 Topic 且当年启动的去重项目数 |
| `associated_project_count` | `BIGINT` | 是 | 任一关联 Topic 为该 Topic 且当年启动的去重项目数；当前未发布 |
| `talent_count` | `BIGINT` | 是 | 2015–2026 年发布 MVP core 中，通过论文署名机构在该位置被观察到且论文 Primary Topic 为该 Topic 的年度去重发布人才数；2000–2014 为 NULL |
| `associated_talent_count` | `BIGINT` | 是 | 任一关联 Topic 为该 Topic 的年度去重人才数；当前未发布 |
| `institution_count` | `BIGINT` | 是 | 该位置、年度、Primary Topic 下论文与项目关联机构的去重并集数；当前未发布 |
| `talent_coverage_status` | `VARCHAR(32)` | 否 | 人才指标覆盖状态；2015–2026 为 `PARTIAL`，2000–2014 为 `NOT_AVAILABLE` |
| `metrics_as_of_date` | `DATE` | 是 | 指标事实统计截止日 |
| `metric_definition_version` | `VARCHAR(64)` | 是 | 指标口径版本 |
| `data_version` | `BIGINT` | 否 | 同一逻辑 Key 的单调版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC 生成时间 |

#### 20.3.1 `talent_count` 固定计算口径

本字段当前发布口径为 `geo_yearly_primary_talent_mvp_v1`，不是完整人口、居住地、任职地或人才
流动统计。固定输入和连接路径为：

```text
发布的100,000名MVP人才
  → 固定MVP core人才—论文—署名机构事实
  → 论文publication_year与primary_topic_id
  → 署名机构的已解析平台位置及CONTINENT/COUNTRY/PROVINCE/CITY祖先路径
  → location_id × publication_year × Primary Topic内COUNT(DISTINCT talent)
```

计算使用人才来源 ID 完成事实去重；这 100,000 个来源 ID 均已通过 identity bridge 映射到稳定
平台 `tal_` ID。一个人才同年在同一位置、同一 Primary Topic 有多篇论文、多个署名或多个机构时
只计一次。同一人才可以在同一年计入多个真实署名位置，也会同时计入叶子位置及其各级祖先位置；
因此不同位置、位置层级或 Topic 的 `talent_count` 不可直接相加后解释为全局去重人数。

只使用论文发表当年的署名机构作为同期地理证据。不得使用 `ads_talent_profile` 的当前机构或机构
当前位置反推人才历史位置，也不得把 ORCID 经历自由文本、当前所在地代理字段或
`ads_talent_yearly_location` 空表混入本指标。该指标表示“在发布 MVP core 论文中被观察到”，不表示
居住、入职、实际在岗、迁入迁出或完整科研人口。

NULL 与 0 的语义固定如下：

- 2015–2026 在发布范围内有该位置—年度—Topic Key、但没有匹配的人才论文证据时写 0；
- 2000–2014 没有发布 MVP core 人才论文年度覆盖，写 NULL，不得写 0；
- 2026 是截至 `metrics_as_of_date=2026-09-18` 的未结束自然年累计值，不得与完整年度直接比较；
- `associated_talent_count` 继续为 NULL，不能用 Primary Topic 人数代填。

`talent_coverage_status='PARTIAL'` 表示只发布上述 Primary Topic 论文观察口径，且仍存在来源覆盖
限制：部分论文没有 Primary Topic，少量署名机构没有已解析位置，全 Topic 的
`associated_talent_count` 尚未发布，ORCID 年度任职区间和 `ads_talent_yearly_location` 也尚未进入
本指标。`NOT_AVAILABLE` 表示该年度不在固定 MVP core 人才论文覆盖范围内。只有完成全 Topic、
位置解析和批准的年度人才位置口径后，才允许在新指标版本中使用 `COMPLETE`；不得原地扩大本版本
含义。

当前发布固定使用以下不可变输入：MVP core Work Snapshot `4292018784001736547`、DWD Work
Snapshot `3691395969244640547`、机构 ADS 人才论文事实 Snapshot `7367496050760891968`、地区机构
映射 Snapshot `4591962443053062500`、Topic 映射 Snapshot `6933579552916378888` 和原地区学科宽表
Snapshot `8559334509421607459`。执行入口、分年聚合和质量校验见
[`docs/geo_ads_primary_talent_v1.md`](docs/geo_ads_primary_talent_v1.md)。

#### 20.3.2 `ads_topic_country_snapshot`

一行表示一个平台 Topic 在一个国家或地区的当前论文全球分布快照。逻辑主键为
`topic_id, country_location_id`。本表服务不分年度展示的世界地图、国家排行榜、占比和趋势箭头；
年度事实仍查询`ads_geo_yearly_discipline_metrics`。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `topic_id` | `VARCHAR(64)` | 否 | Topic平台ID；逻辑主键之一 |
| `country_location_id` | `VARCHAR(64)` | 否 | 国家平台位置ID，关联`ads_location.location_id`；逻辑主键之一 |
| `country_code` | `VARCHAR(8)` | 是 | ISO 3166-1 alpha-2国家或地区代码；供地图要素关联 |
| `country_name` | `VARCHAR(256)` | 否 | 当前发布默认国家名称快照 |
| `country_name_zh` | `VARCHAR(256)` | 是 | 当前治理中文名称快照 |
| `country_name_en` | `VARCHAR(256)` | 是 | 当前英文名称快照 |
| `paper_count` | `BIGINT` | 否 | 观察范围内国家参与发表的去重论文数；国际合作论文可进入多个国家 |
| `paper_fractional_count` | `DECIMAL(20,8)` | 否 | 每篇论文按命中国家数等权分摊后的论文量 |
| `global_paper_count` | `BIGINT` | 否 | 同一Topic观察范围内全部去重论文数，包括未解析到国家的论文 |
| `country_resolved_paper_count` | `BIGINT` | 否 | 同一Topic至少解析到一个国家的去重论文数 |
| `paper_coverage_ratio` | `DECIMAL(18,12)` | 否 | `paper_count/global_paper_count`；是国家参与覆盖率，跨国家之和可大于1 |
| `country_resolution_ratio` | `DECIMAL(9,6)` | 否 | `country_resolved_paper_count/global_paper_count` |
| `paper_fractional_share` | `DECIMAL(18,12)` | 否 | 国家分数论文量占全部已解析国家分数论文量的比例；同一Topic合计为1 |
| `output_rank` | `BIGINT` | 否 | 按分数论文量、参与论文数和国家ID生成的稳定研究产出排名 |
| `ranked_country_count` | `BIGINT` | 否 | 同一Topic进入当前排名的国家/地区数 |
| `baseline_paper_count` | `BIGINT` | 否 | 2020—2022对照期国家参与论文数 |
| `recent_paper_count` | `BIGINT` | 否 | 2023—2025近期国家参与论文数 |
| `baseline_avg_annual_paper_count` | `DECIMAL(20,8)` | 否 | 对照期年均参与论文数 |
| `recent_avg_annual_paper_count` | `DECIMAL(20,8)` | 否 | 近期年均参与论文数 |
| `paper_growth_rate` | `DECIMAL(18,8)` | 是 | `recent_avg/baseline_avg-1`；无有效对照分母时NULL |
| `trend_direction` | `VARCHAR(32)` | 否 | `UP/STABLE/DOWN/INSUFFICIENT_EVIDENCE` |
| `growth_rank` | `BIGINT` | 是 | 满足趋势证据门槛的国家在同一Topic内的增长率稳定排名 |
| `analysis_start_year`, `analysis_end_year` | `SMALLINT NOT NULL` | 否 | 当前固定2015和2025，只使用完整自然年 |
| `baseline_start_year`, `baseline_end_year` | `SMALLINT NOT NULL` | 否 | 当前固定2020和2022 |
| `recent_start_year`, `recent_end_year` | `SMALLINT NOT NULL` | 否 | 当前固定2023和2025 |
| `topic_relation_scope` | `VARCHAR(32)` | 否 | 当前固定`PRIMARY_TOPIC` |
| `coverage_status` | `VARCHAR(32)` | 否 | `COMPLETE/PARTIAL/NOT_AVAILABLE`国家解析覆盖状态 |
| `snapshot_date` | `DATE` | 否 | 当前快照业务日期 |
| `metrics_as_of_date` | `DATE` | 否 | 来源指标统计截止日 |
| `metric_definition_version` | `VARCHAR(64)` | 否 | 当前固定`topic_country_primary_mvp_v1` |
| `data_version` | `BIGINT` | 否 | 同一逻辑Key单调数据版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC生成时间 |

当前固定读取4,000,000篇MVP core论文及其Primary Topic、署名机构、已解析国家和位置维表Snapshot；
只纳入2015—2025完整年度，不把2026部分年度写入排名或趋势。`paper_count`回答国家参与论文数量，
不能跨国家求和解释为全球去重论文数；需要可加总占比时必须使用`paper_fractional_count`及
`paper_fractional_share`。

趋势比较2020—2022和2023—2025两个三年窗口。对照期为0或两个窗口合计少于5篇时固定为
`INSUFFICIENT_EVIDENCE`；其余记录使用±5%稳定带判定`UP/STABLE/DOWN`。改变时间窗口、规模门槛、
稳定带或Topic关系范围必须提升`metric_definition_version`，不得原位扩大本版本含义。

前端一次按`topic_id`读取全部国家并按`output_rank`排序；地图和排行榜使用
`country_location_id`同步选中，地图GeoJSON通过`country_code`关联。边界几何、缩放和动画不进入ADS。
完整查询、发布和恢复说明见[`docs/topic_country_snapshot_v1.md`](docs/topic_country_snapshot_v1.md)。

### 20.4 `ads_geo_yearly_institution_type_metrics`

`ads_geo_yearly_institution_type_metrics` 在行内保存机构类型默认名、中英文名称；机构年度口径与
总表一致。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `location_id` | `VARCHAR(64)` | 否 | 位置平台 ID，关联 `ads_location.location_id`；逻辑主键之一 |
| `statistics_year` | `SMALLINT` | 否 | 统计自然年；逻辑主键之一 |
| `institution_type_id` | `VARCHAR(32)` | 否 | 稳定机构类型代码，关联 `ads_institution_type.institution_type_id`；逻辑主键之一 |
| `institution_type_name` | `VARCHAR(128)` | 否 | 机构类型默认名称快照 |
| `institution_type_name_zh` | `VARCHAR(128)` | 是 | 机构类型中文名快照 |
| `institution_type_name_en` | `VARCHAR(128)` | 是 | 机构类型英文名快照 |
| `institution_count` | `BIGINT` | 是 | 该类型当年有论文或启动项目的去重活跃机构并集数 |
| `paper_active_institution_count` | `BIGINT` | 是 | 该类型当年存在发布论文的去重机构数 |
| `project_start_institution_count` | `BIGINT` | 是 | 该类型当年存在启动项目关系的去重机构数 |
| `new_institution_count` | `BIGINT` | 是 | 该类型中 `established_year` 为当年的去重机构数 |
| `paper_count` | `BIGINT` | 是 | 该类型机构关联的当年去重论文数 |
| `project_count` | `BIGINT` | 是 | 该类型机构关联且当年启动的去重项目数 |
| `talent_count` | `BIGINT` | 是 | 该类型机构关联的年度去重人才数；当前未发布 |
| `talent_coverage_status` | `VARCHAR(32)` | 否 | 人才指标覆盖状态；当前发布值为 `NOT_READY` |
| `institution_established_year_coverage_ratio` | `DECIMAL(9,6)` | 是 | 该位置和类型下机构中 `established_year` 非空的比例 |
| `metrics_as_of_date` | `DATE` | 是 | 指标事实统计截止日 |
| `metric_definition_version` | `VARCHAR(64)` | 是 | 指标口径版本 |
| `data_version` | `BIGINT` | 否 | 同一逻辑 Key 的单调版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC 生成时间 |

### 20.5 `ads_geo_yearly_index`

`ads_geo_yearly_index` 在公式批准前保持空表。只有公式快照和组成项允许使用 `VARIANT`；
常规可筛选指标不得塞入 `component_values` 代替正式字段。

| 字段 | Doris 类型 | 可空 | 说明 |
|---|---|---|---|
| `location_id` | `VARCHAR(64)` | 否 | 位置平台 ID，关联 `ads_location.location_id`；逻辑主键之一 |
| `statistics_year` | `SMALLINT` | 否 | 指数所属统计自然年；逻辑主键之一 |
| `index_code` | `VARCHAR(64)` | 否 | 稳定指数代码；逻辑主键之一 |
| `index_name_zh` | `VARCHAR(256)` | 是 | 指数中文名称快照 |
| `index_name_en` | `VARCHAR(256)` | 是 | 指数英文名称快照 |
| `raw_value` | `DECIMAL(24,8)` | 是 | 公式计算所得、归一化前的原始值 |
| `normalized_value` | `DECIMAL(18,8)` | 是 | 按 `score_version` 规则归一化后的值 |
| `percentile` | `DECIMAL(9,6)` | 是 | 指定比较总体中的百分位，范围为 0–1 |
| `component_values` | `VARIANT` | 是 | 有界的指数组成项名称和值快照 |
| `formula_snapshot` | `VARIANT` | 是 | 可审计的公式、参数和比较总体快照 |
| `score_version` | `VARCHAR(64)` | 否 | 指数公式及归一化规则版本 |
| `calculated_at` | `DATETIME(3)` | 否 | 指数计算时间（UTC） |
| `data_version` | `BIGINT` | 否 | 同一逻辑 Key 的单调版本 |
| `update_time` | `DATETIME(3)` | 否 | UTC 生成时间 |

执行入口：`./scripts/publish_geo_ads.sh`。当前发布核验见
[`reports/geo_ads_v1/post_run_verification.md`](reports/geo_ads_v1/post_run_verification.md)。

## 21. 新兴 Topic 识别

本节只定义“固定 400 万篇 MVP core 中观察到的新兴 Topic”，不得省略 `MVP core` 限定后解释为
全球全量科研的新兴学科。首版使用论文的 Primary Topic；一篇论文最多贡献一个 Topic，保证 Topic
论文数可加总。全部关联 Topic 的加权预警不属于 `emerging_topic_primary_mvp_v1`，后续必须使用新的
`metric_definition_version` 和 `topic_relation_scope` 发布，不得原地扩大首版含义。

正式评分只使用截至统计日已经结束的自然年：长期观察窗为2017—2025，对照窗为2020—2022，近期
窗为2023—2025。2015是观察左边界，只能标记 `BASELINE_LEFT_CENSORED`；2026截至
`metrics_as_of_date=2026-09-18`，只进入趋势展示并标记 `PARTIAL_YEAR`，不得进入窗口、同比门槛或
正式排名。撤稿和 paratext 不进入有效论文总体。

### 21.1 `ads_emerging_topic_yearly_metrics`

一行表示一个平台 Topic 在一个自然年的 MVP core 发展事实。逻辑主键为
`topic_id, statistics_year`。所有已观察 Topic 都补齐2015—2026年份；没有论文的完整年度写0，不用
缺行表示0。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `topic_id` | `VARCHAR(64) NOT NULL` | 关联公共学科维表 |
| Key | `statistics_year` | `SMALLINT NOT NULL` | 2015—2026自然年 |
| 口径 | `topic_relation_scope` | `VARCHAR(32) NOT NULL` | 首版固定`PRIMARY_TOPIC` |
| 论文 | `paper_count` | `BIGINT NOT NULL` | 当年Primary Topic去重论文数 |
| 论文 | `total_mvp_paper_count` | `BIGINT NOT NULL` | 同年有效MVP core论文总数 |
| 论文 | `paper_share` | `DECIMAL(18,12) NOT NULL` | `paper_count / total_mvp_paper_count` |
| 论文 | `paper_count_yoy` | `DECIMAL(18,8)` | 论文数同比；无有效上年分母时NULL |
| 论文 | `paper_share_yoy` | `DECIMAL(18,8)` | 论文份额同比；无有效上年分母时NULL |
| 作者 | `author_count` | `BIGINT NOT NULL` | 当年core论文可识别OpenAlex作者数，不限已发布10万人 |
| 作者 | `new_author_count` | `BIGINT` | 观察窗内首次进入该Topic的作者数；2015为NULL |
| 作者 | `new_author_ratio` | `DECIMAL(9,6)` | 新增作者/当年活跃作者 |
| 机构 | `institution_count` | `BIGINT NOT NULL` | 当年署名关联去重机构数 |
| 机构 | `new_institution_count` | `BIGINT` | 观察窗内首次进入该Topic的机构数；2015为NULL |
| 机构 | `new_institution_ratio` | `DECIMAL(9,6)` | 新增机构/当年活跃机构 |
| 影响 | `cited_by_count` | `BIGINT NOT NULL` | 当年发表论文截至统计日累计被引之和，不是年度收到引用 |
| 影响 | `avg_fwci` | `DECIMAL(14,6)` | 当年有值论文等权平均FWCI |
| 影响 | `impact_percentile` | `DECIMAL(9,6)` | 同发表年、同Subfield平均FWCI的0—100百分位 |
| 覆盖 | `coverage_status` | `VARCHAR(32) NOT NULL` | `BASELINE_LEFT_CENSORED/COMPLETE/PARTIAL_YEAR` |
| 版本 | `metrics_as_of_date` | `DATE NOT NULL` | 指标截止日 |
| 版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 口径版本 |
| 版本 | `data_version` / `update_time` | `BIGINT NOT NULL` / `DATETIME(3) NOT NULL` | 公共版本字段 |

`new_author_count` 和 `new_institution_count` 是在固定MVP观察窗内首次被观察到，不表示作者科研生涯
首次研究该方向或机构真实历史首次进入。`paper_share` 是新兴识别的基础增长量；只使用论文数增长会
把整个MVP总体自然增长误判为Topic增长。

### 21.2 `ads_emerging_topic_snapshot`

一行保存一个 Topic 在当前指标版本下的窗口汇总、分项分数、最终状态和稳定排名，逻辑主键为
`topic_id`。Field/Subfield/Domain ID是本次评分使用的分类快照；名称实时关联公共学科维表，不在本表
复制。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key与分组 | `topic_id` | `VARCHAR(64) NOT NULL` | 平台Topic ID |
| Key与分组 | `subfield_id`, `field_id`, `domain_id` | `VARCHAR(64) NOT NULL` | 分类层级；Subfield为百分位比较组 |
| 窗口论文 | `baseline_paper_count`, `recent_paper_count` | `BIGINT NOT NULL` | 2020—2022、2023—2025论文数 |
| 窗口份额 | `baseline_avg_paper_share`, `recent_avg_paper_share` | `DECIMAL(18,12) NOT NULL` | 两个窗口的年均论文份额 |
| 增长 | `relative_growth` | `DECIMAL(18,8)` | `(近期年均份额+1e-12)/(对照年均份额+1e-12)` |
| 增长 | `share_acceleration` | `DECIMAL(18,12) NOT NULL` | 近期三年份额斜率减对照三年份额斜率 |
| 新近性 | `recent_concentration` | `DECIMAL(9,6)` | 2023—2025论文占2017—2025论文比例 |
| 持续性 | `active_year_count` | `SMALLINT NOT NULL` | 2017—2025有论文年份数 |
| 持续性 | `positive_growth_year_count` | `TINYINT NOT NULL` | 2023—2025相对前一年份额增加次数，0—3 |
| 持续性 | `latest_share_ratio` | `DECIMAL(18,8)` | 2025份额/2024份额 |
| 作者扩散 | `recent_author_count`, `recent_new_author_count` | `BIGINT NOT NULL` | 近期去重活跃和首次观察进入作者数 |
| 作者扩散 | `recent_new_author_ratio` | `DECIMAL(9,6)` | 近期新增作者/近期活跃作者 |
| 机构扩散 | `recent_institution_count`, `recent_new_institution_count` | `BIGINT NOT NULL` | 近期去重活跃和首次观察进入机构数 |
| 机构扩散 | `recent_new_institution_ratio` | `DECIMAL(9,6)` | 近期新增机构/近期活跃机构 |
| 影响 | `recent_impact_percentile` | `DECIMAL(9,6)` | 近期按论文数加权的年度影响力百分位 |
| 分项 | `growth_score`, `acceleration_score` | `DECIMAL(9,6)` | 同Subfield 0—100百分位分 |
| 分项 | `author_diffusion_score`, `institution_diffusion_score` | `DECIMAL(9,6)` | 同Subfield扩散百分位分 |
| 分项 | `impact_score`, `persistence_score` | `DECIMAL(9,6)` | 影响百分位与持续性分 |
| 结果 | `emergence_score` | `DECIMAL(9,6)` | 固定权重综合分0—100；不可评价时NULL |
| 结果 | `emergence_rank` | `BIGINT` | 有分数Topic全局稳定排名 |
| 结果 | `emergence_status` | `VARCHAR(32) NOT NULL` | 下列固定状态之一 |
| 口径版本 | `topic_relation_scope` | `VARCHAR(32) NOT NULL` | 首版固定`PRIMARY_TOPIC` |
| 口径版本 | `metrics_as_of_date`, `metric_definition_version` | `DATE NOT NULL`, `VARCHAR(64) NOT NULL` | 截止日和正式口径版本 |
| 版本 | `data_version` / `update_time` | `BIGINT NOT NULL` / `DATETIME(3) NOT NULL` | 公共版本字段 |

规模证据门槛固定为：近期论文不少于50、2017—2025活跃年份不少于5、近期去重作者不少于20、
近期去重机构不少于5。只有通过门槛的Topic进入同Subfield百分位与综合分计算。综合公式为：

```text
emergence_score =
    0.30 * growth_score
  + 0.20 * acceleration_score
  + 0.15 * author_diffusion_score
  + 0.15 * institution_diffusion_score
  + 0.10 * impact_score
  + 0.10 * persistence_score

persistence_score = positive_growth_year_count / 3 * 100
```

状态按以下顺序判定，避免同一 Topic 命中多个标签：

1. 未通过规模证据门槛：`INSUFFICIENT_EVIDENCE`。
2. `relative_growth>=1.5`，但正增长少于2次或`latest_share_ratio<0.8`：`TRANSIENT_SPIKE`。
3. 同时满足增长、持续性、`recent_concentration>=0.45`且综合分不低于80：`EMERGING`。
4. 与上一条相同但综合分为70—80：`EARLY_EMERGING`。
5. 增长和持续性成立、但近期集中度低于0.45：`ESTABLISHED_GROWING`。
6. 综合分不低于60：`WATCH`；其余为`MATURE`。

累计引用只用于展示，不进入新兴度。影响项使用FWCI及同年同Subfield比较，避免用累计引用系统性偏向
老Topic。影响数据不可评价时不允许用0伪造；首版综合分保持NULL并不能进入新兴状态。

### 21.3 `ads_emerging_topic_key_talent`

只为 `EMERGING/EARLY_EMERGING/WATCH` Topic发布关键人才，每个Topic最多20人，逻辑主键为
`topic_id, talent_id`。候选限定为已发布MVP人才，且2023—2025至少有2篇以该Topic为Primary Topic
的论文；这不是完整全球人才榜。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| Key | `topic_id`, `talent_id` | `VARCHAR(64) NOT NULL` | Topic和人才平台ID |
| 分类 | `talent_role` | `VARCHAR(32) NOT NULL` | `FOUNDING_OR_LEADING/RISING/CORE_CONTRIBUTOR` |
| 证据 | `recent_paper_count` | `BIGINT NOT NULL` | 2023—2025 Primary Topic论文数 |
| 证据 | `first_topic_year`, `latest_topic_year` | `SMALLINT NOT NULL` | 观察窗首末论文年 |
| 证据 | `recent_active_year_count` | `TINYINT NOT NULL` | 近期活跃年份数 |
| 领导力 | `recent_first_author_count`, `recent_corresponding_author_count` | `BIGINT NOT NULL` | 近期作者角色论文数 |
| 影响 | `recent_cited_by_count`, `recent_avg_fwci` | `BIGINT NOT NULL`, `DECIMAL(14,6)` | 近期累计被引和平均FWCI |
| 分项 | `contribution_score`, `impact_score` | `DECIMAL(9,6)` | Topic内论文数和FWCI百分位 |
| 分项 | `leadership_score`, `persistence_score`, `early_entry_score` | `DECIMAL(9,6) NOT NULL` | 领导、持续和早期进入分 |
| 结果 | `metric_weight_coverage` | `DECIMAL(5,4) NOT NULL` | FWCI有值为1，否则为0.75 |
| 结果 | `key_talent_score` | `DECIMAL(9,6) NOT NULL` | 按实际可用权重归一后的0—100分 |
| 结果 | `talent_rank` | `INT NOT NULL` | Topic内稳定排名，最多20 |
| 版本 | `metrics_as_of_date`, `metric_definition_version` | `DATE NOT NULL`, `VARCHAR(64) NOT NULL` | 截止日和口径版本 |
| 版本 | `data_version` / `update_time` | `BIGINT NOT NULL` / `DATETIME(3) NOT NULL` | 公共版本字段 |

关键人才固定权重为近期Topic贡献35%、同Topic影响25%、第一/通讯作者领导力20%、三年持续性10%、
相对Topic观察起点的早期进入10%。FWCI缺失时`impact_score=NULL`，其余75%权重归一到100%，并通过
`metric_weight_coverage=0.75`显式披露，禁止把未知影响力写成0。排名同分依次比较近期论文数和
`talent_id`，保证重跑稳定。

发布入口为：

```bash
./scripts/compose.sh up -d --wait --wait-timeout 300
./scripts/publish_emerging_topic_mvp_v1.sh
```

配置固定全部Iceberg Snapshot、窗口、门槛、权重和生成时间。当前已发布53,952条年度趋势、4,496条
Topic快照和20,235条关键人才关系；`EMERGING/EARLY_EMERGING/WATCH`分别为133/219/806个Topic。
Key重复、Topic孤儿、人才孤儿、覆盖状态、数值范围、Top 20排名和幂等重跑异常均为0。完整核验见
[`reports/emerging_topic_mvp_v1/post_run_verification.md`](reports/emerging_topic_mvp_v1/post_run_verification.md)。

## 22. 人才年度学科与流动

### 22.1 `ads_talent_yearly_discipline`

按 `talent_id, statistics_year, field_id` 保存发布 MVP core 论文形成的年度 Field 画像。论文先按
`talent_id, work_id, field_id` 去重，避免同一论文的多个 Topic 属于同一 Field 时重复累计引用。
每个人才每年按 `paper_count DESC, cited_by_count DESC, field_id ASC` 确定唯一 Primary Field。
2026 是部分年度，只用于展示，不与 2025 形成正式领域迁移事件。

| 字段 | Doris 类型 | 说明 |
|---|---|---|
| `talent_id, statistics_year, field_id` | `VARCHAR(64), SMALLINT, VARCHAR(64) NOT NULL` | 逻辑主键 |
| `paper_count` | `BIGINT NOT NULL` | 该年该Field去重论文数 |
| `cited_by_count` | `BIGINT NOT NULL` | 上述论文截至统计日累计被引之和 |
| `paper_share` | `DECIMAL(9,6) NOT NULL` | 该Field论文数占人才当年有效Field论文数之比 |
| `is_primary_discipline` | `BOOLEAN NOT NULL` | 是否为人才该年的唯一Primary Field |
| `discipline_rank` | `INT NOT NULL` | 人才年度Field稳定排序 |
| `coverage_status` | `VARCHAR(32) NOT NULL` | `COMPLETE/PARTIAL_YEAR` |
| `metrics_as_of_date`, `metric_definition_version` | `DATE, VARCHAR(64) NOT NULL` | 截止日和口径版本 |
| `data_version`, `update_time` | `BIGINT, DATETIME(3) NOT NULL` | 公共版本字段 |

### 22.2 `ads_talent_mobility_event`

保存可以追溯到来源经历或相邻年度 Primary Field 的严格迁移事件。首版只发布三类：

1. `EDUCATION_TO_WORK`：每名人才第一段已解析工作经历，与结束年不晚于工作开始年的最近一段
   已解析教育经历配对；起止机构必须不同。
2. `WORK_TO_WORK`：按开始年、准确开始日期和稳定经历 ID 排序相邻工作经历；前一段必须有结束年，
   `previous_end_year <= next_start_year`，且开始年严格递增、机构不同。重叠任职和同年多机构不作为迁移。
3. `RESEARCH_FIELD_CHANGE`：两个相邻完整自然年的唯一 Primary Field 不同。跨年缺口和2026部分年
   不产生正式事件。

事件年统一采用目标阶段开始年或目标 Primary Field 年。地区变化只在两端相应层级 ID 都非空且不同时
成立；缺失位置不能被解释为跨地区。所有事件均为已观测的部分覆盖结果，不代表完整人口迁移。

| 字段组 | 关键字段 | 说明 |
|---|---|---|
| Key | `mobility_event_id`, `talent_id` | 事件ID由人才、类型、年份和稳定两端证据确定性生成 |
| 时间与类型 | `event_year`, `event_date`, `mobility_type` | 目标阶段的年份、可用准确日期和事件类型 |
| 来源经历 | `from_experience_id`, `to_experience_id` | 教育/工作迁移的可追溯经历ID |
| 机构 | `from_institution_id`, `to_institution_id` | 机构迁移两端 |
| 地区 | `from/to_location_id`及国家、省、城市ID | 流向图各层级端点 |
| 学科 | `from_field_id`, `to_field_id` | 研究领域变化两端；职业事件为空 |
| 跨地区标记 | `is_cross_country/province/city` | 仅两端均已解析且ID不同时为真 |
| 质量 | `assignment_method`, `assignment_confidence`, `coverage_status` | 判定方法、置信度和部分覆盖状态 |
| 证据与版本 | `evidence`, `metrics_as_of_date`, `metric_definition_version`, `data_version`, `update_time` | 审计与版本字段 |

### 22.3 `ads_talent_mobility_yearly_flow`

为动态流向图预聚合年度有向边。`flow_dimension` 固定为 `LOCATION/INSTITUTION/DISCIPLINE`；
`flow_level` 分别使用 `COUNTRY/PROVINCE/CITY`、`INSTITUTION` 或 `FIELD`。同一人才同一年同一有向边
只计一次，`talent_count` 为去重人才数，`mobility_event_count` 为去重事件数。`from_entity_id` 与
`to_entity_id` 必须不同。不得跨边求和后解释为全局去重人才数。

每条流向边当前只保存一个流向级主要原因。9.16.0固定使用
`reason_code='PERSONAL_DEVELOPMENT'`、`reason_label='个人发展原因'`、
`reason_analysis_method='BUSINESS_DEFAULT'`和
`reason_model_version='talent_mobility_reason_default_v1'`。这是产品当前统一展示分类，不是对边内每名人才
个人动机的事实认定。由于没有个人陈述、调查或其他原因证据，`reason_confidence`和`reason_evidence`
保持空，`reason_coverage_status='DEFAULT_ASSIGNED'`。前台原因标题必须读取`reason_label`，说明文字读取
`reason_description`；不得把`reason_code`直接展示给用户，也不得将默认分类改写成已验证的因果结论。

| 原因字段 | Doris 类型 | 说明 |
|---|---|---|
| `reason_code` | `VARCHAR(64) NOT NULL` | 稳定原因代码；当前固定`PERSONAL_DEVELOPMENT` |
| `reason_label` | `VARCHAR(128) NOT NULL` | 前台直接展示字段；当前固定“个人发展原因” |
| `reason_description` | `STRING NOT NULL` | 前台可选说明及非因果语义限制 |
| `reason_analysis_method` | `VARCHAR(32) NOT NULL` | 当前固定`BUSINESS_DEFAULT` |
| `reason_confidence` | `DECIMAL(5,4)` | 证据分析置信度；当前默认分类为空 |
| `reason_model_version` | `VARCHAR(64) NOT NULL` | 原因规则或模型版本 |
| `reason_evidence` | `VARIANT` | 有界原因证据；当前为空 |
| `reason_coverage_status` | `VARCHAR(32) NOT NULL` | 当前固定`DEFAULT_ASSIGNED` |

`ads_geo_yearly_metrics.inbound_talent_count` 和 `outbound_talent_count` 不直接相加流向边人数，而从
事件端点按 `location_id, event_year` 再次去重人才；同一人才同年从多个来源流入同一位置只计一人。
`mobility_event_count` 按涉及该位置的去重事件计数。2000—2026 已发布 Key 无严格事件时写0，
`mobility_coverage_status='PARTIAL'`；未运行本版本的行保持NULL和`NOT_READY`。

### 22.4 `ads_talent_mobility_flow_detail`

保存流向边详情弹窗使用的有界 TopN：`INSTITUTION_PAIR` 表示地区边上的代表起止机构对，
`PRIMARY_FIELD` 表示地区或机构边上迁移人才在事件年的主要 Field。每种明细按去重人才量降序，
再按稳定 ID 排序，最多10条。名称不复制到本表，分别关联机构画像和公共 Field 维表。

首版固定输入、覆盖边界、执行命令和核验查询见
[`docs/talent_mobility_mvp_v1.md`](docs/talent_mobility_mvp_v1.md)。

## 23. Schema 演进流程

修改 ADS 表、字段、Key、ID 语义或统计口径时，必须按以下顺序执行：

1. 修改本文件并提升版本。
2. 在 `ADS_SCHEMA_RELEASE_NOTES.md` 记录兼容性、迁移和数据影响。
3. 更新 Doris 建表 SQL 与在线迁移 SQL。
4. 更新生成程序、字段契约、加载程序和测试。
5. 迁移后核对 `information_schema`、行数、Key 唯一性和关键字段非空率。
6. 更新核验报告；不得用 `CREATE IF NOT EXISTS` 冒充旧表升级。

## 24. 技术点分析 ADS（4.6.0；6.0.0身份口径修订）

### 24.1 身份、中文字段与边界

6.0.0按产品确认口径，将每个入选 ETO `research_cluster_id` 直接认定为一个技术点，并为其确定性生成
`tcn_<32 hex>` 的 `technology_node_id`。`technology_node_id` 是本模块唯一技术点主键，
`research_cluster_id` 仅保留为ETO来源血缘，`node_identity_type`固定为
`ETO_RESEARCH_CLUSTER_TECHNOLOGY`。本模块不再连接上一版本正式Technology目录，删除易产生歧义的
`tech_id`和`mapping_status`字段。

`ads_technology_profile` 保存技术名称、说明和关键词的 `original/en/zh` 三组字段，以及翻译状态、
版本、来源和审核状态。技术名称中文译文已由操作方批量审核通过；说明和关键词中文字段仍可为空，
不得复制英文冒充中文。批量审核表示项目工作流批准，不改变 `DEEPSEEK_LLM` 来源，也不冒充官方术语。
论文、专利、机构和案例表只保存自身名称快照，通过 `technology_node_id` 关联技术画像。

### 24.2 功能点、实现表与使用方法

| 功能点 | 主表 | 辅助表 | 使用方法与当前状态 |
|---|---|---|---|
| 技术网络可视化 | `ads_technology_graph_edge` | `ads_technology_profile` | 按关系类型、证据等级和最低置信分筛边，再连接两端画像；587,252条候选关系 |
| 技术节点下钻 | `ads_technology_profile` | `ads_technology_paper`, `ads_technology_patent`, `ads_technology_institution`, `ads_technology_application_case` | 按同一节点ID查代表论文、专利、机构/企业和项目案例 |
| 语义热点提取 | `ads_technology_hotspot_signal` | `ads_technology_profile` | 当前是ETO标签关键词及年度代理，尚不是全文NLP新短语抽取 |
| 热点趋势分析 | `ads_technology_hotspot_yearly` | `ads_technology_hotspot_snapshot`, `ads_technology_yearly_metrics` | Yearly提供2015—2026完整年度论文、新增引用和热度曲线；Snapshot保留当前状态/排名 |
| 技术趋势关键节点 | `ads_technology_milestone_event` | `ads_technology_yearly_metrics`, `ads_technology_application_case` | 每技术每事件类型最多一条；提供起源、峰值、增长加速、首次专利和首次项目证据 |
| 潜力评估 | `ads_technology_potential_assessment` | `ads_technology_potential_dimension`, `ads_technology_potential_evidence` | 综合表筛选，dimension解释分项，evidence回溯论文/专利/项目 |
| 多技术对比 | `ads_technology_potential_dimension` | `ads_technology_potential_assessment` | 对选中节点按`dimension_code`透视生成雷达图；不保存临时对比 |
| 阶段自动判定 | `ads_technology_stage_assessment` | `ads_technology_assessment_evidence` | 当前发布可复算规则基线，不冒充联网LLM判断 |
| 用户参数研判 | 同上 | 下游应用Job/Prompt存储 | 字段支持Prompt/参数版本；当前没有用户自定义发布行 |
| 深圳数据提取 | `ads_technology_region_yearly_metrics` | `ads_technology_region_institution`, `ads_location` | 通过深圳稳定Location ID过滤；6,233个节点命中深圳证据 |
| 深圳潜力与阶段 | `ads_technology_region_assessment` | 区域事实表 | 查询区域评分、排名、阶段、优势、短板和建议，同时展示覆盖状态 |
| 技术转化流程 | `ads_technology_transfer_stage` | `ads_technology_bottleneck_assessment` | 按`stage_order`画8阶段流程并叠加堵点状态 |
| 堵点识别归因 | `ads_technology_bottleneck_assessment` | `ads_technology_bottleneck_evidence`, `ads_technology_data_coverage` | 当前是证据缺口诊断，不是专家确认因果；外部证据表为空 |
| 政策证据 | `ads_technology_policy_evidence` | `ads_technology_data_coverage` | 当前0行，必须显示`POLICY/NOT_AVAILABLE`，不能解释为无政策 |

深圳市稳定 ID 为 `loc_E16782C21F18EBF8A59C1E98F9C9860B`。应用应先从 `ads_location` 获取治理
ID，再查询区域表，不应按城市名称直接连接或在多个业务模块散落硬编码。

### 24.3 图谱与节点详情

`ads_technology_graph_edge` 一行一条候选关系，保存起止节点、关系类型、方向、证据等级、启发式
置信分、论文引用数与广度、方向优势、时间一致性、Topic Jaccard、共同Patent和family数。关系来源
固定为 `DWS_INFERRED`。有方向关系使用推断upstream作为source、downstream作为target；共演化和
Patent汇聚使用稳定排序端点。置信分只允许同关系类型排序，不是概率，也不证明产业供应链。

代表论文和代表专利分别来自DWS确定性Top 20。`ads_technology_institution` 合并论文署名、确认的专利
受让机构和项目机构证据，`is_company=true` 是关联企业筛选入口。`ads_technology_application_case`
当前全部为 `case_type='RESEARCH_PROJECT'`，只证明项目资助与seed论文的连接；
`market_status='NOT_VERIFIED_AS_MARKET_APPLICATION'`，不得显示成产品落地或商业成功案例。

### 24.4 热点算法

完整对照窗为2020—2022，近期窗为2023—2025。论文份额、作者扩散、机构扩散、专利信号和FWCI
分别转换为全部候选节点中的0—100百分位：

```text
relative_growth = (recent_avg_paper_share + 1e-12)
                / (baseline_avg_paper_share + 1e-12)

hotspot_score = 0.40 * growth_score
              + 0.15 * author_diffusion_score
              + 0.15 * institution_diffusion_score
              + 0.15 * impact_score
              + 0.15 * patent_signal_score
```

近期论文少于3篇为 `INSUFFICIENT_EVIDENCE`；其余按score和relative growth依次判定
`EMERGING/EARLY_EMERGING/WATCH/ESTABLISHED_GROWING/MATURE`。当前为3个EARLY_EMERGING、146个
WATCH、2,539个ESTABLISHED_GROWING、766个MATURE和15,976个证据不足。关键词趋势的
`trend_method='CLUSTER_LABEL_PROXY'` 表示把Cluster标签投影到年度事实，不是逐年全文短语频率。

### 24.5 产业化潜力算法

`technology_insight_mvp_v1` 在19,430个候选节点总体内计算六维百分位：

| 维度 | 权重 | 当前指标 |
|---|---:|---|
| `SCIENTIFIC_SCALE` | 0.20 | seed论文数 |
| `SCIENTIFIC_GROWTH` | 0.20 | 近期论文份额增长 |
| `SCIENTIFIC_IMPACT` | 0.15 | 近期FWCI |
| `PATENT_CONVERSION` | 0.20 | 关联Patent publication数 |
| `INDUSTRY_PARTICIPATION` | 0.15 | 关联company机构数 |
| `PROJECT_EVIDENCE` | 0.10 | 关联科研项目案例数 |

```text
potential_score = sum(dimension_score * dimension_weight for available dimensions)
                / sum(dimension_weight for available dimensions)
```

缺失指标不写0，通过 `metric_weight_coverage` 披露并按可用权重重归一。Project只证明科研项目关联，
company只证明论文、专利受让或项目机构关联，不能证明收入、产品化或市场成功。雷达图直接查询
dimension表，不建立用户组合表；既有 `ads_technology_commercial_value_simulation` 继续保持模拟语义，
不得覆盖本表。

### 24.6 阶段研判算法与交互边界

当前阶段表使用 `RULE_BASED_EVIDENCE_BASELINE`：

```text
无论文                                  -> UNCERTAIN
无专利且热点为EMERGING/EARLY_EMERGING   -> RAPID_DEVELOPMENT
无专利                                  -> EARLY_RESEARCH
有专利但无company证据                   -> ENGINEERING_VALIDATION
同时有company和project证据              -> EARLY_COMMERCIALIZATION
其他                                    -> ENGINEERING_VALIDATION
```

首版Cluster入选本身要求Patent–seed证据，因此实际为10,408个EARLY_COMMERCIALIZATION和9,022个
ENGINEERING_VALIDATION。它不是TRL认证或联网大模型结论。用户实时参数、联网搜索、Prompt、模型调用、
预算和私人上下文属于下游应用状态；只有固定证据截止日、Prompt版本、参数hash、模型版本并经审核的
结果才能作为新 `scenario_type` 发布到ADS。

### 24.7 区域、深圳与阶段算法

区域事实按城市Location聚合机构、company、论文、专利和项目机构证据：

```text
regional_raw = paper_evidence
             + 2 * patent_evidence
             + 2 * project_evidence
             + company_count
regional_potential_score = 同城市全部技术节点的 regional_raw 百分位
```

区域阶段规则为：无专利证据为EARLY_RESEARCH，有专利但无company为ENGINEERING_VALIDATION，否则为
EARLY_COMMERCIALIZATION。深圳已有15,630条技术年度行，覆盖6,233个节点、34,617个年度机构证据和
4,179个年度company证据。政策、市场、产品和真实落地案例未接入，因此区域评估固定披露
`evidence_coverage_status='PARTIAL_INTERNAL_EVIDENCE'`。

### 24.8 转化流程与堵点算法

固定阶段依次为BASIC_RESEARCH、PROOF_OF_CONCEPT、LAB_VALIDATION、PILOT_TEST、ENGINEERING、
REGULATORY_OR_STANDARDIZATION、INDUSTRIALIZATION和MARKET_SCALE。

当前堵点只诊断证据缺口：无项目案例生成 `PROJECT_EVIDENCE_GAP`，无专利生成
`PATENT_EVIDENCE_GAP`，无company生成 `ENTERPRISE_PARTICIPATION_GAP`；所有技术的MARKET_SCALE均
生成 `MARKET_DATA_UNAVAILABLE/UNKNOWN_EXTERNAL_DATA`。这些结果不能显示成专家确认的因果堵点。
`ads_technology_bottleneck_evidence` 当前0行，等待专家知识、试验、标准、监管、市场和供应链来源。

### 24.9 查询路径

```text
全景图：profile <- source/target_technology_node_id -> graph_edge
节点下钻：profile -> paper / patent / institution / application_case
热点曲线：hotspot_snapshot -> yearly_metrics
潜力雷达：potential_assessment -> potential_dimension
阶段解释：stage_assessment -> assessment_evidence
深圳分析：location -> region_yearly_metrics / region_institution / region_assessment
转化诊断：transfer_stage -> bottleneck_assessment -> bottleneck_evidence
缺失提示：profile -> data_coverage
```

### 24.10 当前缺失数据项

| 缺失项 | 影响功能 | 需要补充的最小事实 |
|---|---|---|
| 审核中文翻译 | 全部中文展示 | 名称、说明、关键词译文，翻译版本、来源、审核人和状态 |
| 顶级会议/期刊名单 | 热点发现 | Venue稳定ID、级别、学科、有效期和来源版本 |
| 全文/摘要语义短语 | 智能热点提取 | document ID、phrase、年份、模型、置信度、位置和语义cluster |
| 产品与应用落地 | 典型案例 | 产品/试点/部署ID、企业、客户、地点、阶段、日期、URL和审核状态 |
| 市场事实 | 潜力、阶段、规模化 | 市场规模、收入、采购、融资、客户采用、统计期、币种和来源 |
| 政策文件 | 深圳政策分析 | 政策ID、发布机构、日期、地域、正文、技术关联证据和URL |
| 标准与监管 | 阶段和堵点 | 标准/审批ID、状态、适用技术、机构、日期和来源 |
| 供应链关系 | 转化堵点 | 企业角色、上下游产品/部件、方向、地区、有效期和证据 |
| 专家知识与验证 | 堵点归因 | 阶段、堵点、原因、严重度、建议、专家/机构、审核状态和版本 |
| 产业分类映射扩展 | 产业分析 | `technology_node_id`到IPC/CPC/产业节点的版本化映射 |
| 更完整时间序列 | 热点和阶段 | 固定观察窗全量引用、专利、企业和市场年度事实 |

### 24.11 发布、恢复与验证

```bash
./scripts/build_research_cluster_enrichment_dws.sh
./scripts/publish_technology_ads_v1.sh
```

ADS先在 `iceberg.technology_ads_v1_20261016` 逐表原子物化并校验，再创建Doris 4.6.0表并按
`data_version=202610160201`加载。重复执行跳过已有Iceberg表；Doris目标版本行数与源相等时跳过，
否则写入后重新对账。22张表的逻辑Key重复、评分范围、候选身份、案例类型和POLICY/MARKET覆盖状态
均必须为0异常。报告位于 `reports/technology_ads_v1_20261016/`。

### 24.12 完整字段字典

以下字段定义与 Doris 4.6.0 DDL 保持一致。每张表均给出物理类型、字段含义和逻辑 Key；枚举值、算法公式及使用边界仍以前文为准。
字段注释只更新 Doris 元数据，不改变列名、类型、Key、数据版本或已发布数据；已有环境执行
`sql/doris/ads_schema_4_6_0_technology_comments.sql` 回填，新建环境直接使用带注释的建表 DDL。
Doris 禁止对 Key、HASH distribution 和作为 sequence column 的 `data_version` 执行本类
`MODIFY COLUMN`，因此已有表的这些列无法原位补注释；其定义仍在本字段字典中说明，新建表则在创建时
直接写入全部注释。

已有环境只需执行一次：

```bash
set -a
source .env
set +a
./scripts/compose.sh exec -T -e MYSQL_PWD="$DORIS_PASSWORD" doris-fe \
  mysql --protocol=TCP -h127.0.0.1 -P9030 -uroot \
  < sql/doris/ads_schema_4_6_0_technology_comments.sql
./scripts/compose.sh exec -T -e MYSQL_PWD="$DORIS_PASSWORD" doris-fe \
  mysql --protocol=TCP -h127.0.0.1 -P9030 -uroot \
  < sql/doris/ads_schema_4_7_0_technology_graph_comments.sql
```

重复执行时 Doris 会对已经一致的列返回 `Nothing is changed`；该脚本是一次性元数据迁移，不用于发布
业务数据。

#### 24.12.1 `ads_technology_profile`

技术点画像；每个入选ETO Research Cluster按当前产品口径认定为一个技术点。逻辑 Key：
`technology_node_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性技术点ID |
| 身份与关联 | `research_cluster_id` | `VARCHAR(64)` | 来源ETO研究簇ID |
| 状态与口径 | `node_identity_type` | `VARCHAR(32)` | 固定为`ETO_RESEARCH_CLUSTER_TECHNOLOGY` |
| 展示与说明 | `technology_name_original` | `STRING` | 技术原始名称 |
| 展示与说明 | `technology_name_en` | `STRING` | 技术英文名称 |
| 展示与说明 | `technology_name_zh` | `STRING` | 审核中文技术名称；当前19,430条均非空 |
| 展示与说明 | `technology_description_original` | `STRING` | 技术原始说明 |
| 展示与说明 | `technology_description_en` | `STRING` | 技术英文说明 |
| 展示与说明 | `technology_description_zh` | `STRING` | 审核中文技术说明；当前可为空 |
| 展示与说明 | `keywords_original` | `ARRAY<STRING>` | 原始关键词去重数组 |
| 展示与说明 | `keywords_en` | `ARRAY<STRING>` | 英文关键词去重数组 |
| 展示与说明 | `keywords_zh` | `ARRAY<STRING>` | 审核中文关键词数组；当前可为空 |
| 状态与口径 | `translation_status` | `VARCHAR(32)` | 翻译完成状态；当前统一为`APPROVED` |
| 版本与审计 | `translation_version` | `VARCHAR(64)` | 翻译规则或模型版本 |
| 状态与口径 | `translation_source` | `VARCHAR(32)` | 翻译来源类型 |
| 状态与口径 | `translation_review_status` | `VARCHAR(32)` | 翻译人工审核状态；当前统一为`APPROVED`，无`PENDING` |
| 展示与说明 | `domains_raw` | `STRING` | 来源Domain名称快照 |
| 展示与说明 | `fields_raw` | `STRING` | 来源Field名称快照 |
| 身份与关联 | `leading_topic_id` | `VARCHAR(64)` | 证据量领先的OpenAlex来源Topic ID；经identity bridge映射平台ID |
| 状态与口径 | `chain_role` | `VARCHAR(64)` | 技术链位置角色 |
| 状态与口径 | `is_chain_connected` | `BOOLEAN` | 是否连接到候选技术关系图 |
| 指标 | `upstream_dependency_count` | `BIGINT` | 上游依赖候选节点数 |
| 指标 | `downstream_cluster_count` | `BIGINT` | 下游候选节点数 |
| 指标 | `paper_count` | `BIGINT` | 去重论文数 |
| 指标 | `patent_count` | `BIGINT` | 去重专利publication数 |
| 指标 | `institution_count` | `BIGINT` | 去重关联机构数 |
| 指标 | `company_count` | `BIGINT` | 其中企业类型机构数 |
| 指标 | `project_case_count` | `BIGINT` | 关联科研项目案例数 |
| 指标 | `application_case_count` | `BIGINT` | 全部应用案例数；当前等于项目案例数 |
| 投资额估算 | `annual_investment_estimate_cny` | `DECIMAL(24,2)` | 规则模拟的全球年度研发及商业化投入基准值，人民币元 |
| 投资额估算 | `annual_investment_lower_cny` | `DECIMAL(24,2)` | 同口径规则模拟下界，人民币元 |
| 投资额估算 | `annual_investment_upper_cny` | `DECIMAL(24,2)` | 同口径规则模拟上界，人民币元 |
| 投资额估算 | `investment_estimate_year` | `SMALLINT` | 模拟年度；首版为2026 |
| 投资额估算 | `investment_estimate_currency` | `CHAR(3)` | 固定为`CNY` |
| 投资额估算 | `investment_estimate_scope` | `VARCHAR(64)` | 固定为`GLOBAL_RND_AND_COMMERCIALIZATION` |
| 投资额估算 | `investment_estimate_status` | `VARCHAR(32)` | 固定为`RULE_SIMULATED`，不表示真实市场金额已接入 |
| 投资额估算 | `investment_estimate_confidence` | `VARCHAR(16)` | 当前固定`LOW` |
| 投资额估算 | `investment_estimate_basis` | `STRING` | 中文模拟算法与口径边界 |
| 投资额估算 | `investment_estimate_uncertainties_json` | `STRING` | 主要不确定性JSON数组 |
| 投资额血缘 | `investment_estimate_model_version` | `VARCHAR(128)` | 生成模型版本；规则模拟时为空 |
| 投资额血缘 | `investment_estimate_prompt_version` | `VARCHAR(128)` | Prompt版本；规则模拟时为空 |
| 投资额血缘 | `investment_estimate_method_version` | `VARCHAR(64)` | 指标定义版本 |
| 投资额血缘 | `investment_estimate_input_hash` | `CHAR(64)` | 单条模型输入、Prompt和模型SHA-256 |
| 投资额血缘 | `investment_estimate_release_id` | `VARCHAR(128)` | 不可变估算发布ID |
| 投资额血缘 | `investment_estimate_generated_at` | `DATETIME(3)` | 模型生成UTC时间 |
| 版本与审计 | `source_release_id` | `VARCHAR(128)` | 固定来源发布ID |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

投资额首版是确定性规则模拟值，口径表述为评估年度内全球投入该技术研发、工程化和商业化活动的资本。
它不是市场规模、收入、采购额或单纯融资额，也没有注册的不可变市场金额事实来源。ETO技术簇之间存在
范围重叠，任何层级均不得把各技术估算金额求和解释为总投资。
列表可展示`annual_investment_estimate_cny`，但必须同时标注“模型估算”；悬停或详情应披露上下界、
评估年度、全球口径、低置信度和非事实提示。

首版规则先在全部19,430个技术点内分别计算论文数、专利数、企业数、项目数和产业化潜力的
`percent_rank`，再计算：

```text
investment_index = 0.20 * paper_percentile
                 + 0.25 * patent_percentile
                 + 0.25 * company_percentile
                 + 0.10 * project_percentile
                 + 0.20 * potential_percentile

base_cny = 10,000,000 * 10 ^ (3 * investment_index / 100) * stage_multiplier
lower_cny = base_cny * 0.4
upper_cny = base_cny * 2.5
```

阶段系数为基础/早期研究0.8，概念验证、实验室验证和快速发展0.9，试点、工程化和工程验证1.0，
监管/标准化1.1，产业化和早期商业化1.3，市场规模化1.5，未知阶段0.7。金额统一按人民币元计算并四舍
五入到十万元。最新阶段和潜力记录按`data_version DESC, assessment_id DESC`确定。

#### 24.12.2 `ads_technology_graph_edge`

候选技术节点之间的静态聚合关系；置信分不是概率。逻辑 Key：`edge_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `edge_id` | `VARCHAR(64) NOT NULL` | 候选技术关系确定性ID |
| 身份与关联 | `source_technology_node_id` | `VARCHAR(64)` | 关系起点候选技术节点ID |
| 身份与关联 | `target_technology_node_id` | `VARCHAR(64)` | 关系终点候选技术节点ID |
| 状态与口径 | `relation_type` | `VARCHAR(32)` | 关系类型 |
| 状态与口径 | `direction_status` | `VARCHAR(32)` | 关系方向判定状态 |
| 状态与口径 | `evidence_level` | `VARCHAR(16)` | HIGH、MEDIUM或LOW证据等级 |
| 指标 | `relation_confidence_score` | `DECIMAL(9,6)` | 同关系类型内可比较的启发式置信分 |
| 指标 | `total_citation_count` | `BIGINT` | 两簇间论文引用总次数 |
| 指标 | `dominant_citing_paper_count` | `BIGINT` | 主导方向引用论文数 |
| 指标 | `dominant_cited_paper_count` | `BIGINT` | 主导方向被引论文数 |
| 指标 | `dominant_direction_share` | `DECIMAL(9,6)` | 主导方向引用占双向引用比例 |
| 指标 | `dominant_temporal_consistency` | `DECIMAL(9,6)` | 主导方向引用的时间一致率 |
| 指标 | `shared_topic_count` | `BIGINT` | 两端共同Topic数 |
| 指标 | `topic_jaccard` | `DECIMAL(9,6)` | 两端Topic集合Jaccard系数 |
| 指标 | `shared_patent_count` | `BIGINT` | 两端共同关联专利数 |
| 指标 | `shared_patent_family_count` | `BIGINT` | 两端共同关联专利族数 |
| 状态与口径 | `relation_source` | `VARCHAR(32)` | 关系来源；当前固定DWS_INFERRED |
| 版本与审计 | `graph_release_id` | `VARCHAR(128)` | 固定图关系发布ID |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.3 `ads_technology_paper`

候选技术节点的确定性Top 20代表论文。逻辑 Key：`technology_node_id, paper_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `paper_id` | `VARCHAR(64) NOT NULL` | 平台论文ID |
| 指标 | `doi` | `STRING` | 论文DOI快照 |
| 展示与说明 | `paper_title_original` | `STRING` | 论文原始标题 |
| 展示与说明 | `paper_title_en` | `STRING` | 论文英文标题 |
| 展示与说明 | `paper_title_zh` | `STRING` | 论文中文标题；无审核译文时为空 |
| 时间 | `publication_year` | `INT` | 公开或发表年份 |
| 身份与关联 | `primary_topic_id` | `VARCHAR(64)` | 论文Primary Topic ID |
| 指标 | `cited_by_count` | `BIGINT` | 截至统计日累计被引次数 |
| 指标 | `fwci` | `DOUBLE` | 论文领域加权引用影响力 |
| 状态与口径 | `is_patent_linked_seed` | `BOOLEAN` | 是否为专利引用连接的seed论文 |
| 指标 | `related_patent_count` | `BIGINT` | 与该论文相关的去重专利数 |
| 指标 | `representative_rank` | `BIGINT` | 节点内确定性代表排名 |
| 状态与口径 | `selection_method` | `VARCHAR(64)` | 代表记录选择方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.4 `ads_technology_patent`

候选技术节点的确定性Top 20代表专利。逻辑 Key：`technology_node_id, patent_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `patent_id` | `VARCHAR(64) NOT NULL` | 平台专利ID |
| 指标 | `publication_number` | `VARCHAR(128)` | 专利公开号 |
| 指标 | `country_code` | `VARCHAR(8)` | 专利发布国家或地区代码 |
| 指标 | `kind_code` | `VARCHAR(16)` | 专利文献种类代码 |
| 身份与关联 | `google_family_id` | `VARCHAR(128)` | Google Patents专利族ID |
| 时间 | `priority_date` | `DATE` | 最早优先权日 |
| 时间 | `filing_date` | `DATE` | 申请日 |
| 时间 | `publication_date` | `DATE` | 公开日 |
| 时间 | `publication_year` | `INT` | 公开或发表年份 |
| 时间 | `grant_date` | `DATE` | 授权日 |
| 展示与说明 | `patent_title_original` | `STRING` | 专利原始标题 |
| 展示与说明 | `patent_title_en` | `STRING` | 专利英文标题 |
| 展示与说明 | `patent_title_zh` | `STRING` | 专利中文标题；无审核译文时为空 |
| 指标 | `evidence_count` | `BIGINT` | 支持当前关系的去重证据数 |
| 指标 | `cited_seed_paper_count` | `BIGINT` | 该专利引用的节点seed论文数 |
| 状态与口径 | `evidence_sources` | `ARRAY<STRING>` | 证据来源类型去重数组 |
| 指标 | `representative_rank` | `BIGINT` | 节点内确定性代表排名 |
| 状态与口径 | `selection_method` | `VARCHAR(64)` | 代表记录选择方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.5 `ads_technology_institution`

候选技术节点关联机构及论文、专利、项目证据汇总。逻辑 Key：`technology_node_id, institution_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `institution_id` | `VARCHAR(64) NOT NULL` | North Star统一机构ID |
| 展示与说明 | `institution_name_original` | `STRING` | 机构原始名称 |
| 展示与说明 | `institution_name_en` | `STRING` | 机构英文名称 |
| 展示与说明 | `institution_name_zh` | `STRING` | 机构中文名称 |
| 状态与口径 | `institution_type` | `VARCHAR(32)` | 稳定机构类型代码 |
| 状态与口径 | `is_company` | `BOOLEAN` | 是否为company类型机构 |
| 身份与关联 | `country_location_id` | `VARCHAR(64)` | 平台国家位置ID |
| 身份与关联 | `province_location_id` | `VARCHAR(64)` | 平台省级位置ID |
| 身份与关联 | `city_location_id` | `VARCHAR(64)` | 平台城市位置ID |
| 指标 | `paper_count` | `BIGINT` | 去重论文数 |
| 指标 | `patent_count` | `BIGINT` | 去重专利publication数 |
| 指标 | `project_count` | `BIGINT` | 去重关联科研项目数 |
| 时间 | `first_evidence_year` | `INT` | 首次观察到关系证据的年份 |
| 时间 | `latest_evidence_year` | `INT` | 最近观察到关系证据的年份 |
| 指标 | `institution_rank` | `BIGINT` | 节点内机构确定性排名 |
| 状态与口径 | `has_paper_evidence` | `BOOLEAN` | 是否具有论文署名机构证据 |
| 状态与口径 | `has_patent_evidence` | `BOOLEAN` | 是否具有确认专利机构证据 |
| 状态与口径 | `has_project_evidence` | `BOOLEAN` | 是否具有科研项目机构证据 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.6 `ads_technology_application_case`

候选技术节点关联科研项目案例；不是已验证市场应用。逻辑 Key：`technology_node_id, application_case_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `application_case_id` | `VARCHAR(64) NOT NULL` | 应用案例确定性ID |
| 状态与口径 | `case_type` | `VARCHAR(32)` | 案例类型；当前固定RESEARCH_PROJECT |
| 状态与口径 | `relation_type` | `VARCHAR(64)` | 关系类型 |
| 身份与关联 | `project_id` | `VARCHAR(64)` | 平台科研项目ID |
| 展示与说明 | `case_name` | `STRING` | 优先本地化的案例显示名 |
| 展示与说明 | `case_name_original` | `STRING` | 案例原始名称 |
| 展示与说明 | `case_name_en` | `STRING` | 案例英文名称 |
| 展示与说明 | `case_name_zh` | `STRING` | 案例中文名称 |
| 展示与说明 | `case_description` | `STRING` | 优先本地化的案例说明 |
| 展示与说明 | `case_description_en` | `STRING` | 案例英文说明 |
| 展示与说明 | `case_description_zh` | `STRING` | 案例中文说明 |
| 展示与说明 | `funder_name` | `STRING` | 资助机构名称快照 |
| 状态与口径 | `funding_type` | `VARCHAR(128)` | 资助类型快照 |
| 指标 | `funder_scheme` | `STRING` | 资助计划名称快照 |
| 时间 | `start_date` | `DATE` | 项目开始日期 |
| 时间 | `end_date` | `DATE` | 项目结束日期 |
| 时间 | `effective_start_year` | `INT` | 用于时间分析的项目起始年 |
| 时间 | `end_year` | `INT` | 项目结束年份 |
| 状态与口径 | `start_year_is_inferred` | `BOOLEAN` | 起始年是否由其他日期推断 |
| 状态与口径 | `source_url` | `STRING` | 来源页面URL |
| 指标 | `institution_count` | `BIGINT` | 去重关联机构数 |
| 指标 | `evidence_seed_paper_count` | `BIGINT` | 案例关联的seed论文数 |
| 时间 | `first_evidence_year` | `INT` | 首次观察到关系证据的年份 |
| 时间 | `latest_evidence_year` | `INT` | 最近观察到关系证据的年份 |
| 状态与口径 | `evidence_status` | `VARCHAR(64)` | 案例证据覆盖状态 |
| 指标 | `application_stage` | `VARCHAR(64)` | 应用阶段；当前仅科研项目代理 |
| 状态与口径 | `market_status` | `VARCHAR(64)` | 市场验证状态；当前未验证 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.7 `ads_technology_yearly_metrics`

候选技术节点年度论文、人才、机构及专利指标。逻辑 Key：`technology_node_id, statistics_year`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 时间 | `statistics_year` | `INT NOT NULL` | 统计年份 |
| 指标 | `paper_count` | `BIGINT` | 去重论文数 |
| 指标 | `total_observed_paper_count` | `BIGINT` | 同年全部候选节点观察论文数 |
| 指标 | `paper_share` | `DECIMAL(18,12)` | 节点论文数占同年观察论文数比例 |
| 指标 | `author_count` | `BIGINT` | 当年去重作者数 |
| 指标 | `new_author_count` | `BIGINT` | 当年首次进入节点的作者数 |
| 指标 | `institution_count` | `BIGINT` | 去重关联机构数 |
| 指标 | `new_institution_count` | `BIGINT` | 当年首次进入节点的机构数 |
| 指标 | `company_count` | `BIGINT` | 其中企业类型机构数 |
| 指标 | `cited_by_count` | `BIGINT` | 截至统计日累计被引次数 |
| 指标 | `avg_fwci` | `DOUBLE` | 当年有值论文的平均FWCI |
| 指标 | `patent_count` | `BIGINT` | 去重专利publication数 |
| 指标 | `patent_family_count` | `BIGINT` | 去重专利族数 |
| 时间 | `paper_to_patent_lag_years_avg` | `DOUBLE` | 论文到关联专利的平均年份间隔 |
| 状态与口径 | `coverage_status` | `VARCHAR(32)` | 数据覆盖状态 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.8 `ads_technology_hotspot_signal`

候选技术节点的标签关键词热点信号。逻辑 Key：`technology_node_id, signal_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `signal_id` | `VARCHAR(64) NOT NULL` | 热点信号确定性ID |
| 展示与说明 | `signal_text_original` | `STRING` | 信号原始文本 |
| 展示与说明 | `signal_text_en` | `STRING` | 信号英文文本 |
| 展示与说明 | `signal_text_zh` | `STRING` | 信号中文文本；无审核译文时为空 |
| 状态与口径 | `signal_type` | `VARCHAR(32)` | 信号类型 |
| 指标 | `keyword_rank` | `INT` | 关键词在节点内的稳定排名 |
| 状态与口径 | `extraction_method` | `VARCHAR(64)` | 信号提取方法 |
| 状态与口径 | `trend_method` | `VARCHAR(64)` | 年度趋势计算方法；当前为标签代理 |
| 时间 | `first_observed_year` | `INT` | 首次观察年份 |
| 时间 | `latest_observed_year` | `INT` | 最近观察年份 |
| 指标 | `evidence_paper_count` | `BIGINT` | 支持信号的论文数 |
| 状态与口径 | `translation_status` | `VARCHAR(32)` | 翻译完成状态；DeepSeek草稿为DRAFT_COMPLETE |
| 版本与审计 | `translation_version` | `VARCHAR(64)` | 翻译规则或模型版本；热点信号首版为technology_hotspot_signal_zh_v1 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

热点信号中文翻译按规范化原文去重调用DeepSeek，再展开回全部信号逻辑Key；执行方法见
[`docs/technology/TECHNOLOGY_HOTSPOT_SIGNAL_TRANSLATION.md`](docs/technology/TECHNOLOGY_HOTSPOT_SIGNAL_TRANSLATION.md)。
候选信号的技术性筛选必须按技术点整体比较，入选项的技术相似度和主题相关度必须同时达到发布门槛，
最多保留一项且允许全部拒绝；待执行流程、备份和恢复
方法见[`docs/technology/TECHNOLOGY_HOTSPOT_SIGNAL_FILTER.md`](docs/technology/TECHNOLOGY_HOTSPOT_SIGNAL_FILTER.md)。

#### 24.12.9 `ads_technology_hotspot_snapshot`

候选技术节点的版本化热点评分与状态。逻辑 Key：`technology_node_id, model_version`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 版本与审计 | `model_version` | `VARCHAR(64) NOT NULL` | 评估模型版本 |
| 指标 | `baseline_paper_count` | `BIGINT` | 对照期论文数量 |
| 指标 | `recent_paper_count` | `BIGINT` | 近期论文数量 |
| 指标 | `baseline_avg_paper_share` | `DECIMAL(18,12)` | 对照期平均论文份额 |
| 指标 | `recent_avg_paper_share` | `DECIMAL(18,12)` | 近期平均论文份额 |
| 指标 | `relative_growth` | `DECIMAL(18,8)` | 近期年均论文份额除以对照期年均份额 |
| 指标 | `recent_author_count` | `BIGINT` | 近期作者数量 |
| 指标 | `recent_new_author_count` | `BIGINT` | 近期新增作者数量 |
| 指标 | `recent_new_author_ratio` | `DECIMAL(9,6)` | 近期新增作者比例 |
| 指标 | `recent_institution_count` | `BIGINT` | 近期机构数量 |
| 指标 | `recent_new_institution_count` | `BIGINT` | 近期新增机构数量 |
| 指标 | `recent_new_institution_ratio` | `DECIMAL(9,6)` | 近期新增机构比例 |
| 指标 | `recent_patent_count` | `BIGINT` | 近期专利数量 |
| 指标 | `recent_avg_fwci` | `DOUBLE` | 近期论文平均领域加权引用影响力 |
| 指标 | `growth_score` | `DECIMAL(9,6)` | 增长得分 |
| 指标 | `author_diffusion_score` | `DECIMAL(9,6)` | 新增作者扩散百分位分 |
| 指标 | `institution_diffusion_score` | `DECIMAL(9,6)` | 新增机构扩散百分位分 |
| 指标 | `impact_score` | `DECIMAL(9,6)` | 科研影响百分位分 |
| 指标 | `patent_signal_score` | `DECIMAL(9,6)` | 专利信号得分 |
| 指标 | `hotspot_score` | `DECIMAL(9,6)` | 热点得分 |
| 指标 | `hotspot_rank` | `BIGINT` | 热点排名 |
| 状态与口径 | `hotspot_status` | `VARCHAR(32)` | 热点状态 |
| 风险 | `risk_score` | `DECIMAL(9,6)` | 证据与技术转化不确定性风险分，0–100且越高风险越高；仅`ASSESSED`有效 |
| 风险 | `risk_level` | `VARCHAR(16)` | `LOW/MEDIUM/HIGH`；仅`ASSESSED`有效 |
| 风险 | `risk_coverage_status` | `VARCHAR(32)` | `ASSESSED/INSUFFICIENT_EVIDENCE/INSUFFICIENT_RISK_METRICS/NOT_APPLICABLE` |
| 风险 | `risk_definition_version` | `VARCHAR(64)` | 风险公式、阈值和适用范围版本 |
| 风险 | `risk_summary` | `STRING` | 风险等级含义和证据边界中文说明 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

8.2.0发布`model_version='technology_insight_mvp_v3_evidence_risk'`，由固定的
`technology_insight_mvp_v2_eto_cluster_technology`逐行生成，不覆盖历史模型。风险适用范围只包括
`EMERGING`、`EARLY_EMERGING`、`WATCH`和`ESTABLISHED_GROWING`；`MATURE`标记
`NOT_APPLICABLE`，`INSUFFICIENT_EVIDENCE`不生成高、中、低等级。若四个风险输入任一缺失，标记
`INSUFFICIENT_RISK_METRICS`且分数、等级保持NULL。

风险定义版本固定为`technology_hotspot_evidence_risk_v1`，公式为：

```text
risk_score = 100 - (
    0.25 * author_diffusion_score
  + 0.25 * institution_diffusion_score
  + 0.25 * impact_score
  + 0.25 * patent_signal_score
)
```

`risk_score >= 80`为`HIGH`，`60 <= risk_score < 80`为`MEDIUM`，低于60为`LOW`。
该风险只衡量当前内部数据观察到的作者/机构扩散、科研影响和论文—专利连接综合支撑不足，属于证据与
技术转化不确定性指标。它不衡量技术安全危害、伦理、监管、投资损失、市场规模或商业成功概率，不得
用于准入、投资建议或自动决策；前端必须同时读取`risk_coverage_status`并展示该边界。

#### 24.12.9a `ads_technology_hotspot_yearly`

技术点年度论文、新增引用、热度指数及增长曲线。逻辑Key：
`technology_node_id, statistics_year, model_version`。本表不改变
`ads_technology_hotspot_signal`的关键词信号语义，也不以发表年累计被引冒充年度新增引用。

论文范围固定为ETO Cluster的`is_eto_top_paper=true`关系；`paper_count`按论文发表年统计，
`new_citation_count`按`dwd_work_count_by_year.year`统计该技术全部范围内论文在对应自然年新收到的引用。
2015—2026生成完整技术点×年度网格，零命中显式保存为0；按操作方要求，2026与其他年份一样标记
`coverage_status=COMPLETE`，不执行部分年折算。

论文活跃度和引用关注度分别使用同年、同主Subfield内`ln(1+count)`百分位；主Topic无法连接DWD Topic
时进入`UNCLASSIFIED`可比组。年度热度固定为：

```text
hotspot_score = 0.60 * paper_activity_score
              + 0.40 * citation_attention_score
```

首年同比为空；上年热度为0时同比率为空，避免无穷值。`rolling_3y_score`为含当年的三年移动平均；
`trend_status`只表示年度方向，不替代领域专家对短期热点或长期趋势的判断。完整输入Snapshot、运行命令
和发布核验见[`docs/technology_hotspot_yearly_v1.md`](docs/technology_hotspot_yearly_v1.md)。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性技术点ID |
| Key | `statistics_year` | `SMALLINT NOT NULL` | 自然统计年 |
| Key/版本 | `model_version` | `VARCHAR(64) NOT NULL` | 年度热度模型版本 |
| 学科 | `primary_subfield_source_id` | `VARCHAR(64) NOT NULL` | 主Topic对应OpenAlex Subfield来源ID；未映射为UNCLASSIFIED |
| 原始指标 | `paper_count` | `BIGINT NOT NULL` | 当年发表的ETO top/seed去重论文数 |
| 原始指标 | `new_citation_count` | `BIGINT NOT NULL` | 范围论文当年新收到的引用数 |
| 分母 | `total_observed_paper_count` | `BIGINT NOT NULL` | 同年全部技术点观察论文关系数 |
| 分母 | `total_observed_new_citation_count` | `BIGINT NOT NULL` | 同年全部技术点观察新增引用数 |
| 份额 | `paper_share`, `citation_share` | `DECIMAL(18,12)` | 技术点占同年观察总量比例 |
| 标准化 | `paper_activity_score` | `DECIMAL(9,6) NOT NULL` | 同年同主Subfield论文活跃度百分位分 |
| 标准化 | `citation_attention_score` | `DECIMAL(9,6) NOT NULL` | 同年同主Subfield引用关注度百分位分 |
| 指数 | `hotspot_score` | `DECIMAL(9,6) NOT NULL` | 0.60论文活跃度加0.40引用关注度 |
| 曲线 | `hotspot_score_yoy_change` | `DECIMAL(9,6)` | 同比变化量；首年为空 |
| 曲线 | `hotspot_score_yoy_rate` | `DECIMAL(18,8)` | 同比增长率；首年或上年为0时为空 |
| 曲线 | `rolling_3y_score` | `DECIMAL(9,6) NOT NULL` | 三年移动平均热度 |
| 状态 | `trend_status` | `VARCHAR(32) NOT NULL` | BASELINE/RISING/STABLE/DECLINING/INSUFFICIENT_EVIDENCE |
| 状态 | `coverage_status` | `VARCHAR(32) NOT NULL` | 本版本固定COMPLETE |
| 血缘 | `source_cluster_paper_snapshot_id` | `VARCHAR(32) NOT NULL` | 技术—论文Snapshot |
| 血缘 | `source_work_count_by_year_snapshot_id` | `VARCHAR(32) NOT NULL` | 年度引用Snapshot |
| 血缘 | `source_topic_snapshot_id` | `VARCHAR(32) NOT NULL` | Topic学科归属Snapshot |
| 审计 | `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| 审计 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 指标口径版本 |
| 审计 | `data_version` | `BIGINT NOT NULL` | 行级数据版本 |
| 审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.10 `ads_technology_potential_dimension`

候选技术产业化潜力的分维度评分。逻辑 Key：`technology_node_id, model_version, scenario_id, dimension_code`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 版本与审计 | `model_version` | `VARCHAR(64) NOT NULL` | 评估模型版本 |
| 身份与关联 | `scenario_id` | `VARCHAR(64) NOT NULL` | 评估情景ID |
| 身份与关联 | `dimension_code` | `VARCHAR(64) NOT NULL` | 潜力评估维度代码 |
| 指标 | `raw_value` | `DOUBLE` | 维度计算使用的原始指标值 |
| 指标 | `dimension_score` | `DECIMAL(9,6)` | 维度内0至100百分位分 |
| 指标 | `dimension_weight` | `DECIMAL(5,4)` | 该维度固定权重 |
| 指标 | `weighted_score` | `DECIMAL(9,6)` | 维度分乘以权重 |
| 状态与口径 | `coverage_status` | `VARCHAR(32)` | 数据覆盖状态 |
| 状态与口径 | `calculation_method` | `VARCHAR(128)` | 维度计算方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.11 `ads_technology_potential_assessment`

候选技术产业化潜力综合评估。逻辑 Key：`assessment_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `technology_node_id` | `VARCHAR(64)` | 确定性候选技术节点ID |
| 版本与审计 | `model_version` | `VARCHAR(64)` | 评估模型版本 |
| 身份与关联 | `scenario_id` | `VARCHAR(64)` | 评估情景ID |
| 指标 | `potential_score` | `DECIMAL(9,6)` | 按可用权重归一的潜力综合分 |
| 指标 | `potential_rank` | `BIGINT` | 可评分节点的稳定潜力排名 |
| 指标 | `potential_percentile` | `DECIMAL(9,6)` | 潜力综合分百分位 |
| 状态与口径 | `metric_weight_coverage` | `DECIMAL(5,4)` | 实际可用维度权重之和 |
| 状态与口径 | `assessment_status` | `VARCHAR(64)` | 评估覆盖或完成状态 |
| 状态与口径 | `assessment_method` | `VARCHAR(64)` | 评估方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.12 `ads_technology_potential_evidence`

候选技术潜力评估的可追溯证据。逻辑 Key：`assessment_id, evidence_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `evidence_id` | `VARCHAR(128) NOT NULL` | 评估内证据确定性ID |
| 状态与口径 | `evidence_type` | `VARCHAR(32)` | 论文、专利、项目或外部证据类型 |
| 身份与关联 | `source_entity_id` | `VARCHAR(64)` | 来源实体ID |
| 展示与说明 | `evidence_title` | `STRING` | 证据标题 |
| 时间 | `evidence_year` | `INT` | 证据年份 |
| 指标 | `evidence_rank` | `BIGINT` | 证据排名 |
| 展示与说明 | `evidence_summary` | `STRING` | 证据摘要 |
| 指标 | `evidence_direction` | `VARCHAR(32)` | 证据方向 |
| 指标 | `evidence_quality` | `VARCHAR(64)` | 证据质量等级 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.13 `ads_technology_stage_assessment`

候选技术发展阶段的规则或模型研判。逻辑 Key：`assessment_id`。
`stage_code` 必须引用 `ads_technology_transfer_stage.stage_code` 的八阶段代码域，不得使用
`UNCERTAIN`、`EARLY_RESEARCH`、`ENGINEERING_VALIDATION`、`EARLY_COMMERCIALIZATION` 等平行枚举；
证据不足时仍按当前可观察证据保守归入八阶段之一，并通过置信度、风险和证据覆盖字段表达不确定性。
当前确定性基线只会输出 `BASIC_RESEARCH`、`PROOF_OF_CONCEPT`、`ENGINEERING` 或
`INDUSTRIALIZATION`；由于尚无注册的监管、标准和市场事实来源，不得自动输出
`REGULATORY_OR_STANDARDIZATION` 或 `MARKET_SCALE`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `technology_node_id` | `VARCHAR(64)` | 确定性候选技术节点ID |
| 身份与关联 | `stage_code` | `VARCHAR(64) NOT NULL` | 引用`ads_technology_transfer_stage.stage_code`的八阶段代码 |
| 指标 | `stage_confidence` | `DECIMAL(5,4)` | 阶段置信 |
| 状态与口径 | `assessment_method` | `VARCHAR(64)` | 评估方法 |
| 展示与说明 | `current_status_description` | `STRING` | 当前阶段状态说明 |
| 展示与说明 | `key_bottleneck_summary` | `STRING` | 关键堵点摘要 |
| 指标 | `development_potential_score` | `DECIMAL(9,6)` | 引用的技术潜力综合分 |
| 展示与说明 | `risk_summary` | `STRING` | 风险摘要 |
| 展示与说明 | `action_recommendation` | `STRING` | 行动建议 |
| 展示与说明 | `typical_task_content` | `STRING` | 当前技术与阶段的模型生成典型任务；编号纯文本 |
| 展示与说明 | `representative_case_content` | `STRING` | 代表性案例示意；不是已核验商业成功案例 |
| 状态与口径 | `generated_content_type` | `VARCHAR(32)` | 展示内容性质；首版固定`LLM_DEMONSTRATION` |
| 模型血缘 | `content_provider` | `VARCHAR(64)` | 展示内容实际模型服务提供方 |
| 模型血缘 | `content_model_version` | `VARCHAR(128)` | 展示内容实际模型名称或版本 |
| 模型血缘 | `content_prompt_version` | `VARCHAR(64)` | 展示内容固定Prompt版本 |
| 模型血缘 | `content_input_hash` | `VARCHAR(64)` | 规范化技术、阶段及证据输入SHA-256 |
| 状态与口径 | `content_review_status` | `VARCHAR(48)` | 展示内容审核状态 |
| 模型血缘 | `content_generated_at` | `DATETIME(3)` | 展示内容模型生成时间UTC |
| 模型血缘 | `content_evidence` | `VARIANT` | 案例性质、支撑证据ID、不确定性和置信度快照 |
| 版本与审计 | `model_version` | `VARCHAR(64)` | 评估模型版本 |
| 版本与审计 | `prompt_version` | `VARCHAR(64)` | 生成式评估Prompt版本；规则基线为空 |
| 指标 | `parameter_hash` | `VARCHAR(64)` | 参数哈希 |
| 状态与口径 | `scenario_type` | `VARCHAR(32)` | 情景类型 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.14 `ads_technology_assessment_evidence`

候选技术阶段研判的可追溯证据。逻辑 Key：`assessment_id, evidence_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `evidence_id` | `VARCHAR(128) NOT NULL` | 评估内证据确定性ID |
| 状态与口径 | `evidence_type` | `VARCHAR(32)` | 论文、专利、项目或外部证据类型 |
| 身份与关联 | `source_entity_id` | `VARCHAR(64)` | 来源实体ID |
| 展示与说明 | `evidence_title` | `STRING` | 证据标题 |
| 时间 | `evidence_year` | `INT` | 证据年份 |
| 展示与说明 | `evidence_summary` | `STRING` | 证据摘要 |
| 指标 | `evidence_direction` | `VARCHAR(32)` | 证据方向 |
| 指标 | `evidence_quality` | `VARCHAR(64)` | 证据质量等级 |
| 状态与口径 | `source_url` | `STRING` | 来源页面URL |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.15 `ads_technology_region_yearly_metrics`

候选技术在城市位置的年度机构证据指标。逻辑 Key：`technology_node_id, location_id, statistics_year`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `location_id` | `VARCHAR(64) NOT NULL` | 平台位置ID；当前区域粒度为城市 |
| 时间 | `statistics_year` | `INT NOT NULL` | 统计年份 |
| 身份与关联 | `country_location_id` | `VARCHAR(64)` | 平台国家位置ID |
| 身份与关联 | `province_location_id` | `VARCHAR(64)` | 平台省级位置ID |
| 身份与关联 | `city_location_id` | `VARCHAR(64)` | 平台城市位置ID |
| 展示与说明 | `location_name` | `STRING` | 位置显示名称 |
| 展示与说明 | `location_name_en` | `STRING` | 位置名称英文 |
| 展示与说明 | `location_name_zh` | `STRING` | 位置中文名称 |
| 指标 | `institution_count` | `BIGINT` | 去重关联机构数 |
| 指标 | `company_count` | `BIGINT` | 其中企业类型机构数 |
| 指标 | `paper_institution_evidence_count` | `BIGINT` | 论文机构证据数量 |
| 指标 | `patent_institution_evidence_count` | `BIGINT` | 专利机构证据数量 |
| 指标 | `project_institution_evidence_count` | `BIGINT` | 项目机构证据数量 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.16 `ads_technology_region_institution`

候选技术在城市位置的关联机构证据汇总。逻辑 Key：`technology_node_id, location_id, institution_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `location_id` | `VARCHAR(64) NOT NULL` | 平台位置ID；当前区域粒度为城市 |
| 身份与关联 | `institution_id` | `VARCHAR(64) NOT NULL` | North Star统一机构ID |
| 展示与说明 | `institution_name_original` | `STRING` | 机构原始名称 |
| 展示与说明 | `institution_name_en` | `STRING` | 机构英文名称 |
| 展示与说明 | `institution_name_zh` | `STRING` | 机构中文名称 |
| 状态与口径 | `institution_type` | `VARCHAR(32)` | 稳定机构类型代码 |
| 状态与口径 | `is_company` | `BOOLEAN` | 是否为company类型机构 |
| 指标 | `paper_count` | `BIGINT` | 去重论文数 |
| 指标 | `patent_count` | `BIGINT` | 去重专利publication数 |
| 指标 | `project_count` | `BIGINT` | 去重关联科研项目数 |
| 时间 | `first_evidence_year` | `INT` | 首次观察到关系证据的年份 |
| 时间 | `latest_evidence_year` | `INT` | 最近观察到关系证据的年份 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.17 `ads_technology_region_assessment`

候选技术在城市位置的版本化潜力与阶段评估。逻辑 Key：`technology_node_id, location_id, model_version`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `location_id` | `VARCHAR(64) NOT NULL` | 平台位置ID；当前区域粒度为城市 |
| 版本与审计 | `model_version` | `VARCHAR(64) NOT NULL` | 评估模型版本 |
| 展示与说明 | `location_name` | `STRING` | 位置显示名称 |
| 展示与说明 | `location_name_zh` | `STRING` | 位置中文名称 |
| 指标 | `regional_potential_score` | `DECIMAL(9,6)` | 同城市候选技术区域潜力百分位分 |
| 指标 | `regional_rank` | `BIGINT` | 同城市候选技术稳定排名 |
| 指标 | `institution_count` | `BIGINT` | 去重关联机构数 |
| 指标 | `company_count` | `BIGINT` | 其中企业类型机构数 |
| 指标 | `paper_evidence_count` | `BIGINT` | 区域论文机构证据数 |
| 指标 | `patent_evidence_count` | `BIGINT` | 区域专利机构证据数 |
| 指标 | `project_evidence_count` | `BIGINT` | 区域项目机构证据数 |
| 指标 | `regional_stage_code` | `VARCHAR(64)` | 区域证据推断的发展阶段 |
| 展示与说明 | `strength_summary` | `STRING` | 区域优势摘要 |
| 展示与说明 | `weakness_summary` | `STRING` | 区域短板摘要 |
| 展示与说明 | `recommendation` | `STRING` | 区域发展建议 |
| 状态与口径 | `evidence_coverage_status` | `VARCHAR(64)` | 区域证据域覆盖状态 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.18 `ads_technology_policy_evidence`

候选技术在地区的政策证据；当前预留空表。逻辑 Key：`technology_node_id, location_id, policy_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `location_id` | `VARCHAR(64) NOT NULL` | 平台位置ID；当前区域粒度为城市 |
| 身份与关联 | `policy_id` | `VARCHAR(64) NOT NULL` | 政策文件ID |
| 展示与说明 | `policy_name` | `STRING` | 政策名称 |
| 指标 | `issuing_body` | `STRING` | 政策发布机构 |
| 时间 | `publication_date` | `DATE` | 公开日 |
| 指标 | `applicability_scope` | `STRING` | 政策适用范围 |
| 状态与口径 | `relation_method` | `VARCHAR(64)` | 政策与技术的关联方法 |
| 状态与口径 | `source_url` | `STRING` | 来源页面URL |
| 状态与口径 | `review_status` | `VARCHAR(32)` | 人工审核状态 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.19 `ads_technology_transfer_stage`

技术转化八阶段定义与展示顺序。逻辑 Key：`stage_code`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `stage_code` | `VARCHAR(64) NOT NULL` | 技术发展或转化阶段代码 |
| 指标 | `stage_order` | `INT` | 转化阶段展示顺序 |
| 展示与说明 | `stage_name_zh` | `STRING` | 阶段中文名称 |
| 展示与说明 | `stage_name_en` | `STRING` | 阶段英文名称 |
| 展示与说明 | `stage_description_zh` | `STRING` | 阶段中文说明 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.20 `ads_technology_bottleneck_assessment`

候选技术在转化阶段的证据缺口评估。逻辑 Key：`assessment_id, stage_code, bottleneck_code`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `stage_code` | `VARCHAR(64) NOT NULL` | 技术发展或转化阶段代码 |
| 身份与关联 | `bottleneck_code` | `VARCHAR(64) NOT NULL` | 堵点代码 |
| 身份与关联 | `technology_node_id` | `VARCHAR(64)` | 确定性候选技术节点ID |
| 状态与口径 | `bottleneck_status` | `VARCHAR(64)` | 堵点状态 |
| 指标 | `severity_score` | `INT` | 严重度得分 |
| 指标 | `reason_category` | `VARCHAR(64)` | 原因分类 |
| 展示与说明 | `reason_description` | `STRING` | 原因说明 |
| 展示与说明 | `improvement_recommendation` | `STRING` | 改进建议 |
| 状态与口径 | `assessment_method` | `VARCHAR(64)` | 评估方法 |
| 版本与审计 | `model_version` | `VARCHAR(64)` | 评估模型版本 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.21 `ads_technology_bottleneck_evidence`

技术转化堵点评估的外部证据；当前预留空表。逻辑 Key：`assessment_id, stage_code, evidence_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估结果确定性ID |
| 身份与关联 | `stage_code` | `VARCHAR(64) NOT NULL` | 技术发展或转化阶段代码 |
| 身份与关联 | `evidence_id` | `VARCHAR(128) NOT NULL` | 评估内证据确定性ID |
| 状态与口径 | `evidence_type` | `VARCHAR(32)` | 论文、专利、项目或外部证据类型 |
| 身份与关联 | `source_entity_id` | `VARCHAR(64)` | 来源实体ID |
| 展示与说明 | `evidence_summary` | `STRING` | 证据摘要 |
| 指标 | `evidence_quality` | `VARCHAR(64)` | 证据质量等级 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 24.12.22 `ads_technology_data_coverage`

候选技术各数据域的覆盖状态与缺口说明。逻辑 Key：`technology_node_id, domain_code`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `domain_code` | `VARCHAR(64) NOT NULL` | 数据域代码 |
| 指标 | `evidence_count` | `BIGINT` | 支持当前关系的去重证据数 |
| 状态与口径 | `coverage_status` | `VARCHAR(64)` | 数据覆盖状态 |
| 展示与说明 | `coverage_note` | `STRING` | 覆盖状态或缺口说明 |
| 市场热度 | `market_heat_score` | `TINYINT` | 0–100模型估计分；仅`MARKET/MODEL_ESTIMATED`有效 |
| 市场热度 | `market_heat_level` | `VARCHAR(32)` | `VERY_HIGH/HIGH/MEDIUM/LOW/VERY_LOW` |
| 市场热度 | `market_heat_drivers_json` | `STRING` | 热度驱动因素JSON数组 |
| 市场热度 | `market_heat_uncertainties_json` | `STRING` | 市场化不确定性JSON数组 |
| 市场热度 | `market_heat_confidence` | `VARCHAR(16)` | `LOW/MEDIUM/HIGH`模型估计置信度 |
| 市场热度 | `market_heat_estimation_basis` | `VARCHAR(128)` | 模型估计依据类型 |
| 市场热度 | `market_heat_model_version` | `VARCHAR(128)` | 生成模型版本 |
| 市场热度 | `market_heat_prompt_version` | `VARCHAR(128)` | Prompt版本 |
| 市场热度 | `market_heat_generated_at` | `DATETIME(3)` | 模型生成UTC时间 |
| 版本与审计 | `source_release_id` | `VARCHAR(128)` | 固定来源发布ID |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 指标口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

MARKET域没有注册的不可变市场事实来源时，普通技术保持`NOT_AVAILABLE`且市场热度字段为NULL。允许对明确
标识的候选集写入`MODEL_ESTIMATED`模型估计；此状态不表示市场事实已接入，`evidence_count`保持0，且
必须同时保留模型、Prompt、估计依据、置信度和生成时间。`coverage_note`保存面向展示的估计摘要。

#### 24.12.23 `ads_technology_milestone_event`

为技术趋势折线图保存可复算的简短关键节点。逻辑 Key：`event_id`；该ID由技术节点、事件类型和事件年
确定性生成。每个技术点每种事件类型最多一条。首版不调用大模型，所有模型血缘字段为空；不得把规则
节点展示为专家认定的重大突破、产业化成功或因果结论。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `event_id` | `VARCHAR(64) NOT NULL` | 技术节点、事件类型和年份生成的确定性ID |
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 关联技术点ID |
| 时间 | `event_year` | `INT NOT NULL` | 事件对应真实观察年份 |
| 时间 | `comparison_year` | `INT` | 增长事件的上一观察年份 |
| 状态与口径 | `event_type` | `VARCHAR(32) NOT NULL` | 五类事件枚举 |
| 展示与说明 | `event_title_zh`, `event_summary_zh` | `VARCHAR(128), STRING NOT NULL` | 简短标题及事实摘要 |
| 状态与口径 | `event_nature` | `VARCHAR(32) NOT NULL` | 首版固定`DETERMINISTIC_DERIVATION` |
| 指标 | `metric_name` | `VARCHAR(64) NOT NULL` | 触发事件的指标 |
| 指标 | `metric_value`, `previous_metric_value` | `DOUBLE` | 当前值与对比值 |
| 指标 | `growth_rate` | `DECIMAL(18,8)` | 相对上一观察年的增长率 |
| 指标 | `significance_score` | `DECIMAL(9,6) NOT NULL` | 0—100展示排序启发式分，不是概率 |
| 指标 | `confidence` | `DECIMAL(5,4) NOT NULL` | 规则识别稳定性，不是事实真实性概率 |
| 溯源 | `source_table`, `source_record_id` | `VARCHAR NOT NULL` | 直接支撑事件的ADS表和逻辑记录 |
| 溯源 | `evidence_title`, `evidence_coverage_status` | `STRING, VARCHAR` | 可用的项目标题及来源覆盖状态 |
| 状态与口径 | `derivation_method` | `VARCHAR(128) NOT NULL` | 候选选择、门槛和并列规则版本 |
| 审核 | `review_status` | `VARCHAR(32) NOT NULL` | 首版固定`AUTO_VALIDATED` |
| 模型血缘 | `inference_provider`, `inference_model`, `inference_prompt_version` | `VARCHAR` | 首版均为空 |
| 模型血缘 | `inference_input_hash`, `inference_generated_at` | `CHAR(64), DATETIME(3)` | 首版均为空 |
| 版本与审计 | `metrics_as_of_date`, `metric_definition_version` | `DATE, VARCHAR(64) NOT NULL` | 截止日和事件口径版本 |
| 版本与审计 | `data_version`, `update_time` | `BIGINT, DATETIME(3) NOT NULL` | 数据版本和UTC生成时间 |

事件口径固定如下：

- `ORIGIN`：最早`paper_count>0`的年份。
- `PUBLICATION_PEAK`：论文数最大年份，并列时取最早年份。
- `GROWTH_ACCELERATION`：上一观察年论文数大于0、当前不少于3篇且增长至少50%的候选中取增长率最高者。
- `FIRST_PATENT`：最早`patent_count>0`的年份。
- `FIRST_PROJECT`：按`effective_start_year, application_case_id`稳定选择最早科研项目证据；项目关联仍不等于市场应用。

前端按`technology_node_id`和展示年份查询，使用`event_year`定位折线节点，展示
`event_title_zh/event_summary_zh`；增长详情直接使用`comparison_year/previous_metric_value/metric_value/growth_rate`，
不应从摘要文本反解析数值。

#### 24.12.24 完美技术动态（9.22.0）

首版发布`technology_dynamic_perfect_v1_20261108`，从已通过DeepSeek技术性筛选的
`ads_technology_hotspot_signal`与可复算`ads_technology_milestone_event`中确定15条完整候选。
候选必须具有非空中文技术名及热点名、至少5篇热点支持论文、2025年`RISING`趋势、正热度同比、
专利和项目证据，并限制同一一级Domain最多3条、相同热点词最多1条。主事件限定为2021—2025年，
优先增长加速、首次专利、首次项目和论文峰值。候选排序分只用于策展，不是技术价值或成功概率。

`ads_technology_dynamic`是一条动态一行的头表，保存技术名称、热点名称、变化率、提及次数、领域标签、
主关键事件、展示排名和证据计数。变化率固定为2025年`hotspot_score_yoy_rate`；提及次数固定为
`HOTSPOT_SIGNAL_SUPPORTING_PAPER_COUNT`，即支持入选热点信号的去重论文数，不混加专利、项目和
选择性媒体样本。`change_rate`按比例值存储，`2.6614583`表示`266.14583%`；前端可直接使用
`change_rate_percent`，`change_rate_unit`固定为`RATIO`。

`ads_technology_dynamic_content`保存DeepSeek基于固定证据包补全的`event_detail_zh`、
`research_background_zh`和`industry_impact_zh`。每行保存Provider、Model、Prompt、输入Hash、生成时间、
逐陈述证据映射和审核状态。首版15条均为`deepseek-openai-compatible/deepseek-flash`；
`impact_nature`区分`EVIDENCE_SUPPORTED/POTENTIAL_IMPACT/INSUFFICIENT_EVIDENCE`。科研项目不得写成
商业落地，专利数量不得写成市场规模或收入。

`ads_technology_dynamic_event_content`是事件详情的正式消费表，每个`EVENT`证据严格对应一行，逐事件保存
`event_detail_zh`、`research_background_zh`和`industry_impact_zh`及模型血缘。旧动态级content表保留用于
兼容已有消费者，但不得再用作单个事件详情。DeepSeek输入严格缩减为技术动态标题，以及对应论文、专利、
项目的标题和简介；模型不接收或决定实体ID，关联ID由程序确定性写入。

`ads_technology_dynamic_evidence`只固化`EVENT`。每项动态保留三类代表性事件：排名第一论文的
`PAPER_PUBLICATION`、排名第一专利的`PATENT_APPLICATION`、排名第一项目的`PROJECT_START`；不再把
增长加速、论文峰值等聚合指标作为关键事件。`event_time_point/event_time_precision`保存事件时间点及精度，
`related_paper_id/related_patent_id/related_project_id`中严格只有对应类型的一列非空，当前15条动态共45行。
趋势不再复制到本表，直接按`technology_node_id`读取`ads_technology_hotspot_yearly`；相关成果列表分别读取
`ads_technology_paper`、`ads_technology_patent`、`ads_technology_application_case`并联接profile表。
`PAPER.evidence_id`统一为`ads_paper_profile.paper_id`，`PATENT.evidence_id`统一为
`ads_patent_profile.patent_id`；技术关系表原始ID保存在`source_entity_id`。内容表的supporting ID与证据表
使用同一组统一ID。所有证据标题在写入前移除HTML标签。论文链接优先使用来源落地页或DOI，
专利链接使用Google Patents，项目使用来源URL；无来源URL时保持空，不生成伪链接。

完整执行、口径与验收见
[`docs/technology_dynamic_perfect_v1.md`](docs/technology_dynamic_perfect_v1.md)及
[`reports/technology_dynamic_perfect_v1_20261108/publication_report.md`](reports/technology_dynamic_perfect_v1_20261108/publication_report.md)。

### 24.13 论文证据颠覆性技术候选基线（5.18.0）

本版本新增的“颠覆性”只表示需要进一步复核的技术候选，不是技术替代、产业颠覆、市场成功或专家认定
结论。发布模型`paper_disruption_proxy_v1_3`读取同一不可变Technology ADS发布中的候选技术画像、代表论文
和热点评分快照，不读取联网数据，不调用LLM，也不修改既有4.6.0结果。

每个候选技术先聚合代表论文的被引、FWCI、高影响论文和论文—专利连接，再将以下指标转换为固定
19,430个节点总体内的0—100百分位：

```text
disruption_proxy_score = 0.25 * citation_impact_score
                       + 0.25 * field_normalized_impact_score
                       + 0.20 * breakthrough_paper_score
                       + 0.15 * patent_linkage_score
                       + 0.15 * research_growth_score
```

其中引用影响使用代表论文`ln(1+cited_by_count)`均值，领域归一影响使用平均FWCI，高影响论文固定为
`fwci >= 3.0`，专利连接使用`is_patent_linked_seed`占比并以关联专利数稳定排序，科研增长复用固定
2020—2022对照期和2023—2025近期窗的论文份额增长百分位。

至少5篇代表论文、近期至少3篇论文，并具有引用与FWCI覆盖时才能进入正式评分。综合分不低于80、
引用影响和领域归一影响均不低于70，且专利连接或科研增长至少一项不低于80，标记为
`DISRUPTIVE_CANDIDATE`；综合分不低于70的其余合格节点标记`HIGH_IMPACT_WATCH`。门槛未满足固定为
`INSUFFICIENT_EVIDENCE`，其余为`NOT_FLAGGED`。首轮预检模型`paper_disruption_proxy_v1`使用85分与
60分辅助门槛，未产生候选；v1.2进一步将NULL显式置于百分位最低端，但85分门槛仍高于真实总体最高
综合分81.100160。因此不覆盖任一预检结果，而以v1.3将综合门槛校准为80并保持辅助信号门槛80。
阈值、输入Snapshot、模型版本和生成时间全部固定在
发布配置中；修改任何口径必须创建新模型和新数据版本。

v1.3曾发布`DISRUPTIVE_CANDIDATE` 2条和`HIGH_IMPACT_WATCH` 90条。5.18.1依据操作方明确业务决定，
在新模型`paper_disruption_proxy_v1_4_operator_promoted`中把两类统一标记为
`DISRUPTIVE_CANDIDATE`：最低证据门槛保持不变，综合分不低于70即进入候选，不再保留独立观察标签。
v1.4实际发布19,430条评估：`DISRUPTIVE_CANDIDATE` 92条、`NOT_FLAGGED` 3,179条、
`INSUFFICIENT_EVIDENCE` 16,159条；92个候选共有1,026条逐篇论文证据。该提升属于操作方批准的展示/业务
分类，不表示新增了市场替代、产业格局变化或专家验证证据；前端仍必须显示代理口径与复核提示。
6.0.0以相同公式和门槛发布`paper_disruption_proxy_v1_5_eto_technology_identity`，固定读取
`technology_ads_v2_20261026`，把评估对象正式解释为当前技术点清单中的技术点；评分和92条候选集合不变。

#### 24.13.1 `ads_technology_disruption_assessment`

逻辑Key：`assessment_id`。每个候选技术节点、模型版本生成一个确定性评估ID。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| 身份 | `assessment_id` | `VARCHAR(64) NOT NULL` | 评估确定性ID |
| 身份 | `technology_node_id` | `VARCHAR(64)` | 候选技术节点ID |
| 展示 | `technology_name_original` | `STRING` | 评估时固定的原始名称 |
| 展示 | `technology_name_zh` | `STRING` | 从已批准、内容哈希固定的翻译交付seed冗余的中文技术名称 |
| 学科 | `leading_topic_id` | `VARCHAR(64)` | 从画像冗余的OpenAlex来源Topic ID（`T…`） |
| 学科 | `leading_topic_name_zh` | `STRING` | 已批准中文本地化优先、DWD中文名回退的Topic名称快照 |
| 学科 | `leading_topic_name_en` | `STRING` | DWD英文名优先、OpenAlex原始名回退的Topic名称快照 |
| 版本 | `model_version` | `VARCHAR(64)` | 固定模型版本 |
| 结论 | `disruption_status` | `VARCHAR(32)` | 候选、观察、未标记或证据不足 |
| 指标 | `disruption_proxy_score` | `DECIMAL(9,6)` | 论文证据代理综合分，不是概率 |
| 指标 | `disruption_rank` | `BIGINT` | 合格节点内稳定排名；证据不足为空 |
| 分项 | `citation_impact_score` | `DECIMAL(9,6)` | 对数引用均值百分位 |
| 分项 | `field_normalized_impact_score` | `DECIMAL(9,6)` | 平均FWCI百分位 |
| 分项 | `breakthrough_paper_score` | `DECIMAL(9,6)` | 高影响论文占比百分位 |
| 分项 | `patent_linkage_score` | `DECIMAL(9,6)` | 论文—专利连接百分位 |
| 分项 | `research_growth_score` | `DECIMAL(9,6)` | 科研增长百分位 |
| 证据 | `representative_paper_count` | `BIGINT` | 代表论文数 |
| 证据 | `citation_covered_paper_count` | `BIGINT` | 引用计数覆盖论文数 |
| 证据 | `total_citation_count` | `BIGINT` | 代表论文累计被引之和 |
| 证据 | `avg_fwci`, `max_fwci` | `DECIMAL(18,6)` | 平均/最高FWCI |
| 证据 | `high_impact_paper_count`, `high_impact_paper_ratio` | `BIGINT/DECIMAL` | 高影响论文数与占比 |
| 证据 | `patent_linked_paper_count`, `related_patent_count` | `BIGINT` | 专利连接论文和关联专利数 |
| 证据 | `patent_linked_paper_ratio` | `DECIMAL(9,6)` | 专利连接论文占比 |
| 窗口 | `baseline_paper_count`, `recent_paper_count` | `BIGINT` | 对照期与近期论文数 |
| 状态 | `assessment_status` | `VARCHAR(64)` | 是否满足最低论文证据门槛 |
| 状态 | `assessment_method` | `VARCHAR(64)` | 固定论文证据代理方法 |
| 边界 | `interpretation_note` | `STRING` | 页面必须展示的解释边界 |
| 模型详情 | `detail_content` | `STRING` | 智谱仅基于固定评分、代表论文与代表专利生成的中文详细内容 |
| 模型详情 | `impact_assessment` | `STRING` | 智谱生成的潜在科研影响、技术转化影响与不确定性评估 |
| 模型审计 | `detail_generation_method` | `VARCHAR(64)` | 固定为证据约束摘要方法 |
| 模型审计 | `detail_model_version`、`detail_prompt_version` | `VARCHAR` | 模型与Prompt版本 |
| 模型审计 | `detail_review_status` | `VARCHAR(32)` | 首版固定`PENDING_REVIEW`，不得冒充专家确认结论 |
| 模型审计 | `detail_generated_at` | `DATETIME(3)` | UTC生成时间 |
| 模型证据 | `detail_evidence_paper_count`、`detail_evidence_patent_count` | `INT` | 实际进入模型上下文的代表论文、专利数量 |
| 审计 | `metrics_as_of_date`, `metric_definition_version` | `DATE/VARCHAR` | 统计截止日与口径版本 |
| 审计 | `data_version`, `update_time` | `BIGINT/DATETIME(3)` | 数据版本与生成时间 |

详情字段的正式上游发布为
`iceberg.technology_disruption_dwd_v1_20261030.dwd_technology_disruption_detail`。Doris仅冗余当前
92条候选的展示字段，DWD保留provider、逐条input_hash、固定评估版本和公共血缘字段。首版文本按
操作方明确指示原样发布；`detail_review_status=PENDING_REVIEW`必须与正文同时查询和展示，不能因已
进入DWD/ADS就解释为专家已确认。

2026-10-30生产对账：DWD Snapshot `3485583994851802092`共92行；Doris当前模型版本的92条
`DISRUPTIVE_CANDIDATE`均已写入详情，`data_version=202610290801`，详情和影响评估缺失数均为0，
论文与专利证据计数总和均为726。其他状态行的详情字段保持NULL。

### 24.14 技术点名称全文索引（6.0.1）

Doris Serving层为`ads_technology_profile`的中英文名称建立两个倒排全文索引，不改变表字段、行数据、
逻辑Key或`data_version`：

| 字段 | 索引 | 分词与用途 |
|---|---|---|
| `technology_name_en` | `idx_technology_profile_name_en` | English分词、小写归一、英文名称全文检索 |
| `technology_name_zh` | `idx_technology_profile_name_zh` | 中文细粒度分词、中文名称全文检索 |

英文索引使用`parser=english`；中文索引使用`parser=chinese`和
`parser_mode=fine_grained`。两者均启用`lower_case=true`、`stopwords=none`、
`support_phrase=true`和字典压缩，供Doris `MATCH_ANY`、`MATCH_ALL`及`MATCH_PHRASE`查询使用。
迁移显式执行`BUILD INDEX`，使迁移前已存在的历史行进入索引。

已有环境执行：

```bash
set -a
source .env
set +a
./scripts/compose.sh exec -T -e MYSQL_PWD="$DORIS_PASSWORD" doris-fe \
  mysql --protocol=TCP -h127.0.0.1 -P9030 -uroot \
  < sql/doris/ads_schema_6_0_1_technology_name_search_indexes.sql
```

#### 24.13.2 `ads_technology_disruption_paper_evidence`

逻辑Key：`assessment_id, paper_id`。只保存`DISRUPTIVE_CANDIDATE`和`HIGH_IMPACT_WATCH`的逐篇代表
论文证据；未进入本表不表示论文不存在。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| 身份 | `assessment_id`, `technology_node_id`, `paper_id` | `VARCHAR(64)` | 评估、技术节点与论文ID |
| 展示 | `paper_title_original` | `STRING` | 论文原始标题 |
| 时间 | `publication_year` | `SMALLINT` | 发表年份 |
| 影响 | `cited_by_count`, `fwci` | `BIGINT/DOUBLE` | 累计被引与FWCI |
| 转化 | `is_patent_linked_seed`, `related_patent_count` | `BOOLEAN/BIGINT` | 论文—专利连接事实 |
| 选择 | `representative_rank`, `selection_method` | `BIGINT/VARCHAR` | 节点内排名与选择方法 |
| 角色 | `evidence_role` | `VARCHAR(64)` | 代表、高影响、专利连接或二者兼具 |
| 审计 | `metrics_as_of_date`, `metric_definition_version` | `DATE/VARCHAR` | 统计截止日与口径版本 |
| 审计 | `data_version`, `update_time` | `BIGINT/DATETIME(3)` | 数据版本与生成时间 |

执行入口：

```bash
uv run python -m app.technology_disruption.cli run \
  --config config/technology_disruption_ads_v1_4.json --execute
```

## 25. 动态技术图谱、簇群与演进路径（4.7.0）

4.6.0 的 `ads_technology_profile + ads_technology_graph_edge` 只提供静态节点和聚合关系，不能单独
支撑按年份播放、图簇群着色或代表演进路径。4.7.0 因此新增六张服务表，不修改4.6.0事实语义。

### 25.1 表职责与前端使用方法

| 场景 | 主表 | 使用方法 |
|---|---|---|
| 首屏图节点 | `ads_technology_graph_node` | 直接读取节点名称、主簇群、角色、首次年份和当前推测阶段 |
| 簇群图例/概览 | `ads_technology_community` | 按成员数、内部边数或论文数排序；使用`community_id`着色 |
| 簇群下钻 | `ads_technology_community_member` | 按簇查询成员，按`community_rank`排序，优先展示`CORE/BRIDGE` |
| 年度节点动画 | `ads_technology_evolution_yearly` | 选择年份后更新节点大小、阶段、累计论文和累计专利 |
| 年度关系动画 | `ads_technology_evolution_edge` | `first_evidence_year<=选择年份`时显示；可按证据等级过滤 |
| 代表路径播放 | `ads_technology_evolution_path_step` | 按`path_id, step_order`排序，结合边首次证据年逐步播放 |
| 完整节点详情 | `ads_technology_profile`及论文/专利/机构/案例表 | 从graph node的`technology_node_id`回查4.6.0详细资料 |

推荐首屏不要把587,252条关系全部发送到浏览器。先按簇群、年份、`HIGH/MEDIUM`证据、视口或Top N
节点过滤，再加载局部关系；否则网络毛球既不可读也会造成接口和渲染压力。

### 25.2 `ads_technology_graph_node`

该表是图谱展示节点，不替代完整技术画像。为避免修改已发布4.6.0主表，它将原计划放入profile的
`primary_community_id`正规化为本表的 `community_id`。

| 字段 | 说明 |
|---|---|
| `technology_node_id` | 候选技术节点主键，可连接4.6.0全部详情表 |
| `community_id` | 当前4.7.0主簇群；每个节点恰好一个硬分区 |
| `community_name_original/en/zh` | 簇群显示名；当前名称来自核心节点，中文仍待审核 |
| `community_role` | `CORE/BRIDGE/MEMBER`；单节点簇通常为CORE |
| `community_rank` | 簇内加权度排名 |
| `membership_score` | 簇内边权/全部边权，孤立节点为1；不是分类概率 |
| `external_weight_ratio` | 与其他簇连接权重占比，用于识别桥梁节点 |
| `community_size, is_singleton_community` | 簇规模及单节点簇标识 |
| `first/latest_publication_year` | 当前seed论文观察范围 |
| `current_development_phase` | 最近观察年度的论文时间线推测阶段 |

注意：`community_id` 是算法版本内ID，不能作为跨版本永久业务主键；跨版本比较必须同时带
`metric_definition_version`，并基于成员重叠做映射。

### 25.3 `ads_technology_community` 与成员表

社区算法、边权、seed、分辨率和小簇处理规则以DWS 1.3.0为准。簇群表主要字段：

| 字段 | 说明 |
|---|---|
| `member_count, core_node_count, bridge_node_count` | 全部成员、核心与桥梁节点数 |
| `core_technology_node_id` | 加权度最高的代表节点 |
| `paper_count, patent_count` | 全部成员当前范围内的证据量之和 |
| `first_observed_year, latest_observed_year` | 成员seed论文的总体时间范围 |
| `internal_edge_count, internal_edge_weight` | 簇内候选关系数及置信权重和 |
| `graph_density` | 无向图密度；单节点簇为0 |
| `community_method/seed/resolution` | `LOUVAIN_WEIGHTED_V1/42/1.0` |
| `community_name_translation_status` | 当前为`PENDING` |

为支持列表按学科直接筛选，簇群表同时发布`primary_field_*`和`primary_subfield_*`主分类快照。
该分类先把成员技术的`leading_topic_id`映射到公共学科路径，再按簇内`membership_score`之和、成员数和
`subfield_id`依次确定稳定第一名；Field必须是所选Subfield的父级。它是图簇的主要学科标签，不是唯一
学科归属。`discipline_member_share`披露主Subfield在已分类成员中的占比，`discipline_coverage_rate`
披露成功映射成员占全部成员的比例；前者低于0.70时`is_cross_disciplinary=true`。缺少主Topic的成员
保留在覆盖率分母中，不强行归类。中英文名称是发布快照，公共学科维表仍是名称与层级权威入口。

当前1,731个簇群包含1,708个单节点簇。这表示这些节点在HIGH/MEDIUM证据子图中没有可用于可靠聚类的
邻边，不表示它们在现实中不存在相关技术。前端应提供“未形成可靠簇群”图例，不应把所有单节点簇
合并为一个“其他”簇，否则会伪造成员之间的联系。

### 25.4 `ads_technology_evolution_yearly`

主要字段包括当年/上一观察年度论文数与份额、论文增长率、累计论文/专利、作者、机构、企业数、首次/
最近发表年、距起源年数、阶段和里程碑标识。阶段完整枚举为：

```text
ORIGIN
EMERGENCE
ACCELERATION
EXPANSION
CONSOLIDATION
NO_PUBLICATION_OBSERVED
```

`inference_method='PUBLICATION_TIMELINE_INFERENCE'` 必须随结果展示或进入说明弹窗。年份不是连续日历时，
`previous_*` 是上一观察年度而不是上一自然年；时间序列图应显示真实年份间距，不得把记录等距绘制。

### 25.5 `ads_technology_evolution_edge`

| 字段 | 说明 |
|---|---|
| `first_evidence_year, last_evidence_year` | 当前固定论文引用/共同专利数据的首次和最近证据年 |
| `source/target_first_publication_year` | 两端技术节点首次seed论文年 |
| `node_origin_lag_years` | 目标节点起源年减来源节点起源年 |
| `temporal_alignment_status` | `TIME_ALIGNED/TIME_CONFLICT/UNKNOWN` |
| `is_path_eligible` | 是否通过关系类型、证据等级、时间一致率和起源顺序门槛 |
| `temporal_method` | `PUBLICATION_AND_PATENT_FIRST_EVIDENCE` |

年份选择器的推荐条件是：节点使用 `first_publication_year<=:year`，关系使用
`first_evidence_year<=:year`。`last_evidence_year` 是最近观测年份，不是关系终止年份，因此不能用
`last_evidence_year<:year` 隐藏关系。

### 25.6 `ads_technology_evolution_path_step`

一条路径按 `step_order` 从较早节点走向目标节点。`previous_technology_node_id` 为空的是路径根节点；
其余步骤携带进入当前节点的 `edge_first_evidence_year` 和 `edge_confidence_score`。

| 字段 | 说明 |
|---|---|
| `path_id` | 以发布版本和目标节点生成的确定性ID |
| `target_technology_node_id` | 本条代表路径最终解释的目标节点 |
| `path_length` | 路径包含的节点数 |
| `path_score` | 路径中最低边置信分，不是概率 |
| `is_truncated` | 是否因8步上限截断更早前驱 |
| `path_method` | `BEST_TEMPORALLY_ALIGNED_PREDECESSOR_V1` |

该表只保存每个目标的单条代表路径。用户要查看全部上游分支时，应查询
`ads_technology_evolution_edge`，不能用代表路径证明唯一传承或因果关系。

### 25.7 查询示例与注意事项

```sql
-- 指定簇群的核心节点
SELECT *
FROM ads_technology_graph_node
WHERE community_id = :community_id
ORDER BY community_rank
LIMIT 100;

-- 播放到某一年时可见的高/中证据关系
SELECT *
FROM ads_technology_evolution_edge
WHERE first_evidence_year <= :year
  AND evidence_level IN ('HIGH', 'MEDIUM');

-- 播放某一目标技术的代表路径
SELECT *
FROM ads_technology_evolution_path_step
WHERE target_technology_node_id = :technology_node_id
ORDER BY step_order;
```

必须注意：论文年份是知识活动的代理，不是技术发明日；引用关系是知识依赖证据，不是商业供应链；
Louvain簇群是本次图快照的结构结果，不是人工技术目录；核心节点表示图连接中心性，不表示技术价值
最高；代表路径用于导航，不构成科学史或产业因果结论。

### 25.8 发布与验证

```bash
./scripts/build_technology_graph_dws.sh
./scripts/publish_technology_graph_ads_v2.sh
```

6.13.0 ADS先物化到 `iceberg.technology_graph_ads_v2_20261029`，再幂等加载到Doris；历史
`technology_graph_ads_v1_20261016`保持不变。六张表当前行数依次为
19,430、1,731、19,430、164,354、587,252和47,909；Iceberg与Doris逐表一致，逻辑键重复与时间/
分值异常均为0。全部1,731个社区已获得主Subfield，16个标记为跨学科；唯一缺少主Topic的技术位于
4,151成员社区，故最低分类覆盖率为0.999759，名称空值、比例异常和Subfield—Field父级不一致均为0。
v2报告位于 `reports/technology_graph_ads_v2_20261029/`。

### 25.9 完整字段字典

以下字段定义与 Doris 4.7.0 DDL 保持一致。已有小节重点解释业务语义，本节补齐全部物理字段和类型。
已有环境执行 `sql/doris/ads_schema_4_7_0_technology_graph_comments.sql` 回填元数据注释；该操作不重算
图算法、不改写业务行，也不改变 4.7.0 的 Key 和字段类型。既有表的 Key、HASH distribution 和
`data_version` 同样受 Doris 限制，不能通过 `MODIFY COLUMN` 原位补注释。

#### 25.9.1 `ads_technology_graph_node`

技术图谱首屏节点；包含主簇群和当前演进摘要。逻辑 Key：`technology_node_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 身份与关联 | `research_cluster_id` | `VARCHAR(64)` | 来源ETO研究簇ID |
| 展示与说明 | `technology_name_original` | `STRING` | 技术原始名称 |
| 展示与说明 | `technology_name_en` | `STRING` | 技术英文名称 |
| 展示与说明 | `technology_name_zh` | `STRING` | 审核中文技术名称；当前可为空 |
| 身份与关联 | `community_id` | `VARCHAR(64)` | 算法版本内的主簇群ID |
| 展示与说明 | `community_name_original` | `STRING` | 簇群原始显示名；来自核心节点 |
| 展示与说明 | `community_name_en` | `STRING` | 簇群英文显示名 |
| 展示与说明 | `community_name_zh` | `STRING` | 审核中文簇群名；当前可为空 |
| 状态与口径 | `community_role` | `VARCHAR(32)` | 节点簇内角色：CORE、BRIDGE或MEMBER |
| 指标 | `community_rank` | `BIGINT` | 节点按加权度的簇内稳定排名 |
| 指标 | `membership_score` | `DECIMAL(9,6)` | 簇内边权占全部边权比例；孤立节点为1 |
| 指标 | `weighted_degree` | `DOUBLE` | 节点全部入选关系的置信权重和 |
| 指标 | `external_weight_ratio` | `DECIMAL(9,6)` | 跨簇边权占全部边权比例 |
| 指标 | `community_size` | `BIGINT` | 主簇群成员数 |
| 状态与口径 | `is_singleton_community` | `BOOLEAN` | 是否属于单节点簇 |
| 时间 | `first_publication_year` | `SMALLINT` | 节点seed论文首次发表年份 |
| 时间 | `latest_publication_year` | `SMALLINT` | 节点seed论文最近发表年份 |
| 指标 | `current_development_phase` | `VARCHAR(64)` | 最近观察年度的论文时间线推测阶段 |
| 状态与口径 | `chain_role` | `VARCHAR(64)` | 技术链位置角色 |
| 指标 | `upstream_dependency_count` | `BIGINT` | 上游依赖候选节点数 |
| 指标 | `downstream_cluster_count` | `BIGINT` | 下游候选节点数 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 25.9.2 `ads_technology_community`

固定算法版本内的技术图簇群汇总。逻辑 Key：`community_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `community_id` | `VARCHAR(64) NOT NULL` | 算法版本内的主簇群ID |
| 展示与说明 | `community_name_original` | `STRING` | 簇群原始显示名；来自核心节点 |
| 展示与说明 | `community_name_en` | `STRING` | 簇群英文显示名 |
| 展示与说明 | `community_name_zh` | `STRING` | 审核中文簇群名；当前可为空 |
| 状态与口径 | `naming_method` | `VARCHAR(64)` | 簇群名称选择方法 |
| 指标 | `member_count` | `BIGINT` | 簇群全部成员数 |
| 指标 | `core_node_count` | `BIGINT` | CORE角色节点数 |
| 指标 | `bridge_node_count` | `BIGINT` | BRIDGE角色节点数 |
| 身份与关联 | `core_technology_node_id` | `VARCHAR(64)` | 簇内加权度最高的代表节点ID |
| 主学科快照 | `primary_field_id` | `VARCHAR(64)` | 主Field平台ID；由成员主Topic确定性聚合 |
| 主学科快照 | `primary_field_name_zh` | `STRING` | 主Field中文名称发布快照 |
| 主学科快照 | `primary_field_name_en` | `STRING` | 主Field英文名称发布快照 |
| 主学科快照 | `primary_subfield_id` | `VARCHAR(64)` | 主Subfield平台ID；由成员主Topic确定性聚合 |
| 主学科快照 | `primary_subfield_name_zh` | `STRING` | 主Subfield中文名称发布快照 |
| 主学科快照 | `primary_subfield_name_en` | `STRING` | 主Subfield英文名称发布快照 |
| 主学科指标 | `discipline_member_count` | `BIGINT` | 支持主Subfield的已分类成员数 |
| 主学科指标 | `primary_subfield_weighted_score` | `DOUBLE` | 主Subfield成员`membership_score`之和 |
| 主学科指标 | `discipline_member_share` | `DECIMAL(9,6)` | 支持主Subfield成员占已分类成员比例 |
| 主学科指标 | `discipline_coverage_rate` | `DECIMAL(9,6)` | 可映射成员占全部成员比例 |
| 状态与口径 | `discipline_assignment_method` | `VARCHAR(64)` | 当前为`LEADING_TOPIC_MEMBERSHIP_WEIGHT_V1` |
| 主学科指标 | `secondary_subfield_count` | `BIGINT` | 除主Subfield外的其他已观察Subfield数 |
| 状态与口径 | `is_cross_disciplinary` | `BOOLEAN` | 主Subfield成员占比低于0.70时为真；未分类为NULL |
| 指标 | `paper_count` | `BIGINT` | 簇群成员论文数之和 |
| 指标 | `patent_count` | `BIGINT` | 簇群成员关联专利数之和 |
| 时间 | `first_observed_year` | `SMALLINT` | 成员seed论文最早观察年份 |
| 时间 | `latest_observed_year` | `SMALLINT` | 成员seed论文最近观察年份 |
| 指标 | `internal_edge_count` | `BIGINT` | 簇内入选候选关系数 |
| 指标 | `internal_edge_weight` | `DOUBLE` | 簇内关系置信权重和 |
| 指标 | `graph_density` | `DECIMAL(9,6)` | 簇内无向图密度；单节点簇为0 |
| 状态与口径 | `community_method` | `VARCHAR(64)` | 簇群算法；当前为加权Louvain |
| 指标 | `community_seed` | `INT` | 簇群算法固定随机种子 |
| 指标 | `community_resolution` | `DOUBLE` | Louvain分辨率参数 |
| 展示与说明 | `community_name_translation_status` | `VARCHAR(32)` | 簇群名称翻译审核状态 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 25.9.3 `ads_technology_community_member`

技术节点在主簇群中的成员关系和结构指标。逻辑 Key：`community_id, technology_node_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `community_id` | `VARCHAR(64) NOT NULL` | 算法版本内的主簇群ID |
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 指标 | `membership_score` | `DOUBLE` | 簇内边权占全部边权比例；孤立节点为1 |
| 指标 | `weighted_degree` | `DOUBLE` | 节点全部入选关系的置信权重和 |
| 指标 | `internal_weight` | `DOUBLE` | 节点连接同簇节点的边权和 |
| 指标 | `external_weight` | `DOUBLE` | 节点连接其他簇节点的边权和 |
| 指标 | `external_weight_ratio` | `DECIMAL(9,6)` | 跨簇边权占全部边权比例 |
| 指标 | `community_rank` | `BIGINT` | 节点按加权度的簇内稳定排名 |
| 状态与口径 | `community_role` | `VARCHAR(32)` | 节点簇内角色：CORE、BRIDGE或MEMBER |
| 状态与口径 | `is_primary_community` | `BOOLEAN` | 是否为节点的主簇群；当前恒为真 |
| 指标 | `community_size` | `BIGINT` | 主簇群成员数 |
| 状态与口径 | `community_method` | `VARCHAR(64)` | 簇群算法；当前为加权Louvain |
| 指标 | `community_seed` | `INT` | 簇群算法固定随机种子 |
| 指标 | `community_resolution` | `DOUBLE` | Louvain分辨率参数 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 25.9.4 `ads_technology_evolution_yearly`

技术节点按真实观察年份的论文时间线演进指标。逻辑 Key：`technology_node_id, statistics_year`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `technology_node_id` | `VARCHAR(64) NOT NULL` | 确定性候选技术节点ID |
| 时间 | `statistics_year` | `SMALLINT NOT NULL` | 真实论文观察年份 |
| 指标 | `paper_count` | `BIGINT` | 该观察年度论文数 |
| 指标 | `paper_share` | `DECIMAL(18,12)` | 节点论文数占同年观察论文数比例 |
| 指标 | `previous_paper_count` | `BIGINT` | 上一观察年度论文数；不保证是上一自然年 |
| 指标 | `previous_paper_share` | `DECIMAL(18,12)` | 上一观察年度论文份额 |
| 指标 | `paper_growth_rate` | `DECIMAL(18,8)` | 相对上一观察年度的论文增长率 |
| 指标 | `cumulative_paper_count` | `BIGINT` | 截至该观察年的累计论文数 |
| 指标 | `patent_count` | `BIGINT` | 该观察年度首次关联专利数 |
| 指标 | `cumulative_patent_count` | `BIGINT` | 截至该观察年的累计关联专利数 |
| 指标 | `author_count` | `BIGINT` | 当年去重作者数 |
| 指标 | `new_author_count` | `BIGINT` | 当年首次进入节点的作者数 |
| 指标 | `institution_count` | `BIGINT` | 当年去重机构数 |
| 指标 | `new_institution_count` | `BIGINT` | 当年首次进入节点的机构数 |
| 指标 | `company_count` | `BIGINT` | 当年关联company类型机构数 |
| 时间 | `first_publication_year` | `SMALLINT` | 节点seed论文首次发表年份 |
| 时间 | `latest_publication_year` | `SMALLINT` | 节点seed论文最近发表年份 |
| 时间 | `years_since_origin` | `INT` | 统计年减首次论文年 |
| 指标 | `development_phase` | `VARCHAR(64)` | 论文时间线推测阶段 |
| 状态与口径 | `is_origin_year` | `BOOLEAN` | 是否为节点首次论文年份 |
| 状态与口径 | `is_peak_publication_year` | `BOOLEAN` | 是否为当前观察窗论文数峰值年 |
| 状态与口径 | `inference_method` | `VARCHAR(64)` | 阶段推断方法；当前为论文时间线推断 |
| 状态与口径 | `coverage_status` | `VARCHAR(32)` | 年度事实覆盖状态 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 25.9.5 `ads_technology_evolution_edge`

带首次和最近证据年份的候选技术关系。逻辑 Key：`evolution_edge_id`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `evolution_edge_id` | `VARCHAR(64) NOT NULL` | 带时间技术关系确定性ID |
| 身份与关联 | `source_technology_node_id` | `VARCHAR(64)` | 关系起点候选技术节点ID |
| 身份与关联 | `target_technology_node_id` | `VARCHAR(64)` | 关系终点候选技术节点ID |
| 指标 | `relation_type` | `VARCHAR(32)` | 关系类型 |
| 状态与口径 | `direction_status` | `VARCHAR(32)` | 关系方向判定状态 |
| 指标 | `evidence_level` | `VARCHAR(16)` | HIGH、MEDIUM或LOW证据等级 |
| 指标 | `relation_confidence_score` | `DECIMAL(9,6)` | 同关系类型内可比较的启发式置信分 |
| 指标 | `total_citation_count` | `BIGINT` | 两簇间论文引用总次数 |
| 指标 | `dominant_temporal_consistency` | `DECIMAL(9,6)` | 主导引用方向的时间一致率 |
| 指标 | `shared_topic_count` | `BIGINT` | 两端共同Topic数 |
| 指标 | `topic_jaccard` | `DECIMAL(9,6)` | 两端Topic集合Jaccard系数 |
| 指标 | `shared_patent_count` | `BIGINT` | 两端共同关联专利数 |
| 指标 | `shared_patent_family_count` | `BIGINT` | 两端共同关联专利族数 |
| 时间 | `first_evidence_year` | `SMALLINT` | 当前固定证据中的首次观察年份 |
| 时间 | `last_evidence_year` | `SMALLINT` | 当前固定证据中的最近观察年份；不是终止年 |
| 时间 | `source_first_publication_year` | `SMALLINT` | 起点节点seed论文首次发表年份 |
| 时间 | `target_first_publication_year` | `SMALLINT` | 终点节点seed论文首次发表年份 |
| 时间 | `node_origin_lag_years` | `INT` | 终点首次论文年减起点首次论文年 |
| 状态与口径 | `temporal_alignment_status` | `VARCHAR(32)` | 两端起源与关系方向的时间对齐状态 |
| 状态与口径 | `is_path_eligible` | `BOOLEAN` | 是否满足代表路径候选门槛 |
| 状态与口径 | `temporal_method` | `VARCHAR(64)` | 关系证据年份计算方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

#### 25.9.6 `ads_technology_evolution_path_step`

每个目标技术的一条确定性代表演进路径步骤。逻辑 Key：`path_id, step_order`。

| 字段组 | 字段 | Doris 类型 | 说明 |
|---|---|---|---|
| 身份与关联 | `path_id` | `VARCHAR(64) NOT NULL` | 发布版本与目标节点生成的确定性路径ID |
| 指标 | `step_order` | `INT NOT NULL` | 路径内从根节点开始的步骤序号 |
| 身份与关联 | `target_technology_node_id` | `VARCHAR(64)` | 本条代表路径最终解释的目标节点ID |
| 身份与关联 | `technology_node_id` | `VARCHAR(64)` | 确定性候选技术节点ID |
| 身份与关联 | `previous_technology_node_id` | `VARCHAR(64)` | 前一步技术节点ID；根节点为空 |
| 时间 | `edge_first_evidence_year` | `SMALLINT` | 前一步进入当前节点关系的首次证据年 |
| 指标 | `edge_confidence_score` | `DECIMAL(9,6)` | 前一步进入当前节点关系的置信分 |
| 指标 | `path_length` | `INT` | 代表路径包含的节点数 |
| 指标 | `path_score` | `DECIMAL(9,6)` | 路径中最低边置信分；不是概率 |
| 状态与口径 | `is_truncated` | `BOOLEAN` | 是否因最大8步限制截断更早前驱 |
| 状态与口径 | `path_method` | `VARCHAR(64)` | 确定性代表路径选择方法 |
| 版本与审计 | `metrics_as_of_date` | `DATE` | 指标统计截止日 |
| 版本与审计 | `metric_definition_version` | `VARCHAR(64)` | 图算法与演进口径版本 |
| 版本与审计 | `data_version` | `BIGINT NOT NULL` | 同一业务Key的单调数据版本 |
| 版本与审计 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

## 26. 基础研究问题 ADS（5.2.0）

基础研究问题 ADS 面向下游科研发掘平台，不改变 DWD 审核事实。发布使用固定
`research_problem_dwd_v1_20261019` Snapshot；大模型仅生成说明性增强字段，审核状态恒为
`PENDING_REVIEW`。完整字段由 Iceberg Stage 的物理 Schema 固化，Doris 迁移从该 Schema 生成并保存为
`sql/doris/ads_schema_5_4_0_research_problem.generated.sql`。每张表均包含
`metrics_as_of_date`、`metric_definition_version`、`data_version` 和 `update_time`。

| 表 | 逻辑 Key | 核心字段与用途 |
|---|---|---|
| `ads_research_problem_release` | `release_id` | DWD/ADS发布ID、模型、审核策略、依赖Snapshot和发布时间 |
| `ads_research_problem_overview_snapshot` | `snapshot_date` | 总数、新增、活跃学科、热门词和增长概览 |
| `ads_research_problem_profile` | `problem_id` | 题名、陈述、缺口、背景、现状、等级、提出时间、来源机构、学科、关键词、未来方向、实体计数与热度 |
| `ads_research_problem_discipline` | `problem_id, topic_id` | Topic/Field/Domain、证据数、排名和Leading Topic标记 |
| `ads_research_problem_discipline_metrics` | `topic_id` | 学科问题规模、证据数和热度 |
| `ads_research_problem_discipline_yearly` | `topic_id, statistics_year` | 学科年度趋势 |
| `ads_research_problem_semantic_relation` | `semantic_relation_id` | 主语、关系词、宾语、关系类型、证据、模型置信度和审核状态 |
| `ads_research_problem_keyword` | `problem_keyword_id` | 问题级规范关键词、类型、核心标记和证据 |
| `ads_research_problem_keyword_metrics` | `keyword_key` | 关键词当前统计和问题集合 |
| `ads_research_problem_keyword_yearly` | `keyword_key, statistics_year` | 关键词年度趋势 |
| `ads_research_problem_research_path` | `research_path_id` | 技术路线、未来方向、开放子问题、方法、前提和不确定性 |
| `ads_research_problem_yearly_metrics` | `problem_id, statistics_year` | 论文、专利、人才、机构、被引和累计年度指标 |
| `ads_research_problem_hotspot_snapshot` | `problem_id, model_version` | 五维热点得分、总分、排名、状态与增长率 |
| `ads_research_problem_paper` | `problem_id, paper_id` | 问题—平台论文关联，区分DIRECT/PROXY |
| `ads_research_problem_patent` | `problem_id, patent_id` | 问题—平台专利关联，区分DIRECT/PROXY |
| `ads_research_problem_project` | `problem_id, project_id` | 问题—平台项目关联，区分DIRECT/PROXY |
| `ads_research_problem_talent` | `problem_id, talent_id` | 问题—平台人才关联，区分DIRECT/PROXY |
| `ads_research_problem_institution` | `problem_id, institution_id` | 问题—平台机构关联及分类证据计数 |
| `ads_research_problem_graph_edge` | `edge_id` | 问题间方向、跨簇引用、共享Topic和共享专利证据 |
| `ads_research_problem_event` | `event_id` | 直接论文、专利和项目时间轴事件 |
| `ads_research_problem_provenance` | `provenance_id` | 分域来源表、来源行数、namespace与发布ID |
| `ads_research_problem_change_log` | `change_id` | IDENTIFIED、APPROVED和AI_ENRICHED记录 |

`ads_research_problem_profile`的Doris建表DDL必须为全部字段保留`COMMENT`，表注释固定说明其为基础研究
问题画像。`future_directions`仅是`path_type='FUTURE_DIRECTION'`研究路径标题的有序快照，完整方向标题、
说明、目标、方法、前提、证据、周期、不确定性、审核状态与模型血缘分别读取
`ads_research_problem_research_path`和正式发布表`ads_research_problem_direction`，不得把画像数组解释为
完整方向事实。

关键口径：

- `proposed_date/year` 来自最早 `DIRECT` 支持论文；来源机构是该论文全部可映射平台机构。
- `problem_level`：A 为至少两篇直接论文且具有直接专利或项目证据；B 为至少一篇直接论文；其余 C。
- 趋势使用研究簇代理指标，`metric_scope` 明确标为 `CLUSTER_PROXY`、
  `CLUSTER_TOPIC_PROXY` 或 `LLM_KEYWORD_CLUSTER_PROXY`。
- 热点状态为 `INSUFFICIENT_EVIDENCE`、`EMERGING`、`EARLY_EMERGING`、`WATCH`、
  `ESTABLISHED_GROWING`、`MATURE`。
- `identified_at`、`reviewed_at` 与 `proposed_date` 分别表示模型识别、人工审核和最早论文证据时间。
- `topic_name_zh` 读取固定 Snapshot 的
  `technology_v2.dwd_classification_localized_text`，仅接受 OpenAlex Topic、`zh-Hans`、`title`、
  `approved` 的最新修订；`topic_name_en` 优先读取 Topic 英文名，缺失时回退 OpenAlex 原始名称。

## 27. 基础研究问题竞争、潜力与推荐 ADS（5.3.0）

5.3.0 在5.2.0的22张问题表上新增16张表，并向问题项目、画像、年度、热点和总览表增加可由当前
事实计算的项目资金、活跃度与分项指标。所有不可计算值使用 NULL 或零行空表，必须同时给出
`coverage_status`、`unavailable_reason` 或对应状态字段，不使用年度数据伪造月度事实。

### 27.1 现有表扩展

| 表 | 新增字段组 | 口径 |
|---|---|---|
| `ads_research_problem_project` | `funding_amount_original`、`funding_currency`、`funding_amount_status` | 直接复用关联项目金额和币种；缺失保持NULL |
| `ads_research_problem_profile` | `funded_project_count`、原币种金额、币种、`funding_amount_cny`、`funding_coverage_rate` | 只有全部已知金额属于同一币种才汇总原币种金额；CNY换算当前为空 |
| `ads_research_problem_yearly_metrics` | 项目数、有金额项目数、原币种金额、币种、CNY金额、资金覆盖率 | 按项目有效开始年统计；项目年份没有论文时仍保留一行 |
| `ads_research_problem_hotspot_snapshot` | 项目数、资金覆盖率、项目活跃分、资金分及状态 | 项目活跃分进入热点；未进行币种标准化时资金分为空且不进入总分 |
| `ads_research_problem_overview_snapshot` | 活跃问题数、近3月上升/下降数、近3月平均增长率、月度覆盖状态 | 活跃数从年度发展阶段计算；近3月字段为空 |

### 27.2 时间、热度与生命周期

| 表 | 逻辑 Key | 核心字段 |
|---|---|---|
| `ads_research_problem_monthly_metrics` | `problem_id, statistics_month` | 直接论文、专利、可用项目日期、首次人才/机构、月度活动分、平滑热度和增长率；引用增量与月度资金仍为空 |
| `ads_research_problem_development_snapshot` | `problem_id, model_version` | 首次/最近活跃年、观察活跃年数、最长连续活跃年、峰值年、衰减起点、最近增长率、发展阶段 |
| `ads_research_problem_heat_component` | `problem_id, model_version, component_code` | 论文增长、学术影响、人才扩散、机构扩散、专利、项目及资金分项、权重与贡献 |

`ads_research_problem_development_snapshot`的既有生命周期字段仍按`YEARLY_OBSERVATION`发布；5.16.0不在
该年度快照中回填`continuous_active_months/continuous_decline_months`。需要真实月度活跃、衰减或增长
时应直接查询`ads_research_problem_monthly_metrics`，不得继续使用LLM估算字段冒充事实。

### 27.3 国际、国内和深圳竞争格局

| 表 | 逻辑 Key | 核心字段 |
|---|---|---|
| `ads_research_problem_region_yearly_metrics` | `problem_id, location_level, location_id, statistics_year` | COUNTRY/PROVINCE/CITY/DISTRICT年度论文、专利、项目、机构、企业和份额 |
| `ads_research_problem_region_snapshot` | `problem_id, location_level, location_id, model_version` | 研究热度、前沿引领、投资、协作广度、综合竞争分及排名 |
| `ads_research_problem_region_institution` | `problem_id, location_id, institution_id` | 各地区主要机构的论文、专利、项目、首次/最近证据年及排名 |
| `ads_research_problem_competition_rank` | `problem_id, competition_scope, subject_id, ranking_dimension` | 按研究热度、前沿引领、投资、主体总量和综合竞争分别排名 |

区级位置读取固定 `location_v1_4_20261019`：深圳124家具有论文证据的科研机构已由高德数据解析到
行政区。区级历史指标采用机构当前已确认区级位置回投历史年度，并以
`location_coverage_status=SHENZHEN_AMAP_CURATED` 披露，不解释为机构历史地址。

当前区域前沿引领分是专利与项目信号的启发式代理，投资分因跨币种不可比而为空。国际合作论文会在
每个参与机构所在地区分别计数；`paper_share` 是同一问题、层级、年份内的地区份额，不是全球论文唯一
分数计数。

### 27.4 资金、政策、潜力与预测

| 表 | 逻辑 Key | 核心字段 |
|---|---|---|
| `ads_research_problem_funding_evidence` | `problem_id, project_id` | 项目原金额、币种、资助者、年份、金额状态、换算状态和分配方法 |
| `ads_research_problem_policy_evidence` | `problem_id, policy_id` | 政策标题、层级、发布机构、地区、日期、支持方式和匹配证据；当前零行 |
| `ads_research_problem_potential_dimension` | `assessment_id, dimension_code` | 学术影响、技术转化、政策导向、资金投入、协作广度五维得分、权重和覆盖状态 |
| `ads_research_problem_potential_assessment` | `assessment_id` | 可用维度归一后的潜力分、等级、覆盖率、模型版本和预测状态 |
| `ads_research_problem_potential_evidence` | `assessment_id, dimension_code, evidence_id` | 每个非空维度的来源表、评分方法和值 |
| `ads_research_problem_forecast_yearly` | `problem_id, forecast_model_version, forecast_year, target_metric` | 预测值、上下界、训练截止日、回测误差；当前零行 |

潜力评估当前是 `HEURISTIC_BASELINE_NOT_MACHINE_LEARNING_FORECAST`，不是机器学习预测。政策维度为空；
资金维度暂以有金额项目/项目活跃信号代理，不使用不同币种金额直接比较。未来三年预测表在模型训练与
回测完成前保持空表。

### 27.5 相似问题与推荐

| 表 | 逻辑 Key | 核心字段 |
|---|---|---|
| `ads_research_problem_similarity` | `problem_id, similar_problem_id, model_version` | Topic、共享专利、图关系置信度、综合相似度和排名；语义向量分当前为空 |
| `ads_research_problem_recommendation` | `recommendation_id` | 相似问题或潜在方向、推荐分、排名、原因、主要机构和证据ID |
| `ads_research_problem_recommendation_evidence` | `recommendation_id, evidence_id` | 推荐对应的图边或待复核研究路径证据 |

相似问题当前使用 `DWS_GRAPH_FEATURE_BASELINE`，不得展示为“嵌入语义相似度”。未来方向来自GLM且
保持 `LLM_PENDING_REVIEW`，不能作为已验证研究结论。

### 27.6 实际发布与覆盖边界

2026-10-20已将本节38张表的数据修订发布到Iceberg `research_problem_ads_v1_20261020`及Doris
`gkx_technology_analysis_dev`，逐表行数一致，逻辑Key重复数和关联校验均为0。问题画像覆盖406/406。
学科关联3,584行及学科汇总1,493行的Topic中英文名称均已完整填入，缺失数为0；旧Iceberg发布
`research_problem_ads_v1_20261019`保留不变。
论文平台ID缺失时，`paper_id`使用`openalex:`来源ID回退，并由`paper_id_mapping_status`区分
`PLATFORM_ID`与`SOURCE_ID_FALLBACK`，不得将来源ID回退误认为已完成平台identity映射。

月度、政策、预测、汇率归一、区域投资得分、热点资金得分和语义向量相似度仍未实现；具体行数、覆盖率
及补数依赖见`reports/research_problem_ads_v1_20261020/topic_localization_verification.md`。

## 28. 基础研究问题部署与战略建议 ADS（5.4.0）

本节新增5张表，把既有科研证据与后续人工/算法部署决策分开保存。已有论文、专利、项目或机构关联
只能作为候选证据，不自动产生“推荐”“牵头”“高优先级”等决策结论。待补录值保持NULL并通过状态字段
披露，不使用热点分或潜力分静默替代战略优先级。

### 28.1 `ads_research_problem_deployment`

逻辑Key：`problem_id, deployment_version`。当前为406个问题各建立一条`deployment_v1`骨架。

| 字段组 | 字段 | 类型 | 当前口径 |
|---|---|---|---|
| Key | `problem_id` | `VARCHAR(256) NOT NULL` | 基础问题ID |
| Key | `deployment_version` | `VARCHAR(256) NOT NULL` | 部署清单版本 |
| 展示 | `problem_title_zh/problem_title_en` | `STRING` | 问题中英文标题快照 |
| 分类 | `domain_ids/field_ids/topic_ids` | `ARRAY<STRING>` | 学科分类ID快照 |
| 方向 | `approved_direction_ids` | `ARRAY<STRING>` | 已审核正式方向ID；当前空数组 |
| 机构 | `recommended_institution_ids` | `ARRAY<STRING>` | 已审核推荐机构ID；当前空数组 |
| 机构 | `lead_institution_id` | `STRING` | 建议牵头机构；当前NULL |
| 优先级 | `priority_level` | `STRING` | 正式优先级枚举；当前NULL |
| 优先级 | `priority_score` | `DECIMAL(9,6)` | 战略优先级分；当前NULL |
| 优先级 | `priority_dimension/priority_reason` | `STRING` | 优先级视角及理由；当前NULL |
| 部署 | `deployment_status` | `STRING` | 拟部署、已部署、持续支持、暂停等；当前NULL |
| 部署 | `recommended_investment_level` | `STRING` | 建议投入等级；当前NULL |
| 有效期 | `valid_from/valid_to` | `DATE` | 部署建议有效期 |
| 治理 | `owner_department` | `STRING` | 责任部门 |
| 审核 | `reviewer/reviewed_at/review_status` | `STRING/DATETIME/STRING` | 审核信息；当前`PENDING_SUPPLEMENT` |
| 状态 | `supplement_status` | `STRING` | 当前固定`PENDING_DEPLOYMENT_DATA` |
| 参考 | `hotspot_score/potential_score` | `DECIMAL(9,6)` | 现有热点与潜力参考分，不等同优先级 |
| 参考 | `potential_level` | `STRING` | 现有潜力等级 |
| 追踪 | `source_problem_update_time` | `DATETIME(3)` | 来源问题画像更新时间 |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

### 28.2 `ads_research_problem_direction`

逻辑Key：`direction_id`。当前1,556行来自现有研究路径，并已按操作方批量批准策略发布为正式方向；
原模型审核状态和理由继续保留在`review_reason_zh`中用于审计。

| 字段组 | 字段 | 类型 | 当前口径 |
|---|---|---|---|
| Key | `direction_id` | `VARCHAR(256) NOT NULL` | 稳定方向ID |
| 关联 | `problem_id` | `STRING` | 基础问题ID |
| 版本 | `direction_version` | `STRING` | 当前`direction_v2` |
| 类型 | `direction_type` | `STRING` | 技术路线、未来方向或开放子问题 |
| 内容 | `title_zh/title_en/description_zh/objective_zh` | `STRING` | 方向标题、说明和目标 |
| 方法 | `methods_zh/prerequisites_zh/keyword_terms_zh` | `ARRAY<STRING>` | 方法、前提和关键词 |
| 证据 | `evidence_paper_ids` | `ARRAY<STRING>` | 模型引用的论文证据ID |
| 判断 | `horizon/uncertainty_zh/confidence/direction_rank` | `STRING/STRING/DOUBLE/INT` | 周期、不确定性、置信度与候选排序 |
| 来源 | `source_type/source_id/source_model/source_prompt_version` | `STRING` | 候选来源及模型版本 |
| 审核 | `is_official` | `BOOLEAN` | 当前全部为true |
| 审核 | `review_status/reviewer/reviewed_at` | `STRING/STRING/DATETIME` | 当前为操作方批量批准的正式方向审核信息 |
| 有效期 | `effective_from/effective_to` | `DATE` | 正式方向有效期；当前结束日为空 |
| 状态 | `supplement_status` | `STRING` | 当前`COMPLETE_AI_AUTO_REVIEW` |
| 来源时间 | `source_generated_at` | `DATETIME(3)` | 候选生成时间 |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

### 28.3 `ads_research_problem_institution_match`

逻辑Key：`problem_id, institution_id, model_version`。当前包含问题级深圳证据候选及无直接问题证据时的
深圳全局回退候选。每个问题按成果贡献规则确定且仅确定一家主导单位。

| 字段组 | 字段 | 类型 | 当前口径 |
|---|---|---|---|
| Key | `problem_id/institution_id/model_version` | `VARCHAR(256)` | 问题、机构与匹配版本联合Key |
| 机构 | `institution_name/institution_type_id` | `STRING` | 名称及固定机构画像Snapshot中的稳定类型代码 |
| 地区 | `district_location_id/is_shenzhen` | `STRING/BOOLEAN` | 深圳区级位置及深圳标记 |
| 证据 | `paper_count/patent_count/project_count` | `BIGINT` | 已有问题—机构科研证据计数 |
| 证据 | `talent_count` | `BIGINT` | 问题证据论文中署名该机构的去重人才数；已计算，未命中为0 |
| 证据 | `direct_talent_count/proxy_talent_count` | `BIGINT` | 按问题人才`DIRECT/PROXY`证据等级拆分的去重人才数 |
| 证据 | `talent_evidence_type` | `STRING` | 固定为`PROBLEM_EVIDENCE_WORK_AUTHOR_AFFILIATION` |
| 能力 | `academic_capability_score` | `DECIMAL(9,6)` | DeepSeek学术能力匹配分 |
| 能力 | `talent_capability_score` | `DECIMAL(9,6)` | DeepSeek人才能力匹配分 |
| 能力 | `technology_transfer_score` | `DECIMAL(9,6)` | DeepSeek技术转化能力分 |
| 能力 | `collaboration_score/infrastructure_score` | `DECIMAL(9,6)` | DeepSeek协作与基础设施分 |
| 匹配 | `overall_match_score/match_level/match_rank` | `DECIMAL/STRING/BIGINT` | 模型综合匹配结果及排名 |
| 建议 | `recommended_role/recommendation_reason` | `STRING` | 每问题恰好一家`LEAD`；理由记录贡献计数、排名和原模型理由 |
| 证据 | `evidence_ids` | `ARRAY<STRING>` | 后续匹配证据ID |
| 状态 | `candidate_source` | `STRING` | 成果直接证据、人才署名直接证据或明确标记的全局回退候选 |
| 状态 | `match_status` | `STRING` | `FORMAL_RECOMMENDATION_CONTRIBUTION_LEAD` |
| 审核 | `review_status/reviewer/reviewed_at` | `STRING/STRING/DATETIME` | 贡献规则正式审核信息 |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

### 28.4 `ads_research_problem_strategic_advice`

逻辑Key：`advice_id`。当前包含406条问题级模型建议和480条范围级确定性建议：Topic 450条、Field
26条、Domain 4条。范围级建议只为证据充足的范围发布；仅含1至2个问题的1,043个Topic保留范围指标，
不生成正式建议。

| 字段组 | 字段 | 类型 | 当前口径 |
|---|---|---|---|
| Key | `advice_id` | `VARCHAR(256) NOT NULL` | 稳定建议ID |
| 范围 | `scope_type/scope_id/problem_id/advice_version` | `STRING` | 建议范围、对象与版本 |
| 展示 | `scope_name_zh/advice_title_zh/advice_summary_zh` | `STRING` | 范围名称及建议内容 |
| 行动 | `recommended_action_zh` | `STRING` | 问题级模型行动或范围级规则模板行动 |
| 优先级 | `strategic_priority_score/strategic_priority_level` | `DECIMAL/STRING` | 正式战略优先级 |
| 分项 | `policy_alignment_score/layout_gap_score` | `DECIMAL(9,6)` | 政策契合与布局缺口；政策无证据时保持NULL |
| 参考 | `potential_score/hotspot_score` | `DECIMAL(9,6)` | 已有潜力与热点参考分 |
| 建议 | `recommended_horizon/recommended_institution_ids` | `STRING/ARRAY<STRING>` | 建议周期及推荐机构 |
| 证据 | `evidence_ids` | `ARRAY<STRING>` | 战略建议证据ID |
| 方法 | `advice_method` | `STRING` | 问题级为证据约束模型判断；范围级为`DETERMINISTIC_SCOPE_AGGREGATION_FROM_PROBLEM_EVIDENCE_V1` |
| 审核 | `review_status/reviewer/reviewed_at` | `STRING/STRING/DATETIME` | 范围级为`APPROVED_RULE_BASED`及系统审核溯源 |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

### 28.5 `ads_research_problem_update_signal`

逻辑Key：`signal_id`。当前零行，只有完成两个可比发布或时间窗口后才允许写入。

| 字段组 | 字段 | 类型 | 口径 |
|---|---|---|---|
| Key | `signal_id` | `VARCHAR(256) NOT NULL` | 稳定变化信号ID |
| 关联 | `problem_id/signal_version/signal_type` | `STRING` | 问题、信号版本和类型 |
| 时间 | `signal_date/comparison_start_date/comparison_end_date` | `DATE` | 触发日及比较窗口 |
| 指标 | `metric_name` | `STRING` | 触发信号的指标 |
| 变化 | `previous_value/current_value/absolute_change` | `DOUBLE` | 前值、当前值和绝对变化 |
| 变化 | `change_rate` | `DECIMAL(18,8)` | 相对变化率 |
| 阈值 | `trigger_threshold/severity` | `DOUBLE/STRING` | 触发阈值与严重等级 |
| 标签 | `is_new` | `BOOLEAN` | 是否为新问题信号，不从生成时间猜测 |
| 溯源 | `source_table/evidence_ids/signal_summary_zh` | `STRING/ARRAY/STRING` | 来源、证据和摘要 |
| 处理 | `processing_status/acknowledged_at/acknowledged_by` | `STRING/DATETIME/STRING` | 信号处理状态 |
| 状态 | `supplement_status` | `STRING` | 当前契约为`PENDING_INCREMENTAL_COMPARISON` |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

### 28.6 发布状态

2026-10-20已发布Iceberg `research_problem_ads_v2_20261020`和Doris数据版本`202610200201`。基础问题
ADS共43张表；新增表行数分别为部署406、方向1,556、深圳机构匹配候选642、战略建议406、更新信号0。
43张表Iceberg与Doris逐表行数一致，逻辑Key重复数为0。旧Iceberg namespace保持不变。

## 29. 基础研究问题模型推理增强 ADS（5.5.0）

5.5.0 使用 DeepSeek 对现有问题证据进行第二阶段判断。按业务要求不再设置人工审核门槛，模型输出以
`AUTO_APPROVED_LLM` 正式发布；但所有结果必须保留 provider、model、prompt version、input hash 和
generated time，且不得改变原始论文、专利、项目、资金或年度计数事实。

### 29.1 月度估算隔离

`ads_research_problem_monthly_metrics`自5.16.0起保存直接事件日期聚合的真实月度事实；5.5.0新增的
`ads_research_problem_monthly_estimate`，逻辑 Key 为
`problem_id, statistics_month, metric_name`：

| 字段 | 类型 | 口径 |
|---|---|---|
| `estimated_value` | `DOUBLE` | 年度事实按模型月度权重分布后的估算值 |
| `estimate_method` | `STRING` | 固定 `LLM_TEMPORAL_DISTRIBUTION` |
| `confidence` | `DECIMAL(9,6)` | 模型对分布形态的置信度 |
| `lower_bound/upper_bound` | `DOUBLE` | 模型不确定性比率形成的估算区间 |
| `value_currency` | `STRING` | 仅资金指标保留年度事实的原币种 |
| `source_annual_year/source_annual_value` | `INT/DOUBLE` | 估算所依据的年度事实 |
| `estimated_growth_rate_3m` | `DECIMAL(18,8)` | 当前估算值相对三个月前估算值的变化率 |
| `inference_provider/model/prompt_version/input_hash/generated_at` | `STRING/DATETIME` | 完整模型溯源 |

估算覆盖2023—2025年的`PAPER_COUNT`、`PATENT_COUNT`、`PROJECT_COUNT`和
`FUNDING_AMOUNT`。缺少年度金额时资金估算保持NULL。估算值不得写入任何真实计数字段。
`ads_research_problem_development_snapshot`另增`estimated_continuous_active_months`、
`estimated_continuous_decline_months`、`monthly_estimate_confidence`和`monthly_estimate_method`；原
`continuous_active_months/continuous_decline_months`事实字段继续保持NULL。

### 29.2 正式模型判断

| 表 | 5.5.0 写入内容 | 状态与边界 |
|---|---|---|
| `ads_research_problem_deployment` | 战略优先级、理由、推荐/牵头机构、建议投入等级 | `AUTO_APPROVED_LLM` |
| `ads_research_problem_direction` | 1,556条方向全部写为`APPROVED`并置为正式方向；审核理由保留原模型状态与理由 | 操作方批量批准；原模型判断继续保留在固定AI Seed中供审计 |
| `ads_research_problem_institution_match` | 五维能力分、综合分、角色与理由 | 直接证据候选和全局回退候选分开标识 |
| `ads_research_problem_strategic_advice` | 政策契合、布局缺口、行动建议和周期 | 证据约束模型判断 |
| `ads_research_problem_update_signal` | 新问题及热度变化信号 | 真实前值、当前值和变化率仍为空 |
| `ads_research_problem_policy_evidence` | AI生成政策语境及契合分 | `is_synthetic=true`，不得作为真实政策引用 |
| `ads_research_problem_forecast_yearly` | 2026—2028四项指标情景估算 | `AI_ESTIMATED_NOT_BACKTESTED` |
| `ads_research_problem_similarity` | 模型逐对语义判断分 | 不是向量embedding余弦相似度 |

政策语境不生成文号、发布日期、URL或虚构政策文件。缺少问题级深圳机构证据时，只能从明确标为
`GLOBAL_SHENZHEN_FALLBACK_NO_DIRECT_PROBLEM_EVIDENCE` 的候选池中推荐；该候选机构的全局成果数不得
写入问题—机构直接证据计数字段。

### 29.3 仍为空的事实

缺少来源金额的项目真实金额、逐项目历史汇率、逐月引用事件、月度拨款事实、预测回测误差和向量
embedding继续保持NULL。官方政策和直接事件月度事实已由后续5.12.0与5.16.0版本补充；模型估算仍与
事实字段隔离。

详细执行与治理说明见
[`docs/research_problem_deepseek_inference_v1.md`](docs/research_problem_deepseek_inference_v1.md)。

5.5.0已发布到Iceberg `research_problem_ads_v3_20261020`和Doris
`gkx_technology_analysis_dev`（`data_version=202610200301`）。44张表逐表对账一致，详细行数与仍为空
事实见`reports/research_problem_ads_v3_20261020/deepseek_inference_verification.md`。

## 30. 基础研究问题增长率中位数（5.9.0）

`ads_research_problem_overview_snapshot`保留既有`avg_relative_growth`以兼容已有查询，同时新增适合
总览展示的稳健增长指标及其支持数据：

| 字段 | 类型 | 口径 |
|---|---|---|
| `median_relative_growth_rate` | `DECIMAL(18,8)` | 对有效问题的`relative_growth - 1`取中位数；可直接按百分比格式展示 |
| `relative_growth_sample_count` | `BIGINT` | `relative_growth`非空、实际进入中位数计算的问题数 |
| `relative_growth_total_problem_count` | `BIGINT` | 总览中的全部问题数 |
| `relative_growth_coverage_rate` | `DECIMAL(9,6)` | 有效样本数除以全部问题数 |
| `relative_growth_statistic_method` | `STRING` | 固定`MEDIAN_RECENT_BASELINE_SHARE_RATIO_MINUS_ONE` |

其中`relative_growth`是近期平均论文份额与基期平均论文份额的比值，`1`表示份额持平；因此中位数展示
字段先减去`1`，例如`0.20`表示中位问题的近期份额相对基期增长约20%。中位数使用Trino
`approx_percentile(..., 0.5)`计算，避免少数接近零基期造成的超大倍数主导总览指标。

### 30.1 前端查询近三个月显著增长问题清单

当前没有单独物化“近三个月增长问题清单”表。前端应从
`ads_research_problem_monthly_estimate`按与总览一致的口径计算问题级清单，并连接
`ads_research_problem_profile`取得问题名称与热点信息。当前比较窗口固定为2025年7—9月和
2025年10—12月，指标固定为`PAPER_COUNT`；增长超过10%定义为`RISING`，下降超过10%定义为
`DECLINING`，其余可比较问题定义为`STABLE`。

```sql
WITH problem_growth AS (
    SELECT
        problem_id,
        SUM(estimated_value) FILTER (
            WHERE statistics_month BETWEEN '2025-07' AND '2025-09'
        ) AS previous_3m_value,
        SUM(estimated_value) FILTER (
            WHERE statistics_month BETWEEN '2025-10' AND '2025-12'
        ) AS recent_3m_value,
        COUNT(estimated_value) FILTER (
            WHERE statistics_month BETWEEN '2025-07' AND '2025-09'
        ) AS previous_month_count,
        COUNT(estimated_value) FILTER (
            WHERE statistics_month BETWEEN '2025-10' AND '2025-12'
        ) AS recent_month_count,
        MIN(confidence) FILTER (
            WHERE statistics_month BETWEEN '2025-07' AND '2025-12'
        ) AS comparison_confidence,
        MAX(estimate_method) AS estimate_method
    FROM iceberg.research_problem_ads_v6_20261022
        .ads_research_problem_monthly_estimate
    WHERE metric_name = 'PAPER_COUNT'
    GROUP BY problem_id
), growth_result AS (
    SELECT
        problem_id,
        previous_3m_value,
        recent_3m_value,
        previous_month_count,
        recent_month_count,
        comparison_confidence,
        estimate_method,
        (recent_3m_value - previous_3m_value)
            / NULLIF(previous_3m_value, 0) AS growth_rate_3m
    FROM problem_growth
), classified AS (
    SELECT
        *,
        CASE
            WHEN growth_rate_3m > 0.10 THEN 'RISING'
            WHEN growth_rate_3m < -0.10 THEN 'DECLINING'
            ELSE 'STABLE'
        END AS growth_status,
        CASE
            WHEN previous_month_count = 3 AND recent_month_count = 3
                THEN 'FULL_SIX_MONTH_WINDOW'
            ELSE 'PARTIAL_WINDOW'
        END AS comparison_coverage_status
    FROM growth_result
    WHERE growth_rate_3m IS NOT NULL
)
SELECT
    g.problem_id,
    p.canonical_title_zh,
    p.canonical_title_en,
    g.previous_3m_value,
    g.recent_3m_value,
    g.growth_rate_3m,
    g.growth_status,
    g.previous_month_count,
    g.recent_month_count,
    g.comparison_coverage_status,
    g.comparison_confidence,
    g.estimate_method,
    p.hotspot_score,
    p.hotspot_status
FROM classified g
JOIN iceberg.research_problem_ads_v6_20261022
    .ads_research_problem_profile p
    ON p.problem_id = g.problem_id
WHERE g.growth_status = 'RISING'
ORDER BY g.growth_rate_3m DESC, g.problem_id;
```

移除最后的`WHERE g.growth_status = 'RISING'`即可返回全部可比较问题。当前数据中有月度估算的问题为
364个，其中88个可计算上述两个窗口的增长率：`RISING`67个、`DECLINING`4个、`STABLE`17个。
前端展示“上升占比”时必须明确分母，推荐显示可比较样本口径：`67 / 88 = 76.14%`；同时显示
“有效样本88个”。不得把该比例解释为406个问题总体中的真实观测上升比例。

上述数据全部来自模型月度分布估算。前端必须展示`estimate_method`和`comparison_confidence`，并标注
“月度模型估算，非真实月度观测”。若`comparison_coverage_status='PARTIAL_WINDOW'`，应进一步提示窗口
月份不完整，不能静默解释为完整三个月对比。后续滚动到新时间窗口时，应由服务端传入窗口边界或更新
查询视图，不能继续把2025年固定窗口称为当前自然时间的“近三个月”。

5.9.0已发布到Iceberg `research_problem_ads_v4_20261022`和Doris
`gkx_technology_analysis_dev`（`data_version=202610220101`）。实际中位增长率为`-0.02900810`，即
`-2.900810%`；有效样本345/406，覆盖率`0.849754`。Iceberg与Doris结果一致。

## 31. 基础研究问题年度衰减周期（5.10.0）

`ads_research_problem_development_snapshot`使用`ads_research_problem_yearly_metrics.paper_count`计算截至
最新完整观测年的连续同比衰减周期。当前完整年度上限为2025年；2026年可能是不完整年度，不进入年度
生命周期、衰减周期或衰减率计算。该算法是确定性年度统计，不使用月度模型估算或大模型判断。

| 字段 | 类型 | 口径 |
|---|---|---|
| `decline_start_year` | `INT` | 当前连续衰减段第一个同比下降年份；当前未衰减时为NULL |
| `decline_end_year` | `INT` | 当前连续衰减段最后一个同比下降年份；当前未衰减时为NULL |
| `continuous_decline_years` | `BIGINT` | 截至最新完整观测年的连续同比下降次数 |
| `observed_decline_years` | `BIGINT` | 全部有效相邻年度中观察到的同比下降次数，不要求连续且不只限当前衰减段 |
| `decline_rate_avg` | `DECIMAL(18,8)` | 当前连续衰减段各年度同比增长率的算术平均；衰减时为负数 |
| `decline_rate_cagr` | `DECIMAL(18,8)` | 从衰减开始前一年到衰减结束年的复合年变化率；衰减时为负数 |
| `decline_metric` | `STRING` | 固定`PAPER_COUNT` |
| `decline_status` | `STRING` | `DECLINING/GROWING/RECOVERING/STABLE/INSUFFICIENT_EVIDENCE` |
| `decline_calculation_method` | `STRING` | 固定`TRAILING_CONSECUTIVE_YEAR_OVER_YEAR_DECLINE_V1` |

只有年份相邻的数据才能形成同比判断；存在年度间断时不跨缺口计算衰减。状态规则如下：

- `DECLINING`：最新可用完整年度仍处于连续下降段。
- `RECOVERING`：最新年度增长，且历史上至少观察到一次同比下降。
- `GROWING`：最新年度增长，且历史上没有观察到同比下降。
- `STABLE`：最新年度论文数与上一相邻年度相同。
- `INSUFFICIENT_EVIDENCE`：没有相邻上一年度，不能计算最新年度同比状态。

前端查询示例：

```sql
SELECT
    d.problem_id,
    p.canonical_title_zh,
    d.latest_active_year,
    d.decline_start_year,
    d.decline_end_year,
    d.continuous_decline_years,
    d.observed_decline_years,
    d.decline_rate_avg,
    d.decline_rate_cagr,
    d.decline_metric,
    d.decline_status,
    d.decline_calculation_method
FROM iceberg.research_problem_ads_v6_20261022
    .ads_research_problem_development_snapshot d
JOIN iceberg.research_problem_ads_v6_20261022
    .ads_research_problem_profile p
    ON p.problem_id = d.problem_id
WHERE d.decline_status = 'DECLINING'
ORDER BY
    d.continuous_decline_years DESC,
    d.decline_rate_cagr,
    d.problem_id;
```

5.10.0已发布到Iceberg `research_problem_ads_v5_20261022`和Doris
`gkx_technology_analysis_dev`（`data_version=202610220201`）。406个问题的年度衰减状态已全部写入：
`DECLINING`96、`RECOVERING`48、`GROWING`14、`STABLE`123、`INSUFFICIENT_EVIDENCE`125。
96个当前衰减问题中，连续衰减1年82个、连续衰减2年14个。Iceberg与Doris结果一致。

## 32. 基础研究问题潜在合作领域推荐（5.11.0）

新增`ads_research_problem_collaboration_recommendation`，为预测报告详情页提供可直接查询的“潜在合作
领域 + 牵头机构 + 合作机构”推荐。逻辑Key为`recommendation_id`。当前每个问题取正式研究方向
`direction_rank<=3`，并组合该问题机构匹配`match_rank<=3`，形成3条推荐；本表不新增模型调用，
只确定性组合已发布的DeepSeek方向审核和机构匹配结果。

| 字段组 | 字段 | 类型 | 口径 |
|---|---|---|---|
| Key | `recommendation_id` | `VARCHAR(256) NOT NULL` | 问题、方向和机构数组生成的稳定ID |
| 关联 | `problem_id` | `STRING` | 基础问题ID |
| 合作领域 | `collaboration_field_id` | `STRING` | 当前等于正式方向ID |
| 合作领域 | `collaboration_field_name_zh/collaboration_field_name_en` | `STRING` | 正式方向中英文标题 |
| 方向 | `collaboration_direction_id/direction_type/horizon` | `STRING` | 来源方向ID、类型和周期 |
| 机构 | `recommended_institution_ids` | `ARRAY<STRING>` | 该问题匹配排名前3的深圳候选机构；实际为1至3家 |
| 机构 | `lead_institution_id` | `STRING` | 前3名中角色为LEAD的最优机构；无LEAD时回退匹配排名第1 |
| 合作 | `collaboration_mode` | `STRING` | `MULTI_INSTITUTION_CONSORTIUM/LEAD_WITH_PARTNER/SINGLE_INSTITUTION_LEAD` |
| 评分 | `collaboration_score` | `DECIMAL(9,6)` | 55%方向匹配 + 35%机构能力 + 10%协作准备度，范围0—100 |
| 评分 | `institution_capability_score` | `DECIMAL(9,6)` | 推荐机构`overall_match_score`均值 |
| 评分 | `problem_direction_match_score` | `DECIMAL(9,6)` | 正式方向审核置信度乘100 |
| 评分 | `collaboration_readiness_score` | `DECIMAL(9,6)` | 推荐机构`collaboration_score`均值 |
| 评分 | `complementarity_score` | `DECIMAL(9,6)` | 当前NULL；不能用单机构能力分伪造机构间互补性 |
| 状态 | `complementarity_score_status` | `STRING` | 固定`NOT_AVAILABLE_NO_PAIRWISE_INSTITUTION_COMPLEMENTARITY_EVIDENCE` |
| 说明 | `recommendation_reason_zh` | `STRING` | 合作领域、牵头机构、候选角色及评分摘要 |
| 证据 | `evidence_ids` | `ARRAY<STRING>` | 方向论文证据与机构匹配证据去重并集 |
| 排序 | `recommendation_rank` | `INT` | 问题内合作领域推荐序号1—3 |
| 置信 | `confidence` | `DECIMAL(9,6)` | 方向审核置信与机构判断最低置信度的较小值，范围0—1 |
| 方法 | `recommendation_method` | `STRING` | 固定`EVIDENCE_CONSTRAINED_DIRECTION_INSTITUTION_COMPOSITE_V1` |
| 状态 | `institution_evidence_status` | `STRING` | 直接问题证据、混合证据或深圳机构全局回退候选 |
| 状态 | `source_direction_review_status` | `STRING` | 来源方向的正式审核状态 |
| 状态 | `review_status` | `STRING` | 固定`AUTO_APPROVED_COMPOSITE` |
| 模型溯源 | `inference_provider/inference_model/inference_prompt_version` | `STRING` | 上游DeepSeek判断来源；prompt version为组合口径版本 |
| 模型溯源 | `inference_input_hash/inference_generated_at` | `STRING/DATETIME` | 组合输入hash和上游最近生成时间 |
| 模型溯源 | `source_inference_input_hashes` | `ARRAY<STRING>` | 方向及各推荐机构上游输入hash |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 通用统计与发布版本 |

综合推荐分计算如下：

```text
collaboration_score
  = 0.55 * problem_direction_match_score
  + 0.35 * institution_capability_score
  + 0.10 * collaboration_readiness_score
```

前端查询示例：

```sql
SELECT
    c.problem_id,
    p.canonical_title_zh AS problem_title_zh,
    c.collaboration_field_name_zh,
    c.direction_type,
    c.horizon,
    c.lead_institution_id,
    c.recommended_institution_ids,
    c.collaboration_mode,
    c.collaboration_score,
    c.recommendation_reason_zh,
    c.institution_evidence_status,
    c.confidence,
    c.recommendation_rank
FROM iceberg.research_problem_ads_v6_20261022
    .ads_research_problem_collaboration_recommendation c
JOIN iceberg.research_problem_ads_v6_20261022
    .ads_research_problem_profile p
    ON p.problem_id = c.problem_id
WHERE c.problem_id = :problem_id
ORDER BY c.recommendation_rank, c.recommendation_id;
```

前端必须区分`institution_evidence_status`：

- `DIRECT_PROBLEM_EVIDENCE`表示全部推荐机构均有该问题的直接深圳科研证据。
- `MIXED_DIRECT_AND_FALLBACK`表示推荐机构中同时存在直接证据和全局回退候选。
- `GLOBAL_SHENZHEN_FALLBACK_NO_DIRECT_PROBLEM_EVIDENCE`表示机构是深圳全局候选，不代表已参与该问题。

5.11.0已发布到Iceberg `research_problem_ads_v6_20261022`和Doris
`gkx_technology_analysis_dev`（`data_version=202610220301`）。新增表1,218行，覆盖406/406个问题，
每个问题3个合作领域；489行（163个问题）为全部直接问题证据，729行（243个问题）为全部全局回退候选。
机构数组为1家的174行、2家的66行、3家的978行。综合推荐分范围38.550000—84.983333，均值
65.270464。48行（涉及45个问题）的`evidence_ids`为空，表示方向论文证据与问题—机构实体证据均未提供；
这些记录仍有完整模型输入hash与生成时间，但前端必须显示“无实体证据，仅模型判断/全局候选”，不能据此
声称存在论文、项目或机构参与事实。Iceberg与Doris行数一致，逻辑Key重复数和字段边界异常均为0。

## 33. 基础研究问题官方政策证据与政策导向（5.12.0）

5.12.0以`policy_dwd_v1_20261023`的官方政策文档和条款替换5.5.0生成的合成政策语境。来源范围为
国家、广东省和深圳市政策，采集截止日为2026-10-22；当前语料不含深圳各区独立政策集合。问题—政策
关系采用中文二元词组召回候选，再由DeepSeek在候选政策和候选条款ID内进行证据约束判定。发布门槛为
`relation_confidence >= 0.65`，没有通过门槛的关系不写入，禁止为提高覆盖率强制匹配。

### 33.1 `ads_research_problem_policy_evidence`

一条记录表示一个问题与一份官方政策的匹配证据，逻辑Key为`problem_id, policy_id`。前端政策详情、
政策来源说明和政策导向下钻应查询此表。

| 字段组 | 字段 | 用途 |
|---|---|---|
| 关联 | `problem_id, policy_id, clause_id` | 问题、政策文档及命中条款ID |
| 政策身份 | `policy_title, document_number, policy_level` | 政策标题、文号及`NATIONAL/GUANGDONG/SHENZHEN`层级 |
| 发布主体 | `issuing_organization_name, issuing_organizations, location_id` | 第一发布机构、完整机构数组和地域ID |
| 时间 | `publication_date, document_date, statistics_date, statistics_year, statistics_date_source` | 原始日期及统计采用日期；统计日期优先文档日期，其次发布日期 |
| 有效性 | `effective_date, expiry_date, validity_status` | 生效、失效及`ACTIVE/REPLACED`状态 |
| 支持关系 | `support_type, relation_type, matched_terms` | 支持类型、`DIRECT_SUPPORT/FIELD_SUPPORT`和匹配词 |
| 模型判断 | `relation_method, relation_confidence, alignment_score, match_reason_zh` | 固定混合召回+证据判断方法、0—1置信度、0—100契合分及理由 |
| 证据 | `evidence_excerpt, canonical_url, verification_status, evidence_completeness, full_text_available` | 条款摘录、官方URL、核验和正文可得性 |
| 来源边界 | `is_synthetic, source_type, unavailable_reason` | 固定`false/OFFICIAL_POLICY_DOCUMENT`；缺日期或只有通知时说明原因 |
| 模型溯源 | `inference_provider, inference_model, inference_prompt_version, inference_input_hash, inference_generated_at` | DeepSeek判定的完整版本与输入溯源 |
| 治理 | `review_status, policy_collection_end_date, metrics_as_of_date, metric_definition_version, data_version, update_time` | 固定自动证据约束审核状态及发布版本 |

按问题查看正式政策证据：

```sql
SELECT
    e.problem_id,
    e.policy_id,
    e.policy_title,
    e.policy_level,
    e.issuing_organizations,
    e.statistics_date,
    e.validity_status,
    e.support_type,
    e.relation_type,
    e.alignment_score,
    e.relation_confidence,
    e.evidence_excerpt,
    e.canonical_url,
    e.verification_status
FROM iceberg.research_problem_ads_v7_20261023
    .ads_research_problem_policy_evidence e
WHERE e.problem_id = :problem_id
ORDER BY e.alignment_score DESC, e.statistics_date DESC, e.policy_id;
```

### 33.2 `ads_research_problem_policy_yearly_metrics`

本表粒度为`problem_id, statistics_year, policy_level, support_type`，用于“政策支持数量和时间分布”。

| 字段 | 用途 |
|---|---|
| `policy_count` | 该组合内去重政策数 |
| `active_policy_count/replaced_policy_count` | 当前有效与已被替代政策数 |
| `direct_support_policy_count` | `DIRECT_SUPPORT`去重政策数 |
| `issuing_organization_count` | 去重第一发布机构数 |
| `avg_relation_confidence/avg_alignment_score` | 平均匹配置信度与平均契合分 |
| `first_policy_date/latest_policy_date` | 组内最早和最新统计日期 |
| `policy_ids` | 可下钻的政策ID数组 |
| `coverage_status` | 固定`PARTIAL_OFFICIAL_POLICY_CORPUS`，表示当前语料不是政策全量库 |

时间分布查询：

```sql
SELECT
    statistics_year,
    policy_level,
    support_type,
    sum(policy_count) AS policy_count,
    sum(active_policy_count) AS active_policy_count,
    sum(direct_support_policy_count) AS direct_support_policy_count,
    avg(avg_alignment_score) AS avg_alignment_score
FROM iceberg.research_problem_ads_v7_20261023
    .ads_research_problem_policy_yearly_metrics
WHERE problem_id = :problem_id
GROUP BY statistics_year, policy_level, support_type
ORDER BY statistics_year, policy_level, support_type;
```

### 33.3 政策导向雷达维度

从`ads_research_problem_potential_dimension`筛选`dimension_code='POLICY_ALIGNMENT'`。有官方证据时，
`dimension_score`按政策数量35%、层级权威性20%、时效15%、年份连续性15%、问题契合度15%组合，
`score_method='OFFICIAL_POLICY_EVIDENCE_COMPOSITE_V1'`、
`evidence_status='PARTIAL_OFFICIAL_POLICY_EVIDENCE'`。没有匹配证据时`dimension_score`保持NULL，
`evidence_status='NO_MATCHED_OFFICIAL_POLICY'`；潜力总分仅按可用维度权重重新归一，不能把NULL展示为0分。

```sql
SELECT
    d.problem_id,
    d.dimension_score AS policy_alignment_score,
    d.dimension_weight,
    d.evidence_status,
    d.score_method
FROM iceberg.research_problem_ads_v7_20261023
    .ads_research_problem_potential_dimension d
WHERE d.dimension_code = 'POLICY_ALIGNMENT'
  AND d.problem_id = :problem_id;
```

### 33.4 当前数据结果和展示边界

- 政策DWD共有93份文档、93条条款和19条来源注册记录：国家27、广东29、深圳37。
- 82份政策具有可用于时间统计的日期，11份缺日期；87份为`ACTIVE`，6份为`REPLACED`；85份有正文，
  8份只有通知或元数据。
- 406个问题全部完成候选判定，发布39条关系，覆盖35个问题和8份政策；371个问题没有达到门槛的
  官方政策证据，政策导向维度保持NULL。
- 39条关系中，国家3、广东14、深圳22；`DIRECT_SUPPORT`1条、`FIELD_SUPPORT`38条。
- 政策导向得分仅覆盖35个问题，范围52.725399—80.410714，均值63.582292。
- 语料采集状态为`PARTIAL`。政策数只能表述为“当前已采集官方政策语料中的匹配数量”，不能表述为
  政府发布的全部相关政策数量；缺失的深圳区级政策和后续新增政策需通过新发布版本补充。

Iceberg使用`research_problem_ads_v7_20261023`，Doris使用`gkx_technology_analysis_dev`；两端政策证据
和年度统计均为39行且逻辑Key重复数为0。运行与核验详情见
[`docs/research_problem_official_policy_v1.md`](docs/research_problem_official_policy_v1.md)。

## 34. 基础研究问题方向批量批准（5.12.1）

根据操作方明确批准，`ads_research_problem_direction`的1,556条方向在新发布中统一写为
`review_status='APPROVED'`、`is_official=true`，审核主体为`OPERATOR:BULK_APPROVAL`。固定AI Seed中的
原始模型状态APPROVED 885、REVISED 660、REJECTED 11不改写；新表的`review_reason_zh`同时保存原模型
状态、原理由和批准策略，`inference_*`字段继续指向原模型判断。

该表粒度是“一问题的一方向”，不是“一问题一行”。406个问题各有3至6条方向：3条136个问题、4条
213个、5条46个、6条11个，合计1,556条。`ads_research_problem_deployment.approved_direction_ids`同步
包含全部方向；潜在方向推荐不再排除原REJECTED方向。Iceberg发布为
`research_problem_ads_v8_20261023`，Doris `data_version=202610230201`，旧发布保持不变。

## 35. 基础研究问题机构主导单位规则（5.12.2）

`ads_research_problem_institution_match`使用固定Snapshot
`institution_ads_mvp_v1_stage.ads_institution_profile@8133436263903776083`补齐全部候选机构的
`institution_type_id`。每个问题必须且只能有一家`recommended_role='LEAD'`：只有一家候选机构时直接作为
主导单位；有多家候选机构时，按论文数、专利数和项目数之和降序选择。问题级直接证据使用
`paper_count/patent_count/project_count`，全局回退候选使用对应的`global_candidate_*`计数；两类口径不混写。

当最高贡献计数相同时，使用
`xxhash64(problem_id || institution_id || 'research_problem_contribution_lead_selection_v1')`稳定抽取一家，
避免相同发布输入在重跑时产生不同主导单位。原模型判定为`LEAD`但未被规则选中的机构改记为
`CORE_PARTNER`，其他非主导角色保持模型结果。`recommendation_reason`同时记录机构类型、关联机构数、贡献
计数、贡献排名及原模型理由。

新发布使用Iceberg `research_problem_ads_v9_20261023`和Doris
`data_version=202610230301`；旧发布与固定机构画像Snapshot均不改写。

## 36. 基础研究问题中文搜索索引（5.12.3）

Doris Serving层为基础研究问题建立8个倒排索引，不改变Iceberg表、行数据或`data_version`：

| 表.字段 | 索引 | 分词与用途 |
|---|---|---|
| `ads_research_problem_profile.canonical_title_zh` | `idx_rp_profile_title_zh` | 中文细粒度分词，标题全文检索 |
| `ads_research_problem_profile.problem_statement_zh` | `idx_rp_profile_statement_zh` | 中文细粒度分词，问题陈述检索 |
| `ads_research_problem_profile.knowledge_gap_zh` | `idx_rp_profile_gap_zh` | 中文细粒度分词，知识缺口检索 |
| `ads_research_problem_profile.research_background_zh` | `idx_rp_profile_background_zh` | 中文细粒度分词，研究背景检索 |
| `ads_research_problem_profile.current_research_summary_zh` | `idx_rp_profile_summary_zh` | 中文细粒度分词，研究摘要检索 |
| `ads_research_problem_keyword.keyword_zh` | `idx_rp_keyword_zh` | 中文细粒度分词，关键词全文检索 |
| `ads_research_problem_keyword.keyword_key` | `idx_rp_keyword_key` | 不分词，规范关键词精确过滤 |
| `ads_research_problem_keyword.keyword_type` | `idx_rp_keyword_type` | 不分词，关键词类型精确过滤 |

中文索引统一使用`parser=chinese`、`parser_mode=fine_grained`、`support_phrase=true`，支持Doris
`MATCH_ANY`、`MATCH_ALL`和`MATCH_PHRASE`查询。`LIKE`仍可用于兼容查询，但Doris全文倒排索引由`MATCH`
操作符使用。迁移文件为
[`sql/doris/ads_schema_5_12_3_research_problem_search_indexes.sql`](sql/doris/ads_schema_5_12_3_research_problem_search_indexes.sql)。

本发布完成字段级分词和历史数据索引构建；跨字段权重融合、同义词、拼写纠错、搜索高亮和前端交互仍由
下游科研数据发掘平台实现。

## 37. 基础研究问题项目资金人民币归一（5.12.4）

使用操作方提供的固定最新中间价，把具有有效原币金额的项目统一换算为人民币。汇率口径为
“1单位原币对应人民币元数”；JPY原始报价`100 JPY = 4.2793 CNY`已规范化为
`1 JPY = 0.042793 CNY`。汇率基准日期记录为`2026-10-23`，来源标识为
`OPERATOR_PROVIDED_LATEST_MID_RATE`，换算策略为`FIXED_SNAPSHOT_CNY_PER_CURRENCY_UNIT_V1`。

| 币种 | CNY/原币单位 |
|---|---:|
| USD | 6.7180 |
| EUR | 7.5140 |
| JPY | 0.042793 |
| CHF | 8.1710 |
| CAD | 4.7804 |
| AUD | 4.6982 |

`ads_research_problem_funding_evidence.funding_amount_cny`按项目逐笔换算并保留4位小数；
`ads_research_problem_yearly_metrics.funding_amount_cny`和
`ads_research_problem_profile.funding_amount_cny`分别汇总逐笔人民币金额。原币金额与币种保持不变，
`exchange_rate`、`exchange_rate_date`和`normalization_status`保留本次换算依据。

`ads_research_problem_region_yearly_metrics.funding_amount_cny`仍为空：当前项目资金缺少可靠的机构或地区
分摊依据，禁止把项目总额复制到多个参与地区。该固定快照只提供名义金额横向换算，不代表历史项目发生
年份的购买力或当年汇率。

新发布使用Iceberg `research_problem_ads_v10_20261023`和Doris
`data_version=202610230401`；旧发布保持不变。

## 38. 基础研究问题机构成果与重点学科（5.13.0）

5.13.0新增两张物化ADS表，把“机构与问题相关”进一步约束为“机构与具体成果存在可追溯关系”。只处理
`ads_research_problem_institution_match.candidate_source='EXISTING_SHENZHEN_EVIDENCE'`的机构—问题对；
全局深圳回退推荐机构不计为实际参与机构。

### 38.1 `ads_research_problem_institution_achievement`

逻辑Key：`achievement_relation_id`，由`problem_id + institution_id + achievement_type + achievement_id`
稳定生成。同一成果支持多个问题时保留多条问题级关系。

| 字段组 | 字段 | 类型 | 说明 |
|---|---|---|---|
| Key | `achievement_relation_id` | `VARCHAR(256)` | 问题—机构—成果稳定关系ID |
| 问题与机构 | `problem_id/institution_id/model_version` | `VARCHAR` | 问题、平台机构及机构匹配版本 |
| 机构展示 | `institution_name/institution_type_id/district_location_id` | `VARCHAR` | 机构名称、类型和深圳区级位置 |
| 推荐语境 | `recommended_role/candidate_source` | `VARCHAR` | 主导/伙伴角色；本表只接受已有深圳证据候选 |
| 成果Key | `achievement_type` | `VARCHAR` | `PAPER`、`PATENT`或`PROJECT` |
| 成果Key | `achievement_id/source_achievement_id` | `VARCHAR` | 平台成果ID与OpenAlex/Google来源ID |
| 成果展示 | `achievement_title/achievement_date/achievement_year` | `VARCHAR/DATE/INT` | 成果名称及时间 |
| 问题证据 | `problem_evidence_level` | `VARCHAR` | 成果对问题的`DIRECT/PROXY`证据等级 |
| 机构证据 | `institution_role` | `VARCHAR` | 论文署名机构、确认受让机构或项目机构角色 |
| 机构证据 | `institution_evidence_type` | `VARCHAR` | 署名、confirmed assignee、直接项目机构或受资助论文机构兜底 |
| 机构证据 | `institution_evidence_count/relation_confidence` | `BIGINT/DECIMAL` | 署名作者数、assignee事实数或项目论文证据数，以及来源匹配置信度 |
| 排序指标 | `citation_count/funding_amount_cny` | `BIGINT/DECIMAL` | 论文引用数或项目人民币金额；不适用时为空 |
| 排序指标 | `representative_rank` | `BIGINT` | 同一问题、机构、成果类型内的代表成果排序 |
| 溯源 | `source_relation_id/source_relation_snapshot_id` | `VARCHAR` | 具体成果—机构关系ID及固定Snapshot |
| 边界 | `ownership_scope_note` | `VARCHAR` | 明示论文署名、项目关系或“确认受让人不等于当前权利人”等边界 |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | 公共类型 | 统计截止、口径和发布版本 |

三类成果关联固定为：

```text
问题论文.openalex_work_id
  -> dwd_work_authorship_institution.work_id
  -> entity_source_identity
  -> 平台 institution_id

问题专利.google_patent_publication_id
  -> dwd_patent_institution_google.publication_id
  -> confirmed platform_institution_id

问题项目.project_id
  -> ads_project_institution.project_id
  -> institution_id
```

禁止仅按`problem_id`把问题下全部成果归给所有问题机构。专利关系只消费`resolution_status='confirmed'`；
Google来源不能区分当前权利人，因此不得把本表解释为当前专利所有权。

### 38.2 `ads_research_problem_institution_discipline_metrics`

逻辑Key：`institution_id, topic_id, model_version`。本表只聚合上一张已验证成果关系，不直接聚合推荐候选。

| 字段组 | 字段 | 类型 | 说明 |
|---|---|---|---|
| Key | `institution_id/topic_id/model_version` | `VARCHAR` | 机构、Topic与机构匹配版本 |
| 展示 | `institution_name/institution_type_id` | `VARCHAR` | 机构名称与类型 |
| 学科 | `topic_name_zh/topic_name_en/subfield_id/field_id/domain_id` | `VARCHAR` | Topic双语名称及完整上级学科ID |
| 参与规模 | `problem_count/direct_problem_count` | `BIGINT` | 经成果关系确认的问题数及DIRECT问题数 |
| 成果规模 | `paper_count/patent_count/project_count` | `BIGINT` | 去重论文、专利和项目数 |
| 时间 | `first_achievement_year/latest_achievement_year` | `INT` | 最早与最近成果年份 |
| 明细入口 | `problem_ids` | `ARRAY<STRING>` | 本机构该Topic下的去重问题ID |
| 代表成果 | `representative_achievement_ids` | `ARRAY<STRING>` | 最多20个代表成果ID |
| 排名 | `discipline_rank` | `BIGINT` | 机构内部重点Topic排名 |
| 口径 | `participation_basis` | `VARCHAR` | 固定为`VERIFIED_ACHIEVEMENT_RELATION` |
| 治理 | `metrics_as_of_date/metric_definition_version/data_version/update_time` | 公共类型 | 统计截止、口径和发布版本 |

机构参与问题数必须从成果明细表执行`count(DISTINCT problem_id)`，不能对多个Topic的`problem_count`
直接求和，因为同一个问题可以属于多个Topic。新发布使用Iceberg
`research_problem_ads_v11_20261023`和Doris `data_version=202610231001`；旧发布保持不变。

直接读取`ads_research_problem_institution_match`时必须按当前`data_version`过滤。Doris Unique Key只会
覆盖逻辑Key相同的记录，旧发布中逻辑Key不同的历史候选仍可能保留；5.13.0两张新表由固定v11 Iceberg
输入物化，不受这些历史候选影响。

实际发布`ads_research_problem_institution_achievement`4,586行，覆盖65家机构、163个问题和642个
已有深圳证据机构—问题对，其中论文2,877行、项目1,709行。当前固定confirmed专利机构Snapshot与
这些机构—问题对不存在成果交集，因此专利成果为0行；不能用问题级`patent_count`替代具体专利—机构
证据。`ads_research_problem_institution_discipline_metrics`发布5,492行，覆盖65家机构和865个Topic。

## 39. 基础研究问题机构人才事实（5.14.0）

`ads_research_problem_institution_match.talent_count`使用问题人才和论文署名机构的同成果交集计算：

```text
ads_research_problem_talent(problem_id, talent_id, openalex_author_id, evidence_work_ids)
  -> UNNEST(evidence_work_ids)
  -> dwd_work_authorship_institution(work_id, author_id, institution_id)
  -> entity_source_identity
  -> platform institution_id
```

只有同一名作者在同一篇问题证据论文上署名目标机构时才计入，并按
`problem_id, institution_id, talent_id`去重。不得把机构画像中的全部人才数复制到每一个问题；人才曾在
其他论文或其他年份关联该机构，不足以证明该机构通过该人才参与当前问题。

新增字段：

| 表.字段 | 类型 | 说明 |
|---|---|---|
| `ads_research_problem_institution_match.talent_count` | `BIGINT` | DIRECT和PROXY证据人才去重并集；未命中为0，不再为NULL |
| `ads_research_problem_institution_match.direct_talent_count` | `BIGINT` | DIRECT问题证据人才数 |
| `ads_research_problem_institution_match.proxy_talent_count` | `BIGINT` | PROXY问题证据人才数 |
| `ads_research_problem_institution_match.talent_evidence_type` | `STRING` | 固定计算口径标识 |

原全局回退候选若取得上述同论文人才署名证据，`candidate_source`改记为
`EXISTING_SHENZHEN_TALENT_EVIDENCE`；其全局论文、专利和项目计数仍保留在`global_candidate_*`字段，
不会伪装成问题级成果计数。人才数不进入现有主导单位贡献排名，避免和论文贡献重复放大；主导单位仍按
论文、专利、项目计数之和确定。

实际发布2,586个机构—问题匹配，覆盖406个问题和65家机构；`talent_count`空值0行，725个机构—问题对
人才数大于0，机构—问题人才计数合计2,673，单对最大52。按来源分为已有成果证据642对、人才署名证据
417对、无直接问题证据全局回退1,527对。406个问题全部有机构候选，其中348个问题有多家机构可横向
比较，58个问题只有一家候选机构。

新发布使用Iceberg `research_problem_ads_v12_20261023`和Doris
`data_version=202610231101`。Doris该表当前只保留本版本2,586行；此前642条
`data_version=202610200201`历史记录已按操作方要求删除。

## 40. Topic/Field/Domain战略优先级物化（5.15.0）

5.15.0把问题级潜力、热点、政策和布局缺口按OpenAlex学科层级物化为可直接供条形图、雷达图、
层级树和战略建议面板读取的正式结果。聚合采用问题等权、仅对可用值求平均；未知政策证据保持NULL，
不按0分处理。范围级结果是确定性指标聚合和规则模板，不是新增的大模型预测。

### 40.1 `ads_research_problem_scope_potential_dimension`

逻辑Key：`scope_type, scope_id, dimension_code, model_version`。每个Topic、Field和Domain固定五个维度：
`ACADEMIC_IMPACT`、`TECHNOLOGY_TRANSFER`、`FUNDING_INTENSITY`、`COLLABORATION_BREADTH`、
`POLICY_ALIGNMENT`。

| 表.字段 | 类型 | 说明 |
|---|---|---|
| `ads_research_problem_scope_potential_dimension.scope_type` | `VARCHAR(256)` | `TOPIC/FIELD/DOMAIN` |
| `ads_research_problem_scope_potential_dimension.scope_id` | `VARCHAR(256)` | 范围ID |
| `ads_research_problem_scope_potential_dimension.dimension_code` | `VARCHAR(256)` | 五维潜力代码 |
| `ads_research_problem_scope_potential_dimension.model_version` | `VARCHAR(256)` | 固定`research_problem_scope_potential_v1` |
| `ads_research_problem_scope_potential_dimension.scope_name_zh/scope_name_en` | `STRING` | 范围中英文名称 |
| `ads_research_problem_scope_potential_dimension.parent_scope_type/parent_scope_id` | `STRING` | Topic指向Field、Field指向Domain；Domain为空 |
| `ads_research_problem_scope_potential_dimension.dimension_score` | `DECIMAL(9,6)` | 范围内有值问题的维度均值；无证据为NULL |
| `ads_research_problem_scope_potential_dimension.dimension_weight` | `DECIMAL(9,6)` | 沿用问题级维度权重 |
| `ads_research_problem_scope_potential_dimension.problem_count` | `BIGINT` | 范围内去重问题数 |
| `ads_research_problem_scope_potential_dimension.scored_problem_count` | `BIGINT` | 该维度有值的问题数 |
| `ads_research_problem_scope_potential_dimension.dimension_coverage_rate` | `DECIMAL(9,6)` | `scored_problem_count/problem_count` |
| `ads_research_problem_scope_potential_dimension.dimension_score_p50` | `DECIMAL(9,6)` | 有值问题维度分中位数 |
| `ads_research_problem_scope_potential_dimension.source_problem_ids` | `ARRAY<STRING>` | 参与聚合的全部问题ID |
| `ads_research_problem_scope_potential_dimension.evidence_status` | `STRING` | `AVAILABLE/PARTIAL/NO_EVIDENCE` |
| `ads_research_problem_scope_potential_dimension.aggregation_method` | `STRING` | 固定`EQUAL_PROBLEM_WEIGHT_AVAILABLE_ONLY_V1` |
| `ads_research_problem_scope_potential_dimension.metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 统计日、口径与发布版本 |

实际发布7,615行：1,493个Topic、26个Field、4个Domain各五行。除政策维度外四个维度覆盖率均为100%；
政策维度有值范围为254个Topic、21个Field和4个Domain，平均问题覆盖率分别为9.2151%、8.4799%和
8.9343%。

### 40.2 `ads_research_problem_scope_strategy`

逻辑Key：`scope_type, scope_id, strategy_version`。综合优先级基础权重为潜力35%、热点30%、政策20%、
布局缺口15%；缺失分项从分母移除并对剩余权重归一，不把未知政策当0。潜力总分只纳入范围覆盖率至少
60%的维度。排名在各`scope_type`内独立计算。

| 表.字段 | 类型 | 说明 |
|---|---|---|
| `ads_research_problem_scope_strategy.scope_type/scope_id/strategy_version` | `VARCHAR(256)` | 范围、范围ID与`scope_strategy_v1` |
| `ads_research_problem_scope_strategy.scope_name_zh/scope_name_en` | `STRING` | 范围中英文名称 |
| `ads_research_problem_scope_strategy.parent_scope_type/parent_scope_id` | `STRING` | 上级学科范围 |
| `ads_research_problem_scope_strategy.problem_count` | `BIGINT` | 范围内去重问题数 |
| `ads_research_problem_scope_strategy.high_priority_problem_count` | `BIGINT` | 问题级高优先级数量 |
| `ads_research_problem_scope_strategy.potential_score/hotspot_score` | `DECIMAL(9,6)` | 范围潜力与热点聚合分 |
| `ads_research_problem_scope_strategy.policy_alignment_score/policy_coverage_rate` | `DECIMAL(9,6)` | 政策契合均值及问题覆盖率 |
| `ads_research_problem_scope_strategy.layout_gap_score` | `DECIMAL(9,6)` | 范围布局缺口均值 |
| `ads_research_problem_scope_strategy.strategic_priority_score/strategic_priority_level` | `DECIMAL(9,6)/STRING` | 归一加权优先级分及`HIGH/MEDIUM/LOW` |
| `ads_research_problem_scope_strategy.scope_rank` | `BIGINT` | 同层级优先级排名 |
| `ads_research_problem_scope_strategy.priority_dimension` | `STRING` | 加权贡献最大的潜力维度 |
| `ads_research_problem_scope_strategy.top_problem_ids` | `ARRAY<STRING>` | 按问题级优先级、潜力排序的前20个问题 |
| `ads_research_problem_scope_strategy.source_problem_ids` | `ARRAY<STRING>` | 范围内全部问题ID |
| `ads_research_problem_scope_strategy.recommended_institution_ids` | `ARRAY<STRING>` | 按直接证据问题数、覆盖问题数和事实成果排序的前10家机构 |
| `ads_research_problem_scope_strategy.evidence_coverage_rate` | `DECIMAL(9,6)` | 五维按权重汇总的证据覆盖率 |
| `ads_research_problem_scope_strategy.evidence_status` | `STRING` | `AVAILABLE/PARTIAL_EVIDENCE/INSUFFICIENT_SCOPE_SUPPORT` |
| `ads_research_problem_scope_strategy.calculation_method` | `STRING` | 固定优先级计算口径标识 |
| `ads_research_problem_scope_strategy.metrics_as_of_date/metric_definition_version/data_version/update_time` | `DATE/STRING/BIGINT/DATETIME` | 统计日、口径与发布版本 |

实际发布1,523行：Topic 1,493、Field 26、Domain 4。全部名称、综合分、问题数组和推荐机构数组均有值，
且`source_problem_ids`元素数与`problem_count`一致。450个至少含3个问题的Topic、全部26个Field及4个
Domain可正式发布建议；其余1,043个Topic标记`INSUFFICIENT_SCOPE_SUPPORT`。

### 40.3 范围级正式战略建议

`ads_research_problem_strategic_advice`新增480条范围建议，`advice_method`固定为
`DETERMINISTIC_SCOPE_AGGREGATION_FROM_PROBLEM_EVIDENCE_V1`，`review_status`为
`APPROVED_RULE_BASED`，`evidence_ids`记录Top问题ID。问题级406条模型建议保持不变，总计886行。
范围建议由`ads_research_problem_scope_strategy`一一派生；低支持Topic不生成建议，避免单个问题被包装为
稳定的学科战略结论。

新发布使用Iceberg `research_problem_ads_v13_20261023`和Doris
`data_version=202610231201`，基础问题ADS由48张扩展为50张。50张表逐表对账一致，逻辑Key重复数和
语义边界非法数均为0。

## 41. 基础研究问题真实月度事实与月度热度（5.16.0）

`ads_research_problem_monthly_metrics`按`problem_id, statistics_month`保存真实日期支持的直接证据月度
事实。月份网格从每个问题首次直接事件月开始，连续生成到`metrics_as_of_date`之前最后一个完整自然月；
当前统计日为2026-10-19，因此观测截止月为2026-09。该表不读取
`ads_research_problem_monthly_estimate`，模型估算不得写入任何真实计数字段。

### 41.1 字段与来源

| 表.字段 | 类型 | 说明 |
|---|---|---|
| `ads_research_problem_monthly_metrics.problem_id/statistics_month` | `VARCHAR(256)` | 问题ID和`YYYY-MM`月份，联合逻辑Key |
| `ads_research_problem_monthly_metrics.paper_count` | `BIGINT` | 当月发布日期非空的DIRECT问题论文数 |
| `ads_research_problem_monthly_metrics.patent_count` | `BIGINT` | 当月公开日期非空的DIRECT问题专利数 |
| `ads_research_problem_monthly_metrics.project_count` | `BIGINT` | 当月开始日期非空的DIRECT问题项目数；项目日期不全时是已观察下界 |
| `ads_research_problem_monthly_metrics.new_talent_count` | `BIGINT` | OpenAlex作者首次出现在该问题DIRECT论文中的月份人数 |
| `ads_research_problem_monthly_metrics.new_institution_count` | `BIGINT` | OpenAlex机构首次出现在该问题DIRECT论文中的月份机构数 |
| `ads_research_problem_monthly_metrics.new_citation_count` | `BIGINT` | 当前NULL；没有逐月引用事件 |
| `ads_research_problem_monthly_metrics.funding_amount_original/funding_currency/funding_amount_cny` | `DECIMAL/STRING` | 当前NULL；项目总额不能冒充月度拨款 |
| `ads_research_problem_monthly_metrics.paper_activity_score` | `DECIMAL(9,6)` | 论文月度分项分，0—100 |
| `ads_research_problem_monthly_metrics.patent_activity_score` | `DECIMAL(9,6)` | 专利月度分项分，0—100 |
| `ads_research_problem_monthly_metrics.project_activity_score` | `DECIMAL(9,6)` | 已观察项目月度分项分，0—100 |
| `ads_research_problem_monthly_metrics.talent_activity_score` | `DECIMAL(9,6)` | 新增人才月度分项分，0—100 |
| `ads_research_problem_monthly_metrics.institution_activity_score` | `DECIMAL(9,6)` | 新增机构月度分项分，0—100 |
| `ads_research_problem_monthly_metrics.activity_score` | `DECIMAL(9,6)` | 五项分量的覆盖率重加权综合活动分 |
| `ads_research_problem_monthly_metrics.hotspot_score` | `DECIMAL(9,6)` | 当前及前两月活动分平滑形成的月度热度 |
| `ads_research_problem_monthly_metrics.month_growth_rate` | `DECIMAL(18,8)` | 活动分相对上月增长率 |
| `ads_research_problem_monthly_metrics.growth_rate_3m` | `DECIMAL(18,8)` | 最近3月平均活动分相对前3月平均活动分增长率 |
| `ads_research_problem_monthly_metrics.direct_project_count/dated_direct_project_count` | `BIGINT` | 问题全部DIRECT项目数和有可用开始日期数 |
| `ads_research_problem_monthly_metrics.project_date_coverage_rate` | `DECIMAL(9,6)` | 有日期DIRECT项目数/全部DIRECT项目数；无DIRECT项目时为1 |
| `ads_research_problem_monthly_metrics.project_count_is_lower_bound` | `BOOLEAN` | 项目日期不完整时为true |
| `ads_research_problem_monthly_metrics.paper_coverage_status/patent_coverage_status/project_coverage_status` | `STRING` | 各成果日期覆盖状态 |
| `ads_research_problem_monthly_metrics.metric_scope` | `STRING` | 固定`DIRECT_EVIDENCE`，不得与年度簇代理指标混用 |
| `ads_research_problem_monthly_metrics.calculation_method` | `STRING` | 固定`DIRECT_ENTITY_EVENT_MONTHLY_AGGREGATION_V1` |
| `ads_research_problem_monthly_metrics.activity_score_method` | `STRING` | 固定`MONTH_CROSS_SECTION_LOG_MAX_NORMALIZED_REWEIGHTED_V1` |
| `ads_research_problem_monthly_metrics.hotspot_score_method` | `STRING` | 固定`ROLLING_3M_WEIGHTED_ACTIVITY_50_30_20_V1` |
| `ads_research_problem_monthly_metrics.observation_start_month/observation_end_month` | `STRING` | 问题连续月份网格起止月 |
| `ads_research_problem_monthly_metrics.coverage_status` | `STRING` | 固定`PARTIAL_REAL_MONTHLY_FACT` |
| `ads_research_problem_monthly_metrics.unavailable_reason` | `STRING` | 引用、资金以及项目日期缺口说明 |

### 41.2 月度分项归一化

对月份`m`中的每个指标`i`，在当月已经进入观测窗口的问题总体中进行`log1p`最大值归一：

```text
component_score(i, problem, month)
  = 100 * ln(1 + value(i, problem, month))
        / ln(1 + max_value(i, month))
```

若当月该指标最大值为0，分项分固定为0。该处理降低单月高计数长尾影响，同时保留同一月份内的问题相对
强度；因此分数用于同月横向比较和单问题连续趋势，不应解释为跨数据版本的绝对物理量。

### 41.3 月度活动分

基础权重为论文30%、专利25%、项目10%、新增人才20%、新增机构15%。令`r`为
`project_date_coverage_rate`，月度活动分为：

```text
activity_score
  = (0.30 * paper_activity_score
     + 0.25 * patent_activity_score
     + 0.10 * r * project_activity_score
     + 0.20 * talent_activity_score
     + 0.15 * institution_activity_score)
    / (0.90 + 0.10 * r)
```

项目日期覆盖不足时，项目贡献和有效权重同步按`r`降低；没有DIRECT项目属于已知零值，`r=1`且项目分为
0。论文、专利、新增人才和新增机构均使用直接证据，不用PROXY关联扩大计数。

### 41.4 月度热度

月度热度对活动分做三个月非对称平滑，突出当前月并抑制单月尖峰：

```text
hotspot_score(month)
  = 0.50 * activity_score(month)
  + 0.30 * activity_score(month - 1)
  + 0.20 * activity_score(month - 2)
```

问题观测初期缺少前1月或前2月时，只对实际存在月份的权重重新归一。例如首月热度等于首月活动分，
第二个月按`0.50/0.80`和`0.30/0.80`计算。`hotspot_score`范围为0—100。

### 41.5 增长率边界

`month_growth_rate=(本月活动分-上月活动分)/上月活动分`；`growth_rate_3m`比较最近三个月与此前三个月
的活动分均值。只有基期活动分或基期三个月均值不低于1时才计算相对增长；前后均为0时写0；基期低于1
而当前为正时写NULL，避免接近零基数产生极端增长倍数。三个月增长还要求前后两个窗口都完整包含3个月。

### 41.6 查询示例

```sql
SELECT
    problem_id,
    statistics_month,
    paper_count,
    patent_count,
    project_count,
    new_talent_count,
    new_institution_count,
    activity_score,
    hotspot_score,
    month_growth_rate,
    growth_rate_3m,
    project_date_coverage_rate,
    project_count_is_lower_bound,
    coverage_status
FROM iceberg.research_problem_ads_v14_20261024
    .ads_research_problem_monthly_metrics
WHERE problem_id = :problem_id
ORDER BY statistics_month;
```

本次实际写入91,520行，覆盖406/406个问题，观测范围1929-03至2026-09；累计论文1,294、专利
10,135、项目228、新增人才11,641、新增机构5,603。`month_growth_rate`有值86,338行，
`growth_rate_3m`有值77,178行。项目覆盖状态按问题为：无DIRECT项目149、日期全部可用4、部分可用44、
完全无可用日期209。活动分范围0—94.982833，月度热度范围0—72.222222。

新发布使用Iceberg `research_problem_ads_v14_20261024`和Doris
`data_version=202610240101`；两端月度表均为91,520行，逻辑Key重复和字段边界异常均为0。

## 42. 专利分析 ADS（6.2.0；6.3.0明细扩展；6.3.1完整交叉矩阵；6.8.0分类扩展；6.9.0全局申请人节点；6.10.0最大覆盖专利机构关系；6.11.0单元格增长趋势）

### 42.1 范围与口径

专利分析v1固定读取Google Patents MVP证据子集，按公开文本（`PUBLICATION`）计数，统计年份使用
`publication_year`，范围为1990—2025。2026是不完整年度，不进入总量、排名和趋势；2020—2022为
对照期，2023—2025为近期窗口。当前正式发布运行ID为
`e4dcc585-a9e4-458e-a646-0c441c3eda76`，`data_version=202610280301`。

“关键词”统一使用Topic，关系类型固定为`CITED_SCIENCE_TOPIC`：从专利连接到其引用的MVP论文，再取
论文的OpenAlex Primary Topic。该关系反映被引科学基础，不等于从专利标题、摘要、权利要求或全文
识别的专利内容主题。逐专利关系保存在Iceberg
`patent_analysis_v1_20261028_r7.dws_patent_topic`，并完整发布到Doris
`ads_patent_analysis_topic_patent`。Topic中文名称固定从
治理入口`iceberg.technology_v2.v_openalex_topic_bilingual`物化；该视图只接收当前最新、已批准的
`zh-Hans/title`治理文本，不从英文名机器猜测中文。

### 42.2 ADS表职责

| 表 | 职责 | 主要限制 |
|---|---|---|
| `ads_patent_analysis_summary` | 总览摘要及领先项、增长项、覆盖率 | 每个运行一行 |
| `ads_patent_analysis_topic` | Topic云、排行、年度与趋势 | 仅`CITED_SCIENCE_TOPIC` |
| `ads_patent_analysis_topic_patent` | Topic点击后的完整专利关系、核心专利代理排名 | 每Topic前100仅表示被引科学证据强度 |
| `ads_patent_analysis_jurisdiction` | CN/US/EP/WO总量、占比、排名与趋势 | EP为区域局，WO为国际体系 |
| `ads_patent_analysis_institution` | 已确认受让机构排行与趋势 | 机构解析覆盖率1.9291% |
| `ads_patent_analysis_institution_edge` | 共同受让机构网络 | 不是一般技术相似、竞争或论文合作关系 |
| `ads_patent_analysis_ipc` | IPC来源代码及A—H部类分布 | 接入IPC 2026.01正式中文名称；历史来源代码仍可能无法匹配 |
| `ads_patent_analysis_inventor` | 来源统一姓名排行与趋势 | Top 10000；尚未解析为平台人才 |
| `ads_patent_analysis_cross_metric` | 全部3,484个Topic × 4辖区的专利数、Jaccard和lift | 完整13,936格；`is_topn_truncated=false` |
| `ads_patent_analysis_cross_year` | 全部Topic × 辖区 × 1990—2025自然年的年度趋势 | 完整501,696格；无专利年份显式保留0 |
| `ads_patent_analysis_coverage` | 各数据域覆盖、未解析量和限制 | 法律状态为`NOT_AVAILABLE` |
| `ads_patent_analysis_classification` | IPC/CPC节点、父级、原文及已审核中文快照 | CPC中文翻译本版本明确排除 |
| `ads_patent_analysis_assignee` | 全局申请人节点、排名及平台机构解析状态 | 名称覆盖94.9828%；未确认名称不冒充平台机构 |
| `ads_patent_analysis_patent_institution` | 专利与全部来源机构节点关系 | 2,767,360条；覆盖1,664,521件专利；保留确认标识 |
| `ads_patent_analysis_topic_cpc` | Topic的CPC技术分支完整分布 | 3,480个Topic有CPC；不做TopN截断 |
| `ads_patent_analysis_topic_assignee` | Topic主要申请人来源名称完整分布 | 名称级覆盖94.9828%，不等同平台机构消歧 |
| `ads_patent_analysis_topic_institution` | Topic主要平台机构 | 仅确认机构映射，覆盖率1.9291% |
| `ads_patent_analysis_jurisdiction_institution` | 公开辖区主要平台机构 | 仅确认机构映射 |
| `ads_patent_analysis_institution_classification` | 机构IPC/CPC技术领域分布 | 仅确认机构映射 |
| `ads_patent_analysis_institution_year` | 机构历年专利趋势 | 仅确认机构映射 |
| `ads_patent_analysis_institution_inventor` | 机构核心发明人来源姓名 | 尚未解析为平台人才 |
| `ads_patent_analysis_ipc_topic` | IPC相关热点Topic完整分布 | 不做TopN截断；Topic为被引科学Topic |
| `ads_patent_analysis_entity_patent` | 辖区、IPC、机构代表专利 | 每实体最多20件；证据代理不代表专利价值 |

所有表均带`metrics_as_of_date`、`metric_definition_version`、`data_version`和`update_time`。范围及原始
派生关系保存在同一Iceberg namespace的`dws_patent_analysis_scope`和`dws_patent_topic`；Doris明细表
持有平台`patent_id`，可直接连接`ads_patent_profile`，不再需要在线连接Iceberg。任务、运行、任务关系、
案例及下载制品元数据保存在PostgreSQL `patent_analysis_*`控制表，不属于ADS事实表。

### 42.3 实际发布与覆盖率

正式范围包含1,752,444件公开文本、1,018,177个Google family。Topic覆盖1,707,255件
（97.4214%），辖区覆盖100%，已确认机构覆盖33,807件（1.9291%），IPC覆盖1,749,187件
（99.8141%），来源发明人姓名覆盖1,666,314件（95.0851%）。法律状态没有可用事实，覆盖为0且状态
固定为`NOT_AVAILABLE`，不得用`grant_date`推断当前有效、失效或在审状态。

当前3,484个Topic均已物化中英文名称，73,122条Topic ADS记录中文名非空率为100%。IPC分类字典
固定`release_id=20260101`，53,085个分析IPC代码中51,121个取得`approved`中文名称；未命中项保持
NULL并通过`mapping_coverage_status`显式标识。CPC共161,825个与分析范围相关的节点，中文名称为0，
本版本未调用大模型翻译。发明人`platform_talent_id`为NULL且
`identity_resolution_status='SOURCE_NAME_ONLY'`。机构关系只发布有直接证据的`CO_ASSIGNEE`边；如需技术
关联、合作或竞争关系，必须新增明确算法、关系类型和证据口径。

Topic主要申请机构提供两种语义：`ads_patent_analysis_topic_assignee`直接使用Google Patents统一申请人
名称，覆盖1,664,521/1,752,444件分析专利（94.9828%）；`ads_patent_analysis_topic_institution`只使用
确认映射到平台机构的记录，仍为33,807件（1.9291%）。前者解决名称级排行覆盖不足，后者保留严格的
平台机构身份，不把名称相似或未经审核的候选关系冒充确认机构。

全局节点和列表必须使用`ads_patent_analysis_assignee`，不能对Topic×申请人表跨Topic求和。该表包含
548,274个申请人节点，排名覆盖1—548,274；其中546,566个`unmatched`、33个`ambiguous`、1,675个
`confirmed`，确认节点连接1,454个平台机构。节点可以用`assignee_name`和`assignee_country_code`
展示，以`patent_count`控制大小并按`assignee_rank`排序；只有`platform_institution_id`非空的确认节点
才允许跳转平台机构画像。

专利—机构节点展示统一读取`ads_patent_analysis_patent_institution`，不得再用确认关系表限制主列表。
该表保留2,767,360条来源关系，覆盖1,664,521件分析专利（94.9828%）：34,115条关系标记
`is_confirmed=true`，其余2,733,245条标记为false并使用`assignee:<assignee_key>`作为稳定节点ID。
所有关系均保留`resolution_status`，消费者可以展示确认状态，但默认节点和关系数量包含全部状态。

`ads_patent_analysis_cross_metric`当前按全部3,484个Topic与CN、US、EP、WO四个辖区生成完整笛卡尔
网格，共13,936行。没有专利命中的2,131个组合仍保留一行并写
`joint_patent_count=0`、`joint_share=0`、`jaccard_score=0`和`lift_score=0`，保证矩阵无缺格。
`is_topn_truncated`固定为false。每个单元格同时物化2020—2022对照期与2023—2025近期窗口的
`baseline_patent_count`、`recent_patent_count`、`patent_count_change`、`growth_rate`和
`trend_direction`。13,936格中UP 2,361、DOWN 5,208、STABLE 551、INSUFFICIENT_EVIDENCE 5,816；
对照期为0时增长率保持NULL，避免制造无穷增长率；两期合计少于5件时趋势方向仍标记为证据不足。

`ads_patent_analysis_cross_year`按3,484个Topic、4个辖区和1990—2025共36个自然年生成完整网格，
共501,696行，其中334,362个零命中年度仍显式保留。表内提供年度专利数、专利族数、辖区年度占比、
上一年专利数、同比增量、同比增长率和趋势方向；160,715行具有可计算的同比增长率。EP是区域专利局、
WO是国际申请体系，不能解释为国家。

### 42.4 `ads_patent_analysis_topic_patent`

一行表示当前分析运行中一个Topic与一件平台专利的关系，逻辑主键为
`run_id, topic_id, patent_id`。正式版本写入4,135,575行，覆盖3,484个Topic和1,707,255件专利；
`patent_id`与`ads_patent_profile`的孤儿关系为0。

| 字段 | Doris类型 | 说明 |
|---|---|---|
| `run_id` | `VARCHAR(64) NOT NULL` | 分析运行ID；逻辑主键之一 |
| `topic_id` | `VARCHAR(64) NOT NULL` | 平台Topic ID；逻辑主键之一 |
| `patent_id` | `VARCHAR(64) NOT NULL` | 平台专利ID；逻辑主键之一，可关联`ads_patent_profile.patent_id` |
| `google_patent_publication_id` | `VARCHAR(128) NOT NULL` | Google来源公开文本ID，仅用于审计 |
| `google_family_id` | `VARCHAR(128)` | Google来源专利族ID |
| `publication_year` | `INT NOT NULL` | 专利公开年 |
| `topic_name_zh`, `topic_name_en` | `STRING` | Topic中英文名称快照；中文非空 |
| `relation_type` | `VARCHAR(32) NOT NULL` | 固定`CITED_SCIENCE_TOPIC` |
| `topic_rank_in_patent` | `BIGINT NOT NULL` | Topic在单件专利内的被引论文证据排名 |
| `relation_weight` | `DECIMAL(18,12) NOT NULL` | 该Topic证据论文数占该专利全部Topic证据论文数的比例 |
| `evidence_work_count` | `BIGINT NOT NULL` | 支撑专利—Topic关系的去重被引论文数 |
| `primary_evidence_work_count` | `BIGINT NOT NULL` | Primary Topic证据论文数；本版本关系均由Primary Topic生成 |
| `avg_topic_score`, `max_topic_score` | `DECIMAL(18,8)` | 证据论文中该Topic分数的平均值和最大值 |
| `evidence_count` | `BIGINT NOT NULL` | 上游专利—论文证据计数合计 |
| `is_primary` | `BOOLEAN NOT NULL` | 是否为该专利证据排名第一的Topic |
| `core_patent_rank` | `BIGINT NOT NULL` | 专利在Topic内的证据强度稳定排名 |
| `is_core_patent` | `BOOLEAN NOT NULL` | `core_patent_rank<=100`时为true |
| `ranking_method` | `VARCHAR(64) NOT NULL` | 固定`CITED_SCIENCE_EVIDENCE_V1` |
| `metrics_as_of_date` | `DATE NOT NULL` | 来源指标统计截止日 |
| `metric_definition_version` | `VARCHAR(64) NOT NULL` | 专利分析指标口径版本 |
| `data_version` | `BIGINT NOT NULL` | 当前正式版本`202610280301` |
| `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

`core_patent_rank`依次按`evidence_work_count`、`primary_evidence_work_count`、`max_topic_score`、
`relation_weight`、`publication_year`降序，再按`patent_id`稳定排序。它只衡量专利与被引科学Topic的
证据强度，不表示法律稳定性、专利价值、技术先进性、市场价值或专家认定。

```sql
SELECT r.patent_id,p.title,p.abstract_zh,p.abstract_en,p.publication_date,p.grant_date,
       p.inventors,p.assignees,p.ipc_codes,r.core_patent_rank,
       r.evidence_work_count,r.relation_weight
FROM ads_patent_analysis_topic_patent r
JOIN ads_patent_profile p ON p.patent_id=r.patent_id
WHERE r.run_id='e4dcc585-a9e4-458e-a646-0c441c3eda76'
  AND r.topic_id=:topic_id AND r.is_core_patent=true
ORDER BY r.core_patent_rank;
```

### 42.5 6.8.0—6.11.0新增表实际行数

| 表 | Iceberg / Doris行数 | 支持范围 |
|---|---:|---|
| `ads_patent_analysis_classification` | 214,910 | IPC 53,085；CPC 161,825 |
| `ads_patent_analysis_assignee` | 548,274 | 全局申请人节点；名称级覆盖94.9828% |
| `ads_patent_analysis_patent_institution` | 2,767,360 | 覆盖1,664,521件专利；覆盖率94.9828% |
| `ads_patent_analysis_cross_year` | 501,696 | 3,484个Topic × 4个辖区 × 36年完整趋势网格 |
| `ads_patent_analysis_topic_cpc` | 5,236,443 | 3,480个Topic；完整分布 |
| `ads_patent_analysis_topic_assignee` | 2,400,215 | 3,473个Topic；531,094个规范申请人Key全部命中全局申请人表 |
| `ads_patent_analysis_topic_institution` | 22,552 | Topic×确认机构 |
| `ads_patent_analysis_jurisdiction_institution` | 2,492 | 辖区×确认机构 |
| `ads_patent_analysis_institution_classification` | 162,540 | 确认机构×IPC/CPC |
| `ads_patent_analysis_institution_year` | 5,269 | 确认机构年度趋势 |
| `ads_patent_analysis_institution_inventor` | 26,379 | 确认机构×来源发明人姓名 |
| `ads_patent_analysis_ipc_topic` | 2,482,356 | IPC×Topic完整分布 |
| `ads_patent_analysis_entity_patent` | 633,456 | 辖区80、IPC625,515、机构7,861；每实体最多20件 |

### 42.6 发布与验证

```bash
uv run --frozen alembic upgrade head
./scripts/publish_patent_analysis_v1.sh
uv run --frozen pytest -q tests/test_patent_analysis.py
```

发布链路采用固定Snapshot、隔离Iceberg namespace、逐表逻辑Key校验、Iceberg—Doris行数对账以及
PostgreSQL任务状态更新。实际结果和检查见
[`reports/patent_analysis_v1/post_run_verification.md`](reports/patent_analysis_v1/post_run_verification.md)。

## 43. 深圳GKX产业集群ADS（6.5.0）

本组表使用`ads_sz_gkx_industry_*`前缀，属于独立分类体系，不修改或覆盖`ads_industry`、学科Topic、
论文、专利及既有产业关系。全量成果关系保留在Iceberg DWS；Doris只发布集群画像和两级映射。

### 43.1 `ads_sz_gkx_industry_cluster`

一行一个集群，逻辑主键为`cluster_code`。保存集群名称、组别、产业名称数组、Subfield/Topic数、去重
论文/专利数以及分数计数。专利数只表示`CITED_SCIENCE_TOPIC`被引科学基础关联，不表示专利内容产业。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `cluster_code` | `VARCHAR(32) NOT NULL` | 来源稳定集群编码；逻辑主键，例如`CL-SEI-01` |
| 集群快照 | `cluster_name_zh` | `VARCHAR(256) NOT NULL` | 集群中文名称；仅用于展示，不作为身份键 |
| 集群快照 | `cluster_note_zh` | `VARCHAR(512)` | CSV括号说明；来源缺失时为NULL |
| 集群快照 | `group_name` | `VARCHAR(32) NOT NULL` | 来源组别，当前为`战新`或`未来` |
| 产业成员 | `industry_names` | `ARRAY<STRING> NOT NULL` | 集群内产业名称去重、稳定排序数组；不使用来源产业编码建立身份 |
| 产业成员 | `industry_member_count` | `BIGINT NOT NULL` | DWD中该集群的来源成员行数；保留来源重复名称行，因此可大于`industry_names`长度 |
| 映射覆盖 | `subfield_count` | `BIGINT NOT NULL` | 已批准Cluster—Subfield关系数 |
| 映射覆盖 | `topic_count` | `BIGINT NOT NULL` | 由已批准Subfield关系继承的去重Topic关系数 |
| 论文关联 | `paper_count` | `BIGINT NOT NULL` | `dws_sz_gkx_industry_cluster_paper`中该集群的去重MVP core论文数 |
| 论文关联 | `fractional_paper_count` | `DECIMAL(20,8) NOT NULL` | 论文跨命中集群按最大映射权重归一后的分数计数之和；同一论文跨全部集群权重合计为1 |
| 专利关联 | `patent_count` | `BIGINT NOT NULL` | 通过`CITED_SCIENCE_TOPIC`关联到该集群的去重平台专利数 |
| 专利关联 | `fractional_patent_count` | `DECIMAL(20,8) NOT NULL` | 单件专利按Topic证据权重与集群映射权重计算并跨集群归一后的分数计数之和 |
| 发布版本 | `cluster_release_id` | `VARCHAR(64) NOT NULL` | 不可变产业集群来源发布ID |
| 发布版本 | `mapping_release_id` | `VARCHAR(64) NOT NULL` | 不可变Cluster—Subfield/Topic映射发布ID |
| 统计版本 | `metric_definition_version` | `VARCHAR(64) NOT NULL` | 聚合与成果传播算法版本，当前为`sz_gkx_industry_subfield_inheritance_v1` |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 当前状态行的单调数据版本 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

9.12.0在本表原地补充2021—2025年度发展方案，不建立平行集群主表，也不修改DWD、DWS、来源CSV或
既有Iceberg对象。每个集群固定包含5个年度；每年固定3项发展目标、5项具体任务和4项保障措施。首版
覆盖15个集群、75个集群—年度、225项目标、375项任务和300项保障措施。内容由大模型根据现有集群、
产业成员、Subfield和代表Topic上下文构造，只用于完整展示，不是真实政策、历史事实或实施成效。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| 年度方案 | `annual_plan_year_count` | `INT` | 固定为5；对应2021、2022、2023、2024、2025 |
| 年度方案 | `annual_development_plan` | `JSON` | 根对象含集群快照及5个年度；每年保存数量和完整目标、任务、保障措施数组 |
| 生成治理 | `annual_plan_release_id` | `VARCHAR(96)` | 年度方案不可变发布ID |
| 生成治理 | `annual_plan_model` | `VARCHAR(128)` | 实际生成模型名称 |
| 生成治理 | `annual_plan_prompt_version` | `VARCHAR(64)` | 结构化生成Prompt版本 |
| 生成治理 | `annual_plan_input_hash` | `CHAR(64)` | 集群、产业、学科和Topic模型输入SHA-256 |
| 生成治理 | `annual_plan_value_nature` | `VARCHAR(32)` | 首版固定`LLM_SYNTHETIC`，明确为大模型构造值 |
| 生成治理 | `annual_plan_review_status` | `VARCHAR(64)` | 首版固定`APPROVED_FOR_SHOWCASE_BY_OPERATOR_RULE` |
| 生成治理 | `annual_plan_version` | `BIGINT` | 年度方案单调数据版本 |
| 生成治理 | `annual_plan_update_time` | `DATETIME(3)` | 年度方案发布时间 |

在线迁移先增加可空物理列，发布验收要求上述10个字段在全部15行均有值；JSON内部禁止`null`、空字符串、
空数组、`待补充`、`暂无`等占位内容。年度数组必须严格按2021至2025排列，数量字段必须与数组长度一致，
条目序号必须从1连续编号。原有17个集群画像、计数、版本字段在发布前后执行全量Hash保护，不得随本次
展示数据补充发生变化。

`paper_count`和`patent_count`分别在各集群内去重，但同一成果可以进入多个集群，不能跨集群直接求和
解释为全局去重成果数。需要可加总口径时使用对应`fractional_*_count`；分数计数用于归属分摊，不表示
成果质量、产业贡献、经济价值或因果影响。

### 43.2 `ads_sz_gkx_industry_cluster_subfield`

一行一个集群—Subfield关系，逻辑主键为`cluster_code, subfield_id`。关系类型为
`CORE/SUPPORTING/APPLICATION`，固定规则按操作方授权直接发布为`approved`。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `cluster_code` | `VARCHAR(32) NOT NULL` | 产业集群稳定编码；逻辑主键之一 |
| Key | `subfield_id` | `VARCHAR(64) NOT NULL` | 平台统一Subfield ID；逻辑主键之一，可关联`ads_discipline_subfield.subfield_id` |
| 集群快照 | `cluster_name_zh` | `VARCHAR(256) NOT NULL` | 集群中文名称快照 |
| 来源身份 | `openalex_subfield_id` | `VARCHAR(32) NOT NULL` | OpenAlex来源Subfield ID，只用于来源审计 |
| 学科快照 | `subfield_name_zh` | `VARCHAR(512) NOT NULL` | 已发布Subfield中文名称快照 |
| 学科快照 | `subfield_name_en` | `VARCHAR(512)` | Subfield英文或来源原始名称快照 |
| 关系语义 | `relation_type` | `VARCHAR(32) NOT NULL` | `CORE`核心范围、`SUPPORTING`支撑范围或`APPLICATION`应用范围 |
| 关系语义 | `mapping_weight` | `DECIMAL(9,6) NOT NULL` | 固定映射权重：`CORE=1.0`、`SUPPORTING=0.65`、`APPLICATION=0.45` |
| 映射治理 | `mapping_method` | `VARCHAR(64) NOT NULL` | 当前固定`FIXED_SUBFIELD_RULE_AUTO_APPROVED` |
| 映射治理 | `review_status` | `VARCHAR(24) NOT NULL` | 当前固定`approved`；依据操作方对本发布规则的批量自动批准授权 |
| 发布版本 | `cluster_release_id` | `VARCHAR(64) NOT NULL` | 不可变产业集群来源发布ID |
| 发布版本 | `mapping_release_id` | `VARCHAR(64) NOT NULL` | 不可变映射发布ID；规则变化必须使用新值 |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 当前状态行的单调数据版本 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

同一Subfield可以关联多个集群；同一集群也可以关联多个Subfield。`mapping_weight`只用于本体系内成果
跨集群分摊，不是模型置信度、人工评分、产业相关概率或Subfield内部Topic的质量权重。

### 43.3 `ads_sz_gkx_industry_cluster_topic`

一行一个集群—Topic关系，逻辑主键为`cluster_code, topic_id`。Topic严格继承已发布Subfield关系，
保存OpenAlex来源ID、平台ID、中英文名、所属Subfield、关系类型、权重及不可变映射版本。

| 字段组 | 字段 | Doris类型 | 说明 |
|---|---|---|---|
| Key | `cluster_code` | `VARCHAR(32) NOT NULL` | 产业集群稳定编码；逻辑主键之一 |
| Key | `topic_id` | `VARCHAR(64) NOT NULL` | 平台统一Topic ID；逻辑主键之一，可关联`ads_discipline_topic.topic_id` |
| 集群快照 | `cluster_name_zh` | `VARCHAR(256) NOT NULL` | 集群中文名称快照 |
| 来源身份 | `openalex_topic_id` | `VARCHAR(32) NOT NULL` | OpenAlex来源Topic ID，只用于来源审计 |
| Topic快照 | `topic_name_zh` | `VARCHAR(512) NOT NULL` | 已发布Topic中文名称快照 |
| Topic快照 | `topic_name_en` | `VARCHAR(512)` | Topic英文或来源原始名称快照 |
| 父级学科 | `subfield_id` | `VARCHAR(64) NOT NULL` | 平台统一Subfield ID，可关联`ads_discipline_subfield.subfield_id` |
| 父级学科 | `openalex_subfield_id` | `VARCHAR(32) NOT NULL` | Topic来源记录所属的OpenAlex Subfield ID |
| 关系语义 | `relation_type` | `VARCHAR(32) NOT NULL` | 原样继承Cluster—Subfield的`CORE/SUPPORTING/APPLICATION` |
| 关系语义 | `mapping_weight` | `DECIMAL(9,6) NOT NULL` | 原样继承Cluster—Subfield固定权重 |
| 产业链位置 | `industry_chain_stage` | `VARCHAR(16) NOT NULL` | Topic在当前集群中的位置：`UPSTREAM/MIDSTREAM/DOWNSTREAM`；不是Topic全局属性 |
| 映射治理 | `mapping_method` | `VARCHAR(64) NOT NULL` | 当前固定`SUBFIELD_INHERITANCE_AUTO_APPROVED` |
| 映射治理 | `review_status` | `VARCHAR(24) NOT NULL` | 当前固定`approved`；不是逐Topic人工审核结果 |
| 发布版本 | `cluster_release_id` | `VARCHAR(64) NOT NULL` | 不可变产业集群来源发布ID |
| 发布版本 | `mapping_release_id` | `VARCHAR(64) NOT NULL` | 不可变映射发布ID，与父级Subfield关系一致 |
| 公共版本 | `data_version` | `BIGINT NOT NULL` | 当前状态行的单调数据版本 |
| 公共版本 | `update_time` | `DATETIME(3) NOT NULL` | UTC生成时间 |

本表不是逐Topic语义模型或专家判断结果。只要Topic属于已映射Subfield，就继承对应集群关系；因此适合
产业集群范围召回和下游候选筛选，精度低于逐Topic审核。完整论文、专利关系分别查询Iceberg
`dws_sz_gkx_industry_cluster_paper`和`dws_sz_gkx_industry_cluster_patent`，不在Doris重复保存全量明细。

产业链位置使用固定、互斥且完整的确定性映射：

```text
relation_type='SUPPORTING'  -> industry_chain_stage='UPSTREAM'
relation_type='CORE'        -> industry_chain_stage='MIDSTREAM'
relation_type='APPLICATION' -> industry_chain_stage='DOWNSTREAM'
```

`UPSTREAM`表示基础材料、基础科学或使能技术，`MIDSTREAM`表示集群核心研发、工程或制造范围，
`DOWNSTREAM`表示应用与服务场景。标签继承Cluster—Subfield关系，因此同一Topic在不同集群中可以具有
不同产业链位置；不得脱离`cluster_code`单独解释或汇总为Topic的唯一产业链属性。

发布入口：

```bash
./scripts/compose.sh up -d --wait --wait-timeout 300
./scripts/publish_sz_gkx_industry_v1.sh
```

## 44. 人员能力与深圳基础研究问题匹配 ADS（6.22.0）

本组表只对`ads_research_problem_institution`中能够连接确认、有效深圳机构的问题发布人才匹配。
深圳使用稳定Location ID `loc_E16782C21F18EBF8A59C1E98F9C9860B`判定，不按名称模糊搜索。
当前范围为163个问题、642条问题—深圳机构关系和65家机构；问题侧1,695条Topic关系完整映射到865个
平台Topic，映射缺失为0。人才论文和Topic严格使用2000—2025完整自然年，政治倾向因无来源数据按
业务规则统一为50分并参与综合评分，同时以`NO_DATA_DEFAULT_AVERAGE`披露无证据状态。

### 44.1 `ads_talent_capability_model`

一行一个不可变评分模型版本，逻辑Key为`model_version`。权重或阈值变化必须发布新版本。

| 字段 | 类型 | 说明 |
|---|---|---|
| `model_version` | `VARCHAR(64) NOT NULL` | 人员能力综合评分模型版本 |
| `model_name` | `VARCHAR(256) NOT NULL` | 模型中文名称 |
| `assessment_scope` | `VARCHAR(64) NOT NULL` | 适用范围；当前`SHENZHEN_RESEARCH_PROBLEM` |
| `window_start_year/window_end_year` | `SMALLINT NOT NULL` | 完整论文观察窗，当前2000和2025 |
| `research_perseverance_weight` | `DECIMAL(9,6) NOT NULL` | 科研毅力综合权重，当前0.25 |
| `innovation_capability_weight` | `DECIMAL(9,6) NOT NULL` | 创新能力综合权重，当前0.25 |
| `discipline_match_weight` | `DECIMAL(9,6) NOT NULL` | 学科匹配度综合权重，当前0.40 |
| `political_orientation_weight` | `DECIMAL(9,6) NOT NULL` | 政治倾向综合权重，当前0.10 |
| `political_orientation_default_score` | `DECIMAL(9,6) NOT NULL` | 无数据时统一平均分，当前50 |
| `minimum_topic_paper_count` | `BIGINT NOT NULL` | 候选Topic最低论文数，当前3 |
| `minimum_topic_volume_score` | `DECIMAL(9,6) NOT NULL` | 合格Topic最低论文量百分位，当前50 |
| `minimum_topic_expertise_score` | `DECIMAL(9,6) NOT NULL` | 合格Topic最低专业水平分，当前60 |
| `strong_topic_paper_count` | `BIGINT NOT NULL` | 强Topic最低论文数，当前5 |
| `strong_topic_expertise_score` | `DECIMAL(9,6) NOT NULL` | 强Topic最低专业水平分，当前75 |
| `minimum_problem_weight_coverage` | `DECIMAL(9,6) NOT NULL` | 合格Topic最低问题权重覆盖，当前0.30 |
| `minimum_discipline_match_score` | `DECIMAL(9,6) NOT NULL` | 最低学科匹配度，当前60 |
| `overall_score_formula` | `STRING NOT NULL` | 四维综合评分公式文本 |
| `source_snapshot_ids` | `JSON NOT NULL` | 论文、Topic、问题、机构和映射固定输入版本 |
| `model_status` | `VARCHAR(32) NOT NULL` | `ACTIVE/DRAFT/RETIRED`，当前ACTIVE |
| `metrics_as_of_date` | `DATE NOT NULL` | 指标统计截止日 |
| `data_version/update_time` | `BIGINT/DATETIME(3) NOT NULL` | 数据版本和UTC生成时间 |

### 44.2 `ads_talent_capability_assessment`

保存一名人才一个固定值的科研毅力、创新能力、全部问题总学科匹配度、政治倾向和人才级综合分；
问题级学科匹配度查询§44.5。逻辑Key为`talent_id, model_version`。

| 字段组 | 字段 | 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id/model_version` | `VARCHAR NOT NULL` | 人才ID和模型版本 |
| 科研毅力 | `eligible_paper_count` | `BIGINT NOT NULL` | 2000—2025去重论文数 |
| 科研毅力 | `first_paper_year` | `SMALLINT` | 观察窗内首篇论文年 |
| 科研毅力 | `observation_year_count` | `INT NOT NULL` | `2025-first_paper_year+1` |
| 科研毅力 | `active_year_count` | `INT NOT NULL` | 至少发表一篇论文的年份数 |
| 科研毅力 | `active_year_ratio` | `DECIMAL(9,6) NOT NULL` | 活跃年份数/观察年数 |
| 科研毅力 | `longest_active_year_streak` | `INT NOT NULL` | 最长连续发表年份数 |
| 科研毅力 | `longest_active_year_streak_ratio` | `DECIMAL(9,6) NOT NULL` | 最长连续活跃年数/观察年数 |
| 科研毅力 | `paper_count_percentile_score` | `DECIMAL(9,6) NOT NULL` | 论文数固定总体平均并列百分位分 |
| 科研毅力 | `active_year_ratio_score` | `DECIMAL(9,6) NOT NULL` | 活跃年份比例百分位分 |
| 科研毅力 | `active_streak_ratio_score` | `DECIMAL(9,6) NOT NULL` | 连续活跃比例百分位分 |
| 科研毅力 | `research_perseverance_score` | `DECIMAL(9,6) NOT NULL` | `0.50*论文量+0.30*活跃年份+0.20*连续活跃` |
| 创新能力 | `distinct_topic_count` | `BIGINT NOT NULL` | 2000—2025论文的去重Topic数 |
| 创新能力 | `effective_topic_count` | `DECIMAL(18,8) NOT NULL` | `exp(-sum(p_t*ln(p_t)))`，`p_t`为Topic论文计数份额 |
| 创新能力 | `primary_field_id` | `VARCHAR(64)` | Topic论文计数最多的Field；并列按ID |
| 创新能力 | `paper_count_band` | `VARCHAR(32) NOT NULL` | `1_5/6_10/11_20/21_50/51_100/100_PLUS` |
| 创新能力 | `topic_count_percentile_score` | `DECIMAL(9,6) NOT NULL` | 同主要Field和论文规模组Topic数百分位 |
| 创新能力 | `effective_topic_percentile_score` | `DECIMAL(9,6) NOT NULL` | 同组有效Topic数百分位 |
| 创新能力 | `innovation_capability_score` | `DECIMAL(9,6) NOT NULL` | `0.70*Topic数分+0.30*有效Topic数分` |
| 政治倾向 | `political_orientation_score` | `DECIMAL(9,6) NOT NULL` | 当前所有人才固定50 |
| 政治倾向 | `political_orientation_status` | `VARCHAR(64) NOT NULL` | 当前`NO_DATA_DEFAULT_AVERAGE` |
| 总学科匹配 | `problem_count` | `BIGINT NOT NULL` | 总分分母；当前固定163个深圳相关问题 |
| 总学科匹配 | `candidate_problem_count` | `BIGINT NOT NULL` | 至少有一个3篇论文候选Topic的问题数 |
| 总学科匹配 | `qualified_problem_count` | `BIGINT NOT NULL` | 通过全部问题匹配门槛的问题数 |
| 总学科匹配 | `problem_coverage_ratio` | `DECIMAL(9,6) NOT NULL` | `candidate_problem_count/problem_count` |
| 总学科匹配 | `discipline_match_score` | `DECIMAL(9,6) NOT NULL` | 163个问题级学科匹配度等权平均；缺失问题按0 |
| 总学科匹配 | `best_problem_id` | `VARCHAR(256)` | 问题级学科匹配度最高的问题；并列按问题ID |
| 总学科匹配 | `best_problem_match_score` | `DECIMAL(9,6) NOT NULL` | 最佳问题学科匹配度；无候选为0 |
| 综合 | `overall_score` | `DECIMAL(9,6) NOT NULL` | 25%毅力+25%创新+40%总学科匹配+10%政治倾向 |
| 综合 | `overall_rank` | `BIGINT NOT NULL` | 固定人才总体内人才级综合分稳定排名 |
| 治理 | `benchmark_talent_count` | `BIGINT NOT NULL` | 科研毅力固定基准总体人数 |
| 治理 | `assessment_status` | `VARCHAR(32) NOT NULL` | 当前发布合格行为COMPLETE |
| 来源 | `paper_snapshot_id/topic_snapshot_id` | `VARCHAR(128) NOT NULL` | 固定论文和Topic输入标识 |
| 版本 | `metrics_as_of_date/data_version/update_time` | `DATE/BIGINT/DATETIME(3)` | 统计截止日、版本和UTC生成时间 |

人才级总学科匹配度明确使用全部163个问题作为等权分母：

```text
discipline_match_score(talent)
  = sum(discipline_match_score(talent, problem), all 163 problems) / 163
```

没有生成问题候选行的组合按0计。该分数衡量人才对深圳相关基础研究问题集合的整体覆盖，不替代
`best_problem_match_score`和具体问题匹配结果；专长集中人才的总分可能较低，但其最佳问题分仍可很高。

### 44.3 `ads_talent_capability_dimension_metric`

前端点击评分维度时读取。一行是一项确定性指标，逻辑Key为
`talent_id, model_version, dimension_code, metric_code`。

| 字段 | 类型 | 说明 |
|---|---|---|
| `talent_id/model_version` | `VARCHAR NOT NULL` | 人才ID和模型版本 |
| `dimension_code` | `VARCHAR(64) NOT NULL` | `RESEARCH_PERSEVERANCE/INNOVATION_CAPABILITY/POLITICAL_ORIENTATION` |
| `metric_code` | `VARCHAR(64) NOT NULL` | 维度内稳定指标代码 |
| `dimension_name/metric_name` | `VARCHAR NOT NULL` | 需求名称和详细指标中文名 |
| `raw_value` | `DECIMAL(24,8)` | 原始值；政治倾向因无证据为NULL |
| `normalized_score` | `DECIMAL(9,6) NOT NULL` | 标准化分或政治倾向固定分 |
| `metric_weight` | `DECIMAL(9,6) NOT NULL` | 指标在所属维度内权重 |
| `weighted_contribution` | `DECIMAL(12,8) NOT NULL` | `normalized_score*metric_weight` |
| `calculation_method` | `VARCHAR(128) NOT NULL` | 稳定计算方法代码 |
| `calculation_description` | `STRING NOT NULL` | 公式、基准和解释边界 |
| `evidence_count` | `BIGINT NOT NULL` | 支撑论文、年份或Topic数；政治倾向为0 |
| `metric_status` | `VARCHAR(64) NOT NULL` | `CALCULATED/NO_DATA_DEFAULT_AVERAGE` |
| `metrics_as_of_date/data_version/update_time` | 多类型 | 公共统计与版本字段 |

### 44.4 `ads_talent_research_problem_discipline_match_topic`

只保存人才在问题Topic下至少3篇论文的候选证据，不把单篇偶然命中物化为匹配。问题的OpenAlex Topic
先经`ads_discipline_topic.openalex_topic_id`映射为平台`topic_id`。逻辑Key为
`talent_id, problem_id, topic_id, match_model_version`。

| 字段组 | 字段 | 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id/problem_id/topic_id/match_model_version` | `VARCHAR NOT NULL` | 人才、问题、平台Topic和模型版本 |
| 身份 | `source_openalex_topic_id` | `VARCHAR(64) NOT NULL` | 问题与论文共同使用的来源Topic ID |
| 展示 | `topic_name_zh/topic_name_en/field_id` | 多类型 | Topic中英文名和Field快照 |
| 问题 | `is_leading_topic` | `BOOLEAN NOT NULL` | 是否为问题Leading Topic |
| 问题 | `evidence_work_count/primary_work_count` | `BIGINT NOT NULL` | 问题Topic证据论文和Primary论文数 |
| 问题 | `problem_topic_weight` | `DECIMAL(18,12) NOT NULL` | 问题内归一化Topic重要性 |
| 人才 | `talent_topic_paper_count` | `BIGINT NOT NULL` | 人才2000—2025该Topic去重论文数 |
| 人才 | `talent_topic_citation_count` | `BIGINT NOT NULL` | 上述论文当前非负累计被引之和 |
| 人才 | `talent_topic_citation_per_paper` | `DECIMAL(18,8) NOT NULL` | 篇均累计引用，存在年龄效应 |
| 人才 | `talent_topic_leadership_paper_count` | `BIGINT NOT NULL` | 第一作者或通讯作者论文并集去重数 |
| 人才 | `talent_topic_leadership_ratio` | `DECIMAL(9,6) NOT NULL` | 领导力论文数/Topic论文数 |
| 人才 | `talent_topic_recent_5y_paper_count` | `BIGINT NOT NULL` | 2021—2025该Topic去重论文数 |
| 分项 | `topic_paper_volume_score` | `DECIMAL(9,6) NOT NULL` | 同Topic论文数平均并列百分位分 |
| 分项 | `topic_citation_impact_score` | `DECIMAL(9,6) NOT NULL` | 同Topic篇均引用百分位分 |
| 分项 | `topic_leadership_score` | `DECIMAL(9,6) NOT NULL` | 同Topic领导力比例百分位分 |
| 分项 | `topic_recent_activity_score` | `DECIMAL(9,6) NOT NULL` | 同Topic近五年论文比例百分位分 |
| 分项 | `topic_expertise_score` | `DECIMAL(9,6) NOT NULL` | `0.45*论文量+0.30*引用+0.15*领导力+0.10*近期活跃` |
| 门槛 | `minimum_paper_threshold` | `BIGINT NOT NULL` | 候选最低论文数，当前3 |
| 门槛 | `minimum_expertise_threshold` | `DECIMAL(9,6) NOT NULL` | 合格最低专业分，当前60 |
| 结果 | `is_qualified_topic` | `BOOLEAN NOT NULL` | 同时满足论文量分不低于50且专业分不低于60 |
| 结果 | `is_strong_topic` | `BOOLEAN NOT NULL` | 论文数至少5且专业分至少75 |
| 结果 | `weighted_match_contribution` | `DECIMAL(18,12) NOT NULL` | 合格时`problem_topic_weight*topic_expertise_score`，否则0 |
| 结果 | `qualification_reason` | `VARCHAR(128) NOT NULL` | `STRONG/QUALIFIED/LOW_VOLUME_PERCENTILE/LOW_EXPERTISE` |
| 版本 | `metrics_as_of_date/data_version/update_time` | 多类型 | 公共统计与版本字段 |

问题Topic权重使用：

```text
importance_raw = ln(1 + evidence_work_count + 2 * primary_work_count)
               * (is_leading_topic ? 1.25 : 1.00)
problem_topic_weight = importance_raw / sum(importance_raw within problem)
```

### 44.5 `ads_talent_research_problem_discipline_match`

一名人才与一个深圳相关基础研究问题一行，是匹配列表、排名和报告主表。逻辑Key为
`talent_id, problem_id, match_model_version`。

| 字段组 | 字段 | 类型 | 说明 |
|---|---|---|---|
| Key | `talent_id/problem_id/match_model_version` | `VARCHAR NOT NULL` | 人才、问题和模型版本 |
| 范围 | `is_shenzhen_related_problem` | `BOOLEAN NOT NULL` | 是否由确认深圳机构关系进入范围；当前均TRUE |
| 范围 | `shenzhen_institution_count` | `BIGINT NOT NULL` | 该问题关联去重深圳机构数 |
| 问题 | `problem_topic_count/leading_topic_count` | `BIGINT NOT NULL` | 问题全部Topic和Leading Topic数 |
| 候选 | `candidate_topic_count` | `BIGINT NOT NULL` | 人才至少3篇论文的候选问题Topic数 |
| 合格 | `qualified_topic_count/strong_topic_count` | `BIGINT NOT NULL` | 合格和强匹配Topic数 |
| 合格 | `qualified_leading_topic_count/strong_leading_topic_count` | `BIGINT NOT NULL` | 合格和强匹配Leading Topic数 |
| 覆盖 | `candidate_topic_weight_coverage` | `DECIMAL(9,6) NOT NULL` | 候选Topic覆盖的问题权重 |
| 覆盖 | `qualified_topic_weight_coverage` | `DECIMAL(9,6) NOT NULL` | 合格Topic覆盖的问题权重 |
| 学科匹配度 | `discipline_match_score` | `DECIMAL(9,6) NOT NULL` | `sum(problem_topic_weight*合格Topic专业分)` |
| 排名 | `match_rank` | `BIGINT NOT NULL` | 问题内合格优先、学科匹配度降序、人才ID升序的稳定排名 |
| 门槛 | `has_strong_leading_topic` | `BOOLEAN NOT NULL` | 是否有强匹配Leading Topic |
| 门槛 | `is_eligible_match` | `BOOLEAN NOT NULL` | 是否通过联合推荐门槛 |
| 状态 | `match_status` | `VARCHAR(64) NOT NULL` | `QUALIFIED/BELOW_EXPERTISE_THRESHOLD/INSUFFICIENT_EVIDENCE` |
| 状态 | `eligibility_reason` | `STRING NOT NULL` | 通过或失败原因 |
| 来源 | `problem_snapshot_id/talent_topic_snapshot_id/topic_mapping_version` | `VARCHAR NOT NULL` | 问题、人才Topic和映射输入版本 |
| 版本 | `metrics_as_of_date/data_version/update_time` | 多类型 | 公共统计与版本字段 |

人才只有满足以下全部条件才标记`is_eligible_match=true`：

```text
(strong_leading_topic_count >= 1 OR qualified_topic_count >= 2)
AND qualified_topic_weight_coverage >= 0.30
AND discipline_match_score >= 60
```

### 44.6 实际发布、查询与边界

当前发布`model_version='talent_problem_match_shenzhen_v1'`、`data_version=202610311200`：人才能力
99,996行、维度解释599,976行、Topic匹配证据2,059,636行、人才—问题候选1,142,501行；7,949行
通过门槛，覆盖148个问题和5,351名人才。其余15个问题没有人才通过当前严格门槛，应展示“暂无达到
当前论文水平阈值的人才”，不得自动降低阈值或把候选冒充合格匹配。

完整开发查询、导出字段和解释边界见
[`docs/talent_problem_match_shenzhen_v1.md`](docs/talent_problem_match_shenzhen_v1.md)。发布入口：

```bash
./scripts/compose.sh up -d --wait --wait-timeout 300
./scripts/publish_talent_problem_match_shenzhen_v1.sh
uv run --frozen pytest -q tests/test_talent_problem_match.py
```

## 45. 深圳科研资源短板与趋势

6.25.0新增四张表，服务深圳与固定科技发达城市同行组的Subfield资源比较、趋势节点下钻、机构筛选和
关键短板标注。固定版本`cn_advanced_city_10_v1_20261031`包含北京、上海、深圳、广州、杭州、南京、
武汉、成都、西安和苏州；深圳城市基准严格排除深圳自身，使用其余九城等权均值。正式比较只覆盖
2015—2025完整自然年；截至2026-09-18的2026部分年度不进入短板表。

### 45.1 `ads_resource_benchmark_city`

一行一个基准版本内城市，逻辑Key为`benchmark_version, city_location_id`。`is_target_city`只对深圳为真，
`is_peer_city`只对其余九城为真；`benchmark_weight`v1固定为1。名单、位置ID、纳入原因和有效年度全部
版本化，不得在发布SQL内用城市名称临时匹配或原地改变历史版本。

### 45.2 `ads_city_subfield_resource_yearly`

逻辑Key为`city_location_id, statistics_year, subfield_id`，固定发布10城×11年×252个Subfield完整网格。
`paper_count`为城市全计数，`paper_fractional_count`按同一论文涉及的基准城市数等权分配；正式论文差距
使用后者。`publication_cohort_cited_by_count`表示当年发表论文截至指标日累计被引，`citation_count`
表示固定MVP论文在该自然年新收到的引用分数计数，两者不得混用。`talent_count`直接按城市、年度、
Subfield、来源人才ID去重，不从Topic人才数求和。

项目金额按全部项目机构关系的`evidence_paper_count`分配，全部证据为0时等分；先纳入跨城机构分母，
再汇总到基准城市。产品统一读取`funding_amount_cny`，不区分真实和模拟金额：已有正人民币金额直接
使用；缺失金额以固定中位数581,984.8125元乘项目ID确定性0.8000—1.2000系数估算。每个进入年度、
Primary Topic、Subfield和十城机构范围的项目都参与金额计算，`funding_amount_project_count`必须等于
`project_count`且`funding_amount_coverage_rate=1`。`funding_amount_source`使用
`SOURCE_ONLY/ESTIMATED_ONLY/MIXED/NO_PROJECT`披露来源构成，`funding_amount_method`固定保存算法版本。
原`real_funding_cny/simulated_funding_cny`仅保留历史审计，不作为产品查询或短板判定字段。统一金额仍
表示项目关联分配值，不是实际拨款、到账、承担额或地方财政投入。

### 45.3 `ads_institution_subfield_resource_yearly`

逻辑Key为`institution_id, statistics_year, subfield_id`。十城有论文、引用或人才证据的机构发布观察行；
深圳机构额外补齐全部年度和Subfield零值网格，使完全没有某学科证据的机构也可被筛选和识别。论文、
年度新增引用、人才和资金语义与城市表一致；机构比较按`institution_type_id + statistics_year +
subfield_id`建立九城同行总体，不把高校、企业、医院和政府科研机构混为同一基准。

### 45.4 `ads_city_field_resource_yearly`

逻辑Key为`city_location_id, statistics_year, field_id`，固定发布10城×11年×26个Field完整网格。该表
直接从固定论文、年度引用、人才和项目机构关系证据按Field重算，不从
`ads_city_subfield_resource_yearly`求和。`talent_count`按城市、年度、Field、来源人才ID去重；
`project_count`按城市、年度、Field、项目ID去重，避免同一项目在同城多家机构重复计数；
`avg_citations_per_paper`和`avg_fwci`从Field论文集合重新计算。

论文、引用、分数计数和统一资金的来源、观察范围与Subfield表一致。项目金额继续按全部项目机构关系
权重分配，但项目数、估算项目数、真实项目数、覆盖率和来源状态均在Field目标粒度重新计算。首版发布
2,860行；所有资金单元`funding_amount_project_count=project_count`且覆盖率为1。

### 45.5 `ads_institution_field_resource_yearly`

逻辑Key为`institution_id, statistics_year, field_id`。十城有论文、引用或人才证据的机构发布观察行；
深圳机构额外补齐全部年度和Field零值网格。论文、引用、人才和项目均从证据层按机构、年度、Field
独立重算，其中人才和项目分别按来源人才ID和项目ID去重，不得从Subfield指标求和；均值、覆盖率与
来源状态也必须重新计算。首版发布238,289行，覆盖2,175家机构和26个Field。

两张Field表当前用于Field筛选、趋势和资源总量查询，不改变既有Subfield短板表的粒度或基准规则。
首版质量核验发现城市表2,442个Field单元的去重人才数小于对应Subfield人才数之和，证明Subfield
简单相加会产生重复人才。

### 45.6 `ads_city_domain_resource_yearly`

逻辑Key为`city_location_id, statistics_year, domain_id`，固定发布10城×11年×4个Domain完整网格。
该表直接从固定论文、年度引用、人才和项目机构关系证据按Domain重算，不从Field或Subfield事实表求和。
`talent_count`按城市、年度、Domain、来源人才ID去重；`project_count`按城市、年度、Domain、项目ID去重；
论文均值、资金覆盖率和来源状态也在Domain粒度重新计算。首版发布440行，资金项目参与覆盖率全部为1。

### 45.7 `ads_institution_domain_resource_yearly`

逻辑Key为`institution_id, statistics_year, domain_id`。十城有论文、引用或人才证据的机构发布观察行；
深圳机构额外补齐全部年度和Domain零值网格。论文、引用、人才、项目、均值、覆盖率和来源状态均从
证据层按机构、年度、Domain独立重算，不得从Field或Subfield指标求和。首版发布64,836行，覆盖
2,175家机构和4个Domain；资金项目参与覆盖率全部为1。

两张Domain表当前用于Domain筛选、趋势和资源总量查询，不改变既有Subfield短板表粒度。首版质量
核验中全部440个城市Domain单元的去重人才数均小于对应Field人才数之和，证明Field简单相加会重复。

### 45.8 `ads_research_resource_shortage_yearly`

本表采用指标长表，`target_type`为`CITY/INSTITUTION`，`metric_code`当前为城市
`PAPER_FRACTIONAL_COUNT/CITATION_COUNT/TALENT_COUNT/PROJECT_FUNDING_CNY`或机构
`PAPER_COUNT/CITATION_COUNT/TALENT_COUNT/PROJECT_FUNDING_CNY`。城市基准方法固定为
`PEER_CITY_MEAN_9`；机构固定为`SAME_TYPE_PEER_INSTITUTION_MEAN`且有效同行少于5家时不评估。

固定公式为：

```text
resource_ratio = target_value / benchmark_value
gap_rate = max(0, (benchmark_value - target_value) / benchmark_value)
gap_rate > 0.50 => CRITICAL_SHORTAGE
0.20 < gap_rate <= 0.50 => SHORTAGE
0 <= gap_rate <= 0.20 => BALANCED
target_value > benchmark_value => ADVANTAGE
```

基准为空或为0时使用`NO_VALID_BENCHMARK`；机构同行不足使用`INSUFFICIENT_PEERS`。资金统一金额覆盖率
固定为1，包含估算的单元使用`coverage_status='COMPLETE_WITH_ESTIMATION'`。引用和人才均是固定MVP观察范围的
`PARTIAL`代理指标，允许比较但前端必须展示覆盖说明，不能解释为完整引用流或实际在岗科研人口。
完整字段、查询和执行说明见
[`docs/resource_shortage_v1.md`](docs/resource_shortage_v1.md)。

## 46. 智能推荐与动态更新（6.26.0）

本组表已通过6.26.0 Doris迁移、固定配置和可重跑发布SQL落库。首版运行
`smart_rec_2026_20260918_v1`已发布：1条运行、3条新成果信号、3篇Top论文、3名推荐
人才、3个Topic资源方向、78个Technology代理投资方向和87条证据。

### 46.1 可行性结论与MVP口径

方案在当前MVP数据上可实现，但不能把“最新”、“高H指数”和“Topic关联Technology”作为
隐含口径。首版建议固定为`smart_recommendation_mvp_v1`：

1. “2026年参考了发表的论文”解释为`publication_year=2026`的已发布MVP core论文；不是
   “2026年收到的引用”。如果业务实际要求后者，必须单独读取`dwd_work_count_by_year.year=2026`
   的年度新增引用，不得沿用`ads_paper_profile.cited_by_count`。
2. 高H指数人才池限定为已发布MVP人才中`h_index_score>=99`的前1%，并列值全部保留。
   `h_index`和`h_index_score`只表示固定400万篇MVP core观察集合，不是人才的全球完整H指数。
3. 候选论文必须至少有一名署名人才进入上述人才池；按`cited_by_count DESC,
   publication_date DESC, paper_id ASC`稳定排序，全局取三篇。引用数为指标截止日的累计值，
   2026论文存在明显的发表时间暴露差异，首版只能作为新成果关注度代理。
4. 人才推荐不复制全部论文作者。每篇入选论文只保留高H指数人才池内`h_index DESC,
   citations_count DESC, talent_id ASC`的第一名；同一人才命中多篇时合并为一条推荐。
5. 资源配置方向只使用三篇论文的`primary_topic_id`，按支撑论文数、最高引用数和Topic ID
   稳定排序；不将一篇论文的全部次要Topic扩张成资源建议。
6. 投资方向首版只能使用已有`ads_technology_profile.leading_topic_id`作为
   `LEADING_TOPIC_PROXY_V1`映射：先把平台Topic ID还原到OpenAlex Topic ID，再匹配所有以它为
   leading Topic的Technology。该关系是多对多代理，不是专家确认的投资因果关系；无匹配时
   必须显示“暂无可追溯Technology映射”，不允许按名称模糊猜测。

因此，本MVP能给出“基于固定科研观察集的候选建议”，不能宣称已得到完整人才排名、实际
资源需求或投资回报预测。实际投资决策还需引入专利、项目、市场、政策、标准、成本及专家
审核；不得将本表的代理排名直接用于自动资金配置。

#### 46.1.1 完整计算公式与稳定裁决

以一次运行`r`为单位，令`Y=r.publication_year`、`K=r.top_paper_limit`、
`H=r.high_h_index_score_threshold`。首版分别为2026、3和99。

```text
high_h_talent_set(r)
  = { t | t.h_index_score >= H }

candidate_paper_set(r)
  = distinct { p |
      p.publication_year = Y
      AND p.primary_topic_id IS NOT NULL
      AND exists authorship(p, t), t in high_h_talent_set(r) }

paper_rank(p)
  = row_number over candidate_paper_set(r)
    order by p.cited_by_count DESC,
             p.publication_date DESC,
             p.paper_id ASC

recommended_paper_set(r)
  = { p | paper_rank(p) <= K }
```

`cited_by_count`是`metrics_as_of_date`截止日累计引用，不是2026年度新增引用。
对每篇入选论文，人才二次筛选为：

```text
recommended_talent_for_paper(p)
  = first { t | authorship(p, t) AND t in high_h_talent_set(r) }
    order by t.h_index DESC,
             t.citations_count DESC,
             t.talent_id ASC

supporting_paper_ids(t)
  = distinct sorted { p.paper_id |
      p in recommended_paper_set(r)
      AND recommended_talent_for_paper(p) = t }

talent_recommendation_rank(t)
  = row_number order by
      min(paper_rank(p), p in supporting_paper_ids(t)) ASC,
      t.h_index DESC,
      t.talent_id ASC
```

同一人才被多篇论文选中时只保留一条人才推荐。一个资源Topic的聚合和排名为：

```text
resource_topic_set(r)
  = distinct { p.primary_topic_id | p in recommended_paper_set(r) }

supporting_paper_count(topic)
  = count(distinct p.paper_id where p.primary_topic_id = topic)

max_paper_cited_by_count(topic)
  = max(p.cited_by_count where p.primary_topic_id = topic)

best_paper_rank(topic)
  = min(p.paper_rank where p.primary_topic_id = topic)

resource_direction_rank(topic)
  = row_number order by
      supporting_paper_count DESC,
      max_paper_cited_by_count DESC,
      best_paper_rank ASC,
      topic_id ASC
```

Technology映射及排名为：

```text
technology_matches(topic, technology)
  iff ads_discipline_topic.topic_id = topic
  AND ads_discipline_topic.openalex_topic_id
      = ads_technology_profile.leading_topic_id

source_topic_ids(technology)
  = distinct sorted { topic | technology_matches(topic, technology) }

supporting_paper_ids(technology)
  = union supporting_paper_ids(topic), topic in source_topic_ids(technology)

investment_direction_rank(technology)
  = row_number order by
      min(resource_direction_rank(topic)) ASC,
      cardinality(supporting_paper_ids(technology)) DESC,
      ads_technology_profile.paper_count DESC,
      technology_node_id ASC
```

本版没有权重求和、资金额或投资回报分；`evidence_weight`因此保持NULL。更新信号与
幂等哈希为：

```text
signal_type(entity, current_run, previous_run)
  = NEW,     if entity exists in current_run and not in comparable previous_run
  = CHANGED, if entity exists in both runs and current_row_hash <> previous_row_hash
  = no row,  otherwise

current_row_hash
  = SHA-256(canonical business fields joined with "|")

input_hash
  = SHA-256(model_version, parameters, ordered source snapshot identifiers)

output_hash
  = SHA-256(ordered paper IDs, ordered talent IDs,
            ordered resource Topic IDs, ordered Technology IDs)

evidence_hash
  = SHA-256(evidence entity ID, calculation inputs, mapping method when applicable)
```

首次运行`previous_recommendation_run_id IS NULL`，因此对3篇入选论文发布`NEW/NEW_PUBLICATION`；
另从排名第1论文的署名机构中，按固定机构Snapshot的`works_count DESC, institution_id ASC`
稳定选取1家，发布`INSTITUTION/NEW/NEW_PUBLICATION`。该机构信号表示机构新增一条入选论文关联，
不是机构画像发生变化。首次运行不伪造`CHANGED`。完整业务原因字段分别由`selection_reason`或`recommendation_reason`
承载；可机读溯源由`ads_recommendation_evidence.calculation_step`、
`calculation_description`、`evidence_value_snapshot`和`source_snapshot_id`承载。

### 46.2 `ads_recommendation_run`

一次不可变输入上的推荐运行一行，逻辑Key为`recommendation_run_id`。

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id` | `VARCHAR(64) NOT NULL` | 由模型版本、输入Snapshot和参数哈希确定的运行ID |
| `model_version` | `VARCHAR(64) NOT NULL` | 首版`smart_recommendation_mvp_v1` |
| `run_status` | `VARCHAR(32) NOT NULL` | `BUILDING/VALIDATED/PUBLISHED/FAILED` |
| `publication_year` | `SMALLINT NOT NULL` | 首版为2026 |
| `top_paper_limit` | `INT NOT NULL` | 首版为3 |
| `high_h_index_score_threshold` | `DECIMAL(9,6) NOT NULL` | 首版为99 |
| `talent_selection_rule/paper_selection_rule` | `STRING NOT NULL` | 完整门槛、排序和并列裁决文本 |
| `topic_selection_rule/technology_mapping_rule` | `STRING NOT NULL` | Topic及Technology映射口径 |
| `source_snapshot_ids` | `JSON NOT NULL` | 人才、署名、论文、Topic、身份映射和Technology固定输入 |
| `metrics_as_of_date` | `DATE NOT NULL` | H指数与引用数截止日 |
| `previous_recommendation_run_id` | `VARCHAR(64)` | 用于变更比较的上一已发布运行 |
| `input_hash/output_hash` | `VARCHAR(64) NOT NULL` | 规范化输入与输出SHA-256 |
| `generated_at/data_version/update_time` | 多类型 | UTC生成时间与公共版本字段 |

### 46.3 `ads_scientific_update_signal`

本表不由时间字段直接猜测“新”。`NEW`表示当前已发布运行存在、上一已发布运行不存在；
`CHANGED`表示同一主体的规范化业务哈希变化。逻辑Key为`signal_id`。

| 字段 | 类型 | 说明 |
|---|---|---|
| `signal_id/recommendation_run_id` | `VARCHAR(64) NOT NULL` | 信号ID和当前运行ID |
| `entity_type/entity_id` | `VARCHAR(32)/VARCHAR(64) NOT NULL` | `PAPER/TALENT/INSTITUTION/TOPIC/TECHNOLOGY`及平台ID |
| `signal_type` | `VARCHAR(32) NOT NULL` | `NEW/CHANGED` |
| `change_category` | `VARCHAR(64) NOT NULL` | `NEW_PUBLICATION/CITATION_CHANGED/AFFILIATION_CHANGED/PROFILE_CHANGED/MAPPING_CHANGED` |
| `changed_fields` | `ARRAY<STRING> NOT NULL` | 白名单化变化字段；NEW可为空数组 |
| `previous_value_snapshot/current_value_snapshot` | `JSON` | 只保留有界展示值，完整事实回查固定上游 |
| `previous_row_hash/current_row_hash` | `VARCHAR(64)` | 前后规范化业务哈希；当前值必填 |
| `previous_data_version/current_data_version` | `BIGINT` | 前后来源版本 |
| `detected_at/data_version/update_time` | 多类型 | UTC检测时间与公共版本字段 |

机构变更只能在可比的两个机构发布版本间产生；首次运行没有上一版时只生成`NEW`，
不生成伪`CHANGED`。重试同一`recommendation_run_id`必须得到相同信号集合。

### 46.4 `ads_recommendation_paper`

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id/paper_id` | `VARCHAR(64) NOT NULL` | 运行和论文平台ID |
| `paper_rank` | `INT NOT NULL` | 全局稳定排名1—3 |
| `publication_date/publication_year` | `DATE/SMALLINT NOT NULL` | 发表日期和年份 |
| `cited_by_count` | `BIGINT NOT NULL` | 截至`metrics_as_of_date`的累计引用 |
| `primary_topic_id` | `VARCHAR(64) NOT NULL` | 资源方向所用平台Primary Topic |
| `eligible_high_h_talent_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 使论文进入候选的高H人才集合 |
| `recommended_talent_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 作者内二次筛选后的人才ID |
| `selection_reason/selection_rule_version` | `STRING/VARCHAR(64) NOT NULL` | 可展示原因和固定规则版本 |
| `paper_snapshot_id/authorship_snapshot_id` | `VARCHAR(128) NOT NULL` | 论文及署名证据版本 |
| `metrics_as_of_date/data_version/update_time` | 多类型 | 指标截止日与公共版本字段 |

### 46.5 `ads_recommendation_talent`

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id/talent_id` | `VARCHAR(64) NOT NULL` | 运行和人才ID |
| `recommendation_rank` | `INT NOT NULL` | 按支撑论文最佳排名、H指数和人才ID裁决 |
| `h_index/h_index_score/h_index_rank` | 多类型 | 固定MVP core人才总体的H指数、百分位分和稳定排名 |
| `supporting_paper_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 支持推荐的入选论文，至少一篇 |
| `supporting_paper_count/max_paper_cited_by_count` | `BIGINT NOT NULL` | 支持数和最高论文引用数 |
| `recommendation_reason/selection_rule_version` | `STRING/VARCHAR(64) NOT NULL` | 原因和规则版本 |
| `talent_snapshot_id/metrics_as_of_date` | `VARCHAR(128)/DATE NOT NULL` | 人才指标版本与截止日 |
| `data_version/update_time` | `BIGINT/DATETIME(3) NOT NULL` | 公共版本字段 |

### 46.6 `ads_recommendation_resource_direction`

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id/topic_id` | `VARCHAR(64) NOT NULL` | 运行和平台Topic ID |
| `topic_name_zh/topic_name_en` | `STRING` | 固定学科维表名称快照 |
| `direction_rank` | `INT NOT NULL` | 资源方向排名 |
| `supporting_paper_ids/supporting_talent_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 论文与人才证据 |
| `supporting_paper_count/max_paper_cited_by_count` | `BIGINT NOT NULL` | 排名原始指标 |
| `recommendation_reason` | `STRING NOT NULL` | 只声明“候选资源方向”，不生成资金额 |
| `topic_snapshot_id/data_version/update_time` | 多类型 | Topic版本与公共版本字段 |

### 46.7 `ads_recommendation_investment_direction`

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id/technology_node_id` | `VARCHAR(64) NOT NULL` | 运行和候选技术点ID |
| `technology_name_zh/technology_name_en` | `STRING` | 固定Technology快照名称 |
| `direction_rank` | `INT NOT NULL` | 按Topic排名、支持论文数、Technology论文数和ID裁决 |
| `source_topic_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 导出该Technology的资源Topic |
| `supporting_paper_ids/supporting_talent_ids` | `ARRAY<VARCHAR(64)> NOT NULL` | 上游论文和人才证据 |
| `mapping_method` | `VARCHAR(64) NOT NULL` | 首版`LEADING_TOPIC_PROXY_V1` |
| `mapping_status` | `VARCHAR(32) NOT NULL` | `PROXY_MATCHED/REVIEWED/REJECTED`；首版只能为PROXY_MATCHED |
| `mapping_version/technology_source_release_id` | `VARCHAR(128) NOT NULL` | Topic身份映射与Technology来源发布版本 |
| `recommendation_reason/limitation_note` | `STRING NOT NULL` | 推荐原因和非投资因果声明 |
| `data_version/update_time` | `BIGINT/DATETIME(3) NOT NULL` | 公共版本字段 |

### 46.8 `ads_recommendation_evidence`

一行是一个推荐结果的一条证据，用于“查看推荐来源及模型依据”。逻辑Key为
`recommendation_run_id, recommendation_type, recommendation_id, evidence_id`。

| 字段 | 类型 | 说明 |
|---|---|---|
| `recommendation_run_id` | `VARCHAR(64) NOT NULL` | 关联运行 |
| `recommendation_type/recommendation_id` | `VARCHAR(32)/VARCHAR(64) NOT NULL` | `PAPER/TALENT/RESOURCE_DIRECTION/INVESTMENT_DIRECTION`及结果ID |
| `evidence_id/evidence_type/evidence_entity_id` | 多类型 | 稳定证据ID、`PAPER/TALENT_METRIC/TOPIC_MAP/TECHNOLOGY_MAP`和实体ID |
| `evidence_rank/evidence_weight` | `INT/DECIMAL(9,6)` | 展示顺序和权重；无权重模型时保持NULL |
| `evidence_value_snapshot` | `JSON NOT NULL` | 如H指数、引用数、Primary Topic和mapping method等有界快照 |
| `source_table/source_business_key/source_snapshot_id` | `STRING NOT NULL` | 真实上游表、业务Key和Snapshot |
| `calculation_step/calculation_description` | `VARCHAR(64)/STRING NOT NULL` | 稳定步骤代码与人类可读依据 |
| `evidence_hash` | `VARCHAR(64) NOT NULL` | 规范化证据SHA-256 |
| `data_version/update_time` | `BIGINT/DATETIME(3) NOT NULL` | 公共版本字段 |

### 46.9 发布门禁和前端展示

发布必须验证：固定输入Snapshot全部存在；三篇论文的年份、排名、署名和人才门槛
合法；人才、Topic和Technology的证据引用完整；同一输入重跑的`output_hash`一致；前后运行
仅在输入版本可比时产生`CHANGED`。如果2026年MVP core尚未发布、不足3篇，或其
`metrics_as_of_date`早于论文发表日，运行必须失败或明确发布少于3篇的降级状态，不得用
2025论文静默补齐。

前端“新”/“变动”标识必须读取`ads_scientific_update_signal.signal_type`，不按当前时间现场猜测；
每张推荐卡必须展示`metrics_as_of_date`、模型版本、覆盖边界和至少一条可点击证据。
Technology卡须额外显示“基于Leading Topic代理映射，未经投资审核”。

当前发布入口和回归测试为：

```bash
./scripts/compose.sh up -d --wait --wait-timeout 300
./scripts/publish_smart_recommendation_mvp_v1.sh
uv run --frozen pytest -q tests/test_smart_recommendation_ads.py
```

首版重跑后行数保持`1/4/3/3/3/78/87`（运行/更新信号/论文/人才/资源Topic/
Technology/证据），逻辑Key重复、论文规则违反、人才门槛违反、Topic孤儿、Technology孤儿和
无证据推荐均为0。

## 47. 科研资源配置与优化建议（6.28.0）

本组表仅将2025年`ads_research_resource_shortage_yearly`中同时满足
`assessment_status='ASSESSED'`、`is_critical_shortage=true`和`target_value>0`的记录认定为首版
“真实可行动关键短板”。零观测记录、不可评估记录和普通短板不生成建议。首版不生成管理机制改进建议，
也不调用大模型；方案、优先级和预期效果均由`resource_optimization_rule_v1`确定性产生。

同一`target_type + target_id + statistics_year + subfield_id`的多项短板合并为一条建议，避免论文、引用、
人才和资金分别生成重复方案。2025年7,952条来源短板聚合为4,625条建议；每条建议可通过证据表回溯
原始指标。

### 47.1 `ads_resource_optimization_recommendation`

逻辑Key为`recommendation_id`，ID由目标类型、目标ID、年度、Subfield、基准版本和建议规则版本确定性
生成。`institution_id`只在`target_type='INSTITUTION'`时等于`target_id`，城市建议保持NULL；该显式字段
只服务机构视图，不改变短板表的多态目标模型。机构`target_name`及建议标题优先使用
`ads_institution_profile.name_zh`，只有中文名为空时才回退短板来源名称。

三种视图直接读取同一张表：按学科使用`subfield_id/subfield_name_zh`，按机构使用
`institution_id/target_name`，按研究方向使用`field_id/field_name_zh`。`scope_type`区分
`CITY_SUBFIELD/INSTITUTION_SUBFIELD`。

优先级满分100分，固定公式为：

```text
priority_score = avg_gap_rate * 40
               + shortage_metric_count / 4 * 20
               + persistence_rate * 20
               + confidence_score * 20

priority_score >= 75 => HIGH
60 <= priority_score < 75 => MEDIUM
priority_score < 60 => LOW
```

`persistence_rate`只看2023—2025同一目标、Subfield和当前短板指标满足正值关键短板的年度比例；
`confidence_score`按`COMPLETE=1.0`、`COMPLETE_WITH_ESTIMATION=0.8`、其他部分覆盖`=0.6`计算。
优先级是规划排序，不是因果效果评分。

`recommendation_category`当前为`COMPREHENSIVE_CAPACITY`、`RESOURCE_INPUT`、`OUTPUT_IMPACT`、
`TALENT`、`FUNDING`、`OUTPUT`、`IMPACT`或`MULTI_RESOURCE`，不含管理机制类别。
`implementation_plan`保存可展开的具体方案；
`expected_effect`统一表述为1—3年规划目标，首阶段把相关差距率降至50%以内，必须用后续同口径数据验证，
不得解释为已保证的因果效果。

### 47.2 `ads_resource_optimization_recommendation_evidence`

逻辑Key为`recommendation_id, metric_code, benchmark_version`。每行保存来源短板的`target_value`、
`benchmark_value`、`gap_rate`、`coverage_status`和`coverage_note`。发布门禁要求证据全部满足
`target_value>0`且`gap_rate>0.5`，建议无孤儿、主表`evidence_count`与证据实数完全一致。

当前执行入口和说明为：

```bash
./scripts/publish_resource_optimization_recommendation_v1.sh
uv run --frozen --group integration pytest -q tests/test_resource_optimization_recommendation.py
```

完整字段、查询示例和发布结果见
[`docs/resource_optimization_recommendation_v1.md`](docs/resource_optimization_recommendation_v1.md)。

## 48. 基础研究成果评估演示（6.29.0）

本版本把`ads_research_problem_paper.evidence_level='DIRECT'`与`ads_paper_profile`的交集定义为一期
“基础研究成果”。当前DIRECT关系1,294条，其中342篇具有MVP平台论文画像，另外952篇仅有
`openalex:`来源ID回退，不进入本评估。342篇成果覆盖216个基础研究问题。

本功能是显式演示评估：论文题名、摘要、发表时间、引用、FWCI、Topic、署名机构以及论文—专利/项目
连接属于观测或确定性派生数据；四维评分中的固定代理项、演示期刊影响因子、历史评分曲线、未来预测和
推荐属于`SYNTHETIC_SIMULATION`或`MIXED`。所有包含模拟值的行必须同时发布
`is_synthetic=true`和`review_status='PENDING_REVIEW'`，不得作为专家结论、真实期刊影响因子、投资承诺
或成果转化事实。

四维及综合分均为0—100：

```text
scientific_value = 45% FWCI百分位 + 25%引用百分位
                 + 15% Topic广度百分位 + 15%固定理论价值代理
application_potential = 35%关联专利百分位 + 15%关联授权专利百分位
                      + 15%关联项目百分位 + 35%固定应用代理
innovation = 35% FWCI百分位 + 25% Topic广度百分位 + 40%固定创新代理
academic_impact = 55%引用百分位 + 35% FWCI百分位 + 10%机构广度百分位
overall_value = 30%科学价值 + 25%应用潜力 + 20%创新性 + 25%学术影响力
```

固定代理使用`CRC32(paper_id + component + simulation_seed)`生成，种子和版本公开保存，重跑结果稳定。
论文—专利和论文—项目连接只在同一DIRECT问题内按`evidence_work_ids`核验，授权只表示
`grant_date IS NOT NULL`，不表示专利当前有效或论文已经转化。

### 48.1 表与逻辑Key

| 表 | 逻辑Key | 用途 |
|---|---|---|
| `ads_research_outcome_release` | `release_id` | 发布范围、输入版本、模拟版本和边界 |
| `ads_research_outcome_profile` | `release_id, outcome_id` | 342篇成果画像、四维分、综合分和规则说明 |
| `ads_research_outcome_problem` | `release_id, outcome_id, problem_id` | 成果—基础研究问题DIRECT关系 |
| `ads_research_outcome_discipline` | `release_id, outcome_id, topic_id` | Topic/Field/Domain筛选桥接 |
| `ads_research_outcome_institution` | `release_id, outcome_id, institution_id` | 复用机构Top 20论文证据的署名机构筛选桥接及覆盖状态 |
| `ads_research_outcome_dimension` | `release_id, outcome_id, dimension_code` | 雷达图和多成果对比 |
| `ads_research_outcome_metric` | `release_id, outcome_id, metric_code` | 指标原值、来源、计算方法和真假标识 |
| `ads_research_outcome_yearly_metric` | `release_id, outcome_id, statistics_year, metric_code` | 2015—2026演示评分轨迹 |
| `ads_research_outcome_forecast` | `release_id, outcome_id, forecast_model_version, forecast_year, target_metric` | 2027—2029未回测演示预测 |
| `ads_research_outcome_recommendation` | `release_id, recommendation_id` | 投入、转化和跟进三类演示建议 |

`ads_research_outcome_recommendation.recommendation_title_zh`只保存成果中文题名，不得添加
“科研投入建议”、“成果转化建议”或“持续跟进建议”等固定类型前缀。当来源成果没有中文题名时，
必须先完成全量、版本化且可追溯的中文翻译，不得将英文回退值对外发布为`*_zh`字段。

`outcome_id`首版等于平台`paper_id`。对比分析不建立用户临时表，前端按选择的`outcome_id`直接查询
`ads_research_outcome_dimension`。列表和总览使用主表，学科、机构和问题筛选分别连接三张桥接表。

机构桥接首版复用`ads_institution_paper`，该来源只保存每家机构的Top 20代表论文，因此机构筛选为部分
覆盖，不得把没有机构桥接行解释为论文没有署名机构；完整机构筛选需后续单独物化342篇论文的全量
`dwd_work_authorship_institution`关系。

年度四维曲线是从发表年（早于2015的从2015开始）到2026年的确定性演示轨迹，不是历史时点重新计算；
未来三年全部固定`forecast_status='AI_ESTIMATED_NOT_BACKTESTED'`、`is_backtested=false`。

### 48.2 前端“计算依据”展示契约

用户点击科学价值、应用潜力、创新性或学术影响力时，前端应打开指标详情抽屉或弹窗。这里的“计算依据”
不是只显示一段模型说明，而是按以下四层固定展示；前端不得自行修改权重、用空值补0或把模拟值改写为
事实值。

#### 48.2.1 第一层：本成果的指标结果

从`ads_research_outcome_dimension`读取：

| 页面内容 | 字段 | 说明 |
|---|---|---|
| 指标名称 | `dimension_name_zh` | 科学价值、应用潜力、创新性或学术影响力 |
| 指标得分 | `dimension_score` | 0—100分 |
| 综合价值权重 | `dimension_weight` | 该维度进入综合价值的权重 |
| 对综合价值的贡献 | `weighted_contribution` | `dimension_score * dimension_weight` |
| 同批排名和百分位 | `dimension_rank/dimension_percentile` | 只在当前342篇固定总体内比较 |
| 计算方法 | `score_method` | 当前为`HYBRID_RULE_DETERMINISTIC_DEMO_V1` |
| 简要解释 | `assessment_summary_zh` | 面向用户的口径说明 |
| 数据性质 | `value_nature/is_synthetic/review_status` | 必须与分数同时展示 |

例如`dimension_score=82.641783`、`dimension_weight=0.30`时，页面应显示“科学价值82.64分，
占综合价值30%，贡献24.79分”，不能把82.64直接称为综合价值。

#### 48.2.2 第二层：固定公式

前端按`dimension_code`使用下表，不根据中文名称猜测公式：

| `dimension_code` | 页面公式 | 分项性质 |
|---|---|---|
| `SCIENTIFIC_VALUE` | `45%×FWCI百分位 + 25%×引用百分位 + 15%×Topic广度百分位 + 15%×理论价值代理` | 前三项派生，理论价值代理为模拟 |
| `APPLICATION_POTENTIAL` | `35%×关联专利百分位 + 15%×关联授权专利百分位 + 15%×关联项目百分位 + 35%×应用代理` | 连接数为派生，应用代理为模拟 |
| `INNOVATION` | `35%×FWCI百分位 + 25%×Topic广度百分位 + 40%×创新代理` | 前两项派生，创新代理为模拟 |
| `ACADEMIC_IMPACT` | `55%×引用百分位 + 35%×FWCI百分位 + 10%×机构广度百分位` | 全部为确定性派生 |

综合价值固定显示为：

```text
30%×科学价值 + 25%×应用潜力 + 20%×创新性 + 25%×学术影响力
```

百分位总体固定为本发布的342篇成果，使用Doris`percent_rank()`；NULL FWCI位于排序最低端。固定代理使用
公开的`simulation_seed`与成果`paper_id`计算，公式见本节开头。页面必须在含代理项的维度旁显示
“含模拟指标”；学术影响力可显示“确定性派生”。

#### 48.2.3 第三层：本成果的证据指标

先读取`ads_research_outcome_dimension.evidence_metric_codes`确定应解释的指标，再从
`ads_research_outcome_metric`读取实际可展示的指标行：

| 页面内容 | 字段 |
|---|---|
| 指标名称与代码 | `metric_name_zh/metric_code` |
| 原始值与单位 | `numeric_value/text_value/value_unit` |
| 标准化分、权重和贡献 | `normalized_score/metric_weight/weighted_contribution` |
| 数据来源 | `source_table/source_field` |
| 计算方法 | `calculation_method` |
| 覆盖状态 | `coverage_status` |
| 真假属性 | `value_nature/is_synthetic` |

真假属性的前端文案固定为：

| `value_nature` | 页面标签 | 解释 |
|---|---|---|
| `OBSERVED` | 来源事实 | 直接读取论文画像等事实字段 |
| `DERIVED` | 计算指标 | 从固定来源确定性计算，不是来源原始字段 |
| `MIXED` | 混合评估 | 同时包含事实/派生指标和模拟代理 |
| `SYNTHETIC_SIMULATION` | 模拟数据 | 仅用于功能演示，不得作为事实引用 |

6.29.0已经保存引用、FWCI、关联专利、关联授权专利、关联项目、演示期刊影响因子和四维最终分；但基础
指标行的`normalized_score/metric_weight/weighted_contribution`当前为空，且Topic广度百分位、机构广度
百分位和三个固定代理尚未逐项物化。因此当前页面可以展示“固定公式 + 原始值 + 来源 + 真假属性”，但
不能声称已经提供每个分项的逐项加总复算。字段为空时显示“暂未物化”，禁止前端自行填0或随机补值。

#### 48.2.4 第四层：历史趋势与成果分布

历史趋势读取`ads_research_outcome_yearly_metric`，按当前成果和对应`metric_code`排序展示
`statistics_year/metric_value`。这些曲线固定标记`SYNTHETIC_SIMULATION`，页面标题必须使用“演示评分
轨迹”，不能称为真实历史评价。

相关成果分布从同一发布的`ads_research_outcome_dimension.dimension_score`按10分区间现场聚合。分布表示
342篇固定成果之间的横向位置，不表示全球论文分布或学科总体分布。

#### 48.2.5 前端查询顺序

点击一个维度后依次执行：

```sql
-- 1. 得分、综合权重、贡献和指标代码
SELECT dimension_code,dimension_name_zh,dimension_score,dimension_weight,
       weighted_contribution,dimension_rank,dimension_percentile,
       assessment_summary_zh,evidence_metric_codes,value_nature,is_synthetic,review_status
FROM ads_research_outcome_dimension
WHERE release_id=:release_id AND outcome_id=:outcome_id AND dimension_code=:dimension_code;

-- 2. 当前已物化的原始依据和来源
SELECT metric_code,metric_name_zh,numeric_value,text_value,value_unit,
       normalized_score,metric_weight,weighted_contribution,
       source_table,source_field,calculation_method,value_nature,is_synthetic,coverage_status
FROM ads_research_outcome_metric
WHERE release_id=:release_id AND outcome_id=:outcome_id AND dimension_code=:dimension_code
ORDER BY weighted_contribution DESC,metric_code;

-- 3. 对应演示轨迹
SELECT statistics_year,metric_value,value_nature,is_synthetic,coverage_status
FROM ads_research_outcome_yearly_metric
WHERE release_id=:release_id AND outcome_id=:outcome_id AND metric_code=:score_metric_code
ORDER BY statistics_year;

-- 4. 同维度成果分布
SELECT floor(dimension_score/10)*10 score_bucket,count(*) outcome_count
FROM ads_research_outcome_dimension
WHERE release_id=:release_id AND dimension_code=:dimension_code
GROUP BY 1 ORDER BY 1;
```

`score_metric_code`映射固定为`SCIENTIFIC_VALUE_SCORE`、`APPLICATION_POTENTIAL_SCORE`、
`INNOVATION_SCORE`或`ACADEMIC_IMPACT_SCORE`。前端不得使用演示期刊影响因子替代FWCI，也不得把论文—
专利连接解释为成果已授权、已许可或已转化。

### 48.3 成果趋势、节点案例与范围预测（6.30.0）

6.30.0新增4张表，补齐理论价值增长、应用性提升、学术影响力演变、趋势节点详情以及按学科或机构筛选
的范围趋势和预测。所有趋势均固定在2015—2026观察窗；2027—2029为未回测演示预测。

| 表 | 逻辑Key | 用途 |
|---|---|---|
| `ads_research_outcome_yearly_evidence` | `release_id, outcome_id, statistics_year` | 单篇成果年度引用分配、专利/授权/项目事件及三项价值分 |
| `ads_research_outcome_scope_yearly` | `release_id, scope_type, scope_id, statistics_year, metric_code` | GLOBAL、Topic、Field、Domain、Institution范围年度趋势 |
| `ads_research_outcome_trend_case` | `release_id, scope_type, scope_id, statistics_year, metric_code, outcome_id` | 每个趋势节点最多5篇重点成果 |
| `ads_research_outcome_scope_forecast` | `release_id, scope_type, scope_id, forecast_model_version, forecast_year, target_metric` | 范围级2027—2029预测值和区间 |

#### 48.3.1 单篇成果年度证据

`ads_research_outcome_yearly_evidence`发布：

| 功能 | 字段 | 性质 |
|---|---|---|
| 理论价值增长 | `theoretical_value_score` | 复用科学价值演示轨迹，`SYNTHETIC_SIMULATION` |
| 应用性提升 | `application_value_score` | 应用潜力演示轨迹，`MIXED` |
| 应用年度事件 | `new_patent_link_count/new_granted_patent_count/new_project_link_count` | 按专利公开年、授权年、项目有效开始年确定性派生 |
| 学术影响力演变 | `academic_impact_score` | 引用与FWCI驱动的演示轨迹，`MIXED` |
| 年度新增引用 | `annual_citation_count` | 从当前累计引用按二次增长曲线确定性分配，模拟 |
| 累计引用 | `cumulative_citation_count` | 上述年度分配累计；2026值必须等于当前论文累计引用 |

当前来源没有论文历史时点理论价值和完整逐年引用事件，因此理论价值曲线和年度引用分配不得显示为历史
事实。`citation_allocation_method='CUMULATIVE_CITATION_QUADRATIC_ALLOCATION_V1'`用于明确该边界。专利和
项目年度事件来自已有连接事实，但“连接”仍不等于已完成成果转化。

#### 48.3.2 学科、机构和全局趋势

`ads_research_outcome_scope_yearly.scope_type`固定为`GLOBAL/TOPIC/FIELD/DOMAIN/INSTITUTION`。每个
`scope_id + statistics_year + metric_code`保存：

```text
outcome_count/new_outcome_count          成果总数和当年新发表成果数
metric_value                             分数指标等权平均；事件指标为合计
metric_total/metric_p50/metric_min/max   合计、中位数和范围
metric_change/year_over_year_growth_rate 与上一观察年的变化
observed_outcome_count                   只使用派生事实事件的成果数
synthetic_outcome_count                  含模拟值的成果数
coverage_rate/coverage_status            覆盖和机构代理边界
```

`metric_code`固定包括`THEORETICAL_VALUE_SCORE`、`APPLICATION_VALUE_SCORE`、
`ACADEMIC_IMPACT_SCORE`、`ANNUAL_CITATION_COUNT`、`NEW_PATENT_LINK_COUNT`、
`NEW_GRANTED_PATENT_COUNT`和`NEW_PROJECT_LINK_COUNT`。

学科范围使用342篇成果完整Primary Topic及其Field、Domain父链。机构范围对原有122篇成果使用
`relation_nature='OBSERVED_AUTHORSHIP'`的机构Top 20论文证据；其余220篇使用每个基础问题匹配排名前3的
`relation_nature='PROBLEM_CANDIDATE_PROXY'`深圳机构代理。代理只用于完成机构筛选演示，不表示论文由该
机构署名。当前机构桥接共1,220行、覆盖342篇成果和643家机构，其中署名证据652行、问题候选代理568行。

#### 48.3.3 趋势节点和重点案例

点击趋势节点先读取`ads_research_outcome_scope_yearly`的成果数量、指标值、变化和同比，再按相同
`scope_type/scope_id/statistics_year/metric_code`查询`ads_research_outcome_trend_case`。案例按当年指标值
降序、变化值降序和`outcome_id`稳定排序，每个节点最多5篇。

案例卡展示`title/publication_year/metric_value/metric_change/problem_ids/institution_ids`及
`selection_reason_zh`。`institution_relation_scope='CONTAINS_PROBLEM_CANDIDATE_PROXY'`时必须显示
“机构为问题候选代理，非论文署名”提示。

#### 48.3.4 范围预测

`ads_research_outcome_scope_forecast`把同一范围内单篇成果预测等权聚合，发布预测均值、上下界、来源成果
数和历史观察年数。全部行固定：

```text
forecast_status = AI_ESTIMATED_NOT_BACKTESTED
is_backtested = false
value_nature = SYNTHETIC_SIMULATION
is_synthetic = true
```

它可以驱动可视化预测报告，但不能解释为经训练、回测或校准的领域/机构预测。

前端趋势查询：

```sql
SELECT statistics_year,outcome_count,new_outcome_count,metric_value,metric_p50,
       metric_change,year_over_year_growth_rate,value_nature,is_synthetic,coverage_status
FROM ads_research_outcome_scope_yearly
WHERE release_id=:release_id AND scope_type=:scope_type AND scope_id=:scope_id
  AND metric_code=:metric_code
ORDER BY statistics_year;

SELECT case_rank,outcome_id,title,publication_year,metric_value,metric_change,
       problem_ids,institution_ids,selection_reason_zh,value_nature,
       institution_relation_scope
FROM ads_research_outcome_trend_case
WHERE release_id=:release_id AND scope_type=:scope_type AND scope_id=:scope_id
  AND statistics_year=:statistics_year AND metric_code=:metric_code
ORDER BY case_rank;

SELECT forecast_year,target_metric,forecast_value,lower_bound,upper_bound,
       source_outcome_count,forecast_status,value_nature,is_synthetic,coverage_status
FROM ads_research_outcome_scope_forecast
WHERE release_id=:release_id AND scope_type=:scope_type AND scope_id=:scope_id
  AND target_metric=:target_metric
ORDER BY forecast_year;
```

执行入口：

```bash
./scripts/publish_research_outcome_trend_v1.sh
uv run --frozen pytest -q tests/test_research_outcome_trend.py
```

执行入口：

```bash
./scripts/publish_research_outcome_assessment_demo_v1.sh
uv run --frozen pytest -q tests/test_research_outcome_assessment.py
```

完整字段和前端查询示例见
[`docs/research_outcome_assessment_demo_v1.md`](docs/research_outcome_assessment_demo_v1.md)。

2026-10-31当前发布：成果342、问题关系342、Primary Topic关系342、机构关系1,220、四维记录1,368、
指标依据3,420、年度轨迹9,055、单篇预测5,130、建议1,026；新增成果年度证据1,811、范围年度趋势
41,153、趋势节点案例22,881和范围预测10,944。累计引用终值对账、分数范围、主Key、节点Top 5、案例
外键和模拟标识异常均为0。

## 49. 媒体聚焦证据关系与选择性样本指标（8.5.0）

本组表消费`media_focus_mvp_dws_v3_20261103`，发布ID为`media_focus_ads_v1_20261103`。输入54篇
选择性样本、36个媒体来源和73条文章—目标关系。技术关系仅允许`review_status='HUMAN_APPROVED'`；
机构与人才来源关系保留`SOURCE_CONFIRMED`。所有表都保存DWS release、ADS Schema版本、数据版本和
更新时间，使用Unique Key Merge-on-Write支持同版本幂等重跑。

### 49.1 `ads_media_article_relation`

逻辑主键为`release_id, relation_id`。每行保存一条文章到`TECHNOLOGY/INSTITUTION/AUTHOR`的关系，
包含媒体来源、标题、发布日期、原文URL、目标名称、关系类型、证据等级、置信度、审核状态/方法/人员/
时间、证据文本与位置、模型和Prompt血缘、DWD Snapshot及上游release。证据文本用于页面下钻，原文
URL必须同时展示；模型置信度不是事实概率。

### 49.2 `ads_media_target_daily`

逻辑主键为`release_id, statistics_date, target_type, target_id`。保存目标当天的去重文章数、来源数、
独立编辑来源数、机构自有来源数和关系数。`coverage_status='SELECTIVE_SAMPLE'`表示仅可展示已收录报道
时间线，不能解释为全网日声量或增长率。

### 49.3 `ads_media_source_profile`

逻辑主键为`release_id, media_source_id`。一行保存一个发布内的媒体来源画像，包括来源原始展示名称、
中文展示名称`source_name_zh`、规范域名、所有者类型、编辑独立性类型、主要语言、国家或地区代码、核验
状态和核验时间。中文名来自版本化固定翻译映射；原始名称变化时发布器拒绝复用旧翻译。来源画像直接
来自固定的DWD媒体来源发布，不依赖该来源是否已经形成目标关系；页面来源列表和来源筛选应读取本表。

### 49.4 `ads_media_source_target_edge`

逻辑主键为`release_id, media_source_id, target_type, target_id, window_start_date, window_end_date`。
保存媒体来源到目标的文章数、直接证据文章数、首末报道日期和关系类型数组。该边支持媒体—技术/机构/
人才二部网络，不表示媒体之间的转载传播路径，也不表示统计耦合或因果关系。来源展示名称、域名、来源
所有者类型、编辑独立性类型以及目标名称不在边表重复保存；展示时分别关联`ads_media_source_profile`和
相应的技术、机构或人才画像表。

### 49.5 `ads_media_focus_overview`

逻辑主键为`release_id, window_start_date, window_end_date`。只发布可核验的媒体来源数、文章数、各目标
类型文章数和目标数、技术关系数、人工审核技术关系数及独立来源数。首版不包含热点数量、情感占比或
耦合分；这些功能应显示“数据未支持”，不得填默认0。

## 50. 媒体热点、情感偏向与耦合估算（8.6.0）

本组表消费`media_focus_insight_dws_v1_20261103`，ADS发布ID为`media_focus_ads_v2_20261103`。

### 50.1 `ads_media_hotspot`

逻辑主键为`hotspot_id`，共22行。每行保存原技术点、模型提炼的媒体热点名、文章/来源/关系数、情感分、
正中负标签、置信度、理由、政策相关潜力及论文、专利、项目和规则模拟投资输入。热点名不得等于技术点
名称。情感表示当前选择性报道的语调，不表示社会总体态度。

### 50.2 `ads_media_technology_coupling`

逻辑主键为`coupling_id`，共28行。字段包含`media_attention_score`、`technology_output_score`、
`project_activity_score`、`investment_activity_score`、`policy_relevance_score`、
`technology_development_score`、`coupling_score`、`coupling_level`和`analysis_summary`。投资输入明确为
规则模拟，政策输入明确为`DEEPSEEK_ESTIMATED_NO_POLICY_FACT`。

### 50.3 `ads_media_focus_assessment`

逻辑主键为`insight_release_id`，共1行。保存22个热点、正中负数量和占比、文章数加权总体情感分、
媒体—技术边文章数加权总体耦合分和摘要。当前总体情感57.86分（POSITIVE），正向占95.45%、中性0%、
负向4.55%；总体耦合67.67分（MEDIUM）。所有分值均是有限样本混合估算，不是统计相关或因果事实。

## 51. 热点热度、月度增长与字段注释（8.7.0）

`ads_media_hotspot.heat_value`固定等于同一发布内该热点的去重`article_count`，并保存样本内排名、等级和
`DISTINCT_ARTICLE_COUNT_IN_RELEASE`口径。该热度只比较当前54篇选择性样本，不代表全网传播量、阅读量
或搜索热度。

新增`ads_media_hotspot_monthly`，逻辑主键为`insight_release_id, hotspot_id, statistics_month`。字段
`new_article_count`为当月新增去重新闻数，`previous_cumulative_article_count`为截止上月末累计数，
`monthly_growth_rate`按二者相除。按当前产品口径，首月没有历史基数且有新增新闻时统一写1.0并标记
`INITIAL_100_PERCENT`；禁止填无穷大。

`media_focus_ads_v3_20261103`发布22条热点和40条热点月度记录。全部8张`ads_media%`表的208个字段均已
写入中文Column Comment；可执行维护入口为：

```bash
.venv/bin/python -m app.media_focus.comments
```

## 52. 热点热度回填与首月增长口径修正（8.8.0）

历史`media_focus_ads_v2_20261103`行早于热度字段创建，因此曾出现`heat_value=NULL`。8.8.0按已有
`article_count`回填历史热度；当前v2、v3、v4共66条热点记录均满足`heat_value=article_count>=1`。

增长率字段分为：月度明细使用`ads_media_hotspot_monthly.monthly_growth_rate`，热点当前展示使用
`ads_media_hotspot.latest_month_growth_rate`。上月累计为0且本月有新增时两者统一为1.0（100%）；
其他月份仍按`new_article_count / previous_cumulative_article_count`计算。

## 53. 媒体—技术年度趋势与滞后相关（8.9.0）

本组表消费`media_focus_trend_dws_v1_20261103`，ADS发布ID为
`media_focus_trend_ads_v1_20261103`。全部表和字段均有中文Comment。

### 53.1 `ads_media_technology_article_sentiment`

逐条保存28条人工审核新闻—技术关系的模型情感分、标签、理由、原始标题和URL及完整模型血缘。年度
正中负分布和平均分必须从该表或年度宽表读取，不得复用热点层的综合情感分冒充逐新闻事实。

### 53.2 `ads_media_technology_policy_keyword_evidence`

保存18条出版物—政策词类别证据，涉及5篇新闻、11篇论文和1件专利去重出版物。每行保留原始标题、
摘要、URL、来源表、命中词JSON和次数，可从年度指标下钻到原文。论文和专利仅扫描MVP代表性成果表；
频次不是政策文件数或政策影响分。

### 53.3 `ads_media_technology_yearly_trend`

逻辑主键为`trend_release_id, technology_node_id, statistics_year`，1965—2026共1,364行。当前合计
媒体提及28、论文237、专利5,383、项目892、投融资0、政策词19次。投融资0固定带
`NOT_AVAILABLE_ZERO_PER_REQUIREMENT`，表示缺数据按需求置零，不表示已确认没有事件。

### 53.4 `ads_media_technology_lag_correlation`

保存媒体提及数与论文、专利、项目、政策词、投融资的-3至+3年Pearson相关，共770行；341行可计算，
429行因序列无方差为NULL。正滞后表示对比指标晚于媒体指标。它支持多序列探索，不支持Granger或因果
推断。

## 54. 最新新闻突发事件候选与简报草稿（9.2.0）

新增`ads_media_breaking_event_candidate`，逻辑主键为`release_id, candidate_id`。当前发布从固定的
`dwd_media_article` Snapshot按`published_at DESC, article_id DESC`稳定选择最新5篇去重文章；每篇只
保留一行，不复用文章—目标关系表，避免多实体文章重复展示。选择口径固定为
`LATEST_N_BY_PUBLISHED_AT`，候选状态固定为`PRELIMINARY_REVIEW_REQUIRED`。

模型输入仅包含来源标题、已有摘要、来源类型及已审核文章—实体关系。输出包括候选触发原因、触发因素、
关键事实、涉及科技/机构/人才/项目、传播渠道建议、紧迫度和中文应对简报草稿，并保存模型、Prompt、
逐条输入Hash、DWD Snapshot和DWS release血缘。模型不得生成输入中不存在的实体ID；无摘要时不得补写
研究方法、结果或影响范围。

当前54篇新闻是选择性样本，不是持续全网监测。因此`short_term_growth_status`、
`sentiment_anomaly_status`固定为`INSUFFICIENT_BASELINE`，`source_concentration_status`固定为
`INSUFFICIENT_EVENT_CLUSTER_BASELINE`。本表只能驱动“突发事件候选”人工复核和简报编辑，不能宣称
已检测到真实舆情爆发。加入监控、订阅人、通知渠道和处置状态属于下游应用控制库，不写入ADS事实表。

执行入口：

```bash
./scripts/publish_media_breaking_events_v1.sh
```

## 55. 媒体—技术统计耦合分析（9.5.0）

本组表消费`media_focus_coupling_dws_v1_20261104`，ADS发布ID为
`media_focus_coupling_ads_v1_20261104`。统计范围固定为`MEDIA_MENTION_COUNT`、`PAPER_COUNT`、
`PATENT_COUNT`和`PROJECT_COUNT`。投融资与政策指标不进入本组任何表，不发布占位行或不可用标注。

### 55.1 `ads_media_technology_analysis_run`

逻辑主键为`analysis_run_id`。保存输入序列release、22个主体、1965—2026窗口、年度频率、四项指标、
最大滞后3年、滚动窗口10年、显著性阈值0.05、主体内Benjamini-Hochberg修正、输入哈希和算法版本。
`eligible_observation_statuses_json`固定只包含`OBSERVED`和`OBSERVED_ZERO`。

### 55.2 `ads_media_technology_pairwise_correlation`

逻辑主键为`correlation_id`。四项指标产生`C(4,2)=6`组唯一指标对，每组计算`lag=-3…+3`，共
`22 × 6 × 7 = 924`行。定义固定为：

```text
r(lag) = PearsonCorr(x[t], y[t + lag])
```

`lag>0`表示`metric_x`在时间上领先`metric_y`，`lag<0`表示`metric_y`领先，`lag=0`为同期相关。
同期`lag=0`的6组结果组成4×4对称相关矩阵，对角线由前端固定显示1，不额外写自相关行。P值使用
Pearson t统计量双侧检验；`adjusted_p_value`在同一技术全部42条滞后结果内使用BH修正。
`is_best_lag`按绝对相关系数最大、绝对滞后最小、滞后值最小稳定破平，仅表示探索性下钻入口，不证明
领先机制。无方差时系数与P值保持NULL并标记`INSUFFICIENT_VARIANCE`。

### 55.3 `ads_media_technology_granger_causality`

只对媒体与论文、专利、项目三组分别计算双向预测关系，不计算技术指标之间的Granger，也不包含投资或
政策。每个方向分别测试1、2、3阶，共`22 × 3 × 2 × 3 = 396`行。两个序列先执行一阶差分，再建立：

```text
受限模型:   Δy[t] = c + Σ(a_i × Δy[t-i]) + ε[t]
非受限模型: Δy[t] = c + Σ(a_i × Δy[t-i]) + Σ(b_i × Δx[t-i]) + ε[t]
```

使用嵌套OLS残差平方和F检验；有效回归样本少于30、设计矩阵奇异或残差方差不足时不输出统计量。P值在
同一技术全部18个方向—阶数组合内做BH修正，只有`adjusted_p_value<0.05`才标记
`is_predictively_significant=true`。`FIRST_DIFFERENCE_APPLIED`只说明执行了固定差分，不冒充ADF平稳性
检验；结果必须称为“Granger预测关联”，不得称为真实因果。

### 55.4 `ads_media_technology_rolling_coupling`

媒体分别与论文、专利、项目使用10年右对齐滚动窗口，窗口结束年为热力图X轴，对比指标为Y轴，共
`22 × 3 × (62-10+1) = 3,498`行。定义为：

```text
signed_correlation = PearsonCorr(media_window, comparison_window)
coupling_strength  = abs(signed_correlation)
LOW                = strength < 0.4
MEDIUM             = 0.4 <= strength < 0.7
HIGH               = strength >= 0.7
```

窗口任一序列无方差时强度保持NULL，等级为`NOT_CALCULABLE`。该热力图是滚动统计相关，不复用8.6.0
静态混合估算`coupling_score`。

### 55.5 `ads_media_technology_mechanism_draft`

逻辑主键为`draft_id`，按22项技术×3项技术指标发布66条草稿。确定性模板引用最佳滞后相关ID和通过BH
修正的Granger结果ID，分开保存观察模式、可能机制文字、替代解释、局限和固定非因果声明。全部草稿
固定`review_status='PENDING_REVIEW'`，不得未经专家审核直接转成事实结论。

### 55.6 数据准入与发布校验

1. 只读取`observation_status IN ('OBSERVED','OBSERVED_ZERO')`的时间序列行。
2. 指标集合必须精确等于媒体、论文、专利、项目四项；投资和政策编码出现即终止发布。
3. 未知、缺失和未覆盖值不得改写为`OBSERVED_ZERO`。
4. 所有不可计算结果保留NULL及明确状态，不填0。
5. 当前媒体只有28次选择性样本提及，全部结果均为探索性MVP结果，不代表全网媒体，也不证明因果。

执行命令：

```bash
.venv/bin/python -m app.media_focus.cli --config config/media_focus_mvp_v1.json \
  --generate-coupling-analysis
.venv/bin/python -m app.media_focus.cli --config config/media_focus_mvp_v1.json \
  --publish-coupling-analysis
```

## 56. 媒体网络交互服务（9.6.0）

本组能力继续消费`media_focus_ads_v1_20261103`的54篇选择性样本、36个媒体来源和73条文章—目标关系，
不修改DWD/DWS。当前产品口径允许以目标的去重媒体来源数作为“影响力”代理，但必须通过
`influence_definition='MEDIA_SOURCE_COUNT_PROXY'`保留口径，不得解释为受众规模、转载量或社会影响。

### 56.1 `ads_media_target_network_metric`

逻辑主键为`release_id, target_type, target_id`，当前42行，对应22项技术、5家机构和15名人才。
`media_source_count`为报道目标的去重来源数，`article_count`为去重新闻数，`influence_value`固定等于
`media_source_count`。前端使用`influence_value`控制科技实体/技术主题节点大小；时间范围变化时必须从
`ads_media_article_relation`按日期重新聚合，不能复用全窗口值。

### 56.2 `ads_media_article_keyword`

逻辑主键为`release_id, article_id, keyword`。使用固定`media_keyword_frequency_v1`规则，对每篇文章的
标题与可用摘要进行大小写归一、分词、停用词过滤和词频统计，每篇最多保留64个关键词。字段分别保存
总频次、标题频次、摘要频次、文本输入Hash及提取版本。媒体节点词云按`media_source_id`聚合；目标节点
词云先从`ads_media_article_relation`按目标取去重`article_id`，再聚合关键词，避免一篇文章因多条关系
重复计数。

### 56.3 固定官网刊登路径

`ads_media_article_relation.propagation_path_type`固定为`MEDIA_WEBSITE_PUBLICATION`，中文标签
`propagation_path_label`固定为“媒体官网刊登”。可展示的证据路径为：

```text
媒体来源 → 官网刊登文章 → 技术/机构/人才目标
```

该字段只表示文章在已核验来源网站刊登，不证明媒体间转载、引用、首发或信息扩散顺序；当前不得生成
媒体A→媒体B的有向传播边。

### 56.4 `ads_media_target_region`

逻辑主键为`release_id, target_type, target_id, location_level, location_id`，只支持目标地域，不保存或
过滤媒体来源地域。机构目标使用自身地域，人才目标使用当前机构地域，技术目标使用关联机构地域；每行
保存地域层级、平台位置ID、中英文名称、国家代码、支持机构数及派生依据。地域筛选应使用`EXISTS`，
避免一个目标的多个地域行放大媒体边数量。

### 56.5 情感过滤边界

情感筛选开启后，网络强制限定`target_type='TECHNOLOGY'`，使用
`ads_media_technology_article_sentiment.relation_id + article_id + technology_node_id`连接
`ads_media_article_relation`。当前28条新闻—技术关系均有情感结果；机构和人才关系不参与情感筛选，
不得把缺失情感当作中性。

## 57. 媒体智能推荐与证据溯源（9.7.0）

本组表只消费`media_focus_ads_v1_20261103`的既有文章—目标关系，不扩写外部事实。首版固定发布4张
演示卡片：材料科学实验自主系统、聚变反应堆设计与工程、Harvard Medical School和Hong-Cai Zhou，
覆盖2项技术、1家机构和1名人物。选择是产品演示白名单，不表示全量候选中的全局Top 4。

### 57.1 `ads_media_recommendation_card`

逻辑主键为`release_id, recommendation_id`。每张卡片保存推荐类型、实体ID与名称、实体和全部来源证据
的加权语义相似度、主要理由、代表报道数、完整证据数、三元组数及证据时间范围。卡片相似度按逐篇
DeepSeek语义相似度以既有`relation_confidence`加权平均；该分数只衡量实体和当前证据文本的一致程度，
不是事实概率、实体间相似度、全网热度或影响力。

### 57.2 `ads_media_recommendation_evidence`

逻辑主键为`release_id, recommendation_id, evidence_id`。一行保存卡片的一篇源文档，包含原始标题、
来源、发布日期、原文URL、关系证据、实体—证据相似度、理由和代表性报道排名。点击“证据”必须读取
本表全部记录，而不是只展示`representative_rank`非空的首屏Top 3。`relation_confidence`与
`evidence_similarity_score`分别表达上游关系审核置信度和本次语义贴合度，禁止混为一个指标。

### 57.3 `ads_media_recommendation_fact_triple`

逻辑主键为`release_id, recommendation_id, triple_id`。每条主体—谓语—客体都绑定`evidence_id`和
`article_id`，并保存输入中逐字出现的最短支撑片段。状态固定为`MODEL_EXTRACTED`，表示受约束抽取但
未经独立事实核验；前端必须同时提供原文跳转，不得把模型置信度显示为事实概率。

### 57.4 发布与使用边界

- 机构`PUBLISHED_BY`关系只证明机构官网发布文章，不自动证明机构执行研究或受到影响。
- 人物`SOURCE_CONFIRMED`关系只证明来源明确关联该人物，不自动认定其为意见领袖。
- 当前54篇选择性样本不支持全网召回率、媒体共识或真实传播影响判断。
- 推荐理由和三元组只允许使用标题、现有摘要与关系证据；模型返回未知实体/关系ID或非原文证据片段时
  整批生成失败。

执行命令：

```bash
./scripts/publish_media_smart_recommendations_v1.sh
```

## 58. 多实体多字段全文检索（9.26.1）

本版本不新增名称拼接列，也不改写现有名称字段。Doris `SEARCH`的每一个参与字段都必须拥有可执行的倒排
索引，因此在复用既有索引的基础上，为以下10个缺失字段补充ICU多语言全文索引：

多字段`SEARCH`的SQL语法和查询示例见
[`docs/ADS_MULTIFIELD_SEARCH_FRONTEND_GUIDE.md`](docs/ADS_MULTIFIELD_SEARCH_FRONTEND_GUIDE.md)。

| 表 | `SEARCH`字段集合 | 本版本新增索引字段 |
| --- | --- | --- |
| `ads_talent_profile` | `name/name_zh/name_en/name_zh_candidate/name_original/name_pinyin` | `name/name_original` |
| `ads_technology_profile` | `technology_name_original/technology_name_en/technology_name_zh` | `technology_name_original` |
| `ads_institution_profile` | `name/name_zh/name_en/name_original` | `name_original` |
| `ads_project_profile` | `name/name_zh/name_en/name_original` | `name_zh/name_en/name_original` |
| `ads_technology_hotspot_signal` | `signal_text_original/signal_text_en/signal_text_zh` | 三个字段全部新增 |

前台多字段查询使用参数化调用：

```sql
SELECT *
FROM ads_talent_profile
WHERE SEARCH(:escaped_query, :options_json)
LIMIT :limit;
```

`options_json`由服务端按实体固定生成，例如人才查询为：

```json
{"fields":["name","name_zh","name_en","name_zh_candidate","name_original","name_pinyin"],"type":"best_fields","default_operator":"and"}
```

用户输入必须按SEARCH查询语法转义并通过绑定参数传入，不得直接拼接SQL。`name_aliases`、
`name_search_variants`、机构`acronyms/aliases`等数组字段不加入全文索引，继续使用数组成员精确过滤；如需
对数组内容做模糊全文检索，应另行设计规范化关系表，不在画像主表中增加不可审计的拼接文本。

历史rowset索引回填脚本：

```bash
./scripts/compose.sh exec -T doris-fe bash -lc \
  'MYSQL_PWD="$DORIS_PASSWORD" mysql --protocol=TCP -h127.0.0.1 -P9030 -uroot --show-warnings' \
  < sql/doris/ads_schema_9_26_1_multifield_search_indexes.sql
```

## 59. 技术阶段典型任务与代表性案例内容（9.27.0）

本版本直接扩展`ads_technology_stage_assessment`，不创建平行阶段表，也不改变八阶段判定。固定
`model_version='technology_insight_mvp_v1'`的每条研判使用技术画像、当前阶段说明、堵点、风险、建议和最多
5条`ads_technology_assessment_evidence`作为DeepSeek输入，生成3至5项中文典型任务和一段代表性案例示意。

`typical_task_content`使用编号纯文本，供前端直接分行展示；`representative_case_content`只表达受约束的案例
示意。模型引用论文、专利或科研项目证据时，`content_evidence.case_nature='EVIDENCE_DERIVED'`并保存输入内
证据ID；无合适证据时为`LLM_DEMONSTRATION`。两种性质均不等于产品落地或商业成功事实。

阶段判定的`model_version/prompt_version/parameter_hash`继续承担阶段研判血缘，新增的
`content_provider/content_model_version/content_prompt_version/content_input_hash/content_generated_at`
独立承担展示内容血缘，不得相互覆盖。首版内容状态固定为：

```text
generated_content_type = LLM_DEMONSTRATION
content_review_status  = MODEL_GENERATED_NOT_HUMAN_VERIFIED
```

前端可以将`representative_case_content`放入需求中的“成功案例”区域，但标题或紧邻位置必须显示“AI生成案例
示意，未经人工事实核验”。不得仅凭该字段创建企业、产品、客户、收入、融资、监管批准、市场采用或商业
成功断言。真实成功案例仍需接入产品、试点、部署和市场来源事实后另行发布。

完整执行命令及恢复、缓存和验收方法见
[`docs/technology_stage_content_v1.md`](docs/technology_stage_content_v1.md)：

```bash
./scripts/publish_technology_stage_content_v1.sh
```
