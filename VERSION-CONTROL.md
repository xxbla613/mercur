# 版本控制说明 / Version Control Guide

## 仓库信息 / Repository Information

- **项目名称**: Mercur.js Marketplace Platform
- **本地路径**: `\\wsl.localhost\Ubuntu\home\woshi123\mercur`
- **远程仓库 (Origin)**: https://github.com/xxbla613/mercur.git
- **上游仓库 (Upstream)**: https://github.com/mercurjs/mercur.git
- **Git 用户**: xxbla613
- **Git 邮箱**: xxbla613@users.noreply.github.com

## 已创建的版本 / Created Versions

### orange
- **创建时间**: 2025-01-21
- **Commit**: `a64621ceb`
- **描述**: 初始基线版本，包含项目初始配置
- **变更内容**: 修改了 `bun.lock` 和 `package.json`
- **标签名**: `orange`

---

## 分支管理 / Branch Management

> **AI 提示**: 当用户需要上传分支时，请在下方记录分支信息，方便后续回滚操作。

### 分支记录格式

```
### 分支名称
- **创建时间**: YYYY-MM-DD
- **基于版本**: 基础版本/标签
- **功能描述**: 该分支的功能说明
- **状态**: [开发中 / 已合并 / 已废弃]
- **相关 Commit**: 主要 commit hash
```

---

## 当前活跃分支 / Active Branches

### main
- **状态**: 主分支
- **最新 Commit**: `91905c194` - "docs: add VERSION-CONTROL.md for tracking versions and branches"
- **描述**: 稳定的主分支，所有功能分支最终合并到此

### feat/pending-changes-filter
- **创建时间**: 2025-01-21
- **基于版本**: main (`91905c194`)
- **功能描述**: 在管理员产品列表页面添加"待审核变更"筛选功能，让管理员能够快速筛选出有待审核 ProductChange 的产品
- **状态**: 开发中
- **修改文件**:
  - `packages/core/src/api/admin/products/validators.ts` - 添加 `has_pending_changes` 查询参数
  - `packages/core/src/api/admin/products/route.ts` - 添加筛选逻辑
  - `packages/admin/src/pages/products/product-list/components/product-list-table/use-product-table-filters.tsx` - 添加前端筛选器选项
- **技术说明**: ProductChange 是独立于 Product 的实体，有自己的状态（PENDING/CONFIRMED/DECLINED/CANCELED）。当供应商修改已发布产品时，会创建一个 PENDING 状态的 ProductChange，需要管理员审核。

---

## 常用操作 / Common Operations

### 创建新分支
```bash
wsl git checkout -b feat/feature-name
```

### 推送分支到远程
```bash
wsl git push origin branch-name
```

### 推送带 token
```bash
wsl git push https://your-token@github.com/xxbla613/mercur.git branch-name
```

### 创建新版本标签
```bash
wsl git tag -a tag-name -m "版本描述"
wsl git push origin tag-name
```

### 切换到某个版本
```bash
wsl git checkout tag-name
wsl git checkout main
```

### 同步上游更新
```bash
wsl git fetch upstream
wsl git checkout main
wsl git merge upstream/main
wsl git push origin main
```

### 回滚操作
```bash
wsl git reset --soft commit-hash
wsl git reset --hard commit-hash
wsl git reset --hard tag-name
```

---

## 项目规范 / Project Conventions

详细规范请参考 [CLAUDE.md](./CLAUDE.md)

### 分支命名规范
- `feat/feature` - 新功能
- `fix/bug` - Bug 修复
- `docs/topic` - 文档更新
- `chore/task` - 日常任务、构建配置等

### Commit 规范
- `feat(scope):` - 新功能
- `fix(scope):` - Bug 修复
- `docs:` - 文档更新
- `chore:` - 构建、配置等
- 破坏性更新使用 `!`，例如: `feat(auth)!:`

### 注意事项
- ❌ 不要直接推送到 `main` 分支（除非明确需要）
- ❌ 不要在 commit 或 PR 中提及 AI 工具
- ✅ 总是使用 `bun`（不用 npm, yarn, pnpm）
- ✅ 确保 `bun run build` 通过后再推送
- ✅ Bug 修复和新功能必须包含测试

---

## AI 助手指引 / AI Assistant Guide

### 读取项目规范
在开始任何开发工作前，请先阅读:
1. **[CLAUDE.md](./CLAUDE.md)** - 项目完整开发规范和工作流程
2. **[docs/PRODUCT.md](./docs/PRODUCT.md)** - 产品功能描述
3. **[docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md)** - 系统架构说明
4. **[docs/UI-ARCHITECTURE.md](./docs/UI-ARCHITECTURE.md)** - UI 架构规范

### 创建分支时的工作流程
1. 确认当前在 `main` 分支: `wsl git branch`
2. 拉取最新代码: `wsl git pull origin main`
3. 创建新分支: `wsl git checkout -b type/feature`
4. 开发并提交代码
5. **在本文件中记录分支信息**（填写上方"分支记录格式"）
6. 推送分支: `wsl git push origin branch-name`
7. 更新本文件并提交

### 版本标签管理
当用户要创建新版本时:
1. 确保代码已提交
2. 创建带注释的标签: `wsl git tag -a version-name -m "版本描述"`
3. 推送标签: `wsl git push origin version-name`
4. **在本文件 "已创建的版本" 部分记录新版本信息**
5. 提交本文件的更新

### 推送时使用 Token
如果推送需要身份验证，使用:
```bash
wsl git push https://user-provided-token@github.com/xxbla613/mercur.git branch-or-tag
```

---

## CLAUDE.md 核心要点 / Key Points from CLAUDE.md

### 必读文档
- `docs/PRODUCT.md` - 产品描述
- `docs/ARCHITECTURE.md` - 架构说明
- `docs/UI-ARCHITECTURE.md` - UI 架构

### 构建和运行
```bash
bun install
bun run lint
bun run build
bun run dev
bun run test:integration:tests
```

### 项目结构
- `packages/core` - Medusa.js 插件（核心市场逻辑）
- `packages/cli` - Mercur CLI
- `packages/client` - 类型安全的 API 客户端
- `packages/types` - 共享 TypeScript 类型
- `packages/dashboard-sdk` - Vite 插件（扩展 admin/vendor）
- `packages/dashboard-shared` - 共享仪表板组件
- `packages/admin` - 管理员面板
- `packages/vendor` - 卖家面板
- `apps/api` - Medusa 服务器
- `apps/admin-test` - 管理员应用 (port 7000)
- `apps/vendor` - 卖家应用 (port 7001)

### 编码规则
- **永远不要使用 any**
- 不要生成 AI 风格的注释
- Bug 修复和新功能**必须包含测试**
- 确保 `bun run build` 通过后再完成
- **不要提交**（除非用户明确要求）
- 遵循 Conventional Commits 规范

### 测试 Worktree
当用户要求测试 worktree 时:
```bash
./scripts/dev-worktree.sh worktree-name
```
然后返回这些 URL:
- API: http://localhost:9000
- Admin: http://localhost:7000
- Vendor: http://localhost:7001

---

## 更新日志 / Changelog

### 2025-01-21
- 初始化版本控制文档
- 创建 `orange` 基线版本
- 配置远程仓库（origin 和 upstream）
- 添加 AI 助手指引和 CLAUDE.md 核心要点
