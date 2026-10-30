# Parallel Transfer v2 — 继续升级方案

> 基于 `@memory` (`project_croc_parallel_upgrade.md`) 的后续执行文档。

## 当前状态（来自 memory）
- 版本：v11.6.0 (`05f75b6d`)
- 远程：`origin` = `Joshua-Wang223/Croc`；`compare` = `schollz/croc`
- 已提交 4 个 PR 到上游 `compare/main`：
  - #1399 `feat/parallel-transfer-core`
  - #1400 `feat/resume-journal`
  - #1401 `feat/cli-docs-tests`
  - #1402 `feat/ci-release-infra`
- 上游无 PR 模板，已使用标准开源描述提交。

## 继续升级方案（Parallel v2 后续）

### 1. 功能扩展方向
- **数据面优化**：`parallel_perf.go`、`transferperf/controller.go` 进一步调优；补充 `parallel_protocol_test.go` 覆盖更多边界。
- **恢复能力强化**：`resume/journal.go` + `bitmap.go` 增加断点续传的增量同步；`progressive_hash.go` 验证完整性。
- **CLI / 文档**：`cli.go` 增加并行传输参数（`--parallel`、`--resume`）；更新 `PARALLEL_TRANSFERS.md` 与 `NATIVE_BROWSER_TRANSFERS.md`。
- **CI / 发布**：`.github/workflows/release.yml` 完善矩阵签名；`version/version.go` 同步下一个稳定版标签。

### 2. 分支与提交策略（基于 memory 规范）
- 按功能主题创建独立分支（不要直接在 `main` 上开发大功能）
- 示例：
  - `feat/parallel-perf-tuning`
  - `feat/resume-incremental-sync`
  - `feat/cli-parallel-flags`
- 提交信息使用 conventional commits：`feat:`, `fix:`, `docs:`, `ci:`
- 推送到 `origin`（fork），再通过 `gh pr create --repo schollz/croc --base main --head Joshua-Wang223:feat/xxx` 提交上游 PR

### 3. 当前立即执行
```bash
git checkout -b feat/parallel-v2-follow-up
git add .
git commit -m "feat: continue Parallel v2 upgrade scheme doc and tracking"
git push origin main
```

### 4. 检查点
- [ ] `compare/main` 新 PR 是否被 review
- [ ] `parallel_transfer_test.go` 覆盖率
- [ ] `resume/` 测试通过
- [ ] 上游无 PR 模板，继续用标准描述提交
