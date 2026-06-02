# FreshRSS (Custom Fork)

基于 [FreshRSS/FreshRSS](https://github.com/FreshRSS/FreshRSS) edge 分支的自定义 fork。

## 定制内容

### 1. FeedDAO 批量查询优化 (`app/Models/FeedDAO.php`)
- 新增 `listFeedsByIds()` 方法，通过指定 ID 批量获取 feed，避免加载全部分类

### 2. GReader API 增强 (`p/api/greader.php`)
- **智能 feed 获取**：优先使用 `listFeedsByIds` 精准查询，降级为全分类加载
- **excludeContent 参数**：API 响应中排除正文内容（节省带宽）
- **pub_ot / pub_nt 参数**：按出版日期范围过滤
- **显式 tags 返回**：响应中包含 tags 字段

## 同步上游

```bash
git fetch upstream edge
git merge upstream/edge
# 如有冲突，解决后 commit
git push origin main
```

## Docker 镜像

镜像自动推送到 `aloklok/freshrss-custom`：
- `aloklok/freshrss-custom:latest`
- `aloklok/freshrss-custom:<sha>`
- `aloklok/freshrss-custom:build-<timestamp>`

触发构建：修改 `p/api/greader.php` 或 `app/Models/FeedDAO.php` 后推送到 main 分支，或在 GitHub Actions 中手动触发。
