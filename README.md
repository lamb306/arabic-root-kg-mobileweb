# 阿拉伯语词根知识图谱 - 可公开手机网页版

纯静态单页，无后端，适合部署到 **GitHub Pages / Netlify / Vercel** 等，手机浏览器打开即可使用。

## 文件说明

| 文件 | 说明 |
|------|------|
| `index.html` | 唯一页面：图谱 + 搜索，依赖同目录下的 `data.json` |
| `data.json` | **需自备**：与 Web 版 `my_knowledge_base.json` 格式相同，复制并重命名即可 |

未放置 `data.json` 时，页面会使用内置示例数据展示，并提示访客如何替换为自己的数据。

## 本地预览

用浏览器直接打开 `index.html` 会因跨域限制无法加载 `data.json`。建议用本地服务器（端口号可自行调整，避免与其它项目冲突）：

```bash
cd D:\Arabic_KG\web-public
# 若已安装 Python（如另一个项目已占用 8080，可改用 8081 等任意空闲端口）：
python -m http.server 8081
# 然后访问 http://localhost:8081
```

或把 `my_knowledge_base.json` 复制为 `data.json` 后，用 VS Code 的 Live Server 等工具打开。

## 部署为可公开链接

### 方式一：GitHub Pages

1. 在 GitHub 新建仓库（如 `arabic-root-kg-web`），将本目录推上去：
   ```bash
   cd D:\Arabic_KG\web-public
   copy ..\my_knowledge_base.json data.json
   git init
   git add index.html data.json
   git commit -m "Add public web version"
   git remote add origin https://github.com/你的用户名/arabic-root-kg-web.git
   git push -u origin main
   ```
2. 仓库设置 → Pages → Source 选 **main** 分支、根目录，保存。
3. 几分钟后访问：`https://你的用户名.github.io/arabic-root-kg-web/`。

### 方式二：Netlify

1. 打开 [netlify.com](https://www.netlify.com)，用 GitHub 登录。
2. 新建站点，选择存放 `web-public` 的仓库（或拖拽 `web-public` 文件夹上传）。
3. 发布目录填该目录（如 `web-public`），部署。
4. 获得随机域名，也可绑定自己的域名。

### 方式三：Vercel

1. 打开 [vercel.com](https://vercel.com)，用 GitHub 登录。
2. Import 存放本项目的仓库，根目录改为 `web-public`（或只上传 `web-public` 内容）。
3. 部署后得到 `xxx.vercel.app` 链接。

## 数据更新

- 若数据在仓库里：修改并提交 `data.json` 后重新部署即可。
- 若不想把数据放进仓库：可用 Netlify/Vercel 的构建步骤从别处拉取 JSON，或改用后端接口提供数据（需自行实现）。

## 与其它版本的关系

| 版本 | 说明 |
|------|------|
| **Streamlit (app.py)** | 本地/Cloud 全功能版，导入、删除、总库等。 |
| **Flet (mobile/)** | 手机 App，可打包 APK / IPA。 |
| **本目录 (web-public/)** | 只读展示 + 搜索，纯静态，适合公开分享链接。 |
