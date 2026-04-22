# Skills 加载与文档同步流程总结

## 问题背景
三个技能（cms-cowrite-ingest-document、cms-cowrite-rewrite-document、cms-docdb_1.0.1）文件存在于 ~/.openclaw/skills/ 但未出现在系统加载列表中。原因：Skill 扫描是 Gateway 启动时加载的，之后新增的技能需要重启才能被扫描到。

## 解决方案
不重启也可以直接使用：通过读取 SKILL.md + 调用脚本的方式工作，效果与系统触发一致。

## 文档同步完整流程（知识库 → Cowrite → GitHub）

### 步骤 1：上传到知识库
调用 upload-content 接口，参数：
- content: 文件内容
- fileName: 文件名
- fileSuffix: md
- folderName: AI生成/Skills

### 步骤 2：同步到 Cowrite
使用 ingest_document.py，关键参数：
- --workspace_root: 工作区根目录
- --doc_id: 文档唯一标识
- --source_mode: path
- --source_value: 源文件路径
- --draft_markdown_file: **重要** - 传入原始内容，跳过 build_base_markdown() 生成 instruction prompt
- --confirm: yes

**注意：** .md 源文件默认会走 build_base_markdown() 生成 instruction prompt，而不是直接用原始内容做草稿。必须用 --draft_markdown_file 传入原始内容。

### 步骤 3：同步到 GitHub
1. 上传文件到 GitHub 仓库
2. 创建新 tag 版本
3. 创建 Release

### 正确的 Raw 文件链接格式
```
https://raw.githubusercontent.com/{owner}/{repo}/{tag}/{path}
```

示例：
```
https://raw.githubusercontent.com/doudoudie/cowrite/v1.0.1/cowrite/document-ingest-v1/draft.v1.md
```

## 技能安装
通过 zip 包安装时：
1. 下载 zip 文件
2. 解压到 ~/.openclaw/skills/ 目录
3. 重启 Gateway 使技能生效（不重启也可直接调用脚本使用）

## 涉及的 API

### 知识库上传
- 地址：https://sg-al-cwork-web.mediportal.com.cn/open-api/document-database/file/uploadContent
- 方式：HTTP POST + appKey 鉴权
- 参数：content, fileName, fileSuffix, folderName

### Cowrite ingest
- 方式：直接调用本地脚本 `ingest_document.py`（不经过 HTTP API）
- 脚本路径：`~/.openclaw/skills/cms-cowrite-ingest-document/scripts/document/ingest_document.py`
- 效果：写入 workspace 目录（`cowrite/<doc_id>/`）
