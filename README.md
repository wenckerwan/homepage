# wencker.top 个人主页

纯静态个人主页，基于 [dmego/home.github.io](https://github.com/dmego/home.github.io) 模板定制。
无需构建，克隆下来直接起个静态服务器就能跑。

## 线上地址

| 域名 | 说明 |
| --- | --- |
| https://wencker.top | 主入口 |
| https://www.wencker.top | 同上 |
| https://wencker.pro | 备用入口（经 Cloudflare） |

实际由自有服务器托管（DNS 直连 / Cloudflare 代理到源站），不走 GitHub Pages。
GitHub Pages 的 `gh-pages` 分支仍保留为一份镜像。

## 目录结构

```
index.html            # 单页入口
assets/
  css/                # 样式（custom.css 为本站定制）
  js/                 # 交互脚本（bing.js 生成壁纸列表）
  img/                # 壁纸与头像（约 6.5 MB）
  fonts/ iconfont/    # 字体与图标
  json/               # 数据文件
404.html              # 404 页
docs/                 # 模板原始文档
```

## 本地预览

```bash
# 任意静态服务器均可
python -m http.server 8080
# 打开 http://localhost:8080
```

## 部署

站点为静态文件，部署即同步目录：

```bash
rsync -avz --delete \
  --exclude .git --exclude .github \
  ./ root@<服务器>:/www/wwwroot/wencker_home/index/
```

`.github/` 必须排除——那是仓库自用的 CI，不能出现在网站根目录下。

## 与模板的差异

- 标题、副标题、社交链接改为本站内容
- 导航「博客」项改为「公众号」
- 背景图与头像替换为自有素材（原始素材见同级 `change/` 目录，未纳入仓库）
- 移除了 CNAME（改为自托管，不再由 GitHub Pages 提供域名服务）

## 分支说明

| 分支 | 用途 |
| --- | --- |
| `main` | 项目源码（当前默认分支） |
| `gh-pages` | GitHub Pages 构建源，站点文件与 `main` 相同（仅 README 不同） |

## 许可证

继承上游模板的 MIT 许可，详见 [LICENSE](LICENSE)。
