---
name: wiki-manager
description: 管理 AIPM Wiki 知识库的内容全流程:新增文章入库(选目录、套模板、更新索引、关 Issue、commit)和按选题 Issue 批量生成草稿。在本仓库中新增、修改、批量生成内容,或用户提到"入库"、"批量写文章"、"处理选题 Issue"时使用。
---

# AIPM Wiki 内容管理

本仓库是面向 AI 产品经理入门者的中文知识库。所有内容操作遵循本 skill,保证格式统一、索引不遗漏。

## 目录路由表

| 内容类型 | 目录 | 模板 |
|----------|------|------|
| 学习路线文章 | `docs/00-roadmap/` | 无(自由结构) |
| AI 基础知识 | `docs/01-ai-basics/{machine-learning,llm,prompt-engineering}/` | 无(自由结构) |
| PM 技能文章 | `docs/02-pm-skills/{prd-and-design,model-evaluation,data-annotation,cost-and-tech}/` | 无(自由结构) |
| 案例拆解 | `docs/03-case-studies/{chatbot-assistant,aigc,search-and-rec,vertical}/` | `templates/case-study.md` |
| 面试题 | `docs/04-interview/{basics,product-design,case-analysis,behavioral}/` | `templates/interview-question.md` |
| 面经 | `docs/04-interview/experiences/` | `templates/interview-experience.md` |
| 资源推荐 | `docs/05-resources/` 对应文件内追加 | 无 |

## 内容规范

- 文件名:英文小写 + 连字符,如 `what-is-hallucination.md`;标题用中文写在首行 `# 标题`
- 面经文件名:`公司拼音-岗位方向-YYYYMM.md`
- 图片放 `assets/` 下与 docs 镜像的子目录,相对路径引用
- 站内链接一律用相对路径
- 质量标杆:知识文章参考 `docs/01-ai-basics/llm/what-is-rag.md`,面试题参考 `docs/04-interview/basics/rag-vs-finetuning.md`

## 工作流一:内容入库

任何新内容进入仓库时,依次完成(缺一不可):

```
- [ ] 1. 按路由表确定目录,套用对应模板结构
- [ ] 2. 在所属目录的 README.md 索引中追加条目;若选题原本列在"欢迎认领/征集中"清单里,同时从清单中移除
- [ ] 3. 若新增了目录或重要板块,同步更新根 README.md 导航
- [ ] 4. commit,message 格式:`content: 新增 <标题>`(纠错用 `fix:`,结构调整用 `docs:`)
- [ ] 5. 若对应选题 Issue 存在,commit message 末尾加 `(closes #N)`,或推送后用 gh issue close 关闭
```

## 工作流二:按 Issue 批量生成草稿

**节奏规则(硬约束):**

- 一批 3-5 篇,同一板块聚类,不跨板块混批
- 优先级:`04-interview/basics` → 其他面试题分类 → `01-ai-basics` → `02-pm-skills`
- **案例拆解(03-case-studies)不做批量生成**——需要真实产品体验,只收人工投稿

**流程:**

1. 用 `gh issue list --label "good first issue"` 拉取选题,按上述优先级选一批,向用户确认批次内容
2. 草稿直接生成到**最终路径**(含索引更新),但**不 commit**——git 工作区就是暂存区
3. 生成后提醒用户逐篇审校,并说明:过审的按"工作流一"第 4-5 步 commit + 关 Issue;不过审的 `git checkout -- <file>` 丢弃
4. 一批未审完之前,不在此工作区混做其他改动

**草稿质量要求:**

- 严格套用模板结构,不增删一级标题
- 面试题参考答案给思考框架而非标准答案,必含"追问延伸"
- 涉及具体模型、价格、市场格局等时效性内容,先联网核实或写成不依赖时效的表述
- 每篇末尾"相关阅读"链接到站内已有文章(相对路径),不链接不存在的文件

## 边界

- 不直接 push 未经用户审校的生成内容
- 不修改 `templates/` 和 `.github/` 下的文件,除非用户明确要求
