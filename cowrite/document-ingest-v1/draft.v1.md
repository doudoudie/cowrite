# document_ingest_v1 技能总结

**功能：** 将外部文档导入 agent workspace，生成首版可编辑 Markdown 工作稿

## 核心能力

| 能力 | 说明 |
|------|------|
| 单文件导入 | 上传文件、外部路径、文件链接 → workspace |
| 多文件汇总 | 1~N 个源文档 → 一份聚合的 Markdown 初稿 |
| 格式转换 | Word/PDF/PPT/Markdown → 结构化 Markdown 工作稿 |
| 源文件保留 | 原始文件保存在 `source/` 目录 |

## 生成的工作区结构

```
docs/<docId>/
├── source/           # 原始输入文件
├── drafts/
│   └── draft.v1.md   # 首版可编辑工作稿
└── meta/
    └── state.json     # 文档状态
```

## vs cms-cowrite-ingest-document

| 对比 | cms-cowrite-ingest-document | document_ingest_v1 |
|------|----------------------------|---------------------|
| 来源 | 上传/本地路径/URL | 同左 |
| 输出 | draft.v1.md | 同左 |
| 多文件 | 未明确支持 | ✅ 支持聚合汇总 |
| 依赖 | 需 cms-auth-skills | ✅ 无外部依赖（只用 cp/mkdir/python3） |

## 注意

- **不要**用它做增量编辑已有 draft.vN.md，那是 rewrite 技能的工作
- 如果源文件提取不完整，需在草稿中说明
- 不编造缺失内容

## 适用场景

- "帮我把这个文件变成可编辑的 Markdown"
- "把这份 Word/PDF 整理成初稿"
- "把几个文件汇总成一份文档"
