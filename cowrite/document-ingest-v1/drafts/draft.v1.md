# document_ingest_v1 技能说明

## 定位
将外部文档导入 agent workspace，生成首版可编辑 Markdown 工作稿。

## 适用场景
- 上传文件（Word、PDF、PPT、Markdown 等）导入 workspace
- 外部文件链接（URL、文件路径）导入 workspace
- 多文件汇总：1~N 个源文档聚合为一份 Markdown 初稿
- 为后续版本改写（rewrite）建立标准工作目录

**不适用：** 对已有 draft.vN.md 做增量编辑（那是 rewrite 技能的工作）

## 工作目录结构
```
docs/<docId>/
├── source/           # 原始文件（保留来源）
├── drafts/
│   └── draft.v1.md  # 首版可编辑工作稿
└── meta/
    └── state.json    # 文档状态
```

## 输入源类型
1. 上传的文件实体
2. 外部文件系统路径
3. 文件链接（URL、object key、document ID 等）
4. 已有 Markdown 文件
5. 多个文件（汇总整理）

## 处理规则

### Markdown 文件
- 原始文件保留到 source/
- 内容直接作为 draft.v1.md 基础
- 只清理明显的格式问题，不丢失标题、列表、表格、代码块

### Word/PDF/PPT 等非 Markdown 文件
- 原始文件保留到 source/
- 提取内容转为结构化 Markdown
- 注重内容保真，而非视觉还原

### 多文件场景
- 每个源文件都保留到 source/
- 生成一份聚合的 draft.v1.md
- 默认结构：Overview → Key points by source → Consolidated findings → Open questions → Next steps

## docId 生成规则
1. 优先使用调用方指定的 docId
2. 从文件名或任务名派生稳定 slug
3. 必要时加时间戳或唯一后缀避免冲突
4. 必须文件系统安全（小写字母、数字、连字符）

## state.json 必要字段
```json
{
  "docId": "example-doc",
  "mode": "single-file-rewrite | aggregate-summary",
  "sourceType": "upload | path | link | mixed",
  "sourceFiles": ["docs/example-doc/source/original.ext"],
  "currentVersion": 1,
  "currentDraft": "docs/example-doc/drafts/draft.v1.md",
  "status": "ready_for_edit"
}
```

## 依赖
仅需系统命令：`cp`, `mkdir`, `python3`

## 注意事项
- 不覆盖已存在的 draft.v1.md（除非用户明确要求重生成）
- 提取不完整时需在草稿中说明
- 不编造缺失内容
- 源文件保留与草稿生成必须分开处理
