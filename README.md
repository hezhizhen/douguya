# 道具屋 douguya

一间收藏好用 Web 工具的小店。把别人做好的工具网站收在一起，在需要的时候顺手找到。

- **douguya**：别人做好的 Web 工具。
- [links](https://github.com/hezhizhen/links)：值得保存、阅读的内容。
- [tools-in-html](https://github.com/hezhizhen/tools-in-html)：自己制作的单文件 HTML 工具。

## 使用

直接用浏览器打开 `index.html`，无需安装依赖、构建或启动后端。也可以在仓库目录运行：

```sh
python3 -m http.server 8000
```

然后访问 <http://localhost:8000>。

- 按分类筛选；分类及数量从工具清单自动生成。
- 搜索名称、说明、分类、标签或域名；支持空格分隔的多个关键词，忽略英文大小写。
- 按 `/` 聚焦搜索，按 `Escape` 清空搜索。
- 点星标加入「我的常用」，可与分类、搜索一起使用。
- 默认按名称 A–Z 排序（忽略英文大小写），也可切换为收藏顺序。
- 适配手机、平板和桌面；支持键盘操作、屏幕阅读器和减少动态效果偏好。

常用标记保存在当前浏览器的 `localStorage`，不上传、不跨设备同步。文件预览、localhost 和 GitHub Pages 属于不同地址，标记不会自动互通；清理网站数据会清除标记。浏览器禁止存储时仍可使用，页面会提示标记只能临时保留。

## 维护工具清单

编辑 `index.html` 底部的 `tools` 数组即可。默认展示按名称排序；数组顺序对应「收藏顺序」，新增分类不需要改其他代码。

```js
{
  id: "example-tool",
  name: "Example Tool",
  url: "https://example.com/",
  category: "开发调试",
  description: "用一句话说明这件工具适合做什么。",
  tags: ["格式化", "调试"],
  color: "#e7edf7",
  ink: "#5b7ab9",
  // 可选：网站实际使用的图标地址。
  icon: "https://example.com/favicon.ico"
}
```

- `id` 必须唯一；编辑名称或网址时保留它，避免丢失已有常用标记。
- `url` 使用完整的 HTTPS 地址。
- `color` 和 `ink` 是图标不可用时，字母占位的背景色与文字色。
- `icon` 未设置时，尝试工具网址所在目录下的 `favicon.ico`；加载失败自动保留字母占位。
- favicon 直接请求对应站点，不使用第三方图标聚合服务。远程图标不可用不影响搜索和筛选。

工具清单按个人需要持续维护。工具功能与可用性以对应网站为准。

## 发布到 GitHub Pages

本项目使用一个 `index.html`，CSS、JavaScript 和工具数据均内嵌，不需要 Actions 构建配置。

1. 将 `index.html` 和 README 提交并推送到本仓库的 `master` 分支。
2. 打开仓库 **Settings → Pages**。
3. 在 **Build and deployment → Source** 选择 **Deploy from a branch**。
4. 选择 **master** 分支和 **/ (root)**，点击 **Save**。
5. 等待 Pages 部署完成，再访问 <https://hezhizhen.github.io/douguya/>。

以上地址是默认发布地址；未完成上述设置前不代表网站已上线。之后推送到 `master` 会触发更新。若更改默认分支，也要同步调整 Pages 发布分支。

参考：[GitHub Pages 发布源配置](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)。

## 文件

```text
index.html   页面、样式、交互和工具清单
README.md    使用与维护说明
LICENSE      MIT 许可证
```

页面不加载外部字体、脚本或样式，不接入统计服务；外部请求仅来自工具图标，以及主动点击后打开的工具站点。

## License

[MIT](LICENSE)
