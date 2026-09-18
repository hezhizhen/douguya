# 道具屋 douguya

一间收藏好用 Web 工具的小店。把别人做好的工具网站收在一起，在需要的时候顺手找到。

- **douguya**：别人做好的 Web 工具。
- [links](https://github.com/hezhizhen/links)：值得保存、阅读的内容。
- [tools-in-html](https://github.com/hezhizhen/tools-in-html)：自己制作的单文件 HTML 工具。

## 本地预览

无需安装依赖或构建。在仓库目录运行：

```sh
python3 -m http.server 8000
```

然后访问 <http://localhost:8000>。页面会从同目录的 `tools.json` 读取清单，因此需要通过 HTTP 服务预览，不能直接双击打开 HTML。

- 按分类筛选；分类及数量从清单自动生成。
- 搜索名称、说明、分类、标签或域名；支持多个空格分隔的关键词，忽略英文大小写。
- 按 `/` 聚焦搜索，按 `Escape` 清空搜索。
- 点星标加入「我的常用」，可与分类、搜索一起使用。
- 默认按名称 A–Z 排序，也可切换为收藏顺序。
- 适配手机、平板和桌面，支持键盘操作和屏幕阅读器。

常用标记保存在当前浏览器的 `localStorage`，不上传、不跨设备同步。不同网站地址（包括 localhost、GitHub Pages 和旧版文件预览）之间不自动互通，清理网站数据会清除标记。浏览器禁止存储时，页面会提示标记只能临时保留。

## 维护工具清单

**日常新增、修改或删除网站，只需编辑 `tools.json`。** 页面、样式和交互仍放在 `index.html` 中。

清单是一个 JSON 数组，每个网站对应一个对象：

```json
[
  {
    "id": "example-tool",
    "name": "Example Tool",
    "url": "https://example.com/",
    "category": "开发调试",
    "description": "用一句话说明这件工具适合做什么。",
    "tags": ["格式化", "调试"],
    "icon": "https://example.com/favicon.ico"
  }
]
```

- `id`、`name`、`url`、`category`、`description` 为必填文本；`tags` 为字符串数组，可为空数组。
- `id` 必须唯一且保持稳定。修改名称或网址时保留它，同一网站地址下的已有常用标记就仍然有效。
- `url` 和可选的 `icon` 使用完整的 HTTPS 地址。不需要自定义图标时，直接省略 `icon` 字段。
- 分类从清单自动生成；新增分类不用改页面，不能使用保留名称「全部工具」。
- 默认按名称排序；数组顺序对应「收藏顺序」。
- 字母占位的配色由页面样式统一管理，数据里不需要 `color`、`ink` 等样式字段。
- JSON 必须使用双引号，不支持注释或尾随逗号。保存后刷新页面即可查看更新。

页面会校验清单格式、必填字段、重复 ID 和网址。请求或校验失败时显示加载失败提示，可点击「重新加载」重试；具体原因可在浏览器控制台查看。空数组 `[]` 会显示尚未收录工具的提示。

favicon 直接请求对应站点，可能比文字稍晚显示；未设置 `icon` 时，尝试工具网址所在目录下的 `favicon.ico`。图标加载失败保留字母占位，不影响搜索和筛选。工具功能与可用性以对应网站为准。

## 发布到 GitHub Pages

页面和数据都是静态文件，不需要构建或后端服务。

1. 将 `index.html`、`tools.json` 和 README 提交并推送到本仓库的 `master` 分支。
2. 打开仓库 **Settings → Pages**。
3. 在 **Build and deployment → Source** 选择 **Deploy from a branch**。
4. 选择 **master** 分支和 **/ (root)**，点击 **Save**。
5. 等待部署完成，再访问 <https://hezhizhen.github.io/douguya/>。

上述地址是默认发布地址，不表示已经完成部署。之后只修改 `tools.json` 并推送到发布分支，也会更新网站清单。若更改默认分支，应同步调整 Pages 发布分支。

参考：[GitHub Pages 发布源配置](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 文件

```text
index.html   页面、样式和交互
tools.json   网站清单
README.md    使用与维护说明
LICENSE      MIT 许可证
```

页面不加载外部字体、脚本或样式，不接入统计服务；从同站点加载 `tools.json`，远程请求来自工具图标，以及主动点击后打开的工具站点。

## License

[MIT](LICENSE)
