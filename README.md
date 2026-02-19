# 锐科云工具网导航页 - 部署与使用说明

这是一个**本地可视化编辑+GitHub存储配置**的站长工具导航站，无需后端服务、无需开启GitHub Pages，仅通过GitHub存储`config.json`配置文件，`index.html`可部署在任意静态托管平台（如Nginx、云服务器、对象存储等）。

## 一、环境准备
无需复杂依赖，仅需2个基础条件：
1. **GitHub账号**：用于创建仓库和存储`config.json`配置文件；
2. **本地浏览器**（Chrome/Firefox/Edge等）：用于打开`edit.html`编辑配置；
3. （可选）静态托管平台：如Nginx、阿里云OSS、腾讯云COS、虚拟主机等（用于部署`index.html`）。

## 二、核心文件说明
| 文件名          | 作用描述                                                                 | 存储/部署要求               |
|-----------------|--------------------------------------------------------------------------|-----------------------------|
| `index.html`    | 导航展示主页面（用户访问核心页，含搜索、夜间模式、分区展示等功能）         | 部署到任意静态托管平台      |
| `edit.html`     | 本地配置编辑器（仅本地使用，可视化编辑分区、工具项和站点信息）             | 无需上传，本地留存即可      |
| `config.json`   | 导航数据配置文件（由`edit.html`生成，存储站点信息、分区和工具数据）        | 上传到GitHub仓库（核心）    |

## 三、部署步骤（全程可视化，无需技术基础）

### 1. 创建GitHub仓库（仅存`config.json`）
1. 登录GitHub账号，点击右上角「+」→「New repository」；
2. 填写仓库信息：
   - **Repository name**：建议填写 `tool-nav-config`（或自定义名称）；
   - **Description**：可选，填写“导航页配置文件存储”；
   - **Visibility**：选择「Public」（公开仓库，方便获取Raw链接）；
   - 无需勾选其他选项，点击「Create repository」完成创建。


### 1. 或创建Gitee仓库（仅存`config.json`）
1. 登录Gitee账号，点击右上角「+」→「创建仓库」；
2. 填写仓库信息：
  完成创建。




### 2. 本地编辑配置（使用`edit.html`）
1. 下载核心文件：将`index.html`和`edit.html`保存到本地（复制对应代码即可）；
2. 打开编辑器：双击本地`edit.html`文件，用浏览器直接打开（纯本地运行，无需联网）；
3. 编辑导航内容：
切记，生成完后记得发给元宝（或其他ai，元宝最好）看看生成出的有没有问题
   - **站点信息设置**：
     - 头像URL：填写图片链接（建议96x96px，支持Imgur、阿里云OSS等网络图床）；
     - 站点名称：填写导航站名称（如“锐科云工具网”）；
     - 个性签名：填写副标题（如“10+小站长工具，助力站长加油！”）；
   - **分区管理**：
     - 点击「添加分区」，输入分类名称（如“站长工具”“查询工具”）；
     - 支持编辑（「✎」图标）、删除（「×」图标，至少保留1个分区）；
   - **工具项管理**：
     - 点击「添加导航项」，依次填写：
       - 所属分区：下拉选择已创建分区；
       - 工具名称：如“IPv6反解域名获取”；
       - 图标URL：图片链接（建议64x64px）或Font Awesome类名（如`fa-link`）；
       - 链接URL：工具访问地址（如`https://ipv6.638966.online/`）；
       - 描述：工具简要说明（可选）；
4. 导出配置文件：
   - 点击「保存并下载 config.json」；
   - 输入默认密码 `123456`（可在`edit.html`中搜索`const PASSWORD = "123456"`修改）；
   - 下载生成的`config.json`文件，保存到本地。

### 3. 上传`config.json`到GitHub仓库
1. 进入创建的GitHub仓库（如`tool-nav-config`），点击「Add file」→「Upload files」；
2. 拖拽本地`config.json`文件到上传区域；
3. 填写提交说明（如“初始化配置”），点击「Commit changes」完成上传。

### 4. 生成`config.json`的代理访问链接（关键步骤）
最终需得到类似示例的链接：`https://gh-proxy.com/https://github.com/WinVistaTD/TVlive/raw/main/config.json`，步骤如下：
1. 在GitHub仓库主页，找到已上传的`config.json`文件，点击文件名进入详情页；
2. 点击文件详情页右上角的「Raw」按钮（进入原始文件页面）；
3. 复制浏览器地址栏的Raw链接（格式示例：`https://github.com/你的用户名/你的仓库名/raw/main/config.json`）；
4. 在复制的Raw链接前添加代理前缀 `https://gh-proxy.com/`，拼接后即为最终配置链接；
   - 示例拼接过程：
     - 原始Raw链接：`https://github.com/WinVistaTD/TVlive/raw/main/config.json`
     - 添加代理后：`https://gh-proxy.com/https://github.com/WinVistaTD/TVlive/raw/main/config.json`

### 5. 配置`index.html`并部署
1. 用文本编辑器打开本地`index.html`文件；
2. 搜索代码中的`fetch('https://gh-proxy.com/https://github.com/WinVistaTD/TVlive/raw/main/config.json')`；
3. 将括号内的链接替换为步骤4生成的**自定义代理链接**（确保与示例格式一致）；
4. 保存修改后的`index.html`；
5. 将`index.html`部署到你的静态托管平台（如Nginx的`html`目录、虚拟主机根目录、阿里云OSS等）。

## 四、使用说明

### 1. 导航页使用（用户端）
- 访问部署`index.html`的域名（如`https://tools.你的域名.com/`）；
- 核心功能：
  - 搜索工具：输入名称/描述快速筛选；
  - 分区浏览：按分类点击工具卡片跳转访问；
  - 夜间模式：底部右侧按钮切换（偏好本地保存）。

### 2. 配置更新流程（管理员端）
无需重新部署`index.html`，仅需更新GitHub上的`config.json`：
1. 本地打开`edit.html`，点击「📁 导入 config.json」上传GitHub上的最新`config.json`；
2. 修改分区/工具信息；
3. 重新下载`config.json`，替换GitHub仓库中的旧文件；
4. 刷新导航页即可加载最新配置（代理链接无需修改）。

## 五、注意事项
1. **配置链接格式**：必须严格遵循示例格式（`https://gh-proxy.com/` + GitHub Raw链接），否则加载失败；
2. **文件路径**：`config.json`需放在GitHub仓库根目录，否则Raw链接路径变化需重新配置；
3. **图片链接**：头像、工具图标需用支持跨域的网络图床，避免本地图片无法访问；
4. **密码安全**：默认下载密码`123456`，建议修改为自定义密码；
5. **代理替换**：若`gh-proxy.com`失效，可替换为其他GitHub代理（如`https://gh.api.99988866.xyz/`）；
6. **分区限制**：最多支持100个分区，超出部分导出时自动截断。

## 六、常见问题排查
1. **导航页显示“加载配置失败”**：
   - 直接在浏览器打开代理链接，若无法显示内容`config.json`，说明链接无效，重新生成；
   - 检查`config.json`是否在GitHub仓库根目录；
   - 确认`index.html`中的链接与生成的代理链接一致；
2. **配置更新后未生效**：
   - 清除浏览器缓存刷新；
   - 检查GitHub上的`config.json`是否已更新；
3. **工具图标显示异常**：
   - 检查图标URL有效性，SVG图标需支持跨域；
   - 确认`index.html`已引入Font Awesome CDN（代码中已包含）。

## 七、定制化建议
- 样式修改：编辑`index.html`的`style`标签，自定义颜色、字体、卡片大小；
- 功能扩展：在`index.html`中添加工具标签、使用统计等，需同步修改`edit.html`；
- 域名绑定：在静态托管平台配置自定义域名，提升访问体验；
- 移动端适配：优化`index.html`的响应式样式，适配手机访问。

如需进一步定制或解决部署问题，可参考GitHub官方文档或提交issue反馈！
