# Cloudflare Pages + R2 配置说明

1. 在 R2 的 `text` 桶中，为桶绑定一个公开自定义域名，例如 `download.example.com`（R2 → Settings → Custom Domains）。R2 默认的 `r2.dev` 域名也可用，但不建议用于生产环境。
2. 打开 `index.html`，将 `R2_BASE_URL` 改为该域名（不要末尾 `/`）。
3. 在 `systems` 的 `files` 数组中填写实际文件名。文件在 R2 中的路径应为：`Proxy/文件名` 或 `IIEAO/文件名`，大小写必须一致。
4. 将此文件夹推送到 GitHub，在 Cloudflare Pages 创建项目并连接仓库：Framework preset 选 **None**，Build command 留空，输出目录填 `/`（或留空）。
5. Pages 部署完成后，在 Pages 的 Custom domains 绑定你的访问域名即可。

R2 公网域名只负责下载文件，Pages 负责展示页面。若桶必须保持私有，则不能直接用静态 HTML 下载，需要增加 Cloudflare Worker 生成授权 URL；本页面按公开下载桶方案制作。
